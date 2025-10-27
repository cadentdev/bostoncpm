# Hero Image Redesign - Implementation Plan

**Document Version:** 1.0
**Created:** 2025-10-27
**Project:** Boston CPM Website
**Branch:** development

---

## Executive Summary

This document provides a detailed, step-by-step implementation plan to redesign the hero section of the Boston CPM website. The redesign will transform the hero image to full-width edge-to-edge display, add an ombre gradient overlay, and reposition the H1 heading to the bottom center of the image with enhanced styling.

---

## Requirements Analysis

### Explicit Requirements
1. Make hero image go edge to edge (full width of viewport)
2. Add ombre (shadow gradient) effect covering 30% of bottom of image
3. Gradient transitions from dark (bottom) to transparent (top)
4. Move H1 text "Commercial Property Management" from upper right to bottom center
5. Remove the containing rectangle/box around the text
6. Make text white and bold (font-weight: 800)
7. Maintain current height and aspect ratio of the image
8. Tuck the top of the image under the translucent main menu bar

### Implicit Requirements
- Maintain responsive design for mobile devices
- Ensure text readability over the gradient
- Preserve accessibility (semantic HTML)
- Maintain smooth visual transition with rest of site
- Keep existing navigation behavior unchanged

---

## Current State Analysis

### HTML Structure (Lines 44-52 in /Users/neil/Repos/cadentdev/bostoncpm/dist/index.html)

```html
<!-- Hero Section -->
<section class="hero">
    <div class="hero-image-container">
        <img src="assets/images/hero.jpg" alt="Professional woman working on laptop">
        <div class="hero-overlay">
            <h1>Commercial Property Management</h1>
        </div>
    </div>
</section>
```

**Current Structure:**
- `.hero` section wrapper with max-width: 1200px and horizontal padding
- `.hero-image-container` wrapper for image + overlay
- Hero image with border-radius and box-shadow
- `.hero-overlay` positioned absolutely at top-right with dark background box

### CSS Current State (Lines 182-223 in /Users/neil/Repos/cadentdev/bostoncpm/dist/styles.css)

**Section Container (`.hero`):**
```css
.hero {
    padding: 40px 0 50px;
    max-width: 1200px;          /* Limits width - NEEDS REMOVAL */
    margin: 0 auto;
    padding-left: 20px;          /* Creates gap - NEEDS REMOVAL */
    padding-right: 20px;         /* Creates gap - NEEDS REMOVAL */
    margin-top: 164px;           /* Accounts for nav - NEEDS ADJUSTMENT */
}
```

**Image Container (`.hero-image-container`):**
```css
.hero-image-container {
    position: relative;
    width: 100%;
    margin-bottom: 40px;
}
```

**Image Styling:**
```css
.hero-image-container img {
    width: 100%;
    height: auto;
    border-radius: 12px;         /* Creates rounded corners - NEEDS REMOVAL */
    box-shadow: 0 20px 40px rgba(0,0,0,0.1); /* Creates shadow - NEEDS REMOVAL */
}
```

**Overlay Container (`.hero-overlay`):**
```css
.hero-overlay {
    position: absolute;
    top: 40px;                   /* Top-right positioning - NEEDS CHANGE */
    right: 40px;                 /* Top-right positioning - NEEDS CHANGE */
    background: rgba(0, 0, 0, 0.7); /* Dark box - NEEDS REMOVAL */
    padding: 30px;               /* Box padding - NEEDS REMOVAL */
    border-radius: 8px;          /* Box rounded corners - NEEDS REMOVAL */
    max-width: 40%;              /* Width constraint - NEEDS REMOVAL */
}
```

**H1 Styling:**
```css
.hero-overlay h1 {
    font-size: 3rem;
    font-weight: 700;            /* NEEDS CHANGE to 800 */
    color: white;                /* Already white - OK */
    margin: 0;
    line-height: 1.05;
    letter-spacing: -0.02em;
}
```

### Key Measurements & Context

- **Top Banner Height:** 44px (fixed, lines 40-42 in styles.css)
- **Navbar Height:** 120px (fixed, line 102 in styles.css)
- **Combined Offset:** 164px (44px banner + 120px navbar)
- **Navbar Position:** `top: 44px` (line 91 in styles.css)
- **Current Hero Margin-Top:** 164px (accounts for fixed header)

### Mobile Responsive Considerations

**Current Mobile Styles (Lines 763-791 in styles.css):**
```css
@media (max-width: 768px) {
    .hero {
        margin-top: 160px;       /* Slightly different offset */
    }

    .hero-overlay {
        top: 20px;
        left: 20px;
        right: 20px;
        padding: 20px;
        max-width: none;
    }

    .hero-overlay h1 {
        font-size: 2.4rem;
    }
}

@media (max-width: 480px) {
    .hero-overlay h1 {
        font-size: 2.1rem;
    }

    .hero-overlay {
        top: 15px;
        left: 15px;
        right: 15px;
        padding: 15px;
    }
}
```

---

## Implementation Plan

### Phase 1: HTML Modifications

**File:** `/Users/neil/Repos/cadentdev/bostoncpm/dist/index.html`

**Action:** Update the hero section HTML structure (Lines 44-52)

**Changes:**
- No HTML changes required - the structure is already suitable
- The `.hero-overlay` div will be repurposed for gradient overlay + text positioning

**Rationale:** The existing HTML structure is semantic and flexible enough for the new design. We'll achieve all changes through CSS modifications.

---

### Phase 2: CSS Modifications - Desktop Styles

**File:** `/Users/neil/Repos/cadentdev/bostoncpm/dist/styles.css`

#### Step 1: Remove Section Container Constraints (Lines 183-190)

**Current:**
```css
.hero {
    padding: 40px 0 50px;
    max-width: 1200px;
    margin: 0 auto;
    padding-left: 20px;
    padding-right: 20px;
    margin-top: 164px;
}
```

**Replace With:**
```css
.hero {
    padding: 0;                  /* Remove all padding */
    max-width: 100%;             /* Full width */
    margin: 0;                   /* No horizontal centering margin */
    margin-top: 164px;           /* Keep nav offset - positions under translucent nav */
    width: 100%;                 /* Explicit full width */
    position: relative;          /* Establish positioning context */
}
```

**Rationale:**
- Removes max-width constraint to allow edge-to-edge display
- Removes horizontal padding that creates gaps
- Maintains margin-top to tuck under the translucent navbar (44px banner + 120px navbar = 164px)
- Sets position: relative for proper z-index stacking

---

#### Step 2: Update Image Container (Lines 192-196)

**Current:**
```css
.hero-image-container {
    position: relative;
    width: 100%;
    margin-bottom: 40px;
}
```

**Replace With:**
```css
.hero-image-container {
    position: relative;
    width: 100%;
    margin-bottom: 0;            /* Remove bottom margin */
    overflow: hidden;            /* Clip any overflow */
}
```

**Rationale:**
- Maintains relative positioning for absolute child elements
- Removes bottom margin for tighter section spacing
- Adds overflow: hidden for clean edges

---

#### Step 3: Update Image Styling (Lines 198-203)

**Current:**
```css
.hero-image-container img {
    width: 100%;
    height: auto;
    border-radius: 12px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
}
```

**Replace With:**
```css
.hero-image-container img {
    width: 100%;
    height: auto;
    display: block;              /* Remove inline spacing */
    border-radius: 0;            /* Remove rounded corners for edge-to-edge */
    box-shadow: none;            /* Remove shadow for clean edge */
}
```

**Rationale:**
- Removes border-radius for true edge-to-edge appearance
- Removes box-shadow to eliminate visual separation
- Adds display: block to prevent inline element spacing issues

---

#### Step 4: Transform Overlay to Gradient + Text Container (Lines 205-213)

**Current:**
```css
.hero-overlay {
    position: absolute;
    top: 40px;
    right: 40px;
    background: rgba(0, 0, 0, 0.7);
    padding: 30px;
    border-radius: 8px;
    max-width: 40%;
}
```

**Replace With:**
```css
.hero-overlay {
    position: absolute;
    bottom: 0;                   /* Position at bottom */
    left: 0;                     /* Start at left edge */
    right: 0;                    /* Extend to right edge */
    height: 30%;                 /* Cover 30% of image height */
    background: linear-gradient(to top, rgba(0, 0, 0, 0.85) 0%, rgba(0, 0, 0, 0.6) 40%, transparent 100%);
    display: flex;               /* Flexbox for centering */
    align-items: flex-end;       /* Align content to bottom */
    justify-content: center;     /* Center horizontally */
    padding: 0 20px 30px 20px;   /* Padding: none on sides, 30px bottom */
    border-radius: 0;            /* No rounded corners */
}
```

**Gradient Breakdown:**
- **Start (0%):** `rgba(0, 0, 0, 0.85)` - 85% opacity black at bottom (strongest)
- **Middle (40%):** `rgba(0, 0, 0, 0.6)` - 60% opacity black for smooth transition
- **End (100%):** `transparent` - Fully transparent at top (30% of image height)
- **Direction:** `to top` - Dark to transparent from bottom to top

**Rationale:**
- Changes from top-right box to bottom-spanning gradient overlay
- Uses CSS linear-gradient for ombre effect (dark to transparent)
- 85% opacity at bottom ensures strong contrast for white text readability
- Flexbox centering for precise text positioning
- 30px bottom padding creates breathing room from image edge

---

#### Step 5: Update H1 Styling (Lines 215-222)

**Current:**
```css
.hero-overlay h1 {
    font-size: 3rem;
    font-weight: 700;
    color: white;
    margin: 0;
    line-height: 1.05;
    letter-spacing: -0.02em;
}
```

**Replace With:**
```css
.hero-overlay h1 {
    font-size: 3rem;
    font-weight: 800;            /* Increase weight to 800 (extra bold) */
    color: white;                /* Keep white */
    margin: 0;
    line-height: 1.05;
    letter-spacing: -0.02em;
    text-align: center;          /* Center text */
    text-shadow: 0 2px 8px rgba(0, 0, 0, 0.5); /* Subtle shadow for readability */
    max-width: 90%;              /* Prevent text from touching edges */
}
```

**Rationale:**
- Increases font-weight to 800 as required
- Adds text-align: center for centered positioning
- Adds text-shadow for enhanced readability over gradient
- Constrains max-width to 90% to prevent edge touching on wide screens

---

#### Step 6: Remove/Update Obsolete Hero Content Styles (Lines 224-257)

**Action:** The following CSS blocks can be left as-is since they apply to removed HTML elements:
- `.hero-content` (lines 224-231) - Not used in current HTML
- `.hero-content p` (lines 233-239) - Not used in current HTML
- `.hero-cta` (lines 241-257) - Not used in current HTML

**Rationale:** These styles don't affect the current implementation. Can be removed in future cleanup but not critical for this implementation.

---

### Phase 3: CSS Modifications - Mobile Responsive Styles

**File:** `/Users/neil/Repos/cadentdev/bostoncpm/dist/styles.css`

#### Step 7: Update Mobile Hero Styles (Lines 763-791)

**Current:**
```css
@media (max-width: 768px) {
    .hero {
        margin-top: 160px;
    }

    .hero-overlay {
        top: 20px;
        left: 20px;
        right: 20px;
        padding: 20px;
        max-width: none;
    }

    .hero-overlay h1 {
        font-size: 2.4rem;
    }
}
```

**Replace With:**
```css
@media (max-width: 768px) {
    .hero {
        margin-top: 160px;       /* Keep existing offset for mobile nav */
    }

    .hero-overlay {
        height: 35%;             /* Slightly taller gradient on mobile */
        padding: 0 15px 25px 15px; /* Smaller padding for mobile */
        background: linear-gradient(to top, rgba(0, 0, 0, 0.9) 0%, rgba(0, 0, 0, 0.65) 40%, transparent 100%);
    }

    .hero-overlay h1 {
        font-size: 2.4rem;       /* Keep existing mobile font size */
        max-width: 95%;          /* Allow more width on mobile */
    }
}
```

**Rationale:**
- Increases gradient height to 35% for better text visibility on smaller screens
- Increases gradient opacity (90% at bottom) for enhanced readability
- Reduces padding for mobile screen constraints
- Adjusts max-width to 95% for optimal mobile text display

---

#### Step 8: Update Extra Small Mobile Styles (Lines 846-862)

**Current:**
```css
@media (max-width: 480px) {
    .hero-overlay h1 {
        font-size: 2.1rem;
    }

    .hero-overlay {
        top: 15px;
        left: 15px;
        right: 15px;
        padding: 15px;
    }
    /* ... other styles ... */
}
```

**Replace With:**
```css
@media (max-width: 480px) {
    .hero-overlay {
        height: 40%;             /* Even taller gradient for small screens */
        padding: 0 10px 20px 10px; /* Minimal padding */
        background: linear-gradient(to top, rgba(0, 0, 0, 0.92) 0%, rgba(0, 0, 0, 0.7) 45%, transparent 100%);
    }

    .hero-overlay h1 {
        font-size: 2.1rem;       /* Keep existing extra-small font size */
        max-width: 98%;          /* Nearly full width */
        line-height: 1.1;        /* Tighter line height for small screens */
    }

    /* ... keep existing section heading styles ... */
    .about h2,
    .services h2,
    .areas h2,
    .contact h2 {
        font-size: 2.4rem;
    }
}
```

**Rationale:**
- Increases gradient to 40% height for very small screens
- Further increases gradient opacity (92%) for maximum readability
- Minimal padding to maximize text space
- Allows 98% max-width for optimal small-screen use
- Tightens line-height for better small-screen display

---

### Phase 4: JavaScript Verification

**File:** `/Users/neil/Repos/cadentdev/bostoncpm/dist/script.js`

**Action:** No JavaScript changes required

**Verification Points:**
- Smooth scroll offset calculation (line 22): Uses 164px offset which matches our hero margin-top
- Navbar scroll behavior (lines 62-78): Maintains translucent effect, won't interfere with hero
- Intersection Observer (lines 80-107): Applies to sections, not hero - no conflicts
- No JavaScript directly manipulates hero elements

**Rationale:** All existing JavaScript will continue to function correctly with the new hero design. The scroll offset calculations already account for the fixed navigation structure.

---

## Implementation Order

Execute changes in this specific order to minimize issues:

### Order of Execution:

1. **Backup Current Files**
   - Create backup of `styles.css` before modifications
   - Create backup of `index.html` (though no changes needed)

2. **Desktop CSS Changes (Primary)**
   - Step 1: Update `.hero` section container (Lines 183-190)
   - Step 2: Update `.hero-image-container` (Lines 192-196)
   - Step 3: Update image styling (Lines 198-203)
   - Step 4: Transform `.hero-overlay` to gradient container (Lines 205-213)
   - Step 5: Update `.hero-overlay h1` styling (Lines 215-222)

3. **Test Desktop View**
   - Open site in browser at desktop resolution
   - Verify edge-to-edge display
   - Verify gradient appears correctly (dark at bottom, transparent at top)
   - Verify text is centered at bottom
   - Verify text is readable
   - Check that hero tucks under translucent navbar

4. **Mobile Responsive Changes**
   - Step 7: Update tablet/mobile styles (Lines 763-791)
   - Step 8: Update extra-small mobile styles (Lines 846-862)

5. **Test Responsive Views**
   - Test at 768px width (tablet)
   - Test at 480px width (small mobile)
   - Test at 375px width (extra small mobile)
   - Verify gradient coverage and text readability at all sizes

6. **Final Cross-Browser Testing**
   - Chrome/Edge (Chromium)
   - Firefox
   - Safari (desktop and iOS if available)

---

## CSS Code Summary - Complete Replacement Blocks

For easy implementation, here are the complete CSS blocks to replace:

### Desktop Styles to Replace

```css
/* Lines 183-190 - Replace entire .hero block */
.hero {
    padding: 0;
    max-width: 100%;
    margin: 0;
    margin-top: 164px;
    width: 100%;
    position: relative;
}

/* Lines 192-196 - Replace entire .hero-image-container block */
.hero-image-container {
    position: relative;
    width: 100%;
    margin-bottom: 0;
    overflow: hidden;
}

/* Lines 198-203 - Replace entire .hero-image-container img block */
.hero-image-container img {
    width: 100%;
    height: auto;
    display: block;
    border-radius: 0;
    box-shadow: none;
}

/* Lines 205-213 - Replace entire .hero-overlay block */
.hero-overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 30%;
    background: linear-gradient(to top, rgba(0, 0, 0, 0.85) 0%, rgba(0, 0, 0, 0.6) 40%, transparent 100%);
    display: flex;
    align-items: flex-end;
    justify-content: center;
    padding: 0 20px 30px 20px;
    border-radius: 0;
}

/* Lines 215-222 - Replace entire .hero-overlay h1 block */
.hero-overlay h1 {
    font-size: 3rem;
    font-weight: 800;
    color: white;
    margin: 0;
    line-height: 1.05;
    letter-spacing: -0.02em;
    text-align: center;
    text-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
    max-width: 90%;
}
```

### Mobile Responsive Styles to Replace

```css
/* Within @media (max-width: 768px) block - Lines 763-791 */
@media (max-width: 768px) {
    /* ... keep other existing rules ... */

    .hero {
        margin-top: 160px;
    }

    .hero-overlay {
        height: 35%;
        padding: 0 15px 25px 15px;
        background: linear-gradient(to top, rgba(0, 0, 0, 0.9) 0%, rgba(0, 0, 0, 0.65) 40%, transparent 100%);
    }

    .hero-overlay h1 {
        font-size: 2.4rem;
        max-width: 95%;
    }

    /* ... keep other existing rules ... */
}

/* Within @media (max-width: 480px) block - Lines 846-862 */
@media (max-width: 480px) {
    .hero-overlay {
        height: 40%;
        padding: 0 10px 20px 10px;
        background: linear-gradient(to top, rgba(0, 0, 0, 0.92) 0%, rgba(0, 0, 0, 0.7) 45%, transparent 100%);
    }

    .hero-overlay h1 {
        font-size: 2.1rem;
        max-width: 98%;
        line-height: 1.1;
    }

    /* ... keep other existing rules ... */
}
```

---

## Gradient Technical Specifications

### Desktop Gradient (30% coverage)
```css
background: linear-gradient(
    to top,                         /* Direction: bottom to top */
    rgba(0, 0, 0, 0.85) 0%,        /* Bottom: 85% black opacity */
    rgba(0, 0, 0, 0.6) 40%,        /* Middle: 60% black opacity */
    transparent 100%                /* Top: fully transparent */
);
```

**Visual Effect:**
- Bottom 0-40%: Strong dark gradient (85% to 60% opacity)
- Middle 40-70%: Gradual fade (60% to ~30% opacity)
- Top 70-100%: Rapid fade to transparent (30% to 0% opacity)
- Total coverage: 30% of image height from bottom

### Mobile Gradient (35% coverage)
```css
background: linear-gradient(
    to top,
    rgba(0, 0, 0, 0.9) 0%,         /* 90% black - stronger for readability */
    rgba(0, 0, 0, 0.65) 40%,
    transparent 100%
);
```

### Extra-Small Mobile Gradient (40% coverage)
```css
background: linear-gradient(
    to top,
    rgba(0, 0, 0, 0.92) 0%,        /* 92% black - maximum readability */
    rgba(0, 0, 0, 0.7) 45%,
    transparent 100%
);
```

**Rationale for Increased Mobile Coverage & Opacity:**
- Smaller screens = less vertical space = text needs more dark area
- Increased gradient opacity ensures white text remains readable on all images
- 40% coverage on extra-small ensures sufficient dark background even if text wraps

---

## Responsive Design Breakpoints

| Breakpoint | Width Range | Hero Margin-Top | Gradient Height | Gradient Max Opacity | H1 Font Size | Text Max-Width |
|------------|-------------|-----------------|-----------------|----------------------|--------------|----------------|
| Desktop    | > 768px     | 164px          | 30%             | 85%                 | 3rem         | 90%            |
| Tablet/Mobile | ≤ 768px  | 160px          | 35%             | 90%                 | 2.4rem       | 95%            |
| Small Mobile | ≤ 480px   | 160px          | 40%             | 92%                 | 2.1rem       | 98%            |

---

## Testing Checklist

### Visual Verification
- [ ] Hero image extends to full viewport width (no side gaps)
- [ ] No border-radius or box-shadow on image
- [ ] Image top is positioned under translucent navbar (not covered, but behind)
- [ ] Gradient is visible at bottom 30% of image
- [ ] Gradient transitions smoothly from dark to transparent
- [ ] H1 text is positioned at bottom center
- [ ] H1 text is white and bold (font-weight: 800)
- [ ] No background box around text
- [ ] Text is readable over gradient

### Responsive Verification (Desktop)
- [ ] Test at 1920px width - text doesn't touch edges
- [ ] Test at 1440px width - gradient remains proportional
- [ ] Test at 1024px width - text remains centered

### Responsive Verification (Tablet)
- [ ] Test at 768px width - gradient increases to 35%
- [ ] Test at 600px width - text remains readable

### Responsive Verification (Mobile)
- [ ] Test at 480px width - gradient increases to 40%
- [ ] Test at 375px width - text wraps appropriately
- [ ] Test at 320px width - minimum viable display

### Functional Verification
- [ ] Smooth scroll to sections still works correctly
- [ ] Mobile hamburger menu functions properly
- [ ] Navbar translucency effect on scroll works
- [ ] No JavaScript console errors
- [ ] Page load performance is acceptable

### Cross-Browser Verification
- [ ] Chrome/Edge (desktop and mobile view)
- [ ] Firefox (desktop and mobile view)
- [ ] Safari (desktop and iOS if available)

### Accessibility Verification
- [ ] H1 heading still accessible to screen readers
- [ ] Alt text on hero image remains descriptive
- [ ] Sufficient color contrast for white text on gradient (WCAG AA minimum 4.5:1)

---

## Risk Assessment

### Low Risk Issues
1. **CSS Gradient Browser Support**
   - **Risk:** Linear gradients might not work in extremely old browsers
   - **Mitigation:** Modern syntax is supported in all current browsers (IE11+)
   - **Fallback:** Could add solid background fallback before gradient

2. **Text Readability on Very Bright Images**
   - **Risk:** If hero image changes to very bright photo, text might be harder to read
   - **Mitigation:** 85-92% opacity gradient provides strong contrast
   - **Additional Option:** text-shadow already added for extra readability

### Medium Risk Issues
3. **Mobile Landscape Orientation**
   - **Risk:** On mobile devices in landscape, 40% gradient might cover too much of image
   - **Mitigation:** Test in landscape orientation during Phase 5
   - **Solution:** Could add additional media query for landscape if needed:
     ```css
     @media (max-width: 768px) and (orientation: landscape) {
         .hero-overlay { height: 25%; }
     }
     ```

4. **Very Wide Screens (> 2560px)**
   - **Risk:** Hero image might appear stretched or distorted on ultra-wide monitors
   - **Mitigation:** Hero image should maintain aspect ratio (height: auto)
   - **Solution:** If issues arise, could add max-height constraint

### Minimal Risk Issues
5. **Navigation Bar Overlap**
   - **Risk:** Hero might not tuck properly under translucent nav
   - **Mitigation:** margin-top: 164px already accounts for fixed header
   - **Verification:** Test scroll behavior and nav positioning

6. **Image Aspect Ratio Changes**
   - **Risk:** If hero image is replaced with different aspect ratio photo
   - **Mitigation:** CSS uses height: auto to maintain proportions
   - **Note:** 30% gradient is relative to actual image height

---

## Rollback Plan

If implementation causes issues:

### Quick Rollback
1. Restore backup of `styles.css` from before changes
2. Hard refresh browser (Cmd+Shift+R / Ctrl+Shift+R)

### Partial Rollback Options
If only specific issues arise:

**Issue: Edge-to-edge causes layout problems**
- Restore `.hero` max-width: 1200px and padding

**Issue: Gradient doesn't look right**
- Adjust gradient opacity percentages
- Adjust gradient color stops
- Adjust gradient height percentage

**Issue: Text positioning problems**
- Modify flexbox properties (align-items, justify-content)
- Adjust padding values

**Issue: Mobile responsiveness problems**
- Restore mobile media query styles
- Adjust breakpoint thresholds

---

## Future Enhancement Opportunities

### Optional Improvements (Not Part of Current Scope)
1. **Animated Gradient on Scroll**
   - Gradually reduce gradient opacity as user scrolls past hero
   - Would require JavaScript addition to script.js

2. **Text Fade-In Animation**
   - H1 could fade in after page load
   - Would enhance visual polish

3. **Responsive Image Optimization**
   - Consider using `<picture>` element with srcset for different screen sizes
   - Could improve mobile load performance

4. **Dynamic Gradient Based on Image**
   - JavaScript could analyze hero image brightness and adjust gradient accordingly
   - Would ensure optimal text contrast on any image

5. **Parallax Scroll Effect**
   - Hero image could scroll at different rate than rest of page
   - Would add depth and visual interest

---

## Success Criteria

Implementation will be considered successful when:

1. **Visual Requirements Met:**
   - Hero image displays edge-to-edge across full viewport width
   - Ombre gradient covers 30% of bottom of image (35-40% on mobile)
   - Gradient transitions smoothly from dark to transparent
   - H1 text is positioned at bottom center
   - Text is white, bold (800 weight), and readable
   - No containing box around text

2. **Technical Requirements Met:**
   - Image maintains current aspect ratio
   - Hero tucks under translucent navbar
   - No layout shifts or visual glitches
   - Responsive design works on all tested screen sizes
   - No JavaScript errors
   - No accessibility regressions

3. **Quality Standards Met:**
   - Code follows project CSS conventions
   - Changes are well-documented
   - Testing checklist fully completed
   - Cross-browser compatibility verified
   - Mobile experience is optimal

---

## Appendix A: File References

### Primary Files
- **HTML:** `/Users/neil/Repos/cadentdev/bostoncpm/dist/index.html`
- **CSS:** `/Users/neil/Repos/cadentdev/bostoncpm/dist/styles.css`
- **JavaScript:** `/Users/neil/Repos/cadentdev/bostoncpm/dist/script.js` (no changes)

### CSS Line Number References
- Hero section container: Lines 183-190
- Hero image container: Lines 192-196
- Hero image styling: Lines 198-203
- Hero overlay container: Lines 205-213
- Hero overlay H1: Lines 215-222
- Mobile styles (@768px): Lines 763-791
- Extra small mobile (@480px): Lines 846-862

### HTML Line Number References
- Hero section: Lines 44-52

---

## Appendix B: CSS Variables Reference

Relevant CSS variables used in the project (defined in :root, lines 1-33):

```css
--brand-primary: #1f5ab0;        /* Deep Royal Blue */
--text-primary: #1f2937;         /* Primary text */
--text-secondary: #4b5563;       /* Secondary text */
--text-tertiary: #6b7280;        /* Tertiary text */
--bg-secondary: #f9fafb;         /* Light gray background */
```

**Note:** The hero redesign doesn't directly use these variables but they're listed for context and potential future enhancements.

---

## Appendix C: Browser Compatibility

### CSS Features Used

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| linear-gradient | 26+ | 16+ | 6.1+ | 12+ |
| Flexbox | 29+ | 28+ | 9+ | 11+ |
| rgba() colors | 1+ | 3+ | 3.1+ | 9+ |
| position: relative/absolute | All | All | All | All |
| CSS3 shadows (text-shadow) | 4+ | 3.5+ | 3.1+ | 10+ |

**Verdict:** All CSS features used are well-supported in modern browsers. No compatibility issues expected.

---

## Document Change Log

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-10-27 | Feature Planning Agent | Initial implementation plan created |

---

## Approval & Next Steps

**Status:** PENDING CLIENT APPROVAL

**Recommended Next Steps:**
1. Review this implementation plan with client
2. Address any questions or concerns
3. Upon approval, proceed with implementation in the order specified
4. Test thoroughly using provided checklist
5. Deploy to development branch for staging review
6. After staging approval, merge to main branch

**Estimated Implementation Time:** 30-45 minutes
**Estimated Testing Time:** 20-30 minutes
**Total Estimated Time:** 50-75 minutes

---

**End of Implementation Plan**
