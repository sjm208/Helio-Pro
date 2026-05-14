# Installing HELIO Pro

> **Never used Python before?** Start at Step 1. This guide walks through everything.

---

## What You Need

- A Mac or Windows PC
- An internet connection for the initial install
- About 1 GB of free disk space (2 GB if adding the 3D viewer)

---

## PART 1 — Install Python

### macOS

**Step 1 — Check if Python is already installed**

Open **Terminal** (press `Cmd + Space`, type `terminal`, press Enter) and type:

```
python3 --version
```

If you see `Python 3.10.x` or higher, skip to Part 2.  
If you see `command not found` or a version lower than 3.10, continue below.

---

**Step 2 — Install Python on macOS**

Go to **https://www.python.org/downloads/mac-osx/**

Download the latest **macOS installer** (the big yellow "Download Python 3.x.x" button).

> ✅ Tested versions: **Python 3.10**, **3.11**, **3.12**  
> ❌ Do not use Python 3.13 yet — some libraries are not compatible

Run the `.pkg` installer. Click through all the defaults.

When it finishes, open a **new** Terminal window and type:

```
python3 --version
```

You should now see `Python 3.11.x` or similar.

---

### Windows

**Step 1 — Download Python**

Go to **https://www.python.org/downloads/windows/**

Click the big **"Download Python 3.x.x"** button.

> ✅ Tested versions: **Python 3.10**, **3.11**, **3.12**  
> ❌ Do not use Python 3.13 yet

**Step 2 — Run the installer**

⚠️ **Very important:** On the first installer screen, tick the box that says  
**"Add Python to PATH"** before clicking Install Now.

```
☑  Add Python 3.x to PATH      ← TICK THIS BOX
   Install Now
```

If you miss this, uninstall Python and reinstall — everything breaks without it.

**Step 3 — Verify**

Open **Command Prompt** (press `Win + R`, type `cmd`, press Enter) and type:

```
python --version
```

You should see `Python 3.11.x` or similar.

---

## PART 2 — Download HELIO Pro

Go to **https://github.com/sjm208/Helio-Pro**

Click the green **"< > Code"** button → **"Download ZIP"**

Unzip the downloaded file somewhere permanent — **not** in your Downloads folder.  
Good locations:
- macOS: `Documents/Helio-Pro/`
- Windows: `C:\Users\YourName\Helio-Pro\`

---

## PART 3 — Install Libraries (Easiest Method)

### macOS

Open **Terminal** and type these commands one at a time, pressing Enter after each:

```bash
cd ~/Documents/Helio-Pro
pip3 install -r requirements.txt
```

Wait for everything to download and install. This takes 3–10 minutes depending on your internet connection. You will see lots of text scrolling — that is normal.

When it finishes, run HELIO Pro:

```bash
python3 Helio_Pro_V1.py
```

---

### Windows

Open **Command Prompt** and type:

```
cd C:\Users\YourName\Helio-Pro
pip install -r requirements.txt
```

Replace `YourName` with your actual Windows username.

When finished:

```
python Helio_Pro_V1.py
```

---

## PART 4 — If Something Goes Wrong

### "pip is not recognised" / "pip3: command not found"

**macOS:**
```bash
python3 -m pip install --upgrade pip
python3 -m pip install -r requirements.txt
```

**Windows:**
```
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

---

### "No module named X" error when starting the app

Install the missing module individually:

```bash
pip3 install customtkinter        # macOS
pip install customtkinter         # Windows
```

Common ones that may need manual install:

```bash
pip3 install customtkinter Pillow numpy opencv-python scipy matplotlib vispy trimesh tifffile scikit-image scikit-learn PyOpenGL
```

---

### opencv-python fails to install on macOS (Apple Silicon M1/M2/M3)

```bash
pip3 install opencv-python-headless
```

---

### "Microsoft Visual C++ is required" on Windows

Download and install the **Visual C++ Redistributable**:  
https://aka.ms/vs/17/release/vc_redist.x64.exe

Then re-run `pip install -r requirements.txt`.

---

### Permission errors on macOS ("Operation not permitted")

```bash
pip3 install --user -r requirements.txt
```

---

### The 3D viewer opens but shows a black window

Install PyOpenGL and restart:

```bash
pip3 install PyOpenGL PyOpenGL_accelerate    # macOS
pip install PyOpenGL PyOpenGL_accelerate     # Windows
```

---

## PART 5 — Recommended: Use a Virtual Environment

This keeps HELIO Pro's libraries separate from other Python programs on your machine. Optional but good practice.

**macOS:**
```bash
cd ~/Documents/Helio-Pro
python3 -m venv helio_env
source helio_env/bin/activate
pip install -r requirements.txt
python3 Helio_Pro_V1.py
```

Each time you open a new Terminal to run HELIO, activate the environment first:
```bash
source ~/Documents/Helio-Pro/helio_env/bin/activate
```

**Windows:**
```
cd C:\Users\YourName\Helio-Pro
python -m venv helio_env
helio_env\Scripts\activate
pip install -r requirements.txt
python Helio_Pro_V1.py
```

Each time you open a new Command Prompt:
```
C:\Users\YourName\Helio-Pro\helio_env\Scripts\activate
```

---

## PART 6 — Additional Libraries

The following libraries are required and are included in `requirements.txt`. They install automatically with `pip install -r requirements.txt`. This section covers manual install steps and troubleshooting for each.

### rasterio — GIS Export

Enables georeferenced GeoTIFF export for QGIS and ArcGIS.

**macOS:**
```bash
pip3 install rasterio
```

**Windows** — rasterio can be tricky on Windows. Try in this order:

```
pip install rasterio
```

If that fails:
```
pip install rasterio --find-links https://github.com/cgohlke/geospatial-wheels/releases
```

If that also fails, install the binary wheel directly from:
https://github.com/cgohlke/geospatial-wheels/releases
Download `rasterio‑*.whl` matching your Python version and run:
```
pip install rasterio-2.0.0-cp311-cp311-win_amd64.whl
```
(Replace filename with the one you downloaded.)

---

### rvt-py — Terrain Analysis Algorithms

Enables Sky-View Factor, MSRM, SLRM, ASVF, and Local Dominance terrain engines.
Algorithm credit: Zakšek et al. 2011; Kokalj & Hesse 2017 (Apache 2.0).

```bash
pip3 install rvt-py    # macOS
pip install rvt-py     # Windows
```

---

### pye57 — Point Cloud Export

Enables E57 point cloud export for CloudCompare, Leica, and FARO software.

```bash
pip3 install pye57    # macOS
pip install pye57     # Windows
```

---

### qrcode — QR Code Generation

Enables QR codes in export packages and archive bundles.

```bash
pip3 install "qrcode[pil]"    # macOS
pip install "qrcode[pil]"     # Windows
```

---

### Optional Add-ons

### PyTorch — Neural PS Solver (~2 GB)

Enables the **PyTorch Deep PS** solver, which gives the most accurate normals on difficult surfaces (metal, glazed ceramic, varnish).

**macOS (Apple Silicon M1/M2/M3):**
```bash
pip3 install torch torchvision
```

**macOS (Intel):**
```bash
pip3 install torch torchvision
```

**Windows (CPU only):**
```
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu
```

**Windows (with NVIDIA GPU):**  
Go to https://pytorch.org/get-started/locally/ and use the selector to get the exact command for your CUDA version.

---

### Terrain Analysis — RVT

Enables the full terrain engine suite (Sky-View Factor, MSRM, SLRM, ASVF):

```bash
pip3 install rvt-py    # macOS
pip install rvt-py     # Windows
```

---

### GIS Export — Rasterio

Enables georeferenced GeoTIFF export for QGIS and ArcGIS:

```bash
pip3 install rasterio    # macOS
pip install rasterio     # Windows
```

On Windows, if rasterio fails:
```
pip install rasterio --find-links https://github.com/cgohlke/geospatial-wheels/releases
```

---

### Anthropic AI Analysis

Enables the AI Surface Analysis, AI Condition Report, and AI Caption tools.  
You need an API key from https://console.anthropic.ic.

```bash
pip3 install anthropic    # macOS
pip install anthropic     # Windows
```

Enter your API key in the **AI Tools** tab when HELIO Pro is running.

---

## PART 7 — Creating a Desktop Shortcut

### macOS — Create a launcher script

Open TextEdit, set to Plain Text (Format → Make Plain Text), and paste:

```bash
#!/bin/bash
cd /Users/YourName/Documents/Helio-Pro
python3 Helio_Pro_V1.py
```

Save as `Run HELIO Pro.command` on your Desktop.

In Terminal:
```bash
chmod +x ~/Desktop/Run\ HELIO\ Pro.command
```

Double-click the file to launch.

---

### Windows — Create a batch file

Open Notepad and paste:

```
@echo off
cd C:\Users\YourName\Helio-Pro
python Helio_Pro_V1.py
pause
```

Save as `Run HELIO Pro.bat` on your Desktop.  
Double-click to launch.

---

## Tested Configurations

| OS | Python | Status |
|----|--------|--------|
| macOS 14 Sonoma (Apple Silicon M3) | 3.11, 3.12 | ✅ Fully tested |
| macOS 13 Ventura (Apple Silicon M2) | 3.11 | ✅ Fully tested |
| macOS 12 Monterey (Intel) | 3.10, 3.11 | ✅ Fully tested |
| Windows 11 | 3.10, 3.11, 3.12 | ✅ Fully tested |
| Windows 10 | 3.10, 3.11 | ✅ Fully tested |
| Ubuntu 22.04 | 3.10, 3.11 | ⚠️ Partial (no AppKit) |

---

## Still stuck?

Open an issue at **https://github.com/sjm208/Helio-Pro/issues**

Include:
1. Your operating system and version
2. Your Python version (`python3 --version`)
3. The exact error message you see
4. The contents of `helio_pro.log` (created in the HELIO Pro folder when you run the app)
