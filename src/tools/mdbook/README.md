# mdBook Documentation System

## Overview
mdBook is our Rust-based static site generator, powering both the SL-Configurator documentation and this development workflow documentation.

## Key Features
- **Markdown Source**: Write documentation in familiar Markdown syntax
- **Static Generation**: Fast, secure static site output
- **Rust Integration**: Native Rust toolchain integration
- **Responsive Design**: Mobile-friendly documentation sites
- **Search Integration**: Built-in search functionality
- **GitHub Integration**: Seamless CI/CD with GitHub Actions

## Our Implementation
### Projects Using mdBook
- **SL-Configurator-Docs**: German technical documentation (11 sections, 100+ pages)
- **Development-Workflow-Docs**: This comprehensive development reference

### Configuration
- **Theme**: Custom styling with PragmataPro font integration
- **Navigation**: Hierarchical SUMMARY.md structure
- **Assets**: Co-located images and resources
- **Deployment**: Automated GitHub Pages publishing

## Workflow Integration
- **Content Creation**: Primary documentation authoring system
- **Local Development**: Live preview with `mdbook serve`
- **Version Control**: Git-based content management
- **Deployment**: Automated publishing via GitHub Actions
- **Collaboration**: Multi-contributor documentation workflow

## Usage Patterns
### Daily Development
```bash
cd project-docs
mdbook serve --open    # Live preview
mdbook build          # Production build
mdbook clean          # Clean build artifacts
```

### Content Organization
- **Hierarchical Structure**: Numbered directories for logical flow
- **Cross-references**: Internal linking between sections
- **Asset Management**: Images alongside content files
- **Multi-language**: Support for localized documentation

## Technical Architecture
- **Source**: `src/` directory with Markdown files
- **Configuration**: `book.toml` for site settings
- **Output**: `book/` directory with generated HTML
- **Themes**: Customizable CSS and JavaScript
- **Plugins**: Extensible with Rust-based preprocessors

## Best Practices
- **File Organization**: Clear, numbered directory structure
- **Link Management**: Relative paths for portability
- **Image Optimization**: Compressed images for performance
- **Content Quality**: Consistent formatting and style
- **Version Control**: Exclude build directories from Git