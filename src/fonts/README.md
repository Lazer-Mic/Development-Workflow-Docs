# Custom Fonts

This directory is for your custom font files.

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