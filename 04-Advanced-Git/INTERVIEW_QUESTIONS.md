<div align="center">

<h1>Module 04 — Interview Questions</h1>
<h3>Rebase, Cherry-pick, Reflog, Reset, Restore & Clean</h3>

[![Module](https://img.shields.io/badge/Module-04%20of%2005-blue.svg)](../README.md)
[![Level](https://img.shields.io/badge/Level-Advanced-red.svg)](#)
[![Questions](https://img.shields.io/badge/Questions-32-orange.svg)](#)

**[← Module 03 Interview Questions](../03-Remote-Collaboration/INTERVIEW_QUESTIONS.md) · [Module 04 Content](README.md) · [Next: Module 05 Interview Questions →](../05-GitHub-Expertise/INTERVIEW_QUESTIONS.md)**

</div>

---

These are senior-level questions. If you can answer everything in this file confidently, you are well ahead of most developers in Git knowledge. The reset/rebase/reflog trio is a very common interview test.

---

## 📋 Table of Contents

- [L1 — Conceptual Basics](#l1--conceptual-basics)
- [L2 — Applied Knowledge](#l2--applied-knowledge)
- [L3 — Scenario & Tricky](#l3--scenario--tricky)
- [Quick-Fire Round](#-quick-fire-round)

---

## L1 — Conceptual Basics

**Q1. What is `git rebase`?**

> `git rebase` moves or "replays" commits from one branch onto another base commit. Instead of creating a merge commit, it rewrites the commit history so the feature branch appears to have branched from a more recent point. The result is a **clean, linear history** without merge commits.

---

**Q2. What is interactive rebase (`git rebase -i`)?**

> Interactive rebase opens an editor listing all the commits in the range you specified. For each commit you can choose an action:
> - `pick` — keep the commit as-is
> - `squash` / `fixup` — combine the commit with the one above
> - `reword` — change the commit message
> - `edit` — pause to amend the commit
> - `drop` — delete the commit entirely
>
> This is how teams clean up messy commit history before merging a PR.

---

**Q3. What is `git cherry-pick`?**

> `git cherry-pick <SHA>` applies the changes introduced by a specific commit onto the current branch — without merging the entire branch. It creates a new commit with the same changes but a different SHA. Useful for applying a critical fix from one branch to another.

---

**Q4. What is `git reflog`?**

> `git reflog` is a local log of every movement of `HEAD` — every checkout, commit, reset, rebase, merge, and stash. Unlike `git log`, it shows operations that changed HEAD's position, including operations that "deleted" commits. Data in reflog is kept for ~90 days. It's your ultimate safety net for recovering lost commits.

---

**Q5. What are the three modes of `git reset`?**

> | Mode | Staging Area | Working Directory | Use Case |
> |---|---|---|---|
> | `--soft` | Keeps staged changes | Unchanged | Undo commit, keep changes staged |
> | `--mixed` (default) | Unstages changes | Unchanged | Undo commit + unstage (still have changes) |
> | `--hard` | Clears staging area | **Discards all changes** | Completely undo commits and changes |

---

**Q6. What is the difference between `git reset` and `git revert`?**

> - `git reset` moves the branch pointer backwards, **rewriting history** — previous commits may be unreachable. Unsafe for shared branches.
> - `git revert` creates a **new commit** that undoes the changes of a specified commit, without altering history. Safe for shared/public branches.

---

**Q7. What is `git restore`?**

> `git restore` discards changes in the working directory or unstages files. It was split out of `git checkout` in Git 2.23 to reduce confusion:
> - `git restore filename` — discard unstaged changes in a file
> - `git restore --staged filename` — unstage a file (equivalent to `git reset HEAD filename`)

---

**Q8. What is `git clean`?**

> `git clean` removes **untracked files** (files Git has never tracked) from the working directory. Always run `-n` (dry run) first to preview what would be deleted before actually deleting.
> ```bash
> git clean -n    # preview what would be deleted
> git clean -f    # delete untracked files
> git clean -fd   # delete untracked files and directories
> git clean -fx   # delete untracked + ignored files
> ```

---

## L2 — Applied Knowledge

**Q9. How do you squash the last 3 commits into one using interactive rebase?**

> ```bash
> git rebase -i HEAD~3
> ```
> In the editor that opens, change `pick` to `squash` (or `s`) for commits 2 and 3. Keep the first as `pick`. Save and close. Git will prompt you for a combined commit message.

---

**Q10. How do you undo the last commit but keep the changes staged?**

> ```bash
> git reset --soft HEAD~1
> ```
> The commit is undone, but your changes stay staged (ready to commit again). Useful for fixing the commit message or adding a forgotten file.

---

**Q11. How do you undo the last commit and unstage the changes (but keep them in your working directory)?**

> ```bash
> git reset HEAD~1
> # (equivalent to: git reset --mixed HEAD~1)
> ```
> Changes are kept in your working directory but not staged. This is the default `git reset` mode.

---

**Q12. How do you completely discard the last 2 commits including all their changes?**

> ```bash
> git reset --hard HEAD~2
> ```
> WARNING: This is irreversible for unsaved changes. The commits and their file changes are gone from your working directory. You can recover via `git reflog` within 90 days.

---

**Q13. How do you cherry-pick a commit from another branch?**

> ```bash
> git switch main
> git log feature/hotfix --oneline    # find the SHA you want
> git cherry-pick a3f5c9d             # apply that commit to main
> ```

---

**Q14. How do you recover a commit after an accidental `git reset --hard`?**

> ```bash
> git reflog                       # find the SHA of the lost commit
> git switch -c recovery-branch SHA  # create a branch at that commit
> # or to restore main directly:
> git reset --hard SHA
> ```

---

**Q15. When should you use `git revert` instead of `git reset`?**

> Use `git revert` whenever the commit you want to undo has already been **pushed to a shared remote branch**. `git reset` rewrites history, which would require a force push and would break teammates' local repos. `git revert` is safe because it only adds a new commit.

---

**Q16. What does `git commit --amend` do? When is it safe to use?**

> `git commit --amend` replaces the **most recent commit** with a new one incorporating your current staged changes. You can also change the commit message.
>
> It is safe only if the commit **has not been pushed** to a shared branch yet. Amending a pushed commit creates a diverged history and forces a `--force` push.

---

**Q17. How do you rebase a feature branch onto an updated main?**

> ```bash
> git switch feature/login
> git rebase main
> ```
> This replays `feature/login`'s commits on top of the current `main`. If conflicts arise, Git pauses, you resolve them, then `git rebase --continue`.

---

## L3 — Scenario & Tricky

**Q18. What is the "golden rule" of rebasing?**

> **Never rebase a branch that others are working on.** Rebase rewrites commit SHAs. If you rebase a shared branch and push, everyone who has the old commits will have a diverged history. They will need to reset or re-clone. Only rebase your own **private, local** branches before merging.

---

**Q19. You ran `git reset --hard` and lost changes. Can you recover them?**

> Yes — within 90 days. `git reflog` records the SHA of HEAD before the reset. Find it and reset back:
> ```bash
> git reflog
> # HEAD@{2}: commit: feat: add payment module   ← this is what you want
> git reset --hard HEAD@{2}
> ```

---

**Q20. What is the difference between `git reset HEAD~1` and `git revert HEAD`?**

> - `git reset HEAD~1` moves the branch pointer back one commit — the commit disappears from history. Only safe locally.
> - `git revert HEAD` creates a new commit that reverses the changes introduced by HEAD. The original commit stays in history. Safe on shared branches.

---

**Q21. You are mid-rebase and there are conflicts. What are your options?**

> 1. **Resolve and continue**: fix the conflict, `git add` the resolved file, then `git rebase --continue`
> 2. **Skip this commit**: `git rebase --skip` — drops the conflicting commit
> 3. **Abort entirely**: `git rebase --abort` — returns to the state before rebase started

---

**Q22. What is the difference between `git restore filename` and `git checkout -- filename`?**

> They do the same thing: discard unstaged changes in a working directory file, restoring it to the last committed version. `git restore` (Git 2.23+) is the modern, purpose-built command. `git checkout -- filename` is the legacy syntax. Prefer `git restore` as it is explicit and less confusing.

---

**Q23. Can `git cherry-pick` cause conflicts?**

> Yes. If the commit being cherry-picked modifies lines that have been changed differently in the target branch, a conflict occurs. Resolve it the same way as a merge conflict: edit the file, `git add`, then `git cherry-pick --continue`. To abort: `git cherry-pick --abort`.

---

**Q24. What is `HEAD~1` vs `HEAD^1`? Are they the same?**

> For most cases, yes — both refer to the **first parent** of HEAD (one commit back). The difference appears with merge commits:
> - `HEAD~2` = two generations back (parent of parent)
> - `HEAD^2` = the **second parent** of a merge commit (the branch that was merged in)
>
> `~` traverses depth (generations back), `^` selects which parent at a fork.

---

**Q25. You want to combine commits 3 and 5 in your branch but NOT commit 4. Can interactive rebase do this?**

> Yes, but with care. In the interactive rebase editor you can reorder commits by changing their order in the list, then squash the ones you want combined. Reordering can cause conflicts if the commits have overlapping changes. This is an advanced use case.

---

## ⚡ Quick-Fire Round

| Question | Answer |
|---|---|
| Rebase vs Merge — key difference | Rebase = linear history; Merge = preserves branch history |
| Command to squash last 3 commits | `git rebase -i HEAD~3` |
| `git reset --soft` keeps | Staged changes |
| `git reset --hard` discards | Everything (staged + working directory) |
| Safe undo for pushed commits | `git revert` |
| Unsafe undo for pushed commits | `git reset` (requires force push) |
| Recovery tool for lost commits | `git reflog` |
| How long does reflog keep data? | ~90 days |
| `git clean -n` does | Dry run — shows what would be deleted |
| Apply one commit from another branch | `git cherry-pick SHA` |
| Abort an in-progress rebase | `git rebase --abort` |
| Modern command to discard file changes | `git restore filename` |

---

<div align="center">

**[← Module 03 Interview Questions](../03-Remote-Collaboration/INTERVIEW_QUESTIONS.md) · [Module 04 Content](README.md) · [Next: Module 05 Interview Questions →](../05-GitHub-Expertise/INTERVIEW_QUESTIONS.md)**

*If you can explain reset's three modes, the golden rule of rebase, and recover from `--hard` using reflog — you're at senior level.*

</div>
