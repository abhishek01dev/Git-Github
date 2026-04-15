<div align="center">

<h1>🛠️ Practice Lab — Your Personal Git Dojo</h1>

<p><em>This folder is your dedicated workspace. Every commit you push here is a green square on your GitHub profile — visible proof of your consistency.</em></p>

[![30-Day Challenge](https://img.shields.io/badge/Challenge-30%20Days-orange.svg)](#-the-30-day-system)
[![Daily Logs](https://img.shields.io/badge/Daily-Commit%20Logs-blue.svg)](#-step-by-step-setup)
[![Free Forever](https://img.shields.io/badge/Free-Forever-brightgreen.svg)](../LICENSE)

</div>

---

## 📋 Table of Contents

- [Welcome](#-welcome)
- [How This Works](#-how-this-works)
- [Step-by-Step Setup](#-step-by-step-setup)
- [The 30-Day System](#-the-30-day-system)
- [Daily Log Structure](#-daily-log-structure)
- [Folder Naming Convention](#-folder-naming-convention)
- [Progress Tips & Strategies](#-progress-tips--strategies)
- [What to Do When You're Stuck](#-what-to-do-when-youre-stuck)
- [Sharing Your Progress](#-sharing-your-progress)
- [Quick Reference](#-quick-reference)

---

## 👋 Welcome

You're here because you've forked the **[Git-Mastery-Hub](../README.md)** repository. That single fork was itself a Git action — great job taking that step!

This `Practice-Lab/` folder is your personal workspace. The course modules teach you Git. This lab is where you *use* Git to learn Git — a deliberately recursive approach that builds muscle memory through repetition.

> [!TIP]
> The best way to learn Git is to use Git. Commit your logs every single day —
> your commit graph becomes visible proof of your progress.

---

## ⚙️ How This Works

The system is simple:

```
Study a module  →  Run the lab  →  Fill in your log  →  Commit  →  Push  →  Repeat tomorrow
```

Each day you copy the practice template, fill it in after your session, and commit it with a meaningful message. After 30 days, your `Practice-Lab/` folder contains 30 dated log files and your GitHub profile shows 30+ consecutive green squares.

**Why daily commits?**
- Forces you to actually open a terminal every day
- Makes Git commit/push a reflex, not a chore
- Creates an audit trail of your learning — you can look back at Day 3 notes when something clicks on Day 20
- Your future employer can literally see your consistency

---

## 🚀 Step-by-Step Setup

### Step 1 — Confirm your fork is cloned locally

```bash
git remote -v
# Should show YOUR username, not the upstream repo
# origin  https://github.com/YOUR-USERNAME/Git-Mastery-Hub.git (fetch)
# origin  https://github.com/YOUR-USERNAME/Git-Mastery-Hub.git (push)
```

If you cloned the original instead of your fork:
```bash
# Fix the remote to point to your fork
git remote set-url origin https://github.com/YOUR-USERNAME/Git-Mastery-Hub.git
```

---

### Step 2 — Copy the practice template into this folder

```bash
# From the root of the repository:
cp PRACTICE_TEMPLATE.md Practice-Lab/
```

---

### Step 3 — Rename it with today's date and your day number

Use the format: `YYYY-MM-DD_Day-N_log.md`

```bash
# macOS / Linux
mv Practice-Lab/PRACTICE_TEMPLATE.md Practice-Lab/$(date +%Y-%m-%d)_Day-1_log.md

# Windows (PowerShell)
Rename-Item Practice-Lab\PRACTICE_TEMPLATE.md "Practice-Lab\$(Get-Date -Format 'yyyy-MM-dd')_Day-1_log.md"

# Or manually — just rename it yourself
mv Practice-Lab/PRACTICE_TEMPLATE.md Practice-Lab/2026-04-15_Day-1_log.md
```

---

### Step 4 — Open the log file and fill it in

Each log has six sections. Fill them in **after** your study session while the details are fresh:

| Section | What to Write |
|---|---|
| 📚 Module Studied | Which module folder you worked through today |
| ⚡ Commands Practiced | The commands you ran, what you used them for, any gotchas |
| 🔬 Lab Completed | Checkbox + brief outcome of the hands-on lab |
| 💡 Key Takeaways | Max 3 bullet points — the things that actually clicked |
| ❓ Questions / Blockers | Anything you're stuck on — write it out, it helps clarify your thinking |
| ⭐ Confidence Rating | Check one box: 1 (lost) → 5 (could write a blog post) |

---

### Step 5 — Stage and commit your log

```bash
# Stage only your log file (be specific — don't add unrelated files)
git add Practice-Lab/2026-04-15_Day-1_log.md

# Commit with a clear message
git commit -m "log: Day 1 — Module 00 Introduction & git config setup"
```

**Good commit message pattern:**
```
log: Day N — [Module Name] [brief note]

Examples:
log: Day 1 — Module 00 git config and alias setup
log: Day 7 — Module 02 fast-forward vs 3-way merge
log: Day 15 — Module 04 interactive rebase practice
log: Day 30 — Final review and 30-day reflection
```

---

### Step 6 — Push to your fork

```bash
git push origin main
```

Visit your GitHub profile → look at the contribution graph → there's your green square.

---

### Step 7 — Come back tomorrow

Repeat Steps 2–6. That's the whole system. Consistency is the skill.

---

## 📅 The 30-Day System

Here's a suggested 30-day pacing guide. Adjust based on your speed — some modules may take multiple days:

| Days | Focus | Module |
|---|---|---|
| Day 1 | Setup & configuration, VCS concepts | [00-Introduction](../00-Introduction/README.md) |
| Day 2–3 | First repo, staging, committing, log | [01-Foundations](../01-Foundations/README.md) |
| Day 4–6 | Branches, merging, stashing | [02-Intermediate-Workflows](../02-Intermediate-Workflows/README.md) |
| Day 7–10 | Remotes, GitHub, push/pull, PRs | [03-Remote-Collaboration](../03-Remote-Collaboration/README.md) |
| Day 11–16 | Rebase, cherry-pick, reflog, reset | [04-Advanced-Git](../04-Advanced-Git/README.md) |
| Day 17–20 | GitHub Actions, Pages, Wikis | [05-GitHub-Expertise](../05-GitHub-Expertise/README.md) |
| Day 21–25 | Re-do all labs **from memory** (no peeking) | All modules |
| Day 26–28 | Build a real project using the full workflow | Self-directed |
| Day 29 | Teach someone else one concept (or write a blog post draft) | Any |
| Day 30 | Final reflection — fill in the 30-day summary block | PRACTICE_TEMPLATE |

> [!NOTE]
> There's no rule that says one day = one log. If you spend three days on Module 04, make three logs. The point is daily engagement, not rushing through modules.

---

## 📝 Daily Log Structure

Here's what each section looks like when filled in well:

```markdown
## Day 7 — 2026-04-21

### 📚 Module Studied
Module 02 — Intermediate Workflows: Branching, Merging & Stashing

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| `git switch -c feature/test` | Created a feature branch | Modern syntax — cleaner than checkout |
| `git merge feature/test` | Fast-forward merge | No merge commit when history is linear |
| `git stash` | Saved WIP mid-task | Disappeared from working dir — felt like magic |
| `git stash pop` | Restored the WIP | Came back exactly as I left it |

### 🔬 Lab Completed
- [x] Lab: "Feature Branch Workflow"
- Outcome: Created a branch, made commits, merged back, then triggered a 3-way merge intentionally.

### 💡 Key Takeaways
- Branches are just pointers — they're cheap. Create them freely.
- Fast-forward = straight line. 3-way = two lines meeting.
- Stash is a stack, not a single slot — you can have multiple stashes.

### ❓ Questions / Blockers
- When exactly should I prefer squash merge over regular merge?

### ⭐ Confidence Rating (1-5)
- [x] 4 — Can explain to others
```

---

## 🗂️ Folder Naming Convention

Keep your log files consistently named so they sort properly:

```
Practice-Lab/
├── .gitkeep                              ← Always present — keeps folder tracked
├── 2026-04-15_Day-01_log.md             ← Zero-pad day number for clean sorting
├── 2026-04-16_Day-02_log.md
├── 2026-04-17_Day-03_log.md
├── ...
├── 2026-05-13_Day-29_log.md
└── 2026-05-14_Day-30_log.md             ← 🏆 Final log
```

> [!TIP]
> Zero-pad your day numbers (`Day-01` not `Day-1`) so that `ls` and file explorers sort them correctly. `Day-10` sorts before `Day-9` alphabetically without zero-padding.

---

## 💡 Progress Tips & Strategies

### For Retention
- **Teach it back.** After each module, explain the main concept out loud to yourself (or to a rubber duck). If you can't explain it simply, you haven't understood it yet.
- **Redo labs from memory.** Open a new terminal, a blank directory, and do the lab again without looking at the steps. What you can recreate, you actually know.
- **Look at your logs.** Before starting a new day, re-read your previous log. What felt shaky? Go back and re-practice that command.

### For Consistency
- **Same time every day.** Even 20 minutes at the same time beats 2-hour sessions whenever you feel like it.
- **Don't break the chain.** Put a ✅ on a physical calendar for every day you commit. The chain becomes the motivation.
- **Short days count.** If you only have 10 minutes, open a terminal, run 5 commands from the cheat sheet, fill in a quick log, commit. It still counts. Consistency over intensity.

### For Depth
- **Use the `[Complete Cheat Sheet](../CHEATSHEET.md)`** during practice — look up commands you're unsure of before you guess.
- **Read the `git --help` output** for any command that confuses you: `git reset --help`, `git rebase --help`.
- **Make real mistakes intentionally.** Run `git reset --hard`, then recover with `git reflog`. The muscle memory of recovery is as important as the muscle memory of the commands.

---

## 🆘 What to Do When You're Stuck

**If a command gives an unexpected error:**
```bash
# Read the full error message — Git error messages are actually very good
# Then check the cheat sheet for the correct syntax
cat ../CHEATSHEET.md | grep "git reset"   # or just open CHEATSHEET.md
```

**If you accidentally deleted something:**
```bash
git reflog              # Find the SHA of what you lost
git reset --hard <SHA>  # Restore it
# See Module 04 for the full recovery workflow
```

**If your branch is a mess:**
```bash
git log --oneline --graph   # Visualize what happened
git status                   # See what's staged/unstaged
# Take a breath — almost nothing in Git is permanently irreversible
```

**If you're confused about a concept:**
1. Re-read the relevant module README
2. Draw the diagram on paper — visual understanding comes from re-drawing, not just reading
3. Open an Issue in the upstream repo — your question might help others

> [!WARNING]
> Never use `git reset --hard` or `git push --force` when you're confused and hoping it "fixes" something. First understand what state you're in with `git log --oneline` and `git status`. Then act deliberately.

---

## 🌐 Sharing Your Progress

You're not alone in this. The Git-Mastery-Hub community is built from practitioners just like you.

### Share a check-in on GitHub Issues

1. Go to the upstream **Git-Mastery-Hub** repository on GitHub
2. Click **Issues** → **New Issue**
3. Use a title like: `[30-Day Log] Day 15 check-in — @yourhandle`
4. Share:
   - What module you're on
   - One thing that finally clicked
   - One thing you're still unsure about
   - Your confidence rating trend

### What makes a great check-in post

```markdown
## 30-Day Check-in: Day 15 — @yourhandle

**Module progress:** Through Module 03, starting Module 04 tomorrow

**The thing that finally clicked:**
`git fetch` vs `git pull` — fetch downloads without changing anything local.
I'd been using pull everywhere and had no idea why merge commits kept appearing.

**Still fuzzy on:**
When exactly does rebase make sense vs. merge? The "don't rebase public branches"
rule makes sense but I don't fully understand *why* yet.

**Confidence trend:** 2 → 2 → 3 → 3 → 3 → 4 → 4 (slowly going up!)
```

The community learns together. Your confusion today is someone else's breakthrough tomorrow.

---

## 📖 Quick Reference

| What you need | Where to find it |
|---|---|
| All 77 Git commands | [CHEATSHEET.md](../CHEATSHEET.md) |
| Module 00 — Setup & Config | [00-Introduction/README.md](../00-Introduction/README.md) |
| Module 01 — Init, Add, Commit | [01-Foundations/README.md](../01-Foundations/README.md) |
| Module 02 — Branches & Merge | [02-Intermediate-Workflows/README.md](../02-Intermediate-Workflows/README.md) |
| Module 03 — Remotes & PRs | [03-Remote-Collaboration/README.md](../03-Remote-Collaboration/README.md) |
| Module 04 — Rebase & Reflog | [04-Advanced-Git/README.md](../04-Advanced-Git/README.md) |
| Module 05 — GitHub Features | [05-GitHub-Expertise/README.md](../05-GitHub-Expertise/README.md) |
| Daily log template | [PRACTICE_TEMPLATE.md](../PRACTICE_TEMPLATE.md) |
| Course landing page | [README.md](../README.md) |
| License | [LICENSE](../LICENSE) |

---

<div align="center">

*You forked the repo. Now commit every day.*  
*30 days from now, you'll have the commit history — and the skills — to prove it.*

**[📋 Get the Practice Template →](../PRACTICE_TEMPLATE.md)**

</div>
