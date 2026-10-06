# Regime + Black-Litterman Portfolio Model

This implementation follows the attached roadmap's hierarchy:

**Market data → volatility regime → regime-based asset ranking → investment views → Black-Litterman → portfolio weights → MPT/risk decomposition → stress/backtest evaluation.**

The regime engine is intentionally not an allocator. It produces relative views such as `TLT > SPY`; Black-Litterman decides how far the portfolio should move away from its equilibrium prior.

## Client profiles

### 1. Aggressive Investor

Default example parameters:

- Desired annual return: 14%
- Return hurdle: 75% of target = 10.5%
- Maximum volatility: 50% of current S&P 500 volatility
- Maximum beta: 0.85
- Maximum equity weight: 75%
- Minimum defensive allocation: 10%

These are starting parameters. The code deliberately checks feasibility. When the constraints cannot all be satisfied simultaneously, it reports a `RELAXED_BEST_EFFORT` solution and quantifies the return/volatility/beta violation rather than pretending the target was achieved.

### 2. Low Volatility — Beat Savings

Default example parameters:

- Savings rate hurdle: 3.5%
- Minimum return hurdle: savings rate + 1.0% = 4.5%
- Maximum volatility: 7%
- Maximum beta: 0.35
- Maximum equity weight: 45%
- Minimum defensive allocation: 45%

Replace the savings rate with the actual client hurdle before using the model.

## Where to edit tickers and allocations

The most important blocks are at the top of `regime_bl_portfolio_model.py`:

- `ASSET_UNIVERSE`
- `AGGRESSIVE`
- `LOW_VOL_SAVER`
- `EQUITY_GROUPS`
- `DEFENSIVE_GROUPS`

The `prior_weights` inside each client profile are the Black-Litterman prior, not the final portfolio.

## Data modes

### Fast demo

Running:

```bash
python regime_bl_portfolio_model.py
```

uses deterministic synthetic data and creates a point-in-time research snapshot. This is intentionally fast and is only a pipeline demonstration.

### Real data

Install dependencies:

```bash
pip install -r requirements_regime_bl.txt
```

Then use the functions in the script:

```python
from regime_bl_portfolio_model import (
    ASSET_UNIVERSE,
    AGGRESSIVE,
    LOW_VOL_SAVER,
    download_yfinance_data,
    run_backtest,
)

market = download_yfinance_data(
    ASSET_UNIVERSE.keys(),
    start="2008-01-01",
)

aggressive = run_backtest(
    market,
    AGGRESSIVE,
    start_backtest="2016-01-01",
)

low_vol = run_backtest(
    market,
    LOW_VOL_SAVER,
    start_backtest="2016-01-01",
)

print(aggressive.metrics)
print(low_vol.metrics)
```

## Implied-volatility surface

The script contains a current option-chain hook and a 3D plot function. Historical backtesting of the full moneyness × maturity surface requires point-in-time historical option chains. The historical regime backtest therefore uses VIX/VIX3M plus additional stress proxies unless a professional options dataset is supplied.

## Research safeguards

The model includes:

- point-in-time signal construction;
- next-day implementation after a rebalance signal;
- rolling covariance estimation;
- covariance shrinkage when scikit-learn is available;
- transaction costs;
- explicit optimizer feasibility diagnostics;
- regime-conditional performance analysis;
- beta, Sharpe, Sortino, maximum drawdown, capture ratios, tracking error, information ratio and tail-loss metrics.

The synthetic demonstration must not be interpreted as historical market performance or as an investment recommendation.
