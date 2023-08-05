# Git Course With Mosh

## What is a version control system

A VCS is a software that tracks project changes, stores them in a repository and allows us to view and change the history of the project.

There are two types of VCS

* Centralized
* Distributed

You can use Git in two ways

* using terminal
* using GUI tools

## Configuring git

First of all we need to configure git by setting

* User Name
* User Email
* Default Editor
* Line Ending

There are three levels for configuration

* System -> all users
* Global -> current user
* Local -> current repository

``` git
git config --global user.name userName
git config --global user.email userEmail
git config --global core.editor "code --wait" "VScode as default editor"
git config --global core.autocrlf true "for windows", input "for mac/linux"
git config --global -e to view or change the settings
```

## Getting Help

If You need help for a git command run the command bellow

```git
git commandName --help
```

or

```git
git commandName -h
```

These commands show a short information about the command

## Initializing A Repository

Go to your project directory and run

```git
git init
```

It initializes an empty repository

## Git Workflow

As in your daily basis, you work on some tasks
![working on a task](./Screenshot%20(159).png)

when it is done you commit those changes, committing it is like creating a snapshot

![task done](Screenshot%20(160).png)

in git there is an extra stage called staging-area

![staging area](Screenshot%20(161).png)

Here we decide which changes go with the same commit

![commit changes](Screenshot%20(162).png)

by committing changes are permanently stored in git repository

![commit changes](Screenshot%20(163).png)

note:

staging area doesn't empty after committing, it contains the last staged changes.

## Staging Files

Git doesn't track file automatically, you have to specifically tell git to track files.

```git
add one file
git add file.ext

add multiple files
git add file1.ext file2.ext

add by using a pattern
git add *.js

add current directory recursively
git add .

add everything
git dd *
```