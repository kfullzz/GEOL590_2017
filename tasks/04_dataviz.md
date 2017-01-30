---
title: "task 04: Data Visualization"
date: 27 January 2017
author: Drew Steen
---



# Required reading
* Tufte, The Visual Display of Quantitative Information, Ch 4-6 (on Canvas)

# Recommended reading
* Tufte on Powerpoint (on Canvas)

# Resources
* [Getting started with ggplot2](https://rpubs.com/hadley/ggplot-intro) by Hadley Wickham
* [Cookbook for R](http://www.cookbook-r.com/Graphs/) Graphs chapter
* Many more web resources on **ggplot2:** google will help you. I found [this tutorial](http://tutorials.iq.harvard.edu/R/Rgraphics/Rgraphics.html) to be particularly good.

**Note:** some web resources (including the Wickham ggplot2 book) encourage using ggplot2's `qplot` syntax, which is simpler (but, in my mind, more confusing) than the standard syntax. I encourage you to ignore this syntax; in my opinion it just makes it more difficult to understand **ggplot2**.

# Tasks
* Find a plot in a published paper or scientific book. Evaluate it based on the principles Tufte lays out in the required reading.
* **Create a single, well-commented script** (or R Notebook, if you know how to do that) that does the following
* Determine how many rows the `diamonds` data set that comes loaded with **ggplot2** has
* Use the following code to create a reproducible subset of `diamonds`. *Explain each line of the code in words*.
```
set.seed(1410)
dsmall <- diamonds[sample(nrow(diamonds), 100), ]
```
* Use `dsmall` to create the following plots:
    * A scatterplot of `y` vs `x`, colored by z values and faceted by `cut`
    ![](../plots/t4p1.png "Plot 1")
    * A scatterplot of `price` vs `carat`, colored by `cut` and smoothed (using the `"lm"` method, without standard error bars)  
    ![Alt text](../plots/t4p2.png "Plot 2")
    * A density plot of `carat`, faceted and colored by `clarity`
    ![Alt text](../plots/t4p3.png "Plot 3")
    * A boxplot of `price` as a function of `cut`
    ![Alt text](../plots/t4p4.png "Plot 4")
    * A scatterplot of `y` versus `x`. The points should be red (`colour = "red")`, the color of the smoothing line should be blue (`colour = "blue"`), and the line should be dashed with fat dashes (`linetype=2`). The x and y labels should be set manually as well. *The trickiest part of this may be to figure out where `colour = "red"` etc should go in the code. Think about mapped vs static aesthetic values.*
    ![Alt text](../plots/t4p5.png "Plot 5")

## Ugly plot contest:
Make the worst plot you possibly can in ggplot2. This plot should be awful in two independent respects:
    *  It should represent the data misleadingly (this can sometimes be difficult with ggplot2, but be creative)
    *  It should be as ugly as possible. (`theme` will be helpful here.)
**Print this plot out and bring it in on Friday. We'll make a gallery of bad plots and the 'winner' will get a prize.


