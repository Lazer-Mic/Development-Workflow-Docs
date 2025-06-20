# Git Setup & Workflow

This guide covers Git configuration, GitHub access, and the essential workflow commands for the documentation project.

## 🔧 Git Configuration

### Initial Setup

```bash
# Configure your identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Configure line ending handling
git config --global core.autocrlf input  # macOS/Linux
git config --global core.autocrlf true   # Windows
```

### Verify Configuration

```bash
# Check your configuration
git config --list

# Verify identity
git config user.name
git config user.email
```

## 🔑 GitHub Access Setup

### SSH Key Setup (Recommended)

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (macOS)
pbcopy < ~/.ssh/id_ed25519.pub

# Copy public key to clipboard (Linux)
cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard

# Copy public key to clipboard (Windows)
clip < ~/.ssh/id_ed25519.pub
```

### Add SSH Key to GitHub

1. Go to GitHub Settings → SSH and GPG keys
2. Click "New SSH key"
3. Paste your public key
4. Give it a descriptive title
5. Click "Add SSH key"

### Test SSH Connection

```bash
ssh -T git@github.com
```

## 📁 Repository Setup

### Clone Repositories

```bash
# Clone main documentation project
git clone git@github.com:Lazer-Mic/SL-Configurator-Docs.git

# Clone workflow documentation (this project)
git clone git@github.com:Lazer-Mic/Development-Workflow-Docs.git

# Navigate to projects directory
cd Projects
```

### Repository Structure

```
Projects/
├── SL-Configurator-Docs/
│   ├── de/                    # German documentation
│   ├── .github/              # GitHub Actions
│   └── README.md
└── Development-Workflow-Docs/
    ├── src/                  # Source files
    ├── book.toml            # Configuration
    └── .github/             # Deployment workflow
```

## 🔄 Basic Git Workflow

### Daily Workflow Commands

```bash
# 1. Check status
git status

# 2. Pull latest changes
git pull origin main

# 3. Make your changes...

# 4. Stage changes
git add .

# 5. Commit with descriptive message
git commit -m "feat: add new documentation section"

# 6. Push to GitHub
git push origin main
```

### Commit Message Guidelines

Use conventional commit format:

```bash
# Feature addition
git commit -m "feat: add new documentation section"

# Bug fix
git commit -m "fix: correct image path in installation guide"

# Documentation update
git commit -m "docs: update README with new instructions"

# Configuration change
git commit -m "config: update mdBook settings"

# Refactoring
git commit -m "refactor: reorganize file structure"
```

### Branch Management

```bash
# Create and switch to new branch
git checkout -b feature/new-section

# Switch between branches
git checkout main
git checkout feature/new-section

# Merge feature branch
git checkout main
git merge feature/new-section

# Delete feature branch
git branch -d feature/new-section
```

## 🚨 Common Issues & Solutions

### Authentication Issues

```bash
# If SSH key not working, check:
ssh-add -l  # List loaded keys
ssh-add ~/.ssh/id_ed25519  # Add key if not loaded

# Test GitHub connection
ssh -T git@github.com
```

### Merge Conflicts

```bash
# Check for conflicts
git status

# Resolve conflicts in editor, then:
git add .
git commit -m "resolve merge conflicts"
```

### Undo Changes

```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Undo staged changes
git reset HEAD

# Undo unstaged changes
git checkout -- .
```

## 📋 Git Workflow Checklist

Before pushing to GitHub:

- [ ] **Check status**: `git status`
- [ ] **Pull latest**: `git pull origin main`
- [ ] **Stage changes**: `git add .`
- [ ] **Write commit message**: Use conventional format
- [ ] **Commit changes**: `git commit -m "message"`
- [ ] **Push to GitHub**: `git push origin main`
- [ ] **Check Actions**: Verify deployment in GitHub Actions

## 🔗 Next Steps

- **[mdBook Setup](mdbook-setup.md)**: Install and configure mdBook
- **[Development Workflow](3-development-workflow/README.md)**: Learn the content creation process
- **[Deployment Process](4-deployment/deployment-process.md)**: Understand the deployment workflow

---

*Git is the foundation of our version control workflow. Master these basics before proceeding.* 