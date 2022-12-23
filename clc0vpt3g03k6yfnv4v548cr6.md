# A Cheatsheet For Git

> Here is a cheat sheet for some commonly used Git commands:

### Setup

- <mark>**git config --global user.name "Your Name":**</mark> Set your name to be used as the commit author
- <mark>**git config --global user.email "your@email.com":**</mark> Set your email to be used as the commit author

---

### Creating Repositories
- **<mark>git init:</mark>** Initialize a new Git repository
- **<mark>git clone `<repository>`:</mark>** Clone an existing repository

---

### Making Changes

- <mark>**git status:**</mark> Check the status of your repository
- <mark>**git add `<file>`:**</mark> Add a file to the staging area
- <mark>**git add . :**</mark> Add all modified and new files to the staging area
- <mark>**git commit -m "message":**</mark> Commit changes with a message
- <mark>**git reset HEAD `<file>`:**</mark> Remove a file from the staging area

---

### Viewing History

- <mark>**git log:**</mark> View the commit history
- <mark>**git diff:**</mark> View changes that have not been staged
- <mark>**git diff**</mark> --staged: View changes that have been staged

---

### Working with Remotes

- <mark>**git remote add `<name> <url>`:**</mark> Add a remote repository
- <mark>**git push `<name> <branch>`:**</mark> Push changes to a remote repository
- <mark>**git pull `<name> <branch>`:**</mark> Pull changes from a remote repository

---

### Branching

- <mark>**git branch:**</mark> List all branches
- <mark>**git branch `<name>`:**</mark> Create a new branch
- <mark>**git branch -d `<name>`:**</mark> Delete a branch
- <mark>**git checkout `<name>`:**</mark> Switch to a branch

---

### Merging

- <mark>**git merge `<branch>`:**</mark> Merge a branch into the current branch

---

### Stashing Changes

- <mark>**git stash:**</mark> Stash changes
- <mark>**git stash list:**</mark> View a list of stashes
- <mark>**git stash apply:**</mark> Apply the latest stash
- <mark>**git stash drop:**</mark> Discard the latest stash

---

### Tagging

- <mark>**git tag `<tagname>`:**</mark> Create a new tag
- <mark>**git tag -a `<tagname>` -m "message":**</mark> Create a new tag with a message
- <mark>**git tag -d `<tagname>`:**</mark> Delete a tag
- <mark>**git push --tags:**</mark> Push tags to the remote repository

---

### Reverting Changes

- <mark>**git revert HEAD:**</mark> Revert the last commit
- <mark>**git revert `<commit>`:**</mark> Revert a specific commit

---

### Resetting

- <mark>**git reset HEAD:**</mark> Reset the staging area to the last commit
- <mark>**git reset --hard HEAD:**</mark> Reset the staging area and working directory to the last commit
- <mark>**git reset --hard `<commit>`:**</mark> Reset the staging area and working directory to a specific commit

---

### Aliases
- <mark>**git config --global alias.`<alias_name> <git_command>`:**</mark> Create aliases for commonly used commands