---
layout: book-review
title: Designing Data Intensive Applications
author: Martin Kleppmann
olid: OL36735720M
categories: software-engineering
buy_link: https://amzn.to/44eX3Sy
started: 2024-01-01
finished: 2024-12-31
date: 2024-12-31
released: 2017
stars: 4
status: Finished
---

*Designing Data Intensive Applications* (sometimes abbreviated as DDIA) is maybe the definitive book on system design. I feel like every software engineer I run into has read this book. This makes sense since the book is great. It's broad, covering a vast amount of content, from databases to file formats to distributed systems, but also deep. The book goes into different types of databases and how can be used, but also their internals. In fact, Chapter 3 exclusively covers the data structures used in databases: Hash indices, SSTables, LSM trees, B trees, and columnar storage. I definitely wish I read this book earlier in my career or even in college. Many of the lessons I have learned through experience are recognizable in the pages of DDIA. For example, the guidance on unbundling databases and designing applications around dataflow took me several years to learn at work.

However, DDIA shows its age in certain places. Certain topics are no longer relevant. MapReduce has been succeeded by tools like Spark. Data warehouses are mentioned but data lakes are not. There isn't much devoted running advanced algorithms or training machine learning models on data. But in my opinion, the biggest omission is the cloud[^5]. Rarely do software engineers need to create distributed data systems consisting of servers anymore. It's more common to pay for and use a cloud service that offers a distributed data system like Firebase ready-to-go. The cloud makes understanding the fundamentals in DDIA less important but also introduces novel system design problems such as how to mix cloud services with in house servers.

Overall, DDIA is a strong textbook on system design that I would recommend to every software engineer. Kleppmann is working on a new version of the book, which I look forward to reading when it's released.

---

[^5]: Martin Kleppmann also admits this in https://martin.kleppmann.com/2024/01/04/year-in-review.html.
