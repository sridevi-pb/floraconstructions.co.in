# Flora Constructions — Website

Single-file website. HTML, CSS, JavaScript and the logo artwork all live inside
`index.html`. No build step, no dependencies, no image folder to upload.

---

## 1. Contact form — already connected

The form posts to your endpoint: **https://formspree.io/f/mwlkazjj**

Nothing to configure. One thing to do once, though: **send a test enquiry yourself
after the site goes live.** Formspree emails you a confirmation link on the very first
submission, and enquiries stay pending until you click it.

To point the form somewhere else later, open `index.html` and change one line near the
top of the `<script>` block:

    var FORMSPREE_ID = "mwlkazjj";

**Fields that reach your inbox:** Full Name, Mobile Number, Email Address, Project
Location, Project Type, Approximate Built-up Area, Estimated Budget, Requirements,
plus `interested_in` (which button or package the visitor clicked) and `page_source`.

**If a submission fails,** the visitor sees a message with your phone number rather
than a dead form — the site never swallows a lead silently.

---

## 2. Robot / spam protection

Three layers, all built in, none of them requiring an external service or slowing the
page down:

1. **Human check** — a small sum ("7 + 4 =") the visitor answers before the form will
   send. The numbers are generated fresh in the browser on every page load and after
   every submission, so a bot cannot learn the answer. There's a refresh button if the
   question is unclear, and it works with a keyboard and screen readers.
2. **Honeypot field** — a hidden `_gotcha` input that people never see. Bots fill in
   every field they find; if that one has anything in it, the submission is dropped.
   Formspree also checks this field on their side.
3. **Time trap** — anything submitted within 3.5 seconds of the page loading is a
   script, not a person, so it is rejected with a polite message.

Wrong answers are caught before anything is sent, so bad submissions never reach your
inbox and never count against your Formspree quota. The answer itself is not sent with
the form — it's only used to unlock the send.

**Want Google reCAPTCHA as well?** Formspree offers it on their paid plans — turn it on
in your form's settings there; it applies server-side and needs no change to this file.

---

## 3. Deploy

Upload `index.html` to any host — it works as-is:

| Host | How |
|------|-----|
| Netlify / Vercel | Drag the folder onto the dashboard |
| GitHub Pages | Commit `index.html` to the repo root, enable Pages |
| cPanel / shared hosting | Upload `index.html` to `public_html` |
| Hostinger / GoDaddy | Upload via File Manager to the site root |

The file must be named **index.html** to load as the home page.

---

## 4. Your logo

Your logo file is used exactly as supplied — nothing cropped, recoloured or redrawn.
It appears in four places, all from the same untouched artwork (only scaled down for
the web):

- **Header** — as a rounded 52 px badge beside the FLORA CONSTRUCTIONS name
- **Loading screen** — 260 px, centred
- **Footer** — 190 px
- **Browser tab icon**

To replace it, search `index.html` for `data:image/jpeg;base64,` — there are three
matches: the `--logo` variable at the top of the `<style>` block (used by the loading
screen and the footer), the header `<img>`, and the favicon in `<head>`. Swap each for
a path such as `images/logo.jpg` if you'd rather keep the logo as a separate file.
To change how big it appears, edit `.brand-logo`, `.load-logo` and `.foot-logo`.

---

## 5. Light & dark themes

Both ship with the site.

- A first-time visitor gets whatever their device is set to (Windows/macOS/Android
  light or dark mode).
- The sun/moon button in the header — and a labelled button in the mobile menu —
  switches themes.
- Their choice is remembered on that device.
- The theme is applied before the page paints, so there's no white flash on load.

To force one theme for everyone, replace the `try{...}catch{...}` body in the small
script at the top of `<head>` with:

    document.documentElement.setAttribute("data-theme","dark");   // or "light"

### Colour palette (taken from the logo)

| Role | Light theme | Dark theme | From the logo |
|------|-------------|-----------|---------------|
| Primary / CTA | `#D4006A` → `#A80048` | `#FF2D86` → `#C4005C` | roof + FLORA wordmark |
| Positive (ticks, success) | `#3E8E0E` | `#7FD13B` | leaf + script tagline |
| Informational (tags, icons) | `#0079C8` | `#3BA9F0` | tower blocks + window |
| Text | `#0B2545` | `#E9EFF8` | CONSTRUCTIONS navy |
| Fine rules / package tiers | `#B08028` | `#D9A441` | gold divider lines |

These are CSS variables at the very top of the `<style>` block — `--brand`, `--green`,
`--blue`, `--gold`, `--bg`, `--surface`, `--text`. Change one and it updates everywhere.
`--brand-rgb` must stay in sync with `--brand` (same colour written as `R,G,B`).

---

## 6. Responsive behaviour

Checked at 320, 340, 360, 390, 414, 480, 540, 600, 768, 834, 912, 1024, 1112, 1160,
1200, 1260, 1320, 1400, 1440, 1600 and 1920 px — no sideways scrolling at any of them.

| Width | Navigation | Layout |
|-------|-----------|--------|
| 1400 px and up | Full menu + phone number + Get Free Quote | Everything side by side |
| 1200 – 1399 px | Full menu + Get Free Quote (phone number hidden to make room) | Two columns |
| Below 1200 px | Hamburger → full-screen menu with theme switch and Call/WhatsApp | Sections stack progressively |
| Below 760 px | Hamburger | Single column, tighter spacing |
| Below 430 px | Hamburger, logo badge only | Compact type, buttons and cards |

The desktop menu only appears where the whole row genuinely fits; below that the
hamburger takes over, so nothing is ever clipped off the right edge.

---

## 7. Things you may want to change

| What | Where |
|------|-------|
| Phone number | Search for `7904610062` — appears in tel:, wa.me and display text |
| WhatsApp number | Search for `wa.me/917904610062` (91 = India country code) |
| Project photos | Search for `PROJECTS = [` in the script — swap the `img:` values |
| Service / section photos | Search for `images.unsplash.com` in the HTML |
| Adding an email address | Add an `info-item` block in the Contact section |

Photos are Unsplash stock loaded from their CDN. Replacing them with real Flora
project photos is the single biggest upgrade to the site's credibility.

---

## 8. What's in the site

Menu: HOME · ABOUT · SERVICES · PROJECTS · PACKAGES · WHY US · FAQ · CONTACT
Lead buttons: GET FREE QUOTE · CALL NOW · WHATSAPP US · BOOK SITE VISIT

- Animated hero with rotating imagery, blueprint grid and drifting particles
- 6 services, 6-step process timeline that draws itself as you scroll
- Filterable project gallery with a keyboard-accessible lightbox
- 3 construction packages — no fixed rates published, estimate-request buttons instead
- Why Us, FAQ accordion, enquiry form, floating call/WhatsApp dock
- Every "Enquire" and "Get Project Estimate" button pre-fills the form with that
  service or package, so each lead tells you what it is about
- Keyboard accessible, honours reduced-motion settings, SEO meta tags and
  LocalBusiness structured data included
