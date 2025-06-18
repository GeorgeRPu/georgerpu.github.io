---
layout: book-review
title: A Philosophy of Software Design
author: John Ousterhout
olid: OL28736729M
categories: software-engineering
buy_link: https://amzn.to/442IMIm
started: 2019-01-01
finished: 2019-12-31
date: 2019-12-31
released: 2018
stars: 5
status: Finished
---

*A Philosophy of Software Design* derives from Ousterhout's attempts to teach software design to students at Stanford. From 3 iterations of CS190 comes a few general and coherent principles. *A Philosophy of Software Design* is not only a philosophy; there are some helpful rules of thumb towards the end. But the main contribution of the book is a perspective, synthesized from teaching experience, on good software design and how to achieve it.

1. **Software design is about managing complexity.** Complexity is defined as anything that makes a program difficult to understand. Good software design becomes a purely conceptual activity. Good software design elegant like a good physical theory explaining a wide range of phenomena with few universal constants.

2. **Program strategically**. Design programs multiple times to evaluate the strengths and weaknesses of each architecture.

3. **Modules should be deep.** The best modules provide maximal functionality with minimal interface. They hide implementation details while being general purpose.

4. **Define errors out of existence.** Returning 0 exceptions is better than returning 1 is better than return 2 and so on, because exceptions are part of a module's interface, and complex interfaces leads to shallow modules.

Some of these contradict other bits of advice floating around. For example, most programming best practice books advise that modules should be kept short, often proposing 20[^3] (or some other natural number $n \leq 100$) lines as an upper bound for functions. To fulfill (3), however, often requires functions and classes be long. While (4) may be the superficial consensus, in practice, exceptions are almost always thrown up the software stack.

---

[^3]: "Functions should not be 100 lines long. Functions should hardly ever be 20 lines long." - *Clean Code*, page 34
