# Sofi Portfolio

## Running locally

Open the site through a local HTTP server — **do not open `index.html` directly** as a `file://` URL. YouTube embeds (and some browser APIs) require a real HTTP origin and will fail otherwise.

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080` in your browser.
