---
title: "Task 02: Command Line, Scripts, and IDE"
author: Drew Steen
date: 11 January 2017
---

# Resources
* Lecture 02
* Advanced R (AR) Chapter 1
* R for Data Science (R4DS) Chapter 1

# Tasks: Due Friday, Jan 20
* Use a text editor (not RStudio) to write the R script shown below, and run it from the command line. (See below for the script)
* Launch R from the command line. Use it to calculate the answer to `2+2`, and then quit using `q()`
* Add `2+2` in the RStudio console, and then quit using an R command
* Use RStudio to write a script to do the following:
    * Add 2+2, and assign the result to a variable called `my.variable`
    * Divide `my.variable` by 3 and automatically print the result to the console
* Save the script in your R directory with the filename `task01_script.R`
* Run `task01_script.R` in three different ways:
    * Line-by-line, from the script editor window
    * All at once, using the *Source* button in the script editor window
    * All at once, using the `source` function. *Type `?source` in the console to learn about the `source()` function.*
* Install the `tidyverse` packages.



## Suggested script

```
####
# This is an R script to demonstrate some basic operations in R
####

# Make three vectors 

x <- seq(from=1, to=20, length.out=10)
y <- rnorm(10)
labels <- letters[10] 

d <- data.frame(x, y, labels)

# Save a plot
png("test_plot.png", height=3, width=4, units="inches", res=300)
plot(x, y)
dev.off()

# Save a .csv file with the data
write.csv("test_data.csv")
```