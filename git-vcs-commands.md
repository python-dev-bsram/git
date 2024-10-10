## Git Commands: 

**clone**:  
Clones a remote Git repository to your local machine. This command copies the entire repository, including the history, to your local system.

```bash 
    git clone repository-url
```
---

**pull**:  
Downloads changes from the specified branch on the remote repository and merges them into your local branch.

```bash 
    git pull origin branch-name
```
---

**push**:  
Pushes the changes from your local branch to the corresponding branch on the remote repository.

```bash 
    git push origin branch-name
```

---
**add**:  
Stages all changes in your project directory, making them ready for a commit.

```bash 
    git add .
```

---

**add file**:  
Stages a specific file for commit, instead of staging all changes.

```bash 
    git add filename
```

---

**commit local changes**:  
Creates a new commit with a specific message. The message should describe the changes you made.

```bash  
    git commit -m "your commit message"
```

---

**init**:  
Initializes a new Git repository in your current directory. It creates the ```.git``` directory where Git will track all changes.

```bash 
    git init
```

---

**config**:  
Sets your username for all Git operations. This is a one-time configuration unless you want to change it later.

```bash 
    git config --global user.name "Your Name"
```

---

**config email**:  
Sets your email for Git operations. This email will appear in your commits.

```bash 
    git config --global user.email "your-email@example.com"
```

---

**add origin**:  
Adds a remote repository, usually referred to as "origin," to your local repository. You will use this remote to push and pull changes.


```bash 
    git remote add origin repository-url
```
---
**List origins**:  
Lists all the remote repositories associated with your local repository.

```bash  
    git remote -v
```

---
**check status**:  
Shows the status of your working directory, including files that are staged, unstaged, and untracked.

```bash 
    git status
```


---

**current branch**:  
Lists all the branches in your repository and highlights the branch you are currently on.

```bash 
    git branch
```

---
**list branch**:  
Lists all local and remote branches.

```bash 
    git branch -a
```

---

**switch branch**:  
Switches to the specified branch. This updates the working directory to reflect the state of the branch you're switching to.

```bash 
    git checkout branch-name
```

---

**merge branch**:  
Merges the specified branch into your current branch. If there are conflicts, Git will let you know and you can resolve them before completing the merge.

```bash 
    git merge branch-name
```

---

**git logs**:  
Shows a log of all commits made to the repository, starting from the most recent.

```bash 
    git log
```

---
**diff**:  
Shows the differences between files in your working directory and the last commit. It helps you see what has changed before committing.

```bash  
    git diff
```


---
**stach changes**:  
Temporarily saves your uncommitted changes so you can switch branches or perform other tasks without losing your work.

```bash 
    git stash
```

---
**stash index**:  
Applies a specific stash (based on its index) to your current working directory, without removing it from the stash list.

```bash 
    git stash apply stash@{index}
```

---
**remove stash**:  
Applies the most recent stash and removes it from the stash list.

```bash 
    git stash pop
```

---
**list stash**:  
Lists all the stashes that you've saved.

```bash 
    git stash list
```

---
**clear stash**:  
Deletes all stashed changes at once.

```bash 
    git stash clear
```

---
**reset changes**:  
Resets your working directory and staging area to the state of the last commit, discarding all local changes.

```bash 
    git reset --hard
```

---
**reflog**:  
Displays a log of all Git commands that have been executed, including ones not recorded in the regular commit history.
```bash 
    git reflog
```


---
**rm file commit**:  
Removes the specified file from your working directory and stages the removal for commit.

```bash 
    git rm filename
```

---
**reveret changes**:  
Creates a new commit that undoes the changes from a previous commit without altering the existing commit history.

```bash 
    git revert commit-id
```

---

**log**:  
Displays a condensed version of the commit history, showing only the commit hashes and messages.


```bash 
    git log --oneline
```

---

**cherry-pick**:  
Applies the changes introduced by a specific commit to your current branch, allowing you to pick changes from other branches or parts of the history.

```bash 
    git cherry-pick commit-id
```

---

### What is a Conflict?
A conflict occurs when Git cannot automatically merge changes because the same part of the code was edited in different branches.

### Conflict Resolution Options:

- **Accept Current Changes**:  
  Choose this option if you want to keep your local changes and ignore the incoming changes.

- **Accept Incoming Changes**:  
  Use this option if you want to discard your local changes and accept the changes coming from the remote.

- **Accept Both Changes**:  
  This option keeps both sets of changes. It will merge the local and incoming changes.

- **Compare Changes**:  
  Compare both sets of changes and decide which lines to keep.

---
