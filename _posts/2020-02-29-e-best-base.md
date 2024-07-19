---
layout: post
title: "$e$ is the Best Base"
date: 2020-02-29
description: "And why we don't use it"
giscus_comments: true
toc:
  sidebar: left
tags: computer-science
pretty_table: true
citation: true
---

Suppose we have $N$ small LED lights. We can arrange these lights in a rectange to represent a number. Each column is a single digit. Only 1 light is ever on to signify which digit it is. The number of lights in a column $B$ is the base of the number. The table below represents the number 55 in base 3.

| 27's digit | 9's digit | 1's digit |
| ---------- | --------- | --------- |
| OFF        | OFF       | OFF       |
| ON         | OFF       | OFF       |
| OFF        | OFF       | ON        |

The number of digits is $N/B$. What base $B$ should we choose to maximize the amount of numbers our rectangle can represent?

The the amount of numbers our rectangle can represent is

$$
I(B) = B^{\frac{N}{B}}.
$$

We need to find $\arg\max I(B)$. A trick we borrow from statistics is to maximize $\log I(B)$ instead. The logarithm is a monotic function and so doesn't change the location of the maximum, but $\log I(B)$ will be easier to work with.

$$
\log I(B) = \log B^{\frac{N}{B}} = \frac{N}{B} \log B
$$

The maximum of $\log I(B)$ is the value of $B$ that solves $[\log I(B)]' = 0$.

$$
\begin{align*}
[\log I(B)]' = -\frac{N}{B^2} \log B + \frac{N}{B} \frac{1}{B} &= 0 \\
-\frac{N}{B^2} \log B + \frac{N}{B^2} &= 0 \\
\frac{N}{B^2} \left( 1 - \log B \right) &= 0 \\
1 - \log B &= 0 \\
\log B &= 1 \\
B &= e
\end{align*}
$$

Thus, making the column height as to close to $e$ as possible maximizes the information content of our number system. We compute $I(B)$ at $B = 2, e, 3, 4$ to check our solution.

$$
\begin{align*}
\log I(2) &= \frac{N}{2} \log 2 \approx 0.151 N \\
\log I(e) &= \frac{N}{e} \log e \approx 0.368 N \\
\log I(3) &= \frac{N}{3} \log 3 \approx 0.159 N \\
\log I(4) &= \frac{N}{4} \log 4 \approx 0.151 N
\end{align*}
$$

If 3 is a more efficient base than 2, why do computers use binary? The reason is that the real world is full of noise. For example, suppose we have a circuit where we define 0V as 0, 1.5V as 1, and 3V as 2. This ciruit can only tolerate 1V of noise. Changing the signal by 1V changes the digit. However, if 0V is 0 and 3V is 1, then the circuit can tolerate 1.5V of noise.

There are more complications with ternary circuits. Changing 0 to 1 or 1 to 2 requires a 1V change but 0 to 2 is a 2V change. A ternary circuit is harder to construct in the first place as it needs to be able to distinguish 1.5V from 3V, something that the binary circuit doesn't need to do. All togeether, these engineering concerns mean that binary is the preferred base for electronic computers.
