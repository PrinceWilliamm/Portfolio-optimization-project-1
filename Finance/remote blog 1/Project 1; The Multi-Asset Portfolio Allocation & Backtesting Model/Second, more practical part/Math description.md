**As BL uses more heavy load math for me as a contibutor, this summary page will help to understand it. Also I hope this helps you as a reader to understand my methology better :).
This text is also provided fully by Gemini just for info. Some tweaks here or there were made by Contributor but majorly this task was handled by an external free worker. Enjoy :)
## Step 1: Implied Excess Equilibrium Returns (Reverse Optimization)

The Black-Litterman model uses market equilibrium excess returns as a neutral starting point. Rather than predicting returns directly, it extracts implied excess equilibrium returns using reverse optimization:

$$\Pi = \lambda \Sigma w_{\text{mkt}}$$

|**Variable**|**Matrix Dimension**|**Description**|
|---|---|---|
|$\Pi$|$N \times 1$|Implied Excess Equilibrium Return Vector|
|$\lambda$|Scalar|Risk aversion coefficient of the market|
|$\Sigma$|$N \times N$|Covariance matrix of asset excess returns|
|$w_{\text{mkt}}$|$N \times 1$|Market capitalization weights of the assets|

### Risk Aversion Coefficient ($\lambda$)
The risk aversion coefficient characterizes the expected risk-return tradeoff:


$$\lambda = \frac{E(r) - r_f}{\sigma^2}$$

  
where $E(r)$ is the expected market total return, $r_f$ is the risk-free rate, and $\sigma^2 = w_{\text{mkt}}^T \Sigma w_{\text{mkt}}$ is the variance of the market excess returns.
### Implied Betas ($\beta$)

Implied asset betas relative to the market capitalization-weighted portfolio are derived as:

  
$$\beta = \frac{\Sigma w_{\text{mkt}}}{w_{\text{mkt}}^T \Sigma w_{\text{mkt}}} = \frac{\Sigma w_{\text{mkt}}}{\sigma^2}$$

## Step 2: Portfolio Optimization (Mean-Variance Objective)

The optimum asset weights vector $w$ is found by solving the unconstrained utility maximization problem:

  
$$\max_{w} \left( w' \mu - \frac{\lambda}{2} w' \Sigma w \right)$$


Solving the objective function for $w$ yields:

$$w = (\lambda \Sigma)^{-1} \mu$$

  
If $\mu = \Pi$ (no investor views applied), the optimization returns the benchmark weights $w = w_{\text{mkt}}$.
## Step 3: Structuring Investor Views
Investor views can be absolute or relative and are expressed with an unobserved error vector $\epsilon$:$$Q + \epsilon$$
where $\epsilon \sim \mathcal{N}(0, \Omega)$.

|**Input**|**Matrix Dimension**|**Description**|
|---|---|---|
|$Q$|$K \times 1$|View Vector containing expressed performance estimates for $K$ views|
|$P$|$K \times N$|Matrix mapping $K$ views across $N$ total assets|
|$\Omega$|$K \times K$|Diagonal covariance matrix of error terms representing view uncertainty|

Each row $k$ in matrix $P$ sums to $0$ for relative views, where nominally outperforming assets receive positive weights and underperforming assets receive negative weights.

The variance of an individual view portfolio $k$ is:

$$\text{Var}(p_k) = p_k \Sigma p_k'$$

where $p_k$ is a $1 \times N$ row vector from $P$ corresponding to the $k$-th view.
## Step 4: The Black-Litterman Master Formula
The posterior Combined Expected Return Vector $E[R]$ blends equilibrium returns with investor views:

  
$$E[R] = \left[ (\tau \Sigma)^{-1} + P' \Omega^{-1} P \right]^{-1} \left[ (\tau \Sigma)^{-1} \Pi + P' \Omega^{-1} Q \right]$$

| **Parameter** | **Dimension** | **Role**                                                           |
| ------------- | ------------- | ------------------------------------------------------------------ |
| $E[R]$        | $N \times 1$  | Combined (posterior) expected excess return vector                 |
| $\tau$        | Scalar        | Scaling factor for the uncertainty of the equilibrium distribution |
| $\Sigma$      | $N \times N$  | Covariance matrix of excess returns                                |
| $P$           | $K \times N$  | View identification matrix                                         |
| $\Omega$      | $K \times K$  | Diagonal covariance matrix of view error terms                     |
| $\Pi$         | $N \times 1$  | Implied excess equilibrium return vector                           |
| $Q$           | $K \times 1$  | Expressed investor views vector                                    |

### Standard Calibration of $\Omega$ (He & Litterman Method)

Assuming $\Omega$ is proportional to the variance of the view portfolio scaled by $\tau$:

  
$$\Omega = \begin{bmatrix} (p_1 \Sigma p_1') \tau & 0 & 0 \\ 0 & \ddots & 0 \\ 0 & 0 & (p_K \Sigma p_K') \tau \end{bmatrix}$$

## Step 5: Incorporating User-Specified Confidence Levels ($0\%$ to $100\%$)

### Black-Litterman under 100% Certainty

When an investor has $100\%$ confidence in all views ($\Omega = 0$), the formula simplifies to:


$$E[R_{100\%}] = \Pi + \tau \Sigma P' (P \tau \Sigma P')^{-1} (Q - P \Pi)$$

### Idzorek's Step-by-Step Procedure for Determining $\Omega$
To set $\Omega$ using intuitive user-confidence levels ($C_k \in [0, 1]$):
1. **Calculate single-view 100% expected returns** for view $k$:
    $$E[R_{k,100\%}] = \Pi + \tau \Sigma p_k' (p_k \tau \Sigma p_k')^{-1} (Q_k - p_k \Pi)$$
2. **Compute 100% confidence portfolio weights**:
    $$w_{k,100\%} = (\lambda \Sigma)^{-1} E[R_{k,100\%}]$$
3. **Find the maximum departure from market weights**:
    $$D_{k,100\%} = w_{k,100\%} - w_{\text{mkt}}$$
    
4. **Calculate target portfolio tilt** using user-specified confidence $C_k$:
    $$\text{Tilt}_k = D_{k,100\%} * C_k$$
    
5. **Estimate target weight vector**:
    $$w_{k,\%} = w_{\text{mkt}} + \text{Tilt}_k$$
	
6. **Solve for the view uncertainty parameter ($\omega_k$)** by minimizing squared differences:
    $$\min_{\omega_k} \sum (w_{k,\%} - w_k)^2 \quad \text{subject to } \omega_k > 0$$
    where:$$w_k = (\lambda \Sigma)^{-1} \left[ (\tau \Sigma)^{-1} + p_k' \omega_k^{-1} p_k \right]^{-1} \left[ (\tau \Sigma)^{-1} \Pi + p_k' \omega_k^{-1} Q_k \right]$$
7. **Construct diagonal matrix $\Omega$** using each calculated $\omega_k$ and solve for $E[R]$ in the main Black-Litterman equation.