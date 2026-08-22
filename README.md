<div align="center">

# 🔍 WXL Glue Zoom

**Scroll-wheel zoom with per-race head framing for the character customization screen**

A WarcraftXL module that adds smooth, native-feeling zoom to the 3.3.5a character
creation screen — with head-and-chest framing calibrated per race, so every character
composes perfectly no matter how close you go.

![version](https://img.shields.io/badge/version-v1.0-blue)
![license](https://img.shields.io/badge/license-GPL--3.0-green)
![client](https://img.shields.io/badge/client-3.3.5a%20(12340)-orange)
![renderer](https://img.shields.io/badge/renderer-D3D9-red)

<video src="https://github.com/user-attachments/assets/f8da7962-46ea-4207-8387-62a29ce84322" width="720" controls></video>

</div>

In the stock client the character creation screen is fixed at one distance — you can't
zoom in for a closer look at your character's face, gear, or details. **WXL Glue Zoom**
adds smooth mouse-wheel zoom with intelligent framing that keeps each race's head and
chest perfectly composed, no matter how close you go.

---

## ✨ Features

### 🖱️ Zoom

- **Scroll-wheel zoom** — smooth in and out with a uniform glide; every notch lands as a
  continuous motion, never a jump.
- **Linear perceived zoom** — the FOV and framing scale are composed so the on-screen
  growth rate is constant through the whole range. No "zoom first, scale later" weirdness
  on tall races.

### 🧍 Per-race framing

- **20 calibrated race/gender pairs** — each was visually tuned at max zoom so the head
  and chest land at the same screen position for everyone.
- **Gnomes scale up; Tauren and Night Elves scale down** — short races grow to fill the
  frame, tall races shrink to keep the face centered, and the framing tracks the zoom at
  every step.
- **Formula fallback** — any unlisted model still gets a fitted framing correction
  instead of being left at base scale.

### 🎯 Native feel

- **Rotation** — click-drag rotates the character while zoomed in, exactly like the
  native rotation. Zoom stays where you set it.
- **Scoped** — only activates on the character customization screen; does nothing in the
  world, menus, or character select.

---

## 🏗️ How it's done

```
scroll wheel
     ↓
s_t (smoothed, frame-rate independent)
     ↓
FOV zoom = 1 + (maxZoom − 1)·t          ← glue camera FOV (cam+0x114)
     ↓
scale    = (1 + (Z·S − 1)·t) / (1 + (Z − 1)·t)   ← placement scale, feet-anchored
     ↓
placement = rotBase · scale             ← single writer at the DIP seam
```

- **FOV drive** — the zoom is a camera FOV change on the glue camera, the same projection
  the screen already uses.
- **Framing** — a model-space placement scale anchored at the feet, applied at the final
  draw call so it never fights the engine's own transforms.
- **Drag-native rotation** — the rotation base is captured only while the engine is
  actually writing it, so click-drag rotates natively at any zoom.
- **Per-race table** — each race's `maxZoom` + `scale` endpoint comes from an embedded
  calibration table; unknown models fall back to a fitted formula.

---

## 📦 Installation

1. Download the latest `wxl-glue-zoom.dll` from the [Releases](https://github.com/bozo-1/wxl-glue-zoom/releases) page.
2. Copy it into your client's `Extensions/wxl-glue-zoom/` folder.
3. Launch the client and open the character creation screen — scroll to zoom.

The module is discovered and loaded by the WarcraftXL extension system; no configuration
needed.

---

## 🧰 Requirements

| Component | Requirement |
|---|---|
| 🎮 Game | World of Warcraft **3.3.5a** (build 12340) |
| 🧱 Client framework | **WarcraftXL** (wxl-core) |
| 🎨 Renderer | Direct3D **9** |
| 🔨 Build | wxl-core toolchain (MSVC, x86) for the DLL |

---

## 📁 Project structure

```
wxl-glue-zoom/
├── README.md                 ← this file
├── LICENSE
├── wxl.json                  ← hub manifest (id, version, listing)
├── src/
│   └── WxlGlueZoom.cpp       ← the whole module
└── store/
    └── description.md        ← hub store listing text
```

---

## 🙏 Credits

- **WarcraftXL** — client framework, RE infrastructure, and the offset database that made
  engine-native zoom and framing possible.
- **Blizzard Entertainment** — World of Warcraft, 3.3.5a.

---

## 📜 License

See [LICENSE](LICENSE). WarcraftXL and World of Warcraft assets remain property of their
respective owners; this project's code is licensed as stated in the LICENSE file.
