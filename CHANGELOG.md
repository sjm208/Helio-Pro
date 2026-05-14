# Changelog

All notable changes to HELIO Pro are documented here.

---

## [1.0.0] — 2025-05-14

### Initial public release

**Core Processing**
- Linear Least Squares, IRLS, Robust LS, Shadow-Rejection LS, Iterative Specular Separation solvers
- PyTorch Deep PS neural solver (optional, requires torch)
- Uncalibrated PCA solver
- FFT Poisson and Frankot-Chellappa depth integration
- Iterative Poisson integration for highest-quality depth

**Light Calibration**
- Step 1B: Sphere Sync — RTIBuilder-style chrome sphere detection
- Step 1C: Virtual Dome Calibrator (10 arrangement tools)
- `.lp` import and export (RTIBuilder / CHI standard format)
- AI Light Estimation — infers directions from image content
- **📂 Import RTI Project Folder** — one-click RTIBuilder / Relight project import

**Render Engines (40+)**
- Standard PBR · Robust PBR · Normals USM · Specular Enhancement
- Positive/Negative Openness · Sky-View Factor · Multi-Dir Hillshade
- MSRM · Surface Curvature · SLRM · Local Dominance
- DStretch (YCbCr) · PCA 1/2/3 · False-Colour Depth
- Image Quotient · Shadow-Reject Hillshade · Anisotropic SVF
- Multi-Scale Topographic Position · and more

**3D Viewers**
- VisPy OpenGL 3D mesh viewer with C key clay/colour toggle
- Elevation heatmap viewer
- A/B wipe comparison with Colour B bypass
- 360° auto-sweep at current dome elevation

**Web Export**
- WebRTI (PTM) with dome light control, 7 render modes
- PS Normal-Map RTI viewer (base64 self-contained HTML)
- Combined RTI Viewer — single portable HTML, no server needed
- DeepZoom gigapixel viewer (OpenSeadragon, threaded export with cancel)

**3D Export**
- OBJ, GLB, PLY, STL, E57
- 16-bit PBR Suite (Albedo, Normal, Roughness, Displacement)
- Multi-LOD package
- Facsimile export (3D printing, elevated printing)
- QGIS Plugin export
- Sketchfab direct upload

**Metrology**
- ISO 25178 areal roughness (Sa, Sq, Sz, Ssk, Sku, Smr)
- Z-height calibration with feeler gauge / step block reference
- Depth profile with Ra, Rq, Rz, Rp, Rv
- Dome Coverage Score
- Normal QC vs Flat Report

**Publication**
- Publication sheet with 7 presets (Minimum, Standard, Inscription, Coin/Seal, Manuscript Full, RTI Heritage, All)
- Snapshot All Views export (all engines as PNG)
- Annotation layer (SVG export)

**Museum Archive**
- CIDOC-CRM JSON-LD (Linked Art compliant)
- IIIF 3.0 Presentation API manifest
- LIDO XML
- Dublin Core TIFF embed
- Zenodo deposit package
- MorphoSource package
- Heritage Archive ZIP
- Processing Provenance JSON audit trail

**Performance & Stability**
- All heavy exports run on background threads — UI never freezes
- `self.ph_live` / `self.pw_live` properties prevent reshape crashes after 3D viewer
- Persistent `helio_pro.log` for crash diagnosis
- WebGL canvas capped to 4096px — works on all GPUs including 100MP captures
- Memory cleanup after Low-Frequency Bias Diagnostics and terrain analysis

---

## Roadmap

- [ ] PTM binary importer (`.ptm` from RTIBuilder)
- [ ] HSH RTI binary importer (`.rti` / `.hsz` from Relight)
- [ ] Batch folder processing
- [ ] Direct MorphoSource upload
- [ ] Azure Cognitive Services integration for AI analysis
- [ ] IIIF 3D viewer integration

---

*https://github.com/sjm208/Helio-Pro*
