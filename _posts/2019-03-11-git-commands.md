---
layout: post
title: Git commands in a nut shell
categories: Introduction
tags: git
---

## First-time Setup

-  first thing to do after installing git

`git config --global user.name "my name"`
`git config --global user.email user@email.com`

-  optionally setup editor:

`git config --global core.editor vim`

-  check out setting

`git config --list`

<!-- more -->
## Repo

-  initializing local file to repository

`git init`

-  clone from remote server/web

`git clone https:/url`

## Status

`Untracked` means that the file has never ever been in the commit. Possibly created from scratch or copy from another file. Use `git add filename` to track.

`Unmodified` means that the file is already tracked and has not been modified since the last commit (?). Files has just been clone are tagged with `Unmodified`. 

`Modified` means that the tracked file is modified in the working directory before staged. Use `git add filename` to stage.

`Staged` means that modified files has been staged. Once all the changes have been made, the user can commit the changes, so that the status goes to `Unmodified`.

### Check Status

checking the status (default in the verbose mode):

`git status`

or short version:

`git status -s`

`A` means new files added to the staging area, `M` means modified files, `?` means untracked files.

`M` in the first and second column mean staged and unstaged modification respectively. 

## Ignoring Files

edit the `.gitignore` file. 

## Viewing Changes

-  view the changes after the modify the files in the `Staged` status use 

`git diff`

-  view the changes between the last commit and files in the `Staged` status (before this commit) use:

`git diff --staged`

## Committing Changes

-  commit followed by message use:

`git commit -m "this commits files in the staging area"`

-  commit all files in the `Modified` stage and skip the `Staged` status.

`git commit -a -m "this commits all modified files in track""`

## Remove Files

-  Remove files in both working dir and Git:

`rm filename` 
`git rm filename` and then commit changes.

-  Remove files from being in tracked by git only

`git rm --cached filename`

-  use matching patterns

`git rm log/\*.log` this, for example, remove all the files end up with `.log` below  the `log/` dir. Note that blackslash is necessary before `*`.

## Rename Files

Note that Git does not explicitly track file movements, so use provided git-style instruction to move files:

`git mv filename1 filename2`

## View Commit History

basics use:

`git log`

## Undo

-  recommit from staging area and the previous commit will be rewritten

`git commit --amend`

-  unstage files in staging area use:

`git reset HEAD filename`

-  unmodify a modified file to last unmodified version

`git checkout -- filename`

## Display Remote Servers

`git remote` it will display the default name Git configures as the server: origin.

`git remote -v` will show the URLs.

## Add & Rename & Remove Remote Repos

-  explicitly add a new remote Git repo use:

`git remote add <shortname> <url>`

e.g. `git remote add pb https://github.com/paulboone/ticgit`

-  rename a remote server use:

`git remote rename pb paul`

-  remove a remote server (from current remote server list):

`git remote remove paul`

## Fetch & Pull

-  fetch data from default server:

`git fetch origin` or fetch from specified server name by replace origin with the server shortname

however, this does not automatically merge those works. You have to manually merge them.

-  automatically fetch and merge from a remote branch that is identical to your current branch, use:

`git pull`

### Push

`git push <remote> <branch>`

by default is `git push origin master`

### Inspect a Remote

`git remote show origin`

## Git Branching

### Create new branches

`git branch new_branch`

### Switch Branches

`git checkout branch_1`

### check branches and which current branch is on

`HEAD` points to the current branch you are on

`git log --decorate` check the branches and `HEAD` pointer.

