

https://github.com/user-attachments/assets/f8da7962-46ea-4207-8387-62a29ce84322


# wxl-glue-zoom

Scroll-wheel zoom with per-race head framing on the character customization screen.

In the stock client the character creation screen is fixed at one distance — you can't zoom in for a
closer look at your character's face, gear, or details. This module adds smooth mouse-wheel zoom
with intelligent framing that keeps each race's head and chest perfectly composed, no matter how
close you go.

## How it works

- **Scroll wheel** — smoothly zooms in and out, with a uniform glide so every notch feels continuous.
- **Per-race framing** — each of the 20 race/gender pairs was calibrated visually so the head and chest
  land at the same screen position at max zoom. Gnomes scale up; Tauren and Night Elves scale down;
  the framing tracks the zoom at every step.
- **Rotation** — click-drag to rotate the character while zoomed in, exactly like the native rotation.
  Zoom stays where you set it.
- **Clean** — only activates on the character customization screen; does nothing in the world or menus.

## Requirements

WarcraftXL on a 3.3.5a client, build **12340**.
