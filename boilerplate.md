# Git & GitHub CLI Boilerplate (Windows / PowerShell)

## 1) Setup / Install

### Check Git
```powershell
git --version
```

### Check GitHub CLI
```powershell
gh --version
```

### Install GitHub CLI with winget
```powershell
winget install --id GitHub.cli
```

### If `gh` is still not recognized
Close the terminal completely and open it again, then run:

```powershell
gh --version
```

### Check SSH keys
```powershell
dir $HOME\.ssh
```

### Test SSH connection to GitHub
```powershell
ssh -T git@github.com
```

Expected kind of message:
```text
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 2) GitHub CLI Auth

### Login with GitHub CLI
```powershell
gh auth login
```

Recommended choices:
- GitHub.com
- SSH
- Login with a web browser

### Check auth status
```powershell
gh auth status
```

---

## 3) Repo Creation / Clone

### Go to your working folder
```powershell
cd C:\path\to\your\github-folder
```

### Create a new public repo and clone it locally
```powershell
gh repo create REPO_NAME --public --clone
```

### Create a new private repo and clone it locally
```powershell
gh repo create REPO_NAME --private --clone
```

### Clone an existing repo
```powershell
gh repo clone OWNER/REPO_NAME
```

### Enter the repo folder
```powershell
cd REPO_NAME
```

### Check the remote
```powershell
git remote -v
```

Expected SSH style remote:
```text
origin  git@github.com:OWNER/REPO_NAME.git (fetch)
origin  git@github.com:OWNER/REPO_NAME.git (push)
```

---

## 4) First Commit

### See files
```powershell
dir
```

### See hidden files too
```powershell
dir -Force
```

### Create a README
```powershell
"# Project Title" | Out-File -Encoding utf8 README.md
```

### Create a new file
```powershell
ni app.py
```

### Stage everything
```powershell
git add .
```

### Stage one file only
```powershell
git add README.md
```

### Commit
```powershell
git commit -m "Initial commit"
```

### Push current branch
```powershell
git push
```

### Push and set upstream
```powershell
git push -u origin main
```

---

## 5) Daily Git Commands

### Check status
```powershell
git status
```

### See commit history
```powershell
git log --oneline --graph --decorate --all
```

### Pull latest changes
```powershell
git pull
```

### Add all changes
```powershell
git add .
```

### Commit changes
```powershell
git commit -m "Describe your change"
```

### Push changes
```powershell
git push
```

---

## 6) Branches

### See current branch
```powershell
git branch
```

### See all branches
```powershell
git branch -a
```

### Create a new branch
```powershell
git checkout -b feature/my-branch
```

### Switch to an existing branch
```powershell
git checkout main
```

### Newer switch command
```powershell
git switch main
```

### Create and switch with newer syntax
```powershell
git switch -c feature/my-branch
```

### Push a new branch
```powershell
git push -u origin feature/my-branch
```

### Delete local branch
```powershell
git branch -d feature/my-branch
```

---

## 7) Remote Commands

### Show remotes
```powershell
git remote -v
```

### Add a remote manually
```powershell
git remote add origin git@github.com:OWNER/REPO_NAME.git
```

### Change remote URL
```powershell
git remote set-url origin git@github.com:OWNER/REPO_NAME.git
```

### Remove remote
```powershell
git remote remove origin
```

---

## 8) Undo / Fix Commands

### Unstage a file
```powershell
git restore --staged FILE_NAME
```

### Discard local changes in a file
```powershell
git restore FILE_NAME
```

### Discard all local unstaged changes
```powershell
git restore .
```

### Amend last commit message or content
```powershell
git commit --amend
```

### Reset last commit but keep changes
```powershell
git reset --soft HEAD~1
```

### Reset last commit and unstage changes
```powershell
git reset --mixed HEAD~1
```

### Reset hard to previous commit
```powershell
git reset --hard HEAD~1
```

**Warning:** `--hard` deletes local uncommitted work.

---

## 9) Inspect Changes

### See unstaged changes
```powershell
git diff
```

### See staged changes
```powershell
git diff --staged
```

### See a file's history
```powershell
git log -- FILE_NAME
```

### Show details of a commit
```powershell
git show COMMIT_HASH
```

---

## 10) Stash

### Save local changes temporarily
```powershell
git stash
```

### Save with a message
```powershell
git stash push -m "work in progress"
```

### See stashes
```powershell
git stash list
```

### Restore latest stash
```powershell
git stash pop
```

---

## 11) Tags

### Create a tag
```powershell
git tag v1.0.0
```

### Push tags
```powershell
git push --tags
```

### List tags
```powershell
git tag
```

---

## 12) .gitignore Basics

### Create `.gitignore`
```powershell
ni .gitignore
```

Typical entries:
```gitignore
__pycache__/
*.pyc
.env
.venv/
node_modules/
dist/
build/
.DS_Store
Thumbs.db
```

**Never commit:**
- `.env`
- secrets
- API keys
- private SSH keys
- whole `.ssh` folder

---

## 13) Useful GitHub CLI Commands

### Open repo in browser
```powershell
gh repo view --web
```

### Create a repo without cloning
```powershell
gh repo create REPO_NAME --public
```

### View repo details
```powershell
gh repo view OWNER/REPO_NAME
```

### Create an issue
```powershell
gh issue create
```

### List issues
```powershell
gh issue list
```

### Create a pull request
```powershell
gh pr create
```

### List pull requests
```powershell
gh pr list
```

### Check auth status
```powershell
gh auth status
```

### Logout
```powershell
gh auth logout
```

---

## 14) Common Problems

### `gh` is not recognized
- GitHub CLI is not installed, or
- terminal was not reopened after install, or
- PATH is not updated

### Repo name already exists
```text
GraphQL: Name already exists on this account
```

Fix:
- use another repo name, or
- clone the existing repo:
```powershell
gh repo clone OWNER/REPO_NAME
```

### Wrong dashes in commands
Correct:
```powershell
gh repo create REPO_NAME --public --clone
```

Wrong:
```powershell
gh repo create REPO_NAME —public —clone
```

Use normal keyboard hyphens: `--`

### SSH works but no shell access
This is normal:
```text
GitHub does not provide shell access.
```

It still means SSH auth is working.

---

## 15) Good Minimal Workflow

```powershell
cd C:\path\to\repo
git status
git pull
git add .
git commit -m "Describe change"
git push
```

---

## 16) Recommended Commit Message Style

Examples:
```text
Initial commit
Add README
Create project structure
Add data loading script
Fix login bug
Refactor API client
Update documentation
```

Avoid vague messages like:
```text
update
changes
fix stuff
```

---

## 17) Quick Start Template

### New repo from scratch
```powershell
gh auth status
cd C:\path\to\github-folder
gh repo create REPO_NAME --public --clone
cd REPO_NAME
"# REPO_NAME" | Out-File -Encoding utf8 README.md
git add README.md
git commit -m "Initial commit"
git push -u origin main
```

### Existing repo
```powershell
cd C:\path\to\github-folder
gh repo clone OWNER/REPO_NAME
cd REPO_NAME
git remote -v
```

---

## 18) Commands Used in This Setup Flow

```powershell
git --version
dir $HOME\.ssh
ssh -T git@github.com
winget --version
winget install --id GitHub.cli
gh --version
gh auth login
gh auth status
cd C:\path\to\github-folder
gh repo create REPO_NAME --public --clone
gh repo clone OWNER/REPO_NAME
git remote -v
```

---

## 19) Final Notes

- Use `SSH` for Git operations if you want key-based auth.
- Keep your private SSH key private.
- Public repos expose repo contents, not your local machine.
- Before changing files blindly after clone, run:
```powershell
dir
git status
```
