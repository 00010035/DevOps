# Git Guide

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
   git clone https://<repository-url>
   ```

## Lesson 2: Making Changes and Pushing Code
1. Open and edit a file (e.g., `README.md`):
   ```bash
   vim readme.md
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
   git commit -m "Added readme.md"
   ```
6. Push changes to the repository:
   ```bash
   git push
   ```

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
   git remote add origin https://github.com/00010035/test-private.git
   ```
5. Push your local project:
   ```bash
   git push --set-upstream origin master
   ```

## Lesson 4: Working with Branches
### Managing Branches
1. Create a new branch using the web interface or UI.
2. List all branches:
   ```bash
   git branch
   ```
3. Update your local branches:
   ```bash
   git pull
   ```
4. Switch to a specific branch:
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
   git push
   ```
4. Follow the command prompt instructions, e.g.:
   ```bash
   git push --set-upstream origin feature/database-connection
   
