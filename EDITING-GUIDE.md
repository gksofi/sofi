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
