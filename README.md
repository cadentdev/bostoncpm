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

## 🚀 Multi-Branch Deployment

This site uses a sophisticated GitHub Actions workflow for deploying multiple branch versions to subdirectories of the same GitHub Pages site:

### Live URLs
- **Production**: https://cadentdev.github.io/bostoncpm/ (main branch)
- **New Logo**: https://cadentdev.github.io/bostoncpm/new-logo/ (compass logo + official colors)
- **Arial Version**: https://cadentdev.github.io/bostoncpm/arial/ (new logo + Arial fonts)
- **Version Index**: https://cadentdev.github.io/bostoncpm/versions.html (comparison page)

### Deployment Strategy
- **Single Workflow**: Only deploys from `main` branch (satisfies GitHub Pages environment protection)
- **Multi-Branch Content**: Pulls content from multiple branches during build
- **Path Fixing**: Automatically corrects relative paths for subdirectory deployments
- **Custom Domain Ready**: Easy to configure with custom domain
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

### Brand Versions
- **Production**: Original branding (main branch)
- **New Logo**: Compass logo with official colors (new-logo branch)
- **Arial Version**: New logo with Arial fonts (arial branch)

### Color System
- **Primary Color**: #0358b5 (CSS variable: `--primary-blue`)
- **Hover Color**: #024185 (CSS variable: `--primary-blue-hover`)
- **Section Spacing**: 4rem (CSS variable: `--section-spacing`)
- **Typography**: Professional font pairing with proper hierarchy

### Logo Colors (New Branding)
- **#1f5ab0** - Deep Royal Blue (main text color)
- **#348fd5** - Sky Blue (lighter blue in the compass/circular element)
- **#f7bd00** - Bright Gold/Sunflower Yellow (in the compass star/center point)
- **#a0a0a0** - Silver Gray (in the "COMMERCIAL PROPERTY MANAGEMENT" text)

### Branch-Specific Features
- **new-logo branch**: SVG favicon, compass logo, official brand colors
- **arial branch**: Same new branding but Arial fonts throughout (vs Public Sans/Noto Sans)

## ⚙️ Technical Implementation

### Multi-Branch Deployment Workflow
The `.github/workflows/deploy-environments.yml` workflow:

1. **Triggers**: Only on push to `main` branch (satisfies GitHub Pages environment protection rules)
2. **Content Sourcing**: Checks out main, new-logo, and arial branches separately
3. **Directory Structure**:
   - Main branch content → root directory
   - Other branches → subdirectories (`/new-logo/`, `/arial/`)
4. **Path Fixing**: Uses sed commands to fix relative paths in subdirectory HTML files:
   - `href="styles.css"` → `href="../styles.css"`
   - `src="assets/"` → `src="../assets/"`
   - `src="script.js"` → `src="../script.js"`
5. **Version Index**: Generates styled comparison page at `/versions.html`

### Key Features
- **Environment Protection Compliant**: Resolves GitHub Pages branch restrictions
- **Automatic Updates**: Any push to main triggers deployment of all branch versions
- **Shared Resources**: CSS, JS, and assets served from root, referenced by subdirectories
- **404 Prevention**: Relative path fixes ensure all resources load correctly

## 📄 License

© 2025 Boston CPM. All rights reserved.
