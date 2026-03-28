# 🥊 Boxing Heavy Bag Combo Timer

A single-file, zero-dependency progressive web app for heavy bag training. Built as a fully offline, installable HTML file — no server, no framework, no build step.

---

## Features

### ⏱️ Timer Engine
- Configurable **warmup**, **round**, and **rest** durations (in seconds)
- Up to **40 rounds** per session
- Live countdown with total session time always visible
- Bell sound at every phase transition
- **Pause / Resume** mid-session
- **Screen Wake Lock** — prevents the display from sleeping during training (Chrome/Safari)

### 🥊 Combo System
- **Markov-chain combo generator** — produces realistic boxing combinations on the fly using weighted transitions between all 8 punches:
  - `1` JAB (L) · `2` CROSS (R) · `3` HOOK (L) · `4` HOOK (R)
  - `5` UPPER (L) · `6` UPPER (R) · `7` OVER (L) · `8` OVER (R)
- Combos favour realistic boxing flow: jab as opener, left–right alternation, power shots as finishers
- Variable length: 2–8 punches, weighted toward 3–5
- **"Up Next"** preview: during warmup and rest the next round's combo is shown dimmed so you can visualise it before the bell

### 🎛️ Combo Editor (Settings Screen)
- Pre-generates one combo per round before you start
- Edit any combo before the session:
  - **Click a badge** → cycles through all 8 punch types
  - **Hover → ×** → removes that punch
  - **+** button → adds the next logical punch
  - **↺** per row → randomises that round
  - **↺ Shuffle all** → regenerates all combos at once
- **Drag & drop** to reorder rounds (grab any row and drop it anywhere)
- All edits are saved instantly

### 💾 Persistence
- Settings and combos are **auto-saved to localStorage** on every change
- Everything is restored exactly as you left it on next visit
- **Reset** button wipes localStorage and restores all defaults (6 rounds, 10 s warmup, 180 s round, 30 s rest)

### 📺 Picture-in-Picture
- **PiP button** mirrors the entire workout view into a floating window
- Lets you keep the timer visible while watching tutorials, music, or anything else on screen

### 📱 Fully Responsive
- Fluid punch cards scale with container width using CSS Container Queries (`cqi` units)
- Works from a quarter-width browser window up to full widescreen
- No horizontal scroll at any size, even with 8-punch combos
- Tested on MacBook Air M1 (Chrome) at small window sizes

---

## How to Use

1. **Open `index.html`** in any modern browser — nothing to install, no internet needed
2. Adjust rounds, warmup, round, and rest durations in the Settings panel
3. Review and edit the generated combo for each round in the **Round Combinations** editor
4. Hit **▶ Start workout** — the bell fires and the clock starts
5. During warmup and rest, glance at the **Up Next** card to preview the incoming combo
6. Use **❚❚ Pause** any time; the session resumes exactly where you left off
7. Tap **⧉ PiP** to float the timer over other windows

---

## Technical Notes

| Aspect | Detail |
|---|---|
| Architecture | Single `BagTimerApp` object with named modules |
| Styling | CSS custom properties, `clamp()`, Container Queries, `100svh` |
| Persistence | `localStorage` (key: `bagtimer_v1`) |
| Wake Lock | `navigator.wakeLock.request("screen")` — Chrome 84+, Safari 16.4+ |
| PiP | `documentPictureInPicture` API — Chrome 116+ |
| Combo generation | Markov chain with 8×8 weighted transition table |
| Dependencies | **None** — pure HTML + CSS + vanilla JS |
| File size | ~150 KB (includes embedded audio) |

---

## Browser Support

| Browser | Timer | Wake Lock | PiP |
|---|---|---|---|
| Chrome 116+ | ✅ | ✅ | ✅ |
| Safari 16.4+ | ✅ | ✅ | ❌ |
| Firefox | ✅ | ❌ (silent) | ❌ (silent) |
| Edge 116+ | ✅ | ✅ | ✅ |

---

## Credits

**App concept & product direction** — Arturo Serna Leon  
**Design, architecture & all code** — [Perplexity AI](https://www.perplexity.ai) (Sonnet 4.6 via Perplexity)  
Built entirely through iterative conversation — no external editor, no copy-paste, no manual code edits.
