# Git Guide

## Table of Contents
1. [Setting Up SSH Key for Terminal Connection](#lesson-1-setting-up-ssh-key-for-terminal-connection)
2. [Making Changes and Pushing Code](#lesson-2-making-changes-and-pushing-code)
3. [Connecting a Local Project to Git](#lesson-3-connecting-a-local-project-to-git)
4. [Working with Branches](#lesson-4-working-with-branches)
   - [Connecting Branches](#connecting-branches)
   - [Deleting Branches](#deleting-branches)
   - [Managing Branches](#managing-branches)
   - [Creating a New Branch via Command Line](#creating-a-new-branch-via-command-line)
5. [Git Rebase](#lesson-5-git-rebase)
6. [Git Stash](#lesson-6-git-stash)
7. [Git Log](#lesson-7-git-log)
8. [Resetting to a Previous Version](#lesson-8-resetting-to-a-previous-version)
9. [Amending the Last Commit](#lesson-9-amending-the-last-commit)

---

## Lesson 1: Setting Up SSH Key for Terminal Connection
1. Generate an SSH key:
   ```bash
   ssh-keygen
   ```
2. Log in to your **GitHub/GitLab** account and navigate to **Settings > SSH Keys**.
   1. Copy your public SSH key by running:
      ```bash
      cat ~/.ssh/id_ed25519.pub
      ```
   2. Paste the key into your account.
3. Clone the project:
   ```bash
   git clone git@<repository-url>
   ```

---

## Lesson 2: Making Changes and Pushing Code
1. Open and edit a file (e.g., `README.md`):
   ```bash
   vim README.md
   ```
2. Check the status of changes:
   ```bash
   git status
   ```
3. Stage all changes:
   ```bash
   git add .
   ```
4. Verify changes are staged (in green):
   ```bash
   git status
   ```
5. Commit the changes with a message:
   ```bash
   git commit -m "Added README.md"
   ```
6. Push changes to the repository:
   ```bash
   git push
   ```

---

## Lesson 3: Connecting a Local Project to Git
If you have a local project on your computer, follow these steps:
1. Initialize a Git repository:
   ```bash
   git init
   ```
2. Add your project directory as a safe directory:
   ```bash
   git config --global --add safe.directory '/path/to/your/project'
   ```
3. Create a project on **GitHub/GitLab**.
4. Add the remote repository:
   ```bash
   git remote add origin https://github.com/username/repository.git
   ```
5. Push your local project:
   ```bash
   git push --set-upstream origin master
   ```

---

## Lesson 4: Working with Branches

### Connecting Branches
To connect branches to the master (main):
1. Click on the **Switch branches** button.
2. Select **View all branches**.
3. Choose the branch you want to connect.
4. Click the **...** menu.
5. Select **New pull request**.
6. Create the pull request.
7. Confirm the branch connection.

### Deleting Branches
#### Online (GitHub/Web):
1. Go to **All branches**.
2. Click the **Delete** icon.

#### Locally:
1. Switch to the master branch:
   ```bash
   git checkout master
   ```
2. Pull the latest changes:
   ```bash
   git pull
   ```
3. Delete the branch locally:
   ```bash
   git branch -d <branch-name>
   ```

### Managing Branches
1. List all branches:
   ```bash
   git branch
   ```
2. Update your local branches:
   ```bash
   git pull
   ```
3. Switch to a specific branch:
   ```bash
   git checkout <name-of-branch>
   ```

### Creating a New Branch via Command Line
1. Switch to the `master` branch:
   ```bash
   git checkout master
   ```
2. Create and switch to a new branch locally:
   ```bash
   git checkout -b <name-of-branch>
   ```
3. Push the branch to the remote repository:
   ```bash
   git push --set-upstream origin <name-of-branch>
   ```

---

## Lesson 5: Git Rebase
Imagine two programmers are working on the same branch. Programmer 1 pushes their changes to GitHub. Programmer 2 makes changes but is unaware of the updated branch. When Programmer 2 tries to pull changes, they might encounter an error. To avoid this:

Use the following command to sync all changes:
```bash
git pull -r
```

---

## Lesson 6: Git Stash
### Example:
If you want to save your changes temporarily without committing them:
1. Save changes:
   ```bash
   git stash
   ```
2. Retrieve saved changes:
   ```bash
   git stash pop
   ```

---

## Lesson 7: Git Log
To view the commit history:
```bash
git log
```

### Take a specific commit:
1. Find the commit hash in the log.
2. Check out the commit:
   ```bash
   git checkout <commit-hash>
   ```

---

## Lesson 8: Resetting to a Previous Version
If you made local changes but didn’t push them to GitHub and want to revert to a previous state:
1. Reset hard to a specific version:
   ```bash
   git reset --hard HEAD~<number-of-commits>
   ```
2. Alternatively, reset without discarding changes:
   ```bash
   git reset HEAD~<number-of-commits>
   ```

---

## Lesson 9: Amending the Last Commit
If you want to modify the last commit:
1. Make the necessary changes.
2. Amend the commit:
   ```bash
   git commit --amend
   ```
3. Force push the updated commit:
   ```bash
   git push --force
   ```

