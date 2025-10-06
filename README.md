# Git & GitHub Complete Guide

<div align="center">

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white)

**Ek beginner-friendly, step-by-step guide Git aur GitHub use karne ke liye**

[Quick Start](#-quick-start) • [Scenarios](#-scenarios) • [Commands](#-commands) • [Troubleshooting](#-troubleshooting)

</div>

---

## 🎯 Quick Checklist

<div class="checklist">

- [ ] **Git installed?** → `git --version`
- [ ] **VS Code installed?**
- [ ] **GitHub account ready?**
- [ ] **`code` command enabled?** (VS Code Command Palette)

</div>

---

## 🚀 Quick Start

### Basic Setup (Ek baar karna hai)
```bash
# Git installation check
git --version

# Global configuration
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

---

## 📁 Scenario A: Local Folder → GitHub

<div class="scenario-card">

### 🔹 Step 1: Project Folder Mein Jao
```bash
cd /path/to/your-project
```

### 🔹 Step 2: Git Initialize Karo
```bash
git init
```

### 🔹 Step 3: .gitignore Banayo
```bash
# .gitignore file content
node_modules/
.DS_Store
.vscode/
dist/
*.log
```

### 🔹 Step 4: Files Commit Karo
```bash
git add .
git commit -m "chore: initial commit"
```

### 🔹 Step 5: GitHub Repository Banayo
- GitHub.com → New Repository
- Name: `your-project`
- **Don't check** "Add README"

### 🔹 Step 6: Push to GitHub
```bash
git branch -M main
git remote add origin https://github.com/username/repo.git
git push -u origin main
```

</div>

---

## 📥 Scenario B: GitHub → VS Code

<div class="scenario-card">

### 🔹 Step 1: Repository Clone Karo
```bash
git clone https://github.com/username/repo.git
cd repo
```

### 🔹 Step 2: VS Code Mein Open Karo
```bash
code .
```

### 🔹 VS Code Git Features
- **Source Control Panel** (Left sidebar)
- **Stage Changes** (+) button
- **Commit** (✓) with message
- **Sync Changes** (Bottom status bar)

</div>

---

## 🛠 Common Commands

### 🔧 Basic Workflow
```bash
git status              # Changes dekho
git add .               # Saare files stage karo
git commit -m "message" # Commit karo
git push                # GitHub pe push karo
```

### 🌿 Branching
```bash
git checkout -b feature/new-feature    # Naya branch
git push -u origin feature/new-feature # Branch push karo
git merge branch-name                  # Branch merge karo
```

### ⚡ Utility Commands
```bash
git log --oneline        # Commit history
git diff                 # Changes compare karo
git stash                # Temporary save
git stash pop            # Saved changes wapas lao
```

---

## 🚨 Common Errors & Solutions

### ❌ Error: "unrelated histories"
```bash
git pull origin main --allow-unrelated-histories
git add .
git commit -m "merge remote changes"
git push origin main
```

### ❌ Error: "non-fast-forward"
```bash
git pull origin main --rebase
# Conflicts resolve karo
git rebase --continue
git push origin main
```

---

## 🔐 Authentication: SSH vs HTTPS

### 🔑 SSH Setup (Recommended)
```bash
# SSH key generate karo
ssh-keygen -t ed25519 -C "youremail@example.com"

# SSH agent start karo
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# GitHub pe public key add karo
cat ~/.ssh/id_ed25519.pub
```

### 🔗 Remote URL Change to SSH
```bash
git remote set-url origin git@github.com:username/repo.git
```

---

## 📋 Best Practices

<div class="best-practices">

### ✅ Commit Messages
- `feat: add login form`
- `fix: button alignment`
- `docs: update README`

### ✅ File Management
- Use `.gitignore`
- Don't commit `node_modules/`
- Keep secrets in `.env`

### ✅ Branch Strategy
- `main` branch always stable
- Feature branches: `feature/name`
- Regular `git pull`

</div>

---

## ⚡ Quick Reference

### 🎯 One-Shot Setup
```bash
cd /project
git init
echo "node_modules/" > .gitignore
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/user/repo.git
git push -u origin main
```

### 🔄 Daily Workflow
```bash
git pull
git add .
git commit -m "update"
git push
```

---

## 🎓 Practice Exercise

1. **Local project** setup karo
2. **GitHub repository** banayo
3. **Code push** karo
4. **Clone** in different folder
5. **Changes** karo aur **push** karo

---

<div align="center">

## 🎉 Congratulations!

**Ab tum Git aur GitHub use kar sakte ho!**

[Report Issue](https://github.com/username/repo/issues) • [Contribute](https://github.com/username/repo/pulls)

**Made with ❤️ for beginners**

</div>

---

## 📞 Need Help?

Agar koi problem ho to:
1. **Check common errors** section
2. **Google the error message**
3. **Stack Overflow** pe search karo
4. **Git documentation** padho

---
