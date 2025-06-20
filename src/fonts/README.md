# Custom Fonts

This directory is for your custom font files.

## ⚠️ Copyright Notice

**PragmataPro font files are NOT included in this repository due to copyright restrictions.**

- PragmataPro is a commercial font with copyright protection
- Font files should never be committed to public repositories
- This prevents license violations and legal issues

## 🎨 How to Use PragmataPro Locally

### 1. **Add Your Font Files** (Local Only)
Place your PragmataPro font files in this directory (`src/fonts/`):
- `PragmataProVF_liga_09.ttf`
- `PragmataProVF_Italic_liga_09.ttf`
- `PragmataProVF_09.ttf`
- `PragmataProVF_Italic_09.ttf`

### 2. **Enable Font Loading**
Edit `src/theme/book.css` and uncomment the `@font-face` rules:
```css
@font-face {
    font-family: 'PragmataPro';
    src: url('../fonts/PragmataProVF_liga_09.ttf') format('truetype-variations');
    font-weight: 400 900;
    font-style: normal;
    font-display: swap;
}
```

### 3. **Test Locally**
```bash
mdbook build
mdbook serve --open
```

## 🔒 Security Measures

- Font files are in `.gitignore` to prevent accidental commits
- CSS includes fallback fonts for public deployment
- Local development can use PragmataPro, public site uses fallbacks

## 📱 Public Deployment

The live site will use excellent fallback fonts:
- Fira Code (if available)
- Consolas (Windows)
- Monaco (macOS)
- Menlo (macOS)
- Ubuntu Mono (Linux)

## 🎯 Benefits

- **Local Development**: Full PragmataPro experience
- **Public Site**: Professional fallback fonts
- **Copyright Safe**: No font files in repository
- **Legal Compliance**: Respects font licenses

## How to Add Your Custom Font

1. **Copy your font files** to this directory (`src/fonts/`)
   - Supported formats: `.woff2`, `.woff`, `.ttf`, `.otf`
   - Recommended: Use `.woff2` for best performance

2. **Update the CSS file** (`src/theme/custom.css`):
   - Replace `'YourCustomFont'` with your actual font name
   - Update the file paths to match your font files
   - Example:
   ```css
   @font-face {
       font-family: 'PragmataPro';
       src: url('../fonts/PragmataPro-Regular.woff2') format('woff2');
       font-weight: normal;
       font-style: normal;
   }
   ```

3. **Apply the font** in the CSS:
   ```css
   body {
       font-family: 'PragmataPro', -apple-system, BlinkMacSystemFont, sans-serif;
   }
   ```

4. **Build and test**:
   ```bash
   mdbook build
   mdbook serve --open
   ```

## Font File Examples

- `PragmataPro-Regular.woff2`
- `PragmataPro-Bold.woff2`
- `PragmataPro-Italic.woff2`

## Notes

- Font files are automatically copied to the build output
- Use `.woff2` format for best performance and smaller file sizes
- Make sure you have the rights to use the font in your documentation
- Test the font rendering across different browsers 