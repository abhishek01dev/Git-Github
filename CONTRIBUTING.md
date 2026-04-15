<div align="center">

<h1>🤝 Contributing to GIT&GITHUB</h1>

<p><em>Thank you for taking the time to contribute! Every correction, improvement, and new lab exercise makes this resource better for thousands of learners.</em></p>

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/abhishek01dev/Git-Github/pulls)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

</div>

---

## 📋 Table of Contents

- [Code of Conduct](#-code-of-conduct)
- [Ways to Contribute](#-ways-to-contribute)
- [Before You Start](#-before-you-start)
- [Development Setup](#-development-setup)
- [Contribution Workflow](#-contribution-workflow)
- [Style Guide](#-style-guide)
- [Commit Message Convention](#-commit-message-convention)
- [Pull Request Checklist](#-pull-request-checklist)
- [What Happens After You Open a PR](#-what-happens-after-you-open-a-pr)

---

## 📜 Code of Conduct

This project is a learning community. Everyone — from first-time contributors to experienced engineers — deserves a respectful, welcoming environment.

**Expected behavior:**
- Use welcoming and inclusive language
- Be respectful of differing viewpoints and experience levels
- Accept constructive criticism gracefully
- Focus on what is best for the community

**Unacceptable behavior:**
- Harassment, insults, or personal attacks
- Publishing others' private information without permission
- Any behavior that would be considered inappropriate in a professional setting

Violations may result in removal from the project. Report issues by opening a private Issue or contacting a maintainer.

---

## 🌟 Ways to Contribute

All skill levels are welcome. Here are some great ways to get started:

| Contribution Type | Difficulty | Examples |
|---|:---:|---|
| 🐛 Fix a typo or grammar error | Beginner | Fix a misspelled word, awkward sentence |
| 🔗 Fix a broken link | Beginner | Update a dead URL or incorrect relative path |
| ✍️ Improve an explanation | Intermediate | Rewrite a confusing paragraph more clearly |
| 🔬 Add a lab step | Intermediate | Add an extra practice step to an existing lab |
| 📊 Add a Mermaid diagram | Intermediate | Visualize a concept that currently has no diagram |
| ⌨️ Add a missing command | Intermediate | Document a Git command not yet covered |
| 🆕 Add a new section | Advanced | Add a new sub-topic to an existing module |
| 🌍 Translate a module | Advanced | Translate a README into another language |

**Not sure what to work on?** Look for Issues labeled `good first issue` or `help wanted`.

---

## 🔍 Before You Start

1. **Check existing Issues** — someone may already be working on the same thing.
2. **For large changes**, open an Issue first to discuss the approach before writing content.
3. **For small fixes** (typos, broken links), just open a PR directly — no Issue needed.

---

## 🛠️ Development Setup

GIT&GITHUB is pure Markdown — no build step, no dependencies. All you need is:

```bash
# 1. Fork the repository (click Fork on GitHub)

# 2. Clone your fork
git clone https://github.com/abhishek01dev/Git-Github.git
cd Git-Github

# 3. Create a feature branch (NEVER commit directly to main)
git switch -c fix/typo-in-module-01
# or
git switch -c feat/add-git-bisect-section

# 4. Make your changes in any text editor

# 5. Preview Markdown
#    - VS Code: Ctrl+Shift+V (built-in preview)
#    - GitHub: push to your fork and preview in the browser
#    - Any Markdown previewer works
```

**Recommended editor:** [VS Code](https://code.visualstudio.com/) with the following extensions:
- `yzhang.markdown-all-in-one` — Markdown preview and shortcuts
- `bierner.markdown-mermaid` — Mermaid diagram preview
- `streetsidesoftware.code-spell-checker` — catch typos before committing

---

## 🔄 Contribution Workflow

```
Fork → Clone → Branch → Edit → Commit → Push → Pull Request → Review → Merge
```

```bash
# 1. Keep your fork up to date with upstream
git remote add upstream https://github.com/abhishek01dev/Git-Github.git
git fetch upstream
git merge upstream/main

# 2. Create a focused branch
git switch -c fix/correct-rebase-description

# 3. Make changes — keep them focused on one thing

# 4. Stage and commit with a conventional message
git add 04-Advanced-Git/README.md
git commit -m "fix: correct rebase diagram description in Module 04"

# 5. Push to your fork
git push -u origin fix/correct-rebase-description

# 6. Open a Pull Request on GitHub
#    - Base: main (upstream)
#    - Compare: your branch
#    - Fill in the PR template
```

---

## ✍️ Style Guide

Follow these rules precisely — they ensure the course reads consistently across all modules.

### Module README Structure (MANDATORY)

Every module README must have **exactly these 4 sections** in this order:

```
1. Theoretical Explanation   — concepts, definitions, mental models
2. Visual Diagram            — at least one Mermaid diagram
3. The "Cheat Code" Section  — command table (exact title required)
4. Hands-on Lab              — numbered terminal steps
```

> [!WARNING]
> The command section MUST be titled exactly: **The "Cheat Code" Section**
> Do NOT rename it to "Commands", "Reference", or anything else.

### Formatting Rules

| Element | Rule | Example |
|---|---|---|
| Commands | Always in backtick code spans | `git commit -m "message"` |
| File paths | Always in backtick code spans | `.gitignore`, `~/.gitconfig` |
| Key terms (first use) | **Bold** | **staging area**, **commit SHA** |
| Section headers | Sentence case with emoji prefix | `## 🎯 Learning Objectives` |
| Code blocks | Always specify language | ` ```bash ` or ` ```mermaid ` |
| Callouts | GitHub-flavored format only | `> [!NOTE]`, `> [!TIP]`, `> [!WARNING]` |
| Command tables | 2 columns: Command \| Description | See any module for reference |
| Cheat Sheet tables | 3 columns: Command \| Description \| Source | See CHEATSHEET.md |

### Callout Usage

| Type | When to Use |
|---|---|
| `> [!NOTE]` | Conceptual clarification, important context, mental model correction |
| `> [!TIP]` | Productivity shortcut, best practice, recommended approach |
| `> [!WARNING]` | Destructive command, irreversible action, common dangerous mistake |

### Prohibited Patterns

- ❌ Do NOT use `git checkout` for branch switching without mentioning `git switch` as the modern alternative
- ❌ Do NOT document `--force` without immediately recommending `--force-with-lease`
- ❌ Do NOT leave a module without all 4 required sections
- ❌ Do NOT title the command section anything other than **"The 'Cheat Code' Section"**
- ❌ Do NOT use HTML in content sections (the `<div align="center">` headers are the only exception)
- ❌ Do NOT add commands to a module README without also adding them to `CHEATSHEET.md`

---

## 💬 Commit Message Convention

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>: <short description>

Types:
  fix      — correct an error (typo, wrong command, broken link)
  feat     — add new content (new section, new command, new lab step)
  docs     — meta-documentation changes (CONTRIBUTING.md, README badges)
  style    — formatting only, no content change (spacing, table alignment)
  refactor — restructure without changing meaning
```

**Good examples:**
```bash
fix: correct git reset --hard description in Module 04
feat: add git bisect section to Module 04
fix: update broken link to GitHub Education in Module 05
style: align command tables in CHEATSHEET.md
feat: add Portuguese translation for Module 00
```

**Bad examples:**
```bash
update stuff
fixed things
changes to readme
```

---

## ✅ Pull Request Checklist

Before submitting, verify:

- [ ] My branch is based on the latest `main` (not an old commit)
- [ ] I made changes on a **feature branch**, not directly on `main`
- [ ] My changes follow the [Style Guide](#-style-guide)
- [ ] If I added a command, I also added it to `CHEATSHEET.md`
- [ ] All Mermaid diagrams I touched render correctly (test in VS Code or GitHub preview)
- [ ] No internal links are broken
- [ ] The module README still has exactly 4 sections
- [ ] My commit messages follow the [Conventional Commits](#-commit-message-convention) format
- [ ] I've tested any terminal commands I added or modified

---

## 🔍 What Happens After You Open a PR

1. A maintainer will review your PR within a few days.
2. You may receive feedback — don't be discouraged! Review is part of the process.
3. Address feedback by pushing additional commits to the same branch.
4. Once approved, a maintainer will merge your PR.
5. Your contribution will be credited in the repository's commit history.

Thank you for helping make GIT&GITHUB better for everyone. 🙏

---

<div align="center">

**[← Back to Course Home](README.md)**

</div>
