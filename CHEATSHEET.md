# 📋 Git Mastery Hub — Complete Cheat Sheet

> Cross-referenced from: GitHub Education Cheat Sheet & git --print-out Cheat Sheet

---

## Quick Jump

- [1. Setup & Configuration](#1-setup--configuration)
- [2. Initialize & Clone](#2-initialize--clone)
- [3. Stage & Snapshot](#3-stage--snapshot)
- [4. Committing](#4-committing)
- [5. Branching](#5-branching)
- [6. Merging & Rebasing](#6-merging--rebasing)
- [7. Remote Operations](#7-remote-operations)
- [8. Diff & Inspect](#8-diff--inspect)
- [9. Tracking Path Changes](#9-tracking-path-changes)
- [10. Stashing](#10-stashing)
- [11. Undoing & History Rewriting](#11-undoing--history-rewriting)
- [12. Ignoring Files](#12-ignoring-files)
- [13. Code Archaeology](#13-code-archaeology)
- [14. Ways to Reference a Commit](#14-ways-to-reference-a-commit)

---

## 1. Setup & Configuration

| Command | Description | Source |
|---|---|---|
| `git config --global user.name "[firstname lastname]"` | Set name for version history credit | GitHub Education |
| `git config --global user.email "[valid-email]"` | Set email associated with history markers | GitHub Education |
| `git config --global color.ui auto` | Enable automatic command line coloring | GitHub Education |
| `git config --global core.excludesfile [file]` | Set system-wide ignore pattern file | GitHub Education |
| `git config user.name 'Your Name'` | Set name for current repo only (no --global) | git --print-out |
| `git config --global ...` | Apply any config option globally across all repos | git --print-out |
| `git config alias.st status` | Add an alias (`st` → `status`) | git --print-out |
| `man git-config` | See all possible configuration options | git --print-out |

---

## 2. Initialize & Clone

| Command | Description | Source |
|---|---|---|
| `git init` | Initialize an existing directory as a Git repository | Both |
| `git clone <url>` | Clone a full repository from a remote URL | Both |

---

## 3. Stage & Snapshot

| Command | Description | Source |
|---|---|---|
| `git status` | Show modified files in working tree staged for next commit | Both |
| `git add <file>` | Stage a specific file for next commit | Both |
| `git add .` | Stage all untracked files and changes in current directory | git --print-out |
| `git add -p` | Interactively choose which parts (hunks) of a file to stage | git --print-out |
| `git reset <file>` | Unstage a file while retaining changes in working directory | Both |
| `git reset` | Unstage all staged changes | git --print-out |
| `git rm <file>` | Delete a file and stage that deletion | Both |
| `git rm --cached <file>` | Stop tracking a file without deleting it from disk | git --print-out |
| `git mv <existing-path> <new-path>` | Rename or move a file and stage the change | GitHub Education |
| `git mv <old> <new>` | Rename a file and stage it (alternate syntax) | git --print-out |

---

## 4. Committing

| Command | Description | Source |
|---|---|---|
| `git commit` | Open text editor to compose a commit message | git --print-out |
| `git commit -m 'message'` | Commit with an inline message | git --print-out |
| `git commit -m "[descriptive message]"` | Commit staged snapshot with a descriptive message | GitHub Education |
| `git commit -am 'message'` | Stage all tracked file changes and commit in one step | git --print-out |
| `git commit --amend` | Modify the most recent commit message or add a forgotten file | git --print-out |

---

## 5. Branching

| Command | Description | Source |
|---|---|---|
| `git branch` | List all branches; active branch marked with `*` | Both |
| `git branch <branch-name>` | Create a new branch at the current commit | GitHub Education |
| `git branch --sort=-committerdate` | List branches sorted by most recently committed | git --print-out |
| `git branch -d <name>` | Delete a branch safely (must be fully merged) | git --print-out |
| `git branch -D <name>` | Force-delete a branch regardless of merge status | git --print-out |
| `git switch <name>` | Switch to an existing branch (modern, Git 2.23+) | git --print-out |
| `git switch -c <name>` | Create and switch to a new branch (modern) | git --print-out |
| `git checkout <name>` | Switch to a branch (legacy, still valid) | Both |
| `git checkout -b <name>` | Create and switch to a new branch (legacy) | git --print-out |
| `git checkout` | Switch to a branch (generic form) | GitHub Education |

> [!TIP]
> Prefer `git switch` over `git checkout` for branch operations in Git 2.23+.
> `git checkout` remains valid but handles too many unrelated tasks.

---

## 6. Merging & Rebasing

| Command | Description | Source |
|---|---|---|
| `git merge <branch>` | Merge the specified branch into the current branch | Both |
| `git merge <alias>/<branch>` | Merge a remote-tracking branch into current branch | GitHub Education |
| `git merge --squash <branch>` | Squash all commits from branch into one before merging | git --print-out |
| `git rebase <branch>` | Apply commits of current branch ahead of specified branch | Both |
| `git rebase -i HEAD~6` | Interactively rebase last 6 commits (squash, fixup, reorder, drop) | git --print-out |
| `git switch banana && git rebase main` | Switch to banana branch and rebase it onto main | git --print-out |
| `git switch main && git merge banana` | Switch to main and merge banana into it | git --print-out |
| `git cherry-pick <commit>` | Copy a single commit onto the current branch | git --print-out |

> [!WARNING]
> Rebasing rewrites commit history. Never rebase a branch that others are currently working on.

---

## 7. Remote Operations

| Command | Description | Source |
|---|---|---|
| `git remote add <alias> <url>` | Add a remote URL with a named alias | GitHub Education |
| `git remote add <name> <url>` | Add a remote (alternate parameter naming) | git --print-out |
| `git fetch <alias>` | Download all branches from remote without merging | GitHub Education |
| `git fetch origin main` | Fetch a specific remote branch | git --print-out |
| `git push <alias> <branch>` | Push local branch to remote | GitHub Education |
| `git push origin main` | Push local main branch to origin | git --print-out |
| `git push -u origin <name>` | Push new branch and set up tracking relationship | git --print-out |
| `git push --force-with-lease` | Force push safely — fails if remote has new commits from others | git --print-out |
| `git push --tags` | Push all local tags to remote | git --print-out |
| `git pull` | Fetch and merge from the tracking remote branch | Both |
| `git pull origin main` | Fetch and merge a specific remote branch | git --print-out |
| `git pull --rebase` | Fetch and rebase instead of merge (cleaner linear history) | git --print-out |

> [!WARNING]
> Never use `--force` to push to a shared branch. Always prefer `--force-with-lease` — it prevents overwriting commits pushed by others since your last fetch.

---

## 8. Diff & Inspect

| Command | Description | Source |
|---|---|---|
| `git diff` | Show changes in working directory not yet staged | Both |
| `git diff --staged` | Show staged changes not yet committed | Both |
| `git diff HEAD` | Show all staged and unstaged changes vs last commit | git --print-out |
| `git diff branchB...branchA` | Diff between tips of two branches | GitHub Education |
| `git diff <commit> <commit>` | Diff between two specific commits | git --print-out |
| `git diff <commit> <file>` | Diff a specific file between a commit and working copy | git --print-out |
| `git diff <commit> --stat` | Show file-level change summary for a commit | git --print-out |
| `git show <commit>` | Show a commit's metadata and content changes | git --print-out |
| `git show <commit> --stat` | Show file-level summary of a specific commit | git --print-out |
| `git show [SHA]` | Show any object in Git in human-readable format | GitHub Education |

---

## 9. Tracking Path Changes

| Command | Description | Source |
|---|---|---|
| `git rm <file>` | Delete a file from working tree and stage the deletion | GitHub Education |
| `git mv <existing-path> <new-path>` | Rename or move a file and stage the change | GitHub Education |
| `git log --stat -M` | Show commit log with rename-detection statistics | GitHub Education |

---

## 10. Stashing

| Command | Description | Source |
|---|---|---|
| `git stash` | Save modified and staged changes to a temporary stack | Both |
| `git stash list` | List all stashed changesets | Both |
| `git stash pop` | Apply the top stash entry and remove it from the stack | Both |
| `git stash drop` | Discard the top stash entry without applying it | Both |

---

## 11. Undoing & History Rewriting

| Command | Description | Source |
|---|---|---|
| `git reset HEAD^` | Undo the last commit; keep changes in working directory | git --print-out |
| `git reset --hard <commit>` | Move HEAD to a commit and discard all subsequent changes | Both |
| `git reset --hard` | Delete all staged and unstaged changes (destructive!) | git --print-out |
| `git commit --amend` | Edit the most recent commit message or add a forgotten file | git --print-out |
| `git restore <file>` | Discard unstaged changes to a file | git --print-out |
| `git restore --staged --worktree <file>` | Delete all staged and unstaged changes to a file | git --print-out |
| `git restore <file> --source <commit>` | Restore a file to its state at a specific commit | git --print-out |
| `git checkout <file>` | Discard unstaged changes (legacy form of restore) | git --print-out |
| `git checkout HEAD <file>` | Restore a file to the state of the last commit (legacy) | git --print-out |
| `git checkout <commit> <file>` | Restore a file to its state at a specific commit (legacy) | git --print-out |
| `git reflog BRANCHNAME` | Find commit IDs in reflog to recover from a failed rebase or reset | git --print-out |
| `git clean` | Delete untracked files from the working directory | git --print-out |

> [!NOTE]
> `git reflog` is your safety net. Even after `git reset --hard`, commits are recoverable for ~30 days via the reflog. Run `git reflog BRANCHNAME` to find the SHA, then `git reset --hard <SHA>` to recover.

> [!WARNING]
> `git reset --hard` is destructive — it permanently discards uncommitted work. Always verify what you're resetting before running this command.

---

## 12. Ignoring Files

| Concept | Description | Source |
|---|---|---|
| `.gitignore` file | File listing patterns of paths Git should not track | Both |
| `git config --global core.excludesfile [file]` | Set a global ignore file that applies to every repository | GitHub Education |
| `git rm --cached <file>` | Stop tracking a file already committed (does not delete from disk) | git --print-out |

---

## 13. Code Archaeology

| Command | Description | Source |
|---|---|---|
| `git log` | Show full commit history | Both |
| `git log main` | Show commit history for the main branch | git --print-out |
| `git log --graph main` | Show a visual ASCII branch graph for main | git --print-out |
| `git log --oneline` | Show condensed one-line commit history | git --print-out |
| `git log <file>` | Show commit history for a specific file | git --print-out |
| `git log --follow <file>` | Show history of a file including renames | Both |
| `git log branchB..branchA` | Show commits on branchA not on branchB | GitHub Education |
| `git log --stat -M` | Show commit stats with rename detection | GitHub Education |
| `git log -G banana` | Find commits that added or removed the text "banana" | git --print-out |
| `git blame <file>` | Show who last modified each line of a file | git --print-out |
| `git show <commit>` | Show any object (commit, tag, tree, blob) in human-readable form | git --print-out |

---

## 14. Ways to Reference a Commit

| Reference | Example | Description | Source |
|---|---|---|---|
| Branch name | `main` | Tip of the named branch | git --print-out |
| Tag | `v0.1` | A named, annotated point in history | git --print-out |
| Commit SHA | `3e887ab` | Unique 7-40 character hash of a specific commit | git --print-out |
| Remote branch | `origin/main` | The last known tip of a remote branch | git --print-out |
| Current commit | `HEAD` | Pointer to the currently checked-out commit | git --print-out |
| Relative (caret) | `HEAD^^^` | Three commits before HEAD (each `^` = one parent) | git --print-out |
| Relative (tilde) | `HEAD~3` | Three commits before HEAD (equivalent to `HEAD^^^`) | git --print-out |

> [!NOTE]
> `HEAD~3` and `HEAD^^^` are equivalent. The tilde syntax (`~N`) is easier to read for larger numbers.

---

*Part of the [GIT&GITHUB](../README.md) learning path.*
