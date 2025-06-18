---
layout: book-review
title: System Design Interview
author: Alex Xu
olid: OL30260884M
categories: software-engineerin
buy_link: https://amzn.to/4lbuyvI
started: 2024-01-01
finished: 2024-12-31
date: 2024-12-31
released: 2020
stars: 4
status: Finished
---

*System Design Interview* is the resource for preparing for system design interviews. It was also the first resource for system design interviews, written by Xu after failing to find a satisfactory system design interview preparation resource for his own study. I cannot speak on its utility for system design interviews as I have not participated in many. However, I do believe that is an underrated resource for junior software engineers learning how to design software systems.

*System Design Interview* presents a 4 step framework for system design interviews.

1. Understand the problem and establish the design scope.
2. Propose high-level design and get buy-in.
3. Design deep-dive.
4. Wrap-up.

These match the steps of gathering requirements, high level design + review, low level design + review, and implementation when actually designing software. Thus, the 12 case studies in *System Design Interview* are also 12 examples of design documents. I especially like the case studies "Design Rate Limiter", "Design Consistent Hashing", and "Design Google Drive". Each case study has detailed but clear diagrams that make me feel like I can implement the system Xu has designed. Each chapter has links to learn more.

I have a few qualms with the book.

- The first 2 chapters and case studies present foundational concepts but never go in depth.
- Many case studies don't present alternate designs. Design a Web Crawler is an example. Designing software is often about picking a design out of a larger design space that makes the right tradeoffs: maximizing the attributes you care about most while compromising on less important properties. Alternate designs are useful to understand tradeoffs.

- The book doesn't mention technologies which are now ubiquitous: serverless functions, containers, serverless workflows, NoSQL databases, and, the biggest omission, data pipelines. There is no discussion of data lakes, data warehouses, ETL jobs, or just batch processing systems in general, except for Design a Web Crawler.

These hold the book back, causing my opinion to be lower than many others[^6]. Still, I think it is good starting point for software engineers looking to master system design and system design interviews. For system design, I would recommend pairing it with other books, articles about systems from tech blogs, and system design experience at work or through personal projects.

---

[^6]: For an alternative perspective, see https://blog.pragmaticengineer.com/system-design-interview-an-insiders-guide-review/.
