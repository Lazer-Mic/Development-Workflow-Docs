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

*Complete all setup steps before proceeding to the development workflow.* 