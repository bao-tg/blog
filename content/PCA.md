# Motivation

Sometimes, dueling with the high-dimensional data is exhausted, the computational power required is enormous. This lead to the fact that we need to somehow reduce the dimension of these data.

> The word "dimension" is actually the size of the data, not something that is too abstract.

In some case, reduce the size of the data somehow reduces the noise in the data, make the model more robust. 

> Well, this is quite intriguing to me, because this is empirical result, not rigorous. But what I can expect more from applied mathematics :D.

**Question:**
How can we reduce the size of the data?

> Can we just randomly remove some columns of the data matrix?, or some rows?

Obviously not.

PCA was born to solve this problem, we still reduce the size, meanwhile, we still keep the most "information" of the original data. The "information" will be rigorously defined later.

# PCA

## 2D PCA

In order to undertand the core principle of PCA, we need to understand how PCA works in small dimension first, suppose that we have $n$ 2D datapoints. And we want to reduce these into 1D. It means that we need a a way to transfer 2D data into a single value.

Lets assume that we have the 2D datapoints as in the image:

![[img/regression_notcenter.png]]

Since we want to get 1D value from these 2D data, one of the simple way is that, we project these values into a single line. 

But, which line?. In the picture below, INTUITIVELY, we know that the orange line is better than the blue line. This is not rigorous, I know, but we cannot expect the pure rigorousness in applied maths. Next, we need to write down the maths to tell the computer that okay, lets choose the orange line, not the blue line. 

![[img/compare.png]]

> Typical question when you read this part is: **Can we propose a new way to calculate the 1D value?**. Yes, of course, if you can propose a mathematical framework to reduce the size of data, and somehow, it works better than PCA both speed and performance (Compute faster, provide better accuracy in classification,...) -> then you have a paper :D. But notice that PCA was created in 1901, it means that almost every novel ideas were tested. And there are still many better ways to reduce the size of the data, we learn PCA because it was easy to get familiar and understand :D.

We firstly center the data, or subtract each datapoint by the mean of these datapoints. 

> We do this step because we want to MOVE all of the datapoints in the Oxy coordinate, such that the "good" line will always start at (0, 0). I will let the proof of this part for the readers :D. If this is wrong, notify me hehe.

Next, probably, the difference between the orange line, and the blue line is the sum of "variance", the orange line yields smaller sum of "variance" compared to the blue line.

> The key of learning mathematics is you can transfer what you intuitively feel into mathematical formulas. You feel that orange line is good, but what is exactly good?, in this case, it is variance!!!. We will define variance later.

Given the image, INTUITIVELY, the good line is supposed to yields the small value of $dist(\mathbf{x}_i \leftrightarrow \text{line})$.

![[img/variance.png]]

We note that the line is from the center, it makes the $||\mathbf{x}_i||$ constant. According to Pythagores identity, we need to maximize $\langle \mathbf{x}_i, \mathbf{w} \rangle$. Or, we need to maximize the sum of $\langle \mathbf{x}_i, \mathbf{w} \rangle$, for all datapoints $\mathbf{x}_i$.

> Comment: Note that we know our line passing through O, then a single vector $\mathbb{w}$ can be used to represent the whole line :D.

> That's why we need to center the datapoints.

That's the key point of 2D PCA!. Intuitively, given $n$-dimensional datapoints, if we want to reduce its size into $k$ dimension, we just need to find a space, that has $k$ dimensions, and project our $n$-dimensional datapoints to minimize the sum of variance, or maximize the sum of $\langle \mathbf{x}_i, \mathbf{w} \rangle$. 

> **A space that has $k$ dimensions**, or it has exactly $k$ vectors in its basis. We firstly find the first line, or vector, that satisfies max of sum variance. And then we iteratively find the next vector which yields the max of sum variance, and ensure that this next vector is orthogonal to all of the previous vectors. By this way, we ensure that the $k$ computed vectors forms the whole space, which yields maximize sum of variance of given points into this space!!!. This is a quite beautiful theorem, you can try to prove this in 3D, and generalize it into higher dimension.

Now, it's time for maths.

## High dimensional PCA

Given $N$ datapoints, represent as column vectors $x_1, x_2, \dots, x_N$. $\bar{x}$ is mean of these datapoint. $S$ is called covariance matrix of $N$ given datapoints.
$$
\bar{x} = \frac{1}{N} \sum_{n=1}^{N} x_n
$$

$$
S = \frac{1}{N} \sum_{n=1}^{N} (x_n - \bar{x})(x_n - \bar{x})^{T}
    = \frac{1}{N} \hat{X}\hat{X}^{T}
$$

Our objective problem is to find multiple orthogonal vectors $\mathbf{u}$ such that the sum of all variance is maximize, it can be written as:

$$
\begin{aligned}
\max_{\mathbf{u}} \quad & \mathbf{u}^{\top} \mathbf{S} \mathbf{u} \\
\text{s.t.} \quad 
& \lVert \mathbf{u} \rVert_2^2 = 1 \\
\end{aligned}
$$

> For a given vector $\mathbf{u}$ that satisfies the maximize sum of variance. We can scale $\mathbf{u}$ with an abitrary number, and it still yields the maximize sum of variance. Because of that, we can always scale the $\mathbf{u}$ such that its length is 1.

> This is a **constrained least square** problem!!!. We use KKT condition to solve it.

- Set up the Lagrangian:
  $$
  \mathcal{L}(\mathbf{u}, \lambda) = \mathbf{u}^T S\mathbf{u} - \lambda (\mathbf{u}^T \mathbf{u} - 1)
  $$
- The solution satisfies:
    $$
  S \mathbf{u} = \lambda \mathbf{u}
  $$

Or $\mathbf{u}$ is eigenvector of $S$. With this solution, we plug into our objective function, it yields

(See this [[Eigenvalue, eigenvector.md]] to know how to compute eigenvalue, eigenvectors)

$$\mathbf{u}^{\top} \mathbf{S} \mathbf{u} = \mathbf{u}^{\top} \lambda \mathbf{u} = \lambda$$

The higher $\lambda$, the higher objective function is. This mean that, the first vector $\mathbf{u}$ that we need to find is the eigenvector of $S$ which has the highest eigenvalue.

> The second vector $\mathbf{u}$ that we need to find is the eigenvector of $S$ which has the second highest eigenvalue, and orthogornal to the first eigenvector!!!. Iteratively use this procedure $k$ times, we find $k$ orthogornal vectors, which form the space that we need to find!!!!.

# Terminologies of PCA

> [!Note] Principal Components, Variance
> Each time of PCA procedure, we need to find $\mathbf{u}$ that maximize the sum of variance, this is called a principal component.
>
> Each principal component corresponding with a value, $\lambda$, this is called variance explained by that principal component.
>
> The principal component that has largest $\lambda$ is called, first principal component.
> Similar to the other principal components.

Obviously, the principal component is eigenvector of $S$, and its variance explained is its corresponding eigenvalue.

# Steps of PCA

![[img/pcaprocedure.png]]

The mathematical formulas of the the last step is:

$$
   y = W_k^T x_{\text{centered}}
   $$

- Where:
  - $W_k = (v_1, v_2, \dots, v_k)$ is the matrix of top $k$ eigenvectors.

# Eigenfaces

You can ignore this part, I just want to yap a little bit about this Eigenfaces project.

This is the procedure of eigenfaces

### 1. Dataset Representation
Assume we have $ N $ grayscale face images, each of size $ h \times w $.
Vectorize each image into a column vector:
$
\mathbf{x}_i \in \mathbb{R}^d,\quad d = h \cdot w,\quad i=1,\dots,N
$

Stack them into a data matrix:
$
X = [\mathbf{x}_1\ \mathbf{x}_2\ \cdots\ \mathbf{x}_N] \in \mathbb{R}^{d \times N}
$

### 2. Mean Face
Compute the mean face:
$
\boldsymbol{\mu} = \frac{1}{N}\sum_{i=1}^{N} \mathbf{x}_i
$

Center the data:
$
\tilde{\mathbf{x}}_i = \mathbf{x}_i - \boldsymbol{\mu}
$

$
\tilde{X} = [\tilde{\mathbf{x}}_1\ \cdots\ \tilde{\mathbf{x}}_N]
$

### 3. Covariance Matrix
The covariance matrix is:
$
S = \frac{1}{N}\tilde{X}\tilde{X}^T \in \mathbb{R}^{d \times d}
$

Since $ d \gg N $, compute eigenvectors via:
$
\tilde{X}^T \tilde{X} \mathbf{v}_k = \lambda_k \mathbf{v}_k
$

Recover eigenvectors of $ S $:
$
\mathbf{u}_k = \frac{1}{\sqrt{\lambda_k}} \tilde{X}\mathbf{v}_k
$

### 4. Eigenfaces
Each eigenvector $ \mathbf{u}_k \in \mathbb{R}^d $ is an **eigenface**.

Reshape it back to image form:
$
\mathbf{u}_k \rightarrow U_k \in \mathbb{R}^{h \times w}
$

### 5. Visualization of Eigenfaces
Eigenfaces are visualized by mapping vector values to pixel intensities:
$
I_k = \text{normalize}(U_k)
$

Typical normalization:
$
I_k = \frac{U_k - \min(U_k)}{\max(U_k) - \min(U_k)}
$

Displayed as grayscale images.

The image below shows the eigenfaces:

![[img/eigenfaces.png]]

> Intuitively, we can see that somehow, by maximize the sum of variance, the eigenvectors actually capture "some information" of the original data. The variance is "information" that we want to maximize when reduce the dimension of data, as mentioned in the beginning of the blog.

Another suprised result is that, any face can be represented as a linear combination of these eigenfaces

![[img/eigencombination.png]]

### 6. Projection onto Eigenfaces
Project a face onto the eigenface subspace:
$
\mathbf{y}_i = U^T(\mathbf{x}_i - \boldsymbol{\mu})
$

where:
$
U = [\mathbf{u}_1\ \mathbf{u}_2\ \cdots\ \mathbf{u}_K]
$

### 7. Reconstruction
Reconstruct using $ K $ eigenfaces:
$
\hat{\mathbf{x}}_i = \boldsymbol{\mu} + U\mathbf{y}_i
$

Increasing $ K $ improves visual fidelity.


### Intuition

- Bright/dark regions in eigenfaces correspond to correlated facial features
- Top eigenfaces capture global structure (lighting, pose)
- Later eigenfaces capture fine details

Eigenfaces are **principal components reshaped as images**.


# References

+ https://web.stanford.edu/class/cs168/l/l7.pdf
+ https://machinelearningcoban.com/2017/06/15/pca/