# Deployment Workflow

## Overview
This documents our **actual, production deployment workflow** for the Development Workflow Documentation project. The system automatically builds and deploys mdBook documentation to GitHub Pages using GitHub Actions whenever changes are pushed to the main branch.

**Live Documentation**: https://lazer-mic.github.io/Development-Workflow-Docs/

## Real Deployment Architecture

### Infrastructure Stack
- **Repository**: `Lazer-Mic/Development-Workflow-Docs` (GitHub)
- **Git Remote**: `git@github.com:Lazer-Mic/Development-Workflow-Docs.git` (SSH)
- **Build Tool**: mdBook v0.4.21 (Rust static site generator)
- **Hosting Platform**: GitHub Pages (automatic HTTPS, CDN)
- **Automation**: GitHub Actions (Ubuntu runner)
- **Domain**: GitHub subdomain (`lazer-mic.github.io/Development-Workflow-Docs/`)

### Project Structure
```
/Users/michaelorlando/Projects/2/
├── .github/workflows/deploy.yml    # Actual deployment workflow
├── book.toml                      # mdBook configuration
├── src/                          # Source markdown files
│   ├── SUMMARY.md               # Navigation structure
│   ├── introduction.md          # Landing page
│   ├── languages/               # Programming language docs
│   ├── systems/                 # Development system docs
│   ├── tools/                   # Tool documentation
│   ├── projects/                # Project-specific docs
│   └── workflows/               # Workflow documentation
└── book/                        # Generated output (gitignored)
```

## Actual GitHub Actions Workflow

### Complete Production Workflow File
**File**: `.github/workflows/deploy.yml`
```yaml
name: Deploy Development Workflow Documentation

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup mdBook
        uses: peaceiris/actions-mdbook@v1
        with:
          mdbook-version: '0.4.21'

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Build with mdBook
        run: mdbook build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: book

  # Deployment job
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

### Workflow Breakdown

#### **Trigger Events**
1. **Automatic Deployment**: Every push to `main` branch
2. **Manual Deployment**: Using GitHub Actions "Run workflow" button

#### **Permissions Configuration**
```yaml
permissions:
  contents: read      # Read repository content
  pages: write        # Write to GitHub Pages
  id-token: write     # Generate deployment tokens
```

#### **Concurrency Control**
- **Group**: `"pages"` (only one Pages deployment at a time)
- **Cancel-in-progress**: `false` (let deployments complete)

#### **Two-Job Architecture**
1. **Build Job**: Compiles mdBook → uploads artifact
2. **Deploy Job**: Takes artifact → deploys to GitHub Pages

## Actual mdBook Configuration

### Complete `book.toml` File
```toml
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
auto-hide-menu = false
no-section-label = true
fold.enable = true
fold.level = 0

[output.html.print]
enable = false

[output.html.playground]
editable = false
copyable = false
copy-js = false
line-numbers = false
runnable = false

[output.html.search]
enable = true
limit-results = 30
teaser-word-count = 30
use-boolean-and = true
boost-title = 2
boost-hierarchy = 1
boost-paragraph = 1
expand = true
heading-split-level = 3
prebuild-index = true

[output.html.git]
repository-url = "https://github.com/Lazer-Mic/Development-Workflow-Docs"
repository-icon = "fa-github"
edit-url-template = "https://github.com/Lazer-Mic/Development-Workflow-Docs/edit/main/src/{path}"

additional-css = []
additional-js = []
```

### Configuration Explanation

#### **Book Metadata**
- **Author**: Michael Orlando
- **Source Directory**: `src/` (markdown files)
- **Build Directory**: `book/` (generated HTML)
- **Base URL**: `/Development-Workflow-Docs/` (GitHub Pages subdirectory)

#### **HTML Output Settings**
- **Chapter Numbering**: Disabled (`no-section-label = true`)
- **Menu Behavior**: Always visible (`auto-hide-menu = false`)
- **Collapsible Sections**: Enabled, all collapsed by default (`fold.level = 0`)
- **Print Support**: Disabled (`enable = false`)
- **Code Playground**: Completely disabled (no editing/copying)

#### **Search Configuration**
- **Full-text Search**: Enabled with prebuild index
- **Results Limit**: 30 items
- **Boolean Search**: Enabled (`use-boolean-and = true`)
- **Content Boosting**: Titles (2x), hierarchy (1x), paragraphs (1x)

#### **Git Integration**
- **Edit Links**: Direct to GitHub source files
- **Repository Links**: GitHub icon and links throughout interface
- **No Additional Assets**: Empty CSS/JS arrays (clean setup)

## Deployment Process Flow

### Step-by-Step Deployment

#### **1. Developer Action**
```bash
# Local development
cd /Users/michaelorlando/Projects/2
# Edit markdown files in src/
git add .
git commit -m "feat: update documentation"
git push origin main
```

#### **2. GitHub Actions Trigger**
- Push to `main` branch detected
- Workflow: "Deploy Development Workflow Documentation" starts
- Runner: Fresh Ubuntu environment spins up

#### **3. Build Process**
```bash
# Actions runner executes:
git checkout main                     # Get latest code
mdbook --version                      # v0.4.21 installed
mdbook build                          # Generate static site
# Output: book/ directory with HTML files
```

#### **4. Artifact Management**
- **Upload**: `book/` directory → GitHub Actions artifact
- **Artifact Name**: `github-pages`
- **Retention**: Standard GitHub Actions retention policy

#### **5. Deployment Process**
- **Environment**: `github-pages` (protected environment)
- **URL Generation**: `https://lazer-mic.github.io/Development-Workflow-Docs/`
- **DNS Propagation**: Automatic via GitHub's CDN
- **SSL Certificate**: Automatic HTTPS

#### **6. Verification**
- **Build Status**: Visible in GitHub Actions tab
- **Deploy URL**: Available in workflow output
- **Live Site**: Content immediately available

## Real Performance Metrics

### Typical Build Times
- **Checkout**: ~2-5 seconds
- **mdBook Setup**: ~10-15 seconds
- **Build Process**: ~5-10 seconds (varies with content size)
- **Artifact Upload**: ~5-10 seconds
- **Deployment**: ~30-60 seconds
- **Total Time**: ~1.5-2 minutes per deployment

### Build Efficiency
- **No Caching**: Currently no build caching implemented
- **Clean Builds**: Every deployment is from scratch
- **Artifact Size**: Typically 2-5 MB compressed
- **Bandwidth**: Minimal due to static content

## Current Git Workflow Integration

### Branch Strategy
```bash
# Single branch deployment
main branch → GitHub Pages (production)
# No staging environment currently
```

### Recent Deployment History
```bash
edcf70c feat: set all sections to start collapsed
fcad1d2 fix: restructure navigation for proper collapsible sections  
445c60e fix: correct fold syntax and set level to 1
```

### Commit-to-Live Timeline
1. **Local Commit**: Developer commits changes
2. **Push to GitHub**: `git push origin main`
3. **Action Trigger**: Workflow starts within 10-30 seconds
4. **Build Complete**: ~1-2 minutes after push
5. **Live Update**: Content visible immediately after build

## Local Development Workflow

### Development Commands
```bash
# Navigate to project
cd /Users/michaelorlando/Projects/2

# Start local development server
mdbook serve --open
# Opens: http://localhost:3000
# Auto-reload: Changes trigger browser refresh

# Build locally (same as production)
mdbook build
# Output: book/ directory (gitignored)

# Clean build artifacts
mdbook clean
```

### Local Testing Process
1. **Edit Content**: Modify `.md` files in `src/`
2. **Live Preview**: `mdbook serve --open` for real-time preview
3. **Verify Build**: `mdbook build` to test production build
4. **Commit & Push**: Standard git workflow triggers deployment

## Monitoring & Debugging

### GitHub Actions Monitoring
- **Workflow Status**: GitHub repository → Actions tab
- **Build Logs**: Detailed output for each step
- **Failure Notifications**: Email alerts on build failures
- **Manual Triggers**: "Run workflow" button for manual deployments

### Deployment Verification
- **Live URL**: https://lazer-mic.github.io/Development-Workflow-Docs/
- **Build Status**: Green check marks in commit history
- **GitHub Pages Settings**: Repository → Settings → Pages

### Common Issues & Solutions
```bash
# Build failure due to markdown syntax
# Check: GitHub Actions logs for mdBook errors

# Missing files in deployment
# Verify: All files committed and pushed to main

# Configuration errors
# Check: book.toml syntax and settings

# GitHub Pages not updating
# Check: Repository → Settings → Pages source configuration
```

## Security & Permissions

### Repository Access
- **Repository**: Public (Lazer-Mic/Development-Workflow-Docs)
- **GitHub Actions**: Enabled with standard permissions
- **GitHub Pages**: Public deployment (no authentication required)

### Token Management
- **GITHUB_TOKEN**: Automatic, no manual secrets required
- **Deploy Permissions**: Managed by GitHub Actions environment
- **SSH Access**: Personal SSH key for git operations

### Content Security
- **No Secrets**: No sensitive information in documentation
- **Public Content**: All content intended for public consumption
- **Edit Links**: Direct to public GitHub repository

## Integration Points

### Development Tool Integration
- **Local Editor**: Any markdown editor or IDE
- **Git Client**: Standard git commands or GUI tools
- **Preview**: mdBook local server for development

### External Dependencies
- **mdBook**: Rust-based static site generator
- **GitHub Actions**: Ubuntu runner environment
- **GitHub Pages**: Static hosting and CDN

This represents our **complete, actual deployment setup** - from local development through to live production deployment. Every configuration value, workflow step, and command shown here is exactly what's currently running in production.