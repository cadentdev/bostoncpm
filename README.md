# Boston CPM - Commercial Property Management

A professional one-page website for Boston Commercial Property Management, featuring modern design, comprehensive service information, and responsive layout.

## 🌟 Features

- **Modern Design**: Clean, professional layout with hero section, detailed services, and contact form
- **Responsive**: Mobile-first design with hamburger navigation and adaptive layouts
- **Professional Content**: Comprehensive service descriptions and area coverage
- **Interactive Elements**: Font Awesome icons, hover effects, and smooth scrolling
- **SEO Optimized**: Semantic HTML structure and proper meta tags
- **Contact Integration**: Functional contact form with client-side validation

## 🏗️ Project Structure

```
/
├── README.md              - This file
├── CLAUDE.md             - Development guidance for Claude Code
├── .gitignore            - Git ignore patterns
├── dist/                 - Production-ready website files
│   ├── index.html        - Main website
│   ├── styles.css        - All CSS styling
│   ├── script.js         - JavaScript functionality
│   ├── robots.txt        - Search engine directives
│   └── assets/images/    - Optimized images
└── sources/              - Source materials and design assets
```

## 🚀 Deployment

This site uses GitHub Actions for automatic deployment to GitHub Pages:

- **Staging**: Automatically deploys from `main` branch
- **Production files**: Served from `dist/` directory
- **Custom domain**: Ready for custom domain configuration
- **SEO Control**: robots.txt prevents staging indexing

## 🛠️ Development

This project currently has no server side dependencies. To work on this project locally:

```bash
# Navigate to the dist folder
cd dist
```

Then open `index.html` in your browser.

## 📱 Technology Stack

- **HTML5**: Semantic markup structure
- **CSS3**: Modern styling with Grid, Flexbox, and CSS variables
- **Vanilla JavaScript**: Interactive functionality without frameworks
- **Font Awesome**: Professional icon library
- **Google Fonts**: Public Sans (headings) and Noto Sans (body)

## 🎨 Design System

- **Primary Color**: #0358b5 (CSS variable: `--primary-blue`)
- **Hover Color**: #024185 (CSS variable: `--primary-blue-hover`)
- **Section Spacing**: 4rem (CSS variable: `--section-spacing`)
- **Typography**: Professional font pairing with proper hierarchy

## 📄 License

© 2025 Boston CPM. All rights reserved.
