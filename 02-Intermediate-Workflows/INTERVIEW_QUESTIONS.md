<div align="center">

<h1>Module 02 — Interview Questions</h1>
<h3>Branching, HEAD, Merging, Stashing & Conflict Resolution</h3>

[![Module](https://img.shields.io/badge/Module-02%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Intermediate-yellow.svg)](#)
[![Questions](https://img.shields.io/badge/Questions-30-orange.svg)](#)

**[← Module 01 Interview Questions](../01-Foundations/INTERVIEW_QUESTIONS.md) · [Module 02 Content](README.md) · [Next: Module 03 Interview Questions →](../03-Remote-Collaboration/INTERVIEW_QUESTIONS.md)**

</div>

---

These questions cover the concepts most likely to trip you up in interviews: branching strategy, HEAD, merge types, conflict resolution, and stashing. Mid-level and senior roles ask nearly all of these.

---

## 📋 Table of Contents

- [L1 — Conceptual Basics](#l1--conceptual-basics)
- [L2 — Applied Knowledge](#l2--applied-knowledge)
- [L3 — Scenario & Tricky](#l3--scenario--tricky)
- [Quick-Fire Round](#-quick-fire-round)

---

## L1 — Conceptual Basics

**Q1. What is a branch in Git?**

> A branch is a lightweight, movable pointer to a specific commit. When you create a branch and start committing, the branch pointer moves forward with each new commit. The default branch is usually called `main`. Branches let multiple lines of development happen simultaneously without affecting each other.

---

**Q2. What is HEAD in Git?**

> `HEAD` is a special pointer that indicates **where you currently are** in the repository — specifically, which branch or commit you are working on. It usually points to a branch name (e.g., `HEAD → main`), which in turn points to the latest commit on that branch.

---

**Q3. What is "detached HEAD" state?**

> Detached HEAD occurs when HEAD points directly to a **commit SHA** instead of a branch name. This happens when you checkout a specific commit, tag, or remote branch directly. In this state, new commits you make are not attached to any branch — they can be lost when you switch back. You can recover by creating a new branch: `git switch -c new-branch-name`.

---

**Q4. What is the difference between `git switch` and `git checkout` for changing branches?**

> Both change your current branch, but:
> - `git switch` (introduced in Git 2.23, 2019) is the **modern, purpose-built** command for switching branches
> - `git checkout` is the **older, multipurpose** command that can also checkout files, restore working directory states, and detach HEAD
>
> Prefer `git switch` for branch operations — it's clearer and safer because it won't accidentally overwrite your working directory files.

---

**Q5. What is a fast-forward merge?**

> A fast-forward merge happens when the target branch (e.g., `main`) has not diverged from the feature branch — meaning all commits on `main` are direct ancestors of the feature branch. Git simply moves the `main` pointer forward to the tip of the feature branch. No merge commit is created. The history stays linear.

---

**Q6. What is a 3-way merge?**

> A 3-way merge happens when both branches have diverged — each has commits the other doesn't have. Git uses three points: the **common ancestor** commit, the tip of **branch A**, and the tip of **branch B**. It combines changes from both sides. A new **merge commit** is created with two parents.

---

**Q7. What is a merge conflict?**

> A merge conflict occurs when two branches have changed the **same lines** of the same file differently, and Git cannot automatically decide which version to keep. Git pauses the merge, marks the conflicting sections in the file with `<<<<<<<`, `=======`, and `>>>>>>>` markers, and waits for you to resolve them manually.

---

**Q8. What is `git stash`?**

> `git stash` temporarily saves your uncommitted changes (both staged and unstaged) and reverts your working directory to the last clean commit. It's useful when you need to switch branches quickly without committing half-finished work.

---

## L2 — Applied Knowledge

**Q9. How do you create and switch to a new branch in one command?**

> ```bash
> git switch -c feature/login-page
> # or old syntax:
> git checkout -b feature/login-page
> ```

---

**Q10. How do you merge a branch named `feature/login` into `main`?**

> ```bash
> git switch main          # first switch to the target branch
> git merge feature/login  # merge the feature branch into it
> ```

---

**Q11. How do you resolve a merge conflict step by step?**

> 1. Open the conflicting file — look for `<<<<<<<` markers
> 2. Edit the file to keep the correct content, removing all conflict markers
> 3. Stage the resolved file: `git add filename.js`
> 4. Complete the merge: `git commit` (Git pre-fills a merge commit message)
>
> To abort a merge in progress: `git merge --abort`

---

**Q12. What does `git merge --squash` do?**

> It combines all commits from the feature branch into a **single staged changeset** without creating a merge commit. You then commit manually. The result is one clean commit on the target branch instead of the full feature branch history. Useful for keeping `main` history tidy.

---

**Q13. How do you delete a branch locally?**

> ```bash
> git branch -d feature/login   # safe — refuses if branch isn't merged
> git branch -D feature/login   # force delete — even if not merged
> ```

---

**Q14. How do you see all branches (local and remote)?**

> ```bash
> git branch         # local only
> git branch -r      # remote only
> git branch -a      # all (local + remote)
> ```

---

**Q15. How does `git stash pop` differ from `git stash apply`?**

> Both restore your stashed changes. The difference:
> - `git stash pop` — restores the stash **and removes it** from the stash stack
> - `git stash apply` — restores the stash **but keeps it** in the stash stack (useful if you want to apply the same stash to multiple branches)

---

**Q16. How do you list all stashes? How do you drop a specific one?**

> ```bash
> git stash list              # shows all stashes: stash@{0}, stash@{1}, etc.
> git stash drop stash@{1}    # removes a specific stash
> git stash clear             # removes all stashes
> ```

---

**Q17. What is `git stash push -m "message"` useful for?**

> It stashes with a descriptive label, making it easier to identify later when you have multiple stashes. Without a message, stashes get default names like `WIP on main: a3f5c9d fix login` which can be hard to distinguish.

---

## L3 — Scenario & Tricky

**Q18. What is the difference between `git merge` and `git rebase`? (Overview — deep dive in Module 04)**

> Both integrate changes from one branch into another, but differently:
> - `git merge` creates a **merge commit** and preserves the full branch history (non-destructive)
> - `git rebase` **replays** commits from one branch onto another, creating a linear history (rewrites history)
>
> Rule of thumb: merge for shared/public branches, rebase for local/private branches before merging.

---

**Q19. You are on `feature/login` and run `git merge main`. What happens?**

> Git merges `main` **into your current branch** (`feature/login`) — bringing your feature branch up to date with the latest `main`. This is the reverse of merging your feature into `main`. Useful when `main` has new commits and you want to incorporate them into your feature branch.

---

**Q20. You accidentally deleted a branch. How can you recover it?**

> If you know the last commit SHA (visible in `git reflog`):
> ```bash
> git reflog                          # find the SHA of the deleted branch's tip
> git switch -c recovered-branch SHA  # recreate the branch at that commit
> ```
> `git reflog` records every movement of HEAD — even deleted branches remain in reflog for ~90 days.

---

**Q21. When should you NOT use a fast-forward merge?**

> When you want to **preserve the history** that a feature branch existed. A fast-forward merge erases the record that work happened on a separate branch. Use `git merge --no-ff` to force a merge commit even when fast-forward is possible — this is a common team policy.

---

**Q22. What happens if you run `git stash` and then switch branches?**

> The stash is stored independently of any branch. When you `git stash pop` on a different branch, your stashed changes are applied to that branch instead. This is actually a useful workflow: stash on one branch, switch to another, apply the stash there.

---

**Q23. You have a detached HEAD. You made 3 commits. Now you switch back to `main`. Are those commits lost?**

> They are **not immediately lost** — the commits still exist in Git's object database. But since no branch points to them, they become unreachable and will eventually be garbage collected. To save them:
> ```bash
> git switch -c save-my-work   # create a branch before switching away
> ```
> Or if you already switched away, use `git reflog` to find the commit SHA and create a branch from it.

---

**Q24. What is the conflict marker format in a conflicted file?**

> ```
> <<<<<<< HEAD
> const greeting = "Hello";      ← your current branch's version
> =======
> const greeting = "Hi there";   ← the incoming branch's version
> >>>>>>> feature/greeting
> ```
> You must delete the markers and keep the correct content. After editing, `git add` the file.

---

**Q25. Your team uses `git merge --no-ff`. Why might they do this?**

> `--no-ff` (no fast-forward) forces a merge commit even when the branch could be fast-forwarded. This preserves the evidence in history that a group of commits belonged to a feature branch. Looking at `git log --graph` later, you can clearly see where features began and ended.

---

## ⚡ Quick-Fire Round

| Question | Answer |
|---|---|
| Command to create + switch to a branch | `git switch -c branch-name` |
| Command to merge a branch into current | `git merge branch-name` |
| Command to delete a local branch safely | `git branch -d branch-name` |
| What creates a merge commit? | 3-way merge (and `--no-ff`) |
| What does fast-forward mean? | Pointer moves forward, no merge commit |
| What is HEAD? | Pointer to your current position |
| How to recover from detached HEAD | `git switch -c new-branch` |
| Command to temporarily save work | `git stash` |
| Command to restore and remove stash | `git stash pop` |
| Command to restore and keep stash | `git stash apply` |
| How to abort an in-progress merge | `git merge --abort` |
| Modern command to switch branches | `git switch` |

---

<div align="center">

**[← Module 01 Interview Questions](../01-Foundations/INTERVIEW_QUESTIONS.md) · [Module 02 Content](README.md) · [Next: Module 03 Interview Questions →](../03-Remote-Collaboration/INTERVIEW_QUESTIONS.md)**

*Conflict resolution and branching strategy questions are extremely common. Practise resolving conflicts in a real repo.*

</div>
