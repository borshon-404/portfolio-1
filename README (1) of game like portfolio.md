# Mashzidul Tanun Borshon — My Digital Home
### A playable 3D portfolio website

> Visitors don't scroll a page — they control a character, walk through a front
> gate into a modern house, stroll down a hallway, and **open six doors** to
> discover the portfolio: **Home · About · Services · Projects · Blog · Contact**.

**Everything is in one file: `index.html`** (Three.js is inlined — no CDN, no
build step, no dependencies). Upload it anywhere and it works.

---

## 1 · Quick start

| | |
|---|---|
| **Run locally** | Double-click `index.html` (or serve the folder — not required) |
| **Deploy** | Upload `index.html` to `mashzidultanun.com` via your host / cPanel / Netlify / Vercel / GitHub Pages |
| **File size** | ~700 KB total (the 3D engine is ~600 KB of that; the game itself is ~50 KB) |

### Controls

| Desktop | Mobile |
|---|---|
| `W A S D` / Arrow keys — move | Virtual joystick (left side) — move |
| Mouse drag or click-to-lock — look | Swipe (right side) — look |
| `E` or click — open a door | Tap — open a door |
| `Shift` — run · Mouse wheel — zoom | |
| `ESC` — leave a page, back to the hallway | Return button in the top bar |

**Skip Exploration** (top-right, and on the welcome screen) opens a classic,
fully accessible navigation view — for anyone who can't or doesn't want to play.

---

## 2 · Editing your content — no 3D knowledge needed

Open `index.html` and find the **`CONTENT`** object near the top of the second
`<script>` (search for `CONTENT = {`). Everything editable lives there.

### Replace the placeholder projects
```js
projects: [
  { title:'Modern Agency Website', category:'Web Design',
    tech:['Figma','HTML','CSS'], 
    desc:'Describe the goal, your process and the result.',
    image:'images/project1.jpg',      // ← your image (drop the file next to index.html)
    url:'https://…' },                // ← real link ("View Project" button)
  …
]
```
While `image` is `null`, a generated placeholder cover is used. Delete a card
by removing one `{ … },` block; add more the same way. Category filter chips
are generated automatically from your categories.

### Add blog posts
```js
blog: [
  { title:'My Post', category:'WordPress', date:'Mar 2026',
    excerpt:'One or two hook sentences…', image:null },
  …
]
```
"Read More" currently expands a placeholder body — search for
`[Write the full article here` to put real article text per post.

### Contact details (currently safe placeholders)
In `CONTENT.contact`, replace:
- `email` → `[your-email@example.com]`
- `phone` → `[+880 1XXX-XXXXXX]`
- `socials` → your real LinkedIn / GitHub / Facebook / X URLs

The contact form is front-end only. To make it send, search for
`contactForm` in the file and point it at **Formspree** (easiest:
`action="https://formspree.io/f/YOUR_ID" method="POST"`) or your own backend.

### About / Services / Home text
All in `CONTENT.about`, `CONTENT.services`, `CONTENT.home`. Anything wrapped in
`[brackets]` is a marked placeholder for you to replace — nothing was invented
(no fake awards, clients, years of experience, or contact details).

### To change the 3D world
Search for these clearly-marked sections in the same script:
`CFG` (movement & camera feel), `DOOR_DEFS` (door names/positions),
`buildHouse/buildRooms/buildDecor` (architecture), `buildCharacter` (avatar),
`A` (all sounds are synthesized — tweak or mute freely).

---

## 3 · How it works (architecture)

```
index.html
├─ <style>      … full UI/theme (charcoal + warm gold design system)
├─ <script>     … Three.js r128 (inlined, unmodified)
└─ <script>     … the game + site, in 11 modules:
   1  CONTENT      all portfolio data (the only part you normally edit)
   2  CFG / STATE  game tuning + global state
   3  UTILS        math + procedural textures (wood floor, plaques, art…)
   4  AUDIO        synthesized ambience, footsteps, door sounds (no audio files)
   5  WORLD        renderer, lights, house, six doors, show-rooms, decor
   6  CHARACTER    the avatar + procedural walk/idle animation
   7  PLAYER       movement, AABB collision, third-person camera (wall-aware)
   8  TRANSITIONS  door swing → walk-through → fade → page (and back)
   9  PAGES        readable HTML overlay pages (the "rooms")
   10 UI / INPUT   HUD, prompts, keyboard / mouse / touch joystick
   11 LOOP / BOOT  main loop + loading sequence + WebGL fallback
```

**The loop:** explore → approach a door → `E — Open Projects` → the door
swings open, the character walks through, the camera glides into the glowing
room → the Projects page fades in → **Return to Hallway / ESC** puts the
player back in front of that door → keep exploring.

### Performance notes
- **~200 draw calls, ~7,000 triangles** — lighter than most 3D websites.
- All textures are generated procedurally on a canvas (no image downloads).
- Only one shadow-casting light (the moon); interior lights are shadow-free.
- Pixel ratio is capped (1.5× on touch devices) and rendering **pauses**
  while a portfolio page is open.
- Portfolio/blog images use `loading="lazy"` — set real image URLs and they
  only load when scrolled to.
- If WebGL is unavailable, the site automatically opens the accessible
  Skip-Exploration view instead of breaking.

---

## 4 · Files

| File | Purpose |
|---|---|
| `index.html` | **The whole website** — deploy this |
| `README.md` | This file |
| `screenshots/` | Stills of the experience (welcome, hallway, doors, pages) |

---

## 5 · Suggested next steps

1. Replace the `[bracketed]` placeholders in `CONTENT` (about, contact).
2. Add real projects (`CONTENT.projects`) with images + links.
3. Write 1–3 real blog posts (`CONTENT.blog`).
4. Hook the contact form to Formspree/your backend.
5. Optional: add Google Analytics / Meta tags in `<head>`.

*Built as a playable digital home — mashzidultanun.com*
