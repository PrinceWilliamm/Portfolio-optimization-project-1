# Instruments
These are the chosen ETFs that will represent a portfolio. These exact instruments can be changed easily but it is suggested to keep covariance between them small so that all of the clients eggs aren't in the same basket
	- **VOO
	- VXUS
	- GOVT
	- XAR
	- VNQ (reduced)**
## Code
**The code used to calculate the metrics is provided below
```
	"""
================================================================================
 BLACK-LITTERMAN PORTFOLIO CONSTRUCTION MODEL
================================================================================
Universe:  VOO (US Equity) | VXUS (Intl Equity) | GOVT (US Treasuries)
           XAR (Aerospace & Defense, satellite) | VNQ (REITs, satellite)

Implements, in order, the four steps of the action plan:
    1. Global market-cap ("core") baseline weights                -> w_mkt
    2. Reverse-optimized Implied Equilibrium Returns               -> Pi = delta * Sigma @ w_mkt
    3. User-specified tactical/active views (P, Q) with confidence -> Omega
       (Omega is derived with Idzorek's (2004) intuitive
       0%-100% confidence method - see the "New Method" section of
       the attached paper, "A Step-by-Step Guide to the
       Black-Litterman Model", Section 3.2)
    4. Black-Litterman master equation -> E[R], then a mean-variance
       optimizer with a satellite-sleeve weight cap                -> final weights

All of the values you are likely to want to tweak (baseline weights, views,
risk aversion, tau, satellite cap, data source, etc.) live together in
SECTION 1 below. Nothing below SECTION 2 needs to be touched to run the model
with different numbers.

Requirements:  numpy, pandas, scipy   (pip install numpy pandas scipy)
Optional:      yfinance               (pip install yfinance)  - only needed
               if DATA_SOURCE = "yfinance"
================================================================================
"""

import warnings
import numpy as np
import pandas as pd
from scipy.optimize import minimize, minimize_scalar

pd.set_option("display.float_format", lambda x: f"{x:,.4f}")

# ==============================================================================
# SECTION 1 -- USER-CONFIGURABLE PARAMETERS
# ==============================================================================
# Edit anything in this section. Everything below SECTION 2 reads from here.

# --- Universe -----------------------------------------------------------------
TICKERS = ["VOO", "VXUS", "GOVT", "XAR", "VNQ"]

ASSET_LABELS = {
    "VOO":  "US Equity (VOO)",
    "VXUS": "Intl Equity (VXUS)",
    "GOVT": "US Treasuries (GOVT)",
    "XAR":  "Aerospace & Defense (XAR)",
    "VNQ":  "REITs (VNQ)",
}

# --- STEP 1: Baseline / global market-cap ("core") weights (w_mkt) ------------
# Must sum to 1.0. The satellite names (XAR, VNQ) start at 0% here; any
# allocation they end up with comes entirely from the tactical views in
# STEP 3, subject to the satellite cap in STEP 4.
BASELINE_WEIGHTS = {
    "VOO":  0.55,   # US Equity
    "VXUS": 0.30,   # International Equity
    "GOVT": 0.15,   # Fixed Income (US Treasuries)
    "XAR":  0.00,   # Aerospace & Defense (satellite)
    "VNQ":  0.00,   # REITs (satellite)
}

# --- Risk-aversion coefficient (delta), used in Pi = delta * Sigma @ w_mkt ----
DELTA = 2.5

# --- Historical price data (used to build the covariance matrix, Sigma) ------
DATA_SOURCE = "yfinance"          # "yfinance"  or  "csv"
CSV_PATH = "prices.csv"           # only used if DATA_SOURCE == "csv"
                                   # expected format: one date column + one
                                   # price column per ticker (Yahoo-style export)
LOOKBACK_PERIOD = "5y"            # yfinance period, e.g. "3y", "5y", "10y"
PRICE_INTERVAL = "1mo"            # "1d", "1wk", or "1mo"
_ANNUALIZATION = {"1d": 252, "1wk": 52, "1mo": 12}
ANNUALIZATION_FACTOR = _ANNUALIZATION[PRICE_INTERVAL]

# --- STEP 3: Tactical / active views -------------------------------------------
# Two view types are supported:
#   Absolute: {"type": "absolute", "asset": "TICKER",
#              "return": <annualized excess return>, "confidence": <0-1>}
#   Relative: {"type": "relative", "long": ["A", ...], "short": ["B", ...],
#              "spread": <annualized outperformance>, "confidence": <0-1>}
# "confidence" is the intuitive 0%-100% (0.0-1.0) confidence level; the model
# converts it into Omega for you (Idzorek's method).
VIEWS = [
    {
        "type": "relative",
        "long": ["XAR"],
        "short": ["VOO"],
        "spread": 0.02,       # XAR outperforms VOO by 2.0% annually
        "confidence": 0.60,   # 60% confidence
    },
    {
        "type": "absolute",
        "asset": "VNQ",
        "return": 0.06,       # VNQ absolute excess return of 6.0% annually
        "confidence": 0.40,   # 40% confidence
    },
]

# --- Tau: scales the uncertainty of the equilibrium prior (Pi) ----------------
# Common practitioner range is 0.01-0.05 (Lee, 2000); some authors use 1.0.
TAU = 0.05

# --- STEP 4: Mean-variance optimizer constraints ------------------------------
SATELLITE_TICKERS = ["XAR", "VNQ"]
MAX_SATELLITE_TOTAL_WEIGHT = 0.10   # combined cap on XAR + VNQ
ALLOW_SHORTING = False               # False => long-only (0% <= w <= 100%)
RISK_FREE_RATE = 0.00                # annualized, used only for Sharpe display

# Optional: pin individual tickers to a tighter (min, max) band than the
# global long-only default above -- e.g. to stop the optimizer from swinging
# the core sleeve around too aggressively. Leave empty to use the default
# for every asset.
WEIGHT_BOUNDS_OVERRIDE = {
    # "VOO": (0.20, 0.60),
}

# ==============================================================================
# SECTION 2 -- MODEL IMPLEMENTATION (no need to edit below this line)
# ==============================================================================


# ------------------------------------------------------------------ data -----
def load_price_data() -> pd.DataFrame:
    """Return a DataFrame of adjusted close prices, columns = TICKERS, sorted
    ascending by date, with any non-numeric junk rows/columns removed."""
    if DATA_SOURCE == "yfinance":
        import yfinance as yf

        raw = yf.download(
            TICKERS,
            period=LOOKBACK_PERIOD,
            interval=PRICE_INTERVAL,
            auto_adjust=True,
            progress=False,
        )
        prices = raw["Close"] if isinstance(raw.columns, pd.MultiIndex) else raw
        prices = prices[TICKERS]

    elif DATA_SOURCE == "csv":
        raw = pd.read_csv(CSV_PATH, index_col=0)
        raw.index = pd.to_datetime(raw.index, errors="coerce")
        raw = raw[~raw.index.isna()]
        # Coerce every price column to numeric; this guards against stray
        # header/footer text rows sometimes present in exported CSVs.
        for col in raw.columns:
            raw[col] = pd.to_numeric(raw[col], errors="coerce")
        missing = [t for t in TICKERS if t not in raw.columns]
        if missing:
            raise KeyError(
                f"CSV_PATH is missing columns for: {missing}. "
                f"Available columns: {list(raw.columns)}"
            )
        prices = raw[TICKERS]

    else:
        raise ValueError('DATA_SOURCE must be "yfinance" or "csv"')

    prices = prices.sort_index().dropna(how="any")
    if len(prices) < 12:
        warnings.warn(
            f"Only {len(prices)} usable price observations were loaded; "
            "the covariance matrix may be unreliable."
        )
    return prices


def covariance_matrix(prices: pd.DataFrame) -> pd.DataFrame:
    """Annualized sample covariance matrix of simple returns."""
    returns = prices.pct_change().dropna(how="any")
    sigma = returns.cov() * ANNUALIZATION_FACTOR
    return sigma.loc[TICKERS, TICKERS]


# ------------------------------------------------------------ step 1 & 2 -----
def get_baseline_weight_vector() -> np.ndarray:
    w = np.array([BASELINE_WEIGHTS[t] for t in TICKERS], dtype=float)
    total = w.sum()
    if not np.isclose(total, 1.0, atol=1e-6):
        warnings.warn(
            f"BASELINE_WEIGHTS sums to {total:.4f}, not 1.0 - normalizing."
        )
        w = w / total
    return w


def implied_equilibrium_returns(sigma: np.ndarray, w_mkt: np.ndarray) -> np.ndarray:
    """Pi = delta * Sigma @ w_mkt  (Formula 1)."""
    return DELTA * sigma @ w_mkt


# --------------------------------------------------------------- step 3 -----
def build_view_matrices():
    """Turn the VIEWS list into the P (K x N) matrix and Q (K,) vector.

    Relative-view rows use market-cap weighting within the long/short legs
    (the method Idzorek prefers over simple equal-weighting - see Section
    2.3 / Formula 7 of the attached paper), using BASELINE_WEIGHTS as the
    market-cap proxy.
    """
    n = len(TICKERS)
    idx = {t: i for i, t in enumerate(TICKERS)}
    k = len(VIEWS)
    P = np.zeros((k, n))
    Q = np.zeros(k)
    confidences = np.zeros(k)
    descriptions = []

    for row, view in enumerate(VIEWS):
        confidences[row] = view["confidence"]
        if view["type"] == "absolute":
            P[row, idx[view["asset"]]] = 1.0
            Q[row] = view["return"]
            descriptions.append(
                f'{view["asset"]} = {view["return"]:+.2%} (abs.)'
            )

        elif view["type"] == "relative":
            longs, shorts = view["long"], view["short"]
            long_caps = np.array([BASELINE_WEIGHTS[t] for t in longs])
            short_caps = np.array([BASELINE_WEIGHTS[t] for t in shorts])
            if long_caps.sum() == 0:
                long_caps = np.ones_like(long_caps)  # equal-weight fallback
            if short_caps.sum() == 0:
                short_caps = np.ones_like(short_caps)
            for t, w in zip(longs, long_caps / long_caps.sum()):
                P[row, idx[t]] += w
            for t, w in zip(shorts, short_caps / short_caps.sum()):
                P[row, idx[t]] -= w
            Q[row] = view["spread"]
            descriptions.append(
                f'{"+".join(longs)} outperforms {"+".join(shorts)} '
                f'by {view["spread"]:+.2%}'
            )
        else:
            raise ValueError(f'Unknown view type: {view["type"]!r}')

    return P, Q, confidences, descriptions


# --------------------------------------------------------- Idzorek omega ----
def _single_view_return(p_k, q_k, omega_k, pi, sigma_inv_tau):
    """E[R] from the BL formula using ONE view only (Formula 3 / 12)."""
    omega_inv = 1.0 / omega_k
    A = sigma_inv_tau + omega_inv * np.outer(p_k, p_k)
    b = sigma_inv_tau @ pi + omega_inv * p_k * q_k
    return np.linalg.solve(A, b)


def _weights_from_returns(sigma_inv, exp_returns):
    return (1.0 / DELTA) * (sigma_inv @ exp_returns)


def idzorek_omega(P, Q, confidences, pi, sigma) -> np.ndarray:
    """Derive each view's Omega_kk from its 0-100% user confidence, following
    the 7-step procedure in Section 3.2 ("The New Method") of the attached
    paper. Returns the diagonal Omega matrix (K x K)."""
    sigma_inv = np.linalg.inv(sigma)
    sigma_inv_tau = np.linalg.inv(TAU * sigma)
    w_mkt = get_baseline_weight_vector()
    k = P.shape[0]
    omegas = np.zeros(k)

    for row in range(k):
        p_k, q_k, c_k = P[row], Q[row], confidences[row]

        # Steps 1-2: 100%-confidence combined return & weights for this view
        exp_return_100 = _single_view_return(p_k, q_k, 1e-12, pi, sigma_inv_tau)
        w_100 = _weights_from_returns(sigma_inv, exp_return_100)

        # Step 3: max departure from market-cap weights at 100% confidence
        d_100 = w_100 - w_mkt

        # Step 4-5: scale the departure by the user confidence -> target tilt
        target_w = w_mkt + c_k * d_100

        # Step 6: solve for the omega that reproduces that target tilt
        def objective(omega_k):
            er = _single_view_return(p_k, q_k, omega_k, pi, sigma_inv_tau)
            w_k = _weights_from_returns(sigma_inv, er)
            return np.sum((w_k - target_w) ** 2)

        if c_k >= 0.999:
            omegas[row] = 1e-8  # ~100% confidence -> ~0 uncertainty
        else:
            result = minimize_scalar(
                objective, bounds=(1e-8, 50.0), method="bounded",
                options={"xatol": 1e-10},
            )
            omegas[row] = result.x

    return np.diag(omegas)


# -------------------------------------------------------- step 4: BL eqn ----
def black_litterman_combined_returns(pi, sigma, P, Q, omega) -> np.ndarray:
    """Formula 3 / 19:
    E[R] = [(tau*Sigma)^-1 + P'Omega^-1P]^-1 [(tau*Sigma)^-1*Pi + P'Omega^-1*Q]
    """
    sigma_inv_tau = np.linalg.inv(TAU * sigma)
    omega_inv = np.linalg.inv(omega)
    A = sigma_inv_tau + P.T @ omega_inv @ P
    b = sigma_inv_tau @ pi + P.T @ omega_inv @ Q
    return np.linalg.solve(A, b)


# -------------------------------------------------- mean-variance optimizer -
def optimize_weights(exp_returns, sigma) -> np.ndarray:
    """Maximize  w'E[R] - (delta/2) w'Sigma w   subject to:
         - weights sum to 1
         - long-only bounds (unless ALLOW_SHORTING)
         - combined satellite-sleeve weight <= MAX_SATELLITE_TOTAL_WEIGHT
    """
    n = len(TICKERS)
    sat_idx = [TICKERS.index(t) for t in SATELLITE_TICKERS]

    def neg_utility(w):
        return -(w @ exp_returns - 0.5 * DELTA * w @ sigma @ w)

    constraints = [
        {"type": "eq", "fun": lambda w: np.sum(w) - 1.0},
        {"type": "ineq", "fun": lambda w: MAX_SATELLITE_TOTAL_WEIGHT - np.sum(w[sat_idx])},
    ]
    default_bound = (0.0, 1.0) if not ALLOW_SHORTING else (-1.0, 1.0)
    bounds = [WEIGHT_BOUNDS_OVERRIDE.get(t, default_bound) for t in TICKERS]

    w0 = get_baseline_weight_vector()
    result = minimize(
        neg_utility, w0, method="SLSQP", bounds=bounds, constraints=constraints,
        options={"maxiter": 1000, "ftol": 1e-12},
    )
    if not result.success:
        warnings.warn(f"Optimizer did not converge cleanly: {result.message}")
    return result.x


# ------------------------------------------------------------- reporting ----
def _fmt_pct(x):
    return f"{x:+.2%}"


def print_report(w_mkt, sigma, pi, P, Q, confidences, descriptions, omega,
                  exp_returns, w_final):
    n = len(TICKERS)
    labels = [ASSET_LABELS.get(t, t) for t in TICKERS]

    print("=" * 78)
    print(" STEP 1 & 2 -- BASELINE WEIGHTS & IMPLIED EQUILIBRIUM RETURNS (Pi)")
    print("=" * 78)
    df1 = pd.DataFrame({
        "Asset": labels,
        "Baseline Weight": w_mkt,
        "Implied Equilibrium Return (Pi)": pi,
    }).set_index("Asset")
    df1["Baseline Weight"] = df1["Baseline Weight"].map("{:.2%}".format)
    df1["Implied Equilibrium Return (Pi)"] = df1["Implied Equilibrium Return (Pi)"].map(_fmt_pct)
    print(df1.to_string())
    print(f"\nRisk-aversion coefficient (delta): {DELTA}")

    print("\n" + "=" * 78)
    print(" STEP 3 -- TACTICAL VIEWS")
    print("=" * 78)
    df2 = pd.DataFrame({
        "View": [f"View {i+1}" for i in range(len(VIEWS))],
        "Description": descriptions,
        "Stated Confidence": [f"{c:.0%}" for c in confidences],
        "Implied Omega (variance)": np.diag(omega),
    }).set_index("View")
    print(df2.to_string())

    print("\n" + "=" * 78)
    print(" STEP 4 -- COMBINED RETURN VECTOR E[R] vs. EQUILIBRIUM (Pi)")
    print("=" * 78)
    df3 = pd.DataFrame({
        "Asset": labels,
        "Pi (equilibrium)": pi,
        "E[R] (combined)": exp_returns,
        "Tilt (E[R] - Pi)": exp_returns - pi,
    }).set_index("Asset")
    for col in df3.columns:
        df3[col] = df3[col].map(_fmt_pct)
    print(df3.to_string())

    print("\n" + "=" * 78)
    print(" FINAL PORTFOLIO -- OPTIMIZED WEIGHTS")
    print(f" (satellite sleeve {'+'.join(SATELLITE_TICKERS)} capped at "
          f"{MAX_SATELLITE_TOTAL_WEIGHT:.0%} combined)")
    print("=" * 78)
    df4 = pd.DataFrame({
        "Asset": labels,
        "Baseline Weight": w_mkt,
        "Optimized Weight": w_final,
        "Active Weight (tilt)": w_final - w_mkt,
    }).set_index("Asset")
    df4["Baseline Weight"] = df4["Baseline Weight"].map("{:.2%}".format)
    df4["Optimized Weight"] = df4["Optimized Weight"].map("{:.2%}".format)
    df4["Active Weight (tilt)"] = df4["Active Weight (tilt)"].map(_fmt_pct)
    print(df4.to_string())

    port_return = w_final @ exp_returns
    port_vol = np.sqrt(w_final @ sigma @ w_final)
    sharpe = (port_return - RISK_FREE_RATE) / port_vol if port_vol > 0 else np.nan
    print("\n" + "-" * 78)
    print(f" Expected portfolio return : {port_return:.2%}")
    print(f" Expected portfolio volatility (std dev): {port_vol:.2%}")
    print(f" Expected Sharpe ratio     : {sharpe:.3f}")
    print(f" Sum of weights            : {w_final.sum():.4%}")
    print("-" * 78)


# ------------------------------------------------------------------ main ----
def main():
    prices = load_price_data()
    sigma_df = covariance_matrix(prices)
    sigma = sigma_df.values

    w_mkt = get_baseline_weight_vector()
    pi = implied_equilibrium_returns(sigma, w_mkt)

    P, Q, confidences, descriptions = build_view_matrices()
    omega = idzorek_omega(P, Q, confidences, pi, sigma)
    exp_returns = black_litterman_combined_returns(pi, sigma, P, Q, omega)

    w_final = optimize_weights(exp_returns, sigma)

    print_report(w_mkt, sigma, pi, P, Q, confidences, descriptions, omega,
                 exp_returns, w_final)

    return {
        "prices": prices,
        "sigma": sigma_df,
        "w_mkt": w_mkt,
        "pi": pi,
        "P": P, "Q": Q, "omega": omega,
        "exp_returns": exp_returns,
        "w_final": w_final,
    }


if __name__ == "__main__":
    main()
```
