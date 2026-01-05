# Git Commands Practice (catalog + examples)

This file is a hands-on Git practice catalog. Run these commands inside this repo.

Conventions:

- Replace `<...>` placeholders.
- `origin` means your remote name.
- Commands marked **(rewrites history)** can break shared branches.

---

# Git Commands Practice (command + explanation + example)

Run these commands inside this repo.

Rules:

- Each command is followed by a real example you can copy-paste.
- Replace placeholders like `<branch>` / `<url>`.
- Commands marked **(rewrites history)** are risky on shared branches.

---

## A) Find all commands on your machine

```bash
git help -a                       # List every Git subcommand installed
# Example:
git help -a

git help -g                       # List Git guides (topics like revisions)
# Example:
git help -g

git help <command>                # Open the full manual for a command
# Example:
git help rebase

git <command> -h                  # Show short help/flags
# Example:
git log -h
```

---

## 0) Setup & Config

```bash
git --version                     # Show installed Git version
# Example:
git --version

git config --list                 # Show current config (system/global/local)
# Example:
git config --list

git config --global user.name "Your Name"   # Set commit author name
# Example:
git config --global user.name "Kovendhan"

git config --global user.email "you@example.com"  # Set commit author email
# Example:
git config --global user.email "kovendhan@example.com"

git config --global init.defaultBranch main  # Default branch name for new repos
# Example:
git config --global init.defaultBranch main

git config --global core.autocrlf true       # Windows line-ending handling
# Example:
git config --global core.autocrlf true

git config --global fetch.prune true         # Auto-prune deleted remote branches
# Example:
git config --global fetch.prune true

git config --global pull.rebase false        # Default pull strategy
# Example:
git config --global pull.rebase false

git config --global alias.st status          # Create alias (git st)
# Example:
git config --global alias.st status
```

---

## 1) Create / Clone / Inspect Repo

```bash
git init                          # Create a new repo in current folder
# Example:
git init

git init --bare                   # Create a bare repo (server-style)
# Example:
git init --bare ..\repo-server.git

git clone <url>                   # Download a repo into a new folder
# Example:
git clone https://github.com/git/git.git

git clone <url> <folder>          # Download into a specific folder name
# Example:
git clone https://github.com/git/git.git git-src

git status -sb                    # Short status with branch info
# Example:
git status -sb

git log --oneline --graph --decorate --all   # Compact visual history
# Example:
git log --oneline --graph --decorate --all

git show <commit>                 # Show one commit (diff + message)
# Example:
git show HEAD

git show <commit>:<path>          # Show a file as it existed in a commit
# Example:
git show HEAD:README.md
```

---

## 2) Files: Add / Move / Remove

```bash
git add <file>                    # Stage a file for commit
# Example:
git add readme.md

git add .                         # Stage all changes in current folder
# Example:
git add .

git add -p                        # Stage interactively (hunk by hunk)
# Example:
git add -p

git mv <old> <new>                # Rename/move a file (keeps history)
# Example:
git mv notes.txt docs-notes.txt

git rm <file>                     # Remove file and stage deletion
# Example:
git rm old.txt

git rm --cached <file>            # Stop tracking but keep file on disk
# Example:
git rm --cached .env
```

Create a file quickly (Windows):

```bat
echo hello> hello.txt             REM Create hello.txt
```

---

## 3) Commit

```bash
git commit -m "message"           # Commit staged changes with message
# Example:
git commit -m "Add hello.txt"

git commit                        # Open editor to write a multi-line message
# Example:
git commit

git commit -a -m "message"         # Commit tracked-file changes (skips untracked)
# Example:
git commit -a -m "Update docs"

git commit --amend                # Edit last commit (message and/or content)
# Example:
git commit --amend

git commit --amend --no-edit      # Add staged changes to last commit (keep message)
# Example:
git commit --amend --no-edit
```

---

## 4) Log & Diff

```bash
git log                           # Full commit history
# Example:
git log

git log -p                        # History with patch diffs
# Example:
git log -p

git log --author="Alice"           # Filter commits by author
# Example:
git log --author="kovendhan"

git log --grep="fix"               # Search commit messages
# Example:
git log --grep="stash"

git diff                          # Show unstaged changes
# Example:
git diff

git diff --staged                 # Show staged changes
# Example:
git diff --staged

git diff <a> <b>                  # Compare two commits/refs
# Example:
git diff HEAD~1 HEAD

git diff <commit> -- <path>       # Diff a file between commit and working tree
# Example:
git diff HEAD -- readme.md

git diff --word-diff              # Word-level diff (good for text)
# Example:
git diff --word-diff
```

---

## 5) Undo / Restore / Reset

```bash
git restore <file>                # Discard unstaged changes in a file
# Example:
git restore readme.md

git restore .                     # Discard all unstaged changes
# Example:
git restore .

git restore --staged <file>       # Unstage a file (keep working changes)
# Example:
git restore --staged readme.md

git restore --source <commit> -- <file>   # Restore file content from a commit
# Example:
git restore --source HEAD~1 -- readme.md

git revert <commit>               # Create a new commit that undoes a commit
# Example:
git revert HEAD

git reset --soft <commit>         # **(rewrites history)** Move HEAD; keep staged
# Example:
git reset --soft HEAD~1

git reset --mixed <commit>        # **(rewrites history)** Move HEAD; unstage changes
# Example:
git reset --mixed HEAD~1

git reset --hard <commit>         # **(rewrites history)** Move HEAD; discard changes
# Example:
git reset --hard HEAD~1

git reflog                        # Show where HEAD/branches pointed recently
# Example:
git reflog
```

---

## 6) Branches & Switching

```bash
git branch                        # List local branches
# Example:
git branch

git branch -vv                    # List branches with upstream + last commit
# Example:
git branch -vv

git switch <branch>               # Switch branches (modern)
# Example:
git switch main

git switch -c <new-branch>        # Create + switch to a new branch
# Example:
git switch -c feature/login

git branch -m <old> <new>         # Rename a branch
# Example:
git branch -m feature/login feature/auth

git branch -d <branch>            # Delete a fully-merged branch
# Example:
git branch -d feature/auth

git branch -D <branch>            # Force delete a branch
# Example:
git branch -D wip/experiment

git checkout <branch>             # Legacy switch command
# Example:
git checkout main

git checkout -b <new-branch>      # Legacy create+switch
# Example:
git checkout -b hotfix/typo
```

---

## 7) Merge / Rebase / Cherry-pick

```bash
git merge <branch>                # Merge a branch into the current branch
# Example:
git merge feature/login

git merge --no-ff <branch>        # Always create a merge commit
# Example:
git merge --no-ff feature/login

git merge --abort                 # Cancel a merge (when conflicts happen)
# Example:
git merge --abort

git rebase <upstream>             # **(rewrites history)** Replay commits on new base
# Example:
git rebase main

git rebase -i <base>              # **(rewrites history)** Interactive history rewrite
# Example:
git rebase -i HEAD~3

git rebase --continue             # Continue after resolving rebase conflicts
# Example:
git rebase --continue

git rebase --abort                # Abort the rebase and return to previous state
# Example:
git rebase --abort

git cherry-pick <commit>          # Copy a commit onto current branch
# Example:
git cherry-pick a1b2c3d

git cherry-pick <a>..<b>          # Cherry-pick a range (a exclusive, b inclusive)
# Example:
git cherry-pick HEAD~3..HEAD~1

git cherry-pick --abort           # Abort cherry-pick
# Example:
git cherry-pick --abort
```

---

## 8) Remotes: fetch / pull / push

```bash
git remote -v                     # List remotes and URLs
# Example:
git remote -v

git remote show origin            # Show remote details (branches/tracking)
# Example:
git remote show origin

git remote add origin <url>       # Add a new remote
# Example:
git remote add origin https://github.com/you/repo.git

git remote set-url origin <url>   # Change remote URL
# Example:
git remote set-url origin git@github.com:you/repo.git

git remote rename origin upstream # Rename a remote
# Example:
git remote rename origin upstream

git remote remove <name>          # Remove a remote
# Example:
git remote remove upstream

git fetch                         # Download remote updates (no merge)
# Example:
git fetch

git fetch --all --prune           # Fetch all remotes + prune deleted branches
# Example:
git fetch --all --prune

git fetch origin <branch>         # Fetch just one branch
# Example:
git fetch origin main

git pull                          # Fetch + merge into current branch
# Example:
git pull

git pull --rebase                 # Fetch + rebase your commits on top
# Example:
git pull --rebase

git push                          # Push current branch to its upstream
# Example:
git push

git push -u origin <branch>       # Push and set upstream tracking
# Example:
git push -u origin main

git push --tags                   # Push tags
# Example:
git push --tags

git push --force-with-lease       # **(rewrites history)** Safer force push
# Example:
git push --force-with-lease
```

---

## 9) Tags

```bash
git tag                           # List tags
# Example:
git tag

git tag v1.0.0                    # Create lightweight tag
# Example:
git tag v1.0.0

git tag -a v1.0.0 -m "release"     # Create annotated tag
# Example:
git tag -a v1.0.0 -m "First release"

git show v1.0.0                   # Show what the tag points to
# Example:
git show v1.0.0

git push origin v1.0.0            # Push one tag
# Example:
git push origin v1.0.0

git tag -d v1.0.0                 # Delete local tag
# Example:
git tag -d v1.0.0
```

---

## 10) Stash

```bash
git stash                         # Save uncommitted changes temporarily
# Example:
git stash

git stash -u                      # Also stash untracked files
# Example:
git stash -u

git stash list                    # List stash entries
# Example:
git stash list

git stash show -p stash@{0}       # Show patch of a stash entry
# Example:
git stash show -p stash@{0}

git stash apply stash@{0}         # Apply stash without removing it
# Example:
git stash apply stash@{0}

git stash pop                     # Apply stash and remove it
# Example:
git stash pop

git stash drop stash@{0}          # Delete a stash entry
# Example:
git stash drop stash@{0}

git stash clear                   # Delete all stashes
# Example:
git stash clear
```

---

## 11) Search & Inspect

```bash
git blame <file>                  # Show who last changed each line
# Example:
git blame readme.md

git blame -L 10,40 <file>         # Blame only a line range
# Example:
git blame -L 1,25 readme.md

git grep "TODO"                   # Search tracked files for a string
# Example:
git grep "Practice"

git grep -n "function" -- <path>  # Search in a folder and show line numbers
# Example:
git grep -n "git" -- .

git show-ref                      # List refs (branches/tags) and SHAs
# Example:
git show-ref

git for-each-ref --format="%(refname:short) %(objectname:short)" refs/heads  # Custom branch list
# Example:
git for-each-ref --format="%(refname:short) %(objectname:short)" refs/heads

git describe --tags --always      # Human-friendly name for a commit
# Example:
git describe --tags --always
```

---

## 12) Ignore & Clean

`.gitignore` tells Git which untracked files to ignore.

Example `.gitignore`:

```gitignore
node_modules/
dist/
*.log
.env
```

If a file is already tracked, ignoring it won’t remove it:

```bash
git rm --cached <file>            # Untrack a file but keep it
# Example:
git rm --cached .env
```

Remove untracked files (be careful):

```bash
git clean -n                      # Preview what would be deleted
# Example:
git clean -n

git clean -fd                     # Delete untracked files and folders
# Example:
git clean -fd
```

---

## 13) Patches (share changes without pushing)

```bash
git format-patch -1 <commit>      # Create a patch file for one commit
# Example:
git format-patch -1 HEAD

git format-patch <base>..HEAD     # Create patches for a range of commits
# Example:
git format-patch HEAD~3..HEAD

git apply <patchfile>             # Apply patch to working tree (no commit)
# Example:
git apply 0001-some-change.patch

git am <patchfile>                # Apply patch and create commits
# Example:
git am 0001-some-change.patch

git am --abort                    # Abort an in-progress 'git am'
# Example:
git am --abort
```

---

## 14) Archive & Bundle

```bash
git archive -o source.zip HEAD    # Export repo content (no .git folder)
# Example:
git archive -o source.zip HEAD

git bundle create repo.bundle --all  # Pack repo history into a single file
# Example:
git bundle create repo.bundle --all

git clone repo.bundle <folder>    # Clone from a bundle
# Example:
git clone repo.bundle repo-from-bundle
```

---

## 15) Submodules (optional)

```bash
git submodule add <url> <path>    # Add another repo inside this repo
# Example:
git submodule add https://github.com/libgit2/libgit2.git vendor/libgit2

git submodule update --init --recursive  # Fetch and checkout submodules
# Example:
git submodule update --init --recursive

git submodule foreach git pull    # Run a command in each submodule
# Example:
git submodule foreach git pull
```

---

## 16) Worktrees (multiple working folders)

```bash
git worktree list                 # List worktrees
# Example:
git worktree list

git worktree add ..\wt-feature feature/a  # Create a new working folder for a branch
# Example:
git worktree add ..\wt-feature feature/login

git worktree remove ..\wt-feature         # Remove a worktree
# Example:
git worktree remove ..\wt-feature
```

---

## 17) Troubleshooting & Maintenance

```bash
git bisect start                  # Start binary search for a bad commit
# Example:
git bisect start

git bisect bad                    # Mark current commit as bad
# Example:
git bisect bad

git bisect good <commit>          # Mark a known good commit
# Example:
git bisect good HEAD~10

git bisect reset                  # Stop bisect and return to original branch
# Example:
git bisect reset

git fsck                          # Check repository object integrity
# Example:
git fsck

git gc                            # Compress and clean up repo objects
# Example:
git gc

git maintenance run               # Run Git maintenance tasks
# Example:
git maintenance run
```

---

## 18) Plumbing (advanced)

```bash
git rev-parse HEAD                # Print the SHA for HEAD
# Example:
git rev-parse HEAD

git cat-file -t HEAD              # Show object type (commit/tree/blob)
# Example:
git cat-file -t HEAD

git cat-file -p HEAD              # Pretty-print the object content
# Example:
git cat-file -p HEAD

git ls-tree HEAD                  # List files in a tree object
# Example:
git ls-tree HEAD

git hash-object -w <file>         # Hash and store a file as a blob
# Example:
git hash-object -w readme.md
```

---

## 19) Practice Scenarios

### Scenario A: Basic feature work

```bash
git switch -c feature/login       # Create branch
# Example:
git switch -c feature/login

echo work> login.txt              # Create a file (Windows)

git add login.txt                 # Stage
# Example:
git add login.txt

git commit -m "Add login stub"    # Commit
# Example:
git commit -m "Add login stub"

git switch main                   # Back to main
# Example:
git switch main

git merge feature/login           # Merge the feature
# Example:
git merge feature/login
```

### Scenario B: Create and resolve a conflict

1. Create `feature/a` and `feature/b`.
2. Edit the same line in the same file on both branches.
3. Merge and resolve.

Useful commands during conflicts:

```bash
git status                        # See which files are conflicted
# Example:
git status

git diff                          # See conflict markers and changes
# Example:
git diff

git add <resolved-files>          # Mark conflicts as resolved
# Example:
git add readme.md

git commit                        # Finish the merge commit
# Example:
git commit
```

### Scenario C: Rewrite local history (ONLY if not pushed)

```bash
git rebase -i HEAD~3              # **(rewrites history)** edit last 3 commits
# Example:
git rebase -i HEAD~3
```
