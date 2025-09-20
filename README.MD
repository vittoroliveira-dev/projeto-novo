# 🚀 Static Site Development Guidelines

## 📋 Table of Contents

- [Project Structure](#project-structure)

- [HTML Standards](#html-standards)
  - [Document Structure Requirements](#document-structure-requirements)
    - [Base Template Specification](#base-template-specification)
    - [Semantic HTML Requirements](#semantic-html-requirements)
  - [Accessibility (WCAG 2.1 AA Compliance)](#accessibility-wcag-21-aa-compliance)
    - [ARIA Implementation](#aria-implementation)
    - [Keyboard Navigation](#keyboard-navigation)
  - [Structured Data Implementation](#structured-data-implementation)

- [SEO and Indexing](#seo-and-indexing)
  - [Required Files](#required-files)
    - [robots.txt](#robotstxt)
    - [sitemap.xml](#sitemapxml)
    - [404.html](#404html)

- [CSS Architecture](#css-architecture)
  - [ITCSS + BEM Methodology](#itcss--bem-methodology-with-css-layers)
    - [Layer Structure](#layer-structure)
    - [Design Tokens](#design-tokens)
    - [BEM Naming Convention](#bem-naming-convention)
  - [Responsive Design System](#responsive-design-system)
    - [Mobile-First Grid](#mobile-first-grid)
    - [Container Queries](#container-queries)
  - [Performance CSS](#performance-css)
    - [Critical CSS Strategy](#critical-css-strategy)
    - [Font Loading Optimization](#font-loading-optimization)
  - [Dark Mode Implementation](#dark-mode-implementation)

- [JavaScript Guidelines](#javascript-guidelines)
  - [Modern ES6+ Standards](#modern-es6-standards)
    - [Module Structure](#module-structure)
    - [Component Class Pattern](#component-class-pattern)
    - [Performance Optimization (JS)](#performance-optimization-js)
      - [Ship less JS](#ship-less-js)
      - [Code-split and lazy import](#code-split-and-lazy-import)
      - [Keep handlers responsive (INP)](#preload-what-you-will-need-next)
      - [Vite dynamic imports (glob)](#vite-dynamic-imports-glob)
      - [Preload what you will need next](#preload-what-you-will-need-next)
      - [Keep handlers responsive (INP)](#keep-handlers-responsive-inp)
      - [Avoid layout thrash](#avoid-layout-thrash)
      - [Break up long tasks](#break-up-long-tasks)
      - [Network and fetch priority](#network-and-fetch-priority)
      - [Off-main-thread for heavy work](#off-main-thread-for-heavy-work)
      - [Build-time optimizations (Vite)](#build-time-optimizations-vite)
      - [Event utilities (debounce/throttle)](#event-utilities-debouncethrottle)
    - [Lazy Loading Implementation](#21-lazy-loading-implementation)
    - [Debounce & Throttle Utilities](#22-debounce--throttle-utilities)
    - [Web Vitals Monitoring](#3-web-vitals-monitoring)
    - [Progressive Enhancement](#4-progressive-enhancement)

- [Performance Optimization](#performance-optimization)
  - [Image Optimization Strategy](#1-image-optimization-strategy)
    - [Responsive Images Implementation](#1-image-optimization-strategy)
    - [Modern Image Formats](#12-modern-image-formats-guide)
      - [Overview](#overview)
      - [Format Priority](#format-priority)
      - [Use Cases](#use-cases)
      - [Implementation Examples](#implementation-examples)
      - [Encoding Commands](#encoding-commands)
        - [AVIF Encoding](#avif-encoding)
        - [WebP Encoding - Photos (lossy)](#webp-encoding---photos-lossy)
        - [Batch Processing Example](#batch-processing-example)
      - [Best Practices](#best-practices)
        - [Authoring Rules](#best-practices)
        - [Performance Tips](#performance-tips)
        - [Responsive Considerations](#responsive-considerations)
          - [Testing and Validation](#testing-and-validation)
  - [Resource Hints & Preloading](#resource-hints--preloading)
  - [Service Worker Implementation](#service-worker-implementation)

- [Security Implementation](#security-implementation)
  - [Performance Monitoring](#performance-monitoring)
  - [Google TAG Manager - (GA4, CSP-safe, consent mode, SPA-ready)](#dompurify-usage-self-host-esm--csp-friendly)
  - [Content Security Policy](#content-security-policy)
    - [Tighten CSP (nonce path) and add missing directives](#tighten-csp-nonce-path-and-add-missing-directives)
    - [Static-site (hash path) example](#static-site-hash-path-example)
    - [clarify “Key Directives You Must Use” section](#static-site-hash-path-example)
    - [Trusted Types (Chromium hardening; harmless elsewhere)](#add--trusted-types-chromium-hardening-harmless-elsewhere)
    - [Input sanitization section (expand with URL and HTML guards)](#input-sanitization-section-expand-with-url-and-html-guards)
    - [DOMPurify usage (self-host ESM + CSP-friendly)](#dompurify-usage-self-host-esm--csp-friendly)

  - [Analytics Implementation]()
    - [Google Analytics 4](#google-analytics-4-csp-compatible)
    - [Privacy-Focused Alternatives]()

- [Quality Assurance](#quality-assurance)
  - [Testing Configuration](#1-testing-configuration)
    - [Jest Unit Testing](#11-jest-unit-testing)
    - [Playwright E2E Testing](#12-playwright-e2e-testing)
  - [Performance Budget](#2-performance-budget)

- [Additional Resources](#-additional-resources)
  - [Validation Tools](#validation-tools)
  - [Performance Testing](#performance-testing)
  - [Security Auditing](#security-auditing)
  - [Documentation](#documentation)

- [Production Checklist](#-production-checklist)
  - [Code Quality]()
  - [Performance](#css--performance)
  - [JavaScript & Functionality]()
  - [Accessibility]()
  - [Security](#security)
  - [Progressive Web App]()
  - [Monitoring & Analytics]()
  - [Infrastructure]()
  - [Testing]()
  - [Documentation]().

---

# Project Structure
[⬆️ Back to top](#)

```diff
 project/
├── src/
│   ├── index.html
│   ├── pages/
│   │   └── *.html
│   ├── styles/
│   │   ├── base/
│   │   │   ├── _reset.css
│   │   │   └── _settings.css
│   │   ├── components/
│   │   │   └── _c-*.css
│   │   ├── layout/
│   │   │   └── _grid.css
│   │   ├── utilities/
│   │   │   └── _u-*.css
│   │   └── main.css
│   ├── scripts/
│   │   ├── modules/
│   │   └── main.js
│   └── assets/
│       ├── fonts/
│       ├── images/
│       └── icons/
├── dist/                      # or "docs/" (choose ONE output)
├── public/                    # files served at the site root
│   ├── favicon.svg
│   ├── apple-touch-icon.png
│   ├── robots.txt
│   ├── sitemap.xml
│   ├── 404.html
│   └── icons.svg              # optional SVG sprite
├── .nvmrc
├── package.json
├── vite.config.js
├── postcss.config.js
├── .editorconfig
├── eslint.config.js
├── .stylelintrc.cjs
├── .browserslistrc
├── lighthouserc.json          # or budget.json
├── .nojekyll                  # se publicar via GitHub Pages
├── .github/
│   └── workflows/
│       ├── ci.yml             # lint + build + LHCI
│       └── deploy.yml         # SFTP/rsync, if applicable
├── AGENTS.md 
└── README.md
```

---

# HTML Standards
[⬆️ Back to top](#)

## Document Structure Requirements
[⬆️ Back to top](#)

### Base Template Specification
[⬆️ Back to top](#)

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <!-- Required Meta Tags -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- SEO Meta Tags -->
  <title>Page Title | Brand Name</title>
  <meta name="description" content="155-character maximum description">
  <link rel="canonical" href="https://domain.com/page/">
  <meta name="robots" content="index, follow">
  
  <!-- Open Graph Protocol -->
  <meta property="og:type" content="website">
  <meta property="og:title" content="Page Title">
  <meta property="og:description" content="Engaging description">
  <meta property="og:image" content="https://domain.com/og-image.jpg">
  <meta property="og:image:width" content="1200">
  <meta property="og:image:height" content="630">
  <meta property="og:url" content="https://domain.com/page/">
  
  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:site" content="@handle">
  
  <!-- Favicons -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
  <link rel="alternate icon" href="/favicon.ico">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
  
  <!-- Font Preloading -->
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
  
  <!-- CSS -->
  <link rel="preload" href="/css/critical.css" as="style">
  <link rel="stylesheet" href="/css/critical.css">
  <link rel="stylesheet" href="/styles/main.css">
</head>
<body>
  <!-- Skip Navigation -->
  <a href="#main" class="skip-link">Skip to main content</a>

  <!-- Semantic Structure -->
  <header>
    <nav aria-label="Main navigation"><!-- items --></nav>
  </header>

  <main id="main" tabindex="-1">
    <h1>Single H1 per page</h1>
    <!-- Page content -->
  </main>

  <aside aria-label="Sidebar">
    <!-- Secondary content -->
  </aside>

  <footer>
    <!-- Footer content -->
  </footer>

  <script src="/scripts/main.js" type="module" defer></script>
</body>
</html>
```

### Semantic HTML Requirements
[⬆️ Back to top](#)

- Use HTML5 semantic elements: `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`
- Implement proper heading hierarchy (h1 → h6)
- Single `<h1>` per page.
- Use a list (ul > li > a) for navigation.
- aria-current="page" only on the active page link.
- required replaces aria-required.
- inert prevents focus when the menu is hidden; remove it via JS on open.
- Use aria-live or role="alert", not both; stick with aria-live="polite".
- Set aria-invalid="true" only upon an actual error.
- Unique `<title>` per page (50-60 characters)
- Unique meta descriptions (50-160 characters)

## Accessibility (WCAG 2.1 AA Compliance)
[⬆️ Back to top](#)

### ARIA Implementation
[⬆️ Back to top](#)

```html
<!-- Navigation State -->
<nav aria-label="Navigation State">
  <button type="button" aria-expanded="false" aria-controls="primary-menu" class="c-nav__toggle"
    data-menu-trigger>Menu</button>
  <ul id="primary-menu" class="c-nav__list" hidden data-menu inert>
    <li><a href="/" aria-current="page">Início</a></li>
    <li><a href="/about">Sobre</a></li>
  </ul>
</nav>
```

```html
<!-- Expandable Elements -->
<button aria-expanded="false" aria-controls="menu-items">
  Menu
</button>
<ul id="menu-items" hidden>
  <!-- Menu items -->
</ul>
```

```html
<!-- Form Accessibility -->
 <form>
  <label for="email">Email Address</label>
   <input 
     type="email" 
     id="email" 
     name="email"
    required
    autocomplete="email"
    aria-invalid="false"
    aria-describedby="email-error">
  <span id="email-error" aria-live="polite" class="u-visually-hidden"></span>
 </form>
```

```html
 <!-- Decorative Icons -->
-<svg aria-hidden="true" focusable="false">
+<svg aria-hidden="true" focusable="false" width="24" height="24">
   <!-- Icon content -->
 </svg>
```

### Keyboard Navigation
[⬆️ Back to top](#)

- Implement logical tab order
- Visible focus indicators (minimum 2px outline)
- Skip links for keyboard navigation
- Trap focus in modals

## Structured Data Implementation
[⬆️ Back to top](#)

```html
<script type="application/ldjson">
 {
   "@context": "https://schema.org",
   "@type": "Organization",
  "@id": "https://domain.com/#organization",
  "name": "Company Name",
  "url": "https://domain.com/",
  "logo": {
    "@type": "ImageObject",
    "url": "https://domain.com/logo.png",
    "width": 512,
    "height": 512
  },
  "sameAs": [
     "https://facebook.com/company",
     "https://twitter.com/company"
   ],
  "contactPoint": [{
    "@type": "ContactPoint",
    "telephone": "5511999999999",
    "contactType": "customer service",
    "availableLanguage": ["pt-BR"]
  }]
 }
 </script>
```

```html
<!-- BreadcrumbList for hierarchical pages -->
<script type="application/ldjson">
 {
   "@context": "https://schema.org",
   "@type": "BreadcrumbList",
   "itemListElement": [{
     "@type": "ListItem",
     "position": 1,
     "name": "Home",
    "item": "https://domain.com/"
  },{
     "@type": "ListItem",
     "position": 2,
     "name": "Category",
    "item": "https://domain.com/category/"
 }]
 }
 </script>
```

#### **Notes:**

- Use `@id` to link nodes (e.g., `WebSite.publisher` → `#organization`).
- Provide the phone number in `E.164` format without dashes.
- Set `availableLanguage` as an array containing `"pt-BR`".
- Use trailing slashes on URLs for canonical consistency.

---

# SEO and Indexing
[⬆️ Back to top](#)

## Required Files
[⬆️ Back to top](#)

### robots.txt

```txt
User-agent: *
Disallow:
Sitemap: https://example.com/sitemap.xml
# Staging (usar outro arquivo): 
# User-agent: * 
# Disallow: /
```

### sitemap.xml
[⬆️ Back to top](#)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <lastmod>2025-09-01</lastmod>
  </url>
  <!-- Add other canonical URLs, absolute only -->
</urlset>
```

### 404.html
[⬆️ Back to top](#)

```html
<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="robots" content="noindex, nofollow">
  <title>Página não encontrada — 404</title>
  <link rel="stylesheet" href="%BASE_URL%styles/main.css">
</head>
<body>
  <main id="main">
    <h1>Página não encontrada (404)</h1>
    <p>Voltar para a <a href="%BASE_URL%">página inicial</a>.</p>
  </main>
</body>
</html>
```

#### Notes:

- Place robots.txt, sitemap.xml, and 404.html in the public/ directory so they are output to the site's root when using Vite.
- Use a meta robots tag on the 404 page to prevent the /404.html URL from being indexed when accessed directly.
- Sitemap URLs must always be absolute and canonical. If possible, update the lastmod dates automatically during the build process.

---

# CSS Architecture
[⬆️ Back to top](#)

## ITCSS + BEM Methodology with CSS Layers
[⬆️ Back to top](#)

### Layer Structure
[⬆️ Back to top](#)

```css
/* layer and base structure */
/* main.css */
@layer reset, base, theme, layout, components, utilities, overrides;
 
 @import url('base/_reset.css') layer(reset);
 @import url('base/_settings.css') layer(base);
@import url('base/_theme.css') layer(theme);
 @import url('layout/_grid.css') layer(layout);
 @import url('components/_c-card.css') layer(components);
 @import url('utilities/_u-spacing.css') layer(utilities);
/* just occasional hotfixes here */
@import url('overrides/_shame.css') layer(overrides);
```

### Design Tokens
[⬆️ Back to top](#)

```css
/* tokens e media custom */
:root {
   /* Colors */
   --color-primary-100: hsl(220, 80%, 95%);
   --color-primary-500: hsl(220, 80%, 50%);
   --color-primary-900: hsl(220, 80%, 10%);
  --color-bg: #fff;
  --color-fg: #111;
 
   /* Typography */
   --font-family-base: system-ui, -apple-system, sans-serif;
   --font-size-base: clamp(1rem, 2vw, 1.125rem);
   --line-height-base: 1.6;
 
   /* Spacing */
   --spacing-xs: 0.25rem;
   --spacing-sm: 0.5rem;
   --spacing-md: 1rem;
   --spacing-lg: 2rem;
   --spacing-xl: 4rem;
 
  /* Radius / Shadow */
  --radius-sm: .25rem;
  --radius-md: .5rem;
  --radius-lg: .75rem;
  --shadow-sm: 0 1px 2px rgb(0 0 0 / .06);
  --shadow-md: 0 2px 8px rgb(0 0 0 / .08);

   /* Z-index Scale */
   --z-dropdown: 100;
   --z-sticky: 200;
   --z-overlay: 900;
   --z-modal: 1000;
   --z-tooltip: 1100;
 
   /* Transitions */
   --transition-fast: 150ms ease-in-out;
   --transition-base: 300ms ease-in-out;
  --easing-standard: cubic-bezier(.2, .0, .2, 1);
 
   /* Breakpoints (for JS) */
   --breakpoint-sm: 640px;
   --breakpoint-md: 768px;
   --breakpoint-lg: 1024px;
   --breakpoint-xl: 1280px;

  /* Layout */
  --container-max: 72rem;
  --container-pad: clamp(1rem, 3vw, 2rem);
 }

@custom-media --sm (width >= 640px);
@custom-media --md (width >= 768px);
@custom-media --lg (width >= 1024px);
```

### BEM Naming Convention
[⬆️ Back to top](#)

```css
/* BEM + States without increasing specificity */
/* components/_c-card.css */
@layer components {
  .c-card { background:var(--color-bg); color:var(--color-fg); border-radius:var(--radius-md); box-shadow:var(--shadow-sm); }
  .c-card__header{ padding:var(--spacing-md); }
  .c-card__body{ padding:var(--spacing-md); }
  .c-card__footer{ padding:var(--spacing-md); }
  .c-card--featured { box-shadow:var(--shadow-md); }
  .c-card:where(:hover, :focus-visible) { transform: translateY(-2px); transition: transform var(--transition-base) var(--easing-standard); }
}
```

### Responsive Design System
[⬆️ Back to top](#)

#### Mobile-First Grid
[⬆️ Back to top](#)

```css
/* layout */
 /* layout/_grid.css */
@layer layout {
  .o-container {
    width: min(100% - 2*var(--container-pad), var(--container-max));
    margin-inline: auto;
  }
  .l-grid { display:grid; gap:var(--spacing-md);
    grid-template-columns: repeat(auto-fit, minmax(min(300px, 100%), 1fr)); }
  @media (--md) {
    .l-grid--2-cols { grid-template-columns: repeat(2, 1fr); }
    .l-grid--3-cols { grid-template-columns: repeat(3, 1fr); }
    .l-grid--4-cols { grid-template-columns: repeat(4, 1fr); }
  }
}
```

#### Container Queries

```css
/* utilities */
/* utilities/_u-a11y.css */
@layer utilities {
  .u-visually-hidden { position:absolute !important; width:1px; height:1px; padding:0; margin:-1px; overflow:hidden; clip:rect(0 0 0 0); white-space:nowrap; border:0; }
  .u-focus-ring:focus-visible { outline:2px solid currentColor; outline-offset:2px; }
  .u-no-anim { animation:none !important; transition:none !important; }
}
```

```css
/* theme */
/* base/_theme.css */
@layer theme {
  :root { color-scheme: light dark; }
  @media (prefers-color-scheme: dark) {
    :root { --color-bg:#0b0b0b; --color-fg:#eaeaea; }
  }
  @media (prefers-reduced-motion: reduce) {
    * { animation-duration:.01ms !important; animation-iteration-count:1 !important; transition-duration:.01ms !important; scroll-behavior:auto !important; }
  }
}
```

```css
/* components/_c-card.css */
@layer components {
  .c-card { background:var(--color-bg); color:var(--color-fg); border-radius:var(--radius-md); box-shadow:var(--shadow-sm); }
  .c-card__header{ padding:var(--spacing-md); }
  .c-card__body{ padding:var(--spacing-md); }
  .c-card__footer{ padding:var(--spacing-md); }
  .c-card--featured { box-shadow:var(--shadow-md); }
  .c-card:where(:hover, :focus-visible) { transform: translateY(-2px); transition: transform var(--transition-base) var(--easing-standard); }
}
```

##### **Notes:**

- The theme layer separates `light/dark mode` and motion preference variations.
- An `overrides` layer isolates hotfixes and helps prevent specificity wars.
- Use `@custom-media` queries to standardize breakpoints throughout the CSS.
- Object classes like `.o-container` and accessibility (a11y) utilities reduce code duplication.
- `:where()` mantém especificidade baixa para estados e hovers.

### Performance CSS
[⬆️ Back to top](#)

#### Critical CSS Strategy
[⬆️ Back to top](#)

```css
/* Critical CSS (trimmed, CLS-safe, motion-safe) */
/* Inline in <head> — above-the-fold only */
html { scroll-behavior: smooth; }
body {
  margin: 0;
  font-family: system-ui, -apple-system, Segoe UI, Roboto, sans-serif;
  background: var(--color-bg, #fff);
  color: var(--color-text, #111);
  text-rendering: optimizeLegibility;
}
.l-header { background:#fff; box-shadow:0 2px 4px rgb(0 0 0 / .08); }
.l-hero { min-block-size: 60svh; display:grid; place-items:center; }
img, svg { display:block; max-width:100%; height:auto; }
@media (prefers-reduced-motion: reduce){
  * { animation:none !important; transition:none !important; scroll-behavior:auto; }
}
```

#### Font Loading Optimization
[⬆️ Back to top](#)

```css
/* Font loading (variable-friendly, Vite base, subsets) */
 @font-face {
   font-family: 'CustomFont';
  src: url('%BASE_URL%fonts/custom.woff2') format('woff2');
  font-display: swap; /* consider 'optional' if FOUT is undesirable */
  font-style: normal;
  font-weight: 300 700; /* variable range or set exact weights */
  size-adjust: 105%;
  ascent-override: 90%;
  descent-override: 10%;
  line-gap-override: 0%;
  unicode-range: U000-5FF; /* add extended ranges as needed */
 }
```

### Dark Mode Implementation
[⬆️ Back to top](#)

```css
 /* Dark mode (apply vars to body, add accent color) */
 /* Automatic dark mode */
 :root {
   color-scheme: light dark;
 }
 
 /* Custom properties for themes */
[data-theme="light"] {
   --color-bg: hsl(0, 0%, 100%);
   --color-text: hsl(0, 0%, 10%);
  --accent: hsl(220 80% 50%);
 }
 
 [data-theme="dark"] {
   --color-bg: hsl(0, 0%, 10%);
   --color-text: hsl(0, 0%, 90%);
  --accent: hsl(220 80% 60%);
 }
 
 /* Respect user preference */
 @media (prefers-color-scheme: dark) {
   :root:not([data-theme="light"]) {
     --color-bg: hsl(0, 0%, 10%);
     --color-text: hsl(0, 0%, 90%);
   }
 }

/* Apply theme to actual paint */
body { background-color: var(--color-bg); color: var(--color-text); accent-color: var(--accent); }
```

---

# JavaScript Guidelines
[⬆️ Back to top](#)

## Modern ES6+ Standards
[⬆️ Back to top](#)

### Module Structure
[⬆️ Back to top](#)

```javascript
// main.js
import { LazyLoader } from './modules/LazyLoader.js';
import { MenuController } from './modules/MenuController.js';
import { FormValidator } from './modules/FormValidator.js';
import { PerformanceMonitor } from './modules/PerformanceMonitor.js';

// Initialize on DOM ready
if (document.readyState === 'loading') {
  document.addEventListener('DOMContentLoaded', init);
} else {
  init();
}

function init() {
  new LazyLoader();
  new MenuController();
  new FormValidator();
  new PerformanceMonitor();
}
```

#### **Notes:**
- Use `svh` for stable viewport on mobile to reduce jumps from browser UI.
- Ensure hero image has explicit `width` and `height` in HTML to minimize CLS.
- Consider `font-display: optional` if late font swap hurts layout.

### Component Class Pattern
[⬆️ Back to top](#)

```javascript
// modules/MenuController.js
export class MenuController {
  constructor() {
    this.menu = document.querySelector('[data-menu]');
    this.trigger = document.querySelector('[data-menu-trigger]');
    this.isOpen = false;
    
    if (this.menu && this.trigger) {
      this.init();
    }
  }
  
  init() {
    this.trigger.addEventListener('click', this.toggle.bind(this));
    
    // Escape key closes menu
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' && this.isOpen) {
        this.close();
      }
    });
    
    // Click outside closes menu
    document.addEventListener('click', (e) => {
      if (this.isOpen && !this.menu.contains(e.target) && 
          !this.trigger.contains(e.target)) {
        this.close();
      }
    });
  }
  
  toggle() {
    this.isOpen ? this.close() : this.open();
  }
  
  open() {
    this.menu.hidden = false;
    this.trigger.setAttribute('aria-expanded', 'true');
    this.isOpen = true;
    
    // Trap focus
    this.menu.querySelector('a, button')?.focus();
  }
  
  close() {
    this.menu.hidden = true;
    this.trigger.setAttribute('aria-expanded', 'false');
    this.isOpen = false;
    this.trigger.focus();
  }
}
```

### Performance Optimization (JS)
[⬆️ Back to top](#)

#### Ship less JS
- Budget: ≤150 KB gzipped total, ≤75 KB on first load.
- No polyfills by default. Load only-needed polyfills conditionally.

```html
<!-- Only if feature missing -->
<script type="module">
  if (!('IntersectionObserver' in window)) {
    import('%BASE_URL%polyfills/intersection-observer.min.js');
  }
</script>
```

#### Code-split and lazy import
- Split non-critical modules. Load on visibility or intent.

```javascript
// modules/boostrap-lazy.js
const onIntersect = (el, cb, rootMargin='200px') => {
  const io = new IntersectionObserver(e=>{
    if (e[0].isIntersecting){ io.disconnect(); cb(); }
  },{rootMargin});
  io.observe(el);
};

// Example: heavy carousel only when visible
const spot = document.querySelector('[data-carousel]');
if (spot) onIntersect(spot, async () => {
  const { Carousel } = await import('./Carousel.js');
  new Carousel(spot);
});
```

#### Vite dynamic imports (glob)
- Map page-specific initializers to chunks.

```javascript
// main.js
const inits = import.meta.glob('./pages/**/init-*.js'); // lazy chunks
document.querySelectorAll('[data-init]').forEach(async el => {
  const mod = inits[`./pages/${el.dataset.init}.js`];
  if (mod) (await mod()).default(el);
});
```

#### Preload what you will need next
- Use `modulepreload` for the next likely chunk.

```html
<link rel="modulepreload" href="%BASE_URL%scripts/pages/init-contact.js">
```

#### Keep handlers responsive (INP)
- Use passive listeners, delegate, and yield on long work.

```javascript
// Passive + delegated
document.addEventListener('touchstart', onTap, { passive: true });
document.body.addEventListener('click', (e)=>{
  const btn = e.target.closest('[data-action]');
  if (!btn) return;
  handle(btn.dataset.action);
});

// Yield to input
export async function yieldToInput() {
  // scheduler.isInputPending() guard (if available)
  const s = navigator.scheduling?.isInputPending?.bind(navigator.scheduling);
  if (s && s({ includeContinuous: true })) await Promise.resolve();
  // rIC fallback
  await new Promise(res => {
    (window.requestIdleCallback || setTimeout)(res, 1);
  });
}
```


#### Avoid layout thrash
- Read, then write. Batch via `requestAnimationFrame`.

```javascript
// measure → mutate
function setHeights(nodes){
  const heights = Array.from(nodes, n => n.offsetHeight); // read batch
  requestAnimationFrame(() => {                           // write batch
    nodes.forEach((n,i)=> n.style.blockSize = heights[i] + 'px');
  });
}
```

#### Break up long tasks
- Chunk work into micro-batches under ~50 ms.

```javascript
export async function chunked(list, fn, chunk=50){
  let i=0; const t = performance.now;
  while (i<list.length){
    const start = t();
    for (let c=0; c<chunk && i<list.length; c++, i++) fn(list[i]);
    if (t() - start > 45) await yieldToInput(); // from step 5
  }
}
```

#### Network and fetch priority
- Hint browser priorities and cancel on navigation.

```javascript
// Priority hint where supported
fetch(url, { priority: 'low' }).catch(()=>{});

// Abort stale requests
const ctl = new AbortController();
addEventListener('pagehide', () => ctl.abort(), { once:true });
fetch('/api/list', { signal: ctl.signal });
```

#### Off-main-thread for heavy work
- Use a Worker for parsing, image ops, or large JSON.

```javascript
// worker.js
self.onmessage = (e)=> { const out = heavyCompute(e.data); postMessage(out); };

// main
const w = new Worker(new URL('./worker.js', import.meta.url), { type:'module' });
w.postMessage(data);
w.onmessage = ({data}) => render(data);
```

#### Build-time optimizations (Vite)
- Tree-shake, define env, split vendor, drop debug.

```javascript
// vite.config.js (excerpt)
export default {
  build: {
    minify: 'terser',
    terserOptions: { compress: { drop_console:true, drop_debugger:true } },
    rollupOptions: {
      output: { manualChunks: { vendor: ['lodash-es','dayjs'] } }
    },
    target: 'es2020', // modern output → smaller
  },
  define: { __DEV__: false }
};
```

### Event utilities (debounce/throttle)
- Use your improved helpers for scroll/resize/input.

```javascript
import { debounce, throttle } from './modules/utils.js';
addEventListener('resize', debounce(() => recalc(), 200));
addEventListener('scroll', throttle(() => track(), 150, { trailing:true }));
```
#### Guard CSS/JS interaction
- Prefer CSS for hover/focus states.
- Avoid JS-driven layout where `aspect-ratio`, `:has()`, or `contain` solves it

#### Lazy Loading Implementation
[⬆️ Back to top](#)

```javascript
// LazyLoader.js (robust fallback, srcset/picture, wider rootMargin):
// modules/LazyLoader.js
```javascript
 // LazyLoader.js (robust fallback, srcset/picture, wider rootMargin):
 // modules/LazyLoader.js
 export class LazyLoader {
   constructor() {
    this.images = document.querySelectorAll('img[loading="lazy"], iframe[loading="lazy"]');
     this.imageObserver = null;

    // Fallback for browsers without native lazy loading
    if (!('loading' in HTMLImageElement.prototype)) {
       this.initIntersectionObserver();
     }
   }
   
   initIntersectionObserver() {
    this.imageObserver = new IntersectionObserver((entries) => {
       entries.forEach(entry => {
         if (entry.isIntersecting) {
          const node = entry.target;
          // <picture> support
          if (node.parentElement?.tagName === 'PICTURE') {
            node.parentElement.querySelectorAll('source').forEach(src => {
              if (src.dataset.srcset) src.srcset = src.dataset.srcset;
            });
          }
          // img/iframe attributes
          if (node.dataset.srcset) node.srcset = node.dataset.srcset;
          if (node.dataset.sizes) node.sizes = node.dataset.sizes;
          if (node.dataset.src) node.src = node.dataset.src;
          node.decode?.().catch(() => {}).finally(() => node.classList.add('is-loaded'));
          this.imageObserver.unobserve(node);
         }
       });
     }, {
      rootMargin: '300px 0px',
       threshold: 0.01
     });
     
     this.images.forEach(img => this.imageObserver.observe(img));
    // Cleanup on tab hide
    document.addEventListener('visibilitychange', () => {
      if (document.visibilityState === 'hidden') this.imageObserver.disconnect();
    }, { once: true });
   }
 }
```

#### **Note:**

- Markup note (no code change here): for the fallback to work, use data-src, data-srcset, and data-sizes on lazy elements, plus a low-risk placeholder src if needed.

### Debounce & Throttle Utilities
[⬆️ Back to top](#)

```javascript
 // utils.js (preserve context, cancel/flush options):
 // modules/utils.js

export function debounce(fn, wait = 200, { leading = false, trailing = true } = {}) {
  let timeout, lastArgs, lastThis, result;
  const invoke = () => { const r = fn.apply(lastThis, lastArgs); lastArgs = lastThis = undefined; return r; };
  const later = () => { timeout = undefined; if (trailing && lastArgs) result = invoke(); };
  function debounced(...args) {
    lastArgs = args; lastThis = this;
    const callNow = leading && !timeout;
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
    if (callNow) result = invoke();
    return result;
  }
  debounced.cancel = () => { clearTimeout(timeout); timeout = lastArgs = lastThis = undefined; };
  debounced.flush = () => { if (timeout) { clearTimeout(timeout); later(); } return result; };
  return debounced;
}
 

export function throttle(fn, limit = 200, { leading = true, trailing = true } = {}) {
  let last = 0, timeout, lastArgs, lastThis;
  function invoke(now) { last = now; const r = fn.apply(lastThis, lastArgs); lastArgs = lastThis = undefined; return r; }
  return function throttled(...args) {
    const now = Date.now();
    if (!last && !leading) last = now;
    const remaining = limit - (now - last);
    lastArgs = args; lastThis = this;
    if (remaining <= 0) {
      if (timeout) { clearTimeout(timeout); timeout = undefined; }
      return invoke(now);
    }
    if (trailing && !timeout) {
      timeout = setTimeout(() => { timeout = undefined; invoke(Date.now()); }, remaining);
    }
  };
}
```

### Web Vitals Monitoring
[⬆️ Back to top](#)

```javascript
 // modules/PerformanceMonitor.js
 export class PerformanceMonitor {
   constructor() {
     this.initWebVitals();
     this.trackErrors();
   }
 
   async initWebVitals() {
    // PerformanceMonitor.js (self-hosted ESM, GA4/beacon, extra error hook):
    // Prefer bundling via Vite: `npm i web-vitals`
    const { onLCP, onINP, onCLS, onFCP, onTTFB } = await import('web-vitals/attribution');
    const send = (metric) => {
      // GA4 if available
      if (window.gtag) {
        window.gtag('event', metric.name, {
          value: Math.round(metric.value),
          event_label: metric.id,
          non_interaction: true
        });
      }
      // Self-hosted endpoint (optional)
      const body = JSON.stringify(metric);
      if (!navigator.sendBeacon || !navigator.sendBeacon('/metrics', body)) {
        console.log('[web-vitals]', metric);
      }
    };
     
     onLCP(send);
     onINP(send);
     onCLS(send);
     onFCP(send);
     onTTFB(send);

    // Flush pending metrics on pagehide
    const flush = () => { /* no-op: send() uses Beacon/console */ };
    addEventListener('visibilitychange', () => {
      if (document.visibilityState === 'hidden') flush();
    });
   }
 
   trackErrors() {
     window.addEventListener('error', (e) => {
       const payload = {
         msg: e.message,
         src: e.filename,
         line: e.lineno,
         col: e.colno
       };
       console.warn('[error]', payload);
     });
    window.addEventListener('unhandledrejection', (e) => {
      console.warn('[unhandledrejection]', { reason: String(e.reason) });
    });
   }
 }
```

#### **Notes:**
- Keep `loading="eager"` and `fetchpriority="high"` only for the single above-the-fold hero image; lazy-load the rest.
- If CSP is strict, self-host `web-vitals` and avoid inline code.

---

# Performance Optimization
[⬆️ Back to top](#)

## Image Optimization Strategy
[⬆️ Back to top](#)

### Responsive Images Implementation
[⬆️ Back to top](#)

```html
<!-- <picture> (use %BASE_URL%, add JPG 1600w, keep fetchpriority only for LCP) -->
 <picture>
  <!-- AVIF (optional; remove if you don't ship it) -->
   <source 
     type="image/avif"
     srcset="
      %BASE_URL%img/hero-400w.avif 400w,
      %BASE_URL%img/hero-800w.avif 800w,
      %BASE_URL%img/hero-1200w.avif 1200w,
      %BASE_URL%img/hero-1600w.avif 1600w"
     sizes="(max-width: 640px) 100vw, 
            (max-width: 1024px) 80vw, 
            1200px">
   
   <!-- WebP for modern browsers -->
   <source 
     type="image/webp"
     srcset="
      %BASE_URL%img/hero-400w.webp 400w,
      %BASE_URL%img/hero-800w.webp 800w,
      %BASE_URL%img/hero-1200w.webp 1200w,
      %BASE_URL%img/hero-1600w.webp 1600w"
     sizes="(max-width: 640px) 100vw, 
            (max-width: 1024px) 80vw, 
            1200px">
   
   <!-- JPEG fallback -->
   <img 
    src="%BASE_URL%img/hero-800w.jpg"
     srcset="
      %BASE_URL%img/hero-400w.jpg 400w,
      %BASE_URL%img/hero-800w.jpg 800w,
      %BASE_URL%img/hero-1200w.jpg 1200w,
      %BASE_URL%img/hero-1600w.jpg 1600w"
     sizes="(max-width: 640px) 100vw, 
            (max-width: 1024px) 80vw, 
            1200px"
     alt="Hero image description"
     width="1200"
     height="600"
    loading="eager" fetchpriority="high"  <!-- drop both if not LCP -->
     decoding="async">
 </picture>
```

```html
<!-- Preload LCP image in <head> (matches sources) -->
<link rel="preload" as="image"
  imagesrcset="%BASE_URL%img/hero-800w.webp 800w, %BASE_URL%img/hero-1200w.webp 1200w, %BASE_URL%img/hero-1600w.webp 1600w"
  imagesizes="(max-width: 1024px) 80vw, 1200px"
  href="%BASE_URL%img/hero-1200w.jpg">
```

#### CSS fallback in a single rule (simpler)

```css
   /* CSS background fallback (base path + no-repeat) */
 .hero-background {
  background-image: url("%BASE_URL%img/bg.jpg"); /* fallback */
   background-image: image-set(
    url("%BASE_URL%img/bg.avif") type("image/avif"),
    url("%BASE_URL%img/bg.webp") type("image/webp"),
    url("%BASE_URL%img/bg.jpg") type("image/jpeg")
   );
   background-size: cover;
   background-position: center;
  background-repeat: no-repeat;
 }
```

## Modern Image Formats Guide
[⬆️ Back to top](#)

### Overview
[⬆️ Back to top](#)

#### **Goal**: Ship the smallest files with acceptable quality, correct MIME types, and wide compatibility.

#### **Fallback Strategy:** AVIF (optional) → WebP → JPEG/PNG  • SVG for vectors

### Format Priority
[⬆️ Back to top](#)

| Format | Best For | Browser Support | File Size |
|--------|----------|-----------------|-----------|
| **AVIF** | Photos, complex images | Modern browsers | Smallest |
| **WebP** | Universal fallback | Wide support | Small |
| **JPEG** | Photo compatibility | Universal | Medium |
| **PNG** | Transparency, crisp edges | Universal | Large |
| **SVG** | Vector graphics, icons | Universal | Variable |

### Use Cases
[⬆️ Back to top](#)

#### Photographs
##### **Primary:** AVIF
##### **Fallback:** WebP
##### **Last resort:** JPEG

#### Logos / Icons / Flat illustrations
##### **Preferred:** SVG (don’t rasterize)
##### **Alternative:** PNG/WebP only if raster is required at fixed size

####  UI Screenshots / Crisp edges
##### **Primary:** PNG (lossless, no chroma blur)
##### **Alternative:** AVIF lossless if encoder tested (watch subsampling)

##### Animations
###### **Short loops:** Animated AVIF/WebP
###### **Long/complex:** Video (`.mp4`/`.webm`)

### Implementation Examples
[⬆️ Back to top](#)

#### Responsive Photo with Picture Element

```html
<!-- Hero/Photo Implementation -->
<!-- Implementation example (Vite base, add 1600w, keep fetchpriority only for LCP) -->
 <picture>
  <source type="image/avif"
          srcset="%BASE_URL%img/hero-800.avif 800w, %BASE_URL%img/hero-1200.avif 1200w, %BASE_URL%img/hero-1600.avif 1600w"
           sizes="(max-width: 1024px) 90vw, 1200px">
  <source type="image/webp"
          srcset="%BASE_URL%img/hero-800.webp 800w, %BASE_URL%img/hero-1200.webp 1200w, %BASE_URL%img/hero-1600.webp 1600w"
           sizes="(max-width: 1024px) 90vw, 1200px">
  <img src="%BASE_URL%img/hero-1200.jpg"
       srcset="%BASE_URL%img/hero-800.jpg 800w, %BASE_URL%img/hero-1200.jpg 1200w, %BASE_URL%img/hero-1600.jpg 1600w"
        width="1200" height="600" alt="Hero image description"
       loading="eager" fetchpriority="high" decoding="async">
 </picture>
```

#### Optional — Preload the LCP image (match sources)

```html
<link rel="preload" as="image"
  imagesrcset="%BASE_URL%img/hero-1200.webp 1200w, %BASE_URL%img/hero-1600.webp 1600w"
  imagesizes="(max-width: 1024px) 90vw, 1200px"
  href="%BASE_URL%img/hero-1200.jpg">
```

#### SVG Icons (Recommended)

```html
<!-- Inline SVG Icon -->
<svg aria-hidden="true" focusable="false" width="24" height="24">
  <use href="/icons.svg#check"></use>
</svg>
```

#### CSS Background Images with Fallbacks

```css
/* Modern CSS with image-set() */
.hero-background {
  background-image: image-set(
    url("/img/bg.avif") type("image/avif"),
    url("/img/bg.webp") type("image/webp"),
    url("/img/bg.jpg") type("image/jpeg")
  );
  background-size: cover;
  background-position: center;
}

/* Legacy fallback */
.hero-background {
  background-image: url("/img/bg.jpg"); /* Fallback */
  background-image: image-set(
    url("/img/bg.avif") type("image/avif"),
    url("/img/bg.webp") type("image/webp"),
    url("/img/bg.jpg") type("image/jpeg")
  );
}
```

#### Add authoring rules (concise)

- Convert to `sRGB`, strip EXIF.
- Always set `width`/`height` to avoid CLS.
- Use `loading="eager"` + `fetchpriority="high"` only for the LCP image.
- Remove the AVIF `<source>` if you don’t ship AVIF.

### Encoding Commands
[⬆️ Back to top](#)

#### AVIF Encoding

```bash
##### Preprocess (convert to sRGB and strip metadata)
magick input.jpg -colorspace sRGB -strip input-srgb.jpg

##### General purpose (photos)
avifenc -q 32 -s 6 -y 420 --jobs all input-srgb.jpg -o output.avif
 
##### High quality
avifenc -q 24 -s 4 -y 420 --jobs all input-srgb.jpg -o output.avif
 
##### Small file size
avifenc -q 40 -s 8 -y 420 --jobs all input-srgb.jpg -o output.avif

##### UI / crisp edges (avoid chroma blur)
avifenc -q 28 -s 6 -y 444 --jobs all input-srgb.png -o output.avif

##### Lossless (use sparingly; large files)
avifenc --lossless -s 4 --jobs all input-srgb.png -o output.avif
```

##### WebP Encoding - Photos (lossy)

```bash
cwebp -q 77 -m 6 -sharp_yuv -mt input.jpg -o output.webp
 
##### Graphics/logos (lossless compression)
cwebp -lossless -z 9 -mt input.png -o output.webp
 
##### With transparency
cwebp -q 80 -alpha_q 85 -m 6 -mt input.png -o output.webp

##### Near-lossless for UI (good balance)
cwebp -near_lossless 60 -z 9 -mt input.png -o output.webp
```

#### Batch Processing Example

```bash
##### POSIX: convert all JPEGs to AVIF and WebP (with sRGB preprocessing)
shopt -s nullglob
for img in *.jpg *.jpeg; do
  magick "$img" -colorspace sRGB -strip "tmp-$img"
  avifenc -q 32 -s 6 -y 420 --jobs all "tmp-$img" -o "${img%.*}.avif"
  cwebp -q 77 -m 6 -sharp_yuv -mt "tmp-$img" -o "${img%.*}.webp"
  rm -f "tmp-$img"
done

##### Windows PowerShell: JPEG → AVIF/WebP
Get-ChildItem -Include *.jpg,*.jpeg -File | ForEach-Object {
  magick $_.FullName -colorspace sRGB -strip "$($_.DirectoryName)\tmp-$($_.Name)"
  avifenc -q 32 -s 6 -y 420 --jobs all "$($_.DirectoryName)\tmp-$($_.Name)" -o "$($_.DirectoryName)\$($_.BaseName).avif"
  cwebp -q 77 -m 6 -sharp_yuv -mt "$($_.DirectoryName)\tmp-$($_.Name)" -o "$($_.DirectoryName)\$($_.BaseName).webp"
  Remove-Item "$($_.DirectoryName)\tmp-$($_.Name)"
}
```

#### **Notes:**
- Keep AVIF 4:4:4 for UI and screenshots; 4:2:0 for photos.
- Always convert to sRGB and strip EXIF to reduce size and color surprises.
- Skip AVIF if you don’t serve it; keep WebP + JPEG/PNG.
- Test visually at multiple zoom levels after encoding.

#### Best Practices

##### Authoring Rules

- **Export multiple widths** and serve with `<picture>` + `srcset`
- **Always set `width` and `height`** attributes to prevent Cumulative Layout Shift (CLS)
- **Include accurate `alt` text** for accessibility
- **Convert to sRGB** color space for web compatibility
- **Strip EXIF data** unless specifically required
- **Use cache-friendly filenames** with hashes for 1-year caching
- **Set HTML to no-cache** while images cache long-term

##### Performance Tips

- Use `loading="lazy"` for images below the fold
- Use `loading="eager"` and `fetchpriority="high"` for above-the-fold images
- Always include `decoding="async"` for better performance
- Consider using CSS `aspect-ratio` for responsive containers

##### Responsive Considerations

```html
<!-- Responsive sizes attribute examples -->
sizes="100vw"                           <!-- Full width -->
sizes="(max-width: 768px) 100vw, 50vw"  <!-- Mobile full, desktop half -->
sizes="(max-width: 1024px) 90vw, 1200px" <!-- With max-width -->
```

##### Testing and Validation

- Test images in multiple browsers
- Validate MIME types are served correctly
- Check file sizes with network inspector
- Verify CLS scores don't increase
- Test with slow network connections

##### Browser Support

| Format | Chrome | Firefox | Safari | Edge |
|--------|--------|---------|--------|------|
| AVIF   | 85+    | 93+     | 16.4+  | 85+  |
| WebP   | 32+    | 65+     | 14+    | 18+  |
| JPEG   | ✅     | ✅      | ✅     | ✅   |
| PNG    | ✅     | ✅      | ✅     | ✅   |
| SVG    | ✅     | ✅      | ✅     | ✅   |

---

### Resource Hints & Preloading

```html
 <head>
  <!-- Resource Hints (minimal, accurate, subpath-safe) -->
  <!-- DNS Prefetch (include ONLY if these domains are used) -->
  <!-- <link rel="dns-prefetch" href="https://cdn.example.com"> -->
  <!-- <link rel="dns-prefetch" href="https://analytics.example.com"> -->
   
   <!-- Preconnect for critical origins -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   
   <!-- Preload critical resources -->

  <link rel="preload" href="%BASE_URL%fonts/main.woff2" as="font" type="font/woff2" crossorigin>
  <link rel="preload" href="%BASE_URL%css/critical.css" as="style">
  <!-- ES modules: prefer modulepreload over script preload -->
  <link rel="modulepreload" href="%BASE_URL%scripts/main.js">
  <!-- LCP image (match picture/srcset if used) -->
  <!--
  <link rel="preload" as="image"
        href="%BASE_URL%img/hero-1200.jpg"
        imagesrcset="%BASE_URL%img/hero-1200.webp 1200w, %BASE_URL%img/hero-1600.webp 1600w"
        imagesizes="(max-width: 1024px) 90vw, 1200px">
  -->
   
   <!-- Prefetch next page resources -->

  <link rel="prefetch" href="%BASE_URL%page2.html">
  <!-- Do NOT prefetch CSS; use preload when truly needed -->
  <!-- <link rel="preload" href="%BASE_URL%css/page2.css" as="style"> -->
   
   <!-- Module preload for ES6 modules -->

  <link rel="modulepreload" href="%BASE_URL%scripts/modules/critical.js">
 </head>
```

### Service Worker Implementation

```javascript
// sw.js
// Service Worker (scope-safe, same-origin, nav preload, robust fallbacks)
 const CACHE_VERSION = 'v1.0.0';
 const CACHE_NAMES = {
   static: `static-${CACHE_VERSION}`,
   dynamic: `dynamic-${CACHE_VERSION}`,
   images: `images-${CACHE_VERSION}`
 };
 
 // Install event
 self.addEventListener('install', (event) => {
   event.waitUntil(
     caches.open(CACHE_NAMES.static).then((cache) => {
      // Use %BASE_URL% for subpath deployments
      return cache.addAll([
        '%BASE_URL%',
        '%BASE_URL%styles/main.css',
        '%BASE_URL%scripts/main.js',
        '%BASE_URL%offline.html'
      ]);
     })
   );
   self.skipWaiting();
 });
 
 // Activate event
 self.addEventListener('activate', (event) => {
   event.waitUntil(
     caches.keys().then((cacheNames) => {
       return Promise.all(
         cacheNames
           .filter((cacheName) => {
             return !Object.values(CACHE_NAMES).includes(cacheName);
           })
           .map((cacheName) => caches.delete(cacheName))
       );
     })
   );
  // Navigation preload can improve HTML fetch on slow networks
  if ('navigationPreload' in self.registration) {
    event.waitUntil(self.registration.navigationPreload.enable());
  }
   self.clients.claim();
 });
 
 // Fetch strategies
 self.addEventListener('fetch', (event) => {
   const { request } = event;
  const url = new URL(request.url);

  // Only handle same-origin
  if (url.origin !== location.origin) return;
   
   // Skip non-GET requests
   if (request.method !== 'GET') return;
  // Skip no-store and range requests
  if (request.headers.get('Cache-Control')?.includes('no-store')) return;
  if (request.headers.has('Range')) return;
   
   // HTML: Network first, fallback to cache
  if (request.mode === 'navigate' || request.headers.get('accept')?.includes('text/html')) {
     event.respondWith(
      (async () => {
        try {
          const preload = 'navigationPreload' in self.registration
            ? await event.preloadResponse
            : null;
          const net = preload || await fetch(request, { credentials: 'same-origin' });
          if (net && net.ok) {
            const clone = net.clone();
            caches.open(CACHE_NAMES.dynamic).then((c) => c.put(request, clone));
            return net;
          }
          const cached = await caches.match(request);
          return cached || await caches.match('%BASE_URL%offline.html');
        } catch {
          const cached = await caches.match(request);
          return cached || await caches.match('%BASE_URL%offline.html');
        }
      })()
     );
     return;
   }
   
   // Images: Cache first
   if (request.destination === 'image') {
     event.respondWith(
       caches.match(request).then((response) => {
         return response || fetch(request).then((response) => {
           const responseClone = response.clone();
           caches.open(CACHE_NAMES.images).then((cache) => {
             cache.put(request, responseClone);
           });
           return response;
         });
       })
     );
     return;
   }
   
   // CSS/JS: Cache first with network update
   if (request.destination === 'style' || request.destination === 'script') {
     event.respondWith(
       caches.match(request).then((response) => {
         const fetchPromise = fetch(request).then((networkResponse) => {
           caches.open(CACHE_NAMES.static).then((cache) => {
             cache.put(request, networkResponse.clone());
           });
           return networkResponse;
         });
         return response || fetchPromise;
       })
     );
   }
 });

// Optional: allow clients to trigger skipWaiting after deploy
self.addEventListener('message', (event) => {
  if (event.data === 'SW_SKIP_WAITING') self.skipWaiting();
});
```

#### Registration snippet (ensure correct scope)

```html
<script type="module">
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('%BASE_URL%sw.js', { scope: '%BASE_URL%' })
      .catch(console.error);
  }
</script>
```

##### **Notes:**
- Use `%BASE_URL%` everywhere to work on GitHub Pages or any subpath.
- Do not prefetch CSS. Preload CSS only when you will apply it.
- Cache hashed assets aggressively via HTTP headers; SW should not fight server caching.
- Keep PWA optional. If you do not need offline, skip the SW entirely.

---

# Security Implementation

## Performance Monitoring

```javascript
// monitoring/rum.js
// Self-hosted, sampled RUM with modern Navigation Timing and Web Vitals.
const SAMPLE_RATE = 0.25; // 25% of sessions
const RUM_ENDPOINT = '%BASE_URL%api/metrics';   // adjust to your backend
const ERR_ENDPOINT = '%BASE_URL%api/errors';    // adjust to your backend

if (Math.random() < SAMPLE_RATE && document.visibilityState !== 'prerender') {
  (async function RUM() {
    const state = { metrics: {} };
    const send = (type, data) => {
      const body = JSON.stringify({ type, data, url: location.href, t: Date.now() });
      if (!navigator.sendBeacon || !navigator.sendBeacon(RUM_ENDPOINT, body)) {
        fetch(RUM_ENDPOINT, { method: 'POST', body, headers: { 'Content-Type': 'application/json' }, keepalive: true }).catch(() => {});
      }
    };

    // Navigation Timing Level 2
    addEventListener('load', () => {
      const nav = performance.getEntriesByType('navigation')[0];
      if (nav) {
        state.metrics.nav = {
          ttfb: Math.max(0, nav.responseStart - nav.requestStart),
          domContentLoaded: Math.max(0, nav.domContentLoadedEventEnd - nav.startTime),
          loadEvent: Math.max(0, nav.loadEventEnd - nav.startTime)
        };
        send('nav', state.metrics.nav);
      }
    }, { once: true });

    // Web Vitals (bundle via Vite: npm i web-vitals)
    try {
      const { onLCP, onINP, onCLS, onFCP, onTTFB } = await import('web-vitals/attribution');
      const ship = (m) => send('vital', {
        name: m.name, value: m.value, id: m.id, rating: m.rating,
        navigationType: performance.getEntriesByType('navigation')[0]?.type
      });
      onLCP(ship); onINP(ship); onCLS(ship); onFCP(ship); onTTFB(ship);
    } catch {}

    // Long tasks (Chrome)
    if ('PerformanceObserver' in window) {
      try {
        const lt = new PerformanceObserver((list) => {
          const tasks = list.getEntries().map(e => ({ name: e.name, start: e.startTime, dur: e.duration }));
          if (tasks.length) send('longtasks', tasks);
        });
        lt.observe({ entryTypes: ['longtask'] });
      } catch {}
    }

    // Resource timing (same-origin only; cross-origin often zeroed)
    if ('PerformanceObserver' in window) {
      try {
        const rt = new PerformanceObserver((list) => {
          const slow = list.getEntries()
            .filter(e => e.initiatorType !== 'beacon' && e.duration > 1000)
            .slice(0, 20) // cap payload
            .map(e => ({ name: e.name, type: e.initiatorType, dur: e.duration, size: e.transferSize || e.encodedBodySize || 0 }));
          if (slow.length) send('resources', slow);
        });
        rt.observe({ entryTypes: ['resource'] });
      } catch {}
    }

    // JS errors
    addEventListener('error', (ev) => {
      const payload = {
        msg: ev.message || 'ResourceError',
        src: ev.filename || (ev.target && ev.target.src) || null,
        line: ev.lineno, col: ev.colno
      };
      const body = JSON.stringify({ url: location.href, t: Date.now(), ...payload });
      if (!navigator.sendBeacon || !navigator.sendBeacon(ERR_ENDPOINT, body)) {
        fetch(ERR_ENDPOINT, { method: 'POST', body, headers: { 'Content-Type': 'application/json' }, keepalive: true }).catch(() => {});
      }
    }, true);
    addEventListener('unhandledrejection', (ev) => {
      const body = JSON.stringify({ url: location.href, t: Date.now(), reason: String(ev.reason) });
      if (!navigator.sendBeacon || !navigator.sendBeacon(ERR_ENDPOINT, body)) {
        fetch(ERR_ENDPOINT, { method: 'POST', body, headers: { 'Content-Type': 'application/json' }, keepalive: true }).catch(() => {});
      }
    });

    // Flush before unload
    addEventListener('pagehide', () => send('final', {}), { once: true });
  })();
}
```

## Google TAG - (GA4, CSP-safe, consent mode, SPA-ready)

```html
<!-- GA4 (nonce only on inline; external allowed via CSP) -->
<link rel="preconnect" href="https://www.google-analytics.com">
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXX"></script>
<script nonce="{NONCE}">
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}

 // Consent Mode default (deny until user accepts; adapt as needed)
 gtag('consent', 'default', {
   ad_storage: 'denied',
   analytics_storage: 'denied',
   ad_user_data: 'denied',
   ad_personalization: 'denied',
   wait_for_update: 500
 });

  gtag('js', new Date());

 // SPA note: disable auto page_view if you will send your own events
 // gtag('config', 'G-XXXX', { send_page_view: false });
 gtag('config', 'G-XXXX', {
   transport_type: 'beacon'
 });

 // Example SPA route tracking (call on each route change)
 // function trackPageView(path){ gtag('event', 'page_view', { page_location: location.originpath }); }
 </script>
```

## Content Security Policy 

### Tighten CSP (nonce path) and add missing directives

```http
 Content-Security-Policy:
  default-src 'self';
  base-uri 'self';
  object-src 'none';
  frame-ancestors 'none';
  form-action 'self';
  script-src 'self' 'nonce-RANDOM_VALUE_HERE' 'strict-dynamic';
  script-src-attr 'none';
  style-src 'self'; /* add 'nonce-...' or hash if you inline critical CSS */
  style-src-attr 'none';
  img-src 'self' data: https:;
  font-src 'self' https://fonts.gstatic.com;
  connect-src 'self' https://api.your-service.com;
  upgrade-insecure-requests;
  report-to csp-endpoint; report-uri https://report.example.com/csp  /* optional */
```

#### **Notes:**
- With a nonce + `'strict-dynamic'`, you usually do not need to whitelist CDNs in `script-src`. Any script loaded by a trusted nonce-bearing script is trusted.
- If you inline critical CSS, prefer `style-src 'self' 'nonce-…'` or a `sha256-…` hash instead of `'unsafe-inline'`.
- Keep `script-src-attr 'none'` to kill inline event handlers (`onclick`, etc).

### static-site (hash path) example:

```http
Content-Security-Policy:
  default-src 'self';
  base-uri 'self';
  object-src 'none';
  frame-ancestors 'none';
  form-action 'self';
  script-src 'self' 'sha256-<HASH_OF_INLINE_SCRIPT>';
  script-src-attr 'none';
  style-src 'self' 'sha256-<HASH_OF_INLINE_CRITICAL_CSS>'; /* or omit if no inline CSS */
  style-src-attr 'none';
  img-src 'self' data: https:;
  font-src 'self' https://fonts.gstatic.com;
  connect-src 'self' https://api.your-service.com;
  upgrade-insecure-requests;
```

### clarify “Key Directives You Must Use” section:

```http
script-src 'self' [NONCES_OR_HASHES] 'strict-dynamic';
script-src-attr 'none';
style-src 'self' ['nonce-XYZ' | 'sha256-…']; /* avoid 'unsafe-inline' when possible */
style-src-attr 'none';
base-uri 'self';
report-to csp-endpoint; /* optional reporting */
```

- Add — nonce note (dynamic servers):
  - Generate a cryptographically secure nonce per request.
  - Apply the same nonce to every inline `<script nonce="…">`.
  - Avoid mixing nonced and non-nonced inline scripts.

- Add — hash note (static builds):
  - Compute SHA256/384/512 of the exact inline content at build time.
  - Any change to the inline content requires updating the hash in the header.

#### Add — Trusted Types (Chromium hardening; harmless elsewhere):

```http
Content-Security-Policy: ...; require-trusted-types-for 'script'; trusted-types default dompurify;
```

### Input sanitization section (expand with URL and HTML guards)

```http
// SECURE — render as text; never use innerHTML for unsanitized data.
 displayElement.textContent = userInput;

// Safe URL assignment helper (blocks javascript: and data: for <a>)
function safeHref(el, url) {
  try {
    const u = new URL(url, location.origin);
    if (u.protocol === 'http:' || u.protocol === 'https:') el.setAttribute('href', u.href);
  } catch {/* ignore invalid URLs */}
}
```

### DOMPurify usage (self-host ESM + CSP-friendly):

```html
<!-- bundle DOMPurify locally via Vite; avoid CDN to keep CSP simple -->
<script type="module">
  import DOMPurify from '/scripts/vendor/dompurify.esm.js';
  const cleanHtml = DOMPurify.sanitize(untrustedHtml, { USE_PROFILES: { html: true } });
  displayElement.innerHTML = cleanHtml;
</script>
```

#### Maintainability tips:
- Put the policy in infrastructure config (`_headers`, `netlify.toml`, `nginx.conf`) not in meta tags.
- If you later add GA4 or other third parties, update `connect-src` and `img-src` only. Keep `script-src` nonce-based.
- Prefer no inline scripts/styles. If you must, use nonces or hashes.

# Quality Assurance

## Testing Configuration

### Jest Unit Testing

```javascript
// jest.config.js
export default {
    testEnvironment: 'jsdom',
    setupFilesAfterEnv: ['<rootDir>/tests/setup.js'],
    moduleNameMapper: {
        '^@/(.*)$': '<rootDir>/src/$1',
        '\\.(css|less|scss|sass)$': 'identity-obj-proxy'
    },
    collectCoverageFrom: [
        'src/**/*.js',
        '!src/**/*.test.js',
        '!src/vendor/**'
    ],
    coverageThreshold: {
        global: {
            branches: 80,
            functions: 80,
            lines: 80,
            statements: 80
        }
    }
};
```

#### **Example Test:**

```javascript
// tests/FormValidator.test.js
import { FormValidator } from '../src/modules/FormValidator.js';

describe('FormValidator', () => {
    let form, validator;
    
    beforeEach(() => {
        document.body.innerHTML = `
            <form id="test-form">
                <input type="email" name="email" required>
                <button type="submit">Submit</button>
            </form>
        `;
        form = document.getElementById('test-form');
        validator = new FormValidator(form);
    });
    
    test('validates email field correctly', () => {
        const emailInput = form.querySelector('input[name="email"]');
        
        emailInput.value = 'invalid-email';
        expect(validator.validateField(emailInput)).toBe(false);
        
        emailInput.value = 'valid@email.com';
        expect(validator.validateField(emailInput)).toBe(true);
    });
});
```

#### **Example E2E Test:**

```javascript
// tests/e2e/navigation.spec.js
import { test, expect } from '@playwright/test';

test.describe('Navigation', () => {
    test('should navigate to all main pages', async ({ page }) => {
        await page.goto('/');
        
        // Test navigation menu
        await page.click('nav a[href="/about"]');
        await expect(page).toHaveURL('/about');
        await expect(page).toHaveTitle(/About/);
        
        // Test mobile menu
        await page.setViewportSize({ width: 375, height: 667 });
        await page.click('[data-menu-trigger]');
        await expect(page.locator('[data-menu]')).toBeVisible();
    });
    
    test('should have working skip link', async ({ page }) => {
        await page.goto('/');
        await page.keyboard.press('Tab');
        
        const skipLink = page.locator('.skip-link');
        await expect(skipLink).toBeFocused();
        await skipLink.click();
        
        await expect(page.locator('#main')).toBeFocused();
    });
});
```

## Performance Budget

```json
// budget.json
{
    "path": "/*",
    "timings": [
        {
            "metric": "first-contentful-paint",
            "budget": 1000
        },
        {
            "metric": "largest-contentful-paint",
            "budget": 2500
        },
        {
            "metric": "cumulative-layout-shift",
            "budget": 0.1
        },
        {
            "metric": "total-blocking-time",
            "budget": 200
        }
    ],
    "resourceSizes": [
        {
            "resourceType": "script",
            "budget": 150000
        },
        {
            "resourceType": "stylesheet",
            "budget": 100000
        },
        {
            "resourceType": "image",
            "budget": 500000
        },
        {
            "resourceType": "total",
            "budget": 1000000
        }
    ],
    "resourceCounts": [
        {
            "resourceType": "third-party",
            "budget": 5
        }
    ]
}
```

---

# Additional Resources

## Validation Tools

- [W3C HTML Validator](https://validator.w3.org/)
- [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
- [WAVE Accessibility Checker](https://wave.webaim.org/)
- [Google PageSpeed Insights](https://pagespeed.web.dev/)
- [WebPageTest](https://www.webpagetest.org/)

## Performance Testing

- [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
- [Core Web Vitals Chrome Extension](https://chrome.google.com/webstore/detail/web-vitals/)
- [Chrome DevTools Performance Panel](https://developer.chrome.com/docs/devtools/evaluate-performance/)

## Security Auditing

- [Mozilla Observatory](https://observatory.mozilla.org/)
- [Security Headers](https://securityheaders.com/)
- [SSL Labs](https://www.ssllabs.com/ssltest/)

## Documentation

- [MDN Web Docs](https://developer.mozilla.org/)
- [Can I Use](https://caniuse.com/)
- [web.dev](https://web.dev/)

# Production Checklist

## Code Quality
- [ ] All HTML validated
- [ ] All CSS validated
- [ ] JavaScript linted without errors
- [ ] TypeScript compiled without errors (if applicable)

## Performance
- [ ] Lighthouse score > 95 on all metrics
- [ ] Core Web Vitals within recommended thresholds
- [ ] Performance budget met
- [ ] Images optimized and properly sized
- [ ] Critical CSS inlined
- [ ] JavaScript bundles optimized

## Accessibility
- [ ] WCAG 2.1 AA compliance verified
- [ ] Screen reader tested
- [ ] Keyboard navigation functional
- [ ] Color contrast ratios validated
- [ ] Alt text for all images

## Security
- [ ] Security headers configured
- [ ] SSL certificate valid and configured
- [ ] CSP (Content Security Policy) implemented
- [ ] No mixed content warnings

## SEO & Metadata
- [ ] Sitemap.xml generated and submitted
- [ ] Robots.txt configured
- [ ] Meta descriptions for all pages
- [ ] Open Graph images created (1200x630)
- [ ] Schema.org markup implemented
- [ ] Canonical URLs set

## Progressive Web App
- [ ] Service Worker registered
- [ ] Manifest.json configured
- [ ] Offline functionality tested
- [ ] Add to homescreen prompt working

## Monitoring & Analytics
- [ ] Analytics/monitoring configured
- [ ] Error tracking implemented
- [ ] Performance monitoring active
- [ ] Search Console configured

## Infrastructure
- [ ] CDN configured and tested
- [ ] Backup strategy implemented
- [ ] 404 page created and styled
- [ ] Favicons for all platforms generated

## Testing
- [ ] Cross-browser tested (Chrome, Firefox, Safari, Edge)
- [ ] Mobile responsive verified
- [ ] Forms tested and validated
- [ ] All interactive elements tested

## Documentation
- [ ] README updated with project information
- [ ] Code documented appropriately
- [ ] Deployment instructions documented
- [ ] Environment variables documented
