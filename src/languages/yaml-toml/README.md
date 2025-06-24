# YAML & TOML in Documentation Workflow

## Overview
YAML and TOML serve as the essential configuration backbone for our mdBook documentation system. Our project uses a focused, minimalist approach with just two key configuration files: `book.toml` for mdBook settings and `deploy.yml` for GitHub Actions automation.

## Our Configuration Architecture
- **TOML**: Exclusively for mdBook configuration (book.toml)
- **YAML**: Exclusively for GitHub Actions CI/CD (deploy.yml)
- **Purpose-Built**: Each file serves one specific, critical function
- **Integration-First**: Configurations designed to work seamlessly together
- **Automation-Focused**: Minimal manual intervention required

## TOML Implementation: mdBook Configuration
### Our Actual book.toml Configuration
```toml
# /Users/michaelorlando/Projects/Development-Workflow-Docs/book.toml
[book]
authors = ["Michael Orlando"]
language = "en"
src = "src"
title = "Development Workflow Documentation"
description = "Comprehensive documentation of development tools, workflows, and best practices for the SL-Configurator documentation project"

[build]
build-dir = "book"

[output.html]
site-url = "/Development-Workflow-Docs/"
git-repository-url = "https://github.com/Lazer-Mic/Development-Workflow-Docs"
git-repository-icon = "fa-github"
edit-url-template = "https://github.com/Lazer-Mic/Development-Workflow-Docs/edit/main/src/{path}"

[output.html.search]
enable = true                    # JavaScript-based full-text search
limit-results = 30              # Maximum search results displayed
teaser-word-count = 30          # Preview text length in results
use-boolean-and = true          # Enable AND/OR search operators
boost-title = 2                 # Title text relevance multiplier
boost-hierarchy = 1             # Section hierarchy relevance
boost-paragraph = 1             # Paragraph text relevance
expand = true                   # Expand search terms
heading-split-level = 3         # Split headings for better indexing
prebuild-index = true           # Pre-generate search index for speed
```

### TOML Configuration Breakdown
#### Book Metadata Section
```toml
[book]
authors = ["Michael Orlando"]    # Creator attribution
language = "en"                  # Content language (English)
src = "src"                      # Source directory path
title = "Development Workflow Documentation"
description = "Comprehensive documentation of development tools, workflows, and best practices for the SL-Configurator documentation project"
```

#### Build Configuration
```toml
[build]
build-dir = "book"              # Output directory name
                                # → Generated files in ./book/
                                # → Matches .gitignore exclusions
```

#### HTML Output Settings
```toml
[output.html]
site-url = "/Development-Workflow-Docs/"  # GitHub Pages subdirectory
git-repository-url = "https://github.com/Lazer-Mic/Development-Workflow-Docs"
git-repository-icon = "fa-github"         # FontAwesome GitHub icon
edit-url-template = "https://github.com/Lazer-Mic/Development-Workflow-Docs/edit/main/src/{path}"
```

#### Advanced Search Configuration
```toml
[output.html.search]
enable = true                    # Enables JavaScript search widget
limit-results = 30              # Caps search results for performance
teaser-word-count = 30          # Preview text length
use-boolean-and = true          # Advanced search: "rust AND mdbook"
boost-title = 2                 # Page titles are 2x more relevant
boost-hierarchy = 1             # Section headings relevance
boost-paragraph = 1             # Body text base relevance
expand = true                   # Auto-expand abbreviated terms
heading-split-level = 3         # Index h1, h2, h3 separately
prebuild-index = true           # Generate search.js at build time
```

## YAML Implementation: GitHub Actions Deployment
### Our Actual deploy.yml Workflow
```yaml
# .github/workflows/deploy.yml
name: Deploy Development Workflow Documentation

on:
  # Triggers: Push to main branch or manual execution
  push:
    branches: ["main"]
  workflow_dispatch:

# Modern GitHub Pages permissions model
permissions:
  contents: read
  pages: write
  id-token: write

# Prevent concurrent deployments
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Build job: Generate static site
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup mdBook
        uses: peaceiris/actions-mdbook@v1
        with:
          mdbook-version: '0.4.21'    # Locked version for consistency

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Build with mdBook
        run: mdbook build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: book                  # Upload generated HTML

  # Deploy job: Publish to GitHub Pages
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### YAML Workflow Analysis
#### Trigger Configuration
```yaml
on:
  push:
    branches: ["main"]             # Auto-deploy on main branch changes
  workflow_dispatch:               # Manual execution via GitHub UI
```

#### Security & Permissions
```yaml
permissions:
  contents: read                   # Read repository files
  pages: write                     # Write to GitHub Pages
  id-token: write                  # OIDC token for authentication

concurrency:
  group: "pages"                   # Group name for concurrency control
  cancel-in-progress: false       # Let running deployments complete
```

#### Build Process
```yaml
jobs:
  build:
    runs-on: ubuntu-latest         # GitHub-hosted runner
    steps:
      - uses: actions/checkout@v4  # Get repository code
      - uses: peaceiris/actions-mdbook@v1  # Install mdBook
        with:
          mdbook-version: '0.4.21' # Exact version for reproducibility
      - run: mdbook build          # Generate static HTML
      - uses: actions/upload-pages-artifact@v3  # Package for deployment
```

#### Deployment Integration
```yaml
  deploy:
    environment:
      name: github-pages           # Deployment environment
      url: ${{ steps.deployment.outputs.page_url }}  # Live site URL
    needs: build                   # Wait for build completion
    steps:
      - uses: actions/deploy-pages@v4  # Deploy to GitHub Pages
```

## Configuration Integration Workflow
### Development Process
```bash
# 1. Edit markdown content in src/
vim src/languages/new-language/README.md

# 2. Test locally (uses book.toml configuration)
mdbook serve --open
# → Loads configuration from book.toml
# → Serves with search enabled
# → Live reload for instant preview

# 3. Commit and push changes
git add src/
git commit -m "Add new language documentation"
git push origin main

# 4. GitHub Actions triggered (uses deploy.yml)
# → Checkout code
# → Setup mdBook v0.4.21
# → Build using book.toml settings
# → Deploy to GitHub Pages
```

### Configuration Maintenance Patterns
```toml
# Common book.toml updates:
# 1. Update description when project scope changes
description = "Updated project description"

# 2. Adjust search result limits for performance
limit-results = 20              # Reduce for faster search

# 3. Modify edit links if repository changes
edit-url-template = "https://github.com/NewOrg/NewRepo/edit/main/src/{path}"
```

```yaml
# Common deploy.yml updates:
# 1. Update mdBook version for new features
mdbook-version: '0.4.22'       # Latest stable release

# 2. Add additional build steps if needed
- name: Run link checker
  run: |
    # Additional validation steps
```

## Practical Configuration Management
### File Locations and Responsibilities
```
Development-Workflow-Docs/
├── book.toml                   # mdBook configuration (TOML)
│                              # Controls: build, search, GitHub integration
├── .github/workflows/
│   └── deploy.yml             # GitHub Actions workflow (YAML)
│                              # Controls: CI/CD, deployment automation
└── src/                       # Content (Markdown)
    └── SUMMARY.md             # Navigation structure
```

### Configuration Change Workflow
```bash
# Modify mdBook settings
vim book.toml                  # Update search settings, URLs, metadata

# Test configuration locally
mdbook build                   # Verify configuration is valid
mdbook serve --open            # Test search and navigation

# Modify deployment workflow
vim .github/workflows/deploy.yml  # Update versions, add steps

# Test deployment
git commit -am "Update configuration"
git push origin main           # Triggers deployment test
```

## Advanced Configuration Patterns
### Search Optimization
```toml
# Performance-focused search configuration
[output.html.search]
enable = true
limit-results = 20             # Faster search response
teaser-word-count = 20         # Shorter previews load faster
use-boolean-and = true         # Precise search results
boost-title = 3                # Prioritize page titles heavily
prebuild-index = true          # Essential for fast search
```

### GitHub Integration Enhancement
```toml
# Enhanced GitHub integration
[output.html]
site-url = "/Development-Workflow-Docs/"
git-repository-url = "https://github.com/Lazer-Mic/Development-Workflow-Docs"
git-repository-icon = "fa-github"
edit-url-template = "https://github.com/Lazer-Mic/Development-Workflow-Docs/edit/main/src/{path}"
# → Every page has "Edit this page" link
# → Seamless contribution workflow
```

### Deployment Reliability
```yaml
# Robust deployment configuration
concurrency:
  group: "pages"
  cancel-in-progress: false    # Prevent deployment conflicts

environment:
  name: github-pages           # Protected environment
  url: ${{ steps.deployment.outputs.page_url }}  # Dynamic URL reference
```

## Learning Journey & Configuration Evolution
### Current Proficiency
- ✅ **mdBook TOML Mastery**: Complete understanding of configuration options
- ✅ **GitHub Actions YAML**: Sophisticated CI/CD workflow implementation
- ✅ **Integration Patterns**: Seamless configuration coordination
- ✅ **Performance Optimization**: Search and build performance tuning

### Configuration Insights Gained
- **Minimalist Approach**: Two focused files vs. complex configuration sprawl
- **Integration-First Design**: Configurations designed to work together
- **Performance Considerations**: Search indexing and build optimization
- **Maintenance Simplicity**: Clear ownership and update patterns

### Areas for Future Enhancement
- 🔄 **Custom Themes**: TOML configuration for custom CSS themes
- 🔄 **Multi-environment Workflows**: YAML workflows for staging/production
- 🔄 **Advanced Search**: Custom search preprocessing and indexing
- 🔄 **Quality Gates**: YAML workflows for content validation

## Real-World Configuration Benefits
### Why This Approach Works
- **Focused Purpose**: Each file has one clear responsibility
- **Easy Maintenance**: Minimal configuration surface area
- **Reliable Automation**: Consistent, predictable builds
- **Fast Performance**: Optimized for documentation workflow
- **Clear Integration**: Obvious how pieces work together

### Configuration Philosophy
```yaml
# Our configuration approach:
Simplicity: Minimal necessary configuration
Reliability: Locked versions and consistent behavior
Performance: Optimized for fast builds and search
Integration: Seamless workflow coordination
Maintainability: Clear patterns and easy updates
```

## Integration with Development Tools
### Primary Configuration Tools
- **Cursor IDE**: TOML/YAML syntax highlighting and validation
- **Git**: Version control for configuration changes
- **GitHub Actions**: Automated workflow execution
- **mdBook**: Configuration consumption and build execution

### Configuration Validation
```bash
# Validate TOML configuration
mdbook build                   # Tests book.toml validity

# Validate YAML workflow
# GitHub Actions validates on push
# Local validation with act (optional):
act -n                         # Dry run of workflows
```

This focused approach to YAML and TOML configuration demonstrates how minimal, purpose-built configuration can power sophisticated documentation workflows with maximum reliability and maintainability.