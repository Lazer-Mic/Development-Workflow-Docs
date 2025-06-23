# Automation & Scripts

## Overview
Our automation ecosystem encompasses scripts, tools, and workflows that streamline development processes, reduce manual effort, and ensure consistency across our development environment.

## Automation Philosophy
- **Efficiency First**: Automate repetitive and time-consuming tasks
- **Reliability**: Create robust, error-resistant automation
- **Maintainability**: Write clear, documented, and maintainable scripts
- **Integration**: Seamlessly integrate with existing development tools
- **Continuous Improvement**: Regularly evaluate and enhance automation

## Automation Categories
### Development Environment
```yaml
Environment Automation:
  system-setup:
    description: macOS development environment setup
    scope: Initial system configuration and tool installation
    languages: [bash, python]
    frequency: One-time or new system setup
  
  project-initialization:
    description: New project setup and configuration
    scope: Repository creation, template application, CI/CD setup
    languages: [bash, python, github-cli]
    frequency: Per new project
  
  dependency-management:
    description: Package and dependency updates
    scope: Homebrew, Python, Rust, npm package management
    languages: [bash, python]
    frequency: Weekly/Monthly maintenance
```

### Build & Deployment
```yaml
Build Automation:
  documentation-build:
    description: mdBook build and optimization
    scope: Content compilation, asset optimization, validation
    languages: [bash, rust, python]
    frequency: Every commit/push
  
  deployment-pipeline:
    description: Automated deployment to various targets
    scope: GitHub Pages, staging environments, CDN updates
    languages: [yaml, bash]
    frequency: Continuous deployment
  
  quality-assurance:
    description: Automated testing and validation
    scope: Link checking, content validation, performance testing
    languages: [bash, python, javascript]
    frequency: Pre-deployment
```

### Maintenance & Monitoring
```yaml
Maintenance Automation:
  backup-systems:
    description: Automated backup and archival
    scope: Repository backups, configuration snapshots
    languages: [bash, python]
    frequency: Daily/Weekly
  
  health-monitoring:
    description: System and service health checks
    scope: Site availability, performance metrics, error detection
    languages: [python, bash]
    frequency: Continuous monitoring
  
  cleanup-processes:
    description: Automated cleanup and optimization
    scope: Cache clearing, log rotation, storage optimization
    languages: [bash, python]
    frequency: Regular maintenance cycles
```

## Core Automation Scripts
### System Setup & Configuration
```bash
#!/bin/bash
# system-setup.sh - Complete development environment setup

set -e

echo "🚀 Setting up macOS development environment..."

# Install Xcode Command Line Tools
if ! xcode-select -p &> /dev/null; then
    echo "Installing Xcode Command Line Tools..."
    xcode-select --install
    echo "Please complete Xcode Command Line Tools installation and re-run this script"
    exit 1
fi

# Install Homebrew
if ! command -v brew &> /dev/null; then
    echo "Installing Homebrew..."
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
    eval "$(/opt/homebrew/bin/brew shellenv)"
fi

# Update Homebrew
echo "Updating Homebrew..."
brew update

# Install essential tools
echo "Installing essential development tools..."
brew install git gh curl wget tree jq
brew install python rust node

# Install development applications
echo "Installing development applications..."
brew install --cask cursor iterm2 visual-studio-code

# Install Rust tools
echo "Installing Rust development tools..."
cargo install mdbook
cargo install cargo-watch
cargo install cargo-audit

# Configure Git (if not already configured)
if [ -z "$(git config --global user.name)" ]; then
    read -p "Enter your full name for Git: " git_name
    git config --global user.name "$git_name"
fi

if [ -z "$(git config --global user.email)" ]; then
    read -p "Enter your email for Git: " git_email
    git config --global user.email "$git_email"
fi

# Set up SSH key for GitHub (if not exists)
if [ ! -f ~/.ssh/id_ed25519 ]; then
    echo "Generating SSH key for GitHub..."
    ssh-keygen -t ed25519 -C "$(git config --global user.email)" -f ~/.ssh/id_ed25519 -N ""
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_ed25519
    echo "SSH key generated. Add the following public key to GitHub:"
    cat ~/.ssh/id_ed25519.pub
    echo "Press any key to continue after adding the SSH key to GitHub..."
    read -n 1
fi

# Create project directory structure
echo "Creating project directory structure..."
mkdir -p ~/Projects/{Documentation,Scripts,Templates,Archive}

echo "✅ Development environment setup complete!"
echo ""
echo "Next steps:"
echo "1. Add your SSH key to GitHub if you haven't already"
echo "2. Test GitHub connection: ssh -T git@github.com"
echo "3. Clone your repositories to ~/Projects/"
echo "4. Customize your shell configuration in ~/.zshrc"
```

### Project Initialization Automation
```bash
#!/bin/bash
# project-init.sh - Automated project initialization

PROJECT_NAME="$1"
PROJECT_TYPE="$2"
TEMPLATE_PATH="$3"

if [ $# -lt 2 ]; then
    echo "Usage: $0 <project-name> <project-type> [template-path]"
    echo "Project types: mdbook, python, rust, web"
    exit 1
fi

# Set default template path
TEMPLATE_PATH="${TEMPLATE_PATH:-~/Projects/Templates}"

echo "🚀 Initializing project: $PROJECT_NAME"
echo "📋 Project type: $PROJECT_TYPE"

# Create project from template
if [ -d "$TEMPLATE_PATH/$PROJECT_TYPE" ]; then
    cp -r "$TEMPLATE_PATH/$PROJECT_TYPE" "$PROJECT_NAME"
    cd "$PROJECT_NAME"
    
    # Replace template placeholders
    find . -type f \( -name "*.md" -o -name "*.toml" -o -name "*.yml" -o -name "*.json" \) \
        -exec sed -i "s/{{PROJECT_NAME}}/$PROJECT_NAME/g" {} \;
    find . -type f \( -name "*.md" -o -name "*.toml" -o -name "*.yml" -o -name "*.json" \) \
        -exec sed -i "s/{{AUTHOR_NAME}}/$(git config user.name)/g" {} \;
    find . -type f \( -name "*.md" -o -name "*.toml" -o -name "*.yml" -o -name "*.json" \) \
        -exec sed -i "s/{{AUTHOR_EMAIL}}/$(git config user.email)/g" {} \;
    find . -type f \( -name "*.md" -o -name "*.toml" -o -name "*.yml" -o -name "*.json" \) \
        -exec sed -i "s/{{DATE}}/$(date +%Y-%m-%d)/g" {} \;
else
    echo "❌ Template not found: $TEMPLATE_PATH/$PROJECT_TYPE"
    exit 1
fi

# Initialize Git repository
git init
git add .
git commit -m "feat: initialize $PROJECT_NAME project from $PROJECT_TYPE template"

# Create GitHub repository (if GitHub CLI is available and user confirms)
if command -v gh &> /dev/null; then
    read -p "Create GitHub repository? (y/n): " create_repo
    if [ "$create_repo" = "y" ]; then
        gh repo create "$PROJECT_NAME" --public --source=. --remote=origin --push
        echo "📁 Repository created: https://github.com/$(gh api user --jq .login)/$PROJECT_NAME"
    fi
fi

# Project-specific setup
case "$PROJECT_TYPE" in
    "mdbook")
        echo "📚 Setting up mdBook project..."
        if command -v mdbook &> /dev/null; then
            mdbook build
            echo "🌐 Preview: mdbook serve --open"
        fi
        ;;
    "python")
        echo "🐍 Setting up Python project..."
        python3 -m venv venv
        source venv/bin/activate
        if [ -f "requirements.txt" ]; then
            pip install -r requirements.txt
        fi
        echo "🔧 Activate environment: source venv/bin/activate"
        ;;
    "rust")
        echo "🦀 Setting up Rust project..."
        cargo check
        echo "🔧 Run project: cargo run"
        ;;
esac

echo "✅ Project $PROJECT_NAME initialized successfully!"
echo "📂 Location: $(pwd)"
```

### Deployment Automation
```bash
#!/bin/bash
# deploy.sh - Automated deployment script

PROJECT_TYPE="$1"
ENVIRONMENT="${2:-production}"

echo "🚀 Starting deployment for $PROJECT_TYPE to $ENVIRONMENT..."

# Pre-deployment checks
echo "🔍 Running pre-deployment checks..."

# Check if we're in a git repository
if ! git rev-parse --is-inside-work-tree &> /dev/null; then
    echo "❌ Not in a git repository"
    exit 1
fi

# Check for uncommitted changes
if ! git diff-index --quiet HEAD --; then
    echo "❌ Uncommitted changes detected. Commit changes before deployment."
    exit 1
fi

# Check if we're on the right branch
current_branch=$(git branch --show-current)
if [ "$ENVIRONMENT" = "production" ] && [ "$current_branch" != "main" ]; then
    echo "❌ Production deployments must be from main branch"
    exit 1
fi

# Project-specific deployment
case "$PROJECT_TYPE" in
    "mdbook")
        echo "📚 Deploying mdBook documentation..."
        
        # Build documentation
        echo "🔨 Building documentation..."
        mdbook build
        
        # Test build
        echo "🧪 Testing build..."
        mdbook test
        
        # Deploy to GitHub Pages (if configured)
        if [ -f ".github/workflows/deploy.yml" ]; then
            echo "🌐 Triggering GitHub Actions deployment..."
            git push origin "$current_branch"
        else
            echo "ℹ️  Manual deployment - build complete in book/ directory"
        fi
        ;;
        
    "python")
        echo "🐍 Deploying Python application..."
        
        # Run tests
        echo "🧪 Running tests..."
        if [ -f "requirements-dev.txt" ]; then
            pip install -r requirements-dev.txt
        fi
        python -m pytest tests/ || exit 1
        
        # Deploy based on environment
        case "$ENVIRONMENT" in
            "staging")
                echo "🏗️  Deploying to staging..."
                # Add staging deployment logic
                ;;
            "production")
                echo "🚀 Deploying to production..."
                # Add production deployment logic
                ;;
        esac
        ;;
        
    *)
        echo "❌ Unknown project type: $PROJECT_TYPE"
        exit 1
        ;;
esac

echo "✅ Deployment completed successfully!"
```

## GitHub Actions Integration
### Automated Workflow Templates
```yaml
# .github/workflows/automation.yml
name: Development Automation

on:
  schedule:
    - cron: '0 2 * * 1'  # Weekly on Monday at 2 AM
  workflow_dispatch:

jobs:
  dependency-updates:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Update Homebrew packages
        run: |
          # Create script to update local dependencies
          cat > update-deps.sh << 'EOF'
          #!/bin/bash
          echo "Updating development dependencies..."
          brew update
          brew upgrade
          cargo install-update -a
          pip list --outdated --format=freeze | grep -v '^\-e' | cut -d = -f 1 | xargs -n1 pip install -U
          EOF
          
      - name: Create Pull Request
        uses: peter-evans/create-pull-request@v5
        with:
          title: 'chore: update development dependencies'
          commit-message: 'chore: automated dependency updates'
          branch: 'automated/dependency-updates'
          body: |
            Automated dependency updates:
            - Homebrew packages updated
            - Rust crates updated  
            - Python packages updated
            
            Please review and merge if all checks pass.

  health-check:
    runs-on: ubuntu-latest
    steps:
      - name: Check site availability
        run: |
          sites=(
            "https://lazer-mic.github.io/SL-Configurator-Docs/"
            "https://lazer-mic.github.io/Development-Workflow-Docs/"
          )
          
          for site in "${sites[@]}"; do
            if curl -f -s "$site" > /dev/null; then
              echo "✅ $site is available"
            else
              echo "❌ $site is not available"
              exit 1
            fi
          done

  backup-creation:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
          
      - name: Create backup archive
        run: |
          timestamp=$(date +%Y%m%d-%H%M%S)
          tar -czf "backup-$timestamp.tar.gz" \
            --exclude='.git' \
            --exclude='node_modules' \
            --exclude='target' \
            --exclude='book' \
            .
          
      - name: Upload backup
        uses: actions/upload-artifact@v3
        with:
          name: project-backup
          path: backup-*.tar.gz
          retention-days: 30
```

## Monitoring & Alerting
### Health Check Automation
```python
#!/usr/bin/env python3
# health-check.py - Comprehensive system health monitoring

import requests
import subprocess
import psutil
import json
import smtplib
from datetime import datetime
from email.mime.text import MIMEText
from pathlib import Path

class HealthMonitor:
    def __init__(self, config_file="health-config.json"):
        self.config = self.load_config(config_file)
        self.results = []
    
    def load_config(self, config_file):
        """Load monitoring configuration"""
        default_config = {
            "sites": [
                "https://lazer-mic.github.io/SL-Configurator-Docs/",
                "https://lazer-mic.github.io/Development-Workflow-Docs/"
            ],
            "disk_threshold": 80,
            "memory_threshold": 85,
            "alerts": {
                "email": None,
                "slack_webhook": None
            }
        }
        
        if Path(config_file).exists():
            with open(config_file) as f:
                user_config = json.load(f)
                default_config.update(user_config)
        
        return default_config
    
    def check_website_availability(self):
        """Check if websites are accessible"""
        for site in self.config["sites"]:
            try:
                response = requests.get(site, timeout=10)
                if response.status_code == 200:
                    self.results.append(f"✅ {site} - OK")
                else:
                    self.results.append(f"❌ {site} - HTTP {response.status_code}")
            except requests.RequestException as e:
                self.results.append(f"❌ {site} - Error: {str(e)}")
    
    def check_system_resources(self):
        """Check system resource usage"""
        # Disk usage
        disk_usage = psutil.disk_usage('/')
        disk_percent = (disk_usage.used / disk_usage.total) * 100
        
        if disk_percent > self.config["disk_threshold"]:
            self.results.append(f"⚠️  Disk usage: {disk_percent:.1f}% (threshold: {self.config['disk_threshold']}%)")
        else:
            self.results.append(f"✅ Disk usage: {disk_percent:.1f}%")
        
        # Memory usage
        memory = psutil.virtual_memory()
        if memory.percent > self.config["memory_threshold"]:
            self.results.append(f"⚠️  Memory usage: {memory.percent:.1f}% (threshold: {self.config['memory_threshold']}%)")
        else:
            self.results.append(f"✅ Memory usage: {memory.percent:.1f}%")
    
    def check_development_tools(self):
        """Check if development tools are working"""
        tools = [
            ("git", ["git", "--version"]),
            ("mdbook", ["mdbook", "--version"]),
            ("python", ["python3", "--version"]),
            ("rust", ["rustc", "--version"])
        ]
        
        for name, command in tools:
            try:
                result = subprocess.run(command, capture_output=True, text=True)
                if result.returncode == 0:
                    version = result.stdout.strip().split('\n')[0]
                    self.results.append(f"✅ {name} - {version}")
                else:
                    self.results.append(f"❌ {name} - Command failed")
            except FileNotFoundError:
                self.results.append(f"❌ {name} - Not installed")
    
    def send_alert(self, message):
        """Send alert notification"""
        if self.config["alerts"]["email"]:
            self.send_email_alert(message)
        
        if self.config["alerts"]["slack_webhook"]:
            self.send_slack_alert(message)
    
    def send_email_alert(self, message):
        """Send email alert"""
        # Implementation depends on email configuration
        pass
    
    def send_slack_alert(self, message):
        """Send Slack alert"""
        webhook_url = self.config["alerts"]["slack_webhook"]
        if webhook_url:
            payload = {"text": f"Health Check Alert:\n{message}"}
            requests.post(webhook_url, json=payload)
    
    def run_health_check(self):
        """Run complete health check"""
        print(f"🏥 Running health check at {datetime.now()}")
        
        self.check_website_availability()
        self.check_system_resources()
        self.check_development_tools()
        
        # Print results
        for result in self.results:
            print(result)
        
        # Check for critical issues
        critical_issues = [r for r in self.results if r.startswith("❌")]
        warning_issues = [r for r in self.results if r.startswith("⚠️")]
        
        if critical_issues or warning_issues:
            alert_message = "Health Check Issues Detected:\n" + "\n".join(critical_issues + warning_issues)
            self.send_alert(alert_message)
        
        return len(critical_issues) == 0

if __name__ == "__main__":
    monitor = HealthMonitor()
    success = monitor.run_health_check()
    exit(0 if success else 1)
```

## Maintenance Automation
### Automated Cleanup Scripts
```bash
#!/bin/bash
# cleanup.sh - System and project cleanup automation

echo "🧹 Starting automated cleanup..."

# Clean Homebrew
echo "🍺 Cleaning Homebrew..."
brew cleanup
brew autoremove
brew doctor

# Clean Rust artifacts
echo "🦀 Cleaning Rust build artifacts..."
find ~/Projects -name "target" -type d -exec cargo clean --manifest-path {}/.. \; 2>/dev/null || true

# Clean Python cache
echo "🐍 Cleaning Python cache files..."
find ~/Projects -name "__pycache__" -type d -exec rm -rf {} + 2>/dev/null || true
find ~/Projects -name "*.pyc" -delete 2>/dev/null || true

# Clean mdBook build artifacts
echo "📚 Cleaning mdBook build artifacts..."
find ~/Projects -name "book" -type d -path "*/src/*" -prune -o -name "book" -type d -exec rm -rf {} + 2>/dev/null || true

# Clean macOS system cache
echo "🍎 Cleaning macOS caches..."
sudo periodic daily weekly monthly

# Clean Docker (if installed)
if command -v docker &> /dev/null; then
    echo "🐳 Cleaning Docker..."
    docker system prune -f
fi

# Disk usage report
echo "💾 Current disk usage:"
df -h /

echo "✅ Cleanup completed!"
```

## Future Automation Enhancements
### Planned Improvements
```yaml
Automation Roadmap:
  intelligent-monitoring:
    description: AI-powered anomaly detection
    timeline: Q2 2024
    features:
      - Machine learning-based performance monitoring
      - Predictive maintenance alerts
      - Automated optimization suggestions
  
  cross-platform-support:
    description: Windows and Linux automation support
    timeline: Q3 2024
    features:
      - Platform-agnostic scripts
      - Containerized automation environments
      - Cloud-based automation runners
  
  advanced-integration:
    description: Enhanced tool integration
    timeline: Q4 2024
    features:
      - API-driven automation
      - Webhook-based triggers
      - Multi-service orchestration
```

### Integration Opportunities
- **CI/CD Enhancement**: More sophisticated pipeline automation
- **Security Automation**: Automated security scanning and updates
- **Performance Optimization**: Automated performance testing and optimization
- **Documentation Generation**: Automated documentation updates from code changes
- **Backup & Recovery**: Enhanced backup strategies with automated recovery testing