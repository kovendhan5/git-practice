# Git Practice

This repo is a safe place to practice Git commands locally.

## What to use

- Practice catalog: `git-commands-practice.md`

## Quick start

```bash
git status -sb
git log --oneline --graph --decorate --all
```

## Discover every Git command (installed on your machine)

```bash
git help -a
```

## Suggested practice loop

1. Create/edit a file.
2. `git add -p`
3. `git commit -m "..."`
4. Create a branch and merge it.
5. Practice undo safely: `git restore`, `git revert`, `git reflog`.
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
