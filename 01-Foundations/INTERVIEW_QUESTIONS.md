<div align="center">

<h1>Module 01 — Interview Questions</h1>
<h3>Init, Add, Commit, Status, Log, Diff & File Operations</h3>

[![Module](https://img.shields.io/badge/Module-01%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Beginner–Intermediate-yellow.svg)](#)
[![Questions](https://img.shields.io/badge/Questions-30-orange.svg)](#)

**[← Module 00 Interview Questions](../00-Introduction/INTERVIEW_QUESTIONS.md) · [Module 01 Content](README.md) · [Next: Module 02 Interview Questions →](../02-Intermediate-Workflows/INTERVIEW_QUESTIONS.md)**

</div>

---

These are real interview questions based on the concepts covered in Module 01. These are among the **most commonly asked Git questions** in junior and mid-level developer interviews.

---

## 📋 Table of Contents

- [L1 — Conceptual Basics](#l1--conceptual-basics)
- [L2 — Applied Knowledge](#l2--applied-knowledge)
- [L3 — Scenario & Tricky](#l3--scenario--tricky)
- [Read the Output](#-read-the-output)
- [Quick-Fire Round](#-quick-fire-round)

---

## L1 — Conceptual Basics

**Q1. What does `git init` do?**

> It initialises a new Git repository in the current directory by creating a hidden `.git/` folder. This folder contains all the data structures Git needs: the object database, references, and configuration. Nothing is tracked yet — you still need to add files.

---

**Q2. What is the staging area in Git?**

> The staging area (also called the **index**) is a preparation zone between your working directory and your repository. When you run `git add`, you copy a snapshot of the file into the staging area. When you run `git commit`, Git packages everything currently in the staging area into a permanent commit. It lets you build commits incrementally — you don't have to commit every changed file at once.

---

**Q3. What does `git add .` do?**

> It stages **all changes** in the current directory and subdirectories — new files, modified files, and deleted files. It does not stage files that are excluded by `.gitignore`.

---

**Q4. What is a Git commit?**

> A commit is a permanent snapshot of your staged changes saved in the repository. Each commit has:
> - A unique **SHA hash** (e.g., `a3f5c9d`) as its ID
> - The **author name and email** (from `git config`)
> - A **timestamp**
> - A **commit message** you write
> - A pointer to its **parent commit** (all commits form a linked chain)

---

**Q5. What does `git status` show you?**

> It shows the current state of your working directory and staging area:
> - Files with **staged changes** (ready to commit)
> - Files with **unstaged changes** (modified but not yet staged)
> - **Untracked files** (new files Git has never seen)
> - Which branch you are on
> - Whether your branch is ahead or behind the remote

---

**Q6. What is `git log` used for?**

> `git log` displays the commit history of the current branch. Each entry shows the commit SHA, author, date, and commit message. By default it shows the most recent commits first.

---

**Q7. What is `git diff`?**

> `git diff` shows the exact line-by-line differences between two states. By default (no arguments) it shows changes in your working directory that are **not yet staged**. `git diff --staged` shows changes that are staged but not yet committed.

---

## L2 — Applied Knowledge

**Q8. What is the difference between `git add .` and `git add -A`?**

> In modern Git (2.x) they behave the same from the repository root — both stage all changes including deletions. The historical difference was that `git add .` in older Git didn't stage deletions in parent directories. Today, prefer `git add .` from the project root for clarity.

---

**Q9. You modified 5 files but you only want to commit 2 of them. How do you do it?**

> Stage only the specific files you want:
> ```bash
> git add file1.js file2.css
> git commit -m "feat: update header styles and component"
> ```
> The other 3 files remain modified in your working directory, unstaged.

---

**Q10. What is `git add -p` (patch mode)?**

> It lets you interactively stage parts of a file — called **hunks**. Git shows each changed section and asks `Stage this hunk?` You can say `y` (yes), `n` (no), or `s` (split the hunk further). Useful when you have multiple unrelated changes in one file and want to commit them separately.

---

**Q11. What happens if you run `git commit` without `-m`?**

> Git opens your configured text editor (e.g., VS Code, Vim) so you can write a multi-line commit message. The commit proceeds when you save and close the editor. If you close without writing a message, the commit is aborted.

---

**Q12. What is `git commit -am` and when should you NOT use it?**

> `git commit -am "message"` stages all **tracked, modified** files and commits them in one step — skipping `git add`. You should NOT use it when:
> - You have **new (untracked) files** that need to be committed — `-am` won't stage them
> - You only want to commit **some** modified files, not all
> - You want to review what you're committing before it's committed

---

**Q13. How do you undo the last `git add` (unstage a file without losing changes)?**

> ```bash
> git restore --staged filename.txt
> # or older syntax:
> git reset HEAD filename.txt
> ```
> This moves the file back to the working directory (unstaged) without touching its content.

---

**Q14. What does `git rm` do? How is it different from just deleting a file?**

> `git rm` removes a file from both the working directory and the staging area in one step. If you just delete a file with `rm` or in your file explorer, the deletion is an unstaged change — you still need `git add` (or `git add -A`) to stage it. `git rm` stages the deletion immediately.

---

**Q15. What does `git rm --cached` do?**

> It removes a file from the staging area (stops tracking it) but **keeps the file on disk**. Common use case: you accidentally committed a file that should be in `.gitignore`. You run `git rm --cached secrets.env` to untrack it, then add it to `.gitignore`.

---

**Q16. What does `git mv` do?**

> It renames or moves a file and stages that rename in one step:
> ```bash
> git mv old-name.js new-name.js
> ```
> Equivalent to doing `mv old-name.js new-name.js`, then `git rm old-name.js`, then `git add new-name.js` — but in one command. Git also preserves the file's history across the rename.

---

**Q17. What are the useful variants of `git log`?**

> ```bash
> git log --oneline              # one commit per line (short SHA + message)
> git log --graph --oneline      # ASCII branch graph
> git log --author="Name"        # commits by a specific author
> git log --since="2 weeks ago"  # time-based filter
> git log -n 5                   # last 5 commits only
> git log --stat                 # shows files changed per commit
> git log -p                     # shows full diff for each commit
> git log filename.js            # commits that touched a specific file
> ```

---

## L3 — Scenario & Tricky

**Q18. What is a SHA hash in Git? Why is it important?**

> Every commit, file, and tree in Git is identified by a **SHA-1 hash** — a 40-character hexadecimal string (e.g., `a3f5c9d2...`). It is computed from the content of the commit (author, message, timestamp, parent, and all file contents). If even one character in the commit changes, the SHA changes completely. This makes Git history **tamper-evident** — you can verify any commit's integrity.

---

**Q19. You staged a file and then made more changes to it. What does `git commit` capture?**

> Only the snapshot that was staged at the time of `git add` — **not** the newer changes. The newer changes remain in the working directory as unstaged modifications. This is why the staging area matters: Git commits the staged snapshot, not the current file state.

---

**Q20. Can you change a commit message after committing?**

> Yes, if the commit hasn't been pushed to a shared remote:
> ```bash
> git commit --amend -m "corrected message"
> ```
> This replaces the last commit with a new one (new SHA). Never amend a commit that others have already pulled — it rewrites history and causes problems.

---

**Q21. What is the difference between `git diff` and `git diff --staged`?**

> | Command | Shows |
> |---|---|
> | `git diff` | Changes in working directory that are **not staged** |
> | `git diff --staged` | Changes that **are staged** and ready to commit |
> | `git diff HEAD` | All changes since the last commit (staged + unstaged) |

---

**Q22. Why is an empty commit message not allowed?**

> Git requires a non-empty commit message to enforce meaningful history. A blank message would make it impossible to understand what the commit does when reading the log. If you accidentally open the editor and close it without writing, Git aborts the commit with: `Aborting commit due to empty commit message.`

---

**Q23. What is a "working tree clean" state?**

> It means there are no modified, staged, or untracked files — your working directory exactly matches the last commit. You see this message after a clean `git status` output: `nothing to commit, working tree clean`.

---

## 📖 Read the Output

**Q24. What do the `+` and `-` signs mean in `git diff` output?**

```diff
-const greeting = "Hello";
+const greeting = "Hello, World!";
```

> Lines starting with `-` (in red) were **removed** from the old version. Lines starting with `+` (in green) were **added** in the new version. Lines with neither sign are unchanged context lines.

---

**Q25. What does the `@@` line in `git diff` output mean?**

```
@@ -12,7 +12,8 @@
```

> This is the **hunk header**. It tells you: in the old file, this hunk starts at line 12 and spans 7 lines (`-12,7`). In the new file, it starts at line 12 and spans 8 lines (`+12,8`).

---

**Q26. What does this `git log` output tell you?**

```
commit a3f5c9d (HEAD -> main, origin/main)
Author: Jane Doe <jane@example.com>
Date:   Mon Apr 14 10:23:01 2026 +0530

    feat: add login form validation
```

> - `a3f5c9d` — short SHA of the commit
> - `HEAD -> main` — your current branch pointer is here
> - `origin/main` — the remote also has this commit (branches are in sync)
> - `Author` — who made the commit (from their `git config`)
> - `feat: add login form validation` — the commit message

---

**Q27. You run `git status` and see `Changes not staged for commit`. What does that mean?**

> Git is tracking these files (they've been committed before), and they have been modified since the last commit, but you haven't run `git add` yet. They won't be included in the next commit until you stage them.

---

## ⚡ Quick-Fire Round

| Question | Answer |
|---|---|
| Command to initialize a repo | `git init` |
| Command to stage all changes | `git add .` |
| Command to commit with a message | `git commit -m "message"` |
| Command to see what's staged/unstaged | `git status` |
| Command to see unstaged diff | `git diff` |
| Command to see staged diff | `git diff --staged` |
| Command to see one commit per line | `git log --oneline` |
| Command to stop tracking a file (keep on disk) | `git rm --cached filename` |
| Command to rename a tracked file | `git mv old new` |
| What `-am` skips | New (untracked) files |
| What uniquely identifies a commit | SHA hash |
| Can you stage part of a file? | Yes — `git add -p` |

---

<div align="center">

**[← Module 00 Interview Questions](../00-Introduction/INTERVIEW_QUESTIONS.md) · [Module 01 Content](README.md) · [Next: Module 02 Interview Questions →](../02-Intermediate-Workflows/INTERVIEW_QUESTIONS.md)**

*These questions come up in almost every Git-related interview. Know them cold.*

</div>
