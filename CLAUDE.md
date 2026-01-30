# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A static portfolio website for Natalia Buendia, a product designer. This is a purely frontend project with no build system - HTML files are served directly.

## Development

**Start the development server:**
```bash
# Using VS Code Live Server extension (configured on port 5501)
# Or use any static file server:
npx serve .
python -m http.server 5501
```

The site is accessible at `http://127.0.0.1:5501/`

## Git Workflow

**CRITICAL: Proper commit practices are mandatory in this repository.**

### Commit Guidelines

1. **One feature per commit** - Each commit should contain exactly one logical change or feature
2. **Clear commit messages** - Use descriptive messages that explain what and why, not just what
3. **Separate concerns** - Never mix unrelated changes in a single commit
4. **Atomic commits** - Each commit should be self-contained and functional

### Commit Message Format

Follow this structure:
```
Brief summary (50 chars or less)

Detailed explanation if needed:
- What was changed
- Why it was changed
- Any important implementation details

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

### Examples of Proper Commits

✅ **Good:**
- "Add hover animation to project cards"
- "Fix cursor position offset on Safari"
- "Update Samphire project description and images"

❌ **Bad:**
- "Updates" or "Fix stuff"
- Mixing animation changes with text updates
- Multiple unrelated features in one commit

### Workflow

When implementing multiple changes:
1. Complete one feature fully
2. Test it works independently
3. Commit with clear message
4. Move to next feature
5. Repeat

**Never bundle multiple features into one commit.** Each commit should be reviewable and revertable independently.

## Technology Stack

- **Animations**: GSAP with ScrollTrigger and Flip plugins
- **Smooth Scrolling**: Lenis
- **Page Transitions**: Barba.js
- **Fonts**: Custom "Acid Grotesk" font (in `fonts/`)
- **No build tools** - all dependencies loaded via CDN

## Architecture

### Scroll-Based "Moments" System

The homepage uses a pinned scroll animation that transitions between stacked "moment" sections:
- `#moment-1`: Hero section with image cluster and spotlight effect
- `#moment-2`: Samphire project showcase
- `#moment-3`: Kotie project showcase
- `#moment-4`: Contact section (triggers dark theme)

Each moment uses GSAP ScrollTrigger with scale, opacity, and blur transitions. The animation timeline is defined in `initZoomScroll()`.

### Theme System

CSS variables control the light/dark theme transition (triggered when scrolling to moment-4):
```css
--bg-frame, --bg-outer, --text-color, --cursor-color, --nav-text-color, --bar-bg
```

Theme transitions are animated via GSAP `gsap.to("html", {...})`.

### Custom Cursor

A custom cursor with hover states replaces the default. Classes `hover-link` and `hover-project` modify appearance. The cursor is hidden with `cursor: none` globally.

### Accessibility Mode

Currently disabled (`a11yToggle.addEventListener` is commented out). When enabled, it:
- Disables GSAP scroll animations
- Stops Lenis smooth scrolling
- Shows all moments in a stacked layout

## File Structure

- `index.html` - Main homepage (all CSS and JS are inline)
- `project.html` - Project detail page template
- `pages/about.html` - Empty placeholder
- `fonts/` - Acid Grotesk font files
- `img/` - Portfolio images and mockups
