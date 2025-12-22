# Definition

> [!Note] **Spectral Decomposition**
> Let $A \in \mathbb{R}^{n \times n}$ be symmetric. Then there exist real numbers $\lambda_i \in \mathbb{R}, \ i = 1, \ldots, n$, and a set of orthonormal > vectors $u_i \in \mathbb{R}^n, \ i = 1, \ldots, n$, such that $A u_i = \lambda_i u_i, \quad i = 1, \ldots, n.$
> 
> Equivalently, there exists an orthogonal matrix
> $U = [u_1 \ \cdots \ u_n] \quad \text{(i.e., } UU^T = U^T U = I_n \text{)}$
> and a diagonal matrix
> $\Lambda = \operatorname{diag}(\lambda_1, \ldots, \lambda_n),$
> such that
>
> $$A = U \Lambda U^T = \sum_{i=1}^n \lambda_i u_i u_i^T,\quad \Lambda = \operatorname{diag}(\lambda_1, \ldots, \lambda_n).$$
>
> - The numbers $\lambda_i, \ i = 1, \ldots, n$, are the eigenvalues of $A$.
> - The vectors $u_i, \ i = 1, \ldots, n$, are the associated eigenvectors.

# Key Properties

> [!Note] Property 1:
> $$A^m = U \Lambda^m U^T = \sum_{i=1}^n \lambda_i^m u_i u_i^T,\quad \Lambda^m = \operatorname{diag}(\lambda_1^m, \ldots, \lambda_n^m).$$

> [!Note] Property 2:
> Symmetric matrix has all real eigenvalues.

> [!Note] Property 3:
> If $A$ is symmetric matrix, then $\det(A) = \lambda_1 \lambda_2 \dots \lambda_n$.

> I will let the proof of these properties as the exercise for the readers (I will prove this in the next tutor session of VinPi).

