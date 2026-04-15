# 🗓️ 30-Day Git Mastery Practice Log

**Name:** [Your Name]  
**Start Date:** [YYYY-MM-DD]  
**Fork URL:** [Link to your fork on GitHub]

---

## How to Use This Template

Copy this file into `Practice-Lab/`, rename it `YYYY-MM-DD_Day-N_log.md`, and fill in each section after your daily practice session. Commit and push your log every day — your commit history is your portfolio of progress. Aim for consistency over perfection: a short log every day beats a perfect log once a week.

---

## Day 1 — [Date: Fill in]

### 📚 Module Studied
Module 00 — Introduction: Why Git? Setup & Configuration

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| `git --version` | Verified Git is installed | Got version 2.43.0 |
| `git config --global user.name "..."` | Set my global name | First time setting this up |
| `git config --global user.email "..."` | Set my global email | Used my GitHub email |
| `git config --global color.ui auto` | Enabled color output | Terminal looks much nicer now |
| `git config alias.st status` | Created st alias | Saves typing every time |

### 🔬 Lab Completed
- [x] Lab: "Your First Git Identity Setup"
- Outcome: Successfully configured `~/.gitconfig` with name, email, color, and alias.

### 💡 Key Takeaways
- Git tracks **changes**, not files — this is a new mental model for me.
- The `~/.gitconfig` file stores global settings that apply to every repo on my machine.
- Aliases can save a lot of typing over time.

### ❓ Questions / Blockers
- What happens if I use a different email than my GitHub account email?

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [x] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 2 — [Date: Fill in]

### 📚 Module Studied
Module 01 — Foundations: Init, Add, Commit, Status, Log

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| `git init` | Created my first repository | The `.git/` folder appeared |
| `git status` | Checked working directory state | Red = untracked, green = staged |
| `git add README.md` | Staged a specific file | Only stages what I specify |
| `git add .` | Staged all changes at once | Useful but less precise |
| `git commit -m "..."` | Created my first commit | Got back a commit SHA! |
| `git log --oneline` | Read condensed history | Much cleaner than full `git log` |

### 🔬 Lab Completed
- [x] Lab: "Your First Repository — Track a Project"
- Outcome: Created `my-first-repo`, made two commits, viewed history.

### 💡 Key Takeaways
- The `.git/` directory IS the repository — never delete it.
- The staging area gives me control over exactly what goes into each commit.
- Commit messages should describe the *why*, not just the *what*.

### ❓ Questions / Blockers
- What is `git add -p` for? Need to practice interactive staging.

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [ ] 3 — Solid understanding
- [x] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 3 — [Date: Fill in]

### 📚 Module Studied
Module 02 — Intermediate Workflows: Branching, Merging & Stashing

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| `git switch -c feature/test` | Created and switched to new branch | Modern syntax, cleaner than checkout |
| `git switch main` | Returned to main branch | Files changed back instantly |
| `git merge feature/test` | Merged feature into main | Got a fast-forward merge |
| `git branch -d feature/test` | Deleted merged branch | Keeps repo clean |
| `git stash` | Saved WIP before switching | Changes disappeared safely |
| `git stash pop` | Restored WIP | Changes came back exactly as left |

### 🔬 Lab Completed
- [x] Lab: "Feature Branch Workflow"
- Outcome: Completed both fast-forward and 3-way merge scenarios. Practiced stash.

### 💡 Key Takeaways
- Branches are cheap — create them freely, delete them after merging.
- Fast-forward only happens when target hasn't diverged.
- Stash is like a clipboard for uncommitted work.

### ❓ Questions / Blockers
- When should I use `--squash` vs. regular merge?

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [x] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 4 — [Date: Fill in]

### 📚 Module Studied
Module 03 — Remote Collaboration: Remotes, Push, Pull & Pull Requests

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| `git remote add origin <url>` | Connected local repo to GitHub | origin is just a name/alias |
| `git push -u origin main` | First push to remote | -u sets up tracking |
| `git pull origin main` | Pulled GitHub UI edit locally | fetch + merge in one step |
| `git push -u origin feature/test` | Pushed a feature branch | Showed up in GitHub immediately |

### 🔬 Lab Completed
- [x] Lab: "Connect to GitHub and Collaborate"
- Outcome: Created GitHub repo, pushed, edited in UI, pulled, created and merged a PR.

### 💡 Key Takeaways
- `git fetch` is always safe — it never modifies local work.
- `-u` flag on first push creates the tracking relationship for future pushes.
- Pull Requests are a GitHub layer on top of Git branches — Git itself has no concept of a PR.

### ❓ Questions / Blockers
- When would I use `--force-with-lease`? Seems important to understand.

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [x] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 5 — [Date: Fill in]

### 📚 Module Studied
Module 04 — Advanced Git: Rebase, Cherry-pick, Reflog & History Rewriting

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| `git rebase -i HEAD~5` | Squashed 5 WIP commits into 1 | Opened an interactive editor |
| `git commit --amend` | Fixed a typo in last commit message | Works great for recent commits |
| `git reset --hard HEAD~1` | Practiced "losing" a commit | Very powerful, very scary |
| `git reflog cleanup-practice` | Found my "lost" commit SHA | Reflog saved me! |
| `git cherry-pick <SHA>` | Copied a commit to another branch | Like ctrl+C, ctrl+V for commits |

### 🔬 Lab Completed
- [x] Lab: "Clean Up History with Interactive Rebase"
- Outcome: Squashed 5 commits to 1, practiced reset + reflog recovery.

### 💡 Key Takeaways
- Interactive rebase is incredibly powerful for cleaning up WIP commit history before a PR.
- Reflog is the ultimate safety net — even "lost" commits are recoverable for ~30 days.
- `git reset --hard` is dangerous but the reflog means it's rarely permanent.

### ❓ Questions / Blockers
- Need to practice rebase conflicts — what happens when rebase hits a conflict mid-way?

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [x] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 6 — [Date: Fill in]

### 📚 Module Studied
(Which module did you work on today?)

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] Lab exercise title
- Outcome / what happened:

### 💡 Key Takeaways
- 
- 
- 

### ❓ Questions / Blockers
(Anything you're stuck on)

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [ ] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 7 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] Lab exercise title
- Outcome:

### 💡 Key Takeaways
- 
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [ ] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 8 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] Lab exercise title
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [ ] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 9 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] Lab exercise title
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [ ] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 10 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] Lab exercise title
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [ ] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

## Day 11 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 12 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 13 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 14 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 15 — [Date: Fill in] 🎉 Halfway There!

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 16 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 17 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 18 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 19 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 20 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 21 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 22 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 23 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 24 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 25 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 26 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 27 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 28 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 29 — [Date: Fill in]

### 📚 Module Studied

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways
- 

### ❓ Questions / Blockers

### ⭐ Confidence Rating (1-5)
- [ ] 1 — [ ] 2 — [ ] 3 — [ ] 4 — [ ] 5

---

## Day 30 — [Date: Fill in] 🏆 You Did It!

### 📚 Module Studied / Review

### ⚡ Commands Practiced
| Command | What I Used It For | Notes |
|---|---|---|
| | | |

### 🔬 Lab Completed
- [ ] 
- Outcome:

### 💡 Key Takeaways — 30-Day Reflection
Looking back over 30 days:
- The most valuable thing I learned:
- The command I use most often now:
- What I want to explore next:

### ❓ Questions for Further Exploration

### ⭐ Final Confidence Rating (1-5)
- [ ] 1 — Completely lost
- [ ] 2 — Getting there
- [ ] 3 — Solid understanding
- [ ] 4 — Can explain to others
- [ ] 5 — Could write a blog post

---

*Completed 30-Day Git Mastery Challenge — [Your Name] — [End Date]*

**Share your achievement:** Open an Issue in the Git-Mastery-Hub repo to let the community know you completed the challenge!
