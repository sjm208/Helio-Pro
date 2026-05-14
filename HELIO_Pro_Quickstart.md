# HELIO Pro — Quickstart Manual

> **Version 1.0** · Experimental Research Software  
> Photometric Stereo & RTI Surface Imaging  
> https://github.com/sjm208/Helio-Pro

> ⚠️ **Experimental software.** Core processing (normal maps, depth, relighting, export) works reliably. Some advanced or platform-specific features may be incomplete. If something does not work on your system, please open an issue on GitHub.

---

## About This Software

HELIO Pro was built to experiment with photometric stereo algorithms against a **custom DIY 8-light spider/spoke microcontrolled photo-matrix stereo illumination rig** — a hand-built system designed for accessible, high-quality surface imaging without commercial dome hardware. The software grew from that experiment into a full imaging toolkit.

It has been tested on macOS with a Phase One IQ4 100MP camera. Cross-platform behaviour on all systems has not yet been fully verified.

**What works well:** normal map solving, all render engines, depth integration, relighting viewers, 3D export, publication sheets, metrology.  
**Still maturing:** AI analysis tools, neural PS training, some terrain RVT features.

---

## Before You Begin

This manual teaches you to capture multi-light photographs and turn them into interactive 3D surface data using HELIO Pro. No programming knowledge is required. The software runs on macOS and Windows.

**What you will produce:**
- A high-resolution normal map (surface direction per pixel)
- A depth/relief map (3D height data)
- Interactive relighting viewers for web browsers
- Publication-ready multi-panel figures
- Measured surface roughness (ISO 25178)

---

# PART ONE — BEGINNER

## 1. What Is Photometric Stereo?

Photometric stereo is a technique that uses photographs taken from a **fixed camera** with lights moved to different positions. By comparing how the same surface responds to light from each direction, the software calculates the slope of the surface at every pixel — building a complete normal map and depth model.

```
       CAMERA (fixed, overhead)
            │
            │
     ╔══════▼══════╗
     ║   SUBJECT    ║     ← flat on a table or copy stand
     ╚═════════════╝
    ↗              ↖
  Light 1        Light 2     ← moved between shots
    ↑                ↑
  Same exposure, same ISO, same aperture — only the light moves
```

**You need a minimum of 4 photographs** (4 different light positions). 8–16 gives publication quality. 32–64 gives archival quality.

---

## 2. How to Capture PS Images

### Method A — RTI Dome (Most Accurate)

An RTI dome is a hemisphere of numbered LEDs that fire one at a time. A chrome sphere inside the dome reflects each light as a bright spot, letting HELIO automatically extract the light direction from every image.

```
          ┌─────────────────┐
         /   RTI Dome        \
        /  ●  ●  ●  ●  ●     \
       /  ●           ●       \
      │  ●    SUBJECT   ●      │
       \  ●  (chrome    ●     /
        \  ●  sphere)  ●     /
         \   ●  ●  ●  ●    /
          └───────────────┘
               CAMERA
              (through hole
               at top)
```

**Workflow:**
1. Place your subject flat inside the dome
2. Put a chrome ball (≥25mm diameter) in the corner of the frame
3. Trigger each LED in sequence — one photo per LED
4. Load all images into HELIO Pro → Step 1B (Sphere Sync)

---

### Method B — Manual Flash / Handheld Torch

No dome? You can get good results with a handheld flash or torch moving around your subject.

```
          [Camera on tripod — overhead, pointing straight down]

    Position 1          Position 2          Position 3
    Flash → ↘           Flash → ↓          Flash ↙ ←
              \               |              /
               ▼              ▼            ▼
          ┌──────────────────────────────┐
          │         SUBJECT              │
          └──────────────────────────────┘
   
   Positions: N, NE, E, SE, S, SW, W, NW  (8 positions minimum)
   Elevation: 30°–60° above horizontal
   Distance: consistent (mark positions on the table with tape)
```

**Tips:**
- Keep flash power identical for every shot
- Lock camera exposure manually (M mode)
- Use a cable release or self-timer to avoid camera shake
- Do not change the camera position between shots
- If using a phone, lock focus and exposure before capturing

**Light calibration:** Use HELIO's **Virtual Dome Calibrator** (Step 1C) to enter the approximate positions. You can also use the AI Light Estimation option for legacy captures.

---

### Method C — Fixed Spider Rig

A spider rig has multiple fixed lights (LEDs or strobes) around a central copy stand. Each light fires individually.

```
         Light 2                 Light 3
            ●    Camera (top)    ●
             \        │         /
              \       ↓        /
    Light 1 ●─────────────────── ● Light 4
              /                \
             /                  \
            ●                    ●
         Light 8                 Light 5

             ┌──────────────┐
             │   SUBJECT    │   ← flat copy stand surface
             └──────────────┘
```

Spider rigs give the most consistent results because nothing moves between shots. Use a .lp file from the rig controller (Step 1C → Import .lp) or calibrate once with a sphere.

---

## 3. Installing HELIO Pro

**Requirements:** Python 3.10 or later · macOS 12+ or Windows 10+

```bash
# 1. Install Python dependencies
pip install -r requirements.txt

# 2. Run HELIO Pro
python Helio_Pro_V1.py
```

**Optional (for Neural PS solver):**
```bash
pip install torch torchvision   # ~2 GB download
```

---

## 4. Your First Processing Run — Step by Step

### Step 1 — Load Images

1. Click **Load Images** in the left panel
2. Select all your multi-light photographs (JPEG, PNG, or TIFF)
3. A thumbnail strip appears — check all images loaded correctly

### Step 2 — Calibrate Lights

**If you used a dome with a chrome sphere:**
- Click **1B. Sphere Sync**
- Draw a rectangle around the chrome sphere
- Click **Detect Sphere** — the circle snaps to it automatically
- Click **Accept ROI** — HELIO extracts all light vectors automatically

**If you used a manual torch or handheld flash:**
- Click **1C. Virtual Dome Calibrator**
- Enter the approximate positions of your lights
- Or click **AI Light Estimation** as a last resort

**If you have a .lp file from RTIBuilder or a dome controller:**
- Click **Import .lp File** and select your file

### Step 3 — Process

Click **LOAD SCANS & PROCESS** (the large green button).

Processing takes 10 seconds to 5 minutes depending on image resolution.

When complete, the main viewport shows your normal map under interactive lighting.

### Step 4 — Explore Your Results

**Drag the dome control** (right panel) to relight the surface from any angle.

**Change the render engine** using the dropdown at the top of the right panel:

| Engine | Best For |
|--------|----------|
| Standard PBR | General relighting, publication renders |
| Positive Openness | Raised features, text, inscriptions |
| Sky-View Factor | Even ambient light, no directional shadows |
| Surface Curvature | Fine scratches, drypoint marks |
| Multi-Dir Hillshade | Even 8-direction illumination |
| PCA 1 / 2 / 3 | Material separation, ink analysis |

### Step 5 — Export

**For a quick image:**
- Click **Current Visual (TIFF)** in the 2D Renders tab

**For a publication figure:**
- Tick the panels you want under "Generate Publication Sheet — Options"
- Click **Generate Publication Sheet**
- Choose a preset (Manuscript, Inscription, Coin/Seal)

**For an interactive browser viewer:**
- Click **WebRTI (PTM)** → choose a folder → run `1_Mac.command`
- Or click **🌐 Combined RTI Viewer** for a single portable HTML file (no server needed)

---

## 5. Keyboard Shortcuts

| Key | Action |
|-----|--------|
| Scroll wheel | Zoom in/out |
| Drag | Pan image |
| Shift + drag | Draw depth profile line |
| Alt + drag | Relight from cursor position |
| ↺ ↻ toolbar | Rotate canvas 90° |
| Double-click | Reset zoom / unlock magnifier |

---

# PART TWO — INTERMEDIATE

## 6. Choosing the Right Solver

Open the **Solver** dropdown in the left panel before processing:

```
┌─────────────────────────────────────────────────────────────┐
│  SOLVER SELECTION GUIDE                                       │
│                                                               │
│  Matte surfaces (parchment, paper, stone)                     │
│    → Linear Least Squares  (fast, reliable default)           │
│                                                               │
│  Shiny surfaces (metal, glazed ceramic, varnish)              │
│    → IRLS (Metallic/Specular)  or  Iterative Specular Sep.    │
│                                                               │
│  Coins, stamps, seals, medals                                 │
│    → Robust LS  (handles bright specular hot spots)           │
│                                                               │
│  Hard raking shadows, stone inscriptions                      │
│    → Shadow-Rejection LS                                      │
│                                                               │
│  Best overall quality (requires pip install torch)            │
│    → PyTorch Deep PS                                          │
│                                                               │
│  No light calibration available                               │
│    → Uncalibrated PCA  (approximate)                         │
└─────────────────────────────────────────────────────────────┘
```

---

## 7. Physical Scale Calibration

To get measurements in real units (mm, µm):

1. **Draw Scale Bar** (Metrology tab, Step 1) — drag a line across a ruler or known reference in the image
2. **Calculate PPI** (Metrology tab, Step 2) — enter the real length in mm
3. **Draw Z-Ref** (Step 3) — drag from the base surface to a feature of known height (e.g. a feeler gauge)
4. **Set Z Scale** (Step 4) — enter the height in mm

After calibration, all depth profiles show µm on the Y axis and ISO 25178 roughness values become physically meaningful.

---

## 8. Depth Profile Analysis

After processing, click **Profile (Z)** in the right panel.

Drag a line across any feature to measure:
- **Ra** — mean roughness (average deviation from mean)
- **Rq** — RMS roughness (statistical standard deviation)
- **Rz** — peak-to-valley total range
- **Rp** — maximum peak height
- **Rv** — maximum valley depth

The profile line appears on the reference image. Profiles export as CSV for measurement records.

---

## 9. The A/B Wipe Comparison

Enable the A/B wipe slider to compare two render engines side by side:

```
Before (Engine A)  │  After (Engine B)
                   │
  Normal PBR       │   Positive Openness
  ─ diffuse light  │   ─ raised features white
                   │
    ←─── drag to move ───→
```

- Tick **Colour B** to compare any engine against the original albedo photograph

---

## 10. Terrain Relief (RVT Panel)

The **Terrain Relief** button opens a specialist panel for archaeological-grade surface enhancement:

```
  Z-Factor:  0.05 → gentle (parchment, flat surfaces)
             0.15 → standard (manuscripts, slight relief)
             0.30 → strong (incised stone, deep carving)
             0.80 → dramatic (architectural stone, masonry)
```

**Quick Presets:**
| Preset | Best For |
|--------|----------|
| Sky Diffuse Style | Watermarks, faint parchment texture |
| Sky+HS | Publication-quality manuscript renders |
| Inscription | Cut stone, incised text |
| Drypoint | Copper plate printmaking marks |
| Manuscript | Ink, parchment, paper |

The **RVT Composite** button runs 14 algorithms simultaneously and outputs the HRLC (High Relief Low Contrast) composite as the primary deliverable.

---

# PART THREE — ADVANCED

## 11. Near-Field Light Correction

If your dome radius is smaller than 400mm, lights are close enough that their distance from the surface affects the calculation. Tick **Near-Field Correction** before processing and enter your dome radius in mm.

```
  Small dome (< 400mm):             Large dome (> 400mm):
  
  Light direction varies            Light direction is essentially
  significantly across the          parallel across the whole
  object surface                    object surface
       ↗                              ↑  ↑  ↑  ↑
      /                               │  │  │  │
  ───────────                    ─────────────────
    SUBJECT                           SUBJECT
  
  Use Near-Field Correction         Standard PS works well
```

---

## 12. Specular / Diffuse Separation

Found in the **3D & Web** tab. This mathematically decomposes each pixel into:

- **Diffuse albedo** — the matte surface colour with all highlights removed
- **Specular component** — bright map of gloss, glare, and varnish
- **Gloss index** — fraction of light that is specular (0 = matte, 1 = mirror)
- **Highlight mask** — pixels where gloss exceeds 2 standard deviations

**Use cases:**
- Drypoint prints — the specular map shows surviving burr (conservation indicator)
- Glazed ceramics — maps fired vs unfired zones by gloss difference
- Varnished paintings — reveals uneven ageing, blooming, and retouching areas
- Metal coins — separates corrosion (matte) from clean metal (specular)

---

## 13. Neural PS Training

For institutions with a fixed rig and recurring material type (copper plates, parchment, coins), you can train a neural network on your own images:

1. Process 3–5 captures of the same material type with the default solver
2. Open **AI Tools** tab → **Self-Supervise Model**
3. Set epochs to 200 (500 for highest quality)
4. Click **Start Training** — takes 15–60 minutes
5. The model is saved as `{object}_{date}.pt` in your output folder
6. Select **PyTorch Deep PS** in the solver dropdown on future captures

Accuracy improvement on specular surfaces: typically 15–22% compared to linear least squares.

---

## 14. GIS & Georeferenced Export

For archaeological and architectural PS captures that need to integrate with GIS software:

1. Draw a scale bar (Metrology → Step 1–2) to set physical scale
2. Open **3D & Web** tab → **GIS Hillshades (32-bit)** or **GIS Analysis Maps (32-bit)**
3. HELIO exports georeferenced GeoTIFF files with world files and PRJ projection files
4. Load directly into QGIS or ArcGIS

For one-click QGIS integration, use **Export QGIS Plugin** — this creates an installable Processing plugin that adds all HELIO layers to your QGIS toolbox.

---

## 15. Museum Archive Export

HELIO Pro generates museum-standard linked data alongside every capture.

### Heritage Archive ZIP
A complete archival bundle containing:
- All render engine outputs as TIFFs
- Normal map and depth maps (32-bit)
- Light vectors CSV
- ISO 25178 metrology CSV
- Processing provenance JSON (full audit trail)
- README with methodology notes

### Linked Data Exports
| Format | Purpose |
|--------|---------|
| CIDOC-CRM JSON-LD | Digital repositories, knowledge graphs |
| IIIF 3.0 Manifest | Universal Viewer, Mirador |
| LIDO XML | Europeana, national aggregators |
| Dublin Core TIFF | XMP metadata embedded in TIFFs |
| Zenodo Package | Open DOI-ready deposit |

**Always set the Object ID field** before archiving — it propagates into every filename, manifest URI, and metadata record.

---

## 16. Troubleshooting

| Problem | Likely Cause | Solution |
|---------|-------------|----------|
| Normal map looks noisy / random | Too few images (< 4) | Add more light positions |
| Normal map has "stripy" artefacts | Inconsistent exposure | Tick Normalise Exposure |
| Edges appear darker than centre | Small dome, no near-field correction | Tick Near-Field Correction |
| Depth map has a "bowl" shape | Integrator accumulating error | Tick Parabolic Depth Correct |
| Specular hot spots wash out normals | Wrong solver | Switch to IRLS or Robust LS |
| 3D viewer shows black screen | GPU memory exceeded | Increase Step slider to 3–4 |
| WebRTI shows black canvas | 100MP canvas exceeds GPU limit | Re-export — HELIO caps to 4096px automatically |
| Processing hangs after calibration | Tkinter thread deadlock | Update to latest version |

---

## 17. Recommended Capture Settings

| Camera Setting | Value |
|----------------|-------|
| Mode | Manual (M) |
| ISO | 100–200 (lowest native) |
| Aperture | f/8–f/11 (maximum sharpness zone) |
| Shutter | 1/125s or sync speed for flash |
| White balance | Manual or Kelvin fixed |
| Focus | Manual — lock before first shot |
| File format | RAW → export as 16-bit TIFF, or JPEG at 95%+ |
| Lens | Macro or technical lens; avoid distortion |

**For Phase One / medium format backs:**  
Use tethered capture and a dome controller to fire each LED in sequence. HELIO Pro is optimised for the Phase One IQ4 100MP at 8682×11574px.

---

## 18. Output File Reference

After processing, HELIO Pro creates files in your chosen output folder:

```
Output/
├── {ID}_albedo.tif              — photographic colour (no shading)
├── {ID}_normals.png             — tangent-space normal map (RGB encoded)
├── {ID}_depth_poisson.tif       — depth map, Poisson integration
├── {ID}_depth_frankot.tif       — depth map, Frankot-Chellappa
├── {ID}_roughness.png           — surface roughness map
├── {ID}_specular.png            — specular variance map
├── {ID}_publication_sheet.png  — assembled publication figure
├── web/                         — WebRTI viewer folder
│   ├── index.html
│   ├── albedo.jpg
│   ├── normals.png
│   └── 1_Mac.command
└── {ID}_combined_viewer.html    — portable single-file RTI viewer
```

---

## 19. Getting Help

- **Tooltips:** Hover any button for 0.5 seconds to read its description
- **Getting Started wizard:** Re-open from the 📖 Getting Started button (left panel)
- **GitHub repository:** github.com/sjm208/Helio-Pro
- **Issues:** Use the GitHub Issues tab for bug reports
- **HELIO Pro Issues:** https://github.com/sjm208/Helio-Pro/issues

---

*HELIO Pro is developed at HELIO Pro. Manual version 1.0.*


---

## Key Citations

When using HELIO Pro outputs in research, please cite the underlying algorithms:

**Photometric stereo fundamentals:**  
Woodham, R.J. (1980). Photometric method for determining surface orientation from multiple images. *Optical Engineering*, 19(1), 139–144.

**Polynomial Texture Maps (PTM / WebRTI):**  
Malzbender, T., Gelb, D., & Wolters, H. (2001). Polynomial texture maps. *SIGGRAPH 2001*, 519–528.

**Depth integration (Frankot-Chellappa):**  
Frankot, R.T., & Chellappa, R. (1988). A method for enforcing integrability in shape from shading. *IEEE TPAMI*, 10(4), 439–451.

**Terrain analysis (RVT — Sky-View Factor, MSRM, SLRM):**  
Zakšek, K., Oštir, K., & Kokalj, Ž. (2011). Sky-View Factor as a Relief Visualisation Technique. *Remote Sensing*, 3(2), 398–415.

**IIIF Presentation API:**  
IIIF Consortium (2023). *IIIF Presentation API 3.0*. https://iiif.io/api/presentation/3.0/

Full citation list: see README.md on GitHub.
