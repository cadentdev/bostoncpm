# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Boston Commercial Property Management (CPM) professional one-page website featuring modern design, comprehensive service information, and automated deployment pipeline.

## Project Status

**COMPLETED** - Full-featured professional website with:
- Modern responsive design
- Comprehensive content integration
- GitHub Actions deployment pipeline
- SEO optimization and staging controls

## Development Workflow

This project uses a **development branch workflow**:

```bash
# Work on development branch
git checkout development

# Local development server
cd dist
python3 -m http.server 8000

# Create PR to deploy to staging
gh pr create --title "Description" --body "Details"

# Merge to main triggers GitHub Pages deployment
```

## Repository Structure

```
/
├── README.md                 - Project documentation
├── CLAUDE.md                - This development guide
├── .gitignore               - Git ignore patterns (includes .DS_Store)
├── .github/workflows/       - GitHub Actions
│   └── deploy.yml          - Auto-deployment to GitHub Pages
├── dist/                   - Production website files
│   ├── index.html          - Complete one-page website
│   ├── styles.css          - Modern CSS with variables
│   ├── script.js           - Interactive functionality
│   ├── robots.txt          - SEO control (currently blocking)
│   └── assets/images/      - Optimized images
└── sources/                - Source materials
    ├── boston_cpm_webpage_text.md - Original content
    ├── bostoncpm_logo*.png         - Logo variations
    ├── site_design.jpg             - Design inspiration
    └── images/                     - Source images
```

## CSS Architecture

**CSS Variables** (centralized in `:root`):
- `--section-spacing: 4rem` - Consistent vertical spacing
- `--primary-blue: #0358b5` - Brand color
- `--primary-blue-hover: #024185` - Hover states

**Key Styling Approaches**:
- Mobile-first responsive design
- CSS Grid and Flexbox layouts
- Font Awesome icons (CDN)
- Google Fonts: Public Sans (headings), Noto Sans (body)

## JavaScript Features

- Smooth scrolling navigation
- Mobile hamburger menu
- Contact form validation
- Scroll-based animations (Intersection Observer)
- Dynamic navigation active states
- Service card hover effects

## Content Structure

**Sections**:
1. **Hero**: Image + overlaid heading, description + CTA below
2. **About**: 2-column with text + building image
3. **Services**: 2x2 grid with detailed service cards + FA icons
4. **Areas**: 2-column with building image + service area list
5. **Contact**: 2-column with contact info/image + form
6. **Footer**: 2-column with service areas + logo, centered menu

## Deployment Pipeline

**Multi-Branch GitHub Pages Deployment** (`.github/workflows/deploy-environments.yml`):
- Triggers on push to `main`, `new-logo`, or `arial-font` branches (auto-deployment)
- Deploys multiple branch versions to subdirectories of same GitHub Pages site
- Pulls content from main, new-logo, and arial branches during build
- Fixes relative paths for subdirectory deployments using sed commands

**Branch Strategy & URLs**:
- `main` - Production deployment → `https://cadentdev.github.io/bostoncpm/`
- `new-logo` - New branding version → `https://cadentdev.github.io/bostoncpm/new-logo/`
- `arial` - Arial font version → `https://cadentdev.github.io/bostoncpm/arial/`
- `development` - Active development work (not auto-deployed)

**Version Index**: `https://cadentdev.github.io/bostoncpm/versions.html` - Styled comparison page

## SEO & Staging

- `robots.txt` currently blocks all indexing (staging mode)
- Semantic HTML structure for accessibility
- Proper meta tags and heading hierarchy
- Clean URLs and fast loading

## Design System

**Colors**:
- Primary: #0358b5 (buttons, icons, accents)
- Hover: #024185 (interactive states)
- Text: #1f2937, #4b5563, #6b7280 (hierarchy)

**Typography**:
- Headings: Public Sans (professional, geometric)
- Body: Noto Sans (readable, comprehensive)

**Spacing**:
- Section padding: 4rem (64px)
- Consistent use of CSS variables

## Common Development Tasks

**Local Development**:
```bash
cd dist && python3 -m http.server 8000
```

**Update Colors Site-wide**:
```css
:root {
    --primary-blue: #newcolor;
}
```

**Deploy Changes**:
1. Work in feature branches (`new-logo`, `arial`, etc.)
2. Create PR with descriptive title/body
3. Merge to `main` to trigger multi-branch deployment
4. Deployment pulls latest from all configured branches automatically

**Add New Branch to Deployment**:
1. Add branch name to `.github/workflows/deploy-environments.yml` trigger list
2. Add corresponding sed commands for relative path fixes
3. Update version index page if desired

## Contact Form Integration

Current: Client-side validation only
Future: Requires backend service for form submission (Netlify Forms, Formspree, etc.)