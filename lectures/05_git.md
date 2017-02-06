---
title: "Lecture 06: Version control with git and github"
date: 6 Feb 2017
author: Drew Steen
---



# Version control: Why
* ![final.doc](05_git_images/phd101212s.gif "final.doc")
* Collaboration: like Word's 'track changes' for code (or anything else)
* *Unlike* Word's 'track changes', easily roll back to any former state. 
    * Particularly useful for code, where a change can break your code in ways that can be tough to understand
* git + github: easy remote backup for your project

# Git: What
* A set of files and directories under version control is called repository or *repo* - must all be within the same master directory
* Based on 'commits'
* 'Snapshots' of the state of your 
* All this information lives in the `.git` directory - this is the actual repo

# Git: How

## Setting up

* This is highly platform-specific: Follow the instructions in [Chacon Ch. 1.5](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

## Mechanics
* The three states: Working directory, staging area, and git repository
    * Use `git add` to move files in the working directory to the staging area: `git add myscript.R`
    * Use `git commit` to move files from the staging area to the repo: `git commit -m "corrected normalization procedure"`
* 

## Workflow

