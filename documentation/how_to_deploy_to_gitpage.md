# PURPOSE

This guide explains how to deploy a simple HTML website to GitHub Pages. GitHub Pages is a free hosting service that turns your GitHub repository into a live website. Perfect for portfolios, project demos, and static websites.

# INSTRUCTIONS

## 1. PREPARE YOUR PROJECT

### 1.1 Create Your HTML File
- Create an `index.html` file in your project folder
- This will be the homepage of your site (GitHub Pages looks for `index.html` by default)
- Example location: `C:\dev\github\git-pages\git-test-page-1\index.html`

### 1.2 Test Locally
- Open your `index.html` file in a web browser
- Make sure everything looks and works as expected before deploying

## 2. INITIALIZE GIT REPOSITORY

### 2.1 Open Terminal
- Open PowerShell or Command Prompt
- Navigate to your project folder:
  ```powershell
  cd C:\dev\github\git-pages\git-test-page-1
  ```

### 2.2 Initialize Git
- Run this command to create a new Git repository:
  ```powershell
  git init
  ```
- This creates a hidden `.git` folder that tracks your changes

## 3. COMMIT YOUR FILES

### 3.1 Stage All Files
- Add all files to the staging area:
  ```powershell
  git add .
  ```
- The dot (`.`) means "add everything in this folder"

### 3.2 Create First Commit
- Save your changes with a commit message:
  ```powershell
  git commit -m "Initial commit"
  ```
- The message describes what changes you made

## 4. CONNECT TO GITHUB

### 4.1 Create GitHub Repository
- Go to https://github.com
- Click the "+" button → "New repository"
- Name your repository (e.g., `test-page`)
- Keep it public (required for free GitHub Pages)
- Don't initialize with README (you already have files)
- Click "Create repository"

### 4.2 Link Your Local Repository
- Copy your repository URL (looks like: `https://github.com/username/test-page.git`)
- Run this command to connect your local folder to GitHub:
  ```powershell
  git remote add origin https://github.com/username/test-page.git
  ```
- Replace `username` and `test-page` with your actual GitHub username and repository name

## 5. PUSH TO GITHUB

### 5.1 Upload Your Files
- Send your files to GitHub:
  ```powershell
  git push -u origin main
  ```
- `-u origin main` means "push to the main branch and remember this for next time"
- If the remote has existing content, you may need to force push:
  ```powershell
  git push -u origin main --force
  ```

## 6. ENABLE GITHUB PAGES

### 6.1 Using GitHub CLI (Recommended)
- If you have GitHub CLI installed (`gh`), run:
  ```powershell
  gh api repos/username/test-page/pages -X POST -f source[branch]=main -f source[path]=/
  ```
- Replace `username/test-page` with your GitHub username and repository name

### 6.2 Using GitHub Website (Alternative)
- Go to your repository on GitHub
- Click "Settings" tab
- Scroll down to "Pages" section in the left sidebar
- Under "Source", select:
  - Branch: `main`
  - Folder: `/ (root)`
- Click "Save"

### 6.3 Wait for Deployment
- GitHub Pages takes 1-2 minutes to build and deploy
- Your site will be available at: `https://username.github.io/repository-name/`
- Example: `https://raphaelfeliz.github.io/test-page/`

## 7. MAKE UPDATES (ONGOING)

### 7.1 Edit Your Files
- Make changes to your `index.html` or other files
- Save your changes

### 7.2 Quick Deploy
- Run this single command to stage, commit, and push:
  ```powershell
  git add . ; git commit -m "Update" ; git push
  ```
- Or do it step by step:
  ```powershell
  git add .
  git commit -m "Describe your changes here"
  git push
  ```

### 7.3 View Live Site
- Wait 1-2 minutes for GitHub to rebuild
- Refresh your browser at `https://username.github.io/repository-name/`
- Your changes should now be live!

## 8. TROUBLESHOOTING

### 8.1 Getting 404 Error
- Make sure your main file is named `index.html` (lowercase, no spaces)
- Check that GitHub Pages is enabled in repository settings
- Wait 2-3 minutes after pushing for the site to build
- Check build status:
  ```powershell
  gh api repos/username/repository-name/pages/builds/latest
  ```

### 8.2 Changes Not Showing
- Clear your browser cache (Ctrl + Shift + R or Ctrl + F5)
- Check that your commit was pushed: `git log` to see recent commits
- Verify on GitHub.com that your files updated

### 8.3 Permission Denied When Pushing
- Make sure you're logged into GitHub CLI: `gh auth login`
- Or use a personal access token if using HTTPS
- Or set up SSH keys for authentication

## 9. USEFUL COMMANDS

### 9.1 Check Status
```powershell
git status
```
- Shows which files have changed and haven't been committed

### 9.2 View Commit History
```powershell
git log --oneline
```
- Shows list of all your commits

### 9.3 Check Remote Connection
```powershell
git remote -v
```
- Shows which GitHub repository you're connected to

### 9.4 Undo Uncommitted Changes
```powershell
git checkout -- filename.html
```
- Reverts a file back to its last committed state
