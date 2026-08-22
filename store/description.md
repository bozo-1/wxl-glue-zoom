# Glue Zoom

Scroll-wheel zoom on the character customization screen, with head-and-chest framing tuned per race.

In the stock client the character creation screen is fixed at one distance — you can't zoom in for a
closer look at your character's face, gear, or details. This module adds smooth mouse-wheel zoom with
framing that keeps each race's head and chest composed at every zoom level.

- **Scroll wheel** — smooth, uniform zoom glide; every notch lands as a continuous motion, not a jump.
- **Per-race framing** — all 20 race/gender pairs were calibrated visually. Short races scale up,
  tall races scale down, so the head and chest land at the same screen position at max zoom for
  everyone.
- **Rotation** — click-drag rotates the character while zoomed in, natively, and the zoom stays put.
- **Scoped** — only active on the character customization screen; does nothing anywhere else.

## How it's done

The zoom is a camera FOV drive on the glue camera (`cam+0x114`), the same projection the screen
already uses. The framing is a model-space placement scale anchored at the feet, applied at the
final draw call so it never fights the engine's own transforms. Each race's endpoint values come
from the calibration table embedded in the module; unknown models fall back to a fitted formula.

## Requirements

WarcraftXL on a 3.3.5a client, build **12340**.