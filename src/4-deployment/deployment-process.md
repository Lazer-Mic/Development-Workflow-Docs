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
