<div align="center">

<h1>Module 05 — Interview Questions</h1>
<h3>Tags, .gitignore, Bisect, Blame, GitHub Actions, Pages & Projects</h3>

[![Module](https://img.shields.io/badge/Module-05%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Advanced-red.svg)](#)
[![Questions](https://img.shields.io/badge/Questions-30-orange.svg)](#)

**[← Module 04 Interview Questions](../04-Advanced-Git/INTERVIEW_QUESTIONS.md) · [Module 05 Content](README.md) · [Course Home](../README.md)**

</div>

---

Module 05 questions appear in senior developer, DevOps, and platform engineering interviews. GitHub Actions and CI/CD questions are increasingly common even for mid-level roles.

---

## 📋 Table of Contents

- [Git Tags & Versioning](#-git-tags--versioning)
- [.gitignore](#-gitignore)
- [Git Bisect & Blame](#-git-bisect--blame)
- [GitHub Actions & CI/CD](#-github-actions--cicd)
- [GitHub Features](#-github-features)
- [Quick-Fire Round](#-quick-fire-round)

---

## 🏷️ Git Tags & Versioning

**Q1. What is a Git tag?**

> A tag is a permanent label attached to a specific commit. Unlike branch names, tags do not move when new commits are made. Tags are used to mark release versions (e.g., `v1.0.0`, `v2.3.1`). There are two types: **lightweight** (just a pointer to a commit) and **annotated** (a full Git object with author, date, message, and optional signature).

---

**Q2. What is the difference between a lightweight tag and an annotated tag?**

> | | Lightweight Tag | Annotated Tag |
> |---|---|---|
> | Storage | Simple pointer to commit | Full Git object |
> | Metadata | None | Author, date, message |
> | Signable? | No | Yes (GPG) |
> | Recommended for? | Temporary/local labels | Official releases |
>
> ```bash
> git tag v1.0.0                              # lightweight
> git tag -a v1.0.0 -m "Release version 1"   # annotated
> ```

---

**Q3. What is Semantic Versioning (SemVer)?**

> A widely-used versioning convention: `MAJOR.MINOR.PATCH`
> - **MAJOR** — breaking changes (incompatible with previous version)
> - **MINOR** — new features (backwards-compatible)
> - **PATCH** — bug fixes (backwards-compatible)
>
> Example: `v2.3.1` = major version 2, feature revision 3, patch 1

---

**Q4. How do you push tags to GitHub? Do they push automatically?**

> Tags do **not** push automatically with `git push`. You must push them explicitly:
> ```bash
> git push origin v1.0.0      # push a specific tag
> git push origin --tags      # push all tags at once
> ```

---

**Q5. How do you list, view, and delete a tag?**

> ```bash
> git tag                      # list all tags
> git show v1.0.0              # view tag details + tagged commit
> git tag -d v1.0.0            # delete locally
> git push origin --delete v1.0.0  # delete from remote
> ```

---

## 🚫 .gitignore

**Q6. What is `.gitignore`?**

> `.gitignore` is a file where you list patterns for files and directories that Git should not track. Files matching the patterns will be excluded from `git add` and will not appear in `git status` as untracked.

---

**Q7. What are the common `.gitignore` pattern types?**

> ```
> *.log           # all .log files in any directory
> build/          # entire build directory
> !important.log  # exception — track this file even though *.log is ignored
> **/temp         # any folder named "temp" at any depth
> doc/*.txt       # .txt files directly in doc/ (not subdirectories)
> doc/**/*.txt    # .txt files in doc/ and all subdirectories
> ```

---

**Q8. You committed a file that should have been ignored. Adding it to `.gitignore` doesn't seem to work. Why?**

> Once a file is tracked by Git (has been committed before), `.gitignore` no longer affects it — it's already in the history. To stop tracking it:
> ```bash
> git rm --cached secrets.env
> echo "secrets.env" >> .gitignore
> git commit -m "chore: stop tracking secrets.env"
> ```
> The file stays on disk but Git will ignore future changes to it.

---

**Q9. What is the difference between a project `.gitignore` and a global `.gitignore`?**

> - **Project `.gitignore`** lives in the repository root, applies to everyone who clones the repo, and should be committed.
> - **Global `.gitignore`** lives at `~/.gitignore_global` (set via `git config --global core.excludesfile`) and applies to all repositories on your machine. Use it for editor-specific files (`.vscode/`, `.idea/`, `.DS_Store`) that are your machine's concern, not the project's.

---

**Q10. How do you see which `.gitignore` rule is causing a file to be ignored?**

> ```bash
> git check-ignore -v filename.log
> # .gitignore:3:*.log    filename.log
> ```
> This shows the exact file, line number, and pattern responsible.

---

## 🔍 Git Bisect & Blame

**Q11. What is `git bisect`?**

> `git bisect` is a binary search tool that helps you find which commit introduced a bug. You tell it a known "good" commit and a known "bad" commit, and Git checks out commits in the middle of the range for you to test. Each test you mark as "good" or "bad" and Git narrows down the range until it identifies the exact commit that broke things.

---

**Q12. How do you use `git bisect` step by step?**

> ```bash
> git bisect start
> git bisect bad                  # current commit is broken
> git bisect good v1.0.0          # this version worked
> # Git checks out the midpoint commit — test your code
> git bisect good                 # if it works
> git bisect bad                  # if it's broken
> # Repeat until Git identifies the exact commit
> git bisect reset                # return to original HEAD when done
> ```

---

**Q13. What is `git blame`?**

> `git blame filename` shows every line of a file annotated with the commit SHA, author, and date of the last modification to that line. Useful for understanding why a line exists, who to ask about it, or what commit introduced it.

---

**Q14. How do you find who wrote a specific function using `git blame`?**

> ```bash
> git blame -L 50,75 src/auth.js   # show blame for lines 50–75 only
> ```
> Each line shows: short SHA | author | date | line number | code

---

**Q15. Is `git blame` used to blame people? What is its actual purpose?**

> The name is unfortunate — `git blame` is a **code archaeology tool**, not an accusation tool. Its purpose is to understand context: why was this line written this way, when was it changed, and which commit introduced it so you can read the full commit message for reasoning.

---

## ⚙️ GitHub Actions & CI/CD

**Q16. What is GitHub Actions?**

> GitHub Actions is GitHub's built-in CI/CD (Continuous Integration / Continuous Deployment) platform. You write **workflows** in YAML files stored in `.github/workflows/`. Workflows are triggered by events (push, pull request, schedule) and run jobs in containers on GitHub's servers (or your own runners).

---

**Q17. What are the key components of a GitHub Actions workflow?**

> - **Workflow** — the whole YAML file (`.github/workflows/ci.yml`)
> - **Event (trigger)** — what starts the workflow (`on: push`, `on: pull_request`)
> - **Job** — a group of steps running on one runner (e.g., `build`, `test`, `deploy`)
> - **Step** — an individual task within a job (`run: npm test` or `uses: actions/checkout@v4`)
> - **Runner** — the machine where the job runs (e.g., `ubuntu-latest`)
> - **Action** — a reusable unit of work from the Marketplace (e.g., `actions/checkout`)

---

**Q18. Write a minimal GitHub Actions workflow that runs tests on every push.**

> ```yaml
> name: Run Tests
>
> on: [push, pull_request]
>
> jobs:
>   test:
>     runs-on: ubuntu-latest
>     steps:
>       - uses: actions/checkout@v4
>       - uses: actions/setup-node@v4
>         with:
>           node-version: '20'
>       - run: npm install
>       - run: npm test
> ```

---

**Q19. What is the difference between CI and CD?**

> - **CI (Continuous Integration)** — automatically build and test code every time a change is pushed. Catches bugs early before they reach production.
> - **CD (Continuous Delivery/Deployment)** — automatically deploy the tested code to a staging or production environment. Delivery = deploy to staging (manual approval to prod). Deployment = fully automated to production.

---

**Q20. What is a GitHub Actions secret? Why is it used?**

> A secret is an encrypted environment variable stored in GitHub repository settings. You reference it in workflows as `${{ secrets.MY_SECRET }}`. Used to store sensitive values like API keys, deployment tokens, and passwords so they are never hardcoded in your YAML files or exposed in logs.

---

## 🌐 GitHub Features

**Q21. What is GitHub Pages?**

> GitHub Pages is a free static site hosting service. It serves HTML, CSS, and JavaScript files directly from a GitHub repository. Common uses: project documentation, personal portfolios, open-source project websites. Deployment is triggered by pushing to a specific branch or from a `docs/` folder.

---

**Q22. What is the difference between GitHub Issues and GitHub Projects?**

> - **Issues** — individual work items: bug reports, feature requests, tasks. Each has a title, description, labels, assignees, and comments.
> - **Projects** — a Kanban/table/roadmap board that organises Issues (and PRs) into columns or sprints. Projects give you a high-level view of what's planned, in progress, and done.

---

**Q23. How do you automatically close a GitHub Issue when a PR is merged?**

> Include a keyword in the PR description or commit message followed by the issue number:
> ```
> Fixes #42
> Closes #42
> Resolves #42
> ```
> When the PR is merged into the default branch, GitHub automatically closes the referenced issue.

---

**Q24. What is a GitHub Wiki?**

> A Wiki is a separate documentation space attached to a repository. Unlike the README (which is in the repo), the Wiki is its own Git repository (`repo.wiki.git`). Good for long-form docs, guides, and content that doesn't belong in the codebase itself.

---

**Q25. What is the difference between a GitHub Organization and a personal account?**

> - **Personal account** — belongs to one user. Repositories are owned by that user.
> - **Organization** — a shared account for a company or group. Multiple users can be members with different roles (owner, member). Repositories are owned by the org. Better for teams: centralised billing, team-level permissions, audit logs.

---

**Q26. What are GitHub branch protection rules?**

> Rules that prevent direct changes to important branches (usually `main`). Common protections:
> - Require PR before merging (no direct pushes to main)
> - Require at least N approvals before merge
> - Require CI checks to pass before merge
> - Require branches to be up to date before merge
> - Prevent force pushes and branch deletion

---

## ⚡ Quick-Fire Round

| Question | Answer |
|---|---|
| Lightweight vs annotated tag | Lightweight = pointer only; Annotated = full object with metadata |
| Do tags push automatically? | No — `git push origin --tags` |
| SemVer format | `MAJOR.MINOR.PATCH` |
| How to un-track a committed file | `git rm --cached filename` |
| Tool to find which commit broke something | `git bisect` |
| What `git blame` shows | Author + commit per line |
| Where GitHub Actions workflows live | `.github/workflows/` |
| What triggers a workflow | Events: `push`, `pull_request`, `schedule`, etc. |
| How to use secrets in workflows | `${{ secrets.SECRET_NAME }}` |
| Auto-close issue on PR merge | `Fixes #N` in PR description |
| Free static hosting from GitHub | GitHub Pages |
| Branch protection requires what to merge | PR + approvals + CI checks |

---

<div align="center">

**[← Module 04 Interview Questions](../04-Advanced-Git/INTERVIEW_QUESTIONS.md) · [Module 05 Content](README.md) · [Course Home](../README.md)**

*Completing all 6 modules and their interview question sets puts you ahead of the vast majority of developers in Git and GitHub knowledge.*

</div>
