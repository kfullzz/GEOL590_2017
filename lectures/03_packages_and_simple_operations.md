---
title: "Lecture 03: Objects, functions and data structures: An extremely brief introduction"
date: 12 Jan 2017
author: Drew Steen
---

# Objects

In [Task 02](https://github.com/adsteen/GEOL590_2017/blob/master/tasks/02_scripts.md "Task 02"), you used some extremely basic functionality of R: you created a few *objects* (which you named `x`, `y`, and `d`), and you used the `c()`, `plot()` and `write.csv()` *functions* to do stuff to those objects.

An object is a thing: a container in which to store data, plots, or anything else that can be represented in your computer's memory. Objects (which are also sometimes referred to as variables) are how we store information. Objects have a name, and R will allow a pretty wide range of possible names. It is even possible, on some systems, to use emoji as object names! There are a few hard-and-fast rules:
* Names must consist of letters, numbers, and the `.` or `_` characters - no special characters (`!`, `@` and the like) allowed.
* Object names must start with a letter or `.` - `1a` is not a valid object name, but `.1a` and `a1` are
* Object names cannot be a *reserved word*. Reserved words have a special meaning in R, and include common words like `if`, `else`, `TRUE`, `FALSE`, etc.
You can read more about the naming rules in the documentation for the function `make.names()` - type `?make.names` at the R console to see it.

## Naming conventions
R gives you plenty of rope to hang yourself with in terms of naming objects. Lots of names are valid, but if you want to write code that other people (including your future self) can easily read, you'll want to use a systematic convention for naming objects. For this class, we'll use the following naming conventions (I haven't yet given you enough information to know what all of these words mean, so just try to file this away in your brain for next week):
* **Names should be descriptive:** 
    * Bad: `a`
    * Good: `absorbance` (or `abs` which in my world is widely understood to mean 'absorbance').
* **Names should be concise:** 
    * Bad: `water_temperatures_3rd_creek_2013_to_2017`
    * Good `temp_3rd_crk`. (Some would argue even that is too long; I tend towards descriptiveness over conciseness in my object names)
* **Names should indicate the object type:** For *this class*, our convention will be:
    * Functions, lists, and data frames use `_` to separate words: `temp_3rd_crk`
    * Vectors and arrays get `.` to separate words: `temp.3rd.crk`
    * Don't use 'camel case' (capital letters to separate: `temp3rdCreek`
    * Note [this](https://twitter.com/gastove/status/476087552978739200) and chuckle. 
Note that Hadley Wickham doesn't follow this last convention: in section 2.1.1 of Advanced R, for instance, I would have named the vector `dbl.var` instead of `dbl_var`, since it stores a vector created by `c(1, 2.5, 4.5)`.

Note that I'm encouraging you to use `.` in variable names. This is sort of a quirk of R - in some other languages, `.` is like a grammatical term - `this.that` would mean 'do `this` to `that`' (and there is one specific context in which a similar thing is true in R, but we don't have to worry about that for now). If you move on to other languages, please be aware of this quirk.

There's more information about style in Chapter [5](http://adv-r.had.co.nz/Style.html) of Advanced R. 

# Functions

Objects are like boxes: they sit there and hold stuff. Functions are like machines: they are also objects, but they exist to do stuff. I like to think of them like a food truck: you pass in some information (your order) at the window, some stuff happens in the back that you can't see, and eventually you get a product (your food). In R, you can identify when a function is being called because it is always followed by parentheses: `plot` is an object, `plot()` is a call to the `plot` function. 

In Task 02, you used several functions: `c()`, `plot()`, and `write.csv()`. As you have seen, with most functions, we put some information into the parentheses: `plot(x, y)` makes a plot of y vs x. If we just call `plot()`, R wouldn't know what to do - it would be like standing at the window of a food truck and refusing to give an order. `x` and `y` are called arguments (or, informally, parameters).

Different functions, of course, require different parameters. Some food trucks only serve one thing; you just need to tell them how many of that thing you want. Other food trucks allow you to customize your order endlessly, in which case you need to pass a whole lot of arguments before they'll start working on your order.

Each function has (or should have) *documentation*, which can be accessed by typing `?function_name` (e.g., `?c`) at the command line. R documentation is usually in a standard format. Always be sure to check the following fields:
* **Usage**, which tells you what arguments the function requires
* **Arguments**, which tells you what those arguments do
* **Value**, which tells you what the function returns. 
It is particularly important to notice what type of *data structure* each argument must be, and what data structure the function will return. For instance, the help file for the `lm()` function, which fits linear models (accessible by typing `?lm`), tells you that the function requires a `formula` argument of class *formula*, some optional arguments, and that it will return an object of class *lm*. (More on what these things mean later). 

# Data structures

Objects in R can store different kinds of data. Base R - that is, the software that you downloaded from CRAN - comes with 5 basic data structures. We'll focus on three of these in this class:
* **atomic vectors**, which we'll generally refer to simply as vectors: 1-dimensional 'rows' of data, a bit like a single column in Excel. All the data in an vector needs to be of the same type, i.e. numeric (numbers), logical (true/false), or character. (We'll also run into *factors*, which are vectors of integers that masquerade as vectors of characters. They were very useful 20 years ago, and now cause endless problems.). Because vectors are one-dimensional, we can access any element of a vector using a single number. For instance:
```
my.vec <- c(4, 5, 6, 7)
my.vec[2]
```
* **lists** act a bit like a bag, into which we can stuff anything we want: vectors, arrays, specialized objects we haven't learned about yet, and, importantly, other lists. These are extremely flexible: anything data you can store in R, you can store in a list.
* **data frames** are a special kind of list, in which each element is a vector, and each vector has the same length. I think of them like a rectangular table in Excel - they are basically two-dimensional, and since each vector has to have the same length, they can't have a ragged bottom edge. Since each column of a data frame is a vector, the elements in each column have to be of the same type - numeric, character, logical, etc. However, each column can be of a different type: try `data.frame(a=1:3, b=letters[1:3], c=c(TRUE, TRUE, FALSE))`

*The tidyverse is organized around data frames*, so we will need to get familiar with them. The value of the data frame for storing scientific data is that it encourages the *tidy* format, in which each row corresponds to a unique observation, and each column corresponds to a unique variable required to identify that observation. For instance, if you sent a survey with 3 questions to 50 people, your data frame would likely have $3\times 50 = 150 rows$. We'll discuss the concept of tidy data more later.

# Packages

When you downloaded R, what you got is called *base R*.* Base R is great, but one of the most valuable features of R is that it is very easy to write *packages*, which add functionality to base R. In their simplest incarnation, packages contain extra functions to do new, useful things. 

We'll explore the structure of packages towards the end of class, but for now we just need to know how to use them. There are two steps to using a function:
* Install the package on your hard drive. This only has to be done rarely. The `install.packages` function can install any package that is hosted on CRAN (the Comprehensive R Archive Network); most packages that are meant for widespread use are hosted on CRAN. It is also possible to easily install packages that are hosted elsewhere: for instance, the **devtools** package contains the `install_github` function that automatically installs packages that are hosted on github. 
* Load the package using the `library` function. This needs to be done for each new session of R: as a practical matter, that means every time you restart your computer, restart R Studio, or change between projects.

So, for instance, the first time we want to use the **ggplot2** packages, which is great for making graphs, we would run `install.packages("ggplot2")`. Then, every time we want to actually use the package in a script, we would run `library(ggplot2)` - note that the package name is surrounded by `"` in the first case, but not in the second case.

Usually R is pretty good about figuring out what package a function belongs to - if we call the `ggplot` function, and the **ggplot2** package is loaded, R will know to look in the **ggplot2** package for the `ggplot` function. Sometimes it is useful to be explicit with R (or, with another person) about what package a function belongs to. In that case, we can use the `::` operator, like so: `ggplot2::ggplot()`.
