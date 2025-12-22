# Definition

> [!Note] PSD
> A symmetric matrix $A$ is called positive semidefinite iff: $$x^TAx \geq 0, \forall x \in \mathbb{R}^n$$
> Note that if $x^TAx > 0, \forall x \in \mathbb{R}^n$, we call $A$ is positive definite. Denote $A \succeq 0$.

# Property

> [!Note] Property
> + $A \succeq 0 \iff \lambda_i(A) \ge 0,\; i = 1,\ldots,n$
> + $A \succ 0 \iff \lambda_i(A) > 0,\; i = 1,\ldots,n$
> + It is immediate to see that a positive semidefinite matrix is actually positive definite if and only if it is invertible

> Note that $A$ is symmetric!!!. that means we can do [[Spectral Decomposition.md]]

# Geometric representation of PSD

> [!Note] Ellipsoid
> Given a positive semidefinite matrix $P$, then the Set $\epsilon = \set{x :  x^TPx \leq 1}$, represent the Ellipsoid.

Assume $P = U \Lambda U^T$, then we have $x^TPx = x^TU \Lambda U^Tx$. Let $x^TU = \begin{bmatrix}x_1 \\ x_2 \\ \dots \\ x_n\end{bmatrix}$, the value $P = U \Lambda U^T$ must be represent as $\lambda_1 x_1^2 + \lambda_2 x_2^2 + \dots + \lambda_n x_n^2$. $P \leq 1$, lead to  $\lambda_1 x_1^2 + \lambda_2 x_2^2 + \dots + \lambda_n x_n^2 \leq 1$. This is the equation of ellipsoid.

> I may remind you guys the formulas for the ellipsoid in 2D is: $\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$. $a$, and $b$ is the length of two axis of the ellipsoid!!!.

Here, we have a quite strong comment:

> - The eigenvalues $\lambda_i$ and eigenvectors $u_i$ of $P$ define the orientation and shape of the ellipsoid:
>  - $u_i$ are the directions of the semi-axes of the ellipsoid,
>  - the lengths of the semi-axes are given by $1/\sqrt{\lambda_i}$.
