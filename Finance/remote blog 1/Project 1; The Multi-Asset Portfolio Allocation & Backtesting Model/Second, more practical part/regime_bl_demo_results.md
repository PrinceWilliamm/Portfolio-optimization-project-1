# Demo Results — Regime + Black-Litterman Profiles

> [!warning]
> These figures are produced from the script's deterministic **synthetic dataset**. They demonstrate the mechanics and presentation of the model; they are **not** real market performance and must not be used as evidence of expected returns.

## Market State Used by the Demo

- Current regime: **R4 — High Volatility / Stress**
- Regime confidence: **36.47%**
- Regime stress score: **0.61**
- Synthetic S&P 500 annualized volatility in latest optimization window: **39.42%**

## Client 1 — Aggressive Investor

Configured objective:

- Desired annual return: **14.00%**
- Return hurdle: **10.50%** (75% of target)
- Maximum volatility: **19.71%** (50% of synthetic S&P 500 volatility)
- Maximum beta: **0.85**

Point-in-time BL result:

| Metric                     |              Result |
| -------------------------- | ------------------: |
| Expected BL return         |               5.97% |
| Expected stress return     |             -16.88% |
| Expected volatility        |              20.67% |
| Expected beta              |                0.35 |
| Optimizer status           | RELAXED_BEST_EFFORT |
| Return shortfall vs hurdle |               4.53% |
| Volatility excess          |               0.96% |

Interpretation: in the synthetic example, the 10.5% return hurdle and 50%-of-S&P-volatility ceiling cannot simultaneously be met with the available universe and constraints. The model explicitly surfaces this instead of presenting a false success.

## Client 2 — Low Volatility — Beat Savings

Configured objective:

- Savings hurdle: **3.50%**
- Return hurdle: **4.50%**
- Maximum volatility: **7.00%**
- Maximum beta: **0.35**

Point-in-time BL result:

| Metric | Result |
|---|---:|
| Expected BL return | 3.58% |
| Expected stress return | 5.59% |
| Expected volatility | 7.29% |
| Expected beta | 0.09 |
| Optimizer status | RELAXED_BEST_EFFORT |
| Return shortfall vs hurdle | 0.92% |
| Volatility excess | 0.29% |

Interpretation: the low-volatility profile gets close to the risk and beta objectives, but the particular synthetic universe does not fully clear the return hurdle and volatility ceiling at the same time. This is exactly the sort of feasibility trade-off the model is designed to expose.

## Example Regime Ranking in R4

The synthetic stress regime ranked the following assets near the top:

| Asset | Annualized Return | Annualized Vol | Sortino | Max DD | Regime Score |
|---|---:|---:|---:|---:|---:|
| TLT | 43.23% | 21.57% | 3.85 | -10.88% | 77.33 |
| SGOV | 3.61% | 0.99% | 7.37 | -0.29% | 74.67 |
| IEF | 9.11% | 9.97% | 1.61 | -9.32% | 66.00 |
| USMV | 43.19% | 20.90% | 3.97 | -6.32% | 63.33 |
| DBMF | 19.77% | 10.61% | 3.59 | -5.90% | 62.67 |

The model then translated the ranking into relative BL views rather than directly assigning weights.

### Aggressive example views

- TLT > SPY: +1.15%, 55% confidence
- SGOV > SPY: +1.06%, 55% confidence
- QQQ < SPY: -0.27%, 55% confidence
- EFA < SPY: -0.18%, 55% confidence

### Low-volatility example views

- TLT > SPY: +0.64%, 60% confidence
- SGOV > SPY: +0.59%, 60% confidence
- QQQ < SPY: -0.18%, 60% confidence
- EFA < SPY: -0.18%, 60% confidence

## Key Design Outcome

The architecture is deliberately hierarchical:

**Regime → conditional asset evidence → views → Black-Litterman → constrained allocation → risk decomposition → stress testing.**

The aggressive profile therefore does not need to beat the S&P 500 every year. Its success criterion is whether the return sacrifice is justified by reduced volatility, lower beta and improved stress behavior.

The savings-oriented profile is evaluated more like a capital-preservation mandate: beating its savings-rate hurdle matters, but volatility, beta, drawdown and behavior in R4/R5 conditions matter at least as much.
