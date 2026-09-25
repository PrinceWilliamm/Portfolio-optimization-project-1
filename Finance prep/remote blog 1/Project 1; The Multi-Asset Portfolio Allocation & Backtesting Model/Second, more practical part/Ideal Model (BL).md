**BL model is based on the MPT model but it more refined as an institutional tool.**
The model has the next parameters and values:
- **Market Capitalization Weights ($w_{mkt}$):** The baseline assumption that the global financial market is already efficient. You determine the actual real-world size of your assets (e.g., US equities represent roughly 60% of the global stock market, International 40%).
- **Risk Aversion Parameter ($\delta$):** A measure of how much return the average market participant demands for taking on risk. It is calculated using the market portfolio's expected return and variance.
- **Implied Equilibrium Returns ($\Pi$):** This is the magic of Black-Litterman. Instead of guessing expected returns, you reverse-engineer them from the covariance matrix ($\boldsymbol{\Sigma}$) and market weights. $\Pi = \delta \boldsymbol{\Sigma} w_{mkt}$. This creates a neutral baseline return vector where no asset dominates the others arbitrarily.
- **Investor Views Matrix ($P$ and $Q$):** This is where you inject your active wealth management thesis. Views can be absolute ("I believe SOXX will return 12% next year") or relative ("I believe SOXX will outperform VOO by 3%").
- **Confidence Matrix ($\Omega$):** You quantify how certain you are about your views. High confidence forces the model to tilt heavily toward your view; low confidence keeps the model anchored to the neutral market equilibrium.
The final output is the **Adjusted Expected Return Vector ($E[R]$)**, which mathematically blends the neutral implied returns ($\Pi$) with your subjective views ($Q$), weighted by your confidence ($\Omega$). You then feed this new vector into your standard mean-variance optimizer. *
Optimal model introduces 5 to 8 trading instruments to keep calaculations manageable. 
	These in my upcoming test will include
	- VOO
	- VXUS
	- GOVT
	- XAR
	- VNQ (reduced)