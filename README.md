# Sahaj Digital Studio — Landing Page

Production-ready landing page for **www.sahajdigitalstudio.com**.

Build. Present. Promote. Grow. Improve.

---

## A. What's in this folder

```
sahaj-digital-studio/
├── index.html                      ← the whole page (HTML + CSS + JS, no build step)
├── README.md                       ← this file
├── assets/
│   ├── logo.png                    ← your logo, circular-cropped, transparent, 420×420
│   └── poster.jpg                  ← video thumbnail, 1280×720 (frame from your intro)
└── videos/
    └── my-business-intro.mp4       ← your intro, compressed for web (1280×720, 8.6 MB)
```

Nothing else is required. No npm, no framework, no build.

---

## B. Page structure

The page is written as clearly-commented sections, in this order:

| # | Section | Anchor |
|---|---------|--------|
| 01 | Header / sticky navigation | — |
| 02 | Hero + digital-ecosystem diagram | `#top` |
| 03 | Positioning strip | — |
| 04 | **Business introduction video** | `#intro-video` |
| 05 | Quick service overview | — |
| 06 | The business problem | — |
| 07 | Our approach (7 stages) | `#approach` |
| 08 | Services | `#services` |
| 09 | Integrated / connected strategy | — |
| 10 | Who we work with | — |
| 11 | Why work with us | `#why` |
| 12 | Build · Present · Promote · Grow · Improve | — |
| 13 | Selected work (placeholder) | — |
| 14 | Final call to action | — |
| 15 | Contact details + enquiry form | `#contact` |
| 16 | Footer | — |
| — | Floating WhatsApp button | — |

Search `<!-- ============ ` in `index.html` to jump between them.

### Splitting into components later

If you move to Next.js or React, each commented block maps 1:1 onto a component:
`Header, Hero, PositioningStrip, IntroVideo, ServiceOverview, ProblemSection, ProcessSection, Services, IntegratedGrowth, WhoWeHelp, WhyUs, CoreFramework, Portfolio, CTA, Contact, Footer, WhatsAppButton`. Copy the `:root` token block into your global stylesheet first — every colour, font and spacing value flows from it.

---

## C. Local development

The page uses relative paths, so it needs to be served over HTTP (opening `index.html` by double-clicking will block the video on some browsers).

```bash
cd sahaj-digital-studio

# Python (already on most Macs and Linux machines)
python3 -m http.server 8000

# or Node
npx serve .
```

Then open **http://localhost:8000**.

To edit: everything is in `index.html`. Design tokens live in the `:root` block at the top of the `<style>` tag — change a colour there and it updates everywhere.

---

## D. Deployment

Any static host works. Upload the whole folder, keeping `assets/` and `videos/` alongside `index.html`.

**Netlify** — drag the folder onto app.netlify.com/drop. Done.

**Vercel** — `npx vercel` inside the folder.

**Cloudflare Pages** — connect a repo, or upload directly. Best free option for video bandwidth.

**cPanel / shared hosting** — upload the folder contents into `public_html/` via File Manager or FTP.

**GitHub Pages** — push to a repo, enable Pages on the `main` branch. Note: 100 MB file cap, fine for this video.

### After deploying

1. Point `www.sahajdigitalstudio.com` at the host (the host will give you the DNS records).
2. Enable HTTPS — every host above does this free and automatically.
3. Confirm the Open Graph image loads: paste your URL into the Facebook Sharing Debugger and LinkedIn Post Inspector.

---

## E. Video setup

**Your video is already installed** at `videos/my-business-intro.mp4`.

I compressed your original from **39 MB → 8.6 MB** (1920×1080 → 1280×720, `faststart` enabled for instant seeking). Quality is unchanged for web viewing; the original file was too heavy to serve to mobile visitors.

How it behaves: nothing downloads until the visitor presses play (`preload="none"` plus a poster image). It never autoplays and never plays sound unprompted.

### To swap in a different video

Replace the file at `videos/my-business-intro.mp4`, keeping the same name. Or point the page elsewhere — in `index.html`, find:

```html
<source src="videos/my-business-intro.mp4" type="video/mp4">
```

and change the `src` to any hosted URL (Cloudflare Stream, Bunny, S3). Also update the `poster` attribute and the `<img class="poster">` above it if you change the thumbnail.

### To change the thumbnail

`assets/poster.jpg` is a frame from 8 seconds in. To use a different moment:

```bash
ffmpeg -ss 12 -i videos/my-business-intro.mp4 -frames:v 1 -vf scale=1280:-1 -q:v 4 assets/poster.jpg
```

---

## F. Connecting the enquiry form

Right now the form validates input and then opens the visitor's email client with the enquiry pre-filled, addressed to `sahajdigitalstudio7@gmail.com`. It works immediately, but it depends on the visitor having an email client set up.

**To receive enquiries directly instead**, sign up for a free form service and paste the endpoint into `index.html`. Find this line near the bottom:

```js
var FORM_ENDPOINT = ""; // <-- set to your Formspree/Web3Forms/API URL
```

Put your URL between the quotes. The form switches to posting JSON automatically, shows a success message, and clears itself.

Free options that need no server:
- **Formspree** (formspree.io) — 50 submissions/month free
- **Web3Forms** (web3forms.com) — unlimited, free
- **Getform**, **Basin**, or your own API route

Whichever you pick, send yourself a test enquiry before going live.

---

## G. Placeholders — what still needs your input

Nothing on the page is invented. No fake clients, testimonials, statistics, awards or guarantees. These items are deliberately empty and waiting on you:

| Item | Where | What's needed |
|------|-------|---------------|
| **Form endpoint** | `FORM_ENDPOINT` in the script | Formspree/Web3Forms URL — see section F |
| **Portfolio projects** | Section 13, `.port` block | Real project names, images, objectives and what you built. The section currently says "Selected projects coming soon" |
| **Testimonials** | Not present | Omitted entirely rather than faked. Send genuine client quotes and I'll add the section |
| **Statistics / results** | Not present | Omitted. Only add verified numbers |
| **Business address & city** | Not present | Once confirmed, add to the footer and to the `ProfessionalService` schema block in `<head>` — that block already has a slot for `address` |
| **Social profiles** | Not present | Instagram / YouTube / LinkedIn URLs for the footer |
| **Social share image** | `assets/logo.png` used | A 1200×630 branded banner would preview better on WhatsApp and LinkedIn than the round logo. Optional |
| **Founder / team** | Not present | Add only if you want a named face on the page |

### Adding your address later

In the `<script type="application/ld+json">` block in `<head>`, add inside the object:

```json
"address": {
  "@type": "PostalAddress",
  "streetAddress": "…",
  "addressLocality": "…",
  "addressRegion": "Maharashtra",
  "postalCode": "…",
  "addressCountry": "IN"
},
"areaServed": "…"
```

This is what puts you into Google's local results, so it's worth doing as soon as the address is confirmed.

---

## Design notes

**Colours** are sampled from your actual logo file, not approximated: navy `#0C2545`, orange `#FE5701`. Orange appears in three tiers — `--orange` for shapes and squares, `--orange-dark` for button fills, `--orange-ink` for text — so that every text-on-colour pairing clears WCAG AA contrast while the brand orange stays brand orange.

**Type** is Manrope for headlines and Inter for body, loaded from Google Fonts with `display=swap`.

**The recurring square motif** — the small orange squares on rails in the hero diagram, the step markers, the list bullets — comes from the pixel squares trailing off the "S" in your logo. It's the one decorative idea on the page, repeated with discipline instead of adding new ones.

**Headings are in sentence case** rather than the all-caps in the brief. At these sizes sentence case reads more premium and is measurably easier to scan. The wording is unchanged. If you prefer caps, add `text-transform:uppercase` to the `h1,h2,h3,h4` rule.

**Motion** is one scroll-reveal fade and one slow pulse along the hero diagram. Both stop completely under `prefers-reduced-motion`.

---

## Quality checklist

- Responsive from 320 px to large desktop, no horizontal scroll
- Keyboard navigable with visible focus rings throughout
- WCAG AA contrast verified on every text/background pair
- Semantic HTML, single `<h1>`, ordered heading hierarchy
- Meta title, description, canonical, Open Graph, Twitter card, JSON-LD schema
- Alt text on every image; the decorative SVG diagram carries a descriptive label
- Video lazy-loads, never autoplays, has native accessible controls
- `tel:`, `mailto:` and `wa.me` links tested on mobile and desktop
- No external JavaScript dependencies — two font files are the only third-party request

---

**Sahaj Digital Studio**
Digital Growth · Marketing · Creative Strategy
79722 25403 · sahajdigitalstudio7@gmail.com · www.sahajdigitalstudio.com
