#### Markov's process principle of Transition Probability Matrix, often denoted as *P* 
Markov chains are described followingly
	 "A Markov chain is a kind of stochastic process, which fulfils the Markov property, i.e., the probability that the next state will occur only depends on the present state and not on the sequence of states which preceded it. By this property, Markov chains can be an effective and comfortable way of modelling random processes."
#### The mathematical representation of a Transition Probability Matrix
Through Markov chains one could describe TPM's followingly
	"Think about a Markov chain with n states, named as *1,2,.....n.* The transition probability matrix **P** is an *n×n* matrix where each element $P_{ij}$​ gives the probability of moving from state **i** to state **j** in a one-time step. The matrix below illustrates the relationship between the Transitive Probability Matrix and **P.**"
$$P = \begin{bmatrix} P_{11} & P_{12} & P_{13} & \dots & P_{1m} \\ P_{21} & P_{22} & P_{23} & \dots & P_{2m} \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ P_{n1} & P_{n2} & P_{n3} & \dots & P_{nm} \end{bmatrix}$$
**Rules and boundaries for TRP's and Markov chains**
Not A SINGLE ELEMENT should be found negative inside *P*
On each row of matrix *P* components must add up to 1, represented mathematically by the formula $\sum_j P_{ij} = 1$
### Theoretical Finance example
Markov chains and TRP's are useful in finance and with the help of them we can build for example a Hamiltonian Regime-Switching Model
	State 1 (Bull market/Low volatility); Mean return $\mu_1 = +0.5\%$, Volatility $\sigma_1 = 1\%$
	State 2 (Bear market/High volatility); Mean return $\mu_2 = -1.0\%$, Volatility $\sigma_2 = 3\%$
The probabilities of moving between these states from day *t-1* to day *t* are given by a Transition Matrix *P* 
The following equation represents the model;
$$P = \begin{pmatrix} P(S_t=1 \vert{} S_{t-1}=1) & P(S_t=2 \vert{} S_{t-1}=1) \\ P(S_t=1 \vert{} S_{t-1}=2) & P(S_t=2 \vert{} S_{t-1}=2) \end{pmatrix} = \begin{pmatrix} 0.90 & 0.10 \\ 0.20 & 0.80 \end{pmatrix}$$
- If yesterday was State 1, there is a **90% chance** today stays in State 1, and a **10% chance** it switches to State 2.
- If yesterday was State 2, there is an **80% chance** today stays in State 2, and a **20% chance** it switches back to State 1. 
- For further information, S&P 500 could be used for a model like this
Suppose that yesterday (*t-1*) one estimated that probability for being in state 1 was 70%
$P(S_{t-1} = 1) = 0.70$) and state 2 was 30% ($P(S_{t-1} = 2) = 0.30$).
So, before observing today's return, we could calculate the probability of being in each state today based on yesterday's probabilities and the transition matrix with the following equation:
$$\text{Prior } P(S_t = 1) = P(S_{t-1}=1) \cdot P(S_t=1\vert{}S_{t-1}=1) + P(S_{t-1}=2) \cdot P(S_t=1\vert{}S_{t-1}=2)$$

$$\text{Prior } P(S_t = 1) = (0.70 \times 0.90) + (0.30 \times 0.20) = 0.63 + 0.06 = \mathbf{0.69}$$

$$\text{Prior } P(S_t = 2) = 1 - 0.69 = \mathbf{0.31}$$
Computing the likelihood of the observed return
Assuming returns follow a normal distribution $N(\mu_s, \sigma_s^2)$ in each state, evaluate the normal probability density function (PDF) for $r_t = -2.0\%$ in both states.
The density formula is $f(r) = \frac{1}{\sigma \sqrt{2\pi}} \exp\left(-\frac{(r - \mu)^2}{2\sigma^2}\right)$:

1. **In State 1 ($\mu_1 = 0.5, \sigma_1 = 1.0$):**
$$f(r_t \vert{} S_t = 1) = \frac{1}{1 \sqrt{2\pi}} \exp\left(-\frac{(-2.0 - 0.5)^2}{2(1)^2}\right) = 0.3989 \times \exp(-3.125) \approx \mathbf{0.0175}$$
2. **In State 2 ($\mu_2 = -1.0, \sigma_2 = 3.0$):**
$$f(r_t \vert{} S_t = 2) = \frac{1}{3 \sqrt{2\pi}} \exp\left(-\frac{(-2.0 - (-1.0))^2}{2(3)^2}\right) = 0.1330 \times \exp(-0.0556) \approx \mathbf{0.1258}$$
Computing the Joint probabilities
Multiply the prior probability of being in each state by the likelihood of observing $r_t = -2.0\%$ in that state;
- **Joint Prob (State 1):** $\text{Prior } P(S_t=1) \times f(r_t\vert{}S_t=1) = 0.69 \times 0.0175 = \mathbf{0.012075}$
- **Joint Prob (State 2):** $\text{Prior } P(S_t=2) \times f(r_t\vert{}S_t=2) = 0.31 \times 0.1258 = \mathbf{0.038998}$
Sum the joint probabilities to get the total marginal likelihood of the return;
$$\text{Total Likelihood } f(r_t) = 0.012075 + 0.038998 = 0.051073$$
Now dividing each joint probability by the total likelihood we get the updated (**posterior**) state probabilities;
$$P(S_t = 1 \vert{} r_t) = \frac{0.012075}{0.051073} \approx \mathbf{23.6\%}$$

$$P(S_t = 2 \vert{} r_t) = \frac{0.038998}{0.051073} \approx \mathbf{76.4\%}$$
