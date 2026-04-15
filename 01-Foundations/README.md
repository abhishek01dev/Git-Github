# Module 01 — Foundations: Init, Add, Commit, Status, Log

## Learning Objectives

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

**Previous:** [00-Introduction ←](../00-Introduction/README.md)  
**Next:** [02-Intermediate-Workflows →](../02-Intermediate-Workflows/README.md)  
**Cheat Sheet:** [Full Command Reference →](../CHEATSHEET.md)
