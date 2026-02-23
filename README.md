# pb2.io — punks on billboards, worldwide

A global archive of CryptoPunk billboard exhibitions, inspired by [radio aporee](https://aporee.org) — a living map of the world rendered through field recordings. pb2.io does the same for pixel art: a living map of every city where a CryptoPunk has appeared on a digital billboard, verified on-chain.

---

## What is pb2.io?

CryptoPunks have been appearing on digital billboards around the world — Times Square, Shibuya Crossing, Piccadilly Circus, the Champs-Élysées. pb2.io is the permanent public record of all of it.

Every exhibition submitted to pb2.io is reviewed and issued a **Proof of Exhibition (POE)** — an on-chain attestation that documents the punk, the location, the billboard operator, the dates, and links to photographic evidence. The POE is mintable as an NFT, turning each real-world exhibition into a verifiable artifact.

---

## Features

**Global map** — an SVG world map with live pins for every documented exhibition. Green pins are POE-verified; orange pins are pending review. Hover any pin to preview the punk and city; click to open the full exhibition record.

**Live feed** — a scrolling sidebar of recent exhibitions, newest first, with real CryptoPunk thumbnails pulled from the [punks.art API](https://punks.art/api). New submissions appear in real time.

**Exhibition detail** — clicking any pin or feed item opens a full detail view in the right panel: a simulated billboard display showing the punk at full size, the complete POE data record (date, billboard vendor, duration, operator, on-chain TX hash), a proof photo grid, and the punk's trait attributes.

**Submit Exhibition** — a submission form for punk owners to document their exhibition. Accepts the CryptoPunk ID, wallet address for ownership verification, billboard location, operator/vendor, exhibition dates, proof photos, and additional notes. All submissions go through a review process before a POE is issued.

**Light / dark theme** — a toggle in the nav switches between a dark mode (near-black with orange and green accents) and a light mode (warm off-white with sand tones, terracotta accent, and forest green for verified status). The preference is saved to `localStorage` and respects the system `prefers-color-scheme` setting on first visit.

---

## Tech stack

This is a fully self-contained static site — a single `index.html` file with no build step, no framework, no dependencies beyond two Google Fonts.

| Layer | Detail |
|---|---|
| Markup | Semantic HTML5 |
| Styles | Vanilla CSS with custom properties (`--var` system for full theme support) |
| Scripts | Vanilla JavaScript (ES2020+) |
| Fonts | [Bebas Neue](https://fonts.google.com/specimen/Bebas+Neue) (display) · [DM Mono](https://fonts.google.com/specimen/DM+Mono) (UI/data) |
| Punk images | [punks.art REST API](https://punks.art/api) — free, no auth required |
| Map | Hand-authored inline SVG with CSS variable fills |
| Hosting | GitHub Pages via Namecheap DNS |

---

## Punk image API

Punk images are served by **punks.art**, a free public API covering all 10,000 CryptoPunks. The URL format used throughout the site:

```
https://punks.art/api/punks/{ID}?format=png&size={px}&background=punk
```

The `background=punk` parameter applies the authentic CryptoPunks blue-grey background (`#638696`). No API key is required. If you use this project as a base, please consider crediting [punks.art](https://punks.art) per their request.

---

## Hosting & DNS

The site is hosted on **GitHub Pages** and served via a custom domain configured on **Namecheap**.

### GitHub Pages setup

1. Rename `pb2.html` → `index.html` and push to your repo's `main` branch
2. In the repo: **Settings → Pages → Deploy from branch → main / root**
3. Add a `CNAME` file to the repo root containing: `pb2.io`

### Namecheap DNS (Advanced DNS tab)

| Type | Host | Value |
|---|---|---|
| A Record | @ | 185.199.108.153 |
| A Record | @ | 185.199.109.153 |
| A Record | @ | 185.199.110.153 |
| A Record | @ | 185.199.111.153 |
| CNAME Record | www | `yourusername.github.io.` |

After saving, enable **Enforce HTTPS** in GitHub Pages settings once the SSL certificate provisions (typically within 30 minutes). DNS propagation can take up to 24 hours but usually resolves in minutes.

---

## POE — Proof of Exhibition

A Proof of Exhibition is an on-chain record that a specific CryptoPunk was displayed on a physical digital billboard in the real world. Each POE documents:

- CryptoPunk ID and owner wallet
- Billboard location, vendor/operator
- Exhibition dates and duration
- Photographic evidence (minimum 2 photos required; GPS metadata appreciated)
- On-chain transaction hash

POEs are verified by the pb2.io team before being published to the map. Verified exhibitions display a green `POE` badge in the feed and a green pin on the map. The **Mint POE** button in the detail panel allows owners to mint their verified POE as an ERC-721 token.

---

## Contributing an exhibition

1. Click **+ submit exhibition** in the top nav
2. Fill in your CryptoPunk ID and connect your wallet address for ownership verification
3. Enter the billboard location, operator, and exhibition dates
4. Upload at least 2 proof photos (JPG or PNG, max 10MB each; photos with GPS metadata embedded are strongly preferred)
5. Submit for review — the pb2.io team will verify and issue a POE, typically within 48 hours

---

## Theme system

All colors are defined as CSS custom properties in `:root` (dark) and `html.light` (light). There are no hardcoded color values outside of these two blocks, making it straightforward to add additional themes or adjust the palette.

```css
/* Dark (default) */
:root {
  --bg: #0a0a0a;
  --surface: #111;
  --accent: #ff3c00;
  --green: #00cc70;
  /* ... */
}

/* Light */
html.light {
  --bg: #f0ede8;
  --surface: #faf8f5;
  --accent: #e03000;
  --green: #007a45;
  /* ... */
}
```

Theme transitions are applied globally at 0.3s ease. Images, canvases, and SVG elements are excluded from transitions to prevent visual artifacts during the switch.

---

## Roadmap

- [ ] On-chain POE minting via ERC-721 or EAS attestation
- [ ] Wallet connect for submission ownership verification
- [ ] Replace SVG map with Mapbox / Leaflet for street-level detail
- [ ] Filter map by city, date range, punk type, or verification status
- [ ] Exhibition statistics page — most active cities, punk leaderboard
- [ ] Email/webhook notifications for submission status updates
- [ ] API endpoint for third-party integrations

---

## License

MIT — do whatever you like with the code. CryptoPunks imagery is property of Yuga Labs. Punk images served via the punks.art API; credit them if you build on this.
