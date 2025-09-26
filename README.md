
# DevOps Task 4 — Version-Controlled DevOps Project
 
**Objective:** Manage a DevOps project using Git best practices.  
**Tools:** Git, GitHub.

---

> This README contains *every step* you need to complete the task end-to-end - from local setup on Ubuntu to creating branches, PR workflow, Pull and Merging PRs.
---

## Prerequisites
- Ubuntu machine (or WSL on Windows) with terminal access.  
- Git installed: `sudo apt update && sudo apt install -y git`  
- GitHub account.

---

## One-time local setup (Ubuntu)
Configure your identity and sensible defaults:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Use credential helper if you prefer HTTPS
git config --global credential.helper 'cache --timeout=3600'

# Show helpful git output defaults
git config --global core.editor "nano"                # or code, vim
git config --global pull.rebase false
git config --global init.defaultBranch main
```

---

## Create a repository on GitHub (web UI)
1. Open GitHub (https://github.com) → Click **New** repository.  
2. Enter repository name: `Task4-ElevateLabs`
3. Add description, choose **Public** or **Private** as required.  
4. Click **Create repository**.

---

## Initialize local repo and push to GitHub
Assuming fresh project folder:

```bash
# create project folder
mkdir devops-task4
cd devops-task4

# create recommended files
echo "Sample Tect" > README.md
touch .gitignore

# initialize git
git init

# stage and commit
git add .
git commit -m "initialize repo with README and .gitignore"
git remote add origin https://github.com/Shikhrshukla/Task4-ElevateLabs.git

# set main and push
git branch -M main
git push -u origin main
```

If GitHub repository was initialized with a README already, pull first:
```bash
git pull origin main --allow-unrelated-histories
# resolve any merge, then push
git push origin main
```

---

## Branching model & naming conventions
Recommended simple model:
- `main` — production-ready code only.
- `dev` — integration branch for the next release.
- `feature/add-terraform-setup` — terraform feature branches.

Naming examples:
- `feature/add-terraform-setup`

---

## Feature workflow — step-by-step (commands)

**1. Start from latest dev**
```bash
git checkout -b dev
git pull origin dev
```

**2. Create feature branch**
```bash
git checkout -b feature/add-terraform-setup
```

**3. Implement changes (examples)**
- Add `main.tf` for Terraform.

**4. Stage & commit (small atomic commits)**
```bash
git add main.tf
git commit -m "add main.tf skeleton and variables"
```

**5. Push feature branch**
```bash
git push -u origin feature/add-terraform-setup
```

**6. Open PR to `dev`** (see PR section below)

**7. After PR review & merge to dev**
```bash
# delete remote branch after merge
git push origin --delete feature/add-terraform-setup

# delete local branch
git branch -d feature/add-terraform-setup
```

---

## Pull Request (PR) process
**Web UI:**
1. Visit repo → `Compare & pull request` (or create new PR).
2. Base: `dev`, Head: `feature/add-terraform-setup`.
3. Title: short & clear. Body: what changed, testing steps, related issues.
4. Assign reviewers, add labels, request review.
5. Address feedback by pushing commits to the same branch - PR auto-updates.

---

## Common troubleshooting & fixes
- **"Authentication failed" / keeps asking username+password**  
  - Use SSH keys (recommended) or setup `gh auth login` and credential helper.  
  - For HTTPS storing creds: `git config --global credential.helper store` (stores unencrypted).
- **"refusing to merge unrelated histories"**  
  - Happens when both local and remote have unrelated commits:
    ```bash
    git pull origin main --allow-unrelated-histories
    ```
- **"failed to push some refs"**  
  - Do `git pull --rebase origin <branch>` then resolve and push.
- **Large file / secret accidentally committed**  
  - Use `git rm --cached <file>` and add to `.gitignore`, then commit. For history removal use `git filter-repo` or `git filter-branch` (careful).
- **Accidentally committed to main**  
  - Create a new branch from that commit and reset `main` to previous:
    ```bash
    git branch hotfix-from-accidental
    git reset --hard origin/main
    git push --force origin main   # be careful: force push rewrites history
    ```

---

## Appendix - useful commands summary
```bash
# configure
git config --global user.name "Name"
git config --global user.email "email"

# repo setup & push
git init
git add .
git commit -m "initial"
git remote add origin git@github.com:<user>/devops-task4.git
git branch -M main
git push -u origin main

# branching
git checkout -b dev
git push -u origin dev
git checkout -b feature/name
git push -u origin feature/name

# merging locally
git checkout dev
git merge feature/name

# delete branch
git push origin --delete feature/name
git branch -d feature/name
```

---

## ScreenShots

<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-06-03" src="https://github.com/user-attachments/assets/4e4d93e2-2e02-4c56-8b82-5d74ad54c66c" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-06-58" src="https://github.com/user-attachments/assets/db9b341f-faa6-4505-a8c0-8ea5102c68d8" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-14-01" src="https://github.com/user-attachments/assets/2f85e58f-23b0-4140-9104-da7c940be71b" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-14-11" src="https://github.com/user-attachments/assets/6f273a4f-1b65-4c66-b49e-6935abbadd97" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-14-36" src="https://github.com/user-attachments/assets/6d9be8ae-8962-4a47-b3b3-fa76e4b2f94b" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-14-53" src="https://github.com/user-attachments/assets/bb308a73-baaa-4f37-b03b-a6db5d6415d2" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-15-26" src="https://github.com/user-attachments/assets/68f77e91-5161-4cc2-9a52-195649245d35" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-15-35" src="https://github.com/user-attachments/assets/81ff8623-6640-4bfd-b847-2fbc6017d01d" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 18-18-23" src="https://github.com/user-attachments/assets/10bbc893-fd88-46b9-ae70-cd7c4fa6e332" />
<img width="1920" height="1080" alt="Screenshot from 2025-09-26 19-22-20" src="https://github.com/user-attachments/assets/e8db6a6c-1b1e-483b-b817-af448591a71f" />

---
