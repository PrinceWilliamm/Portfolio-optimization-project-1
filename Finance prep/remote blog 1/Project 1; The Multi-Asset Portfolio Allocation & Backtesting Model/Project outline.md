## What are the aims of the project
Aims are to create a comprehensive analysis on the optimized portfolio the contributor W is going to create with the help of Artificial Intelligence
	The ultimate goal is to have an impact and LinkedIn Larp at the end of this project (if succesful)
Project goals include building a dynamic portfolio optimization model using historical data across different asset classes, backtest the info and gather rather important data for further studies/careers
	Equities, Fixed Income, Commodities, Real Estate
## First part in this magnificent project (MPT)*
More theoretical
- _Firsly:_ Pull historical price data (using Excel, Python, or Google Sheets) for major ETFs representing asset classes (e.g., SPAGG, AGG, GLD, VNQ). Calculate expected returns, variance, and covariance matrices.
- _Secondly:_ Construct a mock client profile (e.g., "Moderate Growth, 15-year horizon") and code or calculate an optimal asset allocation using Modern Portfolio Theory (Efficient Frontier).
- _Thirdly_: Write a concise 2-page investment memo outlining the strategy, maximum drawdown limits, and rebalancing frequency.
## Second part of the project (Black-Litterman model)*
More institutional and therefore practical
	To build the Black-Litterman framework, you must transition away from using historical mean returns as your expected returns. Instead, the model follows a specific, step-by-step mathematical logic.
- **Market Capitalization Weights ($w_{mkt}$):** The baseline assumption that the global financial market is already efficient. You determine the actual real-world size of your assets (e.g., US equities represent roughly 60% of the global stock market, International 40%).
- **Risk Aversion Parameter ($\delta$):** A measure of how much return the average market participant demands for taking on risk. It is calculated using the market portfolio's expected return and variance.
- **Implied Equilibrium Returns ($\Pi$):** This is the magic of Black-Litterman. Instead of guessing expected returns, you reverse-engineer them from the covariance matrix ($\boldsymbol{\Sigma}$) and market weights. $\Pi = \delta \boldsymbol{\Sigma} w_{mkt}$. This creates a neutral baseline return vector where no asset dominates the others arbitrarily.
- **Investor Views Matrix ($P$ and $Q$):** This is where you inject your active wealth management thesis. Views can be absolute ("I believe SOXX will return 12% next year") or relative ("I believe SOXX will outperform VOO by 3%").
- **Confidence Matrix ($\Omega$):** You quantify how certain you are about your views. High confidence forces the model to tilt heavily toward your view; low confidence keeps the model anchored to the neutral market equilibrium.
The final output is the **Adjusted Expected Return Vector ($E[R]$)**, which mathematically blends the neutral implied returns ($\Pi$) with your subjective views ($Q$), weighted by your confidence ($\Omega$). You then feed this new vector into your standard mean-variance optimizer.
## How to Larp*
For my resume, an explicit example of larping would be the next textual example
	_Developed a multi-asset class portfolio optimization model in Excel/Python utilizing Modern Portfolio Theory; backtested historical risk-adjusted returns (Sharpe ratio) across 3 distinct economic cycles to design a risk-aligned asset allocation strategy._