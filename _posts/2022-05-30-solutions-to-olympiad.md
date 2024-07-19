---
layout: post
title: "Solution to Olympiad level counting"
date: 2022-05-30
description: "How many subsets of {1,…,2000} have a sum divisible by 5?"
giscus_comments: true
toc:
  sidebar: left
tags: mathematics
pretty_table: true
citation: true
---

In 3Blue1Brown's latest video [Olympiad level counting: How many subsets of {1,…,2000} have a sum divisible by 5?](https://www.youtube.com/watch?v=bOXCLR3Wric&t=22s), you can find a few easy exercises at the [end](https://youtu.be/bOXCLR3Wric?t=2054). These are the solutions.

## Problem 1

$$
\begin{align*}
\frac{d}{dx} \left[ \frac{1}{1 - x} \right] &= \frac{d}{dx} \left[ \sum_{n=0}^{\infty} x^n \right] \\
\frac{1}{(1 - x)^2} &= \sum_{n=0}^{\infty} nx^{n-1}
\end{align*}
$$

Note that the first term of the sum is 0 so,

$$
\sum_{n=0}^{\infty} nx^{n-1} = \sum_{n=1}^{\infty} nx^{n-1}.
$$

There are infinitely many scenarios you can roll a die before being the number 1.

| Number of rolls | Scenario                       | Probability         |
| --------------- | ------------------------------ | ------------------- |
| 1               | Roll 1                         | $1/6$               |
| 2               | Roll 2-6, roll 1               | $5/6 \cdot 1/6$     |
| ...             |                                |                     |
| $n$             | Roll 2-6 $n - 1$ times, roll 1 | $(5/6)^{n-1} (1/6)$ |
| ...             |                                |                     |

Then the expected value of the number of rolls before seeing 1 is

$$
\sum_{n=1}^{\infty} n p_n = \sum_{n=1}^{\infty} n (5/6)^{n-1} (1/6) = (1/6) \sum_{n=1}^{\infty} n(5/6)^{n-1}.
$$

Let $x = 5/6$.

$$
\sum_{n=1}^{\infty} nx^{n-1} = \frac{1}{(1 - x)^2} = \frac{1}{(1 - 5/6)^2} = \frac{1}{1/36} = 36
$$

Thus the expected number of rolls before seeing 1 is $(1/6)36 = 6$.

## Problem 2

Using the Binomial Theorem,

$$
(1 + x)^n = \sum_{k=0}^{n} {n \choose k} x^k.
$$

Letting $x = 2$,

$$
\sum_{k=0}^{n} {n \choose k} 2^k = (1 + 2)^n = 3^n.
$$

## Problem 3

$$
\begin{align*}
F(x) &= \sum_{n=0}^{\infty} f_n \frac{x^n}{n!} \\
F'(x) &= \sum_{n=1}^{\infty} f_n \frac{x^{n-1}}{(n - 1)!} \\
F''(x) &= \sum_{n=2}^{\infty} f_n \frac{x^{n-2}}{(n - 2)!}
\end{align*}
$$

We can reindex the bottom 2 sums by placing $n$ by $n + 1$ and $n + 2$ respectively.
$$
\begin{align*}
F'(x) &= \sum_{n=0}^{\infty} f_{n+1} \frac{x^n}{n!} \\
F''(x) &= \sum_{n=0}^{\infty} f_{n+2} \frac{x^n}{n!}
\end{align*}
$$
Thus,
$$
F''(x) = \sum_{n=0}^{\infty} f_{n+2} \frac{x^n}{n!} = \sum_{n=0}^{\infty} (f_{n+1} + f_n) \frac{x^n}{n!} = F'(x) + F(x).
$$

### Bonus

$$
\begin{align*}
F''(x) &= F'(x) + F(x) \\
F''(x) - F'(x) - F(x) &= 0
\end{align*}
$$

The characteristic of the homogeneous second order differential equation is $x^2 - x - 1 = 0$ which has roots

$$
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} = \frac{1 \pm \sqrt{1 + 4}}{2} = \frac{1 \pm \sqrt{5}}{2}
$$

Because there are 2 distinct real roots, the general solution is

$$
F(x) = c_1e^{\frac{1 + \sqrt{5}}{2}x} + c_2 e^{\frac{1 - \sqrt{5}}{2}x}.
$$

Since $F(0) = 0$ and $F'(0) = 1$,

$$
\begin{align*}
0 &= c_1 + c_2 \\
0 &= \frac{1 + \sqrt{5}}{2} c_1 + \frac{1 - \sqrt{5}}{2} c_2.
\end{align*}
$$

Thus,

$$
\begin{align*}
1 &= \left( \frac{1 + \sqrt{5}}{2} - \frac{1 - \sqrt{5}}{2} \right) c_1 \\
&= \frac{1 + \sqrt{5} - 1 + \sqrt{5}}{2} c_1 \\
&= \frac{2\sqrt{5}}{2} c_1 \\
c_1 &= \frac{1}{\sqrt{5}} \\
c_2 &= -\frac{1}{\sqrt{5}}
\end{align*}
$$

Recall that $e^x = \sum_{n=0}^{\infty} \frac{x^n}{n!}$.

$$
\begin{align*}
F(x) &= \frac{1}{\sqrt{5}} \sum_{n=0}^{\infty} \frac{(\frac{1 + \sqrt{5}}{2})^n x^n}{n!} - \frac{1}{\sqrt{5}} \sum_{n=0}^{\infty} \frac{(\frac{1 - \sqrt{5}}{2})^n x^n}{n!} \\
&= \sum_{n=0}^{\infty} \frac{(\frac{1 + \sqrt{5}}{2})^n x^n - (\frac{1 - \sqrt{5}}{2})^n x^n}{\sqrt{5} n!} \\
&= \sum_{n=0}^{\infty} \frac{(\frac{1 + \sqrt{5}}{2})^n - (\frac{1 - \sqrt{5}}{2})^n}{\sqrt{5}} \frac{x^n}{n!} = \sum_{n=0}^{\infty} f_n \frac{x^n}{n!}
\end{align*}
$$

Hence,

$$
f_n = \frac{1}{\sqrt{5}} \left[ \left( \frac{1 + \sqrt{5}}{2} \right)^n - \left( \frac{1 - \sqrt{5}}{2} \right)^n \right].
$$

## Problem 4

Recall from Problem 1 that

$$
\frac{1}{1 - x} = \sum_{n=0}^{\infty} x^n.
$$

Thus,

$$
\begin{align*}
\frac{f(x)}{1 - x} &= \left( \sum_{n=0}^{\infty} a_n x^n \right) \left( \sum_{n=0}^{\infty} x^n \right) \\
&= \left( a_0 + a_1x + a_2x^2 + \cdots \right) \left( 1 + x + x^2 + \cdots \right) \\
&= a_0 + a_0x + a_0x^2 + \cdots \\
&\qquad \,\,\, + \, a_1x + a_1x^2 + \cdots \\
&\qquad\qquad\quad\, + \, a_2x^2 + \cdots \\
&= \sum_{n=0}^{\infty} S_n x^n
\end{align*}
$$

where $S_n = \sum_{k=0}^{n} a_k$ is the partial sum of the coefficients up to $a_n$.
