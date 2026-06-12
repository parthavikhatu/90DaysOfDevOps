# Day 24 – Advanced Git: Merge, Rebase, Stash & Cherry-Pick

## Task 1: Git Merge

### Fast-Forward Merge

A fast-forward merge happens when the target branch has no new commits. Git simply moves the branch pointer forward without creating a merge commit.

### Merge Commit

Git creates a merge commit when both branches have new commits and their histories have diverged.

### Merge Conflict

A merge conflict occurs when the same part of a file is modified in different branches and Git cannot automatically decide which change to keep.

### Observations

* Merging feature-login into main resulted in a Fast-Forward Merge.
* Merging feature-signup into main created a Merge Commit because main had additional commits.
* An intentional conflict was created by editing the same line in both branches and resolved manually.

---

## Task 2: Git Rebase

### What Does Rebase Do?

Rebase takes commits from one branch and reapplies them on top of another branch, creating a cleaner and more linear history.

### Rebase vs Merge History

* Merge preserves branch history and creates merge commits.
* Rebase rewrites history to appear as if work was completed sequentially.

### Why Not Rebase Shared Commits?

Rebasing rewrites commit history. If commits have already been pushed and shared, rebasing can cause conflicts and confusion for other team members.

### When to Use Rebase vs Merge

* Use Rebase for a clean, linear history before merging.
* Use Merge when you want to preserve the exact branch history.

### Observations

* Created feature-dashboard branch and added commits.
* Added a new commit to main.
* Rebasing feature-dashboard onto main produced a cleaner commit history.

---

## Task 3: Squash Merge vs Regular Merge

### What is Squash Merge?

Squash merge combines multiple commits from a branch into a single commit before merging.

### Squash Merge Observations

* Created feature-profile branch with multiple small commits.
* Merged using --squash.
* Only one commit appeared on main.

### Regular Merge Observations

* Created feature-settings branch with multiple commits.
* Merged normally.
* All individual commits remained visible in Git history.

### When to Use Squash Merge?

Use squash merge when many small commits belong to one feature and you want a cleaner history.

### Trade-Off of Squashing

* Cleaner commit history.
* Loss of detailed commit-by-commit information.

---

## Task 4: Git Stash

### What is Git Stash?

Git stash temporarily saves uncommitted changes so you can switch branches without committing unfinished work.

### git stash pop vs git stash apply

| Command         | Applies Changes | Removes Stash |
| --------------- | --------------- | ------------- |
| git stash pop   | Yes             | Yes           |
| git stash apply | Yes             | No            |

### Real-World Use Case

Stash is useful when working on a task and an urgent issue requires switching branches immediately.

### Observations

* Stashed unfinished changes.
* Switched branches and completed other work.
* Restored changes using git stash pop.
* Created multiple stashes and applied a specific stash from the list.

---

## Task 5: Cherry-Pick

### What Does Cherry-Pick Do?

Cherry-pick copies a specific commit from one branch and applies it to another branch.

### When Would You Use Cherry-Pick?

* Applying a hotfix to another branch.
* Copying a specific bug fix without merging an entire feature branch.
* Moving selected changes between release branches.

### What Can Go Wrong?

* Merge conflicts.
* Duplicate commits.
* Confusing project history if overused.

### Observations

* Created feature-hotfix branch with three commits.
* Cherry-picked only the second commit onto main.
* Verified that only the selected commit was added.

---

# Commands Learned

```bash
git merge branch-name

git merge --squash branch-name

git rebase main

git stash

git stash push -m "message"

git stash list

git stash pop

git stash apply stash@{0}

git cherry-pick <commit-hash>

git log --oneline --graph --all
```

# Key Takeaways

1. Merge combines branch histories.
2. Fast-forward merge occurs when no divergent commits exist.
3. Rebase creates a cleaner linear history.
4. Never rebase shared commits.
5. Squash merge combines multiple commits into one.
6. Git stash saves unfinished work temporarily.
7. Cherry-pick copies a specific commit to another branch.
8. Merge conflicts occur when Git cannot automatically combine changes.
9. git log --oneline --graph --all helps visualize repository history.
10. Understanding Merge, Rebase, Stash, and Cherry-Pick is essential for real-world Git workflows and DevOps projects.
