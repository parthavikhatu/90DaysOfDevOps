# Day 22 - Git Fundamentals Notes

## What is the difference between git add and git commit?

git add places changes into the staging area.
git commit saves the staged changes permanently in the repository history.

---

## What does the staging area do? Why doesn't Git just commit directly?

The staging area lets us review and select which changes should be included in the next commit. This helps create clean and meaningful commits instead of saving every change immediately.

---

## What information does git log show you?

git log shows commit history including:

* Commit ID (hash)
* Author name
* Date and time
* Commit message

---

## What is the .git folder and what happens if you delete it?

The .git folder contains all repository information, commit history, branches, and configuration. If it is deleted, the directory is no longer a Git repository and all Git history is lost.

---

## What is the difference between a working directory, staging area, and repository?

### Working Directory

Where files are edited.

### Staging Area

Temporary area where changes are prepared for a commit.

### Repository

The database where Git permanently stores commits and project history.
