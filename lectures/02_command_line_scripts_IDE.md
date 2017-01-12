---
title: "Section 2 Note: Directories, the Command Line, Scripts, and the Integrated Development Environment"
output: html
date: 7 Jan 2017
author: Drew Steen
---

# Directories

All files on all computers are organized into directories, or which are often presented to the user as folders. Modern operating systems sometimes make this more difficult to see, and they are almost totally invisible on phone/tablet operating systems, but it is true. Directories have a tree-like structure: there is a single 'root' directory. These sub-directories contain sub-sub-directories, which contain sub-sub-directories, and so on. 

On a Windows machine, the root of the main hard drive is usually denoted `C:`. On machines that run Unix-like operating systems, the root directory is specified with a `~`. OSX (the operating system that Macintosh computers run) is loosely based on Linux, which itself is derived from Unix, so the root on a Mac is `~`. 

Much of the structure of the low-level directories (the ones close to the root) is defined by the operating system. On my Mac, running OSX 10.12, the root (actually the 'user root', but we won't need to worry about this distinction) is at `/Users/andrewsteen` and contains directories with names like `Applications`, `Documents`, `Desktop`, and `Library`, among others. So if I save a file on the desktop, it is actually located at `~/Desktop`. We call this expression the *path* of the file. It gives both you and the computer all the information necessary to find a file.

## Good directory management

Your life will be much easier if you create a logical system of directories. For instance, it might make sense to keep all of the files that you generate under your `Documents` directory (or perhaps in the `Dropbox` directory, if you use Dropbox). Within that directory, you might create directories called `personal`, `classes`, and `research`. Under the `classes` directory, you should have one called `GEOL_590`. 

Note that I put an underscore in `GEOL_590`. That was to avoid having a space in the directory name. **Spaces in file names and directory names cause problems.** Do your future self a favor and never use them.

**I will require a specific directory structure for this class.** You should have a single directory for this class - again, `GEOL_590` would be an eminently sensible name for it. Within this directory, you should have directories with the following names:
* **R**
* **data**
* **plots**
* **misc**

The **R** directory is for all of the R scripts that you will write. Raw data goes in the **data** directory. Take a wild guess what directory you should save your plots in. **misc** is for accessory files - notes to yourself about how you should do an analysis, pdf files of key papers, etc.

## Making your file manager more useful
Your file manager (Windows Explorer or File Explorer on Windows, Finder on OSX) is an easy tool to see what files you have on your computer. These tools are useful, but they are set up by default to be a bit child-proofed. You want to set your file manager to do two things that will make your life easier:
* **Show all hidden files**. Most programs create files that are accessed directly by the program itself, but which humans are never meant to change. You should know about these files, so you should set your system to show hidden or system files by default.
*  **Show file extensions**. Most files have a *file extension* - a few characters after a period that indicate what sort of file it is, for instance `.docx` for a Microsoft Word file, `.gif` for a gif, etc. File extensions are really just a hint to the computer as to what sort of file it should expect. If you save a Word document with the filename `I_am_a_troll.xlsx` and then manually change the file extension to `.gif`, your operating system will probably display the filename with the icon appropriate to a gif image. However, it won't magically become a gif file - you will still be able to open it with Word, but not with an image viewing program. 

You should set your system to show hidden files and file extensions. The method for doing this varies by operating system, and anyway this is a good place to practice using Google to figure out how to do what you need to do (a key software development skill!)

# Scripts: The basis of reproducible data analysis

R is a two-headed beast, like Orthrus, the two-headed dog of Greek legend, or the [two-headed monster from Sesame Street](http://muppet.wikia.com/wiki/Two-Headed_Monster). On the one head, it is a statistical computing environment: a computer program designed to help you to do data analysis, not unlike SAS or (*ahem*) Microsoft Excel. On the other head, it is a language that you can use to write new software. In principle you can write R code to whatever you want, but in practice the language R is mainly good for analyzing data and presenting results. 

These two aspects are what makes R great for reproducible data analysis. Using R as an environment, it is easy to interactively analyze data: you type in a command at the *console* (say, `2+2` and R displays the result (`4`). R in interactive mode is great for quick-and-dirty analyses and to learn how the language works. However, it is not reproducible, since (like with Excel) interactive analyses don't leave a record for future workers to follow.

Therefore, the key to doing reproducible data analysis in R is to write a series of R commands in a document, which are automatically executed in order. This is called a *script*. A script is simply a text document containing a series of commands that can be executed by a computer. (In an R script, those commands are all in the R language; you can write scripts for other languages as well.) By convention, R scripts have the file extension `.R`, but again, this is more for your benefit than for the computer's.

## Comments

Actually, scripts aren't *just* a series of commands that can be executed. Crucially, they can also contain text which is *ignored* by the computer. These are called comments, and in R, they are denoted by a `#` - on a given line of a script, the computer ignores anything after a `#`. **Comments are text in software that humans use to talk directly to other humans.** This is tremendously important in reproducible research. 

The legendary computer scientist Donald Knuth famously proposed the concept of *literate programming*, in which, very roughly, software is designed to be equally legible to humans as to computers. (The [famous quote](http://www.literateprogramming.com/knuthweb.pdf) is "Let us change our traditional attitude to the construction of programs: Instead of imagining that our main task is to instruct a computer what to do, let us concentrate rather on explaining to human beings what we want a computer to do.") In a well-written script, code and comments work together to create a document which is easily and precisely understood by both human and machine.

This is particularly important in collaborations: you want your collaborator to easily understand what your code does. "But wait," you say. "I'm a grad student - I don't really have collaborators. I just sit in a hole and write code and hope to get a degree someday." That may be true - but you still have an important collaborator: your future self. **Future you is a different person than current you**, so you will save your future self a great deal of trouble if you write code that can be read and understood by a complete stranger.

The concept of literate programming may seem a bit absurd to a scientist who is new to writing code, and who is confronted with the perfectly cromulent R command `orange %>% group_by(Tree) %>% do(tidy(lm(age ~ circumference, data=.)))`[From the vignette *broom and dplyr* in the **broom** package by David Robinson and colleagues, https://cran.r-project.org/web/packages/broom/vignettes/broom_and_dplyr.html][2]. How could such an abomination be equally understandable to humans and computers? In fact, once you learn the language, it becomes clear that expression is clearly and efficiently written. The purpose of comments, then, is to explain *why* a given line or section of code is in a script - in the larger picture, what was the author of the code trying to do? Well-written code clearly explains (to the computer and to humans) what the code is supposed to do; comments expalin why it makes sense to do what the code says to do. **Well-written comments are therefore as essential as well-written computer code to reproducible data analysis.**

## Running R scripts from the command line

A script is just a series of commands stored in a text file. A script is to a data analysis project as a blueprint is to a building. Having a script isn't enough, you need to tell R to execute the commands. One way to do this is via the command line.

## The command line: your direct line to your operating system

Back ibefore graphical user interfaces were available, the command line was the only way to tell your operating system to do stuff (for instance, launch a program or copy a file). Nowadays it is easy to do these sorts of thing via mouse clicks, but it is still helpful to have a direct way to issue unambiguous commands to the operating system. 

We access the command line via the *shell*, a simple-seeming program that converts typed text into commands that the operating system can understand. If we want to run an R script, we essentially say: 'Operating system: please ask R to run all of the commands in this text document in order'. The precise prodcedure we use depends on what operating system we're using. On OSX, if we have a written an R script called `my_analysis.R` and saved it in the director at `~/Documents/classes/GEOL_590_1/R` we would open the program called Terminal (click on the magnifying glass to search for the Terminal app), and type `Rscript ~/Documents/classes/GEOL_590_1/R/myanalysis.R`. (We could also navigate to the directory in which we have saved `myanalysis.R` using the `cd` command, and then simply type `Rscript myanalysis.R`. There's a decent intro to shell commands [here](http://www.dummies.com/computers/macs/mac-operating-systems/how-to-use-basic-unix-commands-to-work-in-terminal-on-your-mac/).)

Super! In theory, we can use any text editor to write an R script, and then execute it at the command line, instructing it to save all of our results in well-organized directories. In reality, we'll write our big, complicated R script, run it, and find... that there's an error. We'll hunt down the error, make a guess about how to fix it, run the code again... and there'll be another error. Seriously, no one gets it right on the first try, and most people need a lot of tries to get all but the simplest scripts to do what they're meant to do. (At least, I do, and I'm pretty sure I'm not the only one.) It would be nice to have a way to use R interactively and write scripts at the same time.

# The IDE, or Integrated Development Environment

In truth, running scripts from the command line is pretty clunky. There are a lot of common tasks that could be made easier. This is the *raison d'&ecirc;tre* of the Integrated Development Envrironment (IDE). IDEs exist to simplify the process of writing code (text) and getting computers to run it.

There are several IDEs for R, but RStudio (available for free) is far-and-away the best one. Like any good IDE, RStudio has a deep, rich set of features that make it easier to write R code that does what you want it to do. However, at the core, RStudio contains two important parts: a text editor (not unlike TextWrangler or Notepad++) and a *console* which reports output from R. 

## Projects and the working directory

Before we do any calculations with RStudio, let's talk about one of it's most useful features: *Projects*. RStudio Projects are a great way to organize your real-world data analysis projects, and you should have a different RStudio Project for each actual project. Basically, RStudio Projects keep your data, scripts, and results organized between projects (as long as you keep everything related to different projects in different directories, as you should!). So, the first thing you do when you open RStudio is to make a new project. 

To create a new project for this class, 
* Open RStudio, and go to File -> New Project
* Choose Existing Directory (since you've already set up a directory for this class), browse to the directory for this class, and click Create Project.
* **If the directory is on Dropbox**, you need to take one more step: Turn of Selective Sync for the .Rproj file in your project directory. To do this,
    * Quit RStudio
    * Go to the Dropbox App
    * Choose Settings -> Preferences. Under Account, clikc Selective Sync: Change Settings, navigate to your project folder, and unclick the box next to .Rproj.user. This will prevent RStudio and Dropbox getting into a fight about the correct current state of your RStudio Project.

See more about RStudio Projects [here](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects). 

## Quickstart guide to using RStudio

When you open RStudio, on the left half of the screen you will see the R Console. Again, this is just a place where you can have a conversation with R: you can enter commands, and R can give you results, warnings, error messages and messages. Whenever R starts up it prints some text including the version number of R you are using, some license information, and some miscellaneous tips. This is just like what you saw when you started R from the command line. Try typing `2+2` and press enter (or return). Look, you got an answer! Super. 

Now let's create a script. Go to File -> New File -> R Script. You should see a new window in the upper-left-hand corner of the RStudio window, containing your new, unsaved script. Type `2+2` again and press enter. Nothing happened. Why?

You have made a text file with the text `2+2` in it, but you haven't told the computer to do anything with it. Click on the line that contains `2+2`, but now press command and enter at the same time (Mac) or ctrl+enter (Windows). This sends the command to the console, as if you had typed it in at the console.

**Being able to write code in a script and execute it one line at a time is incredibly useful.** When I am doing data analysis, I want to end up with a reproducible script - but I also want to test my code as I go, to make sure it does what I think it is doing. By composing code in the script window and executing it line by line in the console, we can simultaneously write and test our code, giving us the best of R's 'heads', the statistical analysis environment and the programming language.

## Some very basic basics of the R language

Let's do a few more basic things with an R script. Notice the window in the upper right-hand corner. It has several tabs - the one labeled 'Environment' should be selected; if not, click on it. It should say 'environment is empty'. This is R's way of saying 'I do not have any results in my memory right now'. This, despite the fact that we have already asked R to do calculate the value of 2+2. 

When we type `2+2`, R calculates the answer, and then instantly forgets about it. We have not told R to remember the result of the calculation, so it didn't. In fact, R did go slightly above and beyond the call of duty: it printed the result of the calculation to the console, even though we didn't ask it to do so. 

*If you don't tell R to do anything with the result of a calculation, it will (usually) print the result to the console.* This is called automatic printing, and it is very handy, but it also sort of misses the point of using R for reproducible analysis. Most scripts have many lines of code - I think my papers tend to average in the high hundreds of lines - so we need R to remember the results of one calculation so that we can use them for the next calculation. To do this, we need to **assign the results of an operation to a name** - that is, we need to tell R something like "add 2+2, and assign a name to the result."

The syntax for this is `a <- 2+2`, where `<-` is the *assignment operator*. `<-` is meant to represent an arrow, and the directonality of the arrow is important. I think of the arrow as implying that the value of a calculation is being 'poured' into a variable: 'add 2+2, and put the result into a variable called `a`'. 

There are actually five different assigment operators in R, but I strongly discourage you from using any of them except for `<-`. You can use a backwards arrow to reverse your expression (`2+2 -> a`) but, except in special situations, this just makes your code more confusing. You will also see other people's code online (particularly older code) that uses `=` as an assignment operator, but you shouldn't do this, for two reasons. 
*First, it obscures the directionality of the calculation - with `<-`, it is easy to see that R is performing the calculation on the right hand of the assignment operator, and putting the result into the variable on the left hand. (If we write `a <- b`, it is easy to see that we are taking the value of `b` and assigning it to `a`, but with `a = b` it is harder to see whether the value of `b` is being assigned to `a` or vice versa). 
*Second, we frequently use the `=` operator in a different context in R (more on that later), and we don't want to get the two meanings of `=` confused.

Try executing `a <- 2+2`, either in the script window (command+enter) or the console. Now look at the workspace: you see there is a column for **values**, and `a` is listed as having a value of 4. Great! Now you can do stuff with `a`. Try typing `2*a` at the console. You're on your way to performing your data analysis reproducibly.

## Leftover proof of concept: Running R from the command line

Truth be told, I wasn't sure of where to put this bit of text, so I'm open to suggestions (you'll have a good way to make them once you learn how to use Git and Github). Anyhoo, it is worth proving to yourself that the R console in RStudio really is just a 'window' that looks onto R, which is a totally separate program. To do this: go back to the command line and simply type `R` (OSX) or `R.exe` (Windows). You'll see a window that looks just like the R console in RStudio, because that's what it is. 

Did it work? Great! Now you will never have to do this again. There are specialized cases where it makes sense to run R scripts from the command line (beyond the scope of this course; usually you would do this when you want another program or script to automatically run an R script) for almost all users, almost all of the time, the best way to interact with R is via RStudio.



