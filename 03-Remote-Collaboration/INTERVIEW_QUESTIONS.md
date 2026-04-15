<div align="center">

<h1>Module 03 — Interview Questions</h1>
<h3>Remotes, Push, Pull, Fetch, Authentication & Pull Requests</h3>

[![Module](https://img.shields.io/badge/Module-03%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Intermediate-yellow.svg)](#)
[![Questions](https://img.shields.io/badge/Questions-32-orange.svg)](#)

**[← Module 02 Interview Questions](../02-Intermediate-Workflows/INTERVIEW_QUESTIONS.md) · [Module 03 Content](README.md) · [Next: Module 04 Interview Questions →](../04-Advanced-Git/INTERVIEW_QUESTIONS.md)**

</div>

---

Remote collaboration questions are asked in **almost every developer interview**. Knowing git push, pull, fetch, and PR workflows is a baseline expectation for any role that uses Git on a team.

---

## 📋 Table of Contents

- [L1 — Conceptual Basics](#l1--conceptual-basics)
- [L2 — Applied Knowledge](#l2--applied-knowledge)
- [L3 — Scenario & Tricky](#l3--scenario--tricky)
- [Pull Request Questions](#-pull-request-questions)
- [Quick-Fire Round](#-quick-fire-round)

---

## L1 — Conceptual Basics

**Q1. What is a remote in Git?**

> A remote is a reference to another copy of the repository — usually hosted on GitHub, GitLab, or Bitbucket. It has a name (most commonly `origin`) and a URL. Remotes are how your local repository knows where to push to and pull from.

---

**Q2. What is `origin`?**

> `origin` is the default name Git gives to the remote when you clone a repository. It's just a name — you could rename it to anything. When you run `git push origin main`, you're pushing to the remote named `origin`, to its `main` branch.

---

**Q3. What is the difference between `git fetch` and `git pull`?**

> - `git fetch` downloads changes from the remote but **does not merge** them into your working branch. It updates `origin/main` but your local `main` is untouched.
> - `git pull` = `git fetch` + `git merge`. It downloads **and** immediately merges the remote changes into your current branch.
>
> `git fetch` is safer — you can inspect what changed before merging. `git pull` is faster for simple updates.

---

**Q4. What does `git push` do step by step?**

> 1. Git checks that you have a remote configured (`origin`)
> 2. It verifies you are authenticated (HTTPS token or SSH key)
> 3. It checks that your local branch's history includes all commits the remote has (no divergence)
> 4. It sends your new commits (as compressed objects) to the remote server
> 5. The remote updates its branch pointer to your latest commit

---

**Q5. What is the difference between HTTPS and SSH authentication in Git?**

> | | HTTPS | SSH |
> |---|---|---|
> | Authentication | Username + Personal Access Token | SSH key pair (public + private) |
> | Setup | Simple — works out of the box | Requires key generation and adding public key to GitHub |
> | Credential storage | Token stored in credential helper | Key stored in `~/.ssh/` |
> | Best for | Quick setup, short-term use | Daily use, automation, no password prompts |

---

**Q6. What is a tracking branch?**

> A tracking branch is a local branch that is linked to a remote branch. When a local branch tracks a remote branch, Git knows where to push and pull by default. Created automatically when you clone or use `git push -u origin branch-name`. Check with `git branch -vv`.

---

## L2 — Applied Knowledge

**Q7. How do you add a remote to an existing local repository?**

> ```bash
> git remote add origin https://github.com/username/repo.git
> ```
> Then push for the first time:
> ```bash
> git push -u origin main
> ```
> The `-u` flag sets `origin/main` as the upstream (tracking) branch.

---

**Q8. What does `git push -u origin main` do differently from `git push origin main`?**

> The `-u` (or `--set-upstream`) flag creates a tracking relationship between your local `main` and `origin/main`. After doing this once, you can just run `git push` (without arguments) and Git knows where to push. Without `-u`, you must always specify `git push origin main`.

---

**Q9. How do you set up SSH authentication with GitHub?**

> ```bash
> # 1. Generate an SSH key pair
> ssh-keygen -t ed25519 -C "you@example.com"
>
> # 2. Copy the public key
> cat ~/.ssh/id_ed25519.pub
>
> # 3. Add the public key to GitHub
> # GitHub → Settings → SSH and GPG Keys → New SSH Key → Paste it
>
> # 4. Test the connection
> ssh -T git@github.com
> # Hi username! You've successfully authenticated.
> ```

---

**Q10. How do you view all configured remotes and their URLs?**

> ```bash
> git remote -v
> # origin  https://github.com/username/repo.git (fetch)
> # origin  https://github.com/username/repo.git (push)
> ```

---

**Q11. How do you change a remote URL (e.g., from HTTPS to SSH)?**

> ```bash
> git remote set-url origin git@github.com:username/repo.git
> ```

---

**Q12. What is `git pull --rebase` and why would you use it?**

> Instead of creating a merge commit when pulling, `--rebase` replays your local commits on top of the fetched remote commits. This keeps the history linear and avoids "Merge branch 'main' of..." noise commits. Many teams require `git pull --rebase` as a standard practice.

---

**Q13. How do you fetch changes from the remote without merging?**

> ```bash
> git fetch origin
> git log origin/main --oneline    # review what changed
> git merge origin/main            # merge when you're ready
> ```

---

**Q14. What is `upstream` in the context of a forked repository?**

> When you fork a repository, your fork on GitHub is `origin`. The original repository you forked from is conventionally named `upstream`. You add it with:
> ```bash
> git remote add upstream https://github.com/original-owner/repo.git
> ```
> Then sync updates from the original: `git fetch upstream` → `git merge upstream/main`

---

## L3 — Scenario & Tricky

**Q15. You run `git push` and get "rejected — non-fast-forward." What does this mean?**

> It means the remote has commits that your local branch does not have. Git refuses to push because it would overwrite those remote commits. The correct fix:
> ```bash
> git pull origin main    # fetch and merge the remote changes
> git push origin main    # now your local history includes all remote commits
> ```

---

**Q16. What is the difference between `--force` and `--force-with-lease`?**

> - `--force` overwrites the remote branch unconditionally. If a teammate pushed while you weren't looking, their commits are destroyed. **Dangerous.**
> - `--force-with-lease` checks that the remote branch is exactly where you last fetched it. If someone else pushed in between, the force push is rejected. **Safer.**
>
> Always prefer `--force-with-lease` over `--force` for history-rewriting operations like rebase.

---

**Q17. You cloned a repo two days ago. Since then, your colleague pushed 5 commits. What's the state of your local repo?**

> Your local `main` still points to the commit from two days ago. `origin/main` is stale — it won't automatically update. You need:
> ```bash
> git fetch origin    # updates origin/main to show the 5 new commits
> git merge origin/main  # or git pull origin main
> ```

---

**Q18. What is the difference between a fork and a clone?**

> - **Clone** copies a repository to your local machine. The remote is still the original repo.
> - **Fork** creates a copy of the repository under **your GitHub account** (server-side). You then clone your fork. Changes you push go to your fork, not the original. To contribute back, you open a Pull Request from your fork to the original.

---

**Q19. Can you push directly to someone else's GitHub repository?**

> Only if they have added you as a **collaborator** (repository Settings → Collaborators). Otherwise, you must fork their repo, push to your fork, and open a Pull Request — the repo owner then decides whether to merge it.

---

**Q20. What happens to `origin/main` when you run `git fetch`?**

> `git fetch` downloads the latest commits from the remote and updates the **remote tracking reference** `origin/main` to point to the latest commit on the remote. Your local `main` is not touched. `origin/main` is essentially a read-only snapshot of what the remote looks like.

---

**Q21. How do you push a branch that doesn't exist on the remote yet?**

> ```bash
> git push -u origin feature/new-feature
> ```
> GitHub creates the branch on the remote automatically. The `-u` sets up tracking.

---

**Q22. How do you delete a remote branch?**

> ```bash
> git push origin --delete feature/old-branch
> ```

---

## 🔀 Pull Request Questions

**Q23. What is a Pull Request (PR)?**

> A Pull Request is a GitHub feature (not a Git feature) that lets you propose merging one branch into another. It provides a UI for code review: teammates can comment on specific lines, request changes, and approve before the code is merged. It's the standard collaboration model for open-source and team development.

---

**Q24. What is a "draft Pull Request"?**

> A draft PR signals that the work is in progress and not ready for review. It can't be merged until you mark it as "Ready for review." Useful for getting early feedback or sharing work in progress without accidentally getting it merged.

---

**Q25. What is the difference between "Merge commit", "Squash and merge", and "Rebase and merge" on GitHub?**

> | Option | Result |
> |---|---|
> | **Merge commit** | Creates a merge commit — preserves all feature branch commits |
> | **Squash and merge** | Combines all PR commits into one commit on the target branch |
> | **Rebase and merge** | Replays each PR commit on top of the target branch — no merge commit, linear history |

---

**Q26. What does it mean when a PR has "merge conflicts"?**

> The branch being merged has changes that conflict with the target branch. The PR cannot be auto-merged by GitHub. You must resolve the conflicts locally:
> ```bash
> git fetch origin
> git merge origin/main    # or rebase
> # resolve conflicts
> git push origin feature/branch
> ```
> The PR updates automatically and the conflict is cleared.

---

**Q27. How do you keep your PR branch up to date with main while the PR is open?**

> ```bash
> git fetch origin
> git merge origin/main    # or: git rebase origin/main for linear history
> git push origin feature/branch
> ```
> This is called "updating the branch" — GitHub shows a button for it too.

---

## ⚡ Quick-Fire Round

| Question | Answer |
|---|---|
| Default remote name | `origin` |
| Command to see remotes | `git remote -v` |
| `git pull` = | `git fetch` + `git merge` |
| Safer alternative to `--force` | `--force-with-lease` |
| How to set upstream on first push | `git push -u origin branch` |
| How to delete a remote branch | `git push origin --delete branch` |
| HTTPS auth uses | Username + Personal Access Token |
| SSH auth uses | SSH key pair |
| What `git fetch` does NOT do | Merge into your local branch |
| What is `origin/main`? | Remote tracking reference |
| Fork vs Clone | Fork = your copy on GitHub; Clone = local copy |
| Command to rename a remote | `git remote rename old new` |

---

<div align="center">

**[← Module 02 Interview Questions](../02-Intermediate-Workflows/INTERVIEW_QUESTIONS.md) · [Module 03 Content](README.md) · [Next: Module 04 Interview Questions →](../04-Advanced-Git/INTERVIEW_QUESTIONS.md)**

*Remote workflow questions are asked in almost every developer interview. Know `fetch` vs `pull` and `--force-with-lease` cold.*

</div>
