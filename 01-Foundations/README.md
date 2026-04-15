<div align="center">

<h1>Module 01 — Foundations</h1>
<h3>Init, Add, Commit, Status & Log</h3>

[![Module](https://img.shields.io/badge/Module-01%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Beginner-brightgreen.svg)](#)
[![Commands](https://img.shields.io/badge/Commands-16-purple.svg)](#3-the-cheat-code-section)
[![Lab](https://img.shields.io/badge/Lab-Your%20First%20Repository-orange.svg)](#4-hands-on-lab)
[![Free](https://img.shields.io/badge/License-MIT-blue.svg)](../LICENSE)

**[← 00 Introduction](../00-Introduction/README.md) · [Course Home](../README.md) · [02 Intermediate →](../02-Intermediate-Workflows/README.md)**

</div>

---

## 📋 Module Contents

- [Learning Objectives](#-learning-objectives)
- [1. Theoretical Explanation](#1-theoretical-explanation)
  - [git init & .git/ Directory](#git-init-and-the-git-directory)
  - [The Staging Area (Index)](#the-staging-area-index)
  - [Atomic Commits](#atomic-commits)
  - [Commit SHAs](#commit-shas)
  - [git status Output](#git-status-output)
- [2. Visual Diagram](#2-visual-diagram)
- [3. The "Cheat Code" Section](#3-the-cheat-code-section)
- [4. Hands-on Lab](#4-hands-on-lab)

---

## 🎯 Learning Objectives

By the end of this module you will be able to:

1. Initialize a Git repository.
2. Track files through the staging area.
3. Create commits with descriptive messages.
4. Read commit history.

---

## 1. Theoretical Explanation

### `git init` and the `.git/` Directory

When you run `git init` inside a directory, Git creates a hidden `.git/` subdirectory. This is the **entire repository** — all history, configuration, and metadata lives here.

What's inside `.git/`:

| Item | Purpose |
|---|---|
| `HEAD` | Pointer to the currently checked-out branch |
| `config` | Repository-level configuration |
| `objects/` | All commits, trees, blobs (your actual file content) |
| `refs/` | Branch and tag pointers |
| `index` | The staging area (the list of what will go into the next commit) |
| `COMMIT_EDITMSG` | Most recent commit message |

> [!WARNING]
> Never delete the `.git/` directory. It contains your **entire project history**. Deleting it permanently destroys all commits, branches, and tags. There is no recovery (outside of a remote backup).

### The Staging Area (Index)

The **staging area** — also called the **index** — is one of Git's most powerful and often misunderstood features.

**Why does it exist?** It solves a real problem: you may have modified 10 files, but you only want to commit 3 of them as a single logical change. The staging area lets you carefully select exactly what goes into each commit, creating a clean, meaningful history.

Think of it like this:
- Your **working directory** is your messy desk.
- The **staging area** is the neatly arranged pile you're about to put in an envelope.
- The **commit** is sealing and mailing that envelope — it's now permanent.

### Atomic Commits

An **atomic commit** contains exactly one logical change. Good examples:
- `fix: correct off-by-one error in calculateTotal()`
- `feat: add user login endpoint`
- `docs: update README with setup instructions`

Bad examples:
- `changes` (what changes?)
- `fix bug and add feature and update tests` (three things at once)

Atomic commits make code review easier, make `git bisect` work perfectly, and make reverting mistakes surgical rather than catastrophic.

### Commit SHAs

Every commit is identified by a **SHA-1 hash** — a 40-character hexadecimal string like `3e887ab2f1c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7`. This is computed from the commit's content (author, message, timestamp, parent commit, and file tree). Because it's deterministic, a SHA uniquely and permanently identifies a commit. **Commits are immutable** — changing anything about a commit produces a completely different SHA.

In practice, you only need the first 7 characters (e.g., `3e887ab`) — Git can find the full commit from a unique short prefix.

### `git status` Output

`git status` shows three categories:

| Category | Meaning |
|---|---|
| **Untracked files** | New files Git has never seen — not staged, not committed |
| **Changes not staged** | Files Git knows about (tracked) that have been modified but not staged |
| **Changes to be committed** | Files staged and ready to go into the next commit |

---

## 2. Visual Diagram

The lifecycle of a file from creation through commit:

```mermaid
sequenceDiagram
    participant WD as Working Directory
    participant SA as Staging Area
    participant LR as Local Repository

    WD->>SA: git add &lt;file&gt;
    Note over SA: File is staged (indexed)
    SA->>WD: git reset &lt;file&gt;
    Note over WD: File is unstaged, changes kept
    SA->>LR: git commit -m "message"
    Note over LR: Snapshot is permanently stored
    LR->>WD: git restore &lt;file&gt; / git checkout &lt;file&gt;
    Note over WD: File restored to committed state
```

---

## 3. The "Cheat Code" Section

| Command | Description |
|---|---|
| `git init` | Initialize an existing directory as a Git repository |
| `git status` | Show modified files in working directory staged for next commit |
| `git add <file>` | Stage a specific file for the next commit |
| `git add .` | Stage all untracked files and changes in current directory |
| `git add -p` | Interactively choose which hunks (parts) of a file to stage |
| `git reset <file>` | Unstage a file while keeping changes in working directory |
| `git reset` | Unstage everything — all changes remain in working directory |
| `git diff` | Show changes in working directory not yet staged |
| `git diff --staged` | Show staged changes not yet committed |
| `git diff HEAD` | Show all staged and unstaged changes vs. last commit |
| `git commit` | Open text editor to write a full commit message |
| `git commit -m 'message'` | Commit staged snapshot with an inline message |
| `git commit -am 'message'` | Stage all tracked changes and commit in one step |
| `git log` | Show full commit history with author, date, and message |
| `git log --oneline` | Show condensed one-line commit history |
| `git log --graph main` | Show visual ASCII branch graph for main |

---

## 4. Hands-on Lab

### Lab: "Your First Repository — Track a Project"

You've got this! Let's build your first Git-tracked project from scratch.

**Step 1 — Create a new directory:**
```bash
mkdir my-first-repo && cd my-first-repo
```

**Step 2 — Initialize the repository:**
```bash
git init
```
Output: `Initialized empty Git repository in /path/to/my-first-repo/.git/`

**Step 3 — Create a file:**
```bash
echo "# My Project" > README.md
```

**Step 4 — Check status:**
```bash
git status
```
Observe: `README.md` appears under **Untracked files** in red.

**Step 5 — Stage it:**
```bash
git add README.md
```

**Step 6 — Check status again:**
```bash
git status
```
Observe: `README.md` now appears under **Changes to be committed** in green.

**Step 7 — Commit:**
```bash
git commit -m "Initial commit: add README"
```

**Step 8 — View history:**
```bash
git log
```
You'll see your commit with its full SHA, author, date, and message.

**Step 9 — View condensed history:**
```bash
git log --oneline
```
Much cleaner! You'll see the short SHA and message on one line.

**Step 10 — Make a second commit:**
```bash
echo "This is my first Git project." >> README.md
git diff
```
Observe the `+` line showing your addition. Now stage and commit:
```bash
git add .
git commit -m "Update README with project description"
```

**Step 11 — View full history:**
```bash
git log --oneline
```
You now have two commits. Congratulations — you understand the core Git workflow!

> [!TIP]
> The pattern you just practiced — **edit → stage → commit** — is the heartbeat of Git. Everything else in this course builds on these three steps.

---

## 5. 🏋️ Practice Exercises

> These exercises are designed to be done in a real terminal on real files. Don't just read them — run them. Confidence comes from doing, not watching.

---

### Exercise 1 — The Selective Stage (Core Skill)
You have 5 files. You must stage **only 2** of them. Everything else stays untracked.

**Setup:**
```bash
mkdir staging-practice && cd staging-practice
git init
echo "File A content" > file-a.txt
echo "File B content" > file-b.txt
echo "File C content" > file-c.txt
echo "File D content" > file-d.txt
echo "File E content" > file-e.txt
git status
```

**Your task:** Stage `file-b.txt` and `file-d.txt` only. Do NOT touch the others.
```bash
# Only these two:
git add file-b.txt file-d.txt
git status
```

- [ ] **Done** when `git status` shows `file-b.txt` and `file-d.txt` under "Changes to be committed" (green) and the other three under "Untracked files" (red)

> [!TIP]
> You can stage multiple files in one `git add` command by listing them space-separated. You can also use `git add *.txt` but that would stage all five — not what we want here.

---

### Exercise 2 — The Two-State Diff
Modify a file, stage it, then modify it again. See all three states at once.

**Setup** (continue in `staging-practice/`):
```bash
echo "Original line" > story.txt
git add story.txt
```

Now modify it AGAIN before committing:
```bash
echo "New line added after staging" >> story.txt
```

**Your tasks:**
```bash
git diff           # What does this show?
git diff --staged  # What does this show?
git diff HEAD      # What does this show?
git status         # Notice story.txt appears in BOTH sections
```

- [ ] **Done** when you can explain the difference between all three diff outputs

**Expected insight:** `git diff` shows the unstaged change (the new line). `git diff --staged` shows the staged version. `git status` shows `story.txt` listed twice — once staged, once modified. This is Git's staging area working as designed.

---

### Exercise 3 — Stage in Patches with `git add -p`
Stage only one part of a file that has two separate changes.

**Setup:**
```bash
cat > features.txt << 'EOF'
Feature 1: User login
Feature 2: User logout
Feature 3: Password reset
EOF
git add features.txt && git commit -m "add: initial features list"
```

Now make two unrelated changes in the same file:
```bash
sed -i 's/User login/User login via OAuth/' features.txt
echo "Feature 4: Email verification" >> features.txt
```

**Your task:** Use `git add -p` to stage ONLY the OAuth change, not the new Feature 4 line.
```bash
git add -p features.txt
# Press 's' to split the hunk if Git shows both changes together
# Press 'y' to stage the hunk you want
# Press 'n' to skip the hunk you don't want
git diff --staged   # Should show only the OAuth change
git diff            # Should show only the Feature 4 line
```

- [ ] **Done** when `git diff --staged` shows only the OAuth line and `git diff` shows only Feature 4

---

### Exercise 4 — Three Atomic Commits
Practice the discipline of one logical change = one commit.

**Task:** From scratch, create a project with exactly 3 commits — each covering one logical change.

```bash
mkdir atomic-commits && cd atomic-commits
git init

# Commit 1: Project scaffold
echo "# My Project" > README.md
git add README.md
git commit -m "docs: add initial README"

# Commit 2: Add a feature file
echo "function greet() { return 'hello'; }" > greet.js
git add greet.js
git commit -m "feat: add greet function"

# Commit 3: Add documentation for the feature
echo "## greet()\nReturns the string 'hello'." >> README.md
git add README.md
git commit -m "docs: document greet function in README"
```

Verify:
```bash
git log --oneline
```

- [ ] **Done** when `git log --oneline` shows exactly 3 commits with descriptive messages

**Why this matters:** Real-world Git history is read by humans. A commit named `feat: add greet function` tells a reviewer exactly what changed and why — without opening a single file.

---

### Exercise 5 — Stage, Unstage, Re-stage
Practice the full staging area cycle: add → reset → add selectively.

**Task:**
```bash
mkdir unstage-practice && cd unstage-practice
git init
echo "content" > alpha.txt
echo "content" > beta.txt
echo "content" > gamma.txt

# Stage all three
git add .
git status   # All three staged

# Unstage beta.txt only
git reset beta.txt
git status   # alpha and gamma staged, beta untracked

# Unstage everything
git reset
git status   # All three untracked again

# Now stage only gamma.txt
git add gamma.txt
git commit -m "feat: add gamma only"
git status   # alpha and beta still untracked, gamma committed
```

- [ ] **Done** when the final `git status` shows only `alpha.txt` and `beta.txt` as untracked

---

### Exercise 6 — Read History Like a Pro
Practice the different ways to view commit history.

**Task** (use the `atomic-commits` repo from Exercise 4):
```bash
# Full history
git log

# Condensed
git log --oneline

# With graph (useful once you have branches)
git log --oneline --graph --all

# Last commit only
git log -1

# History of one specific file
git log --oneline README.md

# See what actually changed in the last commit
git show HEAD
```

- [ ] **Done** when you understand what each command outputs and when you'd use each one

---

### 🎯 Module 01 Self-Assessment

Test yourself — can you do each of these from memory?

| Challenge | Confident? |
|---|:---:|
| Create a new repo from scratch | ☐ Yes ☐ Need practice |
| Stage 2 out of 5 files | ☐ Yes ☐ Need practice |
| Unstage a file without losing changes | ☐ Yes ☐ Need practice |
| Explain what `git diff` vs `git diff --staged` shows | ☐ Yes ☐ Need practice |
| Use `git add -p` to stage partial changes | ☐ Yes ☐ Need practice |
| Write a good atomic commit message | ☐ Yes ☐ Need practice |
| Read history with `git log --oneline` | ☐ Yes ☐ Need practice |

Mark every row "Yes" before moving to Module 02. Any "Need practice" rows → go back and redo that exercise.

---

<div align="center">

| ← Previous | Home | Next → |
|:---:|:---:|:---:|
| [00 — Introduction](../00-Introduction/README.md) | [📖 Course Home](../README.md) | [02 — Intermediate Workflows](../02-Intermediate-Workflows/README.md) |

**[📋 Full Cheat Sheet](../CHEATSHEET.md) · [🛠️ Practice Lab](../Practice-Lab/README.md) · [📄 License](../LICENSE)**

*Part of the free, open-source [GIT&GITHUB](../README.md) curriculum — MIT Licensed.*

</div>
