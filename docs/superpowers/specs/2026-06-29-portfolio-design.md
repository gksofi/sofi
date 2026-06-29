# Sofia Garcia Katz — Portfolio Design Spec

**Date:** 2026-06-29
**Owner:** Sofia Garcia Katz
**Status:** Approved

---

## 1. Overview

A single-page personal portfolio for Sofia Garcia Katz, Senior Multimedia Designer from Buenos Aires, Argentina. The goal is to present her identity, experience, and featured work to potential clients and employers in a bold, colorful, and professional way. The portfolio must be easy to edit (text and media), exportable as PDF, and deployable to GitHub Pages.

---

## 2. Technical Approach

- **Single `index.html` file** — no build tools, no dependencies, no server required
- All user-editable content lives in one **JavaScript data object** at the top of the file, clearly separated from layout code
- Media files (images and videos) are placed in a `/media` folder alongside `index.html` and referenced by filename in the data object
- Fonts loaded via Google Fonts CDN (`Space Grotesk` + `Inter`)
- **PDF export:** print from Chrome (Ctrl+P → Save as PDF); layout is print-aware
- **GitHub Pages deployment:** push `index.html` + `/media/` folder; no build step

---

## 3. Visual Design

### Color Palette — "Buenos Aires Nights"

| Role | Color | Hex |
|---|---|---|
| Background (primary) | Deep Navy | `#0D1B2A` |
| Background (alternate) | Navy 2 | `#122333` |
| Background (cards) | Navy 3 | `#1A2F42` |
| Accent — Motion section | Coral Red | `#FF6B6B` |
| Accent — Graphic Design section | Sky Blue | `#6BCBEA` |
| Accent — Social Media section | Violet | `#C77DFF` |
| Highlight / Award | Golden Yellow | `#FFD93D` |
| Body text | Off-white | `#F4F8FB` |
| Muted text | Steel Blue | `#8AA0B4` |
| Borders | Dark Navy | `#1E3048` |

### Typography

- **Headlines:** `Space Grotesk`, weight 800 — used for name, section titles, card titles, modal title
- **Body / UI:** `Inter`, weight 400/500 — used for descriptions, nav links, labels
- **Section eyebrows:** 11px, uppercase, letter-spacing 4px
- **Card titles:** Space Grotesk 700, 16px

### Visual Motifs

- Section eyebrows have a short horizontal rule before the text (`::before` pseudo-element)
- Each of the 3 work sections has its own accent color (coral, sky, violet) used for the eyebrow, card hover border, and section heading
- Subtle radial gradient blobs in the hero background (coral/violet) add depth without clutter
- Cards lift on hover with `translateY(-6px)` and a colored border matching the section accent

---

## 4. Page Structure

All sections are on a single scrollable page. Navigation anchors jump to each section.

```
[NAV]
[HERO]
[ABOUT ME]
[EXPERIENCE]
[REEL]
[MOTION GRAPHICS / VIDEO EDITING]
[GRAPHIC DESIGN]
[SOCIAL MEDIA]
[CONTACT]
[FOOTER]
```

---

## 5. Section Specifications

### 5.1 Navigation

- Sticky top bar, `64px` tall, `backdrop-filter: blur` with semi-transparent navy background
- Left: `SGK.` logo (Space Grotesk 800, coral dot)
- Right: anchor links — About · Experience · Reel · Motion · Graphic Design · Social Media · Contact
- Links: 13px uppercase, letter-spacing 1.5px, muted color → yellow on hover

### 5.2 Hero

- Full viewport height (`min-height: 100vh`)
- Subtle radial gradient blobs (coral top-right, sky bottom-left) as background decoration
- Eyebrow: "Buenos Aires, Argentina" with a sky-blue rule
- Name displayed across 3 lines at massive scale (`clamp(52px, 8vw, 110px)`):
  - Line 1: `SOFIA` — white
  - Line 2: `GARCIA` — coral
  - Line 3: `KATZ` — yellow
- Tagline: short sentence, muted color, max-width 520px
- Two CTAs: "Watch My Reel" (primary coral button) · "Get in Touch" (outline button)
- Scroll hint at bottom-left

### 5.3 About Me

- Two-column layout (bio left, sidebar right)
- **Left:** bio paragraph (editable in data object)
- **Right sidebar — two parts stacked:**
  1. **2×2 grid of detail cards** — each card has a colored top border, a label, a value, and a subtitle:
     - Based in (coral border)
     - Education — graduation info (sky border)
     - Specialties (violet border)
     - Tools (muted border)
  2. **Award card** (full width, spanning the 2 columns of the grid above):
     - Left panel: logo placeholder (dashed border box) + "Award logo" hint text — replaced by dropping in the real logo image
     - Right panel: "Award" eyebrow with trophy icon, award title, subtitle, and "View Award ↗" external link (opens in new tab)
     - Styled with a golden-yellow border and a subtle warm gradient background

### 5.4 Experience

- Timeline-style list, no hard limit on entries
- Each entry: date range (left column, muted) + role / company / description (right column)
- Company name in violet
- Entries separated by a bottom border; last entry has no border

### 5.5 Reel

- Standalone dark section (`#060e17` background) between Experience and the work sections
- Eyebrow: "Showreel" in coral
- Heading: "My **Reel**" (coral accent on "Reel")
- **Video container:** full-width, `aspect-ratio: 16/7`, rounded corners, dark background
  - Accepts either a local `<video>` file or a YouTube/Vimeo `<iframe>` embed — configured via the data object
  - When a video source is provided it renders the real player; when empty it shows the coral play-button placeholder
- Duration badge bottom-right (optional, from data object)

### 5.6 Work Sections (×3)

Three sections in order: Motion Graphics / Video Editing → Graphic Design → Social Media.

Each section:
- Section eyebrow + title
- **3-column card grid** (CSS Grid, `repeat(3, 1fr)`)
- Any number of real work cards + dashed placeholder cards filling remaining slots (always show at least 6 cells total so the grid never looks sparse)

**Work card:**
- Thumbnail area (180px tall): shows the first media item as a background; video cards show a coral play button overlay; image cards show the image
- Media count badge top-right: "⊞ N media"
- Card body: title (Space Grotesk 700) + short description
- "Click to view →" hint in muted color
- On hover: lifts + section-colored border appears
- On click: opens the modal

**Modal / Slideshow:**
- Full-screen dark overlay
- Slideshow area (420px tall): shows all media items for the selected piece, one at a time
  - Images: rendered as `<img>` filling the frame
  - Videos: rendered as `<video>` with controls, or `<iframe>` for YouTube/Vimeo
- Prev / Next arrow buttons (circular, coral on hover)
- Dot indicators (coral = active)
- Below slideshow: piece title (Space Grotesk 800, 26px) + full description
- Close button (✕ top-right) or click overlay or Escape key to dismiss
- Left/right arrow keys navigate slides

**Placeholder cards:**
- Dashed border, transparent background
- Centered "+" circle icon + "Add work piece" label
- Not clickable

### 5.7 Contact

- Two-column layout: intro text left, contact details right
- Contact detail rows: icon + label + value, separated by bottom borders
- Fields: Email, LinkedIn, Instagram, Location (all editable via data object)

### 5.8 Footer

- Full-width dark bar (`#060e17`)
- Left: name with coral dot
- Right: copyright + role + city

---

## 6. Content Data Object

All user-editable content is defined in a single `const PORTFOLIO_DATA = { ... }` block at the top of `index.html`. The structure:

```js
const PORTFOLIO_DATA = {
  name: { first: "Sofia", middle: "Garcia", last: "Katz" },
  tagline: "Senior Multimedia Designer ...",
  location: "Buenos Aires, Argentina",

  about: {
    bio: "...",
    details: {
      basedIn: "Buenos Aires, Argentina",
      education: { degree: "...", school: "..." },
      specialties: ["Motion Graphics", "Graphic Design", "Video Editing", "Social Media"],
      tools: ["After Effects", "Premiere", "Illustrator", "Photoshop", "Figma", "Cinema 4D"],
    },
    award: {
      logo: "media/award-logo.png",   // path to logo image, or "" for placeholder
      title: "Best Motion Design — LATAM Design Awards 2023",
      subtitle: "Awarded for the Colores Agency brand campaign",
      url: "https://example.com/award",
    },
  },

  experience: [
    { period: "2021 — Present", role: "Senior Multimedia Designer", company: "Studio Katz · Buenos Aires", description: "..." },
    // ...
  ],

  reel: {
    src: "media/reel.mp4",   // local file path, or YouTube/Vimeo embed URL, or "" for placeholder
    duration: "2:34",        // optional, shown as badge
  },

  work: {
    motion: {
      title: "Motion Graphics\n& Video Editing",
      pieces: [
        {
          title: "Brand Identity Reel 2024",
          description: "...",
          thumbnail: "media/motion/brand-reel-thumb.jpg",
          media: [
            { type: "video", src: "media/motion/brand-reel.mp4" },
            { type: "image", src: "media/motion/brand-reel-still.jpg" },
          ],
        },
        // more pieces...
      ],
    },
    graphic: { title: "Graphic Design", pieces: [ /* ... */ ] },
    social:  { title: "Social Media",   pieces: [ /* ... */ ] },
  },

  contact: {
    email: "sofia@example.com",
    linkedin: { label: "linkedin.com/in/sofiagkatz", url: "https://linkedin.com/in/sofiagkatz" },
    instagram: { label: "@sofiagkatz", url: "https://instagram.com/sofiagkatz" },
    location: "Buenos Aires, Argentina",
  },
};
```

---

## 7. PDF Export

- A `@media print` stylesheet will:
  - Remove the sticky nav and replace it with a static header block
  - Remove hover effects and modal
  - Ensure work cards don't break across page boundaries (`break-inside: avoid`)
  - Dark section backgrounds become white; text colors invert to near-black for readability
  - Placeholder cards are hidden (`display: none`) so only real work pieces print

---

## 8. File Structure

```
sofi/
├── index.html          ← entire portfolio + data object
├── media/
│   ├── reel.mp4        ← showreel video (or embed URL in data object)
│   ├── award-logo.png  ← award organization logo
│   ├── motion/
│   │   ├── piece-1-thumb.jpg
│   │   ├── piece-1-video.mp4
│   │   └── ...
│   ├── graphic/
│   │   └── ...
│   └── social/
│       └── ...
└── brainstorm/         ← mockup files (not deployed)
```

---

## 9. Editing Guide (for Sofia)

To update any content, open `index.html` in a text editor and find `const PORTFOLIO_DATA` near the top. Every field has a comment explaining what it does.

- **Add a work piece:** add a new object to the relevant `pieces` array with title, description, thumbnail, and media list
- **Add media to a piece:** add items to the `media` array — each has a `type` ("image" or "video") and a `src` (file path or embed URL)
- **Update the reel:** change `reel.src` to your video file or paste a YouTube/Vimeo URL
- **Update the award logo:** drop the image into `/media/` and set `award.logo` to the filename
- **Change contact info:** edit the `contact` block
