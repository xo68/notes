<h1 align="center"> Git </h1>

# Table of content

<!-- vim-markdown-toc GFM -->

* [Introduction](#introduction)
* [Tips](#tips)
  * [Browse the history](#browse-the-history)
  * [Terminology](#terminology)
* [git commands](#git-commands)
  * [git init](#git-init)
  * [git clone](#git-clone)
  * [git worktree](#git-worktree)
  * [git revert](#git-revert)
* [Resources](#resources)

<!-- vim-markdown-toc -->

# Introduction

# Tips

## Browse the history

**Great alias !**  
`$ git config --global alias.lg "log --graph --date=relative --pretty=tformat:'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%an %ad)%Creset'"`

`$ git lg -10`: Display the last 10 commits  
`$ git lg <my_file>`: Display changes related to specific file(s) or directories  
`$ git lg <my_branch>`: Same for 1 or multiple branches  
`$ git lg master..dev`: Specific intervals (works as well with tags)  
`$ git lg --since='1 week ago' --all`: Various alternatives are possible

`--branches`: For local branches  
`--all`: For remotes stuffs (branches, tags, stash)  
`--merges`: Check merges

## Terminology

`HEAD`: The current branch, represented in `.git/HEAD` and as well a pointer to the last commit  
`HEAD^`: Second last commit, equivalent to `HEAD~1`  
`HEAD^^`: Third commit from the top  
`HEAD~3` = `Head^^^` (No number means 1)  
`HEAD~5..HEAD~2`

# git commands

## git init

**git-init - Create an empty Git repository or reinitialize an existing one**

`--bare`: Create a bare repository  
_Useful in case of working with git worktree_

## git clone

**git-clone - Clone a repository into a new directory**

`--bare`: Create a bare repository  
_Useful in case of working with git worktree_

## git worktree

**git-worktree - Manage multiple working trees**

_Command to be used when working with a bare repo_

`$ git worktree add`  
`$ git worktree remove`  
`$ git worktree list`

## git revert

**git-revert - Revert some existing commits**

`-n` : Do not create a new commit

`$ git revert <commit>`: Revert the changes specified by the commit and create a new commit with the reverted changes.

# Resources

- <https://delicious-insights.com/fr/articles-et-tutos/git-log/>
- <https://stackoverflow.com/questions/2221658/whats-the-difference-between-head-and-head-in-git>
