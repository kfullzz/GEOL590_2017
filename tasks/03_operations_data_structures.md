---
title: "Task 03: Simple operations, data structures and subsetting"
date: 18 Jan 2017
author: Drew Steen

# Resources
* [An Introduction to R](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf "R Introduction") by the R Core Team
* AR Chapter 2-3
* R4DS Chapter 9-10, dealing with *tibbles*. As a practical matter we'll work mostly with *tibbles*, but to get there we need to have a good understanding of vectors, lists and data frames.

# Tasks

## Simple operations and data structures: AR Chapter 2
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
    * 2.2.2.2 (that is, question 2 in section 2.2.2): "What happens to a factor when you modify its levels?"
```
f1 <- factor(letters)
levels(f1) <- ref(levels(f1))
```
    * 2.2.2.3: What does this code do?
```
f2 <- rev(factor(letters))
f3 <- factor(letters, levels = rev(letters))
```
    * 2.3.1.1: What does `dim` return when applied to a vector, **and why**?
    * 2.4.5.1: What attributes does a data frame possess?
    * 2.4.5.2: What does `as.matrix()` do when applied to a data frame with columns of different types?
    * 2.4.5.3: Can you have a data frame with 0 rows? What about 0 columns?
    

## Simple operations
* **Read in your own data and figure out what type it is**.
    * Use `read.csv()` to read the file `2016_10_11_plate_reader.csv` in the github `data` directory, and store it in memory as an object. This is an output from an instrument that I have, that measures fluorescence in each well of a 96-well plate. (Hint: use the optional argument `skip = 33`. What effect does that have?)
    * What kind of object did you create? What data type is each column of that object? (`str()`)
    * Now install and load the **tidyverse** package. (Remember, this package is a little unusual - it is a wrapper for about a dozen interrelated packages. Here you're using the **readr** package)
    * Read the same file using the `read_csv` function. How is the resulting object different?

## Subsetting
Note that `mtcars` is a data set that comes with R. You don't have to do anything special to load it into memory.
* Why does `nrow(mtcars)` give a different result than `length(mtcars)`? What does `ncol(mtcars)` return? What is each telling you, and why? 
* Create a vector that is the `cyl` column of `mtcars` in two different ways:
    * using the `$` operator
    * using `[]` subsetting
* Create a data frame that contains all the columns of `mtcars`, but only with cars that weigh less than 3.0 **OR** more than 4.0 (weight is in the `wt` column)
* Create a data frame that contains all the **rows** of `mtcars`, but only the `mpg` and `wt`
* Which cars in the database get gas mileage (`mpg`) equal to the median gas mileage for the set? (Use `median` and `which`).s
* AR 3.1.7.1: Fix the following common subsetting errors (note that `mtcars` is a dataset that is built into base R; you don't have to do anything special to load it:
```
mtcars[mtcars$cyl = 4, ] # Trying to create a data frame of cars with 4 cylinders only
mtcars[-1:4, ]
mtcars[mtcars$cyl <= 5]
mtcars[mtcars$cyl == 4 | 6, ] # The | is an 'or' operator - you want a data frame of cars with 4 OR 6 cylinder engines
```


