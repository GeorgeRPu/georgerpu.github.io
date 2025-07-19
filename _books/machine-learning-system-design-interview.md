---
layout: book-review
title: Machine Learning System Design Interview
author: Alex Xu, Ali Aminian
olid: OL46533616M
categories: machine-learning
buy_link: https://amzn.to/4ll8ije
started: 2025-01-01
finished: 2025-06-30
date: 2025-06-30
released: 2023
stars: 4
status: Finished
---

ML system design interviews are a close cousin of regular system design interviews. You are given a business problem, need to determine requirements, and present a high level overview of your solution. It's no surprise, then, that the author of the most popular book on system design interviews [_System Design Interview_](https://georgerpu.github.io/books/system-design-interview/) would write a book on ML system design interviews—in this case, coauthoring with an ML expert.

In the first chapter, the book provides a framework for how to answer ML system design interviews before going through 10 examples. The framework is simple and intuitive. Unlike _System Design Interview_, _Machine Learning System Design Interview_ doesn't give a quick primer before diving into the example questions. While ML nowadays is a massive field, too much for any 1 book or person to cover, the algorithms and models are essential to any solution. Changing the model can change the rest of the system. For example, since 2022ish, it has become possible to use prompts and LLMs to do fraud detection as opposed to training xgboost/random forest models. Taking the LLM route totally changes the data you need (text vs. numerical features), data engineering (data lake vs structured tables), inference (guardrails vs no guardrails), infrastructure (GPU instances vs. CPU instances), etc. The book partially makes up for this by explaining some ML concepts in the chapters.

My other gripe with the book is the overrepresentation of search/recommendation style problems. Only 3 of the chapters—"Google Street View Blurring System", "Harmful Content Detection", and "People You May Know" (arguably "Ad Click Prediction on Social Platforms" as well)—are about other types of problems. Problems such as content generation, robotics, and chatbots are missing. Otherwise, _Machine Learning System Design Interview_ is a great book that anyone preparing for ML system design interviews should read[^b].

[^b]: Another great preparation resource is [this great article](https://medium.com/data-science/nailing-the-machine-learning-design-interview-6b91bc1d036c).
