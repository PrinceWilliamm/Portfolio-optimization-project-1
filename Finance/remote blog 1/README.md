# Volatility-Regime Core-Satellite Portfolio Model & Options-Driven Black-Litterman Framework
An institutional-grade portfolio optimization and dynamic asset allocation framework written in Python. This repository combines forward-looking options market metrics (At-The-Money Implied Volatility, Term Structure Slope, and Downside Skew) with **Modern Portfolio Theory (MPT)** and the **Black-Litterman Model** to construct dynamic, crash-resistant wealth management portfolios.
## Key Features
- **Forward-Looking Options Surface Signals:** Replaces backward-looking historical variance with options-implied volatility ($IV_{\text{ATM}}$) and tracks term structure slope ($IV_{\text{3M}} - IV_{\text{1M}}$) and downside volatility skew ($IV_{90\%} - IV_{\text{ATM}}$).
- **4-Stage Volatility Regime Classification:** Automatically categorizes market environments into **Low** (31% historical frequency), **Normal** (35%), **Elevated** (25%), and **High / Stress** (9%) states.
- **Black-Litterman Integration:** Blends market equilibrium baseline returns ($\boldsymbol{\Pi} = \delta \boldsymbol{\Sigma} \mathbf{w}_{\text{mkt}}$) with options-derived quantitative views ($P$, $Q$), dynamically scaling view uncertainty ($\boldsymbol{\Omega}$) based on term structure inversion and skew spikes.
- **Core-Satellite Governance:** Enforces structural asset boundaries (70–80% Core broad beta, 20–30% Satellite tactical growth/hedging) to eliminate single-factor concentration risks.
- **Downside Risk Analytics:** Measures Maximum Drawdown (MDD), Sortino Ratio, Value at Risk (VaR), Conditional VaR (CVaR), and upside/downside market capture ratios.
- **Interactive Streamlit Dashboard:** Live UI displaying option surface metrics, regime historical performance, and interactive allocation sliders.
## Asset Universe & Strategic Roles
The model operates across six asset classes designed to optimize correlation decay during market stress:
	The assets **can** be modified to any needs one client might have, but these are just representations of basics

| **Asset Class**            | **Primary Tickers** | **Strategic Role**               | **Baseline Weight** |
| -------------------------- | ------------------- | -------------------------------- | ------------------- |
| **US Equities**            | `VOO` / `SPY`       | Broad Core Equity Beta           | 25.0%               |
| **International Equities** | `VXUS` / `VEU`      | Global Diversification           | 25.0%               |
| **Government Bonds**       | `GOVT` / `TLT`      | Deflationary Risk-Off Anchor     | 10.0%               |
| **Short-Duration / Cash**  | `SGOV` / `BIL`      | Capital Preservation / Liquidity | 10.0%               |
| **Gold & Commodities**     | `GLD` / `DBC`       | Real Asset Inflation Hedge       | 20.0%               |
| **Defensive Alternatives** | `XLP` / `XLU`       | Low-Beta Sector Overlay          | 10.0%               |

## Historical Performance & Risk Benchmarks
Backtested against the S&P 500 across full market cycles (October 2007 – 2026):
With the given allocations and assets I reached the following results

|**Performance / Risk Metric**|**Model Portfolio**|**S&P 500 Benchmark**|**Relative Spread / Benefit**|
|---|---|---|---|
|**Compound Annual Growth Rate (CAGR)**|**6.7%**|10.7%|Defensive growth profile|
|**Annualized Volatility ($\sigma$)**|**10.4%**|15.5%|**-5.1% Risk Reduction**|
|**Maximum Drawdown (MDD)**|**-34.4%**|-50.9%|**+16.5% Drawdown Mitigation**|
|**Drawdown Recovery Period**|**31 months**|52 months|**21 months faster recovery**|
|**Portfolio Beta ($\beta$)**|**0.60**|1.00|Controlled market exposure|
|**Downside Capture Ratio**|**60%**|100%|40% loss mitigation in down years|
|**Sortino Ratio ($R_f = 0\%$)**|**0.70**|0.91|Downside-adjusted return|

## Quantitative Methodology & Mathematical Framework
### 1. Black-Litterman Implied Equilibrium Returns ($\boldsymbol{\Pi}$)
Reverse-engineers global market consensus expected returns using the covariance matrix ($\boldsymbol{\Sigma}$) and global market capitalization weights ($\mathbf{w}_{\text{mkt}}$):
$$\boldsymbol{\Pi} = \delta \boldsymbol{\Sigma} \mathbf{w}_{\text{mkt}}$$

Where $\delta \approx 2.5$ represents the market risk-aversion coefficient.
### 2. Options-Driven Views ($P, Q$) & Uncertainty ($\boldsymbol{\Omega}$)
Tactical views are automatically formulated from option chain pricing:
- **Term Slope Condition ($IV_{3\text{M}} - IV_{1\text{1M}} < 0$):** Indicates near-term market turbulence. Generates a view $Q$ where Short Cash (`SGOV`) and Treasuries (`GOVT`) outperform Equities (`SPY`) by $5.0\%$.
- **Downside Skew Condition ($IV_{90\%} - IV_{\text{ATM}} > +5.0\text{ pts}$):** Indicates high institutional demand for protective puts. Increases view weight towards Gold (`GLD`) and Defensive Sectors (`XLP`).
The view uncertainty matrix ($\boldsymbol{\Omega}$) is scaled continuously using the signal intensity:
$$\Omega_{k,k} = \tau \left( P_k \boldsymbol{\Sigma} P_k^T \right) \cdot f(\text{Term Slope}, \text{Skew})$$
### 3. Posterior Master Equation
Combining market equilibrium with quantitative options views yields the updated return vector $E[R]$:

$$E[R] = \left[ (\tau \boldsymbol{\Sigma})^{-1} + P^T \boldsymbol{\Omega}^{-1} P \right]^{-1} \left[ (\tau \boldsymbol{\Sigma})^{-1} \boldsymbol{\Pi} + P^T \boldsymbol{\Omega}^{-1} Q \right]$$

## Regime Allocation Matrix
Asset allocations shift dynamically based on the current volatility state:
```
  ┌────────────────────────────────────────────────────────┐
  │         Option Surface Feature Engine                  │
  │     (ATM IV, Term Slope, Downside/Upside Skew)         │
  └───────────────────────────┬────────────────────────────┘
                              │
            ┌─────────────────┴─────────────────┐
            ▼                                   ▼
┌──────────────────────────────┐    ┌──────────────────────────────┐
│  Low Volatility (31% time)   │    │ High/Stress Vol (9% time)    │
│  - Equity: 50%               │    │ - Equity: 20%                │
│  - Defensive/Cash: 20%       │    │ - Defensive/Cash: 50%        │
│  - Gold/Commodities: 20%     │    │ - Gold/Commodities: 30%      │
└──────────────────────────────┘    └──────────────────────────────┘
```