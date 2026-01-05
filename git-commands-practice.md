# Git Commands Practice (catalog + examples)

This file is a hands-on Git practice catalog. Run these commands inside this repo.

Conventions:

- Replace `<...>` placeholders.
- `origin` means your remote name.
- Commands marked **(rewrites history)** can break shared branches.

---

## A) How to find “all possible Git commands”

Git has many subcommands (porcelain + plumbing). To list what your installed Git supports:

```bash
git help -a        # list *all* available subcommands on your machine
git help -g        # list Git concept guides (glossary, revisions, workflows)
```

To read documentation:

```bash
git help <command>
git <command> -h
```

Important docs to understand examples:

```bash
git help revisions
git help gitrevisions
git help glossary
```

---

## 0) Setup & Config

```bash
git --version
git config --list
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Common config:

```bash
git config --global init.defaultBranch main
git config --global core.autocrlf true       # common on Windows
git config --global fetch.prune true
git config --global pull.rebase false
```

Aliases:

```bash
git config --global alias.st status
git st
```

---

## 1) Create, Clone, Inspect Repo

```bash
git init
git init --bare
git clone <url>
git clone <url> <folder>
```

Inspect repository state:

```bash
git status -sb
git log --oneline --graph --decorate --all
git show <commit>
git show <commit>:<path>
```

---

## 2) Files: Add, Move, Remove

Stage files:

```bash
git add <file>
git add .
git add -p          # interactive staging
```

Move/rename (records rename in index):

```bash
git mv old.txt new.txt
```

Remove:

```bash
git rm <file>               # remove from working tree + index
git rm --cached <file>      # keep file, untrack it
```

Windows quick file creation:

```bat
echo hello> hello.txt
```

---

## 3) Commit & History Editing

Commit:

```bash
git commit -m "message"
git commit
git commit -a -m "commit tracked changes"
```

Amend last commit:

```bash
git commit --amend
git commit --amend --no-edit
```

Pick commits by message/author:

```bash
git log --author="Alice"
git log --grep="fix"
```

---

## 4) Diff (your best debugging tool)

```bash
git diff
git diff --staged
git diff <commit1> <commit2>
git diff <commit> -- <path>
```

Word diff:

```bash
git diff --word-diff
```

---

## 5) Undo / Restore / Reset

Discard local unstaged edits:

```bash
git restore <file>
git restore .
```

Unstage:

```bash
git restore --staged <file>
```

Restore a file from a commit:

```bash
git restore --source <commit> -- <file>
```

Revert (safe on shared branches):

```bash
git revert <commit>
git revert <oldest_commit>^..<newest_commit>
```

Reset (**rewrites history** on current branch):

```bash
git reset --soft <commit>
git reset --mixed <commit>
git reset --hard <commit>     # DANGEROUS: discards worktree changes
```

Recover “lost” commits:

```bash
git reflog
git reset --hard <reflog_sha>
```

---

## 6) Branches & Switching

```bash
git branch
git branch -vv
git switch <branch>
git switch -c <new-branch>
```

Rename/delete:

```bash
git branch -m <old> <new>
git branch -d <branch>
git branch -D <branch>
```

Legacy switching (still exists):

```bash
git checkout <branch>
git checkout -b <new-branch>
```

---

## 7) Merge, Rebase, Cherry-pick

Merge:

```bash
git merge <branch>
git merge --no-ff <branch>
git merge --abort
```

Rebase (**rewrites history**):

```bash
git rebase <upstream>
git rebase -i <base>
git rebase --continue
git rebase --abort
```

Cherry-pick:

```bash
git cherry-pick <commit>
git cherry-pick <a>..<b>
git cherry-pick --abort
```

---

## 8) Remotes: fetch / pull / push

Inspect:

```bash
git remote -v
git remote show origin
```

Manage:

```bash
git remote add origin <url>
git remote set-url origin <url>
git remote rename origin upstream
git remote remove <name>
```

Fetch:

```bash
git fetch
git fetch --all --prune
git fetch origin <branch>
```

Pull:

```bash
git pull
git pull --rebase
```

Push:

```bash
git push
git push -u origin <branch>
git push --tags
git push --force-with-lease   # safer force
```

---

## 9) Tags

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

## 10) Stash

```bash
git stash
git stash -u
git stash list
git stash show -p stash@{0}
git stash pop
git stash apply stash@{0}
git stash drop stash@{0}
git stash clear
```

---

## 11) Search & Inspect

Blame:

```bash
git blame <file>
git blame -L 10,40 <file>
```

Search tracked content:

```bash
git grep "TODO"
git grep -n "function" -- <path>
```

Show references:

```bash
git show-ref
git for-each-ref --format="%(refname:short) %(objectname:short)" refs/heads
```

Describe a commit (useful with tags):

```bash
git describe --tags --always
```

---

## 12) Ignore & Clean

Create `.gitignore`:

```gitignore
node_modules/
dist/
*.log
.env
```

If already tracked:

```bash
git rm --cached <file>
```

Delete untracked stuff (be careful):

```bash
git clean -n
git clean -fd
```

---

## 13) Patches (apply/send changes without merging)

Create patches:

```bash
git format-patch -1 <commit>
git format-patch <base>..HEAD
```

Apply patches:

```bash
git apply <patchfile>
git am <patchfile>           # applies and creates commits
git am --abort
```

---

## 14) Archive & Bundle

Create a zip/tar of repo content at a commit:

```bash
git archive -o source.zip HEAD
git archive -o source.zip <tag>
```

Bundle (offline transfer of a repo):

```bash
git bundle create repo.bundle --all
git clone repo.bundle <folder>
```

---

## 15) Submodules (optional)

```bash
git submodule add <url> <path>
git submodule update --init --recursive
git submodule foreach git pull
```

---

## 16) Worktrees (multiple working folders for one repo)

```bash
git worktree list
git worktree add ..\wt-feature feature/a
git worktree remove ..\wt-feature
```

---

## 17) Troubleshooting & Maintenance

Find the commit that introduced a bug:

```bash
git bisect start
git bisect bad
git bisect good <commit>
git bisect run <command>
git bisect reset
```

Repair/cleanup:

```bash
git fsck
git gc
git maintenance run
```

---

## 18) Plumbing (advanced) — examples you can actually run

These are lower-level building blocks. You rarely need them, but they explain how Git works.

```bash
git rev-parse HEAD
git cat-file -t HEAD
git cat-file -p HEAD
git ls-tree HEAD
git hash-object -w <file>
git show-index < .git/index
```

---

## 19) Practice Scenarios (guided)

### Scenario A: Basic feature work

```bash
git switch -c feature/login
echo work> login.txt
git add login.txt
git commit -m "Add login stub"
git switch main
git merge feature/login
```

### Scenario B: Create and resolve a conflict

1. Create two branches from `main`.
2. Edit the same line in the same file in both branches.
3. Merge one branch into the other and resolve.

Useful commands during conflict:

```bash
git status
git diff
git add <resolved-files>
git commit
```

### Scenario C: Rewrite local history (ONLY if not pushed)

```bash
git rebase -i HEAD~3
```
