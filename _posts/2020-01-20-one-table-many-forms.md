---
layout: post
title: "One Table, Many Normal Forms"
---

A **relation**[^1] is a table. It is made up of rows, or tuples, $(x_1, \dots, x_n)$ whose members $x_i$ are single values of a data type $D_i$. A column is a list of components from each row. The header of each column is an **attribute**. The name of the relation and the set of attributes are the **relation schema**.

| Title      | Director       | Year | Era           | Actors                         | Studio      | Studio HQ         |
| ---------- | -------------- | ---- | ------------- | ------------------------------ | ----------- | ----------------- |
| Avengers   | Josh Whedon    | 2012 | Blockbuster   | Robert Downey Jr., Chris Evans | Marvel      | Burbank, CA       |
| Casablanca | Michael Curtiz | 1942 | Golden Age    | Ingrid Bergman                 | Warner Bros | Burbank, CA       |
| Star Wars  | George Lucas   | 1977 | New Hollywood | Harrison Ford                  | Lucas Film  | San Francisco, CA |

A relation is in **first normal form** (1NF) if its attribute data types admit single values only. A value in a relation should never be a list or set or some other advanced data structure. Consider the above relation `Movies`. It is not 1NF since multiple actors may be listed per movie. For `Movies` to be in 1NF, we must list the actors in different rows.

| Title      | Director       | Year | Era           | Actor             | Studio      | Studio HQ         |
| ---------- | -------------- | ---- | ------------- | ----------------- | ----------- | ----------------- |
| Avengers   | Josh Whedon    | 2012 | Blockbuster   | Robert Downey Jr. | Marvel      | Burbank, CA       |
| Avengers   | Josh Whedon    | 2012 | Blockbuster   | Chris Evans       | Marvel      | Burbank, CA       |
| Casablanca | Michael Curtiz | 1942 | Golden Age    | Ingrid Bergman    | Warner Bros | Burbank, CA       |
| Star Wars  | George Lucas   | 1977 | New Hollywood | Harrison Ford     | LucasFilm   | San Fransisco, CA |

In a relation, $B_1, \dots, B_k$ **functionally depend** on $A_1, \dots, A_n$ if, whenever two tuples have the same values for $A_1, \dots, A_n$, the two tuples have the same values on $B_1, \dots, B_k$. This is analogous to the definition of a function: some values determine others. The functional dependency (FD) is written as $A_1, \dots, A_n \to B_1, \dots, B_k$.

A **key** is a the minimal set of attributes $A_1, \dots, A_n$ which functionally determine all attributes in a relation. By minimal, we mean that no subset of a key determines all attributes. Relations may have more than one key, in which case a **primary key** must be chosen. In `Movies`, there are 2 keys: `title, year`[^2] and `director, studio, year`[^3].

Any attributes included in a key are **prime**. A relation is in **second normal form** (2NF) if there are no non-prime attributes which functionally depend on a proper subset of a key. `Movies` is not 2NF since the `era` of a film functionally depends on its `year` which is part of the key. We can correct this by splitting spinning of another table `FilmHistory` from `Movies`.

| Title      | Director       | Year | Actor             | Studio      | Studio HQ         |
| ---------- | -------------- | ---- | ----------------- | ----------- | ----------------- |
| Avengers   | Josh Whedon    | 2012 | Robert Downey Jr. | Marvel      | Burbank, CA       |
| Avengers   | Josh Whedon    | 2012 | Chris Evans       | Marvel      | Burbank, CA       |
| Casablanca | Michael Curtiz | 1942 | Ingrid Bergman    | Warner Bros | Burbank, CA       |
| Star Wars  | George Lucas   | 1977 | Harrison Ford     | LucasFilm   | San Francisco, CA |

| Year | Era           |
| ---- | ------------- |
| 2012 | Blockbuster   |
| 1942 | Golden Age    |
| 1977 | New Hollywood |

A relation is in **third normal form** (3NF) if, for every FD $A_1, \dots, A_n \to B_1, \dots, B_k$, either $A_1, \dots, A_n$ is a superkey or every $B_1, \dots, B_k$ not in $\{A_1, \dots, A_n\}$ is prime. While `FilmHistory` is 3NF, `Movies` is not in 3NF. The attribute `studio hq` functionally depends on `studio` not prime. To transform `Movies` into 3NF, split off the studio information into `Studios`.

| Title      | Director       | Year | Actor             | Studio      |
| ---------- | -------------- | ---- | ----------------- | ----------- |
| Avengers   | Josh Whedon    | 2012 | Robert Downey Jr. | Marvel      |
| Avengers   | Josh Whedon    | 2012 | Chris Evans       | Marvel      |
| Casablanca | Michael Curtiz | 1942 | Ingrid Bergman    | Warner Bros |
| Star Wars  | George Lucas   | 1977 | Harrison Ford     | LucasFilm   |

| Year | Era           |
| ---- | ------------- |
| 2012 | Blockbuster   |
| 1942 | Golden Age    |
| 1977 | New Hollywood |

| Studio      | Headquarters      |
| ----------- | ----------------- |
| Marvel      | Burbank, CA       |
| LucasFilm   | San Francisco, CA |
| Warner Bros | Burbank, CA       |

A FD $A_1, \dots, A_n \to B_1, \dots, B_k$ is **trivial** if if $\{B_1, \dots, B_k\} \subset \{A_1, \dots, A_n\}$. These always hold but don't say anything about a relation. A relation is in **Boyce-Codd Normal Form** (BCNF) if, for every non-trivial FD $A_1, \dots, A_n \to B_1, \dots, B_k$, attributes $A_1, \dots, A_n$ are a superkey.

Some actors may sign contracts with studios to appear in a certain studio produced films. So `studio, actor, year` $\to$ `title` is a FD. However, `studio, actor, year` is not a superkey; it contains neither `title, year` nor `director, studio, year`. We can transform `Movies` into BCNF by creating a new table `Contracts`.

| Title      | Director       | Year | Studio      |
| ---------- | -------------- | ---- | ----------- |
| Avengers   | Josh Whedon    | 2012 | Marvel      |
| Avengers   | Josh Whedon    | 2012 | Marvel      |
| Casablanca | Michael Curtiz | 1942 | Warner Bros |
| Star Wars  | George Lucas   | 1977 | LucasFilm   |

| Year | Era           |
| ---- | ------------- |
| 2012 | Blockbuster   |
| 1942 | Golden Age    |
| 1977 | New Hollywood |

| Studio      | Headquarters      |
| ----------- | ----------------- |
| Marvel      | Burbank, CA       |
| LucasFilm   | San Francisco, CA |
| Warner Bros | Burbank, CA       |

| Actor             | Studio      | Year | Title      |
| ----------------- | ----------- | ---- | ---------- |
| Robert Downey Jr. | Marvel      | 2012 | Avengers   |
| Chris Evans       | Marvel      | 2012 | Avengers   |
| Ingrid Bergman    | Warner Bros | 1942 | Casablanca |
| Harrison Ford     | LucasFilm   | 1977 | Star Wars  |

[^1]: Codd borrowed the term from mathematics. A relation is a subset of the Cartesian product $\prod_{\alpha \in A} X_\alpha$.
[^2]: Some movies are remade with the same title. See *A Star is Born* ([1937](), [1954](), [1976](), [2018]())
[^3]: Film making is an incredibly expensive craft. Blockbuster movies have budgets in the hundreds of millions. We can safely assume directors + studios can release at most 1 movie a year.
