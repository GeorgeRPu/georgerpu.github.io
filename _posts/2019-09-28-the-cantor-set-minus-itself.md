---
layout: post
title: The Cantor Set Minus Itself
---

The Cantor set is one of the most famous constructions in all of mathematics. Start with the interval $[0, 1]$, let's call it $E_0$, and remove the middle third. We are left with $E_1 = [0, 1/3] \cup [2/3, 1]$. Do this to get $E_n$ for all $n \in \mathbb{N}$.

```
E_1 = ---------------------------
E_2 = ---------         ---------
E_3 = ---   ---         ---   ---
E_4 = - -   - -         - -   - -
...
```

The **Cantor set** is the intersection of these sets.

$$
C = \bigcap_{n=1}^{\infty} E_n
$$

The Cantor set has a number of interesting properties.

1. It contains no intervals. This makes sense since we break up intervals to create $C$.
2. It's perfect (contains all its limit points). [^1]
3. It's uncountable. This actually follows from (2).
4. It is a null set. At stage $1, 2, \dots, n, \dots$, we remove $1/3, 4/9, \dots, 2^{n-1}/3^n, \dots$; the total sum of these is $1$.


One of the most surprising is that $C - C = [-1, 1]$.

First, what is meant by $C - C$? Here, the subtraction is short for $C + (-C)$. Okay, so what do the negative and addition mean? The **reflection** of a set takes the negative of all it's points. More formally, $-A = \{-x : x \in A\}$. So $-[0, 1] = [-1, 0]$ and $-(-1, 1) = (-1, 1)$. The **translation** of a set shifts it by some quantity.

$$
A + b = \{a + b : a \in A\}
$$

As an example, $[0, 1] + 2 = [2, 3]$. Translating a set $A$ by another set $B$ is the union of the translations of $A$ by every element in $B$.

$$
A + B = \bigcup_{b \in B} A + B = \{a + b : a \in A, b \in B\}
$$

So how do we prove that $C + C = [0, 2]$? The key is in alternate construction of the Cantor set. Write every real number in $[0, 1]$ as its ternary expansion $0.x_1x_2x_3\dots$ where $x_n = 0, 1, 2$. Note that this expansion is not unique. Similar to how $0.\bar{9}_{10} = 1$, so too does $0.\bar{2}_3 = 1$ (from now on, all number are in base 3). By removing the middle third of $[0, 1]$, we remove the numbers between $0.1$ and $0.2 = 0.\bar{1}$. These numbers all have a $1$ in the $x_1$ position. Repeating ad infinitum, we see that the Cantor set consists only of numbers whose ternary expansion does not include a $1$.

Finally, we ready for the proof. Let $z \in [-1, 1]$.

$$
z = \pm 0.z_1z_2z_3\dots
$$

We can choose $x, y \in C$ such that $z = x - y$. Start with $x_n = 0, y_n = 0$ for $n \in \mathbb{N}$.

- If $z_n = 0$, let $x_n = 0$ and $y_n = 0$.
- If $z_n = 2$, let $x_n = 2$ and $y_n = 0$.
- If $z_n = 1$, picking $x_n, y_n$ is harder. Clearly, $x_n = 2$ but what about $y$? Note that $0.2 - 0.0\bar{2} = 0.1$ and $0.2 - 0.02 = 0.11$. So to get $z_n = 1$, we need $y_n = 0, y_{n+1} = 2, y_{n+2}$ and so on. However, now the values of $y_{n+1}, y_{n+2}, \dots$ are nonzero. This is not a problem if $z_{n+1}, z_{n+2}, \dots$ = 0, 1, as we do not need to tamper with $y$. If $z_{n+1} = 1$, then we add back $0.y_1 \dots y_n1 = 0.y_1 \dots y_n\bar{2}$ into $y$.

To get the negative version, swap the role of $x$ and $y$.

$$
-z = -(x - y) = y - x
$$

[^1]: A **limit point** of a set $Y$ is the limit of a convergent sequence contained in $Y$. For example, 0 is the limit point of $(0, 1)$ because $(1/2, 1/3, \dots) \to 0$. Because of this, $(0, 1)$ is not perfect.
