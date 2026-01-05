# Git Commands Practice (with examples)

This file is meant to be a hands-on practice sheet. Run these commands inside this repo.

Notes:

- Anything in `<...>` is a placeholder you should replace.
- Many commands are safe to run repeatedly; commands that rewrite history are clearly marked.

---

## 0) Setup & Help

```bash
git --version
git help
git help <command>
git <command> -h
```

### Configure identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
```

### Useful config (optional)

```bash
git config --global init.defaultBranch main
git config --global core.autocrlf true   # common on Windows
git config --global pull.rebase false
```

---

## 1) Create / Clone Repos

### Initialize a repo

```bash
git init
```

### Clone

```bash
git clone <url>
git clone <url> <folder>
```

---

## 2) Working Directory Basics

### Check status

```bash
git status
git status -sb
```

### See history

```bash
git log
git log --oneline --graph --decorate --all
git log -p
```

### See changes

```bash
git diff            # unstaged
git diff --staged   # staged
git diff <commit1> <commit2>
```

---

## 3) Add / Commit

### Stage

```bash
git add <file>
git add .
git add -p          # stage interactively
```

### Unstage

```bash
git restore --staged <file>
```

### Commit

```bash
git commit -m "message"
git commit
git commit --amend
```

### Create a file quickly (Windows examples)

```bat
echo hello> hello.txt
```

Practice:

1. Create `hello.txt`, stage it, commit it.
2. Modify it twice; use `git add -p` to stage only one hunk.

---

## 4) Undo / Restore (safe-ish)

### Discard local unstaged changes

```bash
git restore <file>
git restore .
```

### Restore a file from a specific commit

```bash
git restore --source <commit> -- <file>
```

### Reset (moves branch pointer)

```bash
git reset --soft <commit>   # keep changes staged
git reset --mixed <commit>  # keep changes unstaged (default)
git reset --hard <commit>   # DANGEROUS: discards local changes
```

### Revert (safe for shared history)

```bash
git revert <commit>
```

---

## 5) Branching

### List / create / switch

```bash
git branch
git branch -vv
git branch <name>
git switch <name>
git switch -c <name>
```

### Rename / delete

```bash
git branch -m <old> <new>
git branch -d <name>
git branch -D <name>  # force
```

Practice:

1. Create a branch `feature/a`.
2. Make a commit on it.
3. Switch back to `main`.

---

## 6) Merge & Rebase

### Merge

```bash
git merge <branch>
git merge --no-ff <branch>
```

### Resolve conflicts

```bash
git status
git add <resolved-files>
git commit
```

### Abort merge

```bash
git merge --abort
```

### Rebase (rewrites history)

```bash
git rebase <upstream>
git rebase --continue
git rebase --abort
git rebase -i <base>
```

---

## 7) Remotes

### Inspect

```bash
git remote -v
git remote show origin
```

### Add / change / remove

```bash
git remote add origin <url>
git remote set-url origin <url>
git remote rename origin upstream
git remote remove <name>
```

### Fetch / pull / push

```bash
git fetch
git fetch --all --prune
git pull
git pull --rebase
git push
git push -u origin <branch>
git push --force-with-lease   # safer force
```

---

## 8) Tags

```bash
git tag
git tag v1.0.0
git tag -a v1.0.0 -m "release"
git show v1.0.0
git push origin v1.0.0
git push origin --tags
git tag -d v1.0.0
```

---

## 9) Stash

```bash
git stash
git stash -u
git stash list
git stash show -p
git stash pop
git stash apply stash@{0}
git stash drop stash@{0}
git stash clear
```

---

## 10) Inspect & Pick Changes

### Blame

```bash
git blame <file>
```

### Show commit / object

```bash
git show <commit>
git show <commit>:<path>
```

### Cherry-pick

```bash
git cherry-pick <commit>
git cherry-pick --abort
```

### Bisect

```bash
git bisect start
git bisect bad
git bisect good <commit>
git bisect run <command>
git bisect reset
```

---

## 11) .gitignore

Create a `.gitignore` file and add patterns like:

```gitignore
node_modules/
dist/
*.log
.env
```

If a file is already tracked, ignoring it won’t remove it:

```bash
git rm --cached <file>
```

---

## 12) Clean up untracked files

```bash
git clean -n      # preview
git clean -fd     # delete untracked files/dirs
```

---

## 13) Submodules (optional)

```bash
git submodule add <url> <path>
git submodule update --init --recursive
git submodule foreach git pull
```

---

## 14) Advanced / Plumbing (practice only)

These are less common day-to-day but good to know.

```bash
git reflog
git fsck
git gc
git cat-file -p <object>
git rev-parse HEAD
git show-ref
```

---

## 15) Mini Practice Scenarios

### Scenario A: Typical feature work

```bash
git switch -c feature/login
echo work> login.txt
git add login.txt
git commit -m "Add login stub"
git switch main
git merge feature/login
```

### Scenario B: Undo a bad commit (shared history)

```bash
git log --oneline
git revert <bad_commit_sha>
```

### Scenario C: Lost a commit? Use reflog

```bash
git reflog
git reset --hard <reflog_sha>
```
