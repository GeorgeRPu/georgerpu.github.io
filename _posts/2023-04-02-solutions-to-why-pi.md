---
layout: post
title: "Solution to Why π is in the normal distribution (beyond integral tricks)"
date: 2023-04-02
description: "The (n-1)-volume of the boundary of a n-dimensional ball"
giscus_comments: true
toc:
  sidebar: left
tags: mathematics
citation: true
---

$$
\newcommand{\D}[1]{\mathop{d#1}}
$$

In 3Blue1Brown's latest video [Why π is in the normal distribution (beyond integral tricks)
](https://www.youtube.com/watch?v=cy8r7WSuT1I), you can find an exercise at the [end](https://youtu.be/cy8r7WSuT1I?t=1500) that computes the $n-1$ volume of the boundary of an $n$-dimensional ball using the integral of a Guassian function. These is the solution.

## Part 1

$$
\begin{align*}
	I_n &= \int_{-\infty}^{\infty} \cdots \int_{-\infty}^{\infty} e^{-(x_1^2 + \dots + x_n^2)} \D{x_1} \cdots \D{x_n} \\
	&= \int_{-\infty}^{\infty} \cdots \int_{-\infty}^{\infty} e^{-x_1^2} \cdots e^{-x_n^2} \D{x_1} \cdots \D{x_n} \\
	&= \int_{-\infty}^{\infty} e^{-x_n^2} \cdots \int_{-\infty}^{\infty} e^{-x_1^2} \D{x_1} \cdots \D{x_n} \\
	&= \underbrace{\sqrt{\pi} \cdots \sqrt{\pi}}_{n \text{ times}} \\
	&= \pi^{n/2}
\end{align*}
$$

## Part 2

The integral $I_n$ calculates the total volume of the $n$-dimensional un-normalized Gaussian in $\mathbb{R}^n$ by integrating $e^{-(x_1^2 + \dots + x_n^2)}$ along each dimension from $-\infty$ to $\infty$.

Another way to calculate the volume of the Gaussian is using hyperspherical coordinates. There is 1 radial coordinate $r \geq 0$, $n-2$ angular coordinates $\phi_1, \dots, \phi_{n-2} \in [0, \pi)$, and another angular coordinate $\theta \in [0, 2\pi)$. As a function of these parameters, the Gaussian only depends on $r$

$$
f(r) = e^{-r^2}
$$

Recall that in polar coordinates $\D{A} = r \D{\theta} \D{r}$. Similarly, $\D{V} = r^{n-1} \D{\phi_1} \cdots \D{\phi_n} \D{\theta} \D{r}$. Let

$$
C_n = \int_{0}^{2\pi} \int_{0}^{\pi} \cdots \int_{0}^{\pi} 1 \D{\phi_1} \cdots \D{\phi_n} \D{\theta}.
$$

Then

$$
\begin{align*}
I_n &= \int_{0}^{r} \int_{0}^{2\pi} \int_{0}^{\pi} \cdots \int_{0}^{\pi} e^{-r^2} r^{n-1} \D{\phi_1} \cdots \D{\phi_n} \D{\theta} \D{r} \\
&= \int_{0}^{r} C_n r^{n-1} e^{-r^2} \D{r}.
\end{align*}
$$

## Part 3

Let $u = r^{n-2}$ and $\D{v} = re^{-r^2} \D{r}$. Then $\D{u} = (n - 2)r^{n-3} \D{r}$ and $v = -\frac{1}{2} e^{-r^2}$.

$$
\begin{align*}
I_n &= \int_{0}^{\infty} C_n r^{n-1} e^{-r^2} \D{r} \\
&= C_n \int_{0}^{\infty}  u \D{v} \\
&= C_n \left( uv - \int_{0}^{\infty} v \D{u} \right) \\
&= C_n \left( \left[ r^{n-2} \cdot -\frac{1}{2}e^{-r^2} \right]_{0}^{\infty} - \int_{0}^{\infty} -\frac{1}{2}e^{-r^2}  (n - 2)r^{n-3} \D{r} \right) \\
\end{align*}
$$

We first compute $\left[ r^{n-2} \cdot -\frac{1}{2}e^{-r^2} \right]_{0}^{\infty}$. Clearly, it is 0 when $r = 0$. When $r \to \infty$,

$$
r^{n-2} \cdot -\frac{1}{2}e^{-r^2} = -\frac{r^{n-2}}{2e^{r^2}} = -\frac{\infty}{\infty}
$$

Using L'Hôpital's rule, we get

$$
-\frac{(n-2)r^{n-3}}{4re^{r^2}} = -\frac{\infty}{\infty}
$$

which is still indeterminate. However, we see that, after $n-3$ more differentiations of the numerator and denominator, the numerator will eventually resolve to a constant while the denominator is $cp(r)e^{r^2}$ for some constant $c$ and $p(r)$ power of $r$.

$$
\lim\limits_{r \to \infty} r^{n-2} \cdot -\frac{1}{2}e^{-r^2} = 0
$$

With the $[uv]_{0}^{\infty}$ term eliminated,

$$
\begin{align*}
I_n &= C_n \left( - \int_{0}^{\infty} -\frac{1}{2}e^{-r^2}  (n - 2)r^{n-3} \D{r} \right) \\
&= \frac{n - 2}{2} C_n \int_{0}^{\infty} r^{n-3}e^{-r^2} \D{r} \\
&= \frac{n - 2}{2} C_n \frac{I_{n-2}}{C_{n-2}}
\end{align*}
$$

since $I_{n-2}$ includes the $C_{n-2}$ term in the integral.

## Part 4

From Part 1, we know that $I_n = \pi^{n/2}$.

$$
\begin{align*}
I_n &= \frac{n - 2}{2} C_n \frac{I_{n-2}}{C_{n-2}} \\
\pi^{n/2} &= \frac{n - 2}{2} C_n \frac{\pi^{(n-2)/2}}{C_{n-2}} \\
C_{n-2} \frac{2}{n-2} \frac{\pi^{n/2}}{\pi^{(n-2)/2}} &= C_n \\
C_{n-2} \frac{2\pi}{n - 2} &= C_n \\
C_n &= \frac{2\pi}{n - 2} C_{n-2}
\end{align*}
$$

Using the recurrence relation, we can compute $C_n$ for any $n$.

$$
\begin{align*}
C_2 &= 2\pi \\
C_3 &= 4\pi \\
C_4 &= \frac{2\pi}{4 - 2} C_2 = 2\pi^2 \\
C_5 &= \frac{2\pi}{5-2}C_3 = \frac{8}{3}\pi^2 \\
C_6 &= \frac{2\pi}{6 - 2}C_4 = \pi^3 \\
C_7 &= \frac{2\pi}{7 - 2}C_5 = \frac{16}{15} \pi^3
\end{align*}
$$

For

$$
S(n) = n\frac{\pi^{n/2}}{(n/2)!} r^{n-1}
$$

to be the volume of the boundary of a $n$-dimensional ball, $S(n)$ must satisfy 2 conditions.

1. $n\frac{\pi^{n/2}}{(n/2)!}$ must satisfy the recurrence relation above for $C_n$.

$$
\begin{align*}
n\frac{\pi^{n/2}}{(n/2)!} &\stackrel{?}{=} \frac{2\pi}{n - 2} (n - 2)\frac{\pi^{(n-2)/2}}{((n-2)/2)!} \\
&\stackrel{?}{=} 2\frac{\pi^{n/2}}{((n-2)/2)!} \\
n/2 \frac{\pi^{n/2}}{(n/2)!} &\stackrel{?}{=} \frac{\pi^{n/2}}{((n-2)/2)!} \\
\frac{\pi^{n/2}}{((n - 2)/2)!} &\stackrel{\checkmark}{=} \frac{\pi^{n/2}}{((n-2)/2)!}
\end{align*}
$$

2. $S(2) = 2\pi r$ and $S(3) = 4\pi r^2$.

$$
\begin{align*}
S(2) &= 2 \frac{\pi^{2/2}}{(2/2)!} r^{2-1} \\
&= 2\pi r \\
S(3) &= 3 \frac{\pi^{3/2}}{(3/2)!} r^{3-1} \\
&= 3 \frac{\pi^{3/2}}{(3/2)!} r^2 \\
&= 3 \frac{\pi^{3/2}}{(3/2)(1/2)(-1/2)!} r^2 \\
&= 3 \frac{\pi^{3/2}}{(3/2)(1/2)\sqrt{\pi}} r^2 \\
&= 4\pi r^2
\end{align*}
$$
