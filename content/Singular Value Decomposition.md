# Definition

> [!Note] **Singular Value Decomposition (SVD)**
>For any matrix $A \in \mathbb{R}^{m \times n}$, there exist matrices $U, \Sigma, V$ such that
>$$
>A = U \Sigma V^\top
>$$
>Where:
>- $U \in \mathbb{R}^{m \times m}$: orthogonal matrix  
 > $$
  >U^\top U = I
  >$$
  >Columns of $U$ are **left singular vectors**.
> - $\Sigma \in \mathbb{R}^{m \times n}$: diagonal matrix  
  >$$
  >\Sigma = \operatorname{diag}(\sigma_1, \sigma_2, \dots, \sigma_r), \quad
  >\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0
  >$$
  >where $\sigma_i$ are **singular values** and $r = \operatorname{rank}(A)$.
> - $V \in \mathbb{R}^{n \times n}$: orthogonal matrix  
  >$$
  >V^\top V = I
  >$$
  >Columns of $V$ are **right singular vectors**.

# Key Property
- Singular values satisfy:
  $$
  \sigma_i = \sqrt{\lambda_i(A^\top A)}
  $$
- Right singular vectors are eigenvectors of $A^\top A$.
- Left singular vectors are eigenvectors of $A A^\top$.

> I highly recommend the readers try to prove this property, for deeply understand it.

This property is the key to construct the SVD form of an abitrary matrix $A$, which is required in the final exams. The next section will describe in details how to compute it.

# Construct SVD form

## Step 1:
Compute $A^\top A$, and $A A^\top$.

## Step 2:
Compute the eigenvalues, and eigenvectors of $A^\top A$, $A A^\top$.

## Step 3:
We sort all of the eigenvalues in ascending order, and take the square root (we only take positive value). And create $\Sigma = \operatorname{diag}(\sigma_1, \sigma_2, \dots, \sigma_r,)$.

## Step 4:
Stack all of the eigenvectors of $AA^\top$, corresponding to $\sigma_1, \sigma_2, \dots, \sigma_r$ into a matrix, it is $U$.
Stack all of the eigenvectors of $A^\top A$, corresponding to $\sigma_1, \sigma_2, \dots, \sigma_r$ into a matrix, it is $V$. 

> Note that the size of $U$ and $V$ isn't always the same. This means that we need to stack into the $\Sigma$ some 0, such that it satisfies the size $m \times n$. For example, $\Sigma = \operatorname{diag}(\sigma_1, \sigma_2, \dots, \sigma_r, 0, 0, 0)$. Actually, there are some 0 eigenvalues when you try to solve the root (value that makes the polynomial is 0) characteristics polynomial. Again, I highly recommend the readers try to solve the mocktest to fully understand this part.

# References

+ https://math.libretexts.org/Bookshelves/Linear_Algebra/Understanding_Linear_Algebra_(Austin)
+ MATH2050, Fall25, VinUniveristy.