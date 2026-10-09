# Grace Kallman — composer portfolio

Static one-page site. No framework, no build step, no dependencies. Open `index.html` and it works.

Replaces the previous Wix site (`gracekatherine2002.wixsite.com/my-site`) while keeping its
layout, palette, typography and motion.

## Files

```
index.html      the whole site (inline CSS + JS)
vercel.json     static config — clean URLs, cache + security headers
images/         self-hosted photos (no Wix CDN dependency)
  hero.jpg          library portrait — hero + contact background
  about.jpg         performing with cello — about section
  v-corvette.jpg    rescore thumbnails
  v-spring.jpg
  v-charade.jpg
  v-sintel.jpg
```

## Design reference

Taken by measurement from the live Wix site, not by eye:

| Token | Value | Used for |
| --- | --- | --- |
| `--red` | `#8B0000` | ABOUT band, solid header on scroll |
| `--red-nav` | `rgba(139,0,0,.77)` | translucent header over the hero |
| `--brown` | `#7B503B` | contact section base tone |
| `--ink` | `#0d0d0d` | page background |
| Display font | **Aboreto** | `GRACE KALLMAN`, section headings |
| Body font | **Work Sans** (200–600) | nav, body copy, captions |

Hero `h1` uses very wide tracking (~0.7em at desktop) to match the original, with a matching
`text-indent` so the right edge stays flush.

## Embeds (live, not copied)

- **Music player** — ReelCrafter album `5ad47d9b-381b-4eb7-a070-f0b4faf4c565`, the same embed the
  Wix site used. The track list (ORCHESTRAL / CHAMBER / HYBRID / ELECTRONIC, 10 tracks) is served by
  ReelCrafter, so it stays in sync when Grace updates it. The audio files themselves are
  expiring signed CloudFront URLs and **cannot** be self-hosted.
- **Rescore videos** — four YouTube videos, click-to-load via `youtube-nocookie.com`. Nothing is
  requested from YouTube until the viewer presses play.

## Motion

- Hero background parallax on scroll (`requestAnimationFrame`, transform only).
- `background-attachment: fixed` parallax behind the music section.
- `IntersectionObserver` fade + slide-up reveals, staggered 90ms between siblings.
- Smooth-scroll anchors with `scroll-padding-top` so the sticky header never covers a heading.
- Every one of the above is disabled under `prefers-reduced-motion: reduce`.

## Local preview

```bash
cd <repo>
python -m http.server 5055
# http://127.0.0.1:5055
```

## Deploy

Already deployed on Vercel. To connect this repo for push-to-deploy:

1. Vercel dashboard → the project → **Settings → Git → Connect Git Repository**
2. Pick `Dukotah/grace-kallman`, branch `main`
3. Framework preset **Other**, root directory `./` — no build command, no output directory

After that every push to `main` redeploys automatically.

Or deploy straight from the CLI:

```bash
vercel deploy --prod
```

## Swapping images

Drop a replacement in `images/` using the same filename. Keep the hero wide (≥2000px) — it is used
full-bleed on both the hero and the contact section. `about.jpg` is cropped to 4:5.
