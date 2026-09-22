# Terminology
#### Expected return
The profit or loss that an investor anticipates in an investment that has known historical rates of return (RoR)
	Furthermore, the expected return is like a long-term average of past returns.
#### Variance ($\sigma^2$) in an portfolio
A measure of volatility of an investment portfolio
	_It evaluates risk reflected by fluctuations in the combined actual returns of securities within a portfolio_
	Relies on standard deviations ($\sigma$)
	_A crucial aspect of modern portfolio management involves leveraging these metrics to optimize risk and return, emphasizing strategic asset selection based on their [correlation](https://www.investopedia.com/terms/c/correlation.asp) coefficients._
		Mathematical representation - **Portfolio variance** = $w_1^2σ_1^2 + w_2^2σ_2^2 + 2w_1 w_2Cov_12$
			Where;
				- $w_1$ = the portfolio weight of the first asset
				- $w_2$ = the portfolio weight of the second asset
				- $σ_1$ = the standard deviation of the first asset
				- $σ_2$ = the standard deviation of the second asset
				- $Cov_1,_2$ = the co-variance of the two assets, which can thus be expressed as
				$p_1,_2σ_1σ_2$, where $p_(1,2)$ is the correlation co-efficient between the two assets
#### Covariance and covariance matrices
Covariance on the other hand in wealth management and finance means a statistical measure that shows how the returns of two assets move in relation to each other. It helps to see wheter assets move hand in hand --> positive covariance or in opposite directions --> negative covariance
		_The directional relationship between the returns on two assets_
	Also helps to separate eggs into different baskets
	Mathematical representation $$\text{Covariance} = \sum \frac{(\text{Ret}_{abc} - \text{Avg}_{abc}) \times (\text{Ret}_{xyz} - \text{Avg}_{xyz})}{\text{Sample Size} - 1}$$
	Where; 
	$\text{Ret}_{abc} = \text{Day's return for ABC stock}$
	$\text{Avg}_{abc} = \text{ABC's average return over the period}$
	$\text{Ret}_{xyz} = \text{Day's return for XYZ stock}$
	$\text{Avg}_{xyz} = \text{XYZ's average return over the period}$
	$\text{Sample Size} = \text{Number of days sampled}$
	Furthermore covariance matrices will become to play and the mathematical representtation of them is noted followingly$$\Sigma = \begin{bmatrix}
\sigma_1^2 & \sigma_{12} & \sigma_{13} & \cdots & \sigma_{1n} \\
\sigma_{21} & \sigma_2^2 & \sigma_{23} & \cdots & \sigma_{2n} \\
\sigma_{31} & \sigma_{32} & \sigma_3^2 & \cdots & \sigma_{3n} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
\sigma_{n1} & \sigma_{n2} & \sigma_{n3} & \cdots & \sigma_n^2
\end{bmatrix}$$

#### Standard deviation
A statistic that measures the dispersion of a dataset relative to its mean and is calculated as the square root of the variance (look up for variance)
	If data points are far from the mean, there is a higher deviation within the data set.
	For example, a volatile stock has a high standard deviation, meaning that its price goes up and down frequently. The standard deviation of a stable [blue-chip](https://www.investopedia.com/terms/b/bluechip.asp) stock, on the other hand, is usually rather low, meaning that its price is usually stable.
	Often used in risk management strategies
Mathematical representation
$$\text{Standard Deviation} = \sqrt{\frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n - 1}}$$
	Where;
	$x_i = \text{Value of the } i^{\text{th}} \text{ point in the data set}$
	$\bar{x} = \text{The mean value of the data set}$
	$n = \text{The number of data points in the data set}$
#### Sharpe Ratio
A measure of an investment's risk-adjusted performance, caculated by comparing its return to that of a risk-free asset
	Proposed by William F. Sharpe shortly after his work in the Capital Asset Pricing Model (CAPM)
Mathematical representation
$$\text{Sharpe Ratio} = \frac{R_p - R_f}{\sigma_p}$$
	Where;
	$R_p = \text{return of portfolio}$
	$R_f = \text{risk-free rate}$
	$\sigma_p = \text{standard deviation of the portfolio's excess return}$
#### Modern portfolio theory (MPT)
A practical method for selecting investments in order to maximize their overall returns within an acceptable level of risk
	Proposed firstly by Harry Markowitz in 1952 in his paper "Portfolio selection" --> nobel prize
	Uses acceptable risk level and optimizes the expected return of the portfolio accordingly
	Works on diversified portfolios
	Futhermore it has been evolved to post modern portfolio theory (PMPT)
	Limitations include unusual market times
