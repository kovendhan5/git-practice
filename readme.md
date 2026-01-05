# Git Practice Workspace

This repo is for practicing common Git commands locally.

## Files

- See `git-commands-practice.md` for commands + examples + exercises.

## Quick start

```bash
git status
git log --oneline --graph --decorate --all
```

## Suggested practice loop

1. Create/edit a file.
2. `git add -p`
3. `git commit -m "..."`
4. Create a branch, merge it, and resolve a conflict once.
   K:\git-practice>git config --global user.name "kovendhan5"

K:\git-practice>git config --global user.email "kovendhanofficial5@gmail.com"

K:\git-practice>git config -list
error: did you mean `--list` (with two dashes)?

K:\git-practice>git config --list
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
http.sslbackend=openssl
http.sslcainfo=C:/Program Files/Git/mingw64/etc/ssl/certs/ca-bundle.crt
core.autocrlf=true
core.fscache=true
core.symlinks=false
pull.rebase=false
credential.helper=manager
credential.https://dev.azure.com.usehttppath=true
init.defaultbranch=master
user.name=kovendhan5
user.email=kovendhanofficial5@gmail.com
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
remote.origin.url=https://github.com/kovendhan5/git-practice.git
remote.origin.fetch=+refs/heads/_:refs/remotes/origin/_
branch.main.remote=origin
branch.main.merge=refs/heads/main
branch.main.vscode-merge-base=origin/main
(END)

K:\git-practice>git init -b newmain
warning: re-init: ignored --initial-branch=newmain
Reinitialized existing Git repository in K:/git-practice/.git/

K:\git-practice>git diff

K:\git-practice>git diff

K:\git-practice>git stash
No local changes to save

K:\git-practice>git stash
warning: in the working copy of 'sample2.txt', LF will be replaced by CRLF the next time Git touches it
Saved working directory and index state WIP on main: 1b74e53 Add sample2.txt with initial content

K:\git-practice>git stash list
stash@{0}: WIP on main: 1b74e53 Add sample2.txt with initial content

K:\git-practice>git stash apply
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git restore <file>..." to discard changes in working directory)
modified: sample2.txt

no changes added to commit (use "git add" and/or "git commit -a")

K:\git-practice>git stash pop
error: Your local changes to the following files would be overwritten by merge:
sample2.txt
Please commit your changes or stash them before you merge.
Aborting
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git restore <file>..." to discard changes in working directory)
modified: sample2.txt

no changes added to commit (use "git add" and/or "git commit -a")
The stash entry is kept in case you need it again.

K:\git-practice>git stash pop
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
Dropped refs/stash@{0} (7965f6c0fde79754364261ec75218ba600035672)

K:\git-practice>git stash clean
fatal: subcommand wasn't specified; 'push' can't be assumed due to unexpected token 'clean'

K:\git-practice>git stash clear

K:\git-practice>git tag v1.0.0.0

K:\git-practice>git blame sample2.txt  
1b74e539 (kovendhan5 2025-02-03 13:54:08 +0530 1) nothing here
6ad72c95 (kovendhan5 2025-02-03 13:57:26 +0530 2) but here i have something!

K:\git-practice>git blame --since ="3 weeks ago"sample.txt
usage: git blame [<options>] [<rev-opts>] [<rev>] [--] <file>

    <rev-opts> are documented in git-rev-list(1)

    --[no-]incremental    show blame entries as we find them, incrementally
    -b                    do not show object names of boundary commits (Default: off)
    --[no-]root           do not treat root commits as boundaries (Default: off)
    --[no-]show-stats     show work cost statistics
    --[no-]progress       force progress reporting
    --[no-]score-debug    show output score for blame entries
    -f, --[no-]show-name  show original filename (Default: auto)
    -n, --[no-]show-number
                          show original linenumber (Default: off)
    -p, --[no-]porcelain  show in a format designed for machine consumption
    --[no-]line-porcelain show porcelain format with per-line commit information
    -c                    use the same output mode as git-annotate (Default: off)
    -t                    show raw timestamp (Default: off)
    -l                    show long commit SHA1 (Default: off)
    -s                    suppress author name and timestamp (Default: off)
    -e, --[no-]show-email show author email instead of name (Default: off)
    -w                    ignore whitespace differences
    --[no-]ignore-rev <rev>
                          ignore <rev> when blaming
    --[no-]ignore-revs-file <file>
                          ignore revisions from <file>
    --[no-]color-lines    color redundant metadata from previous line differently
    --[no-]color-by-age   color lines by age
    --[no-]minimal        spend extra cycles to find better match
    -S <file>             use revisions from <file> instead of calling git-rev-list
    --[no-]contents <file>
                          use <file>'s contents as the final image
    -C[<score>]           find line copies within and across files
    -M[<score>]           find line movements within and across files
    -L <range>            process only line range <start>,<end> or function :<funcname>
    --[no-]abbrev[=<n>]   use <n> digits to display object names

K:\git-practice>git clean
fatal: clean.requireForce is true and -f not given: refusing to clean

K:\git-practice>git clean -d
fatal: clean.requireForce is true and -f not given: refusing to clean

K:\git-practice>git clean -f

K:\git-practice>git revert sample2.txt
fatal: bad revision 'sample2.txt'

K:\git-practice>git revert Add sample2.txt with initial content  
fatal: bad revision 'Add'

K:\git-practice>git revert

K:\git-practice>git revert 1b74e53961012462548f4993a243a393ef7a6add
CONFLICT (modify/delete): sample2.txt deleted in parent of 1b74e53 (Add sample2.txt with initial content) and modified in HEAD. Version HEAD of sample2.txt left in tree.
error: could not revert 1b74e53... Add sample2.txt with initial content
hint: After resolving the conflicts, mark them with
hint: "git add/rm <pathspec>", then run
hint: "git revert --continue".
hint: You can instead skip this commit with "git revert --skip".
hint: To abort and get back to the state before "git revert",
hint: run "git revert --abort".
hint: Disable this message with "git config advice.mergeConflict false"
This reverts commit 1b74e53961012462548f4993a243a393ef7a6add.

# Conflicts:

# sample2.txt

# Please enter the commit message for your changes. Lines starting

# with '#' will be ignored, and an empty message aborts the commit.

#

# On branch main

# Your branch is up to date with 'origin/main'.

#

# You are currently reverting commit 1b74e53.

#

# Changes to be committed:

# deleted: sample2.txt

#

.git/COMMIT_EDITMSG [unix] (14:12 03/02/2025) 18,1 Bot

W11: Warning: File ".git/COMMIT_EDITMSG" has changed since editing started
See ":help W11" for more info.
[O]K, (L)oad File, Load File (a)nd Options:

K:\git-practice>git revert 1b74e53961012462548f4993a243a393ef7a6add
CONFLICT (modify/delete): sample2.txt deleted in parent of 1b74e53 (Add sample2.txt with initial content) and modified in HEAD. Version HEAD of sample2.txt left in tree.
error: could not revert 1b74e53... Add sample2.txt with initial content
hint: After resolving the conflicts, mark them with
hint: "git add/rm <pathspec>", then run
hint: "git revert --continue".
hint: You can instead skip this commit with "git revert --skip".
hint: To abort and get back to the state before "git revert",
hint: run "git revert --abort".
hint: Disable this message with "git config advice.mergeConflict false"
This reverts commit 1b74e53961012462548f4993a243a393ef7a6add.

# Conflicts:

Revert "Add sample2.txt with initial content"

This reverts commit 1b74e53961012462548f4993a243a393ef7a6add.
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~  
.git/COMMIT_EDITMSG [unix] (14:13 03/02/2025) 3,1 All
".git/COMMIT_EDITMSG" [unix] 3L, 109B
