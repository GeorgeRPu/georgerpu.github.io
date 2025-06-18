---
layout: book-review
title: Clean Code
author: Robert C. Martin
olid: OL26222911M
categories: software-engineering
buy_link: https://amzn.to/4jWAxUg
started: 2022-01-01
finished: 2022-12-31
released: 2008
stars: 2
status: Finished
---

*Clean Code* is the pre-eminant book on programming, ranked first in many lists of the books every programmer should read. It is the [number one best seller on Amazon in the Software Design & Engineering](https://www.amazon.com/gp/bestsellers/books/491316/ref=zg_b_bs_491316_1) category yet has also received anti-recommendations in recent years by [bloggers](https://qntm.org/clean) and other [authors](https://web.stanford.edu/~ouster/cgi-bin/aposd2ndEdExtract.pdf). Given my current job as a software developer, I decided to read *Clean Code* to make my own opinion. I review each chapter individually.

Certain chapters are written with/by other authors.

#### 1. Clean Code

The first chapter begins by emphasizing the importance of clean code for the small number of readers who dismiss its value. The remainder of the chapter tries to define what "clean code" means: readability, simplicity, and loftier ideals like elegance.

#### 2. Meaningful Names - Tim Ottinger

The second chapter can be summarized "don't make your names too long" and "don't make your names too short". Typing is easy; don't be lazy and drop important context. Knowing what can be left out from variable names is harder. Err on the side of longer names as unnecessary information can always be ignored by the reader.

#### 3. Functions

The most opinionated rule in the whole book is

> The first rule of functions should be small. The second rule is that *they should be smaller than that* [emphasis in original].

This makes no sense to me. Isn't extracting every few lines of code to a function is equivalent to commenting every few lines? Martin calls comments a necessary evil. Why should writing a psuedo-comment in a function name be considered a success? In my short career, I have read long classes filled with similarly named but slightly different methods like `render` in Listing 3-7. It is not a fun experience.

I agree that functions need a maximum size. Functions should not be longer than a screen. But, functions, at least those rarely called, need a minimum size limit too. Functions should do only one thing, but that thing needs to be significant. Functions incur a cost. They disrupt the linear flow of the code, increase the interface surface area, and introduce coupling between modules. Their benefit needs to be greater than the code.

Otherwise, the advice in the chapter is good. The number of function arguments should be minimized. A large number of arguments makes writing unit tests annoying. Avoiding code duplication is important, but don't over do it. [Deduplication is not worth the wrong abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction). The preference for exceptions instead of error codes is ironic as some modern languages like [Rust](https://doc.rust-lang.org/book/ch09-00-error-handling.html) and [Go](https://go.dev/blog/error-handling-and-go) do not have exceptions.

#### 4. Comments

Martin hates comments.

>  Comments are always failures

(which negatively influences his philosophy around functions and classes). I mostly agree, mainly since old comments tend to linger in the code base, even if more for sociological reasons than practical ones.  Good comments are valuable though. I hope Martin's statements doesn't deter readers from attempting to write good comments.

Martin's classification of good and bad comments looks good to me. His advice against HTML comments is out of date as IDES/editors render stylistic markings now when hovering over the documented entity.

#### 5. Formatting

This is the first chapter I whole heartedly agree with. It formalizes all the rules I intuited over the years from writing large programs. The penultimate section of the book hits a gold nugget. Configure IDE/editor tools to enforce formatting standards for you, and you will never have to think about formatting again.

#### 6. Objects and Data Structures

Martin draws a distinction between objects which only expose their methods and data structures, better called structs, which expose their fields.

1. Adding a new `area` function for `Circle`, `Rectangle`, and `Square` structs requires creating only 1 function, albeit with 3 different area formulas. Adding a new `area` method to `Circle`, `Rectangle`, and `Square` objects means modifying 3 classes.
2. Adding a new `Triangle` struct forces us to modify all our geometric functions: `area`, `perimeter`, etc. Adding a new `Triangle` object doesn't require changes to another other objects.

Essentially, Martin argues that object oriented and procedural code are complimentary. It's an interesting idea, although it feels like the only difference is how the functions are grouped. Underneath, we still need $n_{functions} \cdot n_{shapes}$ formulas.

#### 7. Error Handling - Michael Feathers

Overall, this chapter covers the basics of clean error handling in Java. The "Don't Pass Null" section hits on a core idea from [*A Philosophy of Software Design*](https://georgerpu.github.io/blog/2019/books/)—defining errors away. Adjusting code so that it never returns an error is the cleanest error handling.

As for passing `null`s, the solution is better language design. Languages post 2008 often disallow ordinary objects from being `null`. Only nullable types can be `null`. The compiler can check whether nullable types are being assigned to non-nullable types and throw a compile time exception when there is a risk of a `NullPointerException`.

#### 8. Boundaries - James Grenning

This chapter advocates wrapping external dependencies in a module `m`. Application code only uses `m`, pushing all boundary code interacting with third party packages into `m`. Especially if the application code uses the external package in a few specific ways, I highly recommend doing this. Using adapters and wrappers this way is something I started unconsciously, so it's nice to surface this principle to the level of conscious thought.

#### 9. Unit Tests

Martin advocates for test driven development (TDD) where tests are written first. Only after a test is written, the developer is allowed to write production code to make the test pass[^3].  Given that TDD is not widely practiced and that its efficacy at building better software is contested by [empirical](https://neverworkintheory.org/2012/01/25/realizing-quality-improvement-through-test-driven-development.html) [academic](https://neverworkintheory.org/2016/10/05/test-driven-development.html) [research](https://neverworkintheory.org/2021/09/16/analyzing-the-effects-of-tdd-in-github.html), TDD material probably should have been cut to keep the chapter relevant to as broad of an audience as possible.

The chapter also gives the strange advice to invent a domain specific language just for testing. Personally, I prefer Listing 9-3—which the author calls bad—to Listing 9-4. The name `wayTooCold` is not a verb phrase; I find it hard to interpret the 5 character string representation of `hw`'s state.

Otherwise, the advice in the chapter is good. Test suites are important to working software. Unit tests should follow the setup, operate, check structure. Tests can have multiple asserts but only a single concept. All tests should follow the FIRST principles. I wish the book had covered mocking which is essential to unit testing classes in Java.

#### 10. Classes - Jeff Langr

This chapter offers good advice for breaking up large classes. I agree more with the small classes advice than the small functions advice. Classes become large by having more methods which increases interface costs without providing much more functionality. In fact, having fewer but deeper methods helps keep classes smaller by reducing the number of methods. Each class should have a single responsibility it does well.

#### 11. Systems - Kevin Wampler

This chapter emphasizes the role of dependency injection (DI) and aspect oriented programming (AOP) for clean systems.

1. DI is important whenever writing large applications. It allows classes to use dependency objects in fields without worrying about their origins. For Java, I recommend [Dagger](https://dagger.dev) over [Spring](https://www.baeldung.com/spring-dependency-injection) or [Guice](https://github.com/google/guice)[^4].
2. Often the same code needs to be run in many places. An example is timing every method $f$ and publishing the results to a dashboard. AOP lets us wrap $f$ with our timing code rather than put it into $f$. Every call to $f$ first goes to a timing proxy that starts the timer, internally calls $f$, then publishes $f$'s execution time. The explanation of AOP is really good. This is the first time I felt like I grasped the concept.

DI and AOP are useful tools to construct clean systems but are not panaceas to the problem of clean coding.

#### 12. Emergence - Jeff Langr

This is a weird chapter. It mentions 4 rules of simple design, then tries to show how applying those rules creates a design out of thin air. It advocates no duplication when [a little duplication is ok](https://overreacted.io/goodbye-clean-code/). The section "Minimal Classes and Methods" even acknowledges this.

#### 13. Concurrency - Brett Schuchert

This chapter provides recommendations clean concurrent programming. I don't have much experience writing multithreaded code, but I really like this chapter. Java is way past version 5 now, so some of the advice may be out of date.

#### 14. Successive Refinement

In this chapter, Martin works through an example refactoring of a rough draft of an `Args` class to a clean version. The `Args` class parses command line arguments according to a one line `String` schema. The final implementation is mostly ok, but has a few problems.

- Deciding which marshaler to add based on the schema type symbols should be split into its own method outside of the `Args` class.
- Why make `getValue` a static method in `ArgumentMarshaler`? If the data is stored in a field, why not make `getValue` a regular method.
- `ArgumentMarshaler`'s `set` method should take a `String` instead of an `Iterator<String>`. `ArgumentMarshaler` doesn't need to know that the arguments are being iterated over, just the current argument. This issue can be partially fixed by using a for-each loop
- `currentArgument` shouldn't be a field.

I find code in paper books hard to read. The refactoring of `Args` would be better as a companion video than a chapter.

#### 15. JUnit Internals

Martin refactors the class `ComparisonCompactor` from the JUnit library which creates an error message showing the difference between 2 `String`s. I like the final version more than the final implementation of `Args`. My only complaint is that Martin has a disturbing tendency to use fields like global state. One method will set a field for another method to read it. In this example it is not so bad. Each field isx written in only 1 method while being read by many others. But this tendency flares up in other listings throughout the book.

#### 16. Refactoring `SerialDate`

Another chapter refactoring code. `SerialDate` is a class deep inside the no longer developed [JCommon](https://www.jfree.org/jcommon/) library. Martin heavily criticizes this `SerialDate` class[^5]. This is the most realistic refactoring as Martin tries to fix a poor module than improve an already good one. It is rare to refactor good modules to become great. The chapter doesn't print the original or final version of `SerialDate` so Martin's steps are difficult to follow.

#### 17. Smells and Heuristics

This is the best chapter in the book. It summarizes the content of all the previous chapters in $5 + 4 + 36 + 3 + 7 + 9 = 64$ principles. Some principles like *G4: Overridden Safeties* are mentioned in the rest of the book. After reading the entire book (minus the Appendix), I would recommend newbie programmers just read Chapter 17. Overall, the book isn't as bad as the naysayers claim, but there is questionable information. After reading Chapter 17, I would then recommend newbies read *A Philosophy of Software Design*.

---

[^3]: The developer can refactor code while keeping the tests passing.
[^4]: Both Guice and Dagger v2 are developed by Google. Dagger v1 was developed by Square, the company that sells those point of sale tablets. According to a [Reddit AMA](https://www.reddit.com/r/java/comments/1y9e6t/comment/cfjc242/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button), Google plans to replace Guice with Dagger but, as of 2022, both are actively developed.
[^5]: His first move is to rename it to `DayDate.`
