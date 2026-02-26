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

**You updated a file on your local system**

You edited README.md and committed it.

**Before pulling, you updated the same file directly on GitHub**

Now GitHub has a different version of the same file.

So now:

- Your local main has 1 new commit
- GitHub origin/main has 1 different commit

when we pull the code from the remote:
```bash
git pull origin main


From https://github.com/vaasanth20/ml-project
 * branch            main       -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```
This is called diverged branches

Ran:
```bash
git pull --no-rebase origin main

Merge branch 'main' of https://github.com/vaasanth20/ml-project
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.

From https://github.com/vaasanth20/ml-project
 * branch            main       -> FETCH_HEAD
Auto-merging README.md
Merge made by the 'ort' strategy.
 README.md | 15 ++++++++-------
 1 file changed, 8 insertions(+), 7 deletions(-)
```
Pull changes from GitHub and MERGE them with my local branch.

**Why Git Opened the Commit Message Editor**

Git is creating a merge commit.

It is asking you:

>"Please enter a commit message to explain this merge."

This is normal.

You usually just:

- Press ESC
- Type :wq
- Press Enter

it saves and exits editor.

**What These Lines Mean**
* the line: *
```bash
Merge branch 'main' of https://github.com/vaasanth20/ml-project
```

* Git merged: *

- Your local commit
- GitHub commit

* This part: *
```bash
Auto-merging README.md
```

Git automatically combined both changes.
There was no conflict

* This part: *
```bash
Merge made by the 'ort' strategy.
```

"ort" is Git’s modern merge engine.
It just means:

> Git successfully merged the branches.

Nothing is wrong.

This part:
```bash
README.md | 15 ++++++++-------
1 file changed, 8 insertions(+), 7 deletions(-)
```

This means:

- 8 lines were added
- 7 lines were removed 
- In 1 file (README.md)

**Final Result**

Now your branch contains:

- Your local changes
- GitHub changes
- A merge commit connecting them

