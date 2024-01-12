<h1 align="center"> Git </h1>

# Table of content

<!-- vim-markdown-toc GFM -->

* [Introduction](#introduction)
  * [Backlog / Todo](#backlog--todo)
  * [General](#general)
  * [Aliases](#aliases)
  * [Terminology](#terminology)
    * [General](#general-1)
    * [About commits](#about-commits)
* [git - Basics](#git---basics)
  * [git init](#git-init)
  * [git clone](#git-clone)
  * [git add](#git-add)
  * [git commit](#git-commit)
  * [git diff](#git-diff)
  * [git notes](#git-notes)
  * [git mv](#git-mv)
  * [git reset](#git-reset)
  * [git restore](#git-restore)
  * [git rm](#git-rm)
  * [git status](#git-status)
* [git - Sharing & Updating](#git---sharing--updating)
  * [git fetch](#git-fetch)
  * [git pull](#git-pull)
  * [git push](#git-push)
  * [git remote](#git-remote)
  * [git ls-remote](#git-ls-remote)
  * [git submodule](#git-submodule)
* [git - Branching, Merging & Patching](#git---branching-merging--patching)
  * [git branch](#git-branch)
  * [git checkout](#git-checkout)
  * [git switch](#git-switch)
  * [git merge](#git-merge)
  * [git mergetool](#git-mergetool)
  * [git log](#git-log)
  * [git stash](#git-stash)
  * [git tag](#git-tag)
  * [git revert](#git-revert)
  * [git apply](#git-apply)
  * [git cherry-pick](#git-cherry-pick)
  * [git rebase](#git-rebase)
  * [git worktree](#git-worktree)
* [git - Debugging](#git---debugging)
  * [git bisec](#git-bisec)
  * [git blame](#git-blame)
  * [git grep](#git-grep)
* [Resources](#resources)

<!-- vim-markdown-toc -->

# Introduction

## Backlog / Todo

- Explore custome configuration of git mergetool (i.e. use nvim diff)

## General

- Great visual representation of the git stages & commands  
  <http://ndpsoftware.com/git-cheatsheet.html>

- Guidelines  
  **Do not rebase commits that exist outside your local repository**, people may have based work on.

## Aliases

```bash
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.lg "log --graph --date=relative --pretty=tformat:'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%an %ad)%Creset'"
$ git config --global alias.unstage 'reset HEAD --'
$ git config --global alias.last 'log -1 HEAD'
$ git config --global push.default current
```

- `$ git unstage <file>` = `$ git reset HEAD -- <file>`
- `$ git last`: Display last commit

- `$ git lg`: Friendly log display  
  `$ git lg -10`: Display the last 10 commits  
  `$ git lg <my_file>`: Display changes related to specific file(s) or directories  
  `$ git lg <my_branch>`: Same for 1 or multiple branches  
  `$ git lg master..dev`: Specific intervals (works as well with tags)  
  `$ git lg --since='1 week ago' --all`: Various alternatives are possible

`--branches`: For local branches  
`--all`: For remotes stuffs (branches, tags, stash)  
`--merges`: Check merges

**push.default** set to **current**: Used to simplify the push command. Push the
current branch to update a branch with the same name on the receiving end. Works
in both central and non-central workflows.

## Terminology

- **Index** = **Staging area**: Next files to be commited
- **Detached Head state**: <!-- TODO: To be added -->
- **Fast-forward**: if the targetted branch commit is directly ahead of the commit
  of the current branch, Git simply moves the pointer forward. when you try to
  merge one commit with a commit that can be reached by following the first
  commit’s history, Git simplifies things by moving the pointer forward because
  there is no divergent work to merge together — this is called a “fast-forward.

### General

### About commits

- `HEAD`: The current branch, represented in `.git/HEAD` and as well a pointer
  to the last commit
- `HEAD^`: Second last commit, equivalent to `HEAD~1`
- `HEAD^^`: Third commit from the top
- `HEAD~3` = `Head^^^` (No number means 1)
- `HEAD~5..HEAD~2`

# git - Basics

## git init

Create an empty Git repository or reinitialize an existing one

`--bare`: Create a bare repository

_Useful in case of working with git worktree_

## git clone

Clone a repository into a new directory

`--bare`: Create a bare repository

_Useful in case of working with git worktree_

## git add

## git commit

Record changes to the repository

`-m <msg>`: Use the given \<msg> as the commit message

`--amend <msg>`: Replace the tip of the current branch by creating a new commit
This command takes your staging area and uses it for the commit. If you’ve made
no changes since your last commit (for instance, you run this command
immediately after your previous commit), then your snapshot will look exactly
the same, and all you’ll change is your commit message.

## git diff

Show changes between commits, commit and working tree, etc

## git notes

## git mv

Move or rename a file, a directory, or a symlink

## git reset

Reset current HEAD to the specified state git-reset is about updating your
branch, moving the tip in order to add or remove commits from the branch. This
operation changes the commit history.

- `$ git reset HEAD <file(s)>`: Unstage \<file(s)> This is equivalrent to `$
git restore --staged <file(s)>`

_git-reset can also be used to restore the index, overlapping with git-restore._

## git restore

Restore working tree files

![git_restore](./git/git_restore.jpg)

git-restore is about restoring files in the working tree from either the index
or another commit. This command does not update your branch. The command can
also be used to restore files in the index from another commit.

- `$ git restore --staged <file(s)>`: Restore a file in the index to match the
  version in HEAD
- `$ git restore --source=HEAD --staged --worktree <file(s)>`: Restore both the
  index and the working tree. This is equivalent to `git checkout`.

## git rm

Remove files from the working tree and from the index

`--cached`: Keep the file in the directory but Git will not track it anymore

## git status

Show the working tree status

`-s`: Give the output in the short-format

# git - Sharing & Updating

## git fetch

Download objects and refs from another repository

![git_checkout](./git/git_fetch.png)

- `$ git fetch <remote>`

## git pull

Fetch from and integrate with another repository or a local branch

- `$ git pull`
- `$ git pull origin`

**Avoid `git pull`, preferred method is `git fetch` & `git merge`**

## git push

Update remote refs along with associated objects

- `$ git push <remote> <name>`: Push remote branch
- `$ git push origin <tagname>`: Push a particular tag
- `$ git push origin --tags`: Push all tags
- `$ git push origin --delete <name>`: Push removal of branch name
- `$ git push origin --delete <tagname>`: Delete a remote tag

## git remote

Manage set of tracked repositories

- `$ git remote add <shortname> <url>`: Add a remote, shortname can be used for
  git commands
- `$ git remote rename <current> <new>` : Rename a remote reposity
- `$ git remote remove <shortname>` : Remove a remote reposity
- `$ git remote show <remote>`: Gives some information about remote

`-v`: Display URL

## git ls-remote

List references in a remote repository

- `$ git ls-remote`
- `$ git ls-remote <remote>`

## git submodule

# git - Branching, Merging & Patching

## git branch

List, create, or delete branches

- `$ git branch`: List existing branches
- `$ git branch <name>`: Create a new branch (i.e. creates a new pointer against
  current commit)
- `$ git branch -d <name>`: Delete branch
- `$ git branch -v`: List the last commit for each branch
- `$ git branch -vv`: List the remote tracked branches (i.e. generally executed
  after `$ git fetch --all`)
- `$ git branch --merged`: Find all branches which can be safely deleted, since
  those branches are fully contained by HEAD.
- `$ git branch --no-merged`: Find branches which are candidates for merging
  into HEAD, since those branches are not fully contained by HEAD.
- `$ git branch --move <old_name> <new_name>`: Rename the branch locally
- `$ git push --set-upstream origin <new_name>`: Push the new branch name
- `$ git push origin --delete <name>`: Push removal of branch name
- `$ git branch -u <remote>/<name>`: Change the upstream branch being tracked
  against the current local branch

## git checkout

Switch branches or restore working tree files

_From Git version 2.23 onwards you can use git switch instead of git checkout_

- `$ git checkout -b <branch>`: Create & Switch to a new branch (Locally)
- `$ git checkout -b <branch> <remote>/<branch>`  
   = `$ git checkout --track <remote>/<branch>`  
   = `$ git checkout <branch>`  
  Switch to a branch _This moves the `HEAD` to point to the branch_
- `$ git checkout -b <local_n> <remote>/<branch>`: Use a specific local name

**Special**

- `$ git restore --source=HEAD --staged --worktree <file(s)>`: Restore both the
  index and the working tree, which is equivalent to `git checkout`

## git switch

Switch branches

- `$ git switch <branch>`: Switch to a branch
- `$ git switch -c <branch>`: Create a branch and switch to it
- `$ git switch - `: Switch back to the previous branch

## git merge

Join two or more development histories together

- `$ git merge <branch_name>`: Merge _branch_name_ with current branch

**fast-forward**: _see [Terminology](#terminology)_

## git mergetool

Run merge conflict resolution tools to resolve merge conflicts

`$ git mergetool`: Run one of several merge utilities to resolve merge
conflicts (i.e. typically after git merge)

**git mergetool** creates \*.orig backup files while resolving merges. These are
safe to remove once a file has been merged and its git mergetool session has
completed.

## git log

Show commit logs

_See [Browse the history](#browse-the-history)_

## git stash

## git tag

Create, list, delete or verify a tag object signed with GPG Annotated tags are
meant for release while lightweight tags are meant for private or temporary
object labels.

- `$ git tag`: list all tags (i.e. -l or --list optional)
- `$ git tag -a v0.1 `: Create a new tag "v0.1"
- `$ git tag v0.1-lw`: Create a lightweight tag (i.e. less details)
- `$ git tag -a v0.1 <commit-sha>`: Create a new tag against a previous commit
- `$ git tag -d <tagname>`: Delete a particular tag
- `$ git show v0.1 `: Display tag details for "v0.1"
- `$ git push origin <tagname>`: Push a particular tag
- `$ git push origin --tags`: Push all tags
- `$ git push origin --delete <tagname>`: Delete a remote tag
- `$ git checkout -b version01 v0.1`: Checkout a new branch based on a tag

## git revert

Revert some existing commits git-revert is about making a new commit that
reverts the changes made by other commits.

`-n` : Do not create a new commit

- `$ git revert <commit>`: Revert the changes specified by the commit and create
  a new commit with the reverted changes.

## git apply

## git cherry-pick

## git rebase

Reapply commits on top of another base tip

Typical simple flow:

- `$ git checkout <branch_name>`
- `$ git rebase master`: Apply "branch_name" commits on top of master
- `$ git checkout master`: Back to master
- `$ git merge <branch_name>`: Fast-forward merge

More complex but can be cery useful

- `$ git rebase --onto master <branch1> <branch2>`: This basically says, “Take
  the branch2, figure out the patches since it diverged from branch1, and replay
  these patches in branch2 as if it was based directly off the master branch
  instead.”
- `$ git checkout master`
- `$ git merge <branch2>`: Fast-forward merge

## git worktree

Manage multiple working trees

_Command to be used when working with a bare repo_

`$ git worktree add` `$ git worktree remove` `$ git worktree list`

# git - Debugging

## git bisec

## git blame

## git grep

# Resources

- <https://delicious-insights.com/fr/articles-et-tutos/git-log/>
- <https://stackoverflow.com/questions/2221658/whats-the-difference-between-head-and-head-in-git>
- <https://git-scm.com>
- <https://git-scm.com/book/en/v2>
- <http://ndpsoftware.com/git-cheatsheet.html>
