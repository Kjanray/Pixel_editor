# LED Matrix Pixel Editor

A browser-based pixel art editor for designing sprites and screens for WS2812B LED matrices, built for FPGA projects using Lucid V2 / Alchitry.

Built for **50.002 Computation Structures** at SUTD. Feel free to use, modify, and share.

---

## What It Does

A single-file HTML tool ([led_pixel_editor.html](led_pixel_editor.html)) that lets you visually design pixel art and export it as Lucid V2 `const` arrays ready to paste into your `.luc` ROM files.

- **Visual editing** — click or drag to paint pixels, type R/G/B values, undo per pixel
- **Multiple profiles** — ships with EASY/MED/HARD; add unlimited custom screens
- **Resizable grid** — 4×4 up to 256×256 (default 32×32), pixel data preserved on resize
- **Lucid V2 import & export** — live code preview, copy individual or all profiles, paste existing code back to reconstruct the grid
- **PNG export** — scaled-up nearest-neighbor PNGs for docs and previews
- **Session save/load** — `.ledpx` files store everything (profiles, grid size, settings) so you can share and resume
- **Settings** — color order (GRB/RGB/BGR/…), const prefix, `$reverse()` toggle for serpentine wiring

---

## Getting Started

Download `led_pixel_editor.html` and open it in any modern browser. No server, no install, no build step.

---

## Workflow

```
1. Select or create a profile (e.g. "EASY")
2. Click pixels and set R/G/B values
3. Expand the Lucid code panel for live output
4. Click "Copy EASY" or "Copy All", paste into your .luc ROM
5. Save Session to keep your work as .ledpx
```

---

## Lucid V2 Output Format

```verilog
// EASY — direct 24-bit GRB per pixel
const DISPLAY_EASY = $reverse({
    24h050604, 24h050604, 24h050604, ...  // row 0
    ...
    24h000000, 24h000000, 24h324632, ...  // row 31
})
```

Each pixel is `24h` + 6 hex digits in your chosen color order. `$reverse()` handles serpentine wiring (odd rows read right-to-left). A 32×32 grid produces 1024 values.

---

## Common Pitfalls

**Colors look wrong on the matrix**
Check **Color Order** in Settings — WS2812B uses **GRB**, not RGB.

**Image is mirrored on the matrix**
If your matrix isn't serpentine-wired, uncheck the `$reverse()` toggle in Settings.

---

## Tech Stack

Single HTML file, vanilla JS, Canvas + Blob APIs, zero dependencies, runs entirely client-side.

---

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, ship it.
