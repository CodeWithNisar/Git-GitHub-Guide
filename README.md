# Git & GitHub Complete Guide

Ek beginner-friendly, step-by-step guide Git aur GitHub use karne ke liye. Do scenarios cover kiye gaye hain: **(1) Local folder ko GitHub pe push karna** aur **(2) GitHub repo clone karke VS Code mein open karna**.

---

## 🚀 Quick Checklist (Start karne se pehle)

- [ ] Git installed? (check: `git --version`)
- [ ] VS Code installed?
- [ ] GitHub account ready & logged in?
- [ ] (Optional) `code` command VS Code mein enable (VS Code → Command Palette → "Shell Command: Install 'code' command in PATH")

---

## 1️⃣ Basic Setup (Ek baar karna hota hai)

Agar abhi tak nahi kiya:

```bash
git --version                       # git installed check
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

`--global` ek hi system par permanent hota hai. Agar kisi specific project ke liye alag naam chahiye to us folder mein `git config user.name "Different"` use karo.

---

## 2️⃣ Scenario A - Local Folder → GitHub Push Karna

### Step A1 - Folder mein jao
```bash
cd /path/to/my-project
```

### Step A2 - Check karo agar `.git` pehle se hai
```bash
ls -la        # Mac/Linux
dir /a        # Windows PowerShell
# agar .git visible na ho, to:
git status    # agar "not a git repository" aata hai to init karna hai
```

### Step A3 - Git initialize karo
```bash
git init
```

> **Note:** Agar `.git` pehle se hai to `git init` dobara chalane se koi nuksan nahi - safe hai.

### Step A4 - .gitignore banayo
Create `.gitignore` in project root:
```
node_modules/
.DS_Store
.vscode/
dist/
*.log
```

### Step A5 - Files stage & commit karo
```bash
git add .
git commit -m "chore: initial commit — existing project"
```

### Step A6 - GitHub pe naya repo banayo
- GitHub.com → **New repository**
- Name: `my-project`
- **Do not** check "Add README" (recommended)
- Create repository → copy HTTPS URL (e.g. `https://github.com/username/my-project.git`)

### Step A7 - Local repo ko remote se connect karo & push karo
```bash
git branch -M main
git remote add origin https://github.com/username/my-project.git
git push -u origin main
```

---

### 🔧 Common Error: Remote Rejected / Non-Fast-Forward

**Error:**
```
fatal: refusing to merge unrelated histories
```

**Solution:**
```bash
git pull origin main --allow-unrelated-histories
# conflicts solve karo agar aaye
git add .
git commit -m "merge remote changes"
git push origin main
```

**Ya safer way:**
```bash
git pull origin main --rebase
# conflict resolve -> git rebase --continue
git push origin main
```

---

## 3️⃣ Scenario B - GitHub Repo → VS Code Mein Open Karna

### Step B1 - Clone the repo
```bash
git clone https://github.com/username/my-project.git
cd my-project
```

### Step B2 - Open in VS Code
**CLI se:**
```bash
code .
```

**VS Code GUI se:** File → Open Folder → select `my-project`

### VS Code Mein Git Use Karna (UI)
- VS Code left side "Source Control" icon (git icon) pe jao
- Changes dikhenge - `+` se stage karo, message likho → tick (✔) se commit karo
- Bottom status bar mein branch name aur sync/push/pull buttons dikhte hain

> **Recommended extensions:** **GitLens** (history + blame), **GitHub Pull Requests and Issues** (PRs ke liye)

---

## 4️⃣ Branching, Feature Workflow & Pull Request

### Basic Branch Workflow
```bash
# 1. New branch banayo
git checkout -b feature/add-contact

# 2. Kaam karo → commit karo
git add .
git commit -m "feat: add contact section"

# 3. Branch push karo
git push -u origin feature/add-contact
```

### GitHub Pe PR Banana
1. GitHub pe jao → repo → **Compare & pull request**
2. Create Pull Request → Review → Merge into `main`
3. Delete branch (optional)

---

## 5️⃣ Conflicts Kaise Resolve Karen

### Step-by-Step Conflict Resolution
1. Jab `git pull` ya `merge` ke dauran conflict aaye:
```plaintext
<<<<<<< HEAD
your local changes
=======
remote changes
>>>>>>> branch-name
```

2. VS Code mein file khol kar decide karo - remote/local ya dono ko combine karo
3. Markers hatao, file save karo
4. Stage karo & commit:
```bash
git add conflicted-file.txt
git commit -m "fix: resolve merge conflict in conflicted-file.txt"
git push
```

---

## 6️⃣ SSH vs HTTPS Authentication

### HTTPS (Simple)
- Jab `git push` karoge, agar pehli baar ho to username/password ya Personal Access Token (PAT) poocha ja sakta hai
- Windows/Mac mein Git Credential Manager usually credentials save kar deta hai

### SSH (Recommended - Once and for all)
**Generate SSH key:**
```bash
ssh-keygen -t ed25519 -C "youremail@example.com"
# default location press Enter
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Copy public key and add to GitHub (Settings → SSH and GPG keys → New SSH key). Public key location: `~/.ssh/id_ed25519.pub`

**Switch remote to SSH:**
```bash
git remote set-url origin git@github.com:username/my-project.git
git push
```

---

## 7️⃣ Useful Commands Explained

### Basic Commands
```bash
git status               # kya changes hain
git add <file>           # stage a file
git add .                # stage sab
git commit -m "msg"      # commit with message
git log --oneline        # short history
git diff                 # staged vs unstaged changes
```

### Branching Commands
```bash
git branch               # list branches
git checkout <branch>    # switch branch
git checkout -b new-branch  # create + switch
git merge branch-name    # merge into current branch
```

### Utility Commands
```bash
git stash                # temporary changes save
git stash pop            # stash wapas laao
git revert <commit>      # safe undo (new commit)
git reset --hard HEAD~1  # destructive undo (careful)
```

---

## 8️⃣ Best Practices (Beginners ke liye)

- ✅ **Small commits:** Har commit chhota aur meaningful rakho
- ✅ **Use .gitignore:** node_modules, build files etc. ignore karo
- ✅ **Write README:** Project ka quick description aur run instructions
- ✅ **Branch per work:** `main` ko hamesha stable rakho
- ✅ **Regular sync:** Regularly `git pull` karo
- ✅ **No secrets:** API keys etc. kabhi repo mein na rakho

---

## 9️⃣ Quick Full Example (One-Shot)

Local folder already ready hai to:

```bash
cd /path/to/my-project
git init
echo "node_modules/" > .gitignore
git add .
git commit -m "chore: initial commit"
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

**Agar push error aaye:**
```bash
git pull origin main --allow-unrelated-histories
# fix conflicts if any
git add .
git commit -m "merge remote"
git push origin main
```

---

## 🔟 Practice Exercise

1. Apna existing project folder open karo terminal mein
2. Follow Quick full example commands
3. GitHub pe repo check karo
4. Clone that repo in different folder: `git clone https://github.com/<username>/<repo>.git`
5. VS Code mein `code .` karo → Make small change → Source Control mein commit → Push
6. GitHub pe check karo change reflect hua

---

## 🎯 Super-Short Cheat-Sheet

### Init + First Push
```bash
git init
git add .
git commit -m "initial"
git branch -M main
git remote add origin <url>
git push -u origin main
```

### Day-to-Day Workflow
```bash
git pull
git add .
git commit -m "msg"
git push
```

### Branch Workflow
```bash
git checkout -b feature/x
# after work
git push -u origin feature/x
# create PR on GitHub
```

---

## 📞 Need Help?

Happy Coding! 
