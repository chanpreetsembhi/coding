A simple reference for everyday Git and GitHub use, from basics to common fixes.

## Table of Contents

1. [[#1. First Time Setup (only once on a new computer)|First Time Setup]]
2. [[#2. Starting a Project|Starting a Project]]
3. [[#3. The Basic Daily Workflow|The Basic Daily Workflow]]
4. [[#4. Viewing History|Viewing History]]
5. [[#5. Branching|Branching]]
6. [[#6. Undoing / Reverting Changes ⚠️ (Most asked about!)|Undoing / Reverting Changes]]
7. [[#7. Working with Remotes (GitHub connection)|Working with Remotes]]
8. [[#8. Stashing (save work temporarily without committing)|Stashing]]
9. [[#9. Handling Merge Conflicts|Handling Merge Conflicts]]
10. [[#10. Working with Pull Requests (GitHub feature, not a git command)|Working with Pull Requests]]
11. [[#11. Cheat Sheet – Quick Reference|Cheat Sheet]]
12. [[#12. Tips for Beginners|Tips for Beginners]]

---

## 1. First Time Setup (only once on a new computer)

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Tells Git who you are, so your commits are labeled correctly.

Check your settings:

```bash
git config --list
```

---

## 2. Starting a Project

### Create a new Git repository (repo)

```bash
git init
```

Run this inside a folder to start tracking it with Git.

### Copy (clone) an existing repo from GitHub

```bash
git clone https://github.com/username/repo-name.git
```

Downloads the whole project + its history to your computer.

---

## 3. The Basic Daily Workflow

This is the core cycle you'll use 90% of the time:

```bash
git status        # see what changed
git add .         # stage changes (prepare them for commit)
git commit -m "message describing the change"   # save the changes
git push          # upload to GitHub
```

### Details:

**Check status** – shows changed/new/staged files

```bash
git status
```

**Stage files** (tell Git which changes to include in next commit)

```bash
git add filename.txt      # stage one file
git add .                 # stage everything
```

**Commit** (save a snapshot with a message)

```bash
git commit -m "Fixed login bug"
```

**Push** (send commits to GitHub)

```bash
git push
git push origin main      # push to 'main' branch on 'origin' remote
```

**Pull** (get latest changes from GitHub)

```bash
git pull
```

Always pull before you start working, to avoid conflicts.

---

## 4. Viewing History

```bash
git log                 # full commit history
git log --oneline       # short, one line per commit
git log --oneline --graph   # visual branch history
```

```bash
git diff                # see unstaged changes (line by line)
git diff --staged       # see staged changes not yet committed
```

---

## 5. Branching

Branches let you work on features without touching the main code.

```bash
git branch                     # list branches
git branch new-feature         # create a branch
git checkout new-feature       # switch to that branch
git checkout -b new-feature    # create + switch in one step
```

Newer command (Git 2.23+):

```bash
git switch new-feature         # switch branch
git switch -c new-feature      # create + switch
```

### Merge a branch into main

```bash
git checkout main
git merge new-feature
```

### Delete a branch

```bash
git branch -d new-feature      # safe delete (only if merged)
git branch -D new-feature      # force delete
```

---

## 6. Undoing / Reverting Changes ⚠️ (Most asked about!)

### Undo changes in a file (not yet staged)

```bash
git checkout -- filename.txt
```

or newer:

```bash
git restore filename.txt
```

### Unstage a file (undo `git add`)

```bash
git reset filename.txt
```

or:

```bash
git restore --staged filename.txt
```

### Undo the last commit but KEEP the changes (unstaged)

```bash
git reset --soft HEAD~1
```

### Undo the last commit and DISCARD the changes completely

```bash
git reset --hard HEAD~1
```

⚠️ Careful — this permanently deletes those changes.

```bash
git reset --hard <commit-hash>
```

### Revert a commit (safe way — creates a new commit that undoes it)

```bash
git revert <commit-hash>
```

Best option when the commit is already pushed to GitHub, since it doesn't rewrite history.

```bash
git push --force-with-lease
```

If you used `git reset` (cases 1, 2, or 4) → history changed, so you need:

### Find the commit hash (needed for revert/reset)

```bash
git log --oneline
```

---

## 7. Working with Remotes (GitHub connection)

```bash
git remote -v                          # see connected remotes
git remote add origin <repo-url>       # connect local repo to GitHub
git remote remove origin               # disconnect
```

---

## 8. Stashing (save work temporarily without committing)

```bash
git stash            # save current changes aside
git stash list        # see stashed items
git stash pop         # bring back the last stashed changes
git stash drop        # delete a stash
```

Useful when you need to switch branches quickly but aren't ready to commit.

---

## 9. Handling Merge Conflicts

When Git can't auto-merge, it marks conflicts in the file like:

```
<<<<<<< HEAD
your version
=======
their version
>>>>>>> branch-name
```

1. Open the file, manually choose/edit the correct content
2. Remove the `<<<<<<<`, `=======`, `>>>>>>>` markers
3. Then:

```bash
git add filename.txt
git commit -m "Resolved merge conflict"
```

---

## 10. Working with Pull Requests (GitHub feature, not a git command)

Typical flow:

1. `git checkout -b my-feature` – create a branch
2. Make changes → `git add .` → `git commit -m "..."`
3. `git push origin my-feature`
4. Go to GitHub → "Compare & pull request" → describe changes → submit
5. Once approved, it gets merged into `main`

---

## 11. Cheat Sheet – Quick Reference

|Task|Command|
|---|---|
|Setup name/email|`git config --global user.name/user.email`|
|Start new repo|`git init`|
|Copy repo|`git clone <url>`|
|Check status|`git status`|
|Stage changes|`git add .`|
|Save changes|`git commit -m "message"`|
|Upload to GitHub|`git push`|
|Download updates|`git pull`|
|View history|`git log --oneline`|
|Create branch|`git checkout -b branch-name`|
|Switch branch|`git checkout branch-name`|
|Merge branch|`git merge branch-name`|
|Undo unstaged change|`git restore filename`|
|Unstage file|`git restore --staged filename`|
|Undo last commit (keep changes)|`git reset --soft HEAD~1`|
|Undo last commit (delete changes)|`git reset --hard HEAD~1`|
|Safely undo a pushed commit|`git revert <commit-hash>`|
|Save work temporarily|`git stash`|
|Restore stashed work|`git stash pop`|

---

## 12. Tips for Beginners

- Always run `git status` when unsure what's happening.
- Commit often, with clear short messages.
- Use `git pull` before starting new work to stay updated.
- Prefer `git revert` over `git reset --hard` once you've pushed to GitHub — it's safer since it doesn't erase history.
- Use branches for new features instead of editing `main` directly.