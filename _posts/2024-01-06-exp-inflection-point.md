---
layout: post
title: "The Inflection Point of the Exponential Function"
description: Please stop referring to the "inflection point" of the exponential function.
date: 2024-01-06
giscus_comments: true
toc:
  sidebar: left
tags: mathematics
citation: true
---

An exponential is a function of the form $f(x) = a^x$ where $a > 0$. *The* exponential $\exp(x)$ uses the base $a = e$. Let's plot the exponential function.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 1000)
y = np.exp(x)
plt.plot(x, y)
plt.xlabel('x')
plt.ylabel('y')
plt.xlim(0, 5)
plt.ylim(0, np.exp(5))
plt.show()
```

{% include figure.liquid path="assets/img/2024-01-06/2024-01-06-exp-inflection-point_1_0.png" class="img-fluid" %}

## The "Inflection Point"

To the eye, it appears that the exponential function grows slowly at first, then suddenly starts to grow faster after $x = 3.5$. Often, this point is called the **elbow**, **knee**, or, most egregiously, the **inflection point**.

This is an illusion. If we zoom out, the "inflection point" shifts.


```python
plt.plot(x, y)
plt.xlabel('x')
plt.ylabel('y')
plt.xlim(0, 10)
plt.ylim(0, np.exp(10))
plt.show()
```

{% include figure.liquid path="assets/img/2024-01-06/2024-01-06-exp-inflection-point_3_0.png" class="img-fluid" %}

Now it looks like the "inflection point" is at $x = 8$. If we zoomed in instead of zooming out, the "inflection point" would shift to the left.

```python
plt.plot(x, y)
plt.xlabel('x')
plt.ylabel('y')
plt.xlim(0, 2)
plt.ylim(0, np.exp(2))
plt.show()
```

{% include figure.liquid path="assets/img/2024-01-06/2024-01-06-exp-inflection-point_5_0.png" class="img-fluid" %}

Now it looks like the "inflection point" is at $x = 1$. The "inflection point" is not a real feature of exponentials but a artifact of the way we plot them. Changing our perspective changes the location of the "inflection".

## What is an Inflection Point?

Formally, an **inflection point** is when the derivative changes sign. The problem with saying that an exponential has an inflection point is that the derivative of an exponential is always positive.

$$
\begin{align*}
f(x) &= a^x > 0 \\
f'(x) &= a^x \ln(a) > 0
\end{align*}
$$

Intuitively, the exponential function constantly grows at a geometric rate. Each increment of $x$ by 1 increases the value of the function by a factor of $a$. If we used a log-scale for the $y$-axis, the exponential function would look like a straight line.


```python
plt.plot(x, y)
plt.xlabel('x')
plt.ylabel('y')
plt.yscale('log')
plt.xlim(0, 10)
plt.ylim(1, np.exp(10))
plt.show()
```

{% include figure.liquid path="assets/img/2024-01-06/2024-01-06-exp-inflection-point_7_0.png" class="img-fluid" %}

The exponential has an inflection point no more than a straight line has an inflection point. As long as the original function is always positive, the sign of the derivative in log-scale is the same as normal scale.

$$
\begin{align*}
g(x) &= \log f(x) \\
g'(x) &= f'(x) / f(x)
\end{align*}
$$

## Why do we think there's an Inflection Point?

In high school, I would often get questions like

> A species of bacteria lives in a petri dish. The population doubles every day. In 30 days, the bacteria coveries the entire dish. On which day did the bacter cover half the dish?

wrong. I would put answers like 15 or 20. The correct answer is 29. It took me half a year to catch on. Humans are often bad with exponential growth because we focus on the absolute values. Going from 1/2 to 1 is a bigger change than going from 1/4 to 1/2, but the latter takes the same amount of time as the former. Thus, it seems like all of a sudden, on the last day the bacteria explode in population. We might think that the bacteria have done something different to grow so quickly, that there was an inflection point. In reality, the bacteria have merely continued growing at the same, geometric, rate they always have.

Misunderstanding exponential growth can be a costly mistake. Exponential growth governs much of the world. The spread of diseases, population growth, and the growth of money in a savings account are all exponential.
