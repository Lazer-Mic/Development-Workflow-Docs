# Deployment

This section covers the deployment process and GitHub Actions configuration.

## Overview

The documentation is automatically deployed via GitHub Actions to GitHub Pages.

## Deployment Process

1. **Push to GitHub** - Changes are pushed to the main branch
2. **GitHub Actions** - Automated workflow builds the documentation
3. **GitHub Pages** - Built site is deployed to the web

## GitHub Actions Workflow

The deployment workflow:
- Installs Rust and mdBook
- Builds the documentation
- Fixes base href for GitHub Pages
- Deploys to GitHub Pages

## Manual Deployment

```bash
# Build locally
mdbook build

# Deploy manually (if needed)
# The GitHub Actions workflow handles this automatically
```

---

*This section will be expanded with detailed deployment instructions.*
