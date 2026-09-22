Problem A4 from MIT linear algebra problem sheet
Compute eigenvalues and eigenvectors from the following matrix
$$\begin{pmatrix} -3 & 3 & 2 \\ 1 & -1  & -2 \\ -1 & -3 & 0 \end{pmatrix}$$
In order to count eigenvectors and eigenvalues we need to substract $\lambda$ from each diagonal entry
$$M - \lambda I = \begin{pmatrix} -3 - \lambda & 3 & 2 \\ 1 & -1 - \lambda & -2 \\ -1 & -3 & 0 - \lambda \end{pmatrix}$$
In order to find the determinant we need to address the following formula
$$a(ei - fh) - b(di - fg) + c(dh - eg)$$
in an matrix which has letters in the following way; 
$$\begin{pmatrix} a & b & c \\ d & e & f \\ g & h & i \end{pmatrix}$$
Therefore;
$$\det(M - \lambda I) = $$
$$(-3 - \lambda)\Big((-1 - \lambda)(0 - \lambda) - (-2)(-3)\Big) - 3\Big(1(0 - \lambda) - (-2)(-1)\Big) + 2\Big(1(-3) - (-1 - \lambda)(-1)\Big)$$
##### First term equaling #####
=$$(-3 - \lambda)\Big((0 + \lambda+\lambda^2) - 6\Big)$$
Therefore
$$(-3 - \lambda)\Big(-6 + \lambda+\lambda^2\Big)$$
Which equals to
$$\Big(18 + 3\lambda-4\lambda^2-\lambda^3\Big)$$
##### Second term equaling #####
= $$-3\Big( - \lambda - 2\Big)$$
Which equals to
$$ 3\lambda + 6$$
##### Third term equaling #####
=
$$2\Big(1(-3) - (-1 - \lambda)(-1)\Big)$$
Therefore
$$2\Big(-3 -1 - \lambda\Big)$$
Finally equaling to
$$\Big(-8 - 2\lambda\Big)$$

Combining these all together gives us the equation
$$\det(M - \lambda I) = 18 + 3\lambda-4\lambda^2-\lambda^3 + 3\lambda + 6-6 -2 - 2\lambda$$
With further simplification gives us
$$\det(M - \lambda I) = -\lambda^3-4\lambda^2+4\lambda + 16 = 0$$
Multiplying with -1 to further get the eigenvalues
$$\lambda^3 + 4\lambda^2 - 4\lambda - 16 = 0$$
With grouping we will reach the final eigenvalues;
$$\lambda^2(\lambda + 4) - 4(\lambda + 4) = 0$$

$$(\lambda^2 - 4)(\lambda + 4) = 0$$

$$(\lambda - 2)(\lambda + 2)(\lambda + 4) = 0$$
Eigenvalues equaling to 
$$\lambda_1 = 2, \quad \lambda_2 = -2, \quad \lambda_3 = -4$$
Eigenvectors too evil so coming back later maybe