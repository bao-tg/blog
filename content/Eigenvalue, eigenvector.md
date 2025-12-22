
> [!Note] Eigenvalue, eigenvector: 
> Let $ A \in \mathbb{R}^{n \times n} $.
> A scalar $ \lambda \in \mathbb{R} $ and a nonzero vector $ v \in \mathbb{R}^n $ satisfy $A v = \lambda v $ are called:
> - $ \lambda $: an **eigenvalue** of $ A $.
> - $ v $: an **eigenvector** associated with $ \lambda $.

Note that $A v = \lambda v$ is equivalent to $(A - \lambda I)v = 0$. 

For a given $\lambda$, $v$ is the nonzero solution of the equation $(A - \lambda I)v = 0$, this mean that $(A - \lambda I)$ is not invertible, otherwise, $v$ will always be zero. That means $det(A - \lambda I) = 0$, well, this is actually a [[Polynomials.md]] with the variable $\lambda$.

> Well, this is not quite trivial, readers can try to derive the terms $\det(A - \lambda I)$ for a random square matrix $A$, I suggest you try with matrix $A = \begin{bmatrix}1&9\\20&5\end{bmatrix}$ , the result is surprisingly a polynomial.

> [!Note] Characteristics polynomial:
> For a square matrix $A \in \mathbb{R}^{n \times n}$, the **characteristic polynomial** is defined as $$p_A(\lambda) = \det(A - \lambda I)$$

For a given $\lambda$, we don't acually have only 1 $v$ that satisfies $(A-\lambda I)v = 0$, but the whole space $Null(A-\lambda I)$. This is called eigenspace.

> [!Note] Eigenspace:
> We denote $E_{\lambda} = Null(A-\lambda I)$ is eigenspace of $A$ associate to the eigenvalue $\lambda$.

And the dimension of $E_{\lambda}$ is actually depend on the multiplicity of $\lambda$ in the polynomials $\det(A - \lambda I)$. Expressed by the following proposition

> For example, if $\det(A-\lambda I) = (\lambda - 2)^2(\lambda - 3)$. Then the multiplicity of 2 in $\det(A - \lambda I)$ is 2, for 3, it is 1.

> [!Note] Dimension of eigenspace:
> If $\lambda$ is a real eigenvalue of a matrix $A$, with multiplicity $m$, then
> $$ 
> 1 \leq dim E_{\lambda} \leq m
> $$

> In the exams, we typically encounter the case that all $\lambda$ has the multiplicity of 1. It means that the dimension of the eigenspace is 1, or the eigenvector is in the format of a line!!!. But if the multiplicity is greater than 1, then we need to argue carefully.