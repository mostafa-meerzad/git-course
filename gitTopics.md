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

### Committing Changes

Here is some tips to keep in mind while committing

* Commits should be logically separate
* Commits should not be too big nor too small
* Commits are like check-points ( if you screw-up you can revert changes by ease )
* Commits should be descriptive
* Don't mix-up commits ( you find a bug and a typo these shouldn't be included in a single commit, make a separate commit for each )


## Skipping the staging area

You can skip the staging-area if you know what are you doing, but doing so is not recommended

```git
git commit -am "commit message"
```

## Removing files

If you find out that a file is no longer needed you can remove it.

1. remove a file using standard commands
   ```
   rm fileName.ext
    ```

    ```git
        On branch main
    Changes not staged for commit:
    (use "git add/rm <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
            deleted:    file3.txt
            modified:   gitTopics.md

    no changes added to commit (use "git add" and/or "git commit -a")

    ```

    by removing files this way
    you need to run `git add fileName.ext` to let git know that you removed a file

2. remove a file using git command
    ```git
    git rm fileName.ext
    ```
    by doing so you don't need to tell git that you removed a file


## Renaming or Moving files

to rename a file

1. using standard commands
   ```
   mv fileName.ext newName.ext
   git add newName.ext
   ```
2. using git command
    ```
    git mv fileName.ext newName.ext
    ```


untracked files appear under ***untracked file***

staged files appear under ***changes to be committed***

modified files appear under ***changes not staged of commit***

```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   file2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file3.txt

```