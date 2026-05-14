# HELIO Pro — Capture Guide

*How to photograph objects for photometric stereo*

---

## The Core Principle

Photometric stereo needs **the same scene lit from different directions**. Everything else stays identical:

```
FIXED:   camera position · focus · aperture · ISO · subject
VARIES:  light direction (one shot per position)
```

Minimum: **4 light positions** → basic normal map  
Recommended: **8–16 positions** → publication quality  
Archival: **32–64 positions** → full RTI / museum archive  

---

## Method 1 — RTI Dome

The most accurate method. A hemisphere of LEDs fires one at a time.

```
         ╔═══════════════════════╗
        ╔╝  RTI Dome (top view)  ╚╗
       ╔╝                         ╚╗
      ║  ●  ●  ●  ●  ●  ●  ●  ●   ║   ← LEDs fire one at a time
      ║  ●           ●  ●          ║
      ║  ●   SUBJECT   ●           ║   ← object on flat surface
      ║  ●  (chrome sphere nearby) ║   ← chrome ball for calibration
       ╚╗                         ╔╝
        ╚╗                       ╔╝
         ╚═══════════════════════╝
              ▲ camera hole at top
```

**Setup checklist:**
- [ ] Object flat on the baseboard
- [ ] Chrome sphere (≥25mm) visible in every frame
- [ ] Camera tethered — shoots automatically with each LED
- [ ] Exposure locked (Manual mode)
- [ ] One image per LED firing

**HELIO calibration:** Step 1B → Sphere Sync → draw circle on sphere → Accept

---

## Method 2 — Handheld Flash or Torch

No dome required. Move the light to 8–16 positions around the object.

```
   Top view of positions:

        N
    NW  ↑  NE
      \ | /
   W ─── ─── E      ← light positions
      / | \
    SW  ↓  SE
        S

   Side view:

        [camera overhead, fixed]
               │
    ┌──────────▼──────────┐
    │      SUBJECT        │   ← flat on table
    └─────────────────────┘
       ↗   ↑   ↑   ↑   ↖
      30°–60° elevation above table
```

**Tips:**
- Mark positions on the table with tape — be consistent
- Use the same flash power (or torch distance) every shot
- Lock focus before the first shot — do not touch the camera between shots
- Cover the room windows or shoot at night — ambient light causes errors
- Diffuse the light slightly for matte surfaces (tissue over torch)

**HELIO calibration:** Step 1C → Virtual Dome Calibrator → enter positions  
*Or:* AI Light Estimation (Step 1C → AI Estimate) as a last resort

---

## Method 3 — Fixed Spider Rig

Multiple fixed lights around a copy stand, firing individually.

```
         Light 3  (N)
              ●
             /
Light 2 ●───────────● Light 4
   (NW)  \    CAMERA   /  (NE)
          \      │    /
           \     │   /
    ┌───────────────────────┐
    │      BASEBOARD        │   ← subject here
    └───────────────────────┘
           /     │   \
          /      │    \
Light 8 ●        │     ● Light 5
              Light 6 (S)
```

**Advantages:**
- Nothing moves between shots — most consistent geometry
- Controller fires each LED in sequence automatically
- Export `.lp` file from controller software → import into HELIO

**HELIO calibration:**  
If you have a `.lp` file from your controller: Step 1C → Import .lp File  
If calibrating for the first time: Step 1B → Sphere Sync

---

## Exposure Settings

| Setting | Recommended |
|---------|-------------|
| Mode | Manual (M) |
| ISO | 100–200 (lowest native ISO) |
| Aperture | f/8–f/11 (sharpest zone, maximum depth of field) |
| Shutter | 1/125s (or flash sync speed) |
| White balance | Kelvin fixed (e.g. 5500K) or Custom white balance |
| Focus | Manual — lock before first shot |
| Stabilisation | Off (camera on tripod) |
| File format | RAW → export 16-bit TIFF, or JPEG at quality 95+ |

---

## Camera Positioning

```
   Ideal: camera directly overhead (0° tilt)

        Camera
          │  ← straight down
          │
          ▼
   ┌─────────────┐
   │   SUBJECT   │   ← parallel to sensor plane

   Acceptable: up to 10° tilt if subject fills the frame

   Avoid: steep angles — causes foreshortening in the depth map
```

---

## Subject Preparation

**Flat objects (manuscripts, prints, documents):**
- Use a suction mount or book cradle to keep the surface truly flat
- A 1mm bow across a 300mm page causes measurable depth error

**Coins and medals:**
- Mount obverse and reverse separately
- Use Plasticine or a ring mount to hold at exactly 0° tilt

**3D objects (ceramics, carvings):**
- PS works on relatively flat surfaces — max useful relief ~10–20% of object diameter
- For deeply 3D objects, consider photogrammetry instead

**Chrome sphere:**
- Diameter: 25–50mm is ideal (larger is easier to detect)
- Position: corner of frame, on the same plane as the object
- Keep sphere in every single shot — removing it between shots loses calibration

---

## Common Mistakes

| Mistake | Effect | Fix |
|---------|--------|-----|
| Camera moved between shots | Blur, double edges | Use a tripod with locking head |
| Inconsistent exposure | Noisy normals | Lock Manual mode, check histogram |
| Object moved | Misregistered normal map | Use suction pad or heavy weight |
| Shadows from stand/hands | Dark patches in normal map | Stand well back, use long cable release |
| Too few light positions | Noisy or flat-looking normals | Minimum 8, prefer 16+ |
| Dome too close to object | Near-field error (dark edges) | Tick Near-Field Correction in HELIO |
| Specular hot spots | Blown-out patches | Use IRLS or Robust LS solver |

---

## Importing into HELIO Pro

### From RTIBuilder / Relight
1. Left panel → **📂 Import RTI Project Folder**
2. Select the folder containing your `.lp` file and images
3. HELIO matches images to light vectors automatically
4. Click **LOAD SCANS & PROCESS**

### From scratch (new capture)
1. Left panel → **Load Images** → select all photos
2. Step 1B (sphere in frame) **or** Step 1C (manual/rig)
3. Click **LOAD SCANS & PROCESS**

---

*Part of the HELIO Pro documentation suite — https://github.com/sjm208/Helio-Pro*
