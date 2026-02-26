# Read Me - ML Project

## Stage 1: Basic Setup (Foundation)

### Step 1.1 – Create the Project Directory

```bash
mkdir ml-project
```
mkdir stands for 'make directory'. This command creates a new folder named ml-project.<br/>


### Step 1.2 – Navigate Into the Directory

```bash
cd ml-project
```
cd stands for 'change directory'. This moves your terminal session into the ml-project folder.<br/>


### Step 1.3 – Initialize a Git Repository

```bash
git init
```
This initializes a new empty Git repository inside ml-project.<br/>
It creates a hidden .git/ folder that stores all version control metadata.<br/>


### Step 1.4 – Create the Four Project Files

```bash
touch train.py predict.py utils.py README.md
```
The touch command creates empty files.<br/>
Creates all four project files as empty placeholders<br/>

### Step 1.5 – Check Repository Status

```bash
git status

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    README.md
    predict.py
    train.py
    utils.py

nothing added to commit but untracked files present (use "git add" to track)
```
This shows the current state of the working directory and staging area. It will list all untracked files (the four files you just created) in red.



## Stage 2: Version Control Workflow

Goal: Stage specific files, commit with a meaningful message, create a GitHub repository, connect local to remote, and push changes.<br/>


### Step 2.1 – Stage Only train.py and utils.py
```bash
git add train.py utils.py
```
git add moves specified files to the staging area. By listing only train.py and utils.py, we explicitly exclude predict.py and README.md from this commit.


### Step 2.2 – Commit the Staged Changes
```bash
git commit -m "Add training script and utilities"

[master (root-commit) 000000] Add training script and utilities
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 train.py
 create mode 100644 utils.py
```
git commit staged changes to the local repository history.<br/>


### Step 2.3 – Create Repository on GitHub

Browser method: Go to https://github.com → Click ‘New’ → Name it ml-project → Leave it empty (no README, no .gitignore) → Click 'Create repository'.


### Step 2.4 – Link Local Repository to GitHub
```bash
git remote add origin https://github.com/vaasanth20/ml-project.git
```
This command tells your local Git where the remote (online) repository is located.<br/>

To verify the connection was added successfully, run:<br/>
```bash
git remote -v
```


## Stage 3: Collaborative Workflow

Goal: Safely synchronize remote teammate changes with your local work, commit your local changes, and push everything to GitHub in the correct order.

**Remote:**
    - Updated predict.py (in GitHub)
    - Updated README.md (in GitHub)

**Local (Your Machine):**
    - Modified utils.py (uncommitted)
    - New config.py (uncommitted)


### Step 3.1 – Check Your Current Status First
```bash
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   utils.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md
	config.py
	predict.py

no changes added to commit (use "git add" and/or "git commit -a")

```
Before doing anything, always check what state your working directory is in. This shows us which files are modified or untracked. we should see utils.py as modified and config.py as a new untracked file.


### Step 3.2 – Fetch Remote Changes (Optional but Recommended)
```bash
git fetch origin
```
git fetch downloads all changes from the remote repository.<br/>


### Step 3.3 – Pull Remote Changes
```bash
git pull origin main

From https://github.com/vaasanth20/ml-project
 * branch            main       -> FETCH_HEAD
Updating xxx0000..xxx0000
Fast-forward
 README.md  | 1 +
 predict.py | 1 +
 2 files changed, 2 insertions(+)

```
git pull = git fetch + git merge.<br/>
This command downloads the latest commits from the remote main branch and merges them into your current local branch. Since we modified files (utils.py, config.py) are not yet committed, Git will handle the untracked and unstaged files carefully, only merging the remote-changed files (predict.py, README.md).


### Step 3.4 – Stage Your Modified and New Files
```bash
git add utils.py config.py
```
Now stage your local changes. We stage both the modified utils.py and the brand-new config.py together.


### Step 3.5 – Verify What is Staged
```bash
git status
```
Run git status again to confirm that utils.py and config.py are listed in green under 'Changes to be committed'.


### Step 3.6 – Commit Your Local Changes
```bash
git commit -m "Update utils and add configuration module"
```
###Record our local changes with a clear commit message.<br/>


### Step 3.7 – Push to Remote Repository
```bash
git push origin main
```
Since you already pulled the latest remote changes in Step 3.3,The push will succeed cleanly with no conflicts.


## Issues

### Merge Conflict


