---
title: Git Cheat Sheet
date: "2020-04-21T22:40:32.169Z"
template: "post"
draft: false
slug: "git-cheat-sheet"
category: "Git"
tags:
    - "Git"
    - "Devops"
    - "Developer"
description: "This blog will help in learning Git fundamentals and some useful commands."
socialImage: "/media/gutenberg.jpg"
---

## Git Concepts

Git is a very popular version controller system used widely ranging from individual to large companies. So it is recommended that from college students to working employees everyone should be familiar with Git. So let's start with the basics and some useful commands of Git.<br>
<br>
Basically, Git has 3 states which are as follows.

-   Stage - This state contains the changes of local repository which has to be committed on git
-   Commit - This state contains all the commits of the local repository
-   Remote - All the commits has to be pushed to remote repository which is called Remote state

Every command of git works in these three states. These terminologies have been used in below sections to explain some of the basic and useful commands.

## Basics of Git

To start with Git, everyone should know at least following commands.

-   `git clone <remote-repository-url> <optional folder-name>`<br>
    To clone or download the remote repository on a local machine this command is used. By default it will create a folder with the same name of the remote repository but if you want your local repository folder name something else you can state that in command after the url.

-   `git add <file-name/.>`<br>
    To stage the local repository changes this command is used. We can stage particular file changes by stating that file name or using '.' we can stage all the changed files local repository has.

-   `git commit -m <message>`<br>
    To commit the staged changes this command is used. We can set the commit message using '-m' in command. If we don't pass '-m' in command, it will open the default editor (ex. Notepad++) for commit message to be entered. Also we can pass one more '-m' after the first message which is for optional description message of the commit.

-   `git push`<br>
    This command will push all the local commits to remote repository (Ex. Github).

-   `git checkout <branch-name>`<br>
    To switch between the different branches this command is used. If you want to create a new branch just pass '-b' before the branch-name in the command.

-   `git diff`<br>
    This command will show all the difference between the current staged and last committed changes.

-   `git show <optional commit-id>`<br>
    To show all the changes done in a commit this command is used. If commit-id is not passed it will show the last commit information.

-   `git log -all`<br>
    To check all the previous commits that occured in the local repository this command is used.

-   `git merge <source-branch>`
    When you are dealing with multiple branches and you need to add all the changes done in one branch to another branch this command is used. First you will need to checkout in the destination branch in which you wanted all the changes to come. Then run this command stating the source-braach name. If there are any conflicts it will ask you to resolve those. Once it is done all the changes are pushed in stage state and then you will need to commit.

-   `git fetch`<br>
    To check whether there are any updates on remote repository as compared to local repository this command is used. But it will not replace those remote changes to the local repository.

-   `git pull`<br>
    This command consist of two different commands and those are **git fetch** and **git merge**. It will check for changes on remote and will merge those into the local repository.

## Some useful commands and tricks

-   `git ls-files`<br>
    To check for the files which are being tracked by git on the local repository this command is used.

-   `git commit -am <message>`<br>
    This command is called express commit. It will first stage and then commit those changes in a single step. You can pass the additional commit description with '-m' parameter in command.

-   `git reset <mode> HEAD~1`
    To undo the commits of local repository reset command is used. It has three majorly used modes which are soft, mixed and hard. <br>

    -   `--soft` - This will remove the last commit from current branch and all the changes will be in stage state.
    -   `--mixed` - This is the default mode. This will remove the last commit from the current branch and will not stage the changes. This means if you want those changes to be committed again then you will need to add those changes to stage state first and then commit.
    -   `--hard` - This will remove the last commit from the current branch permanently along with all unstaged changes too.

-   `git reset HEAD <file-name>`<br>
    To backout or unstage the changes done in any file this command is used. This will only unstage the changes. To remove all changes done in that file use `git checkout -- <file-name>`

-   `git log --oneline --graph --all`<br>
    This command will show a one line all commit logs along with '\*' and '-' used graphical representation of all branches it consists of.

-   `git config --global alias.<alias-name> '<command>'`<br>
    When any particular command is very long you can assign it to another alias to shorten the command.
    For Example: _git config --global alias.loghist 'log --oneline --graph --decorate --all'_<br>
    This command creates **loghist** alias and that can be used instead of **log --oneline --graph --decorate --all**. To use alias use `git <alias-name>` for above example **git loghist**.

-   `git mv <file1-name> <file2-name>`<br>
    If file1-name is in commit state and you want to rename the file then this command will rename the committed file1-name to file2-name and will again stage the changes.
    `
-   `git rm <file-name>`<br>
    To delete the commited file this command is used. Once the file is deleted it will stage the delete file changes.

-   `git stash`<br>
    If you want to temporarily hold the unstaged local changes and do it later. Then this command will get you back to the last committed changes.

-   `git stash pop`<br>
    If you want to get back to the holded local changes done this command will do that for you.

## Conclusion

Git is the most useful system for an individual developer to organization level groups, from student to open source contributor. It simplifies the source code management in every software development process.
