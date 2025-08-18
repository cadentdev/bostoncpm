# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the BostonCPM one-page website project. Currently, the repository contains only a README.md file and is in its initial setup phase.

## Project Status

This is a complete one-page website for Boston Commercial Property Management built with vanilla HTML, CSS, and JavaScript.

## Development Setup

This is a static website that requires no build process. To develop locally:

```bash
# Navigate to the dist folder and start a local development server
cd dist
python3 -m http.server 8000
# or
python -m http.server 8000

# Then open http://localhost:8000 in your browser
```

## Repository Structure

```
/
├── README.md           - Basic project description  
├── CLAUDE.md          - This file
├── dist/              - Production-ready website files
│   ├── index.html     - Main HTML file
│   ├── styles.css     - All CSS styles
│   ├── script.js      - JavaScript functionality
│   └── assets/
│       └── images/
│           ├── bostoncpm_logo.png - Company logo
│           └── hero.jpg           - Hero section image
└── sources/           - Source materials and design assets
    ├── boston_cpm_webpage_text.md - Original content
    ├── bostoncpm_logo.png         - Logo file
    ├── site_design.jpg            - Design inspiration
    └── images/                    - Additional image assets
```

## Website Features

- **Responsive Design**: Mobile-first approach with hamburger menu
- **Smooth Scrolling**: Navigation with smooth scroll to sections
- **Interactive Elements**: Hover effects, form validation, scroll animations
- **Contact Form**: Client-side validation (needs backend integration for submission)
- **SEO Optimized**: Semantic HTML structure and proper meta tags

## Code Architecture

- **HTML**: Semantic structure with sections for hero, about, services, areas, and contact
- **CSS**: Modern CSS with Grid and Flexbox layouts, CSS custom properties for theming
- **JavaScript**: Vanilla JS with event listeners for interactivity, Intersection Observer API for animations

## Customization

- Colors can be modified in the `dist/styles.css` file (primary blue: #2563eb)
- Content is easily editable in the `dist/index.html` file
- Logo and hero image can be replaced in the `dist/assets/images/` folder
- Contact form submission needs server-side integration

## Deployment

The `dist/` folder contains all production-ready files and can be deployed to any static hosting service:
- GitHub Pages
- Netlify
- Vercel
- AWS S3
- Any web server