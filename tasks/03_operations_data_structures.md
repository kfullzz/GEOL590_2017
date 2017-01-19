---
title: "Task 03: Simple operations and data structures"
date: 18 Jan 2017
author: Drew Steen

**This is currently incomplete: tasks from AR Chapter 3 will be added.**

# Resources
* [An Introduction to R](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf "R Introduction") by the R Core Team
* AR Chapter 2-3
* R4DS Chapter 9-10. As a practical matter we'll work mostly with *tibbles*, but to get there we need to have a good understanding of vectors and data frames.

# Tasks
* Explore vectorization. Explain the differences and the similarities between the following code snippets. What data structure are `a`, `b`, and `c`?
```
a <- 1
b <- 2
c <- a + b
```
and 
```
set.seed(0) # This ensures that 'random' results will be the same for everyone
d <- rnorm(20)
e <- rnorm(20)
f <- d + e
```
* In my opinion, R's ability to assign attributes to objects is enormously helpful. 
    * Name three ways you could use attributes to make data analysis code more reproducible (i.e., easier for yourself and others to understand). 
    * Create a vector of length 5, and use the `attr` function to associate two different attributes to the vector.
* AR exercises:
    * 2.2.2.2 (that is, question 2 in section 2.2.2: "What happens to a factor when you modify its levels?"
    * 2.2.2.3 
    * 2.3.1, plus, *why* does `dim()` return what it does?
    * 2.4.5.1:5 (that is, section 2.4.5, questions 1 through 5)

