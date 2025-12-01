# GitHub Complete Getting Started Guide 🚀

## 📖 About This Guide

This comprehensive guide follows a **local-to-remote workflow** - the most practical approach for real-world development. You'll learn to:

✅ **Start locally** - Initialize Git repositories on your machine  
✅ **Work safely** - Set up proper `.gitignore` and security practices  
✅ **Track changes** - Master Git commands for version control  
✅ **Push to GitHub** - Connect your local work to remote repositories  
✅ **Collaborate** - Use branches, pull requests, and team workflows  

**Perfect for:** Developers who want to understand Git/GitHub from the ground up, following industry best practices from day one.

---

## 📋 Phase 1: Prerequisites & Account Setup

### 1. Create GitHub Account
```bash
# Go to: https://github.com
# Click "Sign up"
# Choose username, email, password
# Verify email address
```

### 2. Install Required Tools (macOS)
```bash
# Install Git
brew install git

# Install GitHub CLI
brew install gh

# Verify installations
git --version
gh --version
```

## 🔧 Phase 2: Initial Configuration

### 3. Configure Git Identity
```bash
# Set your name (appears in commits)
git config --global user.name "Your Full Name"

# Set email (MUST match GitHub account email)
git config --global user.email "your.email@example.com"

# Set default branch to main
git config --global init.defaultBranch main

# Verify configuration
git config --list
```

### 4. Authenticate with GitHub
```bash
# Login via GitHub CLI
gh auth login

# Choose options:
# → GitHub.com (not Enterprise)
# → HTTPS protocol
# → Yes to authenticate Git with GitHub credentials
# → Login with web browser (easiest)
```

## 🔐 Phase 3: Personal Access Token (For Advanced Use)

### 5. Create Personal Access Token (Optional but Recommended)
```bash
# Via GitHub CLI (easiest)
gh auth token

# Or manually via web:
# 1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
# 2. Click "Generate new token (classic)"
# 3. Set expiration: 90 days
# 4. Select minimal scopes:
#    ☑️ repo (for private repos)
#    ☑️ workflow (if using GitHub Actions)
#    ☑️ read:org (if in organization)
# 5. Generate token and SAVE IT IMMEDIATELY
```

### 6. Use Token for Authentication
```bash
# If using token instead of gh auth login:
git config --global credential.helper store

# First push will prompt for:
# Username: your-github-username
# Password: paste-your-token-here (NOT your GitHub password)
```

## 📁 Phase 4: Repository Creation Workflow

### Method A: Start with Local Project (Most Common)

### 7. Create Local Repository
```bash
# Navigate to your project folder
cd /path/to/your/project

# Initialize Git repository
git init

# Check repository status
git status
```

### 8. Create .gitignore (CRITICAL FIRST STEP)
```bash
# Create .gitignore file
touch .gitignore

# Edit with essential patterns:
cat > .gitignore << 'EOF'
# Sensitive files
.env
*.env
.env.*
**/secrets.json
**/config/credentials/

# Personal data
data/
*.csv
*.xlsx
*.json
logs/
*.log

# Python
__pycache__/
*.pyc
venv/
.venv/
*.egg-info/

# OS files
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
*.swp
EOF
```

### 9. Stage and Commit Files
```bash
# Check what files will be added
git status

# Add all files (respects .gitignore)
git add .

# Create first commit
git commit -m "Initial commit: Project setup"

# Verify commit was created
git log --oneline
```

### 10. Create GitHub Repository and Push
```bash
# Create private repository and push in one command
gh repo create your-project-name --private --source=. --remote=origin --push

# Or step by step:
# gh repo create your-project-name --private
# git remote add origin https://github.com/username/your-project-name.git
# git push -u origin main
```

### Method B: Start with GitHub Repository

### 11. Clone Existing Repository
```bash
# Clone repository
gh repo clone username/repository-name

# Or with git:
git clone https://github.com/username/repository-name.git

# Navigate to repository
cd repository-name
```

## 🔄 Phase 5: Daily Git Workflow

### 12. Standard Working Commands
```bash
# Check repository status
git status

# Check differences before staging
git diff

# Add specific files
git add file1.py file2.py

# Add all changed files
git add .

# Add all files including new ones
git add -A

# Commit with descriptive message
git commit -m "Add feature: user authentication"

# Push to GitHub
git push origin main

# Pull latest changes from GitHub
git pull origin main
```

### 13. Branch Management
```bash
# Create new branch
git checkout -b feature-branch-name

# Switch between branches
git checkout main
git checkout feature-branch-name

# List all branches
git branch -a

# Merge branch to main
git checkout main
git merge feature-branch-name

# Delete branch after merge
git branch -d feature-branch-name
```

### 14. Repository Management
```bash
# View remote repositories
git remote -v

# Add remote repository
git remote add origin https://github.com/username/repo.git

# Change remote URL
git remote set-url origin https://github.com/username/new-repo.git

# Remove remote
git remote remove origin
```

## 🚨 Phase 6: Security & Best Practices

### 15. Security Checklist Before Every Commit
```bash
# Always check what you're about to commit
git status

# Review changes in files
git diff

# Check ignored files aren't accidentally included
git status --ignored

# Verify .env files are excluded
ls -la | grep env
```

### 16. Essential .gitignore Patterns
```gitignore
# API Keys & Credentials
.env
*.env
.env.*
secrets/
config/credentials/
*_key.json
*_token.txt
*_password.txt

# Database
*.db
*.sqlite
*.sql

# Personal/Customer Data
data/
datasets/
*.csv
*.xlsx
*.json
customer_data/
personal_info/

# Logs & Cache
*.log
logs/
cache/
temp/
tmp/

# Python Specific
__pycache__/
*.py[cod]
*$py.class
*.so
venv/
.venv/
*.egg-info/
dist/
build/

# OS & IDE
.DS_Store
Thumbs.db
.vscode/
.idea/
*.swp
*.swo
*~
```

### 17. Repository Visibility Settings
```bash
# Create private repository (default for sensitive work)
gh repo create project-name --private

# Create public repository
gh repo create project-name --public

# Change repository visibility later
gh repo edit --visibility private
gh repo edit --visibility public
```

## 🔍 Phase 7: Troubleshooting Common Issues

### 18. Authentication Problems
```bash
# Re-authenticate with GitHub CLI
gh auth logout
gh auth login --web

# Check authentication status
gh auth status

# Refresh token
gh auth refresh
```

### 19. Repository Issues
```bash
# Remove accidentally committed sensitive file
git rm --cached sensitive_file.env
git commit -m "Remove sensitive file from tracking"
git push origin main

# Reset to previous commit (CAREFUL!)
git reset --hard HEAD~1

# Undo last commit but keep changes
git reset --soft HEAD~1
```

### 20. Connection Issues
```bash
# Test GitHub connection
ssh -T git@github.com

# Check remote URL
git remote get-url origin

# Fix HTTPS/SSH mismatch
git remote set-url origin https://github.com/username/repo.git
```

## 📚 Phase 8: Advanced Features

### 21. GitHub CLI Advanced Commands
```bash
# View repository information
gh repo view

# Clone repository with specific features
gh repo clone username/repo --clone

# Create pull request
gh pr create --title "Feature description" --body "Detailed description"

# View issues
gh issue list

# Create new issue
gh issue create --title "Bug report" --body "Description"
```

### 22. Useful Git Aliases
```bash
# Set up helpful shortcuts
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.ps push
git config --global alias.pl pull

# Usage:
git st    # instead of git status
git cm -m "message"  # instead of git commit -m "message"
```

## 🎯 Complete Example Workflow

### 23. End-to-End Example
```bash
# 1. Setup (one-time)
git config --global user.name "John Doe"
git config --global user.email "john@company.com"
gh auth login

# 2. Start new project
cd ~/projects/my-new-project
git init

# 3. Create .gitignore FIRST
echo ".env
*.log
__pycache__/" > .gitignore

# 4. Add project files
# ... create your project files ...

# 5. Initial commit
git add .
git commit -m "Initial commit: Project setup"

# 6. Create GitHub repository
gh repo create my-new-project --private --source=. --remote=origin --push

# 7. Verify everything worked
gh repo view
git log --oneline
```

## ⚠️ Critical Security Reminders

### Never Commit These:
- `.env` files with API keys
- Database passwords
- Personal access tokens
- Customer data
- Private configuration files
- SSH private keys
- OAuth secrets

### Always Do This:
1. **Create .gitignore FIRST** before any commits
2. **Use private repositories** for work projects
3. **Review `git status`** before every commit
4. **Use descriptive commit messages**
5. **Test .gitignore** with `git status --ignored`
6. **Rotate tokens** every 90 days
7. **Use minimum required permissions** for tokens

## 📚 Official Documentation Sources

### **Core Git Documentation:**
- **Git Official Documentation:** https://git-scm.com/docs
- **Git Tutorial:** https://git-scm.com/docs/gittutorial
- **Git Reference Manual:** https://git-scm.com/docs/git

### **GitHub Official Documentation:**
- **GitHub Docs:** https://docs.github.com/
- **Getting Started with Git:** https://docs.github.com/en/get-started/getting-started-with-git
- **Set up Git:** https://docs.github.com/en/get-started/getting-started-with-git/set-up-git

### **GitHub CLI Documentation:**
- **GitHub CLI Manual:** https://cli.github.com/manual/
- **GitHub CLI Authentication:** https://cli.github.com/manual/gh_auth_login
- **GitHub CLI Repository Commands:** https://cli.github.com/manual/gh_repo

### **Specific Command Documentation:**

**Authentication & Setup:**
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh
- https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens

**Repository Management:**
- https://docs.github.com/en/repositories/creating-and-managing-repositories
- https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository

**Gitignore Patterns:**
- https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files
- https://github.com/github/gitignore (Official .gitignore templates)

**Branching and Workflow:**
- https://docs.github.com/en/pull-requests/collaborating-with-pull-requests
- https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging

**Security Best Practices:**
- https://docs.github.com/en/code-security/getting-started/securing-your-repository
- https://docs.github.com/en/authentication/keeping-your-account-and-data-secure

---
**🎉 You're now ready for professional Git/GitHub workflows!**