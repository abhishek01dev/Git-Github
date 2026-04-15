<div align="center">

<h1>Module 00 — Introduction</h1>
<h3>Why Git? Version Control, Setup & Configuration</h3>

[![Module](https://img.shields.io/badge/Module-00%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Absolute%20Beginner-brightgreen.svg)](#)
[![Commands](https://img.shields.io/badge/Commands-8-purple.svg)](#3-the-cheat-code-section)
[![Lab](https://img.shields.io/badge/Lab-Your%20First%20Git%20Identity%20Setup-orange.svg)](#4-hands-on-lab)
[![Free](https://img.shields.io/badge/License-MIT-blue.svg)](../LICENSE)

**[← Course Home](../README.md) · [Next: Foundations →](../01-Foundations/README.md) · [📋 Full Cheat Sheet](../CHEATSHEET.md)**

</div>

---

## 📋 Module Contents

- [Learning Objectives](#-learning-objectives)
- [1. Theoretical Explanation](#1-theoretical-explanation)
  - [What Is a VCS?](#what-is-a-version-control-system)
  - [Distributed vs. Centralized VCS](#distributed-vs-centralized-vcs)
  - [A Brief History of Git](#a-brief-history-of-git)
  - [Git's Three States](#gits-three-states)
  - [Installing Git](#installing-git)
- [2. Visual Diagram](#2-visual-diagram)
- [3. The "Cheat Code" Section](#3-the-cheat-code-section)
- [4. Hands-on Lab](#4-hands-on-lab)

---

## 🎯 Learning Objectives

By the end of this module you will be able to:

1. Understand what version control is and why Git exists.
2. Install Git on Windows, macOS, and Linux.
3. Configure global identity settings.

---

## 1. Theoretical Explanation

> **Estimated read time:** 10 minutes · **Lab time:** 10 minutes

### What Is a Version Control System?

A **Version Control System (VCS)** is software that tracks changes to files over time. It allows you to:

- Recall specific versions of files at any point in history.
- See who changed what and when.
- Collaborate with others without overwriting each other's work.
- Experiment freely — because you can always roll back.

### Distributed vs. Centralized VCS

There are two primary architectures for version control systems:

| Type | Examples | How It Works |
|---|---|---|
| **Centralized VCS** | Apache SubVersion (SVN), Piper (used by Google) | Single central server holds all history; developers check out working copies |
| **Distributed VCS** | **Git**, Mercurial | Every developer has a complete local copy of the full repository history |

**Git** is a **distributed** VCS. You have the full history on your machine — no network required to commit, branch, or inspect logs. The server is just another peer.

> [!NOTE]
> The course outline references three VCS systems: **Git** (distributed, open-source), **Apache SubVersion** (centralized, open-source), and **Piper** (Google's internal centralized VCS, used for the monorepo that holds billions of lines of code). Understanding these differences helps you appreciate why Git's design choices matter at scale.

### A Brief History of Git

In 2002, the Linux kernel project used a proprietary distributed VCS called **BitKeeper**. In 2005, a dispute between the Linux community and BitKeeper's developer ended that arrangement. **Linus Torvalds** — creator of Linux — spent just ten days writing the first version of Git himself.

Git was designed with these goals:

- Speed
- Simple design
- Strong support for non-linear development (thousands of parallel branches)
- Fully distributed
- Able to handle large projects like the Linux kernel efficiently

### Git's Three States

Every file in a Git repository lives in one of three states. Understanding this is the single most important mental model in Git.

```
Modified → Staged → Committed
```

| State | Location | Meaning |
|---|---|---|
| **Modified** | Working Directory | You have changed the file but not yet told Git about it |
| **Staged** | Staging Area (Index) | You have marked the change to go into the next commit snapshot |
| **Committed** | Local Repository | The snapshot is safely stored in your local Git database |

> [!NOTE]
> Git tracks **changes**, not files. This is the fundamental mental model shift new users need.

### Installing Git

**Windows:**
```bash
# Option 1: Download the installer from https://git-scm.com/download/win
# Option 2: Use winget
winget install --id Git.Git -e --source winget
```

**macOS:**
```bash
# Option 1: Xcode Command Line Tools (installs Git automatically)
xcode-select --install

# Option 2: Homebrew
brew install git
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt update && sudo apt install git
```

**Linux (Fedora/RHEL):**
```bash
sudo dnf install git
```

Verify installation:
```bash
git --version
# Expected output: git version 2.x.x
```

---

## 2. Visual Diagram

Git's three states and the commands that move files between them:

```mermaid
graph TD
    A["🗂️ Working Directory\n(Modified)"] -->|git add| B["📋 Staging Area\n(Staged)"]
    B -->|git commit| C["🗄️ Local Repository\n(Committed)"]
    C -->|git push| D["☁️ Remote Repository\n(e.g., GitHub)"]
    D -->|git pull / git fetch| C
    B -->|git reset| A
    C -->|git checkout / git restore| A
```

---

## 3. The "Cheat Code" Section

| Command | Description |
|---|---|
| `git config --global user.name "[firstname lastname]"` | Set name used in all version history credit |
| `git config --global user.email "[valid-email]"` | Set email associated with all history markers |
| `git config --global color.ui auto` | Enable automatic colorized output in the terminal |
| `git config --global core.excludesfile [file]` | Set a system-wide ignore pattern file |
| `git config alias.st status` | Add an alias — `git st` becomes shorthand for `git status` |
| `git config --global ...` | Apply any config option globally across all repositories |
| `man git-config` | See all possible configuration options in the manual |
| `git --version` | Verify Git is installed and check the version |

---

## 4. Hands-on Lab

### Lab: "Your First Git Identity Setup"

Great job making it to the first lab! Let's get your Git identity configured.

**Prerequisites:** Git installed (see installation steps above).

**Steps:**

**Step 1 — Verify Git is installed:**
```bash
git --version
```
You should see something like `git version 2.43.0`. If you get a "command not found" error, revisit the installation steps above.

**Step 2 — Set your name:**
```bash
git config --global user.name "Your Name"
```
Replace `"Your Name"` with your actual name (or the name you want to appear in commit history).

**Step 3 — Set your email:**
```bash
git config --global user.email "you@example.com"
```
Use the same email you plan to use for your GitHub account.

**Step 4 — Enable color output:**
```bash
git config --global color.ui auto
```

**Step 5 — Verify your configuration:**
```bash
cat ~/.gitconfig
```
You should see output like:
```ini
[user]
    name = Your Name
    email = you@example.com
[color]
    ui = auto
```

**Step 6 — Add a `st` alias for `status`:**
```bash
git config --global alias.st status
```

**Step 7 — Test the alias:**
```bash
git st
```
You will see: `fatal: not a git repository`. **This is correct at this stage!** You haven't created a repository yet — that's the next module.

> [!TIP]
> Your global config is stored in `~/.gitconfig`. You can edit it directly with any text editor. For example: `code ~/.gitconfig` (VS Code) or `nano ~/.gitconfig`.

**Checkpoint:** You should now have a `~/.gitconfig` file with your name, email, color setting, and `st` alias. You're ready to move to Module 01!

---

---

<div align="center">

| ← Previous | Home | Next → |
|:---:|:---:|:---:|
| *(Start of course)* | [📖 Course Home](../README.md) | [01 — Foundations](../01-Foundations/README.md) |

**[📋 Full Cheat Sheet](../CHEATSHEET.md) · [🛠️ Practice Lab](../Practice-Lab/README.md) · [📄 License](../LICENSE)**

*Part of the free, open-source [GIT&GITHUB](../README.md) curriculum — MIT Licensed.*

</div>
