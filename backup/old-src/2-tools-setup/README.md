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

```text
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

## Git Setup & Workflow

### Git Configuration

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

### GitHub Access Setup

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (macOS)
pbcopy < ~/.ssh/id_ed25519.pub
```

### Repository Setup

```bash
# Clone main documentation project
git clone git@github.com:Lazer-Mic/SL-Configurator-Docs.git

# Clone workflow documentation (this project)
git clone git@github.com:Lazer-Mic/Development-Workflow-Docs.git
```

## mdBook Installation & Setup

### Installation

```bash
# Install Rust first (if not already installed)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Install mdBook
cargo install --version "^0.4" mdbook
```

### Basic Commands

```bash
# Build the documentation
mdbook build

# Serve locally with auto-reload
mdbook serve --open

# Clean build artifacts
mdbook clean
```

## Cursor IDE Setup

### Installation

Download Cursor from: https://cursor.sh/

### Configuration

- Install PragmataPro Mono font
- Configure font in Cursor settings
- Set up Claude AI integration

## Claude AI Integration

### Setup

- Claude is built into Cursor IDE
- No additional setup required for basic usage

### CLI Setup (Optional)

```bash
# Install Claude CLI
npm install -g @anthropic-ai/claude-code

# Set API key
export ANTHROPIC_API_KEY=your-api-key
```

## ❓ Troubleshooting

If you encounter issues during setup:
- Check the specific tool setup pages for detailed instructions
- Ensure all system requirements are met
- Verify network connectivity for downloads
- Check the troubleshooting section

---

*Complete all setup steps before proceeding to the development workflow.*
