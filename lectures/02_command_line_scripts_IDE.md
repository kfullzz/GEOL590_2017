---
title: Section 2 Note: The Command Line, Scripts, and the Integrated Development Environment
date: 7 Jan 2017
author: Drew Steen
---

# Directories

All files on all computers are organized into directories, or which are often presented to the user as folders. Modern operating systems sometimes make this more difficult to see, and they are almost totally invisible on phone/tablet operating systems, but it is true. Directories have a tree-like structure: there is a single 'root' directory. These sub-directories contain sub-sub-directories, which contain sub-sub-directories, and so on. 

On a Windows machine, the root of the main hard drive is usually denoted `C:`. On machines that run Unix-like operating systems, the root directory is specified with a `~`. OSX (the operating system that Macintosh computers run) is loosely based on Linux, which itself is derived from Unix, so the root on a Mac is `~`. 

Much of the structure of the low-level directories (the ones close to the root) is defined by the operating system. On my Mac, running OSX 10.12, the root is called `Macintosh HD` and contains `Applications`, `Library`, `System`, and `Users`, as well as a bunch of hidden files. My `Documents` directory is actually located at `~/Users/andrewsteen/Documents` for instance. This expression - `~/Users/andrewsteen/Documents` - is known as a 'path', and gives both you and the computer all the information necessary to find a file.

## Good directory management

Your life will be much easier if you create a logical system of directories. For instance, it might make sense to keep all of the files that you generate under your `Documents` directory (or perhaps in the `Dropbox` directory, if you use Dropbox). Within that directory, you might create directories called `personal`, `classes`, and `research`. Under the `classes` directory, you should have one called `GEOL_590`. 

Note that I put an underscore in `GEOL_590`. That was to avoid having a space in the directory name. **Spaces in file names and directory names cause problems.** Do your future self a favor and never use them.

**I will require a specific directory structure for this class.** You should have a single directory for this class - again, `GEOL_590` would be an eminently sensible name for it. Within this directory, you should have directories with the following names:
* **R**
* **data**
* **plots**
* **misc**

The **R** directory is for all of the R scripts that you will write. Raw data goes in the **data** directory. Take a wild guess where you should save your plots to. **misc** is for accessory files - that note to yourself about how you should do an analysis, or maybe a couple of key papers about your project.

## Making your file browser more useful:
Your computer contains many files that are important and normally accessed only by the system itself. However, you are on your way to becoming a superuser, so you'll want to see them. Set your file browser (Finder on OSX, Windows Explorer on Windows) to show all hidden files. Futhermore, most of your files have a *file extension* - a few characters after a period that indicate what sort of file it is, for instance `.docx` for a Microsoft Word file, `.gif` for a gif, etc. 

File extensions are really just a hint to the computer as to what sort of file it should expect. If you save a Word document with the filename `I_am_a_troll.xlsx` and then manually change the file extension to `.gif`, your operating system will probably display the filename with the icon appropriate to a gif image. However, it won't magically become a gif file - you will still be able to open it with Word, but not with an image viewing program. 

By default operating systems typically hide file extensions. This is fine for many users, because the operating system shows a different icon for different file extensions, and may 'preview' the file as well. However, you will be using file extensions that your operating system doesn't know about, so your life will be much easier if you can see all file extensions. Google "show all file extensions in [your operating system]" to figure out how to do this on your system.

# R in interactive mode

# Scripts: The basis of reproducible data analysis

R is a two-headed beast, like Orthrus, the two-headed dog of Greek legend, or the [two-headed monster from Sesame Street](http://muppet.wikia.com/wiki/Two-Headed_Monster). On the one head, it is a statistical computing environment: a computer program designed to help you to do data analysis, not unlike SAS or (*ahem*) Microsoft Excel. On the other head, it is a language that you can use to write new software. In principle you can write software to whatever you want, but in practice the language R is mainly good for analyzing data and presenting results. 

These two aspects are what makes R great for reproducible data analysis. Using R as an environment, it is easy to interactively analyze data: you type in a command at the *console* (say, `2+2` and R displays the result (`4`). R in interactive mode is great for quick-and-dirty analyses and to learn how the language works. However, it is not reproducible, since (like with Excel) interactive analyses don't leave a record for future workers to follow.

Therefore, the key to doing reproducible data analysis in R is to write a series of R commands in a document, which are automatically executed in order. This is called a *script*. A script is simply a text document containing a series of commands that can be executed by a computer. (In an R script, those commands are all in the R language; you can write scripts for other languages as well.) By convention, R scripts have the file extension `.R`, but again, this is more for your benefit than for the computer's.

## Comments

Actually, scripts aren't *just* a series of commands that can be executed. Crucially, they can also contain text which is *ignored* by the computer. These are called comments, and in R, they are denoted by a `#` - on a given line of a script, the computer ignores anything after a `#`. **Comments are text in software that humans use to talk directly to other humans.** This is tremendously important in reproducible research. 

The legendary computer scientist Donald Knuth famously proposed the concept of *literate programming*, in which, very roughly, software is designed to be equally legible to humans as to computers. [The famous quote is "Let us change our traditional attitude to the construction of programs: Instead of imagining that our main task is to instruct a computer what to do, let us concentrate rather on explaining to human beings what we want a computer to do." Knuth (1984) Literate Programming. The Computer Journal 27:2.][1] In a well-written script, code and comments work together to be equally readable to the computer and to the human. 

The concept of literate programming may seem a bit absurd to a scientist who is new to writing code, and who is confronted with the perfectly cromulent R command `orange %>% group_by(Tree) %>% do(tidy(lm(age ~ circumference, data=.)))`[From the vignette *broom and dplyr* in the **broom** package by David Robinson and colleagues, https://cran.r-project.org/web/packages/broom/vignettes/broom_and_dplyr.html][2]. How could such an abomination be equally understandable to humans and computers? In fact, once you learn the language, it becomes clear that expression is clearly and efficiently written. The purpose of comments, then, is to explain *why* a given line or section of code is in a script - in the larger picture, what was the author of the code trying to do? Well-written code clearly explains (to the computer and to humans) what the code is supposed to do; comments expalin why it makes sense to do what the code says to do. **Well-written comments are therefore as essential as well-written computer code to reproducible data analysis.**

## Running R scripts from the command line

It is important to remember: a script is just a series of commands stored in a text file. A script is to a data analysis project as a blueprint is to a building. Having a script isn't enough, you need to tell R to execute the commands. One way to do this is via the command line.

## The command line: your direct line to your operating system

Back in the day before graphical user interfaces were available, the command line was the only way to tell your operating system to do stuff (for instance, launch a program or copy a file). Nowadays it is easy to do these sorts of thing via mouseclicks, but it is still helpful to have a direct way to issue unambiguous commands to the operating system. 

We access the command line via the shell, a simple-seeming program that converts typed text into commands that the operating system can understand. If we want to run an R script, we essentially say: 'Operating system: please ask R to run all of the commands in this text document in order'. The precise prodcedure we use depends on what operating system we're using. On OSX, if we have a written an R script called `my_analysis.R` and saved it in the director at `~/Documents/classes/GEOL_590_1/R` we would open the program called Terminal (click on the magnifying glass to search for the Terminal app), and type `Rscript ~/Documents/classes/GEOL_590_1/R/myanalysis.R`. (We could also navigate to the directory in which we have saved `myanalysis.R` using the `cd` command, and then simply type `Rscript myanalysis.R`. There's a decent intro to shell commands [here](http://www.dummies.com/computers/macs/mac-operating-systems/how-to-use-basic-unix-commands-to-work-in-terminal-on-your-mac/).)

Super! I theory, we can use any text editor to write an R script, and then execute it at the command line, instructing it to save all of our results in well-organized directories. In reality, we'll write our big, complicated R script, run it, and find... that there's an error. We'll hunt down the error, make a guess about how to fix it, run the code again... and there'll be another error. Seriously, no one gets it right on the first try, and in a complicated script most people need a lot of tries to get it right. (At least, I do, and I'm pretty sure I'm not the only one.) It would be nice to have a way to use R interactively and write scripts at the same time.

# The IDE, or Integrated Development Environment

In truth, running scripts from the command line is pretty clunky. There are a lot of common tasks that could be made easier. This is the *raison d'&ecirc;tre* of the Integrated Development Envrironment (IDE). IDEs exist basically to simplify the process of writing code (text) and getting computers to run it. 