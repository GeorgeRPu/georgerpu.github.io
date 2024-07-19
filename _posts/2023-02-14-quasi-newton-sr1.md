---
layout: post
title: "Quasi-Newton Methods (1/2): SR1"
date: 2023-02-14
description: "An introduction to quasi-Newton methods."
giscus_comments: true
toc:
  sidebar: left
tags: mathematics
citation: true
---

**Newton's method** is a classic optimization algorithm. Given a function $f\colon \mathbb{R}^n \to \mathbb{R}$ which we want to minimize, Newton's method updates a starting point $x_0$ based on the gradient $\nabla f$ and Hessian $Hf$.

$$
x_{k+1} = x - [Hf(x_k)]^{-1} \nabla f(x_k)
$$

While the gradient $\nabla f(x)$ is a $n$-dimensional vector of the partial derivatives

$$
\left(\frac{\partial f}{\partial x_1}, \dots, \frac{\partial f}{\partial x_n} \right),
$$

the Hessian is a $n \times n$​ matrix of all second derivatives.

$$
\begin{bmatrix}
	\frac{\partial^2 f}{\partial x_1^2} & \dots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
	\vdots & \ddots & \vdots \\
	\frac{\partial^2 f}{\partial x_n \partial x_1} & \dots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
$$

Because

1. the Hessian scales quadratically with the number of dimensions and
2. must be inverted,

for applications with high dimensions, such as optimizing the millions of parameters of a neural network, **quasi-Newton methods** that approximate the inverse Hessian from the gradient are preferred over Newton's method. We try to approximate the inverse Hessian instead of the Hessian to avoid performing an expensive matrix inverse.

Let $H_k = B_k^{-1}$ be a matrix. Here, $B_k$ approximates the Hessian while $H_k$​​ approximates the Hessian's inverse.[^1] Our quasi-Newton update rule takes the form:

$$
x_{k+1} = x_k - H_k \nabla f(x_k).
$$

Let $s_k = x_{k+1} - x_k$. Then

$$
s_k = - H_k \nabla f(x_k).
$$

So long as $H_k$ is positive definite, then

$$
-f(x_k)^\top s_k = -f(x_k)^\top H_k \nabla f(x_k).
$$

The directional derivative $\nabla f(x_k)^\top s_k$ is negative and so $s_k$​ is in the downhill direction. Note that if $H_k = I$, the equation above reduces to gradient descent, and if $H_k = [Hf(x)]^{-1}$, the equation reduces to Newton's method.

There are many different approaches to approximate $H_k$​​​​ for quasi-Newton methods. We present 3 over 2 posts.

## Symmetric Rank 1

We can approximate $H_k$ using the secant equation. The secant equation is the multidimensional generalization of the 1D rule that the derivative is approximately the slope of the secant line:

$$
f'(x_1) \approx \frac{f'(x_1) - f''(x_0)}{x_1 - x_0}.
$$

Let $y_k = \nabla f(x_{k+1}) - \nabla f(x_k)$ and $s_k = x_{k+1} - x_k$ as before.

$$
B_{k+1}s_k = y_k
$$

The secant equation gives us $n$ linear equations but $n(n + 1)/2$ unknown values in $B_{k+1}$. The secant equation is underdetermined.

To compensate, we make the ansatz that the $B_{k+1}$ update takes the form

$$
B_{k+1} = B_k + \sigma vv^\top
$$

where $\sigma = \pm 1$. This method is called **Symmetric Rank 1** because $vv^\top$​ is a symmetric rank 1 matrix.

Let's apply the ansatz to the secant equation.

$$
\begin{align*}
	y_k &= B_{k+1}s_k \\
	&= B_ks_k + \sigma vv^\top s_k \\
	&= B_ks_k + (\sigma v^\top s_k)v
\end{align*}
$$

Solve for $v$​.

$$
\begin{align*}
	y_k - B_ks_k &= (\sigma v^\top s_k)v \\
	v &= \frac{y_k - B_ks_k}{\sigma v^\top s_k}
\end{align*}
$$

From the equation for $v$, we get

$$
\begin{align*}
	v^\top s_k &= \frac{(y_k - B_ks_k)^\top s_k}{\sigma v^\top s_k} \\
	(v^\top s_k)^2 &= \frac{(y_k - B_ks_k)^\top s_k}{\sigma}
\end{align*}
$$

Now we can eliminate $vv^\top$ and $\sigma$​​​ from the update.

$$
\begin{align*}
	\sigma vv^\top &= \sigma \frac{y_k - B_ks_k}{\sigma v^\top s_k} \cdot \frac{(y_k - B_ks_k)^\top}{\sigma v^\top s_k} \\
	&= \sigma \frac{(y_k - B_ks_k)(y_k - B_ks_k)^\top}{\sigma^2 (v^\top s_k)^2} \\
	&= \sigma \frac{(y_k - B_ks_k)(y_k - B_ks_k)^\top}{\frac{\sigma^2}{\sigma}(y_k - B_ks_k)^\top s_k} \\
	&= \frac{(y_k - B_ks_k)(y_k - B_ks_k)^\top}{(y_k - B_ks_k)^\top s_k} \\
\end{align*}
$$

After substituting the equation for $\sigma vv^\top$ back into the update rule for $B_k$, we obtain

$$
B_{k+1} = B_k + \frac{(y_k - B_ks_k)(y_k - B_ks_k)^\top}{(y_k - B_ks_k)^\top s_k}.
$$

We can use the [Sherman-Morrison formula](https://en.wikipedia.org/wiki/Sherman–Morrison_formula)

$$
(A + uv^\top)^{-1} = A^{-1} - \frac{A^{-1}uv^\top A^{-1}}{1 + v^\top A^{-1}u}
$$

to calculate the update for the inverse Hessian approximation $H_k$.

$$
H_{k+1} = H_k + \frac{(s_k - H_k y_k)(s_k - H_k y_k)^\top}{(s_k - H_k y_k)^\top y_k}
$$

### Pros

- Storing and updating $H_k$ is $O(n^2)$.
- The outer product $vv^\top$ is positive semi-definite but not necessarily positive definite, making SR1 a good quadratic approximation for non-convex optimization problems.

### Cons

- The denominator can be 0 if $s_k = H_k y_k$ or $(s_k - H_k y_k)^\top y_k = 0$. The only solution is to skip the SR1 update: $H_{k+1} = H_k$​.

[^1]: Yes, it is confusing to have $H_k$ approximate the inverse of the Hessian, but this is the standard notation.
