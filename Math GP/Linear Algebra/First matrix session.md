#### Let's concider a matrix; ####
$$M = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$$
Concider that *v* =
$$ \begin{pmatrix} 1 \\ 1 \end{pmatrix} $$
Further more multiplying *v* with matrix *M*
$$\begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 2(1) + 1(1) \\ 1(1) + 2(1) \end{pmatrix} = \begin{pmatrix} 3 \\ 3 \end{pmatrix}$$
Therefore;
**Eigenvector:** $\begin{pmatrix} 1 \\ 1 \end{pmatrix}$
And;
**Eigenvalue:** $\lambda = 3$

#### Therefore scaling to 3x3 ####
Lets concider a 3x3 matrix M to be;
$$M = \begin{pmatrix} 13 & 12 & 2 \\ 12 & 13 & -2 \\ 2 & -2 & 8 \end{pmatrix}$$
An eigenvalue satisfies the equation $\det(M - \lambda I) = 0$, where *I* is the 3x3 identity matrix
Substracting $\lambda$ from each diagonal entry gives us;
$$M - \lambda I = \begin{pmatrix} 13 - \lambda & 12 & 2 \\ 12 & 13 - \lambda & -2 \\ 2 & -2 & 8 - \lambda \end{pmatrix}$$
For a $3 \times 3$ matrix $\begin{pmatrix} a & b & c \\ d & e & f \\ g & h & i \end{pmatrix}$, the determinant is given by $a(ei - fh) - b(di - fg) + c(dh - eg)$
Therefore;
$$\det(M - \lambda I) = $$
$$(13 - \lambda)\Big((13 - \lambda)(8 - \lambda) - (-2)(-2)\Big) - 12\Big(12(8 - \lambda) - (-2)(2)\Big) + 2\Big(12(-2) - (13 - \lambda)(2)\Big)$$
- **First term:**
    $$(13 - \lambda)\big((\lambda^2 - 21\lambda + 104) - 4\big) = (13 - \lambda)(\lambda^2 - 21\lambda + 100)$$
    $$= 13\lambda^2 - 273\lambda + 1300 - \lambda^3 + 21\lambda^2 - 100\lambda = -\lambda^3 + 34\lambda^2 - 373\lambda + 1300$$
    
- **Second term:**
    $$-12\big((96 - 12\lambda) + 4\big) = -12(100 - 12\lambda) = 144\lambda - 1200$$
- **Third term:**
    $$2\big(-24 - 26 + 2\lambda\big) = 2(2\lambda - 50) = 4\lambda - 100$$
Combining all three parts together gives us the answer of;

$$\det(M - \lambda I) = -\lambda^3 + 34\lambda^2 + (-373 + 144 + 4)\lambda + (1300 - 1200 - 100)$$

$$\det(M - \lambda I) = -\lambda^3 + 34\lambda^2 - 225\lambda = 0$$
Factoring out $-\lambda$ from the polynomial gives us the first eigenvalue:

$$-\lambda(\lambda^2 - 34\lambda + 225) = 0$$
Solving quadratic $\lambda^2 - 34\lambda + 225 = 0$: gives rest of the eigenvalues
Using quadratic solving formula gives us eventually;
$$(\lambda - 25)(\lambda - 9) = 0$$
Therefore other eigenvalue are;
$$\lambda_2 = 25, \quad \lambda_3 = 9$$
Furthermore answer for this 3x3 matrix M;
$$\lambda_1 = 0,  \lambda_2 = 25, \lambda_3 = 9 $$
