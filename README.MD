# 🚀 Static Site Development Guidelines

## 📋 Table of Contents

- [Project Structure](#project-structure)

- [HTML Standards](#html-standards)
  - [Document Structure Requirements](#document-structure-requirements)
    - [Base Template Specification](#11-base-template-specification)
    - [Semantic HTML Requirements](#12-semantic-html-requirements)
  - [Accessibility (WCAG 2.1 AA Compliance)](#2-accessibility-wcag-21-aa-compliance)
    - [ARIA Implementation](#21-aria-implementation)
    - [Keyboard Navigation](#22-keyboard-navigation)
  - [Structured Data Implementation](#3-structured-data-implementation)

- [SEO and Indexing](#seo-and-indexing)
  - [Required Files](#required-files)
    - [robots.txt](#robotstxt)
    - [sitemap.xml](#sitemapxml)
    - [404.html](#404html)
    - [Server Configuration (nginx)](#server-configuration-nginx)

- [CSS Architecture](#css-architecture)
  - [ITCSS + BEM Methodology](#1-itcss--bem-methodology-with-css-layers)
    - [Layer Structure](#1-itcss--bem-methodology-with-css-layers)
    - [Design Tokens](#12-design-tokens)
    - [BEM Naming Convention](#13-bem-naming-convention)
  - [Responsive Design System](#2-responsive-design-system)
    - [Mobile-First Grid](#21-mobile-first-grid)
    - [Container Queries](#22-container-queries-modern-approach)
  - [Performance CSS](#3-performance-css)
    - [Critical CSS Strategy](#31-critical-css-strategy)
    - [Font Loading Optimization](#32-font-loading-optimization)
  - [Dark Mode Implementation](#4-dark-mode-implementation)

- [JavaScript Guidelines](#javascript-guidelines)
  - [Modern ES6+ Standards](#1-modern-es6-standards)
    - [Module Structure](#11-module-structure)
    - [Component Class Pattern](#12-component-class-pattern)
    - [Performance Optimization (JS)](#2-performance-optimization)
    - [Lazy Loading Implementation](#21-lazy-loading-implementation)
    - [Debounce & Throttle Utilities](#22-debounce--throttle-utilities)
    - [Web Vitals Monitoring](#3-web-vitals-monitoring)
    - [Progressive Enhancement](#4-progressive-enhancement)

- [Performance Optimization](#performance-optimization)
  - [Image Optimization Strategy](#1-image-optimization-strategy)
    - [Responsive Images Implementation](#1-image-optimization-strategy)
    - [Modern Image Formats]()
      - [Overview](#overview)
      - [Format Priority](#format-priority)
      - [Use Cases](#use-cases)
      - [Implementation Examples](#implementation-examples)
      - [Encoding Commands](#encoding-commands)
      - [Server Configuration](#server-configuration)
      - [Best Practices](#best-practices)
  - [Resource Hints & Preloading](#2-resource-hints--preloading)
  - [Service Worker Implementation](#service-worker-implementation)
  - [Speculation Rules API](#speculation-rules-api)
  - [Build Configuration](#5-build-configuration)
    - [Vite Configuration](#51-vite-configuration)
    - [PostCSS Configuration](#postcss-configuration)

- [Security Implementation]()
  - [Content Security Policy](#content-security-policy)
    - [CSP Configuration]()
    - [Nonce Implementation]()
  - [Security Headers]()
    - [Apache Configuration]()
    - [Nginx Configuration](#server-configuration-nginx)
  - [TLS/SSL Configuration](#tlsssl-configuration)
    - [SSL Setup](#ssl-setup)
    - [Certificate Management]()
  - [Subresource Integrity]()
  - [Input Sanitization]()

- [Performance Monitoring](#performance-monitoring)
  - [Real User Monitoring](#real-user-monitoring-rum)
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
  - [HTML & SEO]()
  - [CSS & Performance](#css--performance)
  - [JavaScript & Functionality]()
  - [Accessibility & UX]()
  - [Security](#security)
  - [Performance](#performance)
  - [Testing & Monitoring]()
  - [Build & Deployment](#build--deployment)

---

## Project Structure

```bash
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
├── dist/
├── .nvmrc
├── package.json
└── README.md
```

---

## HTML Standards

### 1. Document Structure Requirements

#### 1.1 Base Template Specification

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

#### 1.2 Semantic HTML Requirements

- Use HTML5 semantic elements: `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`
- Implement proper heading hierarchy (h1 → h6)
- Single `<h1>` per page
- Unique `<title>` per page (50-60 characters)
- Unique meta descriptions (150-160 characters)

### 2. Accessibility (WCAG 2.1 AA Compliance)

#### 2.1 ARIA Implementation

```html
<!-- Navigation State -->
<nav aria-label="Primary">
  <a href="/" aria-current="page">Home</a>
  <a href="/about">About</a>
</nav>

<!-- Expandable Elements -->
<button aria-expanded="false" aria-controls="menu-items">
  Menu
</button>
<ul id="menu-items" hidden>
  <!-- Menu items -->
</ul>

<!-- Form Accessibility -->
<form>
  <label for="email">Email Address</label>
  <input 
    type="email" 
    id="email" 
    name="email"
    autocomplete="email"
    aria-required="true"
    aria-invalid="false"
    aria-describedby="email-error">
  <span id="email-error" role="alert" aria-live="polite"></span>
</form>

<!-- Decorative Icons -->
<svg aria-hidden="true" focusable="false">
  <!-- Icon content -->
</svg>
```

#### 2.2 Keyboard Navigation

- Implement logical tab order
- Visible focus indicators (minimum 2px outline)
- Skip links for keyboard navigation
- Trap focus in modals

### 3. Structured Data Implementation

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Company Name",
  "url": "https://domain.com",
  "logo": "https://domain.com/logo.png",
  "sameAs": [
    "https://facebook.com/company",
    "https://twitter.com/company"
  ],
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+55-11-99999-9999",
    "contactType": "customer service",
    "availableLanguage": "Portuguese"
  }
}
</script>

<!-- BreadcrumbList for hierarchical pages -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [{
    "@type": "ListItem",
    "position": 1,
    "name": "Home",
    "item": "https://domain.com"
  },{
    "@type": "ListItem",
    "position": 2,
    "name": "Category",
    "item": "https://domain.com/category"
  }]
}
</script>
```

---

## SEO and Indexing

### Required Files

#### robots.txt
```txt
User-agent: *
Disallow:
Sitemap: https://example.com/sitemap.xml
```

#### sitemap.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <lastmod>2025-09-01</lastmod>
  </url>
</urlset>
```

#### 404.html
```html
<main>
  <h1>Page not found (404)</h1>
  <p>Try the <a href="/">home page</a></p>
</main>
```

#### Server Configuration (nginx)
```nginx
error_page 404 /404.html;
location = /404.html { 
  internal; 
}
```

---

## CSS Architecture

### 1. ITCSS + BEM Methodology with CSS Layers

#### 1.1 Layer Structure

```css
/* main.css */
@layer reset, base, layout, components, utilities;

@import url('base/_reset.css') layer(reset);
@import url('base/_settings.css') layer(base);
@import url('layout/_grid.css') layer(layout);
@import url('components/_c-card.css') layer(components);
@import url('utilities/_u-spacing.css') layer(utilities);
```

#### 1.2 Design Tokens

```css
:root {
  /* Colors */
  --color-primary-100: hsl(220, 80%, 95%);
  --color-primary-500: hsl(220, 80%, 50%);
  --color-primary-900: hsl(220, 80%, 10%);
  
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
  
  /* Z-index Scale */
  --z-dropdown: 100;
  --z-sticky: 200;
  --z-overlay: 900;
  --z-modal: 1000;
  --z-tooltip: 1100;
  
  /* Transitions */
  --transition-fast: 150ms ease-in-out;
  --transition-base: 300ms ease-in-out;
  
  /* Breakpoints (for JS) */
  --breakpoint-sm: 640px;
  --breakpoint-md: 768px;
  --breakpoint-lg: 1024px;
  --breakpoint-xl: 1280px;
}
```

#### 1.3 BEM Naming Convention

```css
/* Block */
.c-card { }

/* Element */
.c-card__header { }
.c-card__body { }
.c-card__footer { }

/* Modifier */
.c-card--featured { }
.c-card--disabled { }

/* State (via separate class) */
.c-card.is-active { }
.c-card.is-loading { }
```

### 2. Responsive Design System

#### 2.1 Mobile-First Grid

```css
.l-grid {
  display: grid;
  gap: var(--spacing-md);
  grid-template-columns: repeat(auto-fit, minmax(min(300px, 100%), 1fr));
}

@media (min-width: 768px) {
  .l-grid--2-cols { grid-template-columns: repeat(2, 1fr); }
  .l-grid--3-cols { grid-template-columns: repeat(3, 1fr); }
  .l-grid--4-cols { grid-template-columns: repeat(4, 1fr); }
}
```

#### 2.2 Container Queries (Modern Approach)

```css
.c-card-container {
  container-type: inline-size;
}

@container (min-width: 400px) {
  .c-card {
    grid-template-columns: 150px 1fr;
  }
}
```

### 3. Performance CSS

#### 3.1 Critical CSS Strategy

```css
/* Inline in <head> - Above the fold styles only */
body { margin: 0; font-family: system-ui; }
.l-header { background: white; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
.l-hero { min-height: 60vh; display: flex; align-items: center; }
```

#### 3.2 Font Loading Optimization

```css
@font-face {
  font-family: 'CustomFont';
  src: url('/fonts/custom.woff2') format('woff2');
  font-display: swap;
  font-weight: 400;
  font-style: normal;
  size-adjust: 105%;
  ascent-override: 90%;
  descent-override: 10%;
  line-gap-override: 0%;
}
```

### 4. Dark Mode Implementation

```css
/* Automatic dark mode */
:root {
  color-scheme: light dark;
}

/* Custom properties for themes */
[data-theme="light"] {
  --color-bg: hsl(0, 0%, 100%);
  --color-text: hsl(0, 0%, 10%);
}

[data-theme="dark"] {
  --color-bg: hsl(0, 0%, 10%);
  --color-text: hsl(0, 0%, 90%);
}

/* Respect user preference */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --color-bg: hsl(0, 0%, 10%);
    --color-text: hsl(0, 0%, 90%);
  }
}
```

---

## JavaScript Guidelines

### 1. Modern ES6+ Standards

#### 1.1 Module Structure

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

#### 1.2 Component Class Pattern

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

### 2. Performance Optimization

#### 2.1 Lazy Loading Implementation

```javascript
// modules/LazyLoader.js
export class LazyLoader {
  constructor() {
    this.images = document.querySelectorAll('img[loading="lazy"]');
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
          const img = entry.target;
          img.src = img.dataset.src;
          img.classList.add('is-loaded');
          this.imageObserver.unobserve(img);
        }
      });
    }, {
      rootMargin: '50px 0px',
      threshold: 0.01
    });
    
    this.images.forEach(img => this.imageObserver.observe(img));
  }
}
```

#### 2.2 Debounce & Throttle Utilities

```javascript
// modules/utils.js
export function debounce(func, wait) {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}

export function throttle(func, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
```

### 3. Web Vitals Monitoring

```javascript
// modules/PerformanceMonitor.js
export class PerformanceMonitor {
  constructor() {
    this.initWebVitals();
    this.trackErrors();
  }

  async initWebVitals() {
    const { onLCP, onINP, onCLS, onFCP, onTTFB } = await import(
      'https://cdn.jsdelivr.net/npm/web-vitals@3/dist/web-vitals.iife.js'
    );
    
    const send = (metric) => {
      // For static sites: integrate with analytics provider or remove
      console.log('[web-vitals]', metric);
    };
    
    onLCP(send);
    onINP(send);
    onCLS(send);
    onFCP(send);
    onTTFB(send);
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
  }
}
```

### 4. Progressive Enhancement

```javascript
// Progressive form enhancement
class FormEnhancer {
  constructor(form) {
    this.form = form;
    this.init();
  }
  
  init() {
    // Works without JS
    this.form.addEventListener('submit', this.handleSubmit.bind(this));
    
    // Enhanced features
    this.addRealtimeValidation();
    this.addAutoSave();
  }
  
  async handleSubmit(e) {
    e.preventDefault();
    
    const formData = new FormData(this.form);
    
    try {
      const response = await fetch(this.form.action, {
        method: this.form.method,
        body: formData,
        headers: {
          'X-Requested-With': 'XMLHttpRequest'
        }
      });
      
      if (response.ok) {
        this.showSuccess();
      } else {
        this.showError();
      }
    } catch (error) {
      // Fallback to regular form submission
      this.form.submit();
    }
  }
  
  addRealtimeValidation() {
    const inputs = this.form.querySelectorAll('input, textarea, select');
    
    inputs.forEach(input => {
      input.addEventListener('blur', () => this.validateField(input));
    });
  }
  
  validateField(field) {
    const isValid = field.checkValidity();
    
    field.setAttribute('aria-invalid', !isValid);
    
    const errorEl = document.getElementById(field.getAttribute('aria-describedby'));
    if (errorEl) {
      errorEl.textContent = isValid ? '' : field.validationMessage;
    }
  }
  
  addAutoSave() {
    const saveData = debounce(() => {
      const data = new FormData(this.form);
      localStorage.setItem(`form-${this.form.id}`, JSON.stringify(Object.fromEntries(data)));
    }, 1000);
    
    this.form.addEventListener('input', saveData);
  }
}
```

---

## Performance Optimization

### 1. Image Optimization Strategy

#### 1.1 Responsive Images Implementation

```html
<picture>
  <!-- AVIF for cutting-edge browsers -->
  <source 
    type="image/avif"
    srcset="
      /img/hero-400w.avif 400w,
      /img/hero-800w.avif 800w,
      /img/hero-1200w.avif 1200w,
      /img/hero-1600w.avif 1600w"
    sizes="(max-width: 640px) 100vw, 
           (max-width: 1024px) 80vw, 
           1200px">
  
  <!-- WebP for modern browsers -->
  <source 
    type="image/webp"
    srcset="
      /img/hero-400w.webp 400w,
      /img/hero-800w.webp 800w,
      /img/hero-1200w.webp 1200w,
      /img/hero-1600w.webp 1600w"
    sizes="(max-width: 640px) 100vw, 
           (max-width: 1024px) 80vw, 
           1200px">
  
  <!-- JPEG fallback -->
  <img 
    src="/img/hero-800w.jpg"
    srcset="
      /img/hero-400w.jpg 400w,
      /img/hero-800w.jpg 800w,
      /img/hero-1200w.jpg 1200w"
    sizes="(max-width: 640px) 100vw, 
           (max-width: 1024px) 80vw, 
           1200px"
    alt="Hero image description"
    width="1200"
    height="600"
    loading="eager"
    fetchpriority="high"
    decoding="async">
</picture>
```

```css
## 1.1.1 CSS fallback in a single rule (simpler)

.hero-background {
  background-image: url("/img/bg.jpg"); /* fallback */
  background-image: image-set(
    url("/img/bg.avif") type("image/avif"),
    url("/img/bg.webp") type("image/webp"),
    url("/img/bg.jpg") type("image/jpeg")
  );
  background-size: cover;
  background-position: center;
}
```

# 1.2 Modern Image Formats Guide

A comprehensive guide for shipping optimized images with the smallest file sizes, acceptable quality, correct MIME types, and wide browser compatibility.

## Overview

**Goal:** Ship the smallest files with acceptable quality, correct MIME types, and wide compatibility.

**Fallback Strategy:** AVIF → WebP → JPEG/PNG (SVG for vectors)

## Format Priority

| Format | Best For | Browser Support | File Size |
|--------|----------|-----------------|-----------|
| **AVIF** | Photos, complex images | Modern browsers | Smallest |
| **WebP** | Universal fallback | Wide support | Small |
| **JPEG** | Photo compatibility | Universal | Medium |
| **PNG** | Transparency, crisp edges | Universal | Large |
| **SVG** | Vector graphics, icons | Universal | Variable |

## Use Cases

### 📸 Photographs
- **Primary:** AVIF
- **Fallback:** WebP
- **Last resort:** JPEG

### 🎨 Logos/Icons/Flat Illustrations
- **Preferred:** SVG
- **Alternative:** AVIF/WebP

### 🖥️ UI Screenshots/Crisp Edges
- **Primary:** AVIF (high quality)
- **Fallback:** PNG if artifacts appear

### 🎬 Animations
- **Short loops:** Animated AVIF/WebP
- **Long/complex:** Video (`.mp4`/`.webm`)

## Implementation Examples

### Responsive Photo with Picture Element

```html
<!-- Hero/Photo Implementation -->
<picture>
  <source type="image/avif"
          srcset="/img/hero-800.avif 800w, /img/hero-1200.avif 1200w"
          sizes="(max-width: 1024px) 90vw, 1200px">
  <source type="image/webp"
          srcset="/img/hero-800.webp 800w, /img/hero-1200.webp 1200w"
          sizes="(max-width: 1024px) 90vw, 1200px">
  <img src="/img/hero-1200.jpg"
       width="1200" height="600" alt="Hero image description"
       loading="eager" fetchpriority="high" decoding="async">
</picture>
```

### SVG Icons (Recommended)

```html
<!-- Inline SVG Icon -->
<svg aria-hidden="true" focusable="false" width="24" height="24">
  <use href="/icons.svg#check"></use>
</svg>
```

### CSS Background Images with Fallbacks

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

## Encoding Commands

### AVIF Encoding
```bash
# General purpose (good starting point)
avifenc input.jpg -q 32 -s 6 -y 420 -o output.avif

# High quality
avifenc input.jpg -q 20 -s 8 -y 444 -o output.avif

# Small file size
avifenc input.jpg -q 40 -s 4 -y 420 -o output.avif
```

### WebP Encoding
```bash
# Photos (lossy compression)
cwebp -q 80 input.jpg -o output.webp

# Graphics/logos (lossless compression)
cwebp -lossless -z 9 input.png -o output.webp

# With transparency
cwebp -q 80 -alpha_q 80 input.png -o output.webp
```

### Batch Processing Example
```bash
# Convert all JPEGs to AVIF and WebP
for img in *.jpg; do
  avifenc "$img" -q 32 -s 6 -y 420 -o "${img%.jpg}.avif"
  cwebp -q 80 "$img" -o "${img%.jpg}.webp"
done
```

## Server Configuration

### Nginx Configuration
```nginx
http {
  include /etc/nginx/mime.types;
  types {
    image/avif avif;
    image/webp webp;
  }
}

server {
  location ~* \.(avif|webp)$ {
    add_header Cache-Control "public, max-age=31536000, immutable";
    try_files $uri =404;
  }
}
```

### Apache Configuration
```apache
AddType image/avif .avif
AddType image/webp .webp

<IfModule mod_expires.c>
  ExpiresActive on
  ExpiresByType image/avif "access plus 1 year"
  ExpiresByType image/webp "access plus 1 year"
</IfModule>

<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE image/svg+xml
  SetEnvIfNoCase Request_URI "\.(avif|webp)$" no-gzip=1
</IfModule>
```

## Best Practices

### ✅ Authoring Rules

- **Export multiple widths** and serve with `<picture>` + `srcset`
- **Always set `width` and `height`** attributes to prevent Cumulative Layout Shift (CLS)
- **Include accurate `alt` text** for accessibility
- **Convert to sRGB** color space for web compatibility
- **Strip EXIF data** unless specifically required
- **Use cache-friendly filenames** with hashes for 1-year caching
- **Set HTML to no-cache** while images cache long-term

### 🎯 Performance Tips

- Use `loading="lazy"` for images below the fold
- Use `loading="eager"` and `fetchpriority="high"` for above-the-fold images
- Always include `decoding="async"` for better performance
- Consider using CSS `aspect-ratio` for responsive containers

### 📱 Responsive Considerations

```html
<!-- Responsive sizes attribute examples -->
sizes="100vw"                           <!-- Full width -->
sizes="(max-width: 768px) 100vw, 50vw"  <!-- Mobile full, desktop half -->
sizes="(max-width: 1024px) 90vw, 1200px" <!-- With max-width -->
```

### 🔍 Testing and Validation

- Test images in multiple browsers
- Validate MIME types are served correctly
- Check file sizes with network inspector
- Verify CLS scores don't increase
- Test with slow network connections

## Browser Support

| Format | Chrome | Firefox | Safari | Edge |
|--------|--------|---------|--------|------|
| AVIF   | 85+    | 93+     | 16.4+  | 85+  |
| WebP   | 32+    | 65+     | 14+    | 18+  |
| JPEG   | ✅     | ✅      | ✅     | ✅   |
| PNG    | ✅     | ✅      | ✅     | ✅   |
| SVG    | ✅     | ✅      | ✅     | ✅   |

---

## Contributing

Feel free to submit issues and enhancement requests! This guide aims to stay current with modern web standards and browser capabilities.

## License

This guide is released under the MIT License. Feel free to use and modify as needed.
### 2. Resource Hints & Preloading

```html
<head>
  <!-- DNS Prefetch for external domains -->
  <link rel="dns-prefetch" href="https://cdn.example.com">
  <link rel="dns-prefetch" href="https://analytics.example.com">
  
  <!-- Preconnect for critical origins -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  
  <!-- Preload critical resources -->
  <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
  <link rel="preload" href="/css/critical.css" as="style">
  <link rel="preload" href="/js/main.js" as="script">
  
  <!-- Prefetch next page resources -->
  <link rel="prefetch" href="/page2.html">
  <link rel="prefetch" href="/css/page2.css">
  
  <!-- Module preload for ES6 modules -->
  <link rel="modulepreload" href="/js/modules/critical.js">
</head>
```

### 3. Service Worker Implementation

```javascript
// sw.js
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
      return cache.addAll([
        '/',
        '/css/main.css',
        '/js/main.js',
        '/offline.html'
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
  self.clients.claim();
});

// Fetch strategies
self.addEventListener('fetch', (event) => {
  const { request } = event;
  const url = new URL(request.url);
  
  // Skip non-GET requests
  if (request.method !== 'GET') return;
  
  // HTML: Network first, fallback to cache
  if (request.headers.get('accept')?.includes('text/html')) {
    event.respondWith(
      fetch(request)
        .then((response) => {
          const responseClone = response.clone();
          caches.open(CACHE_NAMES.dynamic).then((cache) => {
            cache.put(request, responseClone);
          });
          return response;
        })
        .catch(() => caches.match(request))
        .catch(() => caches.match('/offline.html'))
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
```

### 4. Speculation Rules API

#### 4.1 External File Approach (Recommended)

```html
<head>
  <link rel="speculationrules" href="/speculation-rules.json">
</head>
```

Create `/speculation-rules.json`:

```json
{
  "prerender": [
    { "source": "list", "urls": ["/about", "/products", "/contact"] },
    {
      "source": "document",
      "where": {
        "and": [
          { "href_matches": "/*" },
          { "not": { "href_matches": "/admin/*" } },
          { "not": { "selector_matches": "[data-no-prerender]" } }
        ]
      },
      "eagerness": "moderate"
    }
  ],
  "prefetch": [
    { 
      "source": "document", 
      "where": { "selector_matches": "a[href]" }, 
      "eagerness": "conservative" 
    }
  ]
}
```

### 5. Build Configuration

#### 5.1 Vite Configuration

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import { createHtmlPlugin } from 'vite-plugin-html';
import viteCompression from 'vite-plugin-compression';
import viteImagemin from 'vite-plugin-imagemin';

export default defineConfig({
  root: 'src',
  build: {
    outDir: '../dist',
    emptyOutDir: true,
    rollupOptions: {
      input: { 
        main: 'src/index.html', 
        about: 'src/about.html' 
      },
      output: {
        assetFileNames: 'assets/[name]-[hash][extname]',
        chunkFileNames: 'js/[name]-[hash].js',
        entryFileNames: 'js/[name]-[hash].js'
      }
    },
    minify: 'terser',
    terserOptions: { 
      compress: { 
        drop_console: true, 
        drop_debugger: true 
      } 
    },
    cssMinify: true,
    assetsInlineLimit: 4096,
    reportCompressedSize: true
  },
  plugins: [
    createHtmlPlugin({ minify: true }),
    viteCompression({ algorithm: 'brotliCompress', ext: '.br' }),
    viteCompression({ algorithm: 'gzip', ext: '.gz' }),
    viteImagemin({
      gifsicle: { optimizationLevel: 3 },
      optipng: { optimizationLevel: 5 },
      mozjpeg: { quality: 75 },
      pngquant: { quality: [0.65, 0.9], speed: 4 },
      svgo: { 
        plugins: [
          { name: 'removeViewBox', active: false },
          { name: 'removeEmptyAttrs', active: true }
        ] 
      },
      webp: { quality: 75 },
      avif: { quality: 50 }
    })
  ],
  css: { postcss: './postcss.config.js' },
  server: { port: 3000, https: true, open: true },
  preview: { port: 8080, https: true }
});
```

## PostCSS Configuration

### 5.2 PostCSS Configuration

```javascript
// postcss.config.js
import postcssPresetEnv from 'postcss-preset-env';
import autoprefixer from 'autoprefixer';
import cssnano from 'cssnano';
import purgecss from '@fullhuman/postcss-purgecss';

export default {
    plugins: [
        postcssPresetEnv({
            stage: 2,
            features: {
                'nesting-rules': true,
                'custom-properties': true,
                'custom-media-queries': true,
                'has-pseudo-class': true,
                'gap-properties': true,
                'overflow-wrap-property': true
            }
        }),
        
        autoprefixer({
            grid: 'autoplace'
        }),
        
        ...(process.env.NODE_ENV === 'production' ? [
            purgecss({
                content: ['./src/**/*.html', './src/**/*.js'],
                safelist: {
                    standard: [/^is-/, /^has-/, /^js-/],
                    deep: [/^modal/, /^tooltip/],
                    greedy: [/^swiper/]
                }
            }),
            
            cssnano({
                preset: ['advanced', {
                    discardComments: { removeAll: true },
                    reduceIdents: true,
                    mergeIdents: true,
                    discardUnused: true,
                    minifySelectors: true,
                    minifyParams: true,
                    minifyFontValues: true,
                    normalizeUrl: true,
                    colormin: true
                }]
            })
        ] : [])
    ]
};
```

### 5.3 Reinforced PurgeCSS Safelist

```javascript
// postcss.config.js (PurgeCSS section)
purgecss({
  content: ['./src/**/*.html', './src/**/*.js'],
  safelist: {
    standard: [/^is-/, /^has-/, /^u-/, /^c-/, /^l-/, /^js-/],
    deep: [/^modal/, /^tooltip/, /^toast/],
    greedy: [/^swiper/]
  }
})
```

---

## Build & Deployment

### 6.1 Versioned Assets & Caching Strategy

```nginx
# CDN configuration with Brotli/HTTP3 enabled
# CI/CD pipeline: build → tests (lint/a11y/LHCI) → deploy → cache purge (e.g., Cloudflare)

location ~* \.(css|js|png|jpg|svg|woff2)$ {
  add_header Cache-Control "public, max-age=31536000, immutable";
}

location ~* \.(html)$ {
  add_header Cache-Control "no-cache";
}
```

### 6.2 Build Script Configuration

```json
{
  "scripts": {
    "build": "npm run clean && npm run build:css && npm run build:js && npm run build:html",
    "build:css": "postcss src/css/main.css -o dist/css/main.css",
    "build:js": "esbuild src/js/main.js --bundle --minify --outfile=dist/js/main.js",
    "build:html": "node scripts/build-html.js",
    "clean": "rimraf dist",
    "serve": "serve dist -p 3000",
    "preview": "npm run build && npm run serve"
  }
}
```

---

## Quality Assurance

### 1. Testing Configuration

#### 1.1 Jest Unit Testing

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

**Example Test:**

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

#### 1.2 Playwright E2E Testing

```javascript
// playwright.config.js
export default {
    testDir: './tests/e2e',
    timeout: 30000,
    fullyParallel: true,
    forbidOnly: !!process.env.CI,
    retries: process.env.CI ? 2 : 0,
    workers: process.env.CI ? 1 : undefined,
    reporter: 'html',
    use: {
        baseURL: 'http://localhost:3000',
        trace: 'on-first-retry',
        screenshot: 'only-on-failure'
    },
    projects: [
        {
            name: 'chromium',
            use: { ...devices['Desktop Chrome'] }
        },
        {
            name: 'firefox',
            use: { ...devices['Desktop Firefox'] }
        },
        {
            name: 'webkit',
            use: { ...devices['Desktop Safari'] }
        },
        {
            name: 'Mobile Chrome',
            use: { ...devices['Pixel 5'] }
        },
        {
            name: 'Mobile Safari',
            use: { ...devices['iPhone 12'] }
        }
    ],
    webServer: {
        command: 'npm run preview',
        port: 3000,
        reuseExistingServer: !process.env.CI
    }
};
```

**Example E2E Test:**

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

### 2. Performance Budget

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

## Performance Monitoring

### Real User Monitoring (RUM)

```javascript
// monitoring/rum.js
class RealUserMonitoring {
    constructor() {
        this.metrics = {};
        this.init();
    }
    
    init() {
        // Navigation Timing
        if (window.performance && performance.timing) {
            window.addEventListener('load', () => {
                const timing = performance.timing;
                this.metrics.pageLoadTime = timing.loadEventEnd - timing.navigationStart;
                this.metrics.domContentLoaded = timing.domContentLoadedEventEnd - timing.navigationStart;
                this.metrics.ttfb = timing.responseStart - timing.navigationStart;
                this.sendMetrics();
            });
        }
        
        // Core Web Vitals
        if ('web-vitals' in window) {
            import('https://unpkg.com/web-vitals/dist/web-vitals.js').then(({ onCLS, onINP, onLCP }) => {
                onCLS(metric => this.recordMetric('CLS', metric));
                onINP(metric => this.recordMetric('INP', metric));
                onLCP(metric => this.recordMetric('LCP', metric));
            });
        }
        
        // JavaScript Errors
        window.addEventListener('error', (event) => {
            this.recordError({
                message: event.message,
                source: event.filename,
                lineno: event.lineno,
                colno: event.colno,
                stack: event.error?.stack
            });
        });
        
        // Resource Performance
        if (window.PerformanceObserver) {
            const observer = new PerformanceObserver((list) => {
                for (const entry of list.getEntries()) {
                    if (entry.entryType === 'resource') {
                        this.recordResourceTiming(entry);
                    }
                }
            });
            observer.observe({ entryTypes: ['resource'] });
        }
    }
    
    recordMetric(name, metric) {
        this.metrics[name] = {
            value: metric.value,
            delta: metric.delta,
            id: metric.id
        };
        this.sendMetrics();
    }
    
    recordError(error) {
        fetch('/api/errors', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                ...error,
                url: window.location.href,
                userAgent: navigator.userAgent,
                timestamp: new Date().toISOString()
            })
        });
    }
    
    recordResourceTiming(entry) {
        if (entry.duration > 1000) { // Log slow resources
            this.metrics[`slow_resource_${entry.name}`] = {
                duration: entry.duration,
                size: entry.transferSize
            };
        }
    }
    
    sendMetrics() {
        if (navigator.sendBeacon) {
            navigator.sendBeacon('/api/metrics', JSON.stringify({
                metrics: this.metrics,
                url: window.location.href,
                timestamp: new Date().toISOString()
            }));
        }
    }
}

// Initialize monitoring
new RealUserMonitoring();
```

### Google Analytics 4 (CSP Compatible)

```html
<!-- GA4 with CSP nonce -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXX" nonce="{NONCE}"></script>
<script nonce="{NONCE}">
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXX');
</script>
```

### Speculation Rules API

```html
<link rel="speculationrules" href="/speculation-rules.json">
```

```json
// speculation-rules.json
{
  "prerender": [
    {
      "source": "list",
      "urls": ["/about", "/products", "/contact"]
    }
  ],
  "prefetch": [
    {
      "source": "document",
      "where": {
        "selector_matches": "a[href]"
      },
      "eagerness": "conservative"
    }
  ]
}
```

---

## 📚 Additional Resources

### Validation Tools

- [W3C HTML Validator](https://validator.w3.org/)
- [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
- [WAVE Accessibility Checker](https://wave.webaim.org/)
- [Google PageSpeed Insights](https://pagespeed.web.dev/)
- [WebPageTest](https://www.webpagetest.org/)

### Performance Testing

- [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
- [Core Web Vitals Chrome Extension](https://chrome.google.com/webstore/detail/web-vitals/)
- [Chrome DevTools Performance Panel](https://developer.chrome.com/docs/devtools/evaluate-performance/)

### Security Auditing

- [Mozilla Observatory](https://observatory.mozilla.org/)
- [Security Headers](https://securityheaders.com/)
- [SSL Labs](https://www.ssllabs.com/ssltest/)

### Documentation

- [MDN Web Docs](https://developer.mozilla.org/)
- [Can I Use](https://caniuse.com/)
- [web.dev](https://web.dev/)

---

## 🎯 Production Checklist

### Code Quality
- [ ] All HTML validated
- [ ] All CSS validated
- [ ] JavaScript linted without errors
- [ ] TypeScript compiled without errors (if applicable)

### Performance
- [ ] Lighthouse score > 95 on all metrics
- [ ] Core Web Vitals within recommended thresholds
- [ ] Performance budget met
- [ ] Images optimized and properly sized
- [ ] Critical CSS inlined
- [ ] JavaScript bundles optimized

### Accessibility
- [ ] WCAG 2.1 AA compliance verified
- [ ] Screen reader tested
- [ ] Keyboard navigation functional
- [ ] Color contrast ratios validated
- [ ] Alt text for all images

### Security
- [ ] Security headers configured
- [ ] SSL certificate valid and configured
- [ ] CSP (Content Security Policy) implemented
- [ ] No mixed content warnings

### SEO & Metadata
- [ ] Sitemap.xml generated and submitted
- [ ] Robots.txt configured
- [ ] Meta descriptions for all pages
- [ ] Open Graph images created (1200x630)
- [ ] Schema.org markup implemented
- [ ] Canonical URLs set

### Progressive Web App
- [ ] Service Worker registered
- [ ] Manifest.json configured
- [ ] Offline functionality tested
- [ ] Add to homescreen prompt working

### Monitoring & Analytics
- [ ] Analytics/monitoring configured
- [ ] Error tracking implemented
- [ ] Performance monitoring active
- [ ] Search Console configured

### Infrastructure
- [ ] CDN configured and tested
- [ ] Backup strategy implemented
- [ ] 404 page created and styled
- [ ] Favicons for all platforms generated

### Testing
- [ ] Cross-browser tested (Chrome, Firefox, Safari, Edge)
- [ ] Mobile responsive verified
- [ ] Forms tested and validated
- [ ] All interactive elements tested

### Documentation
- [ ] README updated with project information
- [ ] Code documented appropriately
- [ ] Deployment instructions documented
- [ ] Environment variables documented

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd <project-name>
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   ```

4. **Build for production**
   ```bash
   npm run build
   ```

5. **Preview production build**
   ```bash
   npm run preview
   ```

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

*This README serves as the comprehensive technical specification for static site development following industry best practices and modern web standards.*
