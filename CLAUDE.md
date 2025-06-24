# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains **Development Workflow Documentation** - a comprehensive guide documenting development tools, workflows, and best practices for the SL-Configurator documentation project. The project uses mdBook (Rust-based static site generator) and is automatically deployed to GitHub Pages.

**Live Documentation**: https://lazer-mic.github.io/Development-Workflow-Docs/

## Quick Reference

### 📖 Documentation Structure
- **Tools & Setup**: Development environment configuration
- **Languages**: HTML/CSS, JavaScript, Markdown, Python, Rust, YAML/TOML
- **Systems**: Git, GitHub, GitHub Actions, GitHub Pages, macOS, Shell/Zsh
- **Tools**: Claude AI, Cursor, Homebrew, iTerm2, mdBook, Terminal, VS Code
- **Projects**: Automation, SL-Configurator templates
- **Workflows**: Deployment, documentation, learning journey, project management, troubleshooting

## Development Commands

### mdBook Development
```bash
# Navigate to project root
cd Development-Workflow-Docs

# Start development server with auto-reload
mdbook serve --open        # Opens browser at localhost:3000

# Build static site for production
mdbook build

# Clean build artifacts
mdbook clean
```

### Installation Requirements
```bash
# Install mdBook (Rust required)
cargo install --version "^0.4" mdbook

# Or install Rust first if needed
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Architecture Overview

### mdBook Documentation Structure
- **Technology**: mdBook (Rust-based static site generator)
- **Language**: English technical documentation
- **Configuration**: `book.toml` - Main configuration file
- **Content Structure**: 
  - `src/SUMMARY.md` - Table of contents and navigation
  - `src/` - Source markdown files organized by topic
  - `book/` - Generated static site (auto-deployed)
- **Deployment**: GitHub Actions workflow (`.github/workflows/deploy.yml`)
- **Images**: Co-located with markdown files for reliability

### Documentation Hierarchy
1. **Languages**
   - HTML/CSS, JavaScript, Markdown, Python, Rust, YAML/TOML

2. **Systems** 
   - Git, GitHub, GitHub Actions, GitHub Pages, macOS, Shell/Zsh

3. **Tools**
   - Claude AI, Cursor, Homebrew, iTerm2, mdBook, Terminal, VS Code

4. **Projects**
   - Automation, SL-Configurator, Templates

5. **Workflows**
   - Deployment, Documentation, Learning Journey, Project Management, Troubleshooting

## Key Development Patterns

### Content Organization
- **Topic-based Structure**: Content organized by technology/tool categories
- **Co-located Assets**: Images stored alongside markdown files in same directories
- **Cross-references**: Internal links use relative paths between sections
- **Multi-level Navigation**: SUMMARY.md defines nested table of contents structure

### mdBook Configuration
- **Base URL**: Configured for GitHub Pages deployment (`/Development-Workflow-Docs/`)
- **Search**: Prebuild index enabled with boolean search support
- **Git Integration**: Edit links point to GitHub source for easy contributions
- **Responsive Design**: Built-in mobile-responsive theme

### Content Guidelines
- **English Language**: Professional technical English for all documentation
- **Screenshot Documentation**: Extensive use of annotated screenshots
- **Step-by-Step Instructions**: Detailed procedural guidance
- **Consistent Naming**: Kebab-case for directory and file names

## GitHub Actions Deployment

### Automatic Deployment Workflow
```yaml
# Triggers: Push to main branch or manual dispatch
# Build Process:
1. Install Rust and mdBook
2. Build documentation from src/ directory 
3. Fix base href for GitHub Pages
4. Deploy to github-pages environment
```

### Build Configuration
- **Build Directory**: `book/` (excluded from git via .gitignore)
- **Base Path Fixing**: Automated injection of base href for subdirectory deployment
- **Artifact Upload**: Built site uploaded for Pages deployment

## Development Workflow

### Content Updates
1. **Edit Source**: Modify markdown files in `src/` directory
2. **Local Testing**: Run `mdbook serve --open` to preview changes
3. **Image Management**: Place new images in same directory as markdown
4. **Commit & Push**: Changes automatically trigger deployment via GitHub Actions

### Adding New Sections
1. **Create Directory**: Follow topic-based naming convention
2. **Add README.md**: Create main content file in new directory
3. **Update SUMMARY.md**: Add new section to table of contents
4. **Test Locally**: Verify navigation and content before pushing

### Structure Guidelines
- **File Naming**: Use `README.md` for main content in each directory
- **Directory Naming**: Use descriptive names for topics
- **Image Naming**: Descriptive names matching content context
- **Link Format**: Relative paths for internal navigation

## Project Files

### Key Configuration Files
- **`book.toml`** - mdBook configuration and metadata
- **`src/SUMMARY.md`** - Table of contents and navigation structure
- **`.github/workflows/deploy.yml`** - GitHub Actions deployment workflow
- **`.gitignore`** - Excludes build directories and temporary files

## Common Tasks

### Testing Changes Locally
```bash
cd Development-Workflow-Docs
mdbook serve --open    # Auto-reload on file changes
```

### Building for Production
```bash
cd Development-Workflow-Docs
mdbook build          # Output to book/
```

### Adding Images
1. Place image files in the same directory as the markdown file
2. Reference with relative paths: `![Description](./image-name.png)`
3. Use descriptive filenames that match the content context

## File Structure Reference

```
Development-Workflow-Docs/
├── src/                        # Source content
│   ├── SUMMARY.md             # Navigation structure
│   ├── introduction.md        # Project overview
│   ├── languages/             # Programming languages
│   │   ├── html-css/
│   │   ├── javascript/
│   │   ├── markdown/
│   │   ├── python/
│   │   ├── rust/
│   │   └── yaml-toml/
│   ├── systems/               # Development systems
│   │   ├── git/
│   │   ├── github/
│   │   ├── github-actions/
│   │   ├── github-pages/
│   │   ├── macos/
│   │   └── shell-zsh/
│   ├── tools/                 # Development tools
│   │   ├── claude-ai/
│   │   ├── cursor/
│   │   ├── homebrew/
│   │   ├── iterm2/
│   │   ├── mdbook/
│   │   ├── terminal/
│   │   └── vscode/
│   ├── projects/              # Project-specific docs
│   │   ├── automation/
│   │   ├── sl-configurator/
│   │   └── templates/
│   └── workflows/             # Development workflows
│       ├── deployment/
│       ├── documentation/
│       ├── learning-journey/
│       ├── project-management/
│       └── troubleshooting/
├── book.toml                  # mdBook configuration
└── .github/workflows/deploy.yml # Auto-deployment
```

## Content Tags for Quick Reference

**Languages:** HTML, CSS, JavaScript, Markdown, Python, Rust, YAML, TOML  
**Systems:** Git, GitHub, GitHub Actions, GitHub Pages, macOS, Shell, Zsh  
**Tools:** Claude AI, Cursor, Homebrew, iTerm2, mdBook, Terminal, VS Code  
**Projects:** Automation, SL-Configurator, Templates  
**Workflows:** Deployment, Documentation, Learning, Project Management, Troubleshooting

## Testing & Quality Assurance

### Local Testing Commands
```bash
# Test the build process
mdbook build

# Check for broken links (if linkcheck is installed)
mdbook test

# Serve with specific port
mdbook serve --port 3001

# Build with verbose output
mdbook build --verbose
```

### Content Quality Guidelines
- **Consistency**: Use consistent formatting and terminology
- **Accuracy**: Verify all commands and code examples work
- **Completeness**: Include all necessary steps and context
- **Clarity**: Write for different skill levels and backgrounds
- **Images**: Use high-quality screenshots with clear annotations

## Troubleshooting Common Issues

### Build Failures
- Check `book.toml` syntax and configuration
- Verify all referenced images exist
- Ensure SUMMARY.md matches actual file structure
- Check for broken internal links

### Deployment Issues
- Verify GitHub Actions workflow permissions
- Check GitHub Pages settings in repository
- Ensure base URL configuration is correct
- Review build logs for specific errors

### Local Development Issues
- Confirm Rust and mdBook are properly installed
- Check file permissions and directory structure
- Verify port availability for local server
- Clear browser cache if changes don't appear