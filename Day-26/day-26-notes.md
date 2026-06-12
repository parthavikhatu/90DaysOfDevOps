# Day 26 – GitHub CLI: Manage GitHub from Your Terminal

## Introduction

GitHub CLI (gh) is a command-line tool that allows developers and DevOps engineers to interact with GitHub directly from the terminal. It helps manage repositories, issues, pull requests, workflows, releases, and GitHub Actions without opening a web browser.

---

# Task 1: Install and Authenticate

## Installation

Verified GitHub CLI installation using:

```bash
gh --version
```

## Authentication

Logged into GitHub using:

```bash
gh auth login
```

Verified authentication status:

```bash
gh auth status
```

Checked active GitHub account:

```bash
gh api user
```

## What Authentication Methods Does gh Support?

1. Browser-based authentication
2. Personal Access Token (PAT)
3. SSH authentication
4. GitHub Enterprise authentication

---

# Task 2: Working with Repositories

## Create Repository

Created a new public repository with README:

```bash
gh repo create repo-name --public --clone --add-readme
```

## Clone Repository

Cloned repository using GitHub CLI:

```bash
gh repo clone owner/repository
```

## View Repository Details

```bash
gh repo view
```

## List All Repositories

```bash
gh repo list
```

## Open Repository in Browser

```bash
gh repo view --web
```

## Delete Repository

```bash
gh repo delete repo-name
```

### Observations

* Repositories can be created and managed without using GitHub website.
* GitHub CLI saves time and improves productivity.
* Useful for automation and scripting.

---

# Task 3: Issues

## Create Issue

```bash
gh issue create
```

Or:

```bash
gh issue create --title "Bug Report" --body "Application login failed" --label bug
```

## List Open Issues

```bash
gh issue list
```

## View Specific Issue

```bash
gh issue view 1
```

## Close Issue

```bash
gh issue close 1
```

## How Could gh issue Be Used in Automation?

* Automatically create issues when monitoring alerts occur.
* Create issues from CI/CD failures.
* Generate bug reports from scripts.
* Close issues automatically after successful deployment.
* Integrate with Jenkins, Grafana, Prometheus, and monitoring tools.

---

# Task 4: Pull Requests

## Create Branch

```bash
git checkout -b feature-update
```

## Commit Changes

```bash
git add .
git commit -m "Added new feature"
```

## Push Branch

```bash
git push origin feature-update
```

## Create Pull Request

```bash
gh pr create --fill
```

## List Pull Requests

```bash
gh pr list
```

## View Pull Request

```bash
gh pr view
```

## Merge Pull Request

Merge Commit:

```bash
gh pr merge --merge
```

Squash Merge:

```bash
gh pr merge --squash
```

Rebase Merge:

```bash
gh pr merge --rebase
```

## What Merge Methods Does gh pr merge Support?

1. Merge Commit (--merge)
2. Squash Merge (--squash)
3. Rebase Merge (--rebase)

## How Would You Review Someone Else's PR?

View PR:

```bash
gh pr view <pr-number>
```

Checkout PR:

```bash
gh pr checkout <pr-number>
```

Approve PR:

```bash
gh pr review <pr-number> --approve
```

Request Changes:

```bash
gh pr review <pr-number> --request-changes
```

Add Comment:

```bash
gh pr review <pr-number> --comment
```

---

# Task 5: GitHub Actions & Workflows (Preview)

## List Workflow Runs

```bash
gh run list
```

## View Workflow Status

```bash
gh run view <run-id>
```

## List Workflows

```bash
gh workflow list
```

## How Could gh run and gh workflow Be Useful in CI/CD?

* Monitor pipeline execution.
* Check build and deployment status.
* View workflow logs.
* Restart failed workflows.
* Automate deployment monitoring.
* Integrate workflow checks into DevOps scripts.

### Observations

GitHub CLI provides direct visibility into CI/CD pipelines from the terminal, making automation easier and reducing dependency on the web interface.

---

# Task 6: Useful GitHub CLI Commands

## GitHub API

```bash
gh api user
```

Used to make raw GitHub API calls.

## GitHub Gists

Create Gist:

```bash
gh gist create file.txt
```

List Gists:

```bash
gh gist list
```

## Releases

Create Release:

```bash
gh release create v1.0
```

List Releases:

```bash
gh release list
```

## Aliases

Create Alias:

```bash
gh alias set prs "pr list"
```

Use Alias:

```bash
gh prs
```

## Search Repositories

```bash
gh search repos kubernetes
```

### Observations

These commands help automate repetitive GitHub tasks and improve productivity for DevOps engineers.

---

# Key Takeaways

* GitHub CLI enables complete GitHub management from the terminal.
* Authentication can be done using Browser, PAT, SSH, or Enterprise login.
* Repositories, issues, and pull requests can be managed without using a browser.
* GitHub CLI supports GitHub Actions and workflow monitoring.
* Useful for DevOps automation, scripting, and CI/CD operations.
* Commands support JSON output for machine-readable automation.
* GitHub CLI is an essential tool for modern DevOps engineers.

---

# Important Commands Learned Today

```bash
gh auth login
gh auth status
gh repo create
gh repo clone
gh repo view
gh repo list
gh repo delete

gh issue create
gh issue list
gh issue view
gh issue close

gh pr create
gh pr list
gh pr view
gh pr checkout
gh pr review
gh pr merge

gh workflow list
gh run list
gh run view

gh api
gh gist create
gh gist list

gh release create
gh release list

gh alias set
gh alias list

gh search repos
```
