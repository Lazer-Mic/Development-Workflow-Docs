# Git Version Control System

## Overview
Git serves as our primary version control system, managing all code, documentation, and configuration files across multiple projects and repositories.

## Our Git Configuration
- **Global Settings**: Consistent identity and preferences
- **SSH Authentication**: Secure repository access
- **Branching Strategy**: Feature-based development workflow
- **Commit Standards**: Conventional commit messages
- **Integration**: Seamless IDE and terminal integration

## Git Setup & Configuration
### Global Configuration
```bash
# Identity configuration
git config --global user.name "Michael Orlando"
git config --global user.email "email@example.com"

# Default branch
git config --global init.defaultBranch main

# Editor configuration
git config --global core.editor "cursor --wait"

# Line ending handling (macOS)
git config --global core.autocrlf input

# Push configuration
git config --global push.default simple
```

### SSH Key Management
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "email@example.com"

# Add to SSH agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Copy public key for GitHub
pbcopy < ~/.ssh/id_ed25519.pub
```

## Repository Management
### Repository Structure
```
Project Repository/
├── .git/                      # Git metadata
├── .gitignore                 # Ignored files
├── README.md                  # Project documentation
├── src/                       # Source code
├── docs/                      # Documentation
└── .github/                   # GitHub-specific files
    └── workflows/             # GitHub Actions
```

### Common Operations
```bash
# Repository initialization
git init
git remote add origin git@github.com:user/repo.git

# Daily workflow
git status                     # Check repository status
git add .                      # Stage changes
git commit -m "feat: add new feature"  # Commit changes
git push origin main           # Push to remote

# Branch management
git branch feature-branch      # Create branch
git checkout feature-branch    # Switch branch
git merge feature-branch       # Merge branch
```

## Workflow Integration
### Development Workflow
1. **Feature Development**: Create feature branches
2. **Regular Commits**: Frequent, meaningful commits
3. **Code Review**: Pull request workflow
4. **Integration**: Merge to main branch
5. **Deployment**: Automated via GitHub Actions

### Documentation Workflow
```bash
# Documentation updates
cd project-docs
git add src/
git commit -m "docs: update installation guide"
git push origin main
# Triggers automatic deployment
```

## Branching Strategy
### Branch Types
- **main**: Production-ready code
- **feature/***: New feature development
- **fix/***: Bug fixes
- **docs/***: Documentation updates
- **chore/***: Maintenance tasks

### Branch Workflow
```bash
# Start new feature
git checkout main
git pull origin main
git checkout -b feature/new-functionality

# Development work
git add .
git commit -m "feat: implement new functionality"

# Merge back to main
git checkout main
git merge feature/new-functionality
git push origin main
```

## Commit Standards
### Conventional Commits
```bash
# Format: <type>(<scope>): <description>
git commit -m "feat(auth): add user authentication"
git commit -m "fix(docs): correct installation command"
git commit -m "docs: update README with new features"
git commit -m "chore: update dependencies"
```

### Commit Types
- **feat**: New features
- **fix**: Bug fixes
- **docs**: Documentation changes
- **style**: Code style changes
- **refactor**: Code refactoring
- **test**: Test additions or updates
- **chore**: Maintenance tasks

## Advanced Git Features
### Git Aliases
```bash
# Useful aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
```

### Git Hooks
```bash
# Pre-commit hook example
#!/bin/sh
# .git/hooks/pre-commit
# Run linting before commits
npm run lint
cargo fmt --check
```

## Repository Maintenance
### Regular Maintenance
```bash
# Clean up branches
git branch -d feature-branch    # Delete merged branch
git remote prune origin         # Clean up remote references

# Repository optimization
git gc                          # Garbage collection
git fsck                        # File system check

# View repository statistics
git log --oneline --graph --all # Visual history
git shortlog -sn               # Contributor statistics
```

### Troubleshooting
```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Discard local changes
git checkout -- filename
git reset --hard HEAD

# View changes
git diff                       # Working directory changes
git diff --staged             # Staged changes
git log --oneline -10         # Recent commits
```

## Learning Journey
- **Starting Point**: Basic Git commands from tutorials
- **Current Proficiency**: Advanced workflow management
- **Key Skills**: Branching, merging, conflict resolution
- **Practical Application**: Multi-project version control
- **Future Goals**: Advanced Git features and automation

## Integration with Development Tools
### IDE Integration
- **Cursor**: Built-in Git support with visual diff
- **VS Code**: GitLens extension for enhanced Git features
- **Terminal**: Command-line Git operations
- **GitHub**: Remote repository hosting and collaboration

### Automation Integration
- **GitHub Actions**: Automated workflows triggered by Git events
- **Pre-commit Hooks**: Automated code quality checks
- **Deployment**: Git-based deployment strategies
- **Backup**: Git remotes for code backup and distribution

## Security Best Practices
- **SSH Keys**: Secure authentication method
- **Signed Commits**: GPG signing for commit verification
- **Credential Management**: Secure credential storage
- **Access Control**: Proper repository permissions
- **Sensitive Data**: .gitignore for sensitive files