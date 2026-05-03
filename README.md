# Tasks, Not Just Jobs — LARC Counselor Toolkit

Public-facing landing page for **Breakout 5** of the **LARC K–16 Counselor Summit**.

Live URL: https://vrcalip-pixel.github.io/larc-counselors/

Hosts the session toolkit, slide deck, and supporting resources for K–16 counselors. Designed mobile-first so attendees can scan the QR code from the slide deck and immediately access materials on their phones.

---

## What's in this repo

```
larc-counselors/
├── index.html                          # The landing page (single-file site)
├── README.md                           # This file
└── assets/
    ├── LARC_Tasks_Not_Just_Jobs.pptx   # Slide deck
    ├── LARC_Counselors_AI_Toolkit.pdf  # One-page handout
    ├── qr-larc-counselors.png          # QR code (PNG, for slide insertion)
    └── qr-larc-counselors.svg          # QR code (SVG, scalable)
```

The site is **a single static HTML file** with inline CSS — no build step, no JavaScript framework, no external dependencies beyond Google Fonts. This makes it fast to load on conference Wi-Fi and trivial to maintain.

---

## Deploying to GitHub Pages

1. Create a new public repo named `larc-counselors` under your GitHub account
2. Push these files to the `main` branch
3. Go to **Settings → Pages**
4. Under "Build and deployment," set:
   - **Source:** Deploy from a branch
   - **Branch:** `main` / `/ (root)`
5. Save. GitHub will build and publish within 1–2 minutes
6. Site will be live at `https://<your-username>.github.io/larc-counselors/`

If you ever want a custom domain (e.g. `larc.vincentcalip.com`), add a `CNAME` file with the domain and configure your DNS. Not necessary — the GitHub Pages URL is fine for conference distribution.

---

## Updating content

### Updating the deck or PDF
Replace the file in `/assets/` with the same filename. The page links use relative paths, so no HTML changes needed.

### Updating text on the page
Open `index.html` and edit directly. The structure is heavily commented with section markers like `<!-- HERO -->`, `<!-- THE BIG IDEA -->`, etc.

### Adding the session recording
The "Session recording" download card is currently `disabled` (greyed out). To activate it:

1. Upload the recording — recommended: YouTube unlisted, Vimeo, or direct MP4 in `/assets/`
2. In `index.html`, find the `disabled` recording card
3. Change `<a href="#" class="dl-card disabled" aria-disabled="true">` to `<a href="YOUR_VIDEO_URL" class="dl-card">`
4. Update the metadata text from "Coming soon" to actual length (e.g. "45 min · video")

Same pattern applies to the speaker notes card.

---

## QR code

The QR code in `/assets/` points to `https://vrcalip-pixel.github.io/larc-counselors/` and uses **high error correction (Level H)** — meaning it can survive about 30% visual damage and still scan reliably under poor lighting or from across a room.

### Insert into the slide deck
1. Open `LARC_Tasks_Not_Just_Jobs.pptx` in PowerPoint
2. Go to **slide 16** (the park slide)
3. Click on the dashed "QR CODE / (placeholder)" rectangle and delete it
4. Insert the QR via **Insert → Pictures → This Device** and pick `qr-larc-counselors.png`
5. Resize to roughly 2.2" × 2.2" and align to the same position

### If you change the URL
Regenerate the QR with any QR tool. The Python script used to make this one is below — it can be run locally with `pip install qrcode` if needed:

```python
import qrcode
url = 'https://vrcalip-pixel.github.io/larc-counselors/'
qr = qrcode.QRCode(error_correction=qrcode.constants.ERROR_CORRECT_H, box_size=20, border=2)
qr.add_data(url)
qr.make(fit=True)
img = qr.make_image(fill_color='#003366', back_color='#FFFFFF')
img.save('qr-larc-counselors.png')
```

Or use any free online QR generator — just keep the error correction level **High** and use LBCC navy `#003366` as the foreground color for visual consistency with the deck.

---

## Testing locally

Easiest method:

```bash
cd larc-counselors
python3 -m http.server 8000
```

Open `http://localhost:8000` in your browser. Test on both desktop and mobile (use Chrome DevTools device emulation, or actually open it on your phone via your local IP).

---

## Optional: scan analytics

GitHub Pages has built-in **Traffic Insights** at `Insights → Traffic` showing total views, unique visitors, and referrers. No code needed — this is sufficient for understanding session impact.

If you want page-level analytics without compromising counselor privacy, consider:

- **GoatCounter** (free, privacy-respecting, no cookies, GDPR-compliant) — add one `<script>` line
- **Plausible Community Edition** (self-hosted) — same idea, more features

Avoid Google Analytics — it adds cookie-consent overhead and creates privacy concerns for an audience of educators advising minors.

---

## Design notes

- **Colors:** LBCC navy `#003366`, gold `#FFB81C`, cream `#FAF7F0` — matched exactly to the slide deck for visual continuity
- **Type:** Lora (display) + Source Sans 3 (body), via Google Fonts. Falls back to Georgia + system sans if fonts fail to load
- **Accessibility:** Semantic landmarks, focus rings on interactive elements, `prefers-reduced-motion` honored, color contrast meets WCAG AA
- **Mobile-first:** Above-the-fold content prioritizes the two download buttons, sized at 60px+ tap targets

---

## Credit

Built for the **LARC K–16 Counselor Summit**, Breakout 5: *AI and its impact on the future workforce*.

Vincent Calip · Associate Professor · Long Beach City College
[vcalip@lbcc.edu](mailto:vcalip@lbcc.edu)

All session materials are free for educational use.
