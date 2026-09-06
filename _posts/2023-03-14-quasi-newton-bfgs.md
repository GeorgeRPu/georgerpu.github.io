---
layout: post
title: "Quasi-Newton Methods (2/2): BFGS"
date: 2023-03-14
description: "A derivation of the BFGS and L-BFGS algorithms."
giscus_comments: true
toc:
  sidebar: left
tags: mathematics
pretty_table: true
citation: true
---

## BFGS

Instead of making the ansatz that the $B_{k+1}$ update is by summing an outer product, we instead make the ansatz that $H_{k+1}$ should be close to $H_k$ while satisfying the symmetry and secant equation constraints. Hopefully, the closeness requirement will make the update easy to compute.

Thus, $H_{k+1}$ is the solution to the constrained minimization problem

$$
\begin{aligned}
    \min&\quad \|H - H_k\|_{W}^2 \\
    \text{subject to}&\quad H = H^\top \\
    &\quad s_k = Hy_k.
\end{aligned}
$$

Here $\\|A\\|_W = \\|W^{1/2}AA^{1/2}\\|_F$ denotes the **weighted Frobenius norm** where $W$ is any symmetric matrix satisfying $Wy_k = s_k$.

Define

$$
\begin{align*}
	\hat{H} &= W^{1/2}HW^{1/2} & \hat{H}_k &= W^{1/2}H_kW^{1/2} \\
	\hat{s}_k &= W^{1/2}s_k & \hat{y}_k &= W^{-1/2}y_k
\end{align*}
$$

Then the optimization problem becomes

$$
\min \|\hat{H} - \hat{H}_k\|_F^2 \quad\text{subject to} \quad \hat{s}_k = \hat{y}_k = \hat{H}_k \hat{y}_k
$$

as $W^{-1/2}W s_k = W^{-1/2}y_k$.

Since $\hat{y}\_k$ is an eigenvector of $\hat{H}$, let $u = \\hat{y}\_k/\\|\hat{y}\_k\\|$. For an orthonormal complement $u_\perp$, $U = [u \mid u_\perp]$ is an orthonormal basis. Note that

$$
\|\hat{H} - \hat{H}_k\|_F^2 = \|U^\top \hat{H}_kU - U^\top\hat{H}U\|_F^2
$$

because the Frobenius norm is unitary invariant.

$$
\begin{align*}
	U^\top\hat{H}_kU - U^\top\hat{H}U &=
    \begin{bmatrix}
    	u^\top \\
    	u_\perp^\top
    \end{bmatrix}
    \hat{H}_k
    \begin{bmatrix}
    	u & u_\perp
    \end{bmatrix}
    -
    \begin{bmatrix}
    	u^\top \\
    	u_\perp^\top
    \end{bmatrix}
    \hat{H}
    \begin{bmatrix}
    	u & u_\perp
    \end{bmatrix} \\
	&=
	\begin{bmatrix}
		u^\top\hat{H}_k u & u^\top \hat{H}_k u_\perp \\
		u_\perp^\top\hat{H}_k u & u_\perp^\top\hat{H}_ku_\perp
	\end{bmatrix}
	-
    \begin{bmatrix}
    	u^\top\hat{H}u & u^\top\hat{H}u_\perp \\
    	u_\perp^\top\hat{H}u & u_\perp^\top\hat{H}u_\perp
    \end{bmatrix} \\
    &=
    \begin{bmatrix}
    	u^\top\hat{H}_ku & u^\top\hat{H}_ku_\perp \\
    	u_\perp^\top\hat{H}_ku & u_\perp^\top\hat{H}_ku_\perp
    \end{bmatrix}
	-
    \begin{bmatrix}
    	1 & 0 \\
    	0 & u_\perp^\top\hat{H}u_\perp
    \end{bmatrix}
\end{align*}
$$

Since $\hat{H}$ is only present in the lower right entry, $\\|U^\top\hat{H}_k U - U^\top\hat{H}U\\|_F$ is minimized when $U^\top\hat{H}_k U = U^\top\hat{H}U$. Thus the optimal

$$
\begin{align*}
	\hat{H} &= U
	\begin{bmatrix}
		1 & 0 \\
		0 & u_\perp^\top\hat{H}_ku_\perp
	\end{bmatrix}
	U^\top \\
	&= uu^\top + u_\perp u_\perp^\top H_k u_\perp u_\perp^\top \\
	&= uu^\top + (I - uu_\perp)\hat{H}_k(I - uu_\perp)
\end{align*}
$$

since $u_\perp u_\perp^\top = (I - uu_\perp)$.

After substituting the original variables, we get the **Broyden-Fletcher-Goldfarb-Shanno** (BFGS) algorithm.

$$
H_{k+1} = (I - \gamma_k s_ky_k^\top)H_k(I - \gamma_k y_ks_k^\top) + \gamma_k s_k s_k^\top
$$

where $\gamma_k = \frac{1}{y_k^\top s_k}$.

### Pros

BFGS has many advantages over SR1.

- Storing and updating $H_k$ is $O(n^2)$.
- BFGS is a rank 2 method since it is multiplied by and summed with an outer product.
- BFGS converges at a super-linear but not quadratic rate. This makes BFGS faster than gradient descent but slower than Newton's method.

## L-BFGS

Note that we are not actually interested in approximating the Hessian but computing the descent direction $d_k = H_k \nabla f(x)$. Let $q_k = \nabla f(x)$.

$$
\begin{align*}
	H_{k+1} q_{k+1} &= (I - \gamma_k s_ky_k^\top)H_k(I - \gamma_k y_ks_k^\top)q_k + \gamma_k s_k s_k^\top q_k \\
	&= (I - \gamma_k s_ky_k^\top)H_k(q_k - [\gamma_k s_k^\top q_k]y_k)  + [\gamma_k s_k^\top q_k] s_k
\end{align*}
$$

Define $\alpha_k = \gamma_k s_k^\top q_k$ and $q_{k+1} = q_k - \alpha_k y_k$.

$$
\begin{align*}
	H_{k+1} q_{k+1} &= (I - \gamma_k s_ky_k^\top)H_kq_{k+1} + \alpha_k s_k \\
	&= [H_kq_{k+1}] - \gamma_k s_ky_k^\top[H_kq_{k+1}] + \alpha_k s_k
\end{align*}
$$

Letting $z_k = H_kq_{k+1}$ and $\beta_k = \gamma_k y_k^\top z_k$, we have

$$
H_{k+1}q_{k+1} = z_{k+1} - \beta_ks_k + \alpha_ks_k^\top = z_k + (\alpha_k - \beta_k) s_k^\top.
$$

The **Limited-memory BFGS** (L-BFGS) approximates the BGFS algorithm using only $O(n)$ space by storing $m \ll n$ pairs $(s_k, y_k), \dots, (s_{k-m+1}, y_{k-m+1})$ by making the assumption that $H_{k-m+1} = \gamma_{k-m+1} I$. Then we can compute the current descent direction using the algorithm below.

```python
lr = # learning rate

k = 0
while not converged:
    q = grad(f(x))
    for i in range(k - m + 1):
        alpha = gamma * s.t() @ q
        q -= alpha * y
    z = gamma * q
    for i in range(max(0, k - m), k):
        beta = gamma * y.t() @ z
        z += (alpha - beta) * z
    x -= lr * z
    k += 1
```

### Pros

- L-BGFS uses only $O(mn)$ memory compared to $O(n^2)$ for BFGS.

### Cons

- L-BFGS does not have the same theoretical guarantees as BFGS. In practice, L-BFGS can perform just as well as BFGS.

Number of iterations required for different optimization algorithms to find the minimum $(1, 1)$ of the **Rosenbrock function** $f(x, y) = (1 - x)^2 + 100(y - x^2)^2$.

| Starting Point | Newton-CG | SR1         | BFGS        | L-BFGS      |
| -------------- | --------- | ----------- | ----------- | ----------- |
| (10, 10)       | 51        | 133         | 87          | 46 :trophy: |
| (-1, -1)       | 38        | 49          | 31          | 26 :trophy: |
| (0, 100)       | 37        | 49          | 72          | 34 :trophy: |
| (-100, 0)      | 140       | 14 :trophy: | 394         | 58          |
| (0.5, 0.5)     | 26        | 41          | 17 :trophy: | 18          |
