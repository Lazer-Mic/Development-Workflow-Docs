# HTML & CSS Development

## Overview
HTML and CSS form the foundation of our documentation systems, providing structure and styling for mdBook-generated sites. Our approach focuses on leveraging mdBook's built-in theming system while maintaining typography consistency across development tools.

## Our Implementation
- **mdBook Built-in Theming**: 5 theme variants (Light, Navy, Coal, Rust, Ayu)
- **CSS Custom Properties**: Systematic design tokens
- **Typography Strategy**: Open Sans + Source Code Pro + PragmataPro integration
- **Responsive Design**: Mobile-first documentation layouts
- **Performance Optimization**: WOFF2 fonts and optimized CSS

## mdBook Theme System
### Built-in Theme Architecture
```
book/css/
├── general.css     # Main content styling
├── chrome.css      # UI chrome and navigation
├── variables.css   # CSS custom properties and themes
└── print.css       # Print-specific styles
```

### CSS Variables Structure
```css
:root {
    --sidebar-target-width: 300px;
    --sidebar-width: min(var(--sidebar-target-width), 80vw);
    --page-padding: 15px;
    --content-max-width: 750px;
    --menu-bar-height: 50px;
    --mono-font: "Source Code Pro", Consolas, "Ubuntu Mono", Menlo, "DejaVu Sans Mono", monospace;
}
```

### Theme Variants
1. **Light** (default) - Clean, bright documentation
2. **Navy** - Professional dark theme
3. **Coal** - High-contrast dark theme  
4. **Rust** - Warm, rust-colored theme
5. **Ayu** - Modern dark theme with blue accents

## Typography System
### Font Stack Implementation
```css
/* Body Text */
font-family: "Open Sans", sans-serif;
/* Weights: 300, 400, 600, 700, 800 */

/* Code/Monospace */
font-family: "Source Code Pro", Consolas, "Ubuntu Mono", Menlo, "DejaVu Sans Mono", monospace;
/* Weight: 500 */

/* Editor Integration (PragmataPro) */
font-family: 'PragmataPro Mono', monospace;
/* Used in: VS Code, Cursor, iTerm2, Terminal */
```

### Font Loading Strategy
- **WOFF2 format** for optimal performance
- **Preload critical fonts** for better UX
- **Fallback stacks** for reliability

## Icon Integration
### FontAwesome 4.7.0
```html
<!-- GitHub integration example -->
git-repository-icon = "fa-github"
```

**Available icons:**
- Navigation icons
- Social media links  
- UI elements
- Status indicators

## Syntax Highlighting
### Multiple Theme Support
```
book/
├── highlight.css        # Base16 Atelier Dune Light
├── tomorrow-night.css   # Dark theme
└── ayu-highlight.css    # Ayu theme variant
```

## Configuration Approach
### book.toml HTML Output Settings
```toml
[output.html]
site-url = "/Development-Workflow-Docs/"
git-repository-url = "https://github.com/Lazer-Mic/Development-Workflow-Docs"
git-repository-icon = "fa-github"
edit-url-template = "https://github.com/Lazer-Mic/Development-Workflow-Docs/edit/main/src/{path}"
```

## Responsive Design Strategy
### Mobile-First Approach
```css
/* Default mobile styles */
.container {
    padding: 1rem;
}

/* Tablet and up */
@media (min-width: 768px) {
    .container {
        padding: 2rem;
        max-width: 1200px;
        margin: 0 auto;
    }
}
```

### Key Breakpoints
- **Mobile**: < 768px
- **Tablet**: 768px - 1024px  
- **Desktop**: > 1024px
- **Wide**: > 1200px

## Performance Optimization
### Font Loading
- **WOFF2 compression** for smaller file sizes
- **Font-display: swap** for better loading UX
- **Selective font weights** to reduce payload

### CSS Organization
- **Component-based structure** for maintainability
- **CSS custom properties** for theme consistency
- **Minimal custom CSS** leveraging mdBook defaults

## Development Workflow
### Local Development
```bash
# Start development server
mdbook serve --open

# Theme testing across variants
# Use theme switcher in top-right corner

# Browser DevTools inspection
# Focus on responsive behavior
```

### Theme Customization
1. **Identify target elements** in browser DevTools
2. **Locate relevant CSS files** in `book/css/`
3. **Test across all theme variants**
4. **Verify responsive behavior**

## Integration Points
### mdBook Configuration
- **HTML output settings** in `book.toml`
- **Search functionality** with styling hooks
- **Edit links** integration with GitHub

### GitHub Pages Deployment
- **Base URL configuration** for subdirectory hosting
- **Asset path resolution** for fonts and images
- **GitHub repository integration** via edit links

## Learning Journey
### Current Proficiency
- ✅ **mdBook theming system** understanding
- ✅ **CSS custom properties** for design tokens
- ✅ **Responsive design** principles
- ✅ **Typography hierarchy** implementation

### Areas for Growth
- 🔄 **Advanced CSS animations** for enhanced UX
- 🔄 **CSS Grid** for complex layouts
- 🔄 **Custom mdBook themes** development
- 🔄 **Performance optimization** techniques

## Tools & Workflow
### Development Tools
- **Browser DevTools** for styling and debugging
- **mdBook serve** for live reload development
- **GitHub Pages** for production deployment
- **Git** for version control of styling changes

### Typography Tools
- **PragmataPro licensing** for editor consistency
- **Google Fonts** for Open Sans variants
- **Font optimization** for web delivery

## Best Practices
### CSS Architecture
- **Leverage mdBook defaults** before customizing
- **Use CSS custom properties** for consistency
- **Test across all theme variants**
- **Maintain responsive design principles**

### Performance
- **Optimize font loading** with appropriate strategies
- **Minimize custom CSS** to reduce maintenance
- **Use efficient selectors** for better performance
- **Test on various devices** and connection speeds