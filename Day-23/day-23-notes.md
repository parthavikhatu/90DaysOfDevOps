# Day 23 – Git Branching & Working with GitHub

## Task 1: Understanding Branches

### What is a branch in Git?

A branch is an independent line of development that allows you to work on changes without affecting the main code.

### Why do we use branches instead of committing everything to main?

Branches help developers work on new features, bug fixes, and experiments safely without breaking the main branch.

### What is HEAD in Git?

HEAD is a pointer that refers to the current branch and latest commit you are working on.

### What happens to your files when you switch branches?

Git changes your working directory files to match the selected branch.

---

## Task 2: Branching Commands – Hands-On

### Commands Used

```bash
git branch
git branch feature-1
git checkout feature-1
git checkout -b feature-2
git switch feature-1
git switch main
git switch -c feature-2
git add .
git commit -m "Added feature1 file"
git log --oneline
git branch -d feature-2
git branch -D feature-2
```

### Observation

A commit made on feature-1 does not appear on main until the branch is merged.

### Difference Between git switch and git checkout

git switch is specifically designed for switching branches and is easier to understand. git checkout can switch branches as well as restore files.

---

## Task 3: Push to GitHub

### Commands Used

```bash
git remote add origin https://github.com/USERNAME/devops-git-practice.git
git remote -v
git push -u origin main
git push -u origin feature-1
```

### Difference Between origin and upstream

origin:
The remote repository you cloned from or your own GitHub repository.

upstream:
The original repository from which a fork was created.

---

## Task 4: Pull from GitHub

### Commands Used

```bash
git pull origin main
```

### Difference Between git fetch and git pull

git fetch:
Downloads changes from the remote repository but does not merge them.

git pull:
Downloads changes and automatically merges them into the current branch.

---

## Task 5: Clone vs Fork

### Clone a Repository

```bash
git clone https://github.com/octocat/Hello-World.git
```

### What is the difference between clone and fork?

Clone:
Creates a local copy of a repository on your machine.

Fork:
Creates a copy of a repository under your GitHub account.

### When would you clone vs fork?

Clone:
When you have direct access to the repository.

Fork:
When contributing to someone else's repository.

### After forking, how do you keep your fork in sync with the original repo?

```bash
git remote add upstream https://github.com/original-owner/repository.git
git fetch upstream
git merge upstream/main
git push origin main
```

---

## What I Learned

1. Branches allow isolated development without affecting the main branch.
2. GitHub remotes help synchronize local and remote repositories.
3. Forking is useful for contributing to repositories you do not own.
