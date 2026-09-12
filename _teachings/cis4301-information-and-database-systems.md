---
layout: course
title: CIS4301 Information and Database Systems 1 (TA)
description: First part of a two-course sequence on the essential concepts, principles, and techniques of modern database systems, covering the modeling and querying of data with conceptual data models and the development of a database application.
instructor: Dr. Pete Dobbins
year: 2020
term: Spring
location: CSE A101
time: Mondays, Wednesdays, and Fridays, 9:35-10:25 AM
course_id: cis4301-information-and-database-systems
schedule:
  - week: 1
    date: Jan 6
    topic: Introduction, Installation
    description: Chapters 1.1-1.4.
  - week: 2
    date: Jan 13
    topic: ER Diagrams, Relational Model
    description: Chapters 4.1-4.6.
  - week: 3
    date: Jan 20
    topic: MariaDB, SQL, and Java I
    description: Chapters 2.1-2.3, 6.1.
  - week: 4
    date: Jan 27
    topic: Relational Algebra I and II
    description: Chapters 2.4, 5.1-5.2.
  - week: 5
    date: Feb 3
    topic: Functional Dependencies
    description: Chapters 3.1-3.2.
  - week: 6
    date: Feb 10
    topic: Exam I
  - week: 7
    date: Feb 17
    topic: Normal Forms
    description: Chapters 3.3-3.5.
  - week: 8
    date: Feb 24
    topic: MariaDB and SQL II
    description: Chapters 6.1-6.3.
  - week: 9
    date: Mar 9
    topic: MariaDB and SQL III
    description: Chapters 6.4-6.5.
  - week: 10
    date: Mar 16
    topic: Transactions
    description: Chapter 6.6.
  - week: 11
    date: Mar 23
    topic: Exam II
  - week: 12
    date: Mar 30
    topic: Constraints, Foreign Keys, Triggers
    description: Chapter 7.
  - week: 13
    date: Apr 6
    topic: Views
    description: Chapters 8.1-8.2.
  - week: 14
    date: Apr 13
    topic: Cursors and Stored Procedures
    description: Chapters 9.3-9.4.
  - week: 15
    date: Apr 20
    topic: Exam III
---

## Course Overview

This course introduces the principles of relational databases. It covers:

- **Entity-relationship modeling.** Entities, attributes, and relationships; multiplicity (many-to-many, many-to-one, one-to-one), roles, is-a hierarchies, and weak entities. Design principles of faithfulness, avoiding redundancy, and simplicity. Keys, referential integrity, and degree constraints, and how to convert an ER diagram into relations.
- **Design theory.** Functional dependencies, keys and superkeys, Armstrong's inference rules, closures, and minimal bases. Redundancy, update, and deletion anomalies. Decomposition into Boyce-Codd normal form and third normal form, with the chase test for lossless joins and dependency preservation.
- **Relational algebra.** Set operations, selection, projection, cross product, natural and theta joins, and composing them into queries. Extended relational algebra on bags: duplicate elimination, sorting, aggregation, grouping, and outer joins.
- **SQL.** Selection and projection, data types and NULL semantics, joins, set operations, scalar and correlated subqueries, subqueries in FROM clauses, aggregation with GROUP BY and HAVING, table creation and schema modification, insertion and deletion, and views.
- **Beyond querying.** Transactions, constraints and foreign keys, triggers, cursors, and stored procedures.

## Homework

Programming work used MariaDB, with Java and JDBC for application code. Homework combined written problems with a semester-long project distributed in parts, and the lowest homework score was dropped.

## Prerequisites

- COP3503 or COP3504
- COT3100 Applications of Discrete Structures

## Textbook

- _A First Course in Database Systems_, 3rd edition, Ullman and Widom, or the comprehensive version, _Database Systems: The Complete Book_, 2nd edition, Garcia-Molina, Ullman, and Widom

## Grading

- Exams (3): 60%, 20% each
- Homework: 40%

## My Role

I was one of four Undergraduate Teaching Assistants (UF uses the term Peer Mentor). I held office hours, wrote solutions and grading rubrics for the homework and exams, graded SQL and JDBC submissions, and proctored exams. The semester moved online midway through because of the pandemic.
