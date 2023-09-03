# Git Course With Mosh

## What is a version control system

A VCS is a software that tracks project changes, stores them in a repository and allows us to view and change the history of the project.

There are two types of VCS

- Centralized
- Distributed

You can use Git in two ways

- using terminal
- using GUI tools

## Configuring git

First of all we need to configure git by setting

- User Name
- User Email
- Default Editor
- Line Ending

There are three levels for configuration

- System -> all users
- Global -> current user
- Local -> current repository

```git
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

or for short details

```git
git commandName -h
```

These commands show information about the command

## Initializing A Repository

Go to your project directory and run

```git
git init
```

It initializes an empty repository

## Git Workflow

As in your daily basis, you work on some tasks
![working on a task](<./Screenshot%20(159).png>)

when it is done you commit those changes, committing it is like creating a snapshot

![task done](<Screenshot%20(160).png>)

in git there is an extra stage called staging-area

![staging area](<Screenshot%20(161).png>)

Here we decide which changes go with the same commit

![commit changes](<Screenshot%20(162).png>)

by committing changes are permanently stored in git repository

![commit changes](<Screenshot%20(163).png>)

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

- Commits should be logically separate
- Commits should not be too big nor too small
- Commits are like check-points ( if you screw something you can revert changes by ease )
- Commits should be descriptive
- Don't mix-up commits ( you find a bug and a typo these shouldn't be included in a single commit, make a separate commit for each )

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

untracked files appear under **_untracked file_**

staged files appear under **_changes to be committed_**

modified files appear under **_changes not staged of commit_**

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

- directories end with a /
- files end with a extension
- patterns can be used

files/directories are not going to be ignored if you add them to **gitignore** file, after they are tracked by git.

first remove them from the staging-area by running `git rm --cached fileName` for single file or `git rm --cached -r directoryName` for a directory.

then commit after that as git recommends itself to tell git that you no longer need to keep track of that file.

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

`git diff` compares working directory with staging area and shows the difference

`git diff --staged` compares staging area with the last commit and shows the difference

## Viewing history

`git log` shows all the commits made in the repo from latest to oldest

each commit includes

1. commit id
2. author info
3. date of commit
4. commit message

some useful options of `git log`

- --online -> shows a compact version of commits
  - id
  - message
- --reverse -> reverses the default order or showing commit (oldest to newest)

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

`git restore .` doesn't restore untracked files to their previous versions.

the following does

if you want to throw everything use `git clean -fd` to remove all directories in the project directory

> it is a dangerous command to use because there is no way to recover removed files

## Restoring a file to a pervious version

`git restore --source=commitId fileName`

`git restore --source=head fileName`

`git restore --source=head~stepNum fileName`

## Viewing history

`git log` to show all commits

`git log --oneline` show all commit in a compact way in one line

`git log --oneline --stat` shows number of changes made to each file as well as commit information

`git log --patch` shows more detail about files in each commit by showing the difference of those files

## Filtering the history

`git log --oneline -number` shows as number commits

`git log --oneline -3` shows three commits

`git log --online --author="authorName"` commits made by the specified author

`git log --oneline --before="2023-4-1"` commits made before specified date

`git log --oneline --after="2023-4-1"` commits made after specified date

`git log --after="yesterday"`

`git log --after="three days ago"`

`git log --after="one week ago"`

`git log --grep="wordInCommitMessage"` returns commit containing specified word in it's commit message

`git log -S"specified text"` returns commits that introduced or removed **specified text** changes that include the given text

`git log -S"hello world" --patch` shows commits that includes **hello world** in the files and shows the difference

`git log --oneline startId..endId` showing commits between specified range of commits

`git log fileName.ext` shows all commit that touch up provided file

`git log --oneline -- fileName.ext` use **--** to separate the file name form the options

`git log --oneline -- .\gitTopics.md --patch` is not going to work because providing **options** after putting **--** git interprets them as fileName

`git log --oneline --patch -- .\gitTopics.md ` this is going to work and show the diff of commits containing the specified file

## Formatting the log output

to customize the `git log` output there are placeholder to use

- %an -> author name
- %ae -> author email
- %H -> commit hash
- %h -> abbreviated commit hash
- %cn -> committer name
- %cd -> commit date
- %s -> commit message

`git log --pretty=format:"one or more placeholders"`

`git log --pretty=format:"%an %h"` to show authorName and the commit hash

you can even colorize the log output

`git log --pretty=format:"%Cgreen %an"` show authorName in green

`git log --pretty=format:"%Cgreen %an %Creset %cd"` show authorName in green and after that rest the output color to default (white)

default supported colors

- %Cred
- %Cgreen
- %Cblue
- %Creset -> reset the color back to default

## Creating aliases

by creating aliases you can run long commands by ease

`git config --global alias.customAlias "log --pretty=format:'%an %h %s'"`

`git config --global alias.customAlias "custom commands"`

`git config --global alias.lg "log --pretty=format:'%an %h %s'"`

from now on you can run `git lg` to get:

- author name
- commit hash
- commit message

information about each commit.

## Viewing a commit

`git show commitId` or `git show head~stepsNum` to view a commit

these command show:

- commit hash
- author info
- date info
- message
- diff of that commit

you can define the filePath that you are interested in

`git show head~2:testPath/files/test.txt`

and git will show the actual file.

if you want to see the files that hsa been changed in that commit

`git show head~2 --name-only` shows only the names of the files

to see the status of files in a specific commit

`git show head~2 --name-status`

## Viewing changes across commits

if you need to see which files have been changed between two commit

`git diff firstCommit secondCommit` difference of files between two commits

`git diff firstCommit secondCommit --name-only` show only names of the changed files

`git diff firstCommit secondCommit --name-status` show status of the changed files

`git diff firstCommit secondCommit fileName` show difference of the specified file between two commits

## Checking out a commit

you can view the complete snapshot of your project (each file at that point)

`git checkout commitId` reverts working directory back to it's sate stored in that commit

### detached head state

you may encounter this situation by **checking out** to a commit or a branch.

Here we have our first commit on the left and the last commit on the right, each commit pointing to it's previous commit, this is how git tracks commits in a project

![commits](<Screenshot%20(174).png>)

All the commits we made so far are part of what is called the **master/ main** branch or the main line of work

the way git represents branches it uses a pointer

![commits](<Screenshot%20(175).png>)

**master** points to the last commit we have created so far

as we create more commits master gos forward

![commits](<Screenshot%20(176).png>)
![commits](<Screenshot%20(177).png>)
![commits](<Screenshot%20(178).png>)
![commits](<Screenshot%20(179).png>)

in git we can have multiple branches so git needs to know in which branch we are currently working on, to do this it uses another special pointer called **head**

**head** points to the current branch we are working on

![commits](<Screenshot%20(180).png>)
![commits](<Screenshot%20(181).png>)

When we **checkout** a particular commit head points to that commit

this situation is called **detached head state**

in this situation **head** is not pointing to a branch anymore it is pointing to a specific commit.

![commits](<Screenshot%20(182).png>)

![commits](<Screenshot%20(182).png>)
![commits](<Screenshot%20(182).png>)
![commits](<Screenshot%20(182).png>)

in this situation we should not create a commit.

only view your code

![commits](<Screenshot%20(183).png>)

because at some point we have to attach **head** back to a branch

![commits](<Screenshot%20(184).png>)

when we do that the commit made there is not reachable by any other commits (dead commit)

also git removes such commits to save space

![commits](<Screenshot%20(185).png>)

`git log --all` to show all commits of your repository

## Finding bugs using bisect

git bisect is good git tool to find bugs in your project across commits

with **bisect** you need to assign _good_ or _bad_ to commits in order to find the bug

`git bisect start` to start the bisect

`git bisect bad` marks the last commit as a bad commit

now you should give git a good commit so it can find the bug

`git bisect good commitId` this commit is assigned as a good commit (no bugs)

now your working directory is restored to a commit in the middle of bad and good commits

`git bisect good` by running this git knows that the middle commit which head is attached to it now is a good commit (no bug)

`git bisect bad` if the bug is present in the project

at the end run

`git bisect reset` the attach head back to master (the last commit)

## Finding contributors using shortlog

Sometimes we need to see all the people contributing to our repo, here is how to do so

`git shortlog ` showing all contributors with all the commit messages the provided

`git shortlog -n` **-b** sorts contributors based on there number of commits

`git shortlog -s` **-s** shows the commit count with the contributor name

`git shortlog -h` see the git help for more options

`git shortlog -s -n --before="one week ago"` to filter the output

## Viewing the history of a file

`git log fileName.ext` to see all the commits that have touched the specified file

`git log --oneline fileName.ext` for shorter review

`git log --oneline --stat fileName.ext` to see the statistics of all the changes made to the file in each commit

`git log --oneline --patch fileName.ext` to see the **patch** (the actual changes) of the file in each commit

## Restoring a deleted file

`git checkout fileName.ext commitId` to restore a deleted file from another commit that includes it

## Blaming

`git blame fileName.ext` to basically blame a contributor for the line of code they wrote, it shows **each line of file** and **who wrote** it with **date and time**

`git blame -e fileName.ext` shows emails of authors of each line

`git blame -L startLine, endLine fileName.ext` only shows lines in the specified range

`git blame -h` help for more options

## Tagging

if you need to bookmark a certain commit in the history of project like a commit that represents a certain version of the project

`git tag tagItself commitId` to tag a commit

`git tag v1.0` tags the last commit

`git tag v0.5 20bcd` tags the last commit

you can reference a commit by it's tag too

`git checkout v1.0`

`git tag` to see all the tags we created

- light weight tag -> just a simple tag
- annotated tag -> a complete object with several properties

`git tag -a tagItself -m "a message" commitId` create an annotated tag

`git tag -n` to show tag messages or commit messages

`git show tagName` shows the tag information (annotated tag)

- tagger
- date of creation
- tag message

`git tag -d tagName` to delete a tag

## Branching

## What are branches

![branches](<Screenshot%20(187).png>)

branches allow us to diverge from the main line of work and start working on something else in isolation

- keep main line as stable as possible
- make a new branch for every new feature, when done merge those branches
- each branch is isolated form the others

## Working with branches

`git branch branchName` create a new branch called branchName

`git branch` to see all the branches

`git switch branchName` to switch to a branchName

`git switch -C newBranch` create and switch to newBranch

`git branch -m oldName newName` to rename the branch

> convention to name a bug fix branch **login/bugfix** follow this pattern

- bugfix/signUp
- bugfix/newFeature

you may want to delete branches after merging them to the main branch

`git branch -d branchName` to remove the specified branch

`git diff firstBranch secondBranch` compares two branches and shows the difference of files in them

`git diff firstBranch secondBranch --name-only` shows the file names that are different between two branches

`git diff firstBranch secondBranch --name-status` shows the files name and status that are different between two branches and will be effected

### Stashing

stashing a file means to store it somewhere save to avoid losing it.

when you switch branches and are not done with the changes `git` will warn you that your changes in the current branch which are not committed yet will be overwritten

`git stash push -m "stash message"` stashes working directory and staging area, newly untracked files are not included in stash by default

`git stash -a -m "message"` to stash all files including the untracked files

`git stash list` to list all your stashed modifications

`git stash show` to inspect stashed modifications

`git stash show 0` to inspect stashed modifications in the latest stash by providing `stash index` 0 is the latest, 1 is the one before the last stash

`git stash apply stashIndex` to apply that specified stash

`git stash drop stashIndex` to remove that one specified stash

`git stash clear` to clear all the stashes

## Merging

merging is all about bringing changes from one branch to another

1. one way merge, if branches have not diverged
2. thee way merge, if branches have diverged
   
`git merge branchName` to merge target branch in to current branch

`git merge --no-ff branchName` merge target branch to current branch and make a merge commit even if fast-forward merge is possible

`git config ff no` to disable fast-forward merging in the current repository

`git config --global ff no` to disable ff for the current user

* if there is a direct linear path from one branch to another branch they are not diverged and can be merged by a ff merge

### Viewing merged branches

typically after merging a branch to main branch you want to remove that branch to avoid future confusions

`git branch --merged` to list all merged branches

`git branch -d branchName` to remove the specified branch

`git branch --no-merged` to list all unmerged branches


### merge conflicts

* if the same line is changed in more than one branch
* changed in one branch but deleted in another branch
* same file is added in two branches with different content

when merge conflict occurs by running `git status` under `unmerged paths` you can find all the files that caused the conflict and need to be addressed

> if you introduce new changes in the conflicted file while resolving the conflicts and commit it
> it is referred as evil-commit because these changes are not introduce anywhere in the history

### aborting merge

`git merge --abort` to cancel the merge process for whatever reason if you are not ready to handle the conflicts, all resolved conflicts will be gone and the repository is back to the state before starting the merge

### undoing a faulty merge

if you merge and find out the the app is not working in this kind of situation you need to undo the merge

* removing the merge commit > rewriting the history as if it has never happened

`git reset --hard head~1`

when resetting the `head` pointer there is three options

1. soft
2. mixed
3. hard

#### soft

 `git reset --soft head~1`
 git is going to have the `head` pointer pointing to a different (specified) snapshot.
 in this case the `staging-area` and the `working-directory` is not going to change

#### mixed

 `git reset --mixed head~1`
 git is going to have the `head` pointer pointing to a different (specified) snapshot.
 in this case the `staging-area` will look like what it looks like in that `snapshot`, but the `working-directory` is not going to change


#### hard

 `git reset --hard head~1`
 git is going to have the `head` pointer pointing to a different (specified) snapshot.
 and `staging-area` as will as the  `working-directory` will be like in that snapshot

---
* revert the merge > make another commit which will cancel all the changes in this commit

`git revert -m 1 head` -m is the parent-number, 1 means the first parent, head is the last commit.

parent is the branch in which this commit is made.

### squash merge

if you have a branch that has no good history, it's commits are too fine-grain or doesn't represent a logical chain set and you don't want this branch to become part of the history of the main branch, `squash merge` can be helpful to combine commits of that branch and make a new commit with a better representation of history and apply it on top of main branch

and you can delete that branch with bad history

> **squash merge** is not a merge commit. it is just a regular commit added on top of (ex, main) branch

*merging bugfix to main*

1. `git switch main` switch to main
2. `git merge --squash bugfix` create a squash merge
3. `git commit -m "the message of merge"` now all those changes are in the staging area and we need to make a commit 

git is not taking the squash-merge as a regular 
merge, even though we combined all the changes in 
bugfix branch git still is going to list this bugfix
 branch under the `unmerged branches`, to avoid
 future confusion remove the bugfix branch after
 squash merging.

### rebasing

rebasing is a way of bringing changes from one branch to another branch. it will result a linear commit history just like `three-way` merge.

with this technic you can change the base of a branch (where the branch is diverging)

1. switch to the branch you want to rebase
2. `git rebase targetBranch` rebase the current branch to `targetBranch`
3. merge the newly added commits.

if there is a conflict resolve it as normal
then run the following commands

* `git rebase --continue` to add next commit on top of main-branch
* `git rebase --skip` to skip the current commit and move on to the next commit
* `git rebase --abort` to cancel the rebase operation

### cherry picking

if there is some changes in another branch and you want to have it in the main branch but you are also not ready to merge these branches you can cherry-pick those changes to the main branch

first switch to the branch that you want to add a feature from another branch to it.

then run the following commands

`git cherry-pick commitID` 

if there is any conflict resolve it and make a commit 

`git commit` let git open the default editor and you may accept the default message or write your own

### picking a particular file from another branch

`git restore --source=BranchName fileName` git is going to restore specified file(s) to the working directory from the latest version of the file in the specified branch