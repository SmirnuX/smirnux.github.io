---
title: "Git cheatsheet"
categories:
  - Cheatsheet
tags:
  - Git
excerpt_separator: "<!--more-->"
toc: true
toc_sticky: true
---

Some commands for git I found useful.

<!--more-->

## Log

Check history of single line (or range of lines)

```bash
git log -L15,+1:'path/to/your/file.txt'

# Detailed description
# -L <start>,<end>:<file>
# -L :<funcname>:<file>
```

Graph view

```bash
git log --oneline --graph
git log --oneline --decorate --all --graph
```

## Checkout

Create branch and checkout to it

```bash
git checkout -b <branchname>
```

Checkout and merge simultaneously

```bash
git checkout -m <branchname>
```

## Reset

**Warning:** Do not use `reset` commands! As alternative to `git reset --hard` use `git stash -u` to stash all files (untracked included), so it can be reverted later.
{: .notice--warning}

`git reset` list

```bash
git reset --soft    # No changes in index/working tree
git reset --mixed   # Changes index, but not working tree
git reset --hard    # Reset index and working tree
```

Discard unstaged changes for a file

```bash
git checkout "path/to/file"
```

## Detaching HEAD

```bash
git checkout --detach [<branch>]
git checkout [--detach] <commit>
```

Detaching HEAD, leading to "DETACHED HEAD" state.
"DETACHED HEAD" - HEAD usually points to tip of some branch, but if we use git checkout --detach - we can point it to some commit.
In this state we can create commits from another commit, but these commits WON'T BE POINTED BY SOMEONE!

```
          Nothing points here, these commits will be deleted by
          garbage collector
          |
          v    HEAD (refers to branch 'master')
      e---f     |
     /          v
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
```

Use:

```bash
git checkout -b foo  # or "git switch -c foo"  **(1)**
git branch foo                                 **(2)**
git tag foo                                    **(3)**
```

## Clone

Clone to specified folder

```bash
git clone <dest> <folder>
```

Clone current repository (only files, tracked by git) to other folder. Useful, when you want to prepare files for transfer (so it won't include cache, build files and all other stuff that should be in your `.gitignore`)

```bash
# Inside of repository
git clone . <path/to/folder>
```

## Squash

Squash last N commits (interactive) through rebase

```bash
git rebase -i HEAD~<N>
```

## Tagging

Tags are very useful to mark specific commits. It's more lightweight than creating whole new branch.

```bash
git tag -a v1.4 -m "my version 1.4"

# Such tags won't be pushed automatically, do it like this:
git push origin v1.4
```

## Remove tracking files

Such action is often needed, if `gitignore` is updated with path to file, that is already being tracked.

```bash
git rm --cached <file>	# Remove file from tracking, but leave it in index
```

## Handling remotes

Rename remote

```bash
git remote rename origin old-origin
git remote add origin https://dev.robopro.pro/...
```

Push all tags and branches to remote:
(can work not very well)

```bash
git push --set-upstream origin --all
git push --set-upstream origin --tags
```

## Configuration

```bash
git config --global user.name
git config --global user.email

git config --global credential.helper 'cache --timeout 900'
# 15 minutes. Might not be safe
```

## Empty branch

Use the `--orphan` when creating the branch:

```bash
git checkout --orphan YourBranchName
```

This branch may be unpushable (to make it pushable, create commit with following command)

```bash
git commit --allow-empty -m "Initial commit"
```
