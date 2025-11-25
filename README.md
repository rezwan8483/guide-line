------------------------------------------------------------------------
## WSL (Windows Subsystem for Linux) Setup
### Enable WSL (PowerShell Admin)
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
wsl --import Ubuntu "C:\WSL" "C:\WSL-Backup\Ubuntu-Backup.tar"
```
### Delete Corrupted WSL Instance
``` powershell
wsl --unregister Ubuntu
```
------------------------------------------------------------------------
## Git Examples
### Clone Specific Branch

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
###Create a new branch (best practice: don't work on main)
``` bash
git checkout -b feature/edit-readme
```
###Edit a file
``` bash
vi README.md
```
###Check what changed
``` bash
git status
# Shows modified files and your branch name
git diff README.md
# Shows the unstaged changes you made in README.md
```
###Stage (add) changes
``` bash
git add README.md
# or add everything changed:
git add -A

````
###Confirm staged changes:
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
###Push the branch to remote
``` bash
git push -u origin feature/edit-readme
```
------------------------------------------------------------------------
