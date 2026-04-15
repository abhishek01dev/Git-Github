<div align="center">

<h1>Module 00 — Interview Questions</h1>
<h3>Version Control, Git vs GitHub, Setup & Configuration</h3>

[![Module](https://img.shields.io/badge/Module-00%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Beginner-brightgreen.svg)](#)
[![Questions](https://img.shields.io/badge/Questions-25-orange.svg)](#)

**[← Course Home](../README.md) · [Module 00 Content](README.md) · [Next: Module 01 Interview Questions →](../01-Foundations/INTERVIEW_QUESTIONS.md)**

</div>

---

These are real interview questions based on the concepts covered in Module 00. Questions are split by difficulty — entry-level roles typically ask L1 and L2, while mid-level roles may ask L3.

---

## 📋 Table of Contents

- [L1 — Conceptual Basics](#l1--conceptual-basics)
- [L2 — Applied Knowledge](#l2--applied-knowledge)
- [L3 — Scenario & Tricky](#l3--scenario--tricky)
- [Quick-Fire Round](#-quick-fire-round)

---

## L1 — Conceptual Basics

**Q1. What is Version Control? Why do developers use it?**

> Version Control is a system that records changes to files over time so you can recall specific versions later. Developers use it to collaborate without overwriting each other's work, track the full history of every change, and roll back to any previous state if something breaks.

---

**Q2. What is the difference between Git and GitHub?**

> **Git** is a version control tool that runs locally on your computer. It tracks changes in your files. **GitHub** is a cloud-based hosting service for Git repositories. Git is the software; GitHub is the platform. You can use Git without GitHub (just locally), but you can't use GitHub without Git.

---

**Q3. What is a repository?**

> A repository (repo) is a folder that Git is tracking. It contains your project files plus a hidden `.git/` folder where Git stores the entire history of all changes ever made. There are two types: **local** (on your machine) and **remote** (on GitHub or a server).

---

**Q4. What are the three types of version control systems?**

> 1. **Local VCS** — history stored only on your own machine (e.g., RCS)
> 2. **Centralized VCS (CVCS)** — one central server holds history; everyone connects to it (e.g., SVN, Perforce)
> 3. **Distributed VCS (DVCS)** — every developer has a full copy of the history locally (e.g., Git, Mercurial)

---

**Q5. Who created Git and why?**

> **Linus Torvalds** created Git in **2005**. The Linux kernel team had been using a proprietary DVCS called BitKeeper, but the free license was revoked. Torvalds built Git in about two weeks as a free, fast, distributed alternative.

---

**Q6. What are Git's three states? Explain each briefly.**

> Every file in Git lives in one of three states:
> - **Working Directory** — the actual files you see and edit on disk
> - **Staging Area (Index)** — a "draft" area where you group changes before committing
> - **Repository (.git)** — the permanent history stored by Git after a commit

---

**Q7. What does `git config --global` do?**

> It saves settings to your user-level config file (`~/.gitconfig`) that apply to all repositories on your machine. The most common uses are setting your name and email, which are embedded into every commit you make.

---

**Q8. What is the difference between `git config --global` and `git config --local`?**

> `--global` applies to all repositories for your user account. `--local` (the default) applies only to the current repository and is stored in `.git/config`. Local settings override global ones.

---

## L2 — Applied Knowledge

**Q9. You just installed Git. What are the first two commands you should run?**

> ```bash
> git config --global user.name "Your Name"
> git config --global user.email "you@example.com"
> ```
> These set your identity, which Git embeds into every commit. Without this, your commits will either fail or show the wrong author.

---

**Q10. How do you check what Git version you have installed?**

> ```bash
> git --version
> # git version 2.43.0
> ```

---

**Q11. How do you view all your current Git configuration settings?**

> ```bash
> git config --list
> # or to see where each setting is coming from:
> git config --list --show-origin
> ```

---

**Q12. What is the `.git` folder? Can you delete it?**

> The `.git` folder is where Git stores the entire history of your repository — all commits, branches, tags, and configuration. If you delete it, your folder becomes a plain directory with no Git history. You would lose all version control tracking. Do not delete it unless you intentionally want to "un-Git" a folder.

---

**Q13. What is the difference between a Distributed VCS and a Centralized VCS?**

> In a **Centralized VCS** (like SVN), there is one server with the full history. Developers only have the latest snapshot. If the server goes down, no one can commit or see history.
>
> In a **Distributed VCS** (like Git), every developer has the **full history** on their own machine. You can commit, branch, and work completely offline. The server (GitHub) is just one of many copies.

---

**Q14. What is a `git alias` and how do you create one?**

> An alias is a shortcut for a longer Git command.
> ```bash
> git config --global alias.st status
> git config --global alias.lg "log --oneline --graph"
> ```
> After this, `git st` runs `git status` and `git lg` runs the log command.

---

**Q15. What does `git config --global core.editor "code --wait"` do?**

> It sets VS Code as your default Git editor (for commit messages, rebase instructions, etc.). The `--wait` flag tells Git to wait until you close the VS Code tab before continuing.

---

## L3 — Scenario & Tricky

**Q16. A colleague says "just push to GitHub." What questions would you ask to clarify?**

> Good clarifying questions:
> - Push to which branch — `main`, a feature branch, or a new branch?
> - Do you want to create a Pull Request or push directly?
> - Is the remote set up already (`git remote -v`) or do I need to add it?
> - Should I push my local commits or is there a specific branch to merge first?

---

**Q17. What happens if two developers commit to the same file at the same time in Git? Does Git automatically merge them?**

> Git does not automatically merge conflicts. If both developers changed **different lines** in the same file, Git can often auto-merge. If they changed the **same lines**, Git raises a **merge conflict** and pauses the merge — you must manually choose which version to keep.

---

**Q18. Can you use Git without GitHub?**

> Yes. Git is a local tool. You can `git init`, create commits, create branches, and have a full version history entirely on your own machine without ever touching GitHub. GitHub is only needed when you want to share code or collaborate remotely.

---

**Q19. What is the difference between `git config --global user.email` and the email on your GitHub account?**

> They are independent. Your `git config` email is embedded into your commit objects locally. Your GitHub account email is for login and notifications. However, GitHub matches commit authors to accounts by email — if your `git config` email matches your GitHub account email, GitHub will show your avatar on commits and count them toward your contribution graph.

---

**Q20. You run `git config --global user.name "John"` and then `git config --local user.name "Jane"` inside a repo. Which name appears in commits made inside that repo?**

> **Jane** — local config overrides global config. Settings closer to the repository always take precedence: local > global > system.

---

**Q21. Someone asks: "Is GitHub the same as Git?" How do you explain it simply?**

> Git is like Microsoft Word — it's the software that does the work on your computer. GitHub is like Google Drive — it's the cloud service where you store and share those Word documents. You can use Word without Google Drive. But to share Word docs with others using Drive, you still need Word.

---

**Q22. What are the advantages of DVCS over CVCS?**

> - Work offline — full history is local
> - Faster operations — no network needed for most commands
> - No single point of failure — every clone is a backup
> - Branching is cheap and fast
> - Developers can share code peer-to-peer without a central server

---

## ⚡ Quick-Fire Round

| Question | Answer |
|---|---|
| Who created Git? | Linus Torvalds |
| What year was Git created? | 2005 |
| What file stores global Git config? | `~/.gitconfig` |
| What folder contains local Git history? | `.git/` |
| What's the command to check Git version? | `git --version` |
| What's the default branch name in modern Git? | `main` (was `master`) |
| Is GitHub owned by Microsoft? | Yes (acquired 2018) |
| What does VCS stand for? | Version Control System |
| Name 2 other Git hosting platforms besides GitHub | GitLab, Bitbucket |
| What's the first thing you do after installing Git? | Set `user.name` and `user.email` |

---

<div align="center">

**[← Course Home](../README.md) · [Module 00 Content](README.md) · [Next: Module 01 Interview Questions →](../01-Foundations/INTERVIEW_QUESTIONS.md)**

*Practice these until you can answer without looking. Then move to Module 01.*

</div>
