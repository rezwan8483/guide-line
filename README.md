------------------------------------------------------------------------
## WSL (Windows Subsystem for Linux) Setup | Enable WSL (PowerShell Admin)
``` powershell
wsl --install
wsl --set-default-version 2
```
### Install Ubuntu 24.04
``` powershell
wsl --list --online
wsl --install -d Ubuntu-24.04
```
### Enter WSL & Update
``` bash
wsl
sudo apt update && sudo apt upgrade -y
```
### Backup WSL
``` powershell
wsl --export Ubuntu-24.04 "C:\WSL-Backup\Ubuntu-Backup.tar"
```
### Restore WSL
``` powershell
wsl --import Ubuntu-24.04 "." "C:\WSL-Backup\Ubuntu-Backup.tar"
```
### Delete Corrupted WSL Instance
``` powershell
wsl --list --verbose
wsl --unregister Ubuntu-24.04
```
------------------------------------------------------------------------
### Install Git on Ubuntu
**Installation**
``` bash
sudo apt install git -y
```
**Verify**
``` bash
git --version
```
------------------------------------------------------------------------
### GitHub CLI Setup (Ubuntu)
``` bash
sudo apt install curl -y
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh -y
gh --version
# Login
gh auth login
```
------------------------------------------------------------------------
### How to Clone my private Repo in Ubuntu
``` bash
ssh-keygen -t ed25519 -C "md-sarowar-alam"
cat ~/.ssh/id_ed25519.pub
# Go to https://github.com/settings/keys and save the key 
ssh -T git@github.com
# Success Message 
### Hi md-sarowar-alam! You've successfully authenticated, but GitHub does not provide shell access.
```
### => Now you can clone any repo from yor added Git
``` bash
git clone git@github.com:md-sarowar-alam/ostad-class-08.git
```
### Create a file and Push to remote repo 
``` bash
git status
git add README.md
git commit -m "Add my First File"
git push origin main
```
### Create a New Branch
``` bash
git checkout -b feature/my-branch
git branch -a
```
### Edit Files in the Branch
``` bash
git add .
# commit
git commit -m "My updates in branch"
# Push Branch to Remote
git push -u origin feature/my-branch
# Get Latest update of the branch from Remote Repo while local branch Selected * feature/my-branch
git pull
```
### Sync Branch with Main (Fresh Update from main → branch) | it won't work if there is no commit to any file.
``` bash
git checkout feature/my-branch
git fetch origin
git merge origin/main
```
### Sync Branch with Main | Rebase (fresh start, cleaner history)
``` bash
git checkout feature/my-branch
git fetch origin
git rebase origin/main
```

### if there is any conflict and you want to refresh branch as main 
``` bash 
# Discard all local changes
git reset --hard
# Switch to the branch you want to refresh
git checkout feature/my-branch
# Reset that branch to match main
git fetch origin
git reset --hard origin/main
# Update this to Remote Branch 
git push origin feature/my-branch --force
```
### if you want to Delete the Branch Instead
``` bash
git checkout main
git branch -D feature/my-branch
```
------------------------------------------------------------------------
### you Have udpated and fixed branch and you want to merge that to main 
``` bash 
# Switch to main
git checkout main
# Make sure main is up to date
git pull origin main
# Merge the branch into main
git merge feature/my-branch
# Push the updated main to remote
git push origin main
```
### Get the log of all 
``` bash 
git log --oneline --graph --decorate --all
```
------------------------------------------------------------------------------------------------------------------------------------------------
### Create a branch from feature/my-branch
``` bash 
git checkout feature/my-branch
git checkout -b feature/my-branch-from-branch
# Edit files and commit
vi README.md
git add .
git commit -m "Update from branch-based branch"
# Push this branch to remote
git push -u origin feature/my-branch-from-branch
```
### Create a branch from main
``` bash
git checkout main
git checkout -b feature/my-branch-from-main
# Edit files and commit
vi README.md
git add .
git commit -m "Update from main-based branch"
# Push this branch to remote
git push -u origin feature/my-branch-from-main
```
### Merge feature/my-branch-from-main into feature/my-branch-from-branch
``` bash
git checkout feature/my-branch-from-branch
git fetch origin
git merge origin/feature/my-branch-from-main
# Resolve conflicts if any | Commit merge
git push origin feature/my-branch-from-branch
```
### Merge feature/my-branch-from-branch into feature/my-branch-from-main
``` bash
git checkout feature/my-branch-from-main
git fetch origin
git merge origin/feature/my-branch-from-branch
# Resolve conflicts if any | Commit merge
git push origin feature/my-branch-from-main
```
------------------------------------------------------------------------
### If you find any conflict
``` bash 
# Open the file and resolve conflict
vi README.md
git add . 
git commit -m "Merge feature/my-branch-from-main into feature/my-branch-from-branch"
git push origin feature/my-branch-from-branch
```
------------------------------------------------------------------------
### Create a Local Git Repository
``` bash
#Create a folder
mkdir my-local-repo-creation-private
cd my-local-repo-creation-private
# Initialize git
git init
# Add files
echo "Hello World" > readme.txt
git add .
# Commit
git commit -m "Creating repo from Ubuntu"
```
### Create a GitHub Repository from Command Line (GitHub CLI)
``` bash
gh repo create my-local-repo-creation-private --private --source=. --remote=origin --push
```
------------------------------------------------------------------------
### Git Examples | Clone Specific Branch
``` bash
git clone --branch feature/test-change-02 --single-branch git@github.com:md-sarowar-alam/batch-08-class-git.git
```
### Clone deafult / main branch 
``` bash
git clone git@github.com:md-sarowar-alam/batch-08-class-git.git
```
### Merge Main Into Branch
``` bash
git checkout feature/test-change-02
git pull origin main
```
### Rebase Branch

``` bash
git fetch origin
git rebase origin/main
```
### Commit or Stash Before Rebase
``` bash
git add .
git commit -m "WIP"
git rebase origin/main
```
### Reset Branch to Main
``` bash
git checkout feature/my-change
git fetch origin
git reset --hard origin/main
git push --force origin feature/my-change
```
### Create a new branch (best practice: don't work on main)
``` bash
git checkout -b feature/edit-readme
```
### Edit a file
``` bash
vi README.md
```
### Check what changed
``` bash
git status
# Shows modified files and your branch name
git diff README.md
# Shows the unstaged changes you made in README.md
```
### Stage (add) changes
``` bash
git add README.md
# or add everything changed:
git add -A

````
### Confirm staged changes:
``` bash
git status
git diff --staged   # shows exactly what will be committed
```
### Commit your changes
``` bash
git commit -m "Improve README: add clone and usage examples"
# If you prefer multi-line message:
git commit
# (this opens your editor to write subject + body)
```
### Push the branch to remote
``` bash
git push -u origin feature/edit-readme
```
### Merge main into your branch (simple & safe)
``` bash
cd batch-08-class-git
git checkout feature/test-change-02
git pull origin main
# or (same thing)
git merge origin/main
```
------------------------------------------------------------------------
### Here is exactly how to create a repo locally and push it to GitHub | Create a local folder for your new repository
``` bash
mkdir my-new-repo
cd my-new-repo
```
### Initialize Git
``` bash 
git init
```
### Set default branch to main (recommended):
``` bash
git branch -M main
```
### Create some files
``` bash
echo "Hello GitHub" > README.md
```
### Stage and commit your files
``` bash
git add .
git commit -m "Initial commit"
```
### Create a remote repository on GitHub | Use GitHub CLI (gh)
``` bash
gh repo create my-new-repo --public --source=. --remote=origin
gh repo create my-new-repo --private --source=. --remote=origin
```
### Push your local repo to GitHub
``` bash
git push -u origin main
```
### Done! Your repo is now on GitHub.
``` bash
git remote -v
```
------------------------------------------------------------------------
### Merge one Branch into another
``` bash
git checkout feature/my-change-01
git fetch origin
git pull --rebase origin feature/my-change-01
git merge feature/my-change-02
```
### Revert & Reset Operations | Safe Revert (Creates new commit)
``` bash
git revert -m 1 7f076de5fed8cf5ac9cb544fa0f6e28e4243ed6d
git push origin main
```
### Dangerous Reset (Rewrites history)
``` bash
git reset --hard 38f5d6
git push origin main --force
```
### Warning: --force push overwrites remote history. Use with caution!
### Cleanup Operations | Delete Branches | Delete local branch
``` bash
git branch -d feature/my-change-01
```
### Force delete local branch
``` bash
git branch -D feature/my-change-01
```
### Delete remote branch
``` bash
git push origin --delete feature/my-change-01
```
------------------------------------------------------------------------
### Restore file from main | If you want the file back:
``` bash
git checkout origin/main -- file.txt
git add file.txt
git commit
```

---
------------------------------------------------------------------------
# Complete Forking Workflow (Step-by-Step)

## STEP 1 --- Fork the Repository (on GitHub)

-   Go to the original repository\
-   Click **Fork**\
-   Choose your GitHub account\
-   Your fork is created: `github.com/yourname/repo`

🎉 You now have your **origin** fork.

------------------------------------------------------------------------

## STEP 2 --- Clone Your Fork

``` bash
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
cd REPO_NAME
```

------------------------------------------------------------------------

## STEP 3 --- Add Upstream Remote

Your local repo only knows about your fork (`origin`).\
Add the original repo as `upstream`.

``` bash
git remote add upstream https://github.com/ORIGINAL_OWNER/REPO_NAME.git
```

Verify:

``` bash
git remote -v
```

Example:

    origin    https://github.com/yourname/repo.git (fetch)
    upstream  https://github.com/original/repo.git (fetch)

------------------------------------------------------------------------

## STEP 4 --- Stay Updated with Upstream

Always sync before starting new work.

``` bash
git fetch upstream
git checkout main
git merge upstream/main
```

Or safer:

``` bash
git pull upstream main
```

Push updated main to your fork:

``` bash
git push origin main
```

------------------------------------------------------------------------

## STEP 5 --- Create a Feature Branch

    git checkout -b feature/my-new-change

------------------------------------------------------------------------

## STEP 6 --- Do Your Work

    git add .
    git commit -m "Add new feature"

------------------------------------------------------------------------

## STEP 7 --- Push the Branch to Your Fork

    git remote set-url origin git@github.com:md-sarowar-alam/sarowar.git
    git push origin feature/my-new-change
    
------------------------------------------------------------------------

## STEP 8 --- Create Pull Request

-   Go to your fork on GitHub\
-   Click **Compare & pull request**\
-   Create PR from your fork → upstream/main

------------------------------------------------------------------------

## STEP 9 --- Make Requested Changes

    git add .
    git commit -m "Fix review comments"
    git push origin feature/my-new-change

PR updates automatically.

------------------------------------------------------------------------

## STEP 10 --- Merge (Maintainer Does This)

Maintainer approves & merges into upstream.\
Your fork becomes outdated → **repeat Step 4**.

------------------------------------------------------------------------

## Workflow Diagram

               +----------------------------+
               |      Upstream Repo         |
               |   original project owner   |
               +-------------+--------------+
                             ^
                             | Pull Request
                             |
             +---------------+----------------+
             |        Your Fork (origin)     |
             |   github.com/yourname/repo    |
             +---------------+----------------+
                             ^
                             |
                             | git push
                             v
                    +--------+--------+
                    |   Local Repo    |
                    +-----------------+

------------------------------------------------------------------------

## Why Forking Workflow Is Secure

  Action                        Allowed?
  ----------------------------- ----------
  Direct push to main repo      ❌ No
  PR-based merge                ✔ Yes
  Editing your fork             ✔ Yes
  Accidental deletion of main   ❌ No
  Force push to upstream        ❌ No

<!-- SECTION START -->
# Deploying a Node.js App to Heroku (When Starting From an Empty Git Repo)

This guide walks you through creating a simple Node.js + Express app and
deploying it to **Heroku**, even if your repository is empty.

------------------------------------------------------------------------

## 🚀 Prerequisites

Ensure the following are installed:

### **Git**

    git --version

### **Node.js & npm**

    node --version
    npm --version

### **Heroku CLI**

    heroku --version

------------------------------------------------------------------------

## 📁 Step 1: Create Project Folder

    mkdir my-heroku-app
    cd my-heroku-app

------------------------------------------------------------------------

## 🔧 Step 2: Initialize Git Repository

    git init

------------------------------------------------------------------------

## 🟦 Step 3: Initialize Node.js Project

    npm init -y

### Replace/ensure your `package.json` looks like:

``` json
{
  "name": "my-heroku-app",
  "version": "1.0.0",
  "description": "Simple Node.js app for Heroku",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^5.1.0"
  }
}
```

------------------------------------------------------------------------

## 📦 Step 4: Install Express

    npm install express

------------------------------------------------------------------------

## 📝 Step 5: Create `server.js`

    nano server.js

### Add the following content:

``` js
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.send('Hello World! Your Node.js app is running on Heroku 🚀');
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

------------------------------------------------------------------------

## 🔧 Step 6: Add Heroku `Procfile`

    nano Procfile

### Add:

    web: node server.js

------------------------------------------------------------------------

## 🛑 Step 7: Add `.gitignore`

    nano .gitignore

### Content:

    node_modules
    .env

------------------------------------------------------------------------

## 💾 Step 8: Commit Everything

    git add .
    git commit -m "Initial commit: Node.js Express app ready for Heroku"

------------------------------------------------------------------------

## ☁️ Step 9: Create Heroku App

    heroku login

Follow the on‑screen steps.

------------------------------------------------------------------------

## 🚀 Step 10: Deploy to Heroku

    git push heroku master:main

------------------------------------------------------------------------

## 📜 Debug Logs (Optional)

    heroku logs --tail

------------------------------------------------------------------------

## 📂 Final Folder Structure

    my-heroku-app/
    ├── Procfile
    ├── package.json
    ├── server.js
    ├── node_modules/ (ignored in Git)
    ├── .gitignore

------------------------------------------------------------------------

## 🎉 Deployment Complete!

Your app is now live on Heroku. Enjoy building!

<!-- SECTION END -->


## 🧑‍💻 Author
**Md. Sarowar Alam**  
Lead DevOps Engineer, Hogarth Worldwide  
📧 Email: sarowar@hotmail.com  
🔗 LinkedIn: [linkedin.com/in/sarowar](https://www.linkedin.com/in/sarowar/)

---
