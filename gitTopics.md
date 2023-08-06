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
   ```

   ```
    Changes not staged for commit:
    (use "git add/rm <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
            deleted:    file1.txt

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
            file11.txt

    no changes added to commit (use "git add" and/or "git commit -a")
    ```
    now you need to run `git add newName.ext`

2. using git command
    ```
    git mv fileName.ext newName.ext
    ```

untracked files appear under ***untracked file***

staged files appear under ***changes to be committed***

modified files appear under ***changes not staged of commit***

```git

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

## Ignoring files

.gitignore file is a special file that git ignores files of which paths are added to it.

* directories end with a /
* files end with a extension
* patterns can be used

## Git status

`git status`
shows status of the repository

`git status -s`
shows a brief status of repo

## Viewing the staged and unstaged changes

If you want to see exactly what was changed, use `git diff` command.

git diff is usually used to answer two questions:

1. what have you changed but not yet staged
2. what have you changed that you are about to commit


## Viewing history

`git log` shows all the commits made in the repo from latest to oldest

each commit includes

1. commit id
2. author info
3. date of commit
4. commit message
   
some useful options of `git log`

* --online -> shows a compact version of commits
  * id
  * message
* --reverse -> reverses the default order or showing commit (oldest to newest)

## Viewing a commit

you can use `git show` command to see exactly what is inside a commit

Two ways to reference a commit

1. using `head` which points to the last commit, you can also go back as many steps as you want by `head~StepNum` like `head~2` which refers to the second commit before the last commit

2. providing the commit id, you can provide a few characters as long as there is no ambiguity

`git show ` command shows only diff of the specified commit.

If you want to see all the files and directories in a commit 
use

`git ls-tree yourDesiredCommit`

like 

`git ls-tree head` which shows all files and directories in the last commit

you can also view a specific file using `show` command by putting a **:** and providing the path of that file

`git show head:path/testFile.txt`

`git show 0bf3:path/testFile.txt`

## Unstaging files

git restore with -- staged argument unstages the specified file from the staging area

`git restore --staged fileName.ext`
`git restore --staged *.js`
`git restore --staged *`
`git restore --staged .`

## Removing local changes

git restore with no arguments restores specified file/files in working directory

which means it restores to it's previous version

if you want to remove all local changes and start everything from scratch run

`git restore fileName.ext`
`git restore *.js`
`git restore *`

`restore` command can be used to restore all changes to their previous versions saved in the last commit.

if you want to throw everything use `git clean -fd` to remove all directories in the project directory 
> it is a dangerous command to use because there is no way to recover removed files

## Restoring a file to a pervious version

`git restore --source=commitId fileName`
`git restore --source=head fileName`
`git restore --source=head~stepNum fileName`

## Viewing history 

`git log` to show all commits

`git log --oneline` show all commit in a compact way in one line

`git log --oneline --stat` to see which files have been changed

