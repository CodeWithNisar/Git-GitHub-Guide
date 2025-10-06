# Git & GitHub Complete Guide 🚀

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white)

**A Beginner-Friendly Guide from Zero to Hero**

[Quick Start](#-quick-checklist) • [Local to GitHub](#-scenario-a---local-folder--github) • [GitHub to Local](#-scenario-b---github--vs-code) • [Commands](#-essential-commands) • [Troubleshooting](#-common-errors--solutions)

</div>

---

## 🎯 Quick Checklist

Before you begin, make sure you have:

- ✅ **Git installed** → Check with `git --version`
- ✅ **VS Code installed**
- ✅ **GitHub account** ready & logged in
- ✅ **(Optional)** `code` command enabled in VS Code

---

## ⚙️ Basic Setup (One-Time Configuration)

```bash
# Check Git installation
git --version

# Configure your identity
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

> **Note:** `--global` sets this for all projects on your system. For specific projects, use `git config user.name "Project Specific"` inside that folder.

---

## 📁 Scenario A - Local Folder → GitHub

### Step 1: Navigate to Your Project
```bash
cd /path/to/your-project
```

### Step 2: Check if Git is Already Initialized
```bash
# For Mac/Linux:
ls -la

# For Windows PowerShell:
dir /a

# If .git folder doesn't exist:
git status
```

### Step 3: Initialize Git Repository
```bash
git init
```

### Step 4: Create .gitignore File
Create a file named `.gitignore` in your project root:

```gitignore
node_modules/
.DS_Store
.vscode/
dist/
*.log
.env
```

### Step 5: Stage and Commit Files
```bash
git add .
git commit -m "chore: initial commit — existing project"
```

### Step 6: Create GitHub Repository
- Go to [GitHub.com](https://github.com)
- Click **New repository**
- Name: `your-project-name`
- **Do NOT check** "Add README" (recommended)
- Create repository and copy the HTTPS URL

### Step 7: Connect and Push to GitHub
```bash
git branch -M main
git remote add origin https://github.com/username/your-project.git
git push -u origin main
```

---

## 🚨 Common Error: Remote Rejected

If you get this error:
```bash
fatal: refusing to merge unrelated histories
```

### Solution 1: Allow Unrelated Histories
```bash
git pull origin main --allow-unrelated-histories
# Resolve any conflicts if they appear
git add .
git commit -m "merge remote changes"
git push origin main
```

### Solution 2: Use Rebase (Safer)
```bash
git pull origin main --rebase
# Resolve conflicts and continue
git rebase --continue
git push origin main
```

---

## 📥 Scenario B - GitHub → VS Code

### Step 1: Clone Repository
```bash
git clone https://github.com/username/repository-name.git
cd repository-name
```

### Step 2: Open in VS Code
```bash
# Using command line:
code .

# Or through VS Code GUI:
# File → Open Folder → Select your project folder
```

### VS Code Git Interface
- **Source Control Panel** (Left sidebar - Git icon)
- **Stage Changes** using the `+` button
- **Commit** with message using the `✓` button
- **Sync Changes** using bottom status bar buttons

> **Recommended Extensions:** 
> - **GitLens** - Enhanced Git history and blame annotations
> - **GitHub Pull Requests** - Manage PRs directly in VS Code

---

## 🌿 Branching & Pull Requests

### Create Feature Branch
```bash
git checkout -b feature/add-new-feature
```

### Work on Your Feature
```bash
# Make your changes, then:
git add .
git commit -m "feat: add new feature description"
```

### Push Branch and Create PR
```bash
git push -u origin feature/add-new-feature
```

### GitHub Pull Request Process
1. Go to your repository on GitHub
2. Click **Compare & pull request**
3. Add description and create PR
4. After review, merge into `main`
5. (Optional) Delete the feature branch

---

## ⚔️ Conflict Resolution

When conflicts occur, you'll see:

```plaintext
<<<<<<< HEAD
Your local changes
=======
Remote changes from GitHub
>>>>>>> branch-name
```

### Resolution Steps:
1. **Open the file** in VS Code
2. **Choose which changes** to keep (local, remote, or both)
3. **Remove conflict markers** (`<<<<<<<`, `=======`, `>>>>>>>`)
4. **Save the file**
5. **Stage and commit** the resolved file

```bash
git add conflicted-file.txt
git commit -m "fix: resolve merge conflict in conflicted-file.txt"
git push
```

---

## 🔐 Authentication: SSH vs HTTPS

### 🔑 HTTPS (Simple)
- First-time push will ask for username/password
- Use **Personal Access Token** (PAT) instead of password
- Credentials are saved by Git Credential Manager

### 🚀 SSH (Recommended - More Secure)

#### Generate SSH Key:
```bash
ssh-keygen -t ed25519 -C "youremail@example.com"
# Press Enter for default location
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

#### Add to GitHub:
1. Copy public key: `cat ~/.ssh/id_ed25519.pub`
2. Go to GitHub → Settings → SSH and GPG keys
3. Click **New SSH key**
4. Paste your public key

#### Switch Remote URL to SSH:
```bash
git remote set-url origin git@github.com:username/repository.git
```

---

## 💡 Essential Commands Quick Reference

### Basic Workflow
```bash
git status               # Check current changes
git add .                # Stage all files
git add filename.txt     # Stage specific file
git commit -m "message"  # Commit with message
git push                 # Push to remote
git pull                 # Pull latest changes
```

### Branch Management
```bash
git branch               # List all branches
git checkout branch-name # Switch branch
git checkout -b new-branch # Create and switch to new branch
git merge branch-name    # Merge branch into current
```

### History & Differences
```bash
git log --oneline        # Compact commit history
git diff                 # Show unstaged changes
git diff --staged        # Show staged changes
```

### Utility Commands
```bash
git stash                # Temporarily save changes
git stash pop            # Restore stashed changes
git revert commit-hash   # Safe undo (creates new commit)
git reset --hard HEAD~1  # Destructive undo (use carefully!)
```

---

## 🏆 Best Practices for Beginners

### ✅ Commit Convention
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `style:` - Code style changes
- `refactor:` - Code refactoring

### ✅ File Management
- Always use `.gitignore`
- Never commit `node_modules/`, `.env`, or build folders
- Keep commits small and focused

### ✅ Branch Strategy
- Keep `main` branch always stable
- Use feature branches: `feature/description`
- Regularly pull changes: `git pull origin main`

### ✅ Security
- **Never commit** API keys, passwords, or secrets
- Use environment variables (`.env` file)
- Add `.env` to `.gitignore`

---

## ⚡ Quick Start Examples

### One-Shot Setup (New Project)
```bash
cd /path/to/your-project
git init
echo "node_modules/" > .gitignore
git add .
git commit -m "chore: initial commit"
git branch -M main
git remote add origin https://github.com/username/repo.git
git push -u origin main
```

### Daily Workflow
```bash
# Start your day:
git pull origin main

# After making changes:
git add .
git commit -m "feat: describe your changes"
git push
```

### Feature Development
```bash
# Create feature branch:
git checkout -b feature/your-feature

# After completing work:
git push -u origin feature/your-feature
# Then create PR on GitHub
```

---

## 🎯 Practice Exercise

Follow these steps to practice:

1. **Setup**: Navigate to your project folder in terminal
2. **Initialize**: Run the one-shot setup commands above
3. **Verify**: Check your repository on GitHub
4. **Clone**: Clone the repo in a different folder: `git clone https://github.com/username/repo.git`
5. **Modify**: Open in VS Code (`code .`), make a small change
6. **Commit**: Use VS Code Source Control to commit and push
7. **Verify**: Check GitHub to see your changes

---

## 🎪 Super-Short Cheat Sheet

### Initial Setup & First Push
```bash
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin <repository-url>
git push -u origin main
```

### Daily Development
```bash
git pull
git add .
git commit -m "meaningful message"
git push
```

### Branch Workflow
```bash
git checkout -b feature/description
# ... work on feature ...
git push -u origin feature/description
# Create PR on GitHub
```

---

## ❓ Need Help?

### Common Issues & Solutions:

1. **Permission Denied**: 
   - Use SSH instead of HTTPS
   - Generate and add SSH key to GitHub

2. **Wrong Credentials**:
   - Update saved credentials in system keychain
   - Use Personal Access Token

3. **Merge Conflicts**:
   - Use VS Code conflict resolver
   - Carefully choose which changes to keep

4. **Wrong Branch**:
   - Check current branch: `git branch`
   - Switch branch: `git checkout main`

---

<div align="center">

## 🎉 Congratulations!

You're now ready to use Git and GitHub like a pro!

**Happy Coding! 🚀**

---

*This guide is maintained with ❤️ for the developer community*

[Report Issue](https://github.com/username/repo/issues) • [Contribute](https://github.com/username/repo/pulls) • [Star](https://github.com/username/repo)

</div>

---

## 📚 Additional Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub Learning Lab](https://lab.github.com/)
- [Visual Git Guide](https://marklodato.github.io/visual-git-guide/)
- [Conventional Commits](https://www.conventionalcommits.org/)
