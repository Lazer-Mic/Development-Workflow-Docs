# mdBook Installation & Setup

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
