# Development Environment Setup

This section covers the complete setup of your development environment for working on the SL-Configurator documentation project.

## 🛠️ Required Tools

### Core Development Tools
- **Git**: Version control system
- **mdBook**: Static site generator (Rust-based)
- **Cursor**: AI-powered code editor
- **Claude AI**: AI assistant for development

### Optional Tools
- **Homebrew**: Package manager (macOS)
- **Rust**: Programming language (for mdBook)
- **Node.js**: JavaScript runtime (if needed)

## 📋 Setup Checklist

- [ ] **Git Setup**: Configure Git and GitHub access
- [ ] **mdBook Installation**: Install and configure mdBook
- [ ] **Cursor Setup**: Configure Cursor IDE
- [ ] **Claude Integration**: Set up Claude AI in Cursor
- [ ] **Repository Cloning**: Clone both documentation projects

## 🔧 System Requirements

### macOS (Recommended)
- macOS 10.15 or later
- Terminal or iTerm2
- Homebrew (for easy package management)

### Windows
- Windows 10 or later
- Git Bash or WSL
- Chocolatey (optional package manager)

### Linux
- Ubuntu 18.04+ or similar
- Standard terminal
- Package manager (apt, yum, etc.)

## 🚀 Quick Setup Commands

### macOS Setup
```bash
# Install Homebrew (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Git
brew install git

# Install Rust (required for mdBook)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Install mdBook
cargo install --version "^0.4" mdbook
```

### Windows Setup
```bash
# Install Chocolatey (if not installed)
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Install Git
choco install git

# Install Rust
winget install Rust.Rust

# Install mdBook
cargo install --version "^0.4" mdbook
```

## 📁 Project Structure

After setup, your development environment should look like this:

```
Projects/
├── SL-Configurator-Docs/          # Main documentation
│   ├── de/                        # German documentation
│   ├── .github/                   # GitHub Actions
│   └── README.md
├── Development-Workflow-Docs/      # This project
│   ├── src/                       # Source files
│   ├── book.toml                  # Configuration
│   └── .github/                   # Deployment workflow
└── .gitignore                     # Global gitignore
```

## 🔗 Next Steps

1. **[Git Setup](git-setup.md)**: Configure Git and GitHub
2. **[mdBook Installation](mdbook-setup.md)**: Install and configure mdBook
3. **[Cursor Setup](cursor-setup.md)**: Configure Cursor IDE
4. **[Claude Integration](claude-setup.md)**: Set up Claude AI

## ❓ Troubleshooting

If you encounter issues during setup:
- Check the specific tool setup pages for detailed instructions
- Ensure all system requirements are met
- Verify network connectivity for downloads
- Check the [Troubleshooting](4-deployment/troubleshooting.md) section

---

*Complete all setup steps before proceeding to the development workflow.* # Git Setup & Workflow

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

*Git is the foundation of our version control workflow. Master these basics before proceeding.* # mdBook Installation & Setup

This guide covers the installation and configuration of mdBook for the documentation project.

## Installation

### macOS/Linux
```bash
# Install Rust first (if not already installed)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Install mdBook
cargo install --version "^0.4" mdBook
```

### Windows
```bash
# Install Rust first
winget install Rust.Rust

# Install mdBook
cargo install --version "^0.4" mdBook
```

## Configuration

The project uses `book.toml` for configuration. Key settings include:

```toml
[book]
authors = ["Michael Orlando"]
language = "en"
src = "src"
title = "Development Workflow Documentation"

[output.html]
git-repository-url = "https://github.com/Lazer-Mic/Development-Workflow-Docs"
git-repository-icon = "fa-github"
```

## Basic Commands

```bash
# Build the documentation
mdbook build

# Serve locally with auto-reload
mdbook serve --open

# Clean build artifacts
mdbook clean
```

## Project Structure

```
src/
├── SUMMARY.md              # Table of contents
├── 1-introduction/         # Project overview
├── 2-tools-setup/          # Development environment
├── 3-development-workflow/ # Content creation
├── 4-deployment/           # Deployment process
└── 5-best-practices/       # Quality guidelines
```

---

*This section will be expanded with more detailed mdBook configuration and usage instructions.*
# Cursor IDE Setup

This guide covers setting up Cursor IDE for the documentation project.

## Installation

Download Cursor from: https://cursor.sh/

## Configuration

### Font Setup
- Install PragmataPro Mono font
- Configure font in Cursor settings

### AI Integration
- Set up Claude AI integration
- Configure AI assistance features

---

*This section will be expanded with detailed Cursor configuration instructions.*
# Claude AI Integration

This guide covers setting up Claude AI for development assistance.

## Setup

### Cursor Integration
- Claude is built into Cursor IDE
- No additional setup required for basic usage

### CLI Setup (Optional)
```bash
# Install Claude CLI
npm install -g @anthropic-ai/claude-code

# Set API key
export ANTHROPIC_API_KEY=your-api-key
```

---

*This section will be expanded with detailed Claude AI usage instructions.*
