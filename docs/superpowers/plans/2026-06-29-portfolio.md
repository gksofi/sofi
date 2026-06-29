# Sofia Garcia Katz — Portfolio Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single `index.html` portfolio file driven by a JS data object — no build tools, deployable to GitHub Pages, printable as PDF.

**Architecture:** One HTML file. A `const PORTFOLIO_DATA` block at the top holds all user-editable content. Render functions at the bottom read from the data object and write HTML into pre-existing section containers on `DOMContentLoaded`. The modal slideshow is the only interactive component. A `@media print` block handles PDF export.

**Tech Stack:** Vanilla HTML/CSS/JS, Google Fonts CDN (`Space Grotesk` + `Inter`), no dependencies.

## Global Constraints

- No build tools, no npm, no frameworks — single `index.html` + `media/` folder
- Fonts via `https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700;800&family=Inter:wght@400;500&display=swap`
- Color palette — CSS custom properties on `:root`:
  - `--navy: #0D1B2A` · `--navy2: #122333` · `--navy3: #1A2F42`
  - `--coral: #FF6B6B` · `--sky: #6BCBEA` · `--violet: #C77DFF` · `--yellow: #FFD93D`
  - `--white: #F4F8FB` · `--muted: #8AA0B4` · `--border: #1E3048`
- Typography: `Space Grotesk` for all headings/titles, `Inter` for body/UI
- Visual verification after every task — open `index.html` directly in browser (no server needed)
- Approved mockup for visual reference: `brainstorm/full-mockup-v3.html`

---

## File Map

| File | Responsibility |
|---|---|
| `index.html` | Entire portfolio — data object, CSS, HTML, JS |
| `media/` | All user media (images, videos) |
| `media/motion/` | Motion graphics / video editing pieces |
| `media/graphic/` | Graphic design pieces |
| `media/social/` | Social media pieces |
| `EDITING-GUIDE.md` | Plain-English guide for Sofia to update content |

---

## Task 1: HTML scaffold + full CSS + PORTFOLIO_DATA

**Files:**
- Create: `index.html`
- Create: `media/.gitkeep`, `media/motion/.gitkeep`, `media/graphic/.gitkeep`, `media/social/.gitkeep`

**Produces:** `PORTFOLIO_DATA` constant consumed by all render functions in Tasks 2–5. Empty section shells that render functions will populate.

- [ ] **Step 1: Create the media folder structure**

```bash
mkdir -p media/motion media/graphic media/social
touch media/.gitkeep media/motion/.gitkeep media/graphic/.gitkeep media/social/.gitkeep
```

- [ ] **Step 2: Create `index.html` with full content**

Write the complete file below. It contains: Google Fonts link, all CSS, `PORTFOLIO_DATA`, empty section shells, modal HTML, and an empty `<script>` block (render functions added in Task 2+).

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sofia Garcia Katz — Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700;800&family=Inter:wght@400;500&display=swap" rel="stylesheet">
<style>
/* ── RESET ───────────────────────────────── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

/* ── TOKENS ──────────────────────────────── */
:root {
  --navy:   #0D1B2A;
  --navy2:  #122333;
  --navy3:  #1A2F42;
  --coral:  #FF6B6B;
  --sky:    #6BCBEA;
  --violet: #C77DFF;
  --yellow: #FFD93D;
  --white:  #F4F8FB;
  --muted:  #8AA0B4;
  --border: #1E3048;
}

/* ── BASE ────────────────────────────────── */
body {
  font-family: 'Inter', system-ui, sans-serif;
  background: var(--navy);
  color: var(--white);
  overflow-x: hidden;
}
a { color: inherit; text-decoration: none; }

/* ── NAV ─────────────────────────────────── */
#nav {
  position: sticky; top: 0; z-index: 100;
  background: rgba(13,27,42,0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border);
  display: flex; justify-content: space-between; align-items: center;
  padding: 0 60px; height: 64px;
}
.nav-logo {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 800; font-size: 20px; letter-spacing: -0.5px;
}
.nav-logo span { color: var(--coral); }
.nav-links { display: flex; gap: 36px; flex-wrap: wrap; }
.nav-links a {
  font-size: 13px; font-weight: 500; letter-spacing: 1.5px;
  text-transform: uppercase; color: var(--muted); transition: color 0.2s;
}
.nav-links a:hover { color: var(--yellow); }

/* ── HERO ────────────────────────────────── */
#hero {
  min-height: 100vh;
  display: flex; flex-direction: column; justify-content: center;
  padding: 100px 60px 80px;
  position: relative; overflow: hidden;
}
.hero-bg-accent {
  position: absolute; top: -80px; right: -80px;
  width: 500px; height: 500px; border-radius: 50%;
  background: radial-gradient(circle, rgba(199,125,255,0.12) 0%, transparent 70%);
  pointer-events: none;
}
.hero-bg-accent2 {
  position: absolute; bottom: 40px; left: -100px;
  width: 400px; height: 400px; border-radius: 50%;
  background: radial-gradient(circle, rgba(107,203,234,0.08) 0%, transparent 70%);
  pointer-events: none;
}
.hero-eyebrow {
  font-size: 12px; font-weight: 700; letter-spacing: 4px;
  text-transform: uppercase; color: var(--sky); margin-bottom: 20px;
  display: flex; align-items: center; gap: 12px;
}
.hero-eyebrow::before { content: ''; width: 40px; height: 2px; background: var(--sky); }
.hero-name {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 800; font-size: clamp(52px, 8vw, 110px);
  line-height: 0.95; letter-spacing: -3px; max-width: 900px;
}
.accent-coral { color: var(--coral); }
.accent-yellow { color: var(--yellow); }
.hero-tagline {
  margin-top: 32px; font-size: 18px; color: var(--muted);
  max-width: 520px; line-height: 1.6;
}
.hero-cta { margin-top: 48px; display: flex; gap: 16px; flex-wrap: wrap; }
.btn-primary {
  background: var(--coral); color: #fff;
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700; font-size: 13px; letter-spacing: 1px;
  text-transform: uppercase; padding: 14px 32px; border-radius: 4px;
}
.btn-outline {
  border: 2px solid var(--muted); color: var(--muted);
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700; font-size: 13px; letter-spacing: 1px;
  text-transform: uppercase; padding: 12px 32px; border-radius: 4px;
  background: none;
}
.hero-scroll-hint {
  position: absolute; bottom: 40px; left: 60px;
  font-size: 11px; letter-spacing: 2px; text-transform: uppercase;
  color: var(--muted); display: flex; align-items: center; gap: 12px;
}
.hero-scroll-hint::after { content: ''; width: 60px; height: 1px; background: var(--muted); }

/* ── SECTIONS — COMMON ───────────────────── */
section { padding: 100px 60px; }
.section-eyebrow {
  font-size: 11px; font-weight: 700; letter-spacing: 4px;
  text-transform: uppercase; margin-bottom: 12px;
  display: flex; align-items: center; gap: 12px;
}
.section-eyebrow::before { content: ''; width: 32px; height: 2px; }
.section-title {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 800; font-size: clamp(32px, 4vw, 52px);
  letter-spacing: -1px; line-height: 1.05; margin-bottom: 48px;
}

/* ── ABOUT ───────────────────────────────── */
#about { background: var(--navy2); border-top: 1px solid var(--border); }
#about .section-eyebrow { color: var(--yellow); }
#about .section-eyebrow::before { background: var(--yellow); }
.about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; }
.about-bio { font-size: 17px; color: var(--muted); line-height: 1.75; }
.about-bio strong { color: var(--white); }
.about-sidebar { display: flex; flex-direction: column; gap: 20px; }
.detail-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.detail-cell {
  background: var(--navy3); border-radius: 8px;
  padding: 16px 18px; border-top: 3px solid;
}
.detail-label {
  font-size: 10px; font-weight: 700; letter-spacing: 2px;
  text-transform: uppercase; margin-bottom: 7px;
}
.detail-value { font-size: 14px; color: var(--white); font-weight: 600; line-height: 1.4; }
.detail-sub { font-size: 12px; color: var(--muted); margin-top: 3px; line-height: 1.4; }
.award-card {
  background: var(--navy3); border-radius: 8px;
  border: 1px solid rgba(255,217,61,0.25); overflow: hidden;
}
.award-card-inner { display: flex; }
.award-logo {
  width: 96px; flex-shrink: 0;
  background: rgba(255,217,61,0.06);
  border-right: 1px solid rgba(255,217,61,0.15);
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  gap: 8px; padding: 20px 10px;
}
.award-logo-placeholder {
  width: 52px; height: 52px; border-radius: 8px;
  border: 2px dashed rgba(255,217,61,0.3);
  display: flex; align-items: center; justify-content: center; font-size: 22px;
}
.award-logo-hint {
  font-size: 9px; text-align: center; color: rgba(255,217,61,0.4);
  letter-spacing: 0.5px; line-height: 1.4;
}
.award-content { flex: 1; padding: 20px 22px; }
.award-eyebrow {
  font-size: 10px; font-weight: 700; letter-spacing: 2px;
  text-transform: uppercase; color: var(--yellow); margin-bottom: 8px;
  display: flex; align-items: center; gap: 8px;
}
.award-eyebrow::before { content: '🏆'; font-size: 13px; }
.award-title {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700; font-size: 15px; color: var(--white);
  line-height: 1.35; margin-bottom: 6px;
}
.award-sub { font-size: 12px; color: var(--muted); margin-bottom: 14px; }
.award-link {
  display: inline-flex; align-items: center; gap: 5px;
  font-size: 11px; font-weight: 700; letter-spacing: 1px;
  text-transform: uppercase; color: var(--yellow);
  border-bottom: 1px solid rgba(255,217,61,0.3); padding-bottom: 1px;
}
.award-link::after { content: '↗'; }
.award-link:hover { color: var(--white); }

/* ── EXPERIENCE ──────────────────────────── */
#experience { background: var(--navy); border-top: 1px solid var(--border); }
#experience .section-eyebrow { color: var(--violet); }
#experience .section-eyebrow::before { background: var(--violet); }
.exp-list { display: flex; flex-direction: column; }
.exp-item {
  display: grid; grid-template-columns: 200px 1fr;
  gap: 40px; padding: 36px 0; border-bottom: 1px solid var(--border);
}
.exp-period { font-size: 13px; color: var(--muted); font-weight: 500; padding-top: 6px; }
.exp-role {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700; font-size: 20px; margin-bottom: 4px;
}
.exp-company { font-size: 14px; color: var(--violet); font-weight: 500; margin-bottom: 10px; }
.exp-desc { font-size: 14px; color: var(--muted); line-height: 1.65; }

/* ── REEL ────────────────────────────────── */
#reel {
  background: #060e17; border-top: 1px solid var(--border);
  padding: 80px 60px;
}
#reel .section-eyebrow { color: var(--coral); }
#reel .section-eyebrow::before { background: var(--coral); }
.reel-heading {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 800; font-size: clamp(28px, 3.5vw, 44px);
  letter-spacing: -1px; margin-bottom: 36px;
}
.reel-heading span { color: var(--coral); }
.reel-container {
  width: 100%; aspect-ratio: 16 / 7;
  background: #0a1520; border-radius: 12px;
  border: 1px solid var(--border);
  position: relative; overflow: hidden;
  display: flex; align-items: center; justify-content: center;
}
.reel-container::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(135deg, rgba(255,107,107,0.06) 0%, transparent 40%),
              linear-gradient(315deg, rgba(199,125,255,0.06) 0%, transparent 40%);
  pointer-events: none;
}
.reel-play-wrap {
  display: flex; flex-direction: column; align-items: center; gap: 20px; z-index: 1;
}
.reel-play-btn {
  width: 80px; height: 80px; border-radius: 50%;
  background: var(--coral);
  display: flex; align-items: center; justify-content: center;
  font-size: 28px; color: #fff;
  box-shadow: 0 0 0 16px rgba(255,107,107,0.12), 0 0 0 32px rgba(255,107,107,0.05);
}
.reel-play-label {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700; font-size: 14px; letter-spacing: 3px;
  text-transform: uppercase; color: var(--muted);
}
.reel-duration {
  position: absolute; bottom: 20px; right: 24px;
  font-size: 12px; color: var(--muted); letter-spacing: 1px;
  background: rgba(6,14,23,0.8); padding: 4px 12px; border-radius: 20px;
}

/* ── WORK SECTIONS ───────────────────────── */
.work-section { border-top: 1px solid var(--border); }
#motion  { background: var(--navy2); }
#graphic { background: var(--navy);  }
#social  { background: var(--navy2); }
#motion  .section-eyebrow { color: var(--coral); }
#motion  .section-eyebrow::before { background: var(--coral); }
#graphic .section-eyebrow { color: var(--sky); }
#graphic .section-eyebrow::before { background: var(--sky); }
#social  .section-eyebrow { color: var(--violet); }
#social  .section-eyebrow::before { background: var(--violet); }

.work-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }

.work-card {
  background: var(--navy3); border-radius: 10px; overflow: hidden;
  cursor: pointer; border: 1px solid transparent;
  transition: transform 0.25s, border-color 0.25s, box-shadow 0.25s;
}
.work-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 20px 50px rgba(0,0,0,0.4);
}
#motion  .work-card:hover { border-color: var(--coral); }
#graphic .work-card:hover { border-color: var(--sky); }
#social  .work-card:hover { border-color: var(--violet); }

.work-card.placeholder {
  border: 2px dashed var(--border); background: transparent;
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  min-height: 220px; gap: 10px; cursor: default;
}
.work-card.placeholder:hover { transform: none; box-shadow: none; border-color: var(--border); }
.placeholder-plus {
  width: 40px; height: 40px; border-radius: 50%;
  border: 2px dashed #2a4060;
  display: flex; align-items: center; justify-content: center;
  font-size: 20px; color: #2a4060;
}
.placeholder-text {
  font-size: 12px; color: #2a4060;
  letter-spacing: 1px; text-transform: uppercase; font-weight: 600;
}

.card-thumb {
  height: 180px; position: relative;
  background: var(--navy2); background-size: cover; background-position: center;
  overflow: hidden;
}
.card-play {
  position: absolute; top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  width: 44px; height: 44px; border-radius: 50%;
  background: rgba(255,107,107,0.9);
  display: flex; align-items: center; justify-content: center;
  font-size: 16px; color: #fff; pointer-events: none;
}
.card-thumb-count {
  position: absolute; top: 10px; right: 10px;
  background: rgba(13,27,42,0.85);
  font-size: 11px; color: var(--muted); font-weight: 600;
  padding: 3px 8px; border-radius: 20px;
}
.card-body { padding: 16px 18px 20px; }
.card-title {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700; font-size: 16px; margin-bottom: 6px; line-height: 1.2;
}
.card-desc { font-size: 13px; color: var(--muted); line-height: 1.5; }
.card-hover-hint {
  font-size: 11px; color: #2a4060; letter-spacing: 1px;
  text-transform: uppercase; margin-top: 10px;
  display: flex; align-items: center; gap: 6px;
}
.card-hover-hint::before { content: '→'; }

/* ── MODAL ───────────────────────────────── */
#modal-overlay {
  display: none; position: fixed; inset: 0; z-index: 1000;
  background: rgba(5,12,20,0.95);
  align-items: center; justify-content: center; padding: 40px;
}
#modal-overlay.open { display: flex; }
.modal {
  background: var(--navy2); border-radius: 12px; overflow: hidden;
  max-width: 860px; width: 100%;
  border: 1px solid var(--border); position: relative;
  max-height: 90vh; display: flex; flex-direction: column;
}
.modal-close {
  position: absolute; top: 16px; right: 20px;
  font-size: 22px; color: var(--muted); cursor: pointer;
  background: none; border: none; z-index: 10; line-height: 1;
}
.modal-close:hover { color: var(--white); }
.modal-slideshow {
  position: relative; height: 420px; flex-shrink: 0;
  background: #060e17; overflow: hidden;
}
#modal-slide-content {
  position: absolute; inset: 0;
  display: flex; align-items: center; justify-content: center;
}
.slide-nav {
  position: absolute; top: 50%; transform: translateY(-50%);
  width: 100%; display: flex; justify-content: space-between;
  padding: 0 16px; pointer-events: none; z-index: 2;
}
.slide-btn {
  pointer-events: all;
  background: rgba(13,27,42,0.8); border: 1px solid var(--border);
  color: var(--white); width: 40px; height: 40px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; font-size: 16px; transition: background 0.2s;
}
.slide-btn:hover { background: var(--coral); border-color: var(--coral); }
#modal-dots {
  position: absolute; bottom: 14px; left: 50%; transform: translateX(-50%);
  display: flex; gap: 7px; z-index: 2;
}
.dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: #2a4060; cursor: pointer; transition: background 0.2s;
}
.dot.active { background: var(--coral); }
.modal-body { padding: 28px 32px 32px; overflow-y: auto; }
#modal-title {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 800; font-size: 26px; margin-bottom: 12px;
}
#modal-desc { font-size: 15px; color: var(--muted); line-height: 1.7; }

/* ── CONTACT ─────────────────────────────── */
#contact { background: var(--navy2); border-top: 1px solid var(--border); }
#contact .section-eyebrow { color: var(--yellow); }
#contact .section-eyebrow::before { background: var(--yellow); }
.contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: start; }
.contact-intro { font-size: 18px; color: var(--muted); line-height: 1.7; }
.contact-intro strong { color: var(--white); }
.contact-links { display: flex; flex-direction: column; }
.contact-item {
  display: flex; align-items: center; gap: 20px;
  padding: 20px 0; border-bottom: 1px solid var(--border);
}
.contact-icon {
  width: 44px; height: 44px; border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
  font-size: 18px; flex-shrink: 0;
}
.contact-detail-label {
  font-size: 11px; letter-spacing: 2px; text-transform: uppercase;
  color: var(--muted); margin-bottom: 3px;
}
.contact-detail-value { font-size: 15px; font-weight: 600; color: var(--white); }
a.contact-detail-value:hover { color: var(--yellow); }

/* ── FOOTER ──────────────────────────────── */
#footer {
  background: #060e17; border-top: 1px solid var(--border);
  padding: 32px 60px;
  display: flex; justify-content: space-between; align-items: center;
}
.footer-name {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 800; font-size: 16px; color: var(--muted);
}
.footer-name span { color: var(--coral); }
.footer-copy { font-size: 13px; color: #2a4060; }

/* ── PRINT ───────────────────────────────── */
@media print {
  #nav, #modal-overlay, .hero-scroll-hint,
  .work-card.placeholder, .hero-cta { display: none !important; }

  body { background: #fff !important; color: #111 !important; }

  section, #reel, #footer {
    background: #fff !important;
    border-color: #ddd !important;
    padding: 40px 40px !important;
  }

  .section-title, #modal-title, .hero-name,
  .card-title, .exp-role, .footer-name { color: #111 !important; }

  .section-eyebrow, .detail-label, .award-eyebrow,
  .exp-company, .contact-detail-label { color: #555 !important; }

  .about-bio, .exp-desc, .card-desc, #modal-desc,
  .contact-intro, .detail-sub { color: #444 !important; }

  .detail-cell, .award-card, .work-card { background: #f5f5f5 !important; }

  .work-card, .exp-item, .detail-cell { break-inside: avoid; }

  .hero-name .accent-coral { color: var(--coral) !important; }
  .hero-name .accent-yellow { color: #c49b00 !important; }

  #hero { min-height: auto; padding: 60px 40px 40px; }
  .hero-bg-accent, .hero-bg-accent2 { display: none; }
}
</style>
</head>
<body>

<nav id="nav"></nav>

<section id="hero" class="hero"></section>

<section id="about"></section>

<section id="experience"></section>

<section id="reel" class="work-section"></section>

<section id="motion" class="work-section"></section>

<section id="graphic" class="work-section"></section>

<section id="social" class="work-section"></section>

<section id="contact"></section>

<footer id="footer"></footer>

<!-- Modal -->
<div id="modal-overlay" onclick="handleOverlayClick(event)">
  <div class="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div class="modal-slideshow">
      <div id="modal-slide-content"></div>
      <div class="slide-nav">
        <button class="slide-btn" onclick="prevSlide()">‹</button>
        <button class="slide-btn" onclick="nextSlide()">›</button>
      </div>
      <div id="modal-dots"></div>
    </div>
    <div class="modal-body">
      <div id="modal-title"></div>
      <div id="modal-desc"></div>
    </div>
  </div>
</div>

<script>
/* ═══════════════════════════════════════════════════════════════
   PORTFOLIO DATA
   Edit everything in this block. Do not touch anything below it.
═══════════════════════════════════════════════════════════════ */
const PORTFOLIO_DATA = {
  // Your name — shown in nav, hero, footer
  name: { first: 'Sofia', middle: 'Garcia', last: 'Katz' },
  // Your job title
  role: 'Senior Multimedia Designer',
  // Your city — shown in hero eyebrow and footer
  location: 'Buenos Aires, Argentina',
  // One-line tagline shown under your name in the hero
  tagline: 'Senior Multimedia Designer crafting bold identities, motion, and social experiences that move people.',

  about: {
    // Your bio — HTML allowed (use <strong> for bold, <br> for line breaks)
    bio: 'I\'m a <strong>Senior Multimedia Designer</strong> based in <strong>Buenos Aires, Argentina</strong>, with over 8 years of experience crafting visual identities, motion graphics, and social media campaigns for brands across Latin America and beyond.<br><br>I believe design should be felt, not just seen. My work lives at the intersection of <strong>storytelling, motion, and visual strategy</strong> — turning ideas into experiences that resonate.',

    details: {
      basedIn:    { value: 'Buenos Aires',        sub: 'Argentina' },
      education:  { value: 'B.A. Graphic Design', sub: 'Universidad de Buenos Aires' },
      specialties:{ value: 'Motion · Design',     sub: 'Video · Social Media' },
      tools:      { value: 'Ae · Pr · Ai · Ps',  sub: 'Figma · Cinema 4D' },
    },

    award: {
      // Path to award logo image, e.g. 'media/award-logo.png'. Leave '' for placeholder icon.
      logo: '',
      title: 'Best Motion Design — LATAM Design Awards 2023',
      subtitle: 'Awarded for the Colores Agency brand campaign',
      // Full URL to the award page — opens in new tab
      url: 'https://example.com/award',
    },
  },

  // Work history — add or remove entries as needed
  experience: [
    {
      period: '2021 — Present',
      role: 'Senior Multimedia Designer',
      company: 'Studio Katz · Buenos Aires',
      description: 'Leading visual identity and motion projects for brands across fashion, tech, and culture. Responsible for art direction, motion production, and social strategy.',
    },
    {
      period: '2018 — 2021',
      role: 'Motion Designer',
      company: 'Agencia Colores · Buenos Aires',
      description: 'Produced motion graphics and video content for campaigns reaching 2M+ viewers. Collaborated with clients in FMCG and lifestyle brands across LATAM.',
    },
    {
      period: '2015 — 2018',
      role: 'Junior Graphic Designer',
      company: 'Freelance · Buenos Aires',
      description: 'Built a client base in print, identity, and social media design while completing postgraduate studies in motion graphics.',
    },
  ],

  reel: {
    // Your showreel. Options:
    //   Local file:  'media/reel.mp4'
    //   YouTube URL: 'https://www.youtube.com/watch?v=YOUR_ID'
    //   Vimeo URL:   'https://vimeo.com/YOUR_ID'
    //   Leave ''     to show the placeholder
    src: '',
    // Video duration shown as a badge (optional). Leave '' to hide.
    duration: '',
  },

  work: {
    motion: {
      sectionTitle: 'Motion Graphics\n& Video Editing',
      // Add your pieces below. Each piece can have multiple media items.
      // thumbnail: path to the image shown on the card (optional — uses first media item if blank)
      // media: array of { type: 'image'|'video', src: 'path or URL' }
      pieces: [
        // Example — uncomment and fill in with your real work:
        // {
        //   title: 'Brand Identity Reel 2024',
        //   description: 'Full motion identity for a BA fashion label.',
        //   thumbnail: 'media/motion/brand-reel-thumb.jpg',
        //   media: [
        //     { type: 'video', src: 'media/motion/brand-reel.mp4' },
        //     { type: 'image', src: 'media/motion/brand-reel-still.jpg' },
        //   ],
        // },
      ],
    },
    graphic: {
      sectionTitle: 'Graphic Design',
      pieces: [
        // { title: '...', description: '...', thumbnail: '...', media: [...] },
      ],
    },
    social: {
      sectionTitle: 'Social Media',
      pieces: [
        // { title: '...', description: '...', thumbnail: '...', media: [...] },
      ],
    },
  },

  contact: {
    // HTML allowed in intro
    intro: 'Interested in working together? I\'m available for <strong>freelance projects</strong>, <strong>collaborations</strong>, and <strong>full-time opportunities</strong>.<br><br>Let\'s create something bold.',
    email:    { label: 'sofia@example.com',             url: 'mailto:sofia@example.com' },
    linkedin: { label: 'linkedin.com/in/sofiagkatz',    url: 'https://linkedin.com/in/sofiagkatz' },
    instagram:{ label: '@sofiagkatz',                   url: 'https://instagram.com/sofiagkatz' },
    location: 'Buenos Aires, Argentina',
  },
};

/* ═══════════════════════════════════════════════════════════════
   RENDER FUNCTIONS — do not edit below this line
═══════════════════════════════════════════════════════════════ */

</script>
</body>
</html>
```

- [ ] **Step 3: Verify**

Open `index.html` in a browser. Expected: blank dark navy page (`#0D1B2A`) with no content yet and no console errors. The page title should read "Sofia Garcia Katz — Portfolio".

- [ ] **Step 4: Commit**

```bash
git init
git add index.html media/
git commit -m "feat: scaffold HTML, CSS, and PORTFOLIO_DATA"
```

---

## Task 2: Render Nav, Hero, About, Experience

**Files:**
- Modify: `index.html` — add render functions inside the `<script>` block, after the comment `RENDER FUNCTIONS — do not edit below this line`

**Consumes:** `PORTFOLIO_DATA.name`, `.role`, `.location`, `.tagline`, `.about`, `.experience`

**Produces:** `renderNav()`, `renderHero()`, `renderAbout()`, `renderExperience()` — called by init in Task 3+

- [ ] **Step 1: Add render functions to the script block**

Replace the line `/* ═══ RENDER FUNCTIONS — do not edit below this line ═══ */` with:

```js
/* ═══════════════════════════════════════════════════════════════
   RENDER FUNCTIONS — do not edit below this line
═══════════════════════════════════════════════════════════════ */

function renderNav() {
  const d = PORTFOLIO_DATA;
  const initials = d.name.first[0] + d.name.middle[0] + d.name.last[0];
  document.getElementById('nav').innerHTML = `
    <div class="nav-logo">${initials}<span>.</span></div>
    <nav class="nav-links">
      <a href="#about">About</a>
      <a href="#experience">Experience</a>
      <a href="#reel">Reel</a>
      <a href="#motion">Motion</a>
      <a href="#graphic">Graphic Design</a>
      <a href="#social">Social Media</a>
      <a href="#contact">Contact</a>
    </nav>
  `;
}

function renderHero() {
  const d = PORTFOLIO_DATA;
  document.getElementById('hero').innerHTML = `
    <div class="hero-bg-accent"></div>
    <div class="hero-bg-accent2"></div>
    <div class="hero-eyebrow">${d.location}</div>
    <div class="hero-name">
      ${d.name.first}<br>
      <span class="accent-coral">${d.name.middle}</span><br>
      <span class="accent-yellow">${d.name.last}</span>
    </div>
    <p class="hero-tagline">${d.tagline}</p>
    <div class="hero-cta">
      <a href="#reel" class="btn-primary">Watch My Reel</a>
      <a href="#contact" class="btn-outline">Get in Touch</a>
    </div>
    <div class="hero-scroll-hint">Scroll to explore</div>
  `;
}

function renderAbout() {
  const d = PORTFOLIO_DATA;
  const det = d.about.details;
  const aw  = d.about.award;

  const logoHtml = aw.logo
    ? `<img src="${aw.logo}" alt="Award logo" style="width:52px;height:52px;object-fit:contain;border-radius:4px;">`
    : `<div class="award-logo-placeholder">🏅</div><div class="award-logo-hint">Award<br>logo</div>`;

  document.getElementById('about').innerHTML = `
    <div class="section-eyebrow">About Me</div>
    <div class="section-title">Who I Am</div>
    <div class="about-grid">
      <div class="about-bio">${d.about.bio}</div>
      <div class="about-sidebar">
        <div class="detail-grid">
          <div class="detail-cell" style="border-top-color:var(--coral)">
            <div class="detail-label" style="color:var(--coral)">Based in</div>
            <div class="detail-value">${det.basedIn.value}</div>
            <div class="detail-sub">${det.basedIn.sub}</div>
          </div>
          <div class="detail-cell" style="border-top-color:var(--sky)">
            <div class="detail-label" style="color:var(--sky)">Education</div>
            <div class="detail-value">${det.education.value}</div>
            <div class="detail-sub">${det.education.sub}</div>
          </div>
          <div class="detail-cell" style="border-top-color:var(--violet)">
            <div class="detail-label" style="color:var(--violet)">Specialties</div>
            <div class="detail-value">${det.specialties.value}</div>
            <div class="detail-sub">${det.specialties.sub}</div>
          </div>
          <div class="detail-cell" style="border-top-color:var(--muted)">
            <div class="detail-label" style="color:var(--muted)">Tools</div>
            <div class="detail-value">${det.tools.value}</div>
            <div class="detail-sub">${det.tools.sub}</div>
          </div>
        </div>
        <div class="award-card">
          <div class="award-card-inner">
            <div class="award-logo">${logoHtml}</div>
            <div class="award-content">
              <div class="award-eyebrow">Award</div>
              <div class="award-title">${aw.title}</div>
              <div class="award-sub">${aw.subtitle}</div>
              <a class="award-link" href="${aw.url}" target="_blank" rel="noopener">View Award</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  `;
}

function renderExperience() {
  const d = PORTFOLIO_DATA;
  const items = d.experience.map((e, i) => `
    <div class="exp-item" ${i === d.experience.length - 1 ? 'style="border-bottom:none"' : ''}>
      <div class="exp-period">${e.period}</div>
      <div>
        <div class="exp-role">${e.role}</div>
        <div class="exp-company">${e.company}</div>
        <div class="exp-desc">${e.description}</div>
      </div>
    </div>
  `).join('');

  document.getElementById('experience').innerHTML = `
    <div class="section-eyebrow">Career</div>
    <div class="section-title">Experience</div>
    <div class="exp-list">${items}</div>
  `;
}
```

- [ ] **Step 2: Add DOMContentLoaded init (partial — calls only the 4 functions defined so far)**

Add this at the very end of the `<script>` block, after the render functions:

```js
document.addEventListener('DOMContentLoaded', () => {
  renderNav();
  renderHero();
  renderAbout();
  renderExperience();
  // renderReel(), renderWorkSections(), renderContact(), renderFooter() added in Tasks 3–4
});

document.addEventListener('keydown', e => {
  if (e.key === 'Escape')      closeModal();
  if (e.key === 'ArrowRight')  nextSlide();
  if (e.key === 'ArrowLeft')   prevSlide();
});
```

Note: `closeModal`, `nextSlide`, `prevSlide` are defined in Task 4. The keydown listener is safe to add now — they will exist by the time any key is pressed.

- [ ] **Step 3: Verify**

Open `index.html` in a browser. Scroll through the page and confirm:
- Sticky nav shows `SGK.` logo and 7 anchor links
- Hero shows full-screen with name on 3 lines (white / coral / yellow), tagline, two buttons
- About shows bio on left; 2×2 detail grid + award card on right (with placeholder trophy icon since `award.logo` is `''`)
- Experience shows 3 entries in timeline layout, last entry has no bottom border
- No console errors

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: render nav, hero, about, and experience sections"
```

---

## Task 3: Render Reel + Work Sections

**Files:**
- Modify: `index.html` — add `getEmbedInfo`, `renderReel`, `renderWorkSections` to script block; update DOMContentLoaded

**Consumes:** `PORTFOLIO_DATA.reel`, `.work.motion`, `.work.graphic`, `.work.social`

**Produces:** `getEmbedInfo(src)` consumed by Task 4 modal; `renderWorkSections()` sets `onclick="openModal(...)"` wired in Task 4

- [ ] **Step 1: Add helper + render functions inside the script block, before the DOMContentLoaded call**

```js
/* ── Detect video embed type ───────────────── */
function getEmbedInfo(src) {
  if (!src) return null;
  if (/youtube\.com\/watch\?v=/.test(src)) {
    const id = new URL(src).searchParams.get('v');
    return { type: 'iframe', url: `https://www.youtube.com/embed/${id}` };
  }
  if (/youtu\.be\//.test(src)) {
    const id = src.split('youtu.be/')[1].split('?')[0];
    return { type: 'iframe', url: `https://www.youtube.com/embed/${id}` };
  }
  if (/vimeo\.com\/(\d+)/.test(src)) {
    const id = src.match(/vimeo\.com\/(\d+)/)[1];
    return { type: 'iframe', url: `https://player.vimeo.com/video/${id}` };
  }
  return { type: 'video', url: src };
}

function renderReel() {
  const reel = PORTFOLIO_DATA.reel;
  const embed = getEmbedInfo(reel.src);
  let playerHtml;

  if (!embed) {
    playerHtml = `
      <div class="reel-play-wrap">
        <div class="reel-play-btn">▶</div>
        <div class="reel-play-label">Watch Showreel</div>
      </div>`;
  } else if (embed.type === 'iframe') {
    playerHtml = `<iframe src="${embed.url}" style="width:100%;height:100%;border:none;" allowfullscreen allow="autoplay; fullscreen; picture-in-picture"></iframe>`;
  } else {
    playerHtml = `<video src="${embed.url}" controls style="width:100%;height:100%;"></video>`;
  }

  const durationHtml = reel.duration
    ? `<div class="reel-duration">${reel.duration}</div>` : '';

  document.getElementById('reel').innerHTML = `
    <div class="section-eyebrow">Showreel</div>
    <div class="reel-heading">My <span>Reel</span></div>
    <div class="reel-container">
      ${playerHtml}
      ${durationHtml}
    </div>
  `;
}

function renderWorkSections() {
  const sections = [
    { key: 'motion',  id: 'motion',  data: PORTFOLIO_DATA.work.motion },
    { key: 'graphic', id: 'graphic', data: PORTFOLIO_DATA.work.graphic },
    { key: 'social',  id: 'social',  data: PORTFOLIO_DATA.work.social },
  ];

  const MIN_CELLS = 6;

  sections.forEach(({ key, id, data }) => {
    const pieces = data.pieces;

    const cardHtml = pieces.map((piece, i) => {
      const firstMedia = piece.media && piece.media[0];
      const isVideo    = firstMedia && firstMedia.type === 'video';
      const thumbSrc   = piece.thumbnail || (firstMedia ? firstMedia.src : '');
      const thumbStyle = thumbSrc
        ? `background-image:url('${thumbSrc}');background-size:cover;background-position:center;`
        : '';
      const count = piece.media ? piece.media.length : 0;

      return `
        <div class="work-card" onclick="openModal('${key}', ${i})">
          <div class="card-thumb" style="${thumbStyle}">
            ${isVideo ? '<div class="card-play">▶</div>' : ''}
            ${count > 0 ? `<div class="card-thumb-count">⊞ ${count} media</div>` : ''}
          </div>
          <div class="card-body">
            <div class="card-title">${piece.title}</div>
            <div class="card-desc">${piece.description}</div>
            <div class="card-hover-hint">Click to view</div>
          </div>
        </div>`;
    }).join('');

    const placeholderCount = Math.max(0, MIN_CELLS - pieces.length);
    const placeholderHtml  = Array(placeholderCount).fill(`
      <div class="work-card placeholder">
        <div class="placeholder-plus">+</div>
        <div class="placeholder-text">Add work piece</div>
      </div>`).join('');

    const titleHtml = data.sectionTitle.replace('\n', '<br>');

    document.getElementById(id).innerHTML = `
      <div class="section-eyebrow">Featured Work</div>
      <div class="section-title">${titleHtml}</div>
      <div class="work-grid">${cardHtml}${placeholderHtml}</div>
    `;
  });
}
```

- [ ] **Step 2: Update DOMContentLoaded to call the new functions**

Replace the existing `DOMContentLoaded` listener with:

```js
document.addEventListener('DOMContentLoaded', () => {
  renderNav();
  renderHero();
  renderAbout();
  renderExperience();
  renderReel();
  renderWorkSections();
  // renderContact(), renderFooter() added in Task 4
});
```

- [ ] **Step 3: Verify**

Open `index.html`. Scroll past Experience and confirm:
- **Reel section**: dark background, coral play button placeholder (since `reel.src` is `''`), "My Reel" heading
- **Motion / Graphic Design / Social Media sections**: each shows 6 dashed placeholder cards (since `pieces` arrays are empty)
- Section eyebrow color is coral / sky / violet respectively
- No console errors

Test with a real piece: temporarily add one entry to `PORTFOLIO_DATA.work.motion.pieces`:
```js
{ title: 'Test Piece', description: 'A test.', thumbnail: '', media: [{ type: 'image', src: '' }] }
```
Expected: 1 real card (dark background thumbnail) + 5 placeholder cards. Remove the test entry when done.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: render reel and work section grids"
```

---

## Task 4: Modal Slideshow + Contact + Footer

**Files:**
- Modify: `index.html` — add modal JS functions, `renderContact`, `renderFooter`; finalize DOMContentLoaded

**Consumes:** `PORTFOLIO_DATA.contact`; `getEmbedInfo()` from Task 3; `openModal(sectionKey, pieceIndex)` called by card `onclick` from Task 3

- [ ] **Step 1: Add modal JS functions inside the script block, before DOMContentLoaded**

```js
/* ── Modal ─────────────────────────────────── */
let _modalPieces = [];
let _modalSlide  = 0;

function openModal(sectionKey, pieceIndex) {
  const piece     = PORTFOLIO_DATA.work[sectionKey].pieces[pieceIndex];
  _modalPieces    = piece.media || [];
  _modalSlide     = 0;

  document.getElementById('modal-title').textContent = piece.title;
  document.getElementById('modal-desc').textContent  = piece.description;

  // Build dots
  const dotsEl = document.getElementById('modal-dots');
  dotsEl.innerHTML = _modalPieces.map((_, i) =>
    `<div class="dot${i === 0 ? ' active' : ''}" onclick="goToSlide(${i})"></div>`
  ).join('');

  // Hide nav arrows when only 1 slide
  document.querySelector('.slide-nav').style.display =
    _modalPieces.length > 1 ? 'flex' : 'none';

  _renderSlide(0);
  document.getElementById('modal-overlay').classList.add('open');
}

function closeModal() {
  document.getElementById('modal-overlay').classList.remove('open');
  document.getElementById('modal-slide-content').innerHTML = '';
}

function handleOverlayClick(e) {
  if (e.target === document.getElementById('modal-overlay')) closeModal();
}

function goToSlide(n) {
  _modalSlide = (n + _modalPieces.length) % _modalPieces.length;
  _renderSlide(_modalSlide);
  document.querySelectorAll('#modal-dots .dot').forEach((dot, i) =>
    dot.classList.toggle('active', i === _modalSlide)
  );
}

function nextSlide() {
  if (!document.getElementById('modal-overlay').classList.contains('open')) return;
  goToSlide(_modalSlide + 1);
}

function prevSlide() {
  if (!document.getElementById('modal-overlay').classList.contains('open')) return;
  goToSlide(_modalSlide - 1);
}

function _renderSlide(n) {
  const media   = _modalPieces[n];
  const content = document.getElementById('modal-slide-content');
  if (!media) { content.innerHTML = ''; return; }

  if (media.type === 'image') {
    content.innerHTML = `<img src="${media.src}" alt=""
      style="width:100%;height:100%;object-fit:contain;">`;
    return;
  }

  // video type
  const embed = getEmbedInfo(media.src);
  if (!embed) { content.innerHTML = ''; return; }

  if (embed.type === 'iframe') {
    content.innerHTML = `<iframe src="${embed.url}"
      style="width:100%;height:100%;border:none;"
      allowfullscreen allow="autoplay; fullscreen; picture-in-picture"></iframe>`;
  } else {
    content.innerHTML = `<video src="${embed.url}" controls
      style="width:100%;height:100%;max-height:420px;background:#000;"></video>`;
  }
}
```

- [ ] **Step 2: Add renderContact and renderFooter**

```js
function renderContact() {
  const c = PORTFOLIO_DATA.contact;
  document.getElementById('contact').innerHTML = `
    <div class="section-eyebrow">Get in Touch</div>
    <div class="section-title">Contact</div>
    <div class="contact-grid">
      <p class="contact-intro">${c.intro}</p>
      <div class="contact-links">
        <div class="contact-item">
          <div class="contact-icon" style="background:#FF6B6B22;">📧</div>
          <div>
            <div class="contact-detail-label">Email</div>
            <a class="contact-detail-value" href="${c.email.url}">${c.email.label}</a>
          </div>
        </div>
        <div class="contact-item">
          <div class="contact-icon" style="background:#6BCBEA22;">💼</div>
          <div>
            <div class="contact-detail-label">LinkedIn</div>
            <a class="contact-detail-value" href="${c.linkedin.url}" target="_blank" rel="noopener">${c.linkedin.label}</a>
          </div>
        </div>
        <div class="contact-item">
          <div class="contact-icon" style="background:#C77DFF22;">📸</div>
          <div>
            <div class="contact-detail-label">Instagram</div>
            <a class="contact-detail-value" href="${c.instagram.url}" target="_blank" rel="noopener">${c.instagram.label}</a>
          </div>
        </div>
        <div class="contact-item" style="border-bottom:none;">
          <div class="contact-icon" style="background:#FFD93D22;">📍</div>
          <div>
            <div class="contact-detail-label">Location</div>
            <div class="contact-detail-value">${c.location}</div>
          </div>
        </div>
      </div>
    </div>
  `;
}

function renderFooter() {
  const d = PORTFOLIO_DATA;
  document.getElementById('footer').innerHTML = `
    <div class="footer-name">${d.name.first} ${d.name.middle} ${d.name.last}<span>.</span></div>
    <div class="footer-copy">© ${new Date().getFullYear()} · ${d.role} · ${d.location}</div>
  `;
}
```

- [ ] **Step 3: Finalize DOMContentLoaded — replace existing listener with the complete version**

```js
document.addEventListener('DOMContentLoaded', () => {
  renderNav();
  renderHero();
  renderAbout();
  renderExperience();
  renderReel();
  renderWorkSections();
  renderContact();
  renderFooter();
});
```

- [ ] **Step 4: Verify the full portfolio**

Open `index.html` in a browser. Check each section:

1. **Nav** — sticky, shows `SGK.` + links; clicking an anchor scrolls to the right section
2. **Hero** — full-screen, three-line name, two buttons
3. **About** — bio left; 2×2 detail grid + award card right; "View Award" link opens in new tab
4. **Experience** — 3 entries
5. **Reel** — placeholder play button showing (src is empty)
6. **Work sections** — 6 placeholder cards each (no real pieces yet)
7. **Contact** — two columns; email/LinkedIn/Instagram links clickable
8. **Footer** — name + copyright
9. **Modal test**: add a temporary piece to `work.motion.pieces`:
   ```js
   { title: 'Test', description: 'Desc.', thumbnail: '', media: [{ type: 'image', src: 'https://picsum.photos/800/450' }, { type: 'image', src: 'https://picsum.photos/800/451' }] }
   ```
   Click the card → modal opens → navigate with arrows / dots / keyboard → Escape closes. Remove the test piece when done.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: modal slideshow, contact, and footer — portfolio complete"
```

---

## Task 5: Editing guide for Sofia

**Files:**
- Create: `EDITING-GUIDE.md`

- [ ] **Step 1: Create `EDITING-GUIDE.md`**

```markdown
# How to Edit Your Portfolio

All your content lives in one place: the `index.html` file.  
Open it in any text editor (Notepad, TextEdit, VS Code, etc.).

Scroll to the very top of the file until you see this line:

```
const PORTFOLIO_DATA = {
```

Everything between the `{` and the matching `}` a few hundred lines later
is yours to edit. The layout, colours, and animations are handled
automatically — **you never need to touch anything else**.

---

## Your Name, Title, and Tagline

```js
name: { first: 'Sofia', middle: 'Garcia', last: 'Katz' },
role: 'Senior Multimedia Designer',
location: 'Buenos Aires, Argentina',
tagline: 'Senior Multimedia Designer crafting bold identities...',
```

Replace the text inside the quotes with your own. Don't delete the quotes or commas.

---

## About Me bio

```js
bio: 'I\'m a <strong>Senior Multimedia Designer</strong>...',
```

Edit the text inside the quotes.  
Use `<strong>word</strong>` to make a word **bold**.  
Use `<br><br>` to start a new paragraph.  
Use `\'` whenever you need an apostrophe inside the text (e.g. `I\'m`).

---

## About Me — side details (Based in, Education, Specialties, Tools)

```js
details: {
  basedIn:    { value: 'Buenos Aires', sub: 'Argentina' },
  education:  { value: 'B.A. Graphic Design', sub: 'Universidad de Buenos Aires' },
  specialties:{ value: 'Motion · Design',     sub: 'Video · Social Media' },
  tools:      { value: 'Ae · Pr · Ai · Ps',  sub: 'Figma · Cinema 4D' },
},
```

`value` is the main line. `sub` is the smaller line below it.

---

## Award

```js
award: {
  logo: '',                          // ← path to your award logo image
  title: 'Best Motion Design ...',
  subtitle: 'Awarded for ...',
  url: 'https://example.com/award', // ← link to the award page
},
```

**To add the logo:**
1. Copy your logo image into the `media/` folder (e.g. `award-logo.png`)
2. Change `logo: ''` to `logo: 'media/award-logo.png'`

**To link to the award page:**  
Replace `https://example.com/award` with the real URL.

---

## Experience

```js
experience: [
  {
    period: '2021 — Present',
    role: 'Senior Multimedia Designer',
    company: 'Studio Katz · Buenos Aires',
    description: 'Leading visual identity...',
  },
  // more entries below...
],
```

Each `{ ... }` block is one job. To add a new one, copy an existing block,
paste it after the last one (before the `]`), and change the text.
Make sure each block ends with a comma `,` except the very last one.

---

## Showreel Video

```js
reel: {
  src: '',       // ← your video here
  duration: '',  // ← e.g. '2:34'  (optional)
},
```

**Option 1 — local video file:**
1. Copy your video into the `media/` folder (e.g. `reel.mp4`)
2. Set `src: 'media/reel.mp4'`

**Option 2 — YouTube:**
1. Go to your YouTube video
2. Copy the URL from the browser address bar (e.g. `https://www.youtube.com/watch?v=abc123`)
3. Set `src: 'https://www.youtube.com/watch?v=abc123'`

**Option 3 — Vimeo:**  
Same as YouTube but use the Vimeo URL (e.g. `https://vimeo.com/123456789`).

---

## Adding a Work Piece

Find the section you want (motion, graphic, or social) and add a block inside `pieces: [...]`:

```js
motion: {
  sectionTitle: 'Motion Graphics\n& Video Editing',
  pieces: [
    {
      title: 'Brand Identity Reel 2024',
      description: 'Full motion identity for a fashion label.',
      thumbnail: 'media/motion/brand-reel-thumb.jpg',
      media: [
        { type: 'video', src: 'media/motion/brand-reel.mp4' },
        { type: 'image', src: 'media/motion/brand-reel-still.jpg' },
      ],
    },
    // add more pieces here
  ],
},
```

### Fields explained:

| Field | What it does |
|---|---|
| `title` | The title shown on the card and in the popup |
| `description` | The text shown in the popup below the media |
| `thumbnail` | The image shown on the card (optional — uses first media item if empty) |
| `media` | The list of images/videos shown in the popup slideshow |

### Adding media to a piece:

Each item in `media` is either an image or a video:

```js
{ type: 'image', src: 'media/motion/my-image.jpg' }
{ type: 'video', src: 'media/motion/my-video.mp4' }
{ type: 'video', src: 'https://www.youtube.com/watch?v=abc123' }
{ type: 'video', src: 'https://vimeo.com/123456789' }
```

Put your image and video files in the correct subfolder:
- Motion pieces → `media/motion/`
- Graphic design pieces → `media/graphic/`
- Social media pieces → `media/social/`

---

## Contact Details

```js
contact: {
  email:    { label: 'sofia@example.com',          url: 'mailto:sofia@example.com' },
  linkedin: { label: 'linkedin.com/in/sofiagkatz', url: 'https://linkedin.com/in/sofiagkatz' },
  instagram:{ label: '@sofiagkatz',                url: 'https://instagram.com/sofiagkatz' },
  location: 'Buenos Aires, Argentina',
},
```

`label` is what visitors see on screen. `url` is where they go when they click it.

---

## Exporting as PDF

1. Open `index.html` in **Google Chrome**
2. Press `Ctrl + P` (Windows) or `Cmd + P` (Mac)
3. Set **Destination** to "Save as PDF"
4. Set **Paper size** to A4 or Letter
5. Enable **Background graphics** (in "More settings") to keep the colours
6. Click **Save**

---

## Publishing to GitHub Pages

1. Create a new repository on GitHub (e.g. `sofia-portfolio`)
2. Upload `index.html` and the entire `media/` folder to the repository
3. Go to **Settings → Pages**
4. Under **Source**, select **Deploy from a branch**, choose `main`, folder `/ (root)`
5. Click **Save** — your portfolio will be live at `https://yourusername.github.io/sofia-portfolio/`
```

- [ ] **Step 2: Verify the guide**

Read through the guide and check:
- Every section of the portfolio has a matching editing section
- The code snippets match exactly what's in `index.html`'s `PORTFOLIO_DATA`
- The PDF and GitHub Pages instructions are accurate

- [ ] **Step 3: Commit**

```bash
git add EDITING-GUIDE.md
git commit -m "docs: add plain-English editing guide for portfolio content"
```

---

## Self-Review Checklist

**Spec coverage:**

| Spec requirement | Covered in |
|---|---|
| Single `index.html`, no build tools | Task 1 |
| `PORTFOLIO_DATA` const at top | Task 1 |
| Google Fonts (Space Grotesk + Inter) | Task 1 CSS |
| Buenos Aires Nights palette via CSS vars | Task 1 CSS |
| Sticky nav with anchor links | Task 2 `renderNav` |
| Hero — 3-line name, coral/yellow accents, tagline, CTAs | Task 2 `renderHero` |
| About — bio + 2×2 detail grid + award card with logo + external link | Task 2 `renderAbout` |
| Experience — timeline list | Task 2 `renderExperience` |
| Reel — auto-detect local/YouTube/Vimeo, placeholder when empty | Task 3 `renderReel` |
| 3 work sections, each with own accent color | Task 3 `renderWorkSections` |
| Card grid — 3-col, min 6 cells, placeholder cards | Task 3 `renderWorkSections` |
| Card thumbnail, video play button, media count badge | Task 3 `renderWorkSections` |
| Modal slideshow — images + video + iframe, arrows, dots, keyboard | Task 4 modal JS |
| Modal close on Escape / overlay click / ✕ button | Task 4 modal JS |
| Contact — two-column layout, clickable links | Task 4 `renderContact` |
| Footer | Task 4 `renderFooter` |
| `@media print` — white backgrounds, hidden placeholders, break-inside | Task 1 CSS |
| `media/` folder structure | Task 1 |
| Non-technical editing guide | Task 5 |

All spec requirements covered. No gaps found.
