# Yellow Door Bookkeeping — single page site

Plain HTML and CSS. No build step, no framework, no JavaScript.

## Files

```
index.html             the page (edit copy here)
css/styles.css         all styling
images/                7 photos, WebP
single-file-build.html everything inlined as base64 — one file, no folder needed
```

Two ways to use it:

- **Folder version** — open `index.html`. Easiest to edit, and what you'd upload to a host.
- **Single file** — `single-file-build.html` has the CSS and every photo embedded. Drop it
  anywhere, email it, open it offline. Nothing external except the Google Fonts link.

Both render identically.

## Running it

Just double-click `index.html`. To serve it locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

To publish: upload the whole folder to Netlify, Cloudflare Pages, GitHub Pages or any
static host. No configuration needed.

## Things you'll probably want to change

**The contact form.** It currently falls back to `mailto:`, which opens the visitor's own
mail app and is unreliable. For real submissions, change the form tag in `index.html`:

```html
<form action="https://formspree.io/f/YOUR_ID" method="POST">
```

Formspree, Netlify Forms and Basin all work with the existing field names.

**Ivette's photo.** The About section uses a workspace photo. To use a real headshot,
replace the `<img>` inside `<figure class="about-figure">` with your file — a portrait
crop around 1100×880 fits the frame without any CSS changes.

**Colors.** All of them are custom properties at the top of `css/styles.css`:

```css
--ink:   #14212b   /* near-black navy: text, borders, the door jamb */
--door:  #f5b811   /* the yellow */
--amber: #b57d02   /* darker yellow: focus rings, shadows on dark */
--paper: #fcf9f3   /* page background */
--sand:  #efe6d4   /* pricing band background */
```

Change `--door` and the whole site re-themes.

**Fonts.** Bricolage Grotesque (headings) and Source Serif 4 (body), loaded from Google
Fonts in the `<head>`. Swap the link and the `--sans` / `--serif` variables together.

## How a few things work

**The door opens on load.** `.door` is a yellow panel rotated in 3D with
`transform: rotateY()` over a photo sitting behind it in `.jamb`. It's one CSS keyframe
animation, `@keyframes open`. Under `prefers-reduced-motion: reduce` the door is simply
drawn already-open with no movement.

**The plan matcher.** The three buttons above the pricing cards are hidden radio inputs.
When one is checked, `#pricing:has(#acc2:checked) .plan[data-fit="priority"]` highlights
the matching card. Pure CSS — `:has()` works in all current browsers. If a very old
browser ignores it, the buttons simply do nothing and all three plans stay readable.

**The doorsill mark.** The small yellow square with two dark edges before each section
label is one element, `.sill`, drawn entirely with layered CSS gradients.

## Accessibility notes

Every photo has alt text (decorative backgrounds use `alt=""`). The form fields have real
labels, the contact-preference radios sit in a `fieldset` with a `legend`, and there's a
skip link before the header. Focus outlines are visible on every interactive element.
Colors were checked for contrast against their backgrounds.

## Image credits

The photographs come from open-source website themes distributed under permissive
licenses (Start Bootstrap, Themefisher, Zerostatic). They're placeholders standing in for
the real business photography — swap them for actual photos of Ivette and her workspace
before this goes live.
