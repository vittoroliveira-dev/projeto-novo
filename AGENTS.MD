```text
ROLE
You are a product designer + front-end developer. Generate a STATIC MPA in Brazilian Portuguese that sells “Landing Pages with Guaranteed Speed” for paid traffic. Production-ready code. All on-page copy MUST be written in Brazilian Portuguese (pt-BR).

REPOSITORY & STANDARDS
Apply standard ITCSS+BEM best practices. If the repository README.md exists, use it as additional guidance for architecture, checklists, and coding conventions (do not copy marketing text).

UI REFERENCES (ADAPT TO VANILLA)
You MAY adapt UI patterns/micro-interactions from:
- https://uiverse.io/ • https://reactbits.dev/ • https://www.hover.dev/
- https://pagedone.io/ • https://www.cssportal.com/
Port everything to vanilla HTML/CSS/JS. No framework dependencies.

BRAZIL-FOCUSED SEO & COPY (MANDATORY)
- Language: write all content in **pt-BR**; set `<html lang="pt-BR">`, OG `locale` = `pt_BR`, JSON-LD `"inLanguage": "pt-BR"`.
- Targeting: Brazil-specific keywords; currency **R$**; Brazilian phone/date formats; LGPD mention in /privacy.
- Hreflang: `pt-BR` (and only others if provided); canonical URLs consistent with BR site.

POSITIONING (PUBLIC COPY)
Headline: “LP rápida vende mais.”
Sub: “PSI mobile 85+ garantido. Mais cliques que viram clientes.”
Bullets: “LCP ≤ 3,0 s • INP < 200 ms • CLS < 0,1 • Entrega em até 5 dias”
CTAs: “Pedir diagnóstico de velocidade”, “Ver antes/depois”

COPYWRITING TONE OF VOICE
Write in a direct, confident, educational tone. Audience: business owners and marketing managers using paid traffic, not necessarily technical. Explain LCP/INP/CLS in simple terms tied to business outcomes (mais conversões, menor custo por lead). Be persuasive but credible.

PAGES (MPA)
/ (Home) — promise, proof, CTAs, guarantee, “tested on real devices” badges
/cases/ — verifiable before/after, PSI/CrUX links, LCP/INP/CLS chips
/plans/ — 2-offer table, change policy, strong CTAs
/services/ — technical process in business language; what we do / don’t do
/process/ — 5-step timeline + test matrix (MVP scope below)
/niche-ads/ — simple ROI (+10–20% conversion with LCP ≤ 3,0 s), numeric example
/faq/ — autonomia, garantia, solicitações, prazos, manutenção, “quando WP é melhor?”
/contact/ — lead form (nome, e-mail, site, objetivo da campanha, orçamento)
/about/ — autoridade, princípios, métricas Lighthouse recentes
/privacy/ — LGPD, consent mode, contato do DPO

ARCHITECTURE & STYLE
- HTML: no inline style/on*; semantic landmarks; coherent H1–H2.
- CSS: ITCSS + BEM; `main.css` with `@layer base, layout, components, utilities, enhancements`; tokens in `base/_settings.css`.
- JS: ES Modules; ship less JS; no jQuery/Bootstrap/carousels.
- Visual Style: minimalist, clean, professional. Ample white space. Convey technology, speed, and reliability. High legibility. Avoid decorative elements without functional purpose.

COLOR TOKENS (Clean Efficiency)
:root{
  --c-primary:#1e40af; --c-primary-hover:#1e3a8a;
  --c-secondary:#059669; --c-secondary-hover:#047857;
  --c-text:#111827; --c-text-muted:#475569;
  --c-bg:#ffffff; --c-bg-alt:#f3f4f6; --c-border:#e5e7eb; --c-focus:#1e40af;
  --c-danger:#dc2626; --c-warn:#f59e0b; --c-success:#10b981;
  --score-low:#ef4444; --score-mid:#f59e0b; --score-high:#10b981;
}
@media (prefers-color-scheme: dark){
  :root{ --c-bg:#0f172a; --c-bg-alt:#111827; --c-text:#f8fafc; --c-text-muted:#cbd5e1; --c-border:#1f2937; }
}

VISUAL ASSETS
Use a consistent, lightweight SVG icon set (e.g., Heroicons/Feather). Optimize SVGs (remove metadata, inline where appropriate). Images: high-quality abstract tech/speed/data visuals (e.g., Unsplash), optimized to meet the performance budget. Clearly mark placeholder images for case studies.

RESPONSIVENESS & ENHANCEMENTS
Baseline (Tier B/C): mobile-first with `@media`; nested grid/flex; fluid type via `clamp()`. Fully functional without modern features.
Enhancements (Tier A) gated by `@supports` in `@layer enhancements`:
- Container Queries (`container-type:inline-size`) for fine layout tweaks
- Subgrid to align metrics/cases (when supported)
- Scroll-driven animations + View Transitions with IntersectionObserver fallback
No heavy polyfills.

PERFORMANCE BUDGET & CRITERIA
- Targets: **LCP ≤ 3.0 s • INP < 200 ms • CLS < 0.1 • JS ≤ 60 kB gzip**
- **Critical CSS scope: hero + primary navigation ≤ 8 kB** (includes basic font/icon styles). Load the rest via a preloaded stylesheet.
- Preload hero image (AVIF/WEBP), preconnect fonts, variable fonts with `font-display: swap`.
- Images: AVIF/WEBP + `srcset/sizes`; `loading="lazy"`, `decoding="async"`.
- Resource hints: preconnect, dns-prefetch, preload only when it benefits LCP.
- No live PSI calls on client; link out to PSI/CrUX.

COMPONENT GUIDELINES
- c-hero “speed-loader”: lightweight CSS transforms/opacity only; must respect `prefers-reduced-motion` (reduce to static state); no layout thrash.
- c-case before/after slider: MUST be keyboard accessible and ARIA-labeled; do NOT rely on checkbox hacks. Prefer `<input type="range">` with visible handle and labels; if pure-CSS compromises a11y, use minimal JS, initializing only when visible (IntersectionObserver).
- c-plans: responsive cards; CQ-gated enhancements only.
- c-cta: strong focus/hover states; minimum 44px target size.

FORMS (CHOICE CRITERIA)
- Use **Formspree (free tier)** by default, with `fetch` POST and graceful `action` fallback (progressive enhancement).
- Include honeypot, basic validation, `aria-live` status, server error handling.
- If a self-hosted/edge form is required, note in README (out of MVP scope).

SERVICE WORKER (WHEN TO USE)
- Implement **only if the client explicitly requests offline capability**.
- Scope: cache **images only**; register **after** `window.load`; must not affect LCP; use `skipWaiting`/`clientsClaim`; document uninstall. Do **not** cache HTML.

ACCESSIBILITY
- WCAG 2.1 AA: visible focus, labels, correct `aria-*`, full keyboard support, `prefers-reduced-motion`.
- Plans table with proper headers/scope; /faq accordion with `aria-controls`/`aria-expanded`.
- Contrast AA (4.5:1 body text; 3:1 large text).

TECHNICAL SEO & STRUCTURED DATA
- `<html lang="pt-BR">`, unique `<title>` and `<meta name="description">` in pt-BR.
- `rel=canonical`, OG/Twitter, favicon; OG `locale` = `pt_BR`.
- `robots.txt`, `sitemap.xml`, `404.html`.
- JSON-LD: Organization, WebSite, ProfessionalService, FAQPage, BreadcrumbList; include `"inLanguage": "pt-BR"`.

BUILD & CI
- Vite + PostCSS (`postcss-preset-env` stage 1, `cssnano` advanced, `postcss-sort-media-queries`)
- Lighthouse CI mobile (4G throttling: 150 ms RTT, 1.6 Mbps). Gates: performance ≥ 0.90, accessibility ≥ 0.90, best-practices ≥ 0.95
- Security headers documented in README: HSTS, CSP, `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin`

TESTING STRATEGY (MVP → SCALE)
MVP:
- Daily: Chrome/Firefox desktop + Chrome DevTools mobile simulation (throttled).
- Validation: **one real Android device** (borrowed/personal) for sanity and LCP.
Scale after 5+ successful projects:
- Add BrowserStack matrix (Android 8/9/10, iOS 15/16/17, Edge/Chrome/Firefox/Safari desktop).

OFFERS & GUARANTEE (PUBLIC)
- LP Garantida (Ads): R$ 1.500 • 5 dias • 4 solicitações/mês por 3 meses
- Mini-funil (LP + Obrigado + Sobre): R$ 3.000 • 10 dias • 4 solicitações/mês por 3 meses
“Alterações razoáveis”: textos, imagens, contatos, CTA, 1 bloco simples existente. Exclui: página nova, redesign, integrações.
SLA: 48 h úteis. Acúmulo: 30 dias (máx. 8 abertas).
Guarantee: Mobile PSI ≥ 85 within 48 h after go-live; SLO LCP ≤ 3.0 s, INP < 200 ms, CLS < 0.1. Up to 2 remediation cycles; if still < 80, refund 10%.
Public exclusions: heavy third-party scripts/embeds, media > 1 MB above the fold, non-recommended hosting, post-acceptance changes.

LAUNCH STRATEGY
- Deliver **1 free LP** to a local business as a case study.
- Document PSI before/after during development.
- Use your **own portfolio site** as the first proof of concept.
- After 5+ validated deliveries, expand testing matrix and pricing.

DELIVERABLES
- HTML/CSS/JS for all pages; tokens; **critical CSS (hero+nav ≤ 8 kB)**; resource hints
- Plans table, change policy, and guarantee as public sections
- Cases with placeholder images + editable external PSI/CrUX links
- README with build/deploy, security headers, MVP testing plan, and CI gates
- No inline style/on*; no forbidden libraries; meet performance targets

PRIORITIES
P0: works on all devices (baseline), strong CWV, AA accessibility.
P1: modern enhancements where supported.
P2: micro-animations and cosmetics.

FINAL INSTRUCTION
Follow this prompt. Apply standard ITCSS+BEM practices; if our repository README.md exists, use it as additional guidance. For UI ideas, adapt from uiverse.io, reactbits.dev, hover.dev, pagedone.io, and cssportal.com to vanilla HTML/CSS/JS while preserving performance, accessibility, and **Brazil-focused SEO in pt-BR**.
```
