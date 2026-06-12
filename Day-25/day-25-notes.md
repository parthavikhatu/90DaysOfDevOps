# Day 25 – Git Reset vs Revert & Branching Strategies

## Task 1: Git Reset – Observations

### Difference Between --soft, --mixed, and --hard

| Option            | Commit History | Staging Area        | Working Directory |
| ----------------- | -------------- | ------------------- | ----------------- |
| git reset --soft  | Commit removed | Changes kept staged | Changes kept      |
| git reset --mixed | Commit removed | Changes unstaged    | Changes kept      |
| git reset --hard  | Commit removed | Changes removed     | Changes deleted   |

### Which One Is Destructive and Why?

git reset --hard is destructive because it permanently deletes changes from the working directory and staging area.

### When Would You Use Each One?

* --soft: When you want to modify or combine commits while keeping changes staged.
* --mixed: When you want to unstage changes but keep the code.
* --hard: When you want to completely discard commits and changes.

### Should You Ever Use git reset on Pushed Commits?

No. Reset rewrites commit history and can create problems for other developers working on the same repository.

---

## Task 2: Git Revert – Observations

### What Happens When Reverting Commit Y?

Git creates a new commit that reverses the changes introduced by commit Y.

### Is Commit Y Still in History?

Yes. Commit Y remains in the commit history, but a new revert commit is added.

### How Is git revert Different from git reset?

* git reset removes commits from branch history.
* git revert creates a new commit that undoes previous changes.

### Why Is Revert Considered Safer?

Because it preserves commit history and does not rewrite shared history.

### When Would You Use Revert vs Reset?

* Use reset for local commits that have not been pushed.
* Use revert for commits that have already been pushed or shared.

---

## Task 3: Reset vs Revert Summary

| Feature                      | git reset                     | git revert                |
| ---------------------------- | ----------------------------- | ------------------------- |
| What it does                 | Moves branch pointer backward | Creates a new undo commit |
| Removes commit from history? | Yes                           | No                        |
| Rewrites history?            | Yes                           | No                        |
| Safe for shared branches?    | No                            | Yes                       |
| When to use                  | Local cleanup                 | Undo pushed commits       |

---

## Task 4: Branching Strategies

### 1. GitFlow

#### How It Works

Uses multiple long-lived branches:

* main
* develop
* feature
* release
* hotfix

#### Flow

main
│
├── develop
│ ├── feature/login
│ ├── feature/payment
│
├── release/v1.0
│
└── hotfix/critical-bug

#### Used For

Large teams and projects with scheduled releases.

#### Pros

* Well organized
* Stable production branch
* Supports multiple releases

#### Cons

* Complex workflow
* More branch management

---

### 2. GitHub Flow

#### How It Works

Create a feature branch from main, make changes, open a Pull Request, review, merge, and deploy.

#### Flow

main
│
├── feature-login
├── feature-payment
└── feature-dashboard

#### Used For

Startups, SaaS products, and continuous deployment environments.

#### Pros

* Simple
* Fast development
* Easy collaboration

#### Cons

* Not ideal for maintaining multiple release versions

---

### 3. Trunk-Based Development

#### How It Works

Developers work directly on main or use very short-lived branches and merge frequently.

#### Flow

main
│
├── short-feature-1
├── short-feature-2
└── short-feature-3

#### Used For

High-speed development teams with strong CI/CD pipelines.

#### Pros

* Fast integration
* Fewer merge conflicts
* Supports continuous delivery

#### Cons

* Requires automated testing
* Requires disciplined development practices

---

## Answers

### Which Strategy Would You Use for a Startup Shipping Fast?

GitHub Flow

### Which Strategy Would You Use for a Large Team with Scheduled Releases?

GitFlow

### Which One Does Kubernetes Use?

Kubernetes mainly follows Trunk-Based Development with pull requests and short-lived branches.

---

## Important Commands Learned Today

### Reset

git reset --soft HEAD~1

git reset --mixed HEAD~1

git reset --hard HEAD~1

### Revert

git revert <commit-hash>

### Recovery

git reflog

### Why git reflog Is Important

git reflog acts as Git's safety net. It records every movement of HEAD and allows recovery of commits even after a hard reset.

---

## Key Takeaways

* Use reset to move branch history backward.
* Use revert to safely undo commits.
* Avoid reset on pushed commits.
* Revert is safer for shared repositories.
* GitFlow is best for large teams with release cycles.
* GitHub Flow is best for startups and rapid deployment.
* Trunk-Based Development is best for CI/CD-focused teams.
* git reflog can recover lost commits after mistakes.
