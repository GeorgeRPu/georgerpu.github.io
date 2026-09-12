---
layout: course
title: CIS4930 Natural Language Processing with Python (TA)
description: Special topics course introducing the essential concepts, principles, and techniques of natural language processing, with topics spanning information extraction, grammars, disambiguation, and system modeling, classification, and evaluation.
instructor: Dr. Pete Dobbins
year: 2021
term: Spring
course_id: cis4930-nlp-with-python
---

## Course Overview

A CISE special topics course introducing the essential concepts, principles, and techniques of Natural Language Processing (NLP). It covers:

- Python for text processing: frequency distributions, conditional frequency distributions, file I/O, and regular expressions
- Corpora, training versus testing, overfitting, and Zipf's law
- Bigrams, collocations, and n-gram language models
- Statistical tests for collocations: t-test and chi-square test
- Parts of speech and tagging
- Supervised classification, feature extraction, naive Bayes classifiers, decision trees, and maximum entropy classifiers
- Evaluation: confusion matrices, precision, recall, and cross validation
- Finite state automata, chunking, and context-free grammars

## Homework

The programming assignments I helped write and autograde:

1. Implementing core text-processing functions from scratch, without external libraries, to understand how NLTK works under the hood
2. Building a k-gram language model as a conditional frequency distribution and using it to generate text
3. Writing a regular-expression tokenizer, extracting part-of-speech features, and identifying collocations with a chi-square test
4. Scraping Shakespeare's Roman tragedies from the MIT Shakespeare site, tagging lines by type, and analyzing their meter
5. Training a classifier to identify whether lines of dialogue come from a Shakespeare comedy or tragedy
6. Writing a context-free grammar in NLTK to parse source code into code, block comments, and inline comments

## Prerequisites

- COP3530 Data Structures and Algorithms

## Textbook

- _Natural Language Processing with Python_, 2nd edition, Bird, Klein, and Loper, available free at [nltk.org/book](https://www.nltk.org/book/)

## My Role

I served as an Undergraduate Teaching Assistant (UF uses the term Peer Mentor). I co-wrote the six programming assignments and the exam questions, built the test suites and a Canvas-integrated autograder that downloaded submissions, ran the tests, and posted grades and comments, and held office hours.
