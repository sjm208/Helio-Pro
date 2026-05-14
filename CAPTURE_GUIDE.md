# HELIO Pro — Capture Guide
*Optimal photographic workflows for photometric stereo and RTI.*

---

## 1. The Core Principle
Photometric stereo relies on a single, strict rule: **The scene must remain entirely static while the light source changes direction.** 

Every variable in the optical chain remains fixed. Only the angle of illumination changes per exposure.

> **The Capture Matrix**
> *   **FIXED:** Camera position · Focus · Aperture · ISO · Subject
> *   **VARIES:** Light direction (One image captured per light position)

*   **4 Light Positions:** Minimum requirement (basic normal map generation).
*   **8–16 Positions:** Recommended for publication-quality surface reconstruction.
*   **32–64 Positions:** Archival standard (full RTI / museum-grade archive).

---

## 2. Capture Methods

### Method A: The RTI Dome
The most precise and automated method. A hemisphere array of LEDs fires sequentially, perfectly mapped to the subject. The camera is positioned directly overhead, looking down through the top of the dome at the subject and calibration sphere.

**Setup Checklist:**
*   [ ] Subject secured flat on the baseboard.
*   [ ] Chrome calibration sphere placed on the same plane, visible in every frame.
*   [ ] Camera tethered for automated firing synced with the LED array.
*   [ ] Exposure locked (Manual Mode).

**HELIO Calibration:** `Step 1B → Sphere Sync → Draw circle on sphere → Accept`

### Method B: Handheld Flash or Torch
A flexible, dome-free approach. The light source is manually moved to 8–16 distinct positions around the object (North, South, East, West, and the diagonals), maintaining an elevation of 30°–60° above the table.

**Pro-Tips:**
*   Mark your 8–16 positions on the table with tape to ensure consistent spacing.
*   Cover windows and eliminate ambient room light; stray light introduces severe vector errors.
*   Maintain the exact same flash power or torch distance for every shot.

**HELIO Calibration:** 
*   If you shot with a chrome sphere: `Step 1B → Sphere Sync`
*   If you shot without a sphere: `Step 1C → Virtual Dome Calibrator → Enter positions` *(Alternatively: Use AI Light Estimation as a fallback).*

### Method C: Fixed Spider Rig
A hybrid approach using multiple fixed lights mounted around a copy stand. This is highly effective whether using a commercial solution or a custom 8-LED DIY system.

**Advantages:**
*   Absolute geometric consistency; nothing physically moves during the capture sequence.
*   Ideal for batch processing and automated controller sequences.
*   Allows the use of predefined `.lp` (light position) files.

**HELIO Calibration:** 
*   With controller file: `Step 1C → Import .lp File`
*   First-time rig calibration: `Step 1B → Sphere Sync`

---

## 3. Exposure & Camera Specifications

Consistency is more important than absolute brightness. Ensure your camera is completely locked down.

| Setting | Recommendation |
| :--- | :--- |
| **Mode** | Manual (M) |
| **ISO** | Base native ISO (e.g., 100 or 200) for minimum noise. |
| **Aperture** | f/8 – f/11 (Maximum sharpness and sufficient depth of field). |
| **Shutter** | 1/125s (Or your specific flash sync speed). |
| **White Balance**| Fixed Kelvin (e.g., 5500K) or a Custom Preset. Never Auto. |
| **Focus** | Manual — lock focus precisely before the first exposure. |
| **Stabilisation**| OFF (OIS/IBIS can cause micro-shifts on a tripod). |
| **File Format** | RAW → Export as 16-bit TIFF (especially critical when resolving fine, drypoint details with high-resolution sensors like a Phase One 100 Megapixel back). |

---

## 4. Geometric Alignment

To prevent depth map foreshortening, the camera sensor must be perfectly parallel to the subject surface. 

*   **Ideal:** Camera directly overhead, 0° tilt.
*   **Acceptable:** Up to 10° tilt if the subject fills the frame.
*   **Avoid:** Steep angles. 

---

## 5. Subject Preparation

**Flat Objects (Historical Manuscripts, Prints, Copper Plates):**
*   Use a suction mount, vacuum table, or specialized book cradle to keep the surface entirely flat.
*   *Note:* Even a 1mm bow across a 300mm document will introduce measurable topological errors in the final depth map.

**Coins and Medals:**
*   Mount obverse and reverse separately.
*   Use dark Plasticine or a bespoke 3D-printed ring mount to hold the coin at exactly a 0° tilt.

**3D Objects (Ceramics, Carvings):**
*   Photometric stereo excels on low-relief surfaces (maximum useful relief is ~10–20% of the object's diameter). 
*   For highly dimensional or deep 3D objects, cross-polarised photogrammetry is recommended instead.

**The Chrome Sphere (If applicable):**
*   **Placement:** Must sit on the *exact same plane* as the object surface, typically in the corner of the frame. 
*   **Rule:** Never remove or bump the sphere mid-sequence. 

---

## 6. Troubleshooting Common Capture Errors

| Visual Artifact in HELIO | Likely Cause | The Fix |
| :--- | :--- | :--- |
| **Blur / Double Edges** | Camera moved between shots. | Use a heavier tripod, tighten the head, use a cable release. |
| **Noisy / Grainy Normals**| Inconsistent exposure or Auto-ISO. | Lock camera to full Manual. Check histograms. |
| **Misregistered Maps** | Object shifted during capture. | Secure object with mounts or weights. |
| **Dark Patches** | Shadows from stands or your hands. | Step further back during exposure. |
| **Flat-looking Normals** | Insufficient light angles. | Increase capture count (Minimum 8, ideally 16+). |
| **Dark Edges (Vignette)** | Light source was too close to subject. | Tick **Near-Field Correction** in HELIO. |
| **Blown-out Patches** | Specular hot spots from bare LEDs. | Use **IRLS** or **Robust LS** solver in HELIO. |

---

## 7. Importing into HELIO Pro

*Tip: If you are processing a massive backlog of map or manuscript classmarks, utilizing custom AppleScripts to automate and organize your folder structures beforehand will save significant time during the import phase.*

### Method A: From RTIBuilder / Relight Folders
1. Navigate to the left panel → **📂 Import RTI Project Folder**
2. Select the parent directory containing your `.lp` file and the corresponding image sequence.
3. HELIO will automatically parse and match the images to the light vectors.
4. Click **LOAD SCANS & PROCESS**.

### Method B: From Scratch (New Custom Capture)
If you are not importing a pre-existing RTI folder, you need to manually load your images and define your light sources.

1. Navigate to the left panel → **Load Images** and select your entire photo sequence.
2. **Define the Light Vectors:** Choose your calibration path:
   * **Step 1B (Sphere Sync):** Use this if you included a chrome calibration sphere. Draw a UI circle around the sphere, and HELIO will calculate the light angles automatically.
   * **Step 1C (Virtual Dome / Manual Array):** Use this if you did *not* use a sphere (e.g., handheld torch). You will manually input the angles for each light position into the interface.
3. Click **LOAD SCANS & PROCESS**.

---
*Part of the HELIO Pro documentation suite — [https://github.com/sjm208/Helio-Pro](https://github.com/sjm208/Helio-Pro)*
