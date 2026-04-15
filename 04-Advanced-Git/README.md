<div align="center">

<h1>Module 04 — Advanced Git</h1>
<h3>Rebase, Cherry-pick, Reflog & History Rewriting</h3>

[![Module](https://img.shields.io/badge/Module-04%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Advanced-red.svg)](#)
[![Commands](https://img.shields.io/badge/Commands-13-purple.svg)](#3-the-cheat-code-section)
[![Diagrams](https://img.shields.io/badge/Diagrams-2%20gitGraphs-teal.svg)](#2-visual-diagrams)
[![Lab](https://img.shields.io/badge/Lab-Interactive%20Rebase-orange.svg)](#4-hands-on-lab)
[![Free](https://img.shields.io/badge/License-MIT-blue.svg)](../LICENSE)

**[← 03 Remote Collaboration](../03-Remote-Collaboration/README.md) · [Course Home](../README.md) · [05 GitHub Expertise →](../05-GitHub-Expertise/README.md)**

> [!WARNING]
> This module covers commands that **rewrite commit history**. Understand each command before running it. The lab is designed to be safe — always work on a practice branch, never on `main`.

</div>

---

## 📋 Module Contents

- [Learning Objectives](#-learning-objectives)
- [1. Theoretical Explanation](#1-theoretical-explanation)
  - [Rebase: Replaying Commits](#rebase-replaying-commits)
  - [Interactive Rebase (-i)](#interactive-rebase--i)
  - [Cherry-Pick: Copying a Commit](#cherry-pick-copying-a-commit)
  - [Reflog: Git's Undo History](#reflog-gits-undo-history)
  - [git reset — Three Modes](#git-reset--three-modes)
  - [git commit --amend](#git-commit---amend)
  - [git restore](#git-restore-file)
- [2. Visual Diagrams](#2-visual-diagrams)
- [3. The "Cheat Code" Section](#3-the-cheat-code-section)
- [4. Hands-on Lab](#4-hands-on-lab)

---

## 🎯 Learning Objectives

By the end of this module you will be able to:

1. Rebase a branch onto another.
2. Interactively squash and reorder commits.
3. Cherry-pick individual commits.
4. Use reflog to recover from mistakes.
5. Understand `git reset` hard/soft/mixed.

---

## 1. Theoretical Explanation

### Rebase: Replaying Commits

**Rebase** takes the commits on your current branch and replays them one by one on top of another branch. Each replayed commit gets a brand-new SHA — even if the content is identical — because its parent commit has changed.

**Why use rebase?**
- Keeps a clean, linear history (no merge commits cluttering `git log`)
- Makes it look like your feature was built on top of the latest main, even if you branched from an older commit
- Makes code review easier — reviewers see a clean sequence of changes

> [!WARNING]
> Rebasing rewrites commit history. **Never rebase a branch that others are currently working on.** If you push a rebased branch that others have based work on, their history diverges and they'll face painful conflicts.

### Interactive Rebase (`-i`)

`git rebase -i HEAD~N` opens an editor with the last N commits listed. You can:

| Action | Effect |
|---|---|
| `pick` | Keep the commit as-is (default) |
| `squash` (s) | Combine this commit with the previous one; merge messages |
| `fixup` (f) | Combine with previous commit; discard this commit's message |
| `reword` (r) | Keep the commit but edit its message |
| `drop` (d) | Delete the commit entirely |
| `edit` (e) | Pause and let you amend the commit |

### Cherry-Pick: Copying a Commit

`git cherry-pick <SHA>` copies a single commit from anywhere in history onto the current branch. The original commit stays where it was; a new commit with the same changes (but a new SHA) is added to your current branch.

Use cases:
- Backporting a bug fix to a release branch
- Grabbing one feature commit from a larger branch that's not ready to merge

### Reflog: Git's Undo History

The **reflog** records every position HEAD has been at — every commit, every reset, every checkout, every rebase step. It's stored locally and retained for ~30 days by default.

This is your ultimate safety net. Even if you do `git reset --hard` and "lose" commits, the reflog has their SHAs.

> [!NOTE]
> `git reflog` is your safety net. Even after `git reset --hard`, commits are recoverable for ~30 days via the reflog. Run `git reflog BRANCHNAME` to find the SHA of the commit you want to recover, then `git reset --hard <SHA>` to restore it.

### `git reset` — Three Modes

| Command | Moves HEAD? | Clears Staging Area? | Clears Working Directory? | Use For |
|---|---|---|---|---|
| `git reset HEAD^` (mixed, default) | Yes | Yes | No | Undo last commit, keep changes staged/unstaged |
| `git reset --soft HEAD^` | Yes | No | No | Undo last commit, keep changes staged |
| `git reset --hard <commit>` | Yes | Yes | **Yes** | Nuclear reset — all changes gone |

> [!WARNING]
> `git reset --hard` is destructive — it permanently discards all uncommitted changes in both the staging area and the working directory. Use with extreme caution.

### `git commit --amend`

Amend modifies the **most recent commit**. You can:
- Change the commit message
- Add files you forgot to stage

```bash
# Forgot to add a file:
git add forgotten-file.txt
git commit --amend --no-edit  # keeps existing message

# Change the commit message:
git commit --amend -m "Better commit message"
```

> [!WARNING]
> Amending rewrites the commit (new SHA). Never amend a commit that has already been pushed to a shared remote.

### `git restore <file>`

A modern, focused command for discarding changes:
- `git restore <file>` — discard unstaged changes to one file
- `git restore --staged --worktree <file>` — discard all staged and unstaged changes to one file
- `git restore <file> --source <commit>` — restore a file to its state at a specific commit

---

## 2. Visual Diagrams

### Diagram A — Rebase (Before and After)

Before rebase — `feature` branched from an older `main`:
```mermaid
gitGraph
   commit id: "A"
   commit id: "B"
   branch feature
   commit id: "D (original)"
   commit id: "E (original)"
   checkout main
   commit id: "C"
```

After `git rebase main` — commits replayed on top of C:
```mermaid
gitGraph
   commit id: "A"
   commit id: "B"
   commit id: "C"
   branch feature
   commit id: "D' (replayed)"
   commit id: "E' (replayed)"
```

### Diagram B — Cherry-Pick

```mermaid
gitGraph
   commit id: "A"
   commit id: "B"
   branch feature
   commit id: "D"
   commit id: "E"
   checkout main
   commit id: "C"
   commit id: "D' (cherry-picked from feature)"
```

---

## 3. The "Cheat Code" Section

| Command | Description |
|---|---|
| `git rebase <branch>` | Apply commits of current branch ahead of specified branch |
| `git rebase -i HEAD~6` | Interactively rebase last 6 commits (squash, fixup, reorder, drop) |
| `git reset HEAD^` | Undo last commit; keep changes in working directory |
| `git reset --hard <commit>` | Move HEAD to commit and discard all subsequent changes |
| `git reset --hard` | Delete all staged and unstaged changes (destructive!) |
| `git commit --amend` | Edit the most recent commit message or add a forgotten file |
| `git cherry-pick <commit>` | Copy a single commit onto the current branch |
| `git reflog BRANCHNAME` | Find commit IDs in reflog to recover from a failed rebase or reset |
| `git restore <file>` | Discard unstaged changes to one file |
| `git restore --staged --worktree <file>` | Discard all staged and unstaged changes to one file |
| `git restore <file> --source <commit>` | Restore a file to its state at a specific commit |
| `git clean` | Delete untracked files from working directory |
| `git show <SHA>` | Show any object in Git in human-readable format |

---

## 4. Hands-on Lab

### Lab: "Clean Up History with Interactive Rebase"

This is one of the most powerful tools in Git for maintaining a professional commit history.

**Step 1 — Create a practice branch:**
```bash
git switch -c cleanup-practice
```

**Step 2 — Make 5 quick commits:**
```bash
echo "Word 1" >> story.txt && git add . && git commit -m "wip: add word 1"
echo "Word 2" >> story.txt && git add . && git commit -m "wip: add word 2"
echo "Word 3" >> story.txt && git add . && git commit -m "wip: add word 3"
echo "Word 4" >> story.txt && git add . && git commit -m "wip: add word 4"
echo "Word 5" >> story.txt && git add . && git commit -m "wip: add word 5"
```

**Step 3 — See the messy history:**
```bash
git log --oneline
```
You'll see 5 separate "wip" commits.

**Step 4 — Start interactive rebase:**
```bash
git rebase -i HEAD~5
```
Your editor opens with 5 lines like:
```
pick abc1234 wip: add word 1
pick def5678 wip: add word 2
pick ghi9012 wip: add word 3
pick jkl3456 wip: add word 4
pick mno7890 wip: add word 5
```

**Step 5 — Squash commits 2–5 into commit 1:**  
Change `pick` to `fixup` (or `f`) for lines 2–5:
```
pick abc1234 wip: add word 1
fixup def5678 wip: add word 2
fixup ghi9012 wip: add word 3
fixup jkl3456 wip: add word 4
fixup mno7890 wip: add word 5
```
Save and exit the editor.

**Step 6 — Verify the clean history:**
```bash
git log --oneline
```
You now have 1 combined commit instead of 5.

**Step 7 — Rename the commit message:**
```bash
git commit --amend -m "feat: build initial story with 5 words"
```

**Step 8 — Practice recovery:**  
Deliberately "lose" the commit:
```bash
git reset --hard HEAD~1
git log --oneline
```
The commit appears gone!

**Step 9 — Use reflog to find it:**
```bash
git reflog cleanup-practice
```
Find the SHA of your "lost" commit (look for the line before the reset).

**Step 10 — Recover:**
```bash
git reset --hard <SHA>
git log --oneline
```
Your commit is back. You've got this — the reflog is always watching.

> [!TIP]
> Before any risky operation (hard reset, rebase, amend), note your current commit SHA with `git log --oneline -1`. If something goes wrong, you have the SHA ready for reflog recovery.

---

<div align="center">

| ← Previous | Home | Next → |
|:---:|:---:|:---:|
| [03 — Remote Collaboration](../03-Remote-Collaboration/README.md) | [📖 Course Home](../README.md) | [05 — GitHub Expertise](../05-GitHub-Expertise/README.md) |

**[📋 Full Cheat Sheet](../CHEATSHEET.md) · [🛠️ Practice Lab](../Practice-Lab/README.md) · [📄 License](../LICENSE)**

*Part of the free, open-source [GIT&GITHUB](../README.md) curriculum — MIT Licensed.*

</div>
