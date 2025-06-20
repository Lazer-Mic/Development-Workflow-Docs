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
# Deployment Process

This guide covers the automated deployment process using GitHub Actions.

## Automated Deployment

The deployment process is fully automated:

1. **Push to GitHub** - Changes trigger GitHub Actions
2. **Build Process** - mdBook builds the documentation
3. **Deploy to Pages** - Built site deploys to GitHub Pages

## Manual Steps

```bash
# Build locally
mdbook build

# Commit and push
git add .
git commit -m "feat: add new content"
git push origin main
```

## Deployment Timeline

- Build time: ~1-2 minutes
- Deployment time: ~30 seconds
- Total time: ~2-3 minutes

---

*This section will be expanded with detailed deployment procedures.*
# GitHub Pages Configuration

This guide covers GitHub Pages setup and configuration.

## GitHub Pages Setup

GitHub Pages is automatically configured via GitHub Actions:

- **Source**: GitHub Actions
- **Branch**: Not applicable (Actions deployment)
- **Custom domain**: Optional

## Configuration

The workflow automatically:
- Builds the documentation
- Fixes base href for subdirectory deployment
- Deploys to GitHub Pages

## URL Structure

- **Repository**: https://github.com/Lazer-Mic/Development-Workflow-Docs
- **Live site**: https://lazer-mic.github.io/Development-Workflow-Docs/

---

*This section will be expanded with detailed GitHub Pages configuration.*
# Troubleshooting Deployment

This guide covers common deployment issues and solutions.

## Common Issues

### Build Failures
- Check for missing files
- Verify markdown syntax
- Ensure all referenced files exist

### Deployment Failures
- Check GitHub Actions logs
- Verify repository permissions
- Ensure GitHub Pages is enabled

### Local Build Issues
```bash
# Clean and rebuild
mdbook clean
mdbook build
```

## Getting Help

- Check GitHub Actions logs
- Review error messages
- Test locally first
- Check file permissions

---

*This section will be expanded with detailed troubleshooting procedures.*
