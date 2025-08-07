---
layout: default
title: Allmaps CLI - Generate a Cloud-Optimized GeoTIFF
---
# Getting Ready

Note: This assumes some familiarity with the command line in a Unix environment
(Linux, Mac, or a Unix-like enviornment on a Windows PC),
installing packages, and 
generating and running scripts from the command line.

# Windows Only: Set up WSL

[Windows Subsystem for Linux Documentation](https://learn.microsoft.com/en-us/windows/wsl/)

If you don't have a Linux distribution set up for WSL, install Ubuntu:

`wsl --install -d Ubuntu`

Now you can launch a Ubuntu environment from your Windows desktop environment.

# Environment Setup

```bash
sudo apt update && sudo apt upgrade -y

# Basic developer tools (optional)
sudo apt install -y build-essential curl git nano

# Node.js & npm (for Allmaps CLI)
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

# GDAL (geospatial library)
sudo apt install -y gdal-bin libgdal-dev

# Python tools (optional)
sudo apt install -y python3-pip python3-venv
```

--------------------

# Generating a GeoTIFF  using Allmaps CLI

This guide outlines the steps for generating a Cloud Optimized GeoTIFF (COG) of the Green Bay map from the AGSL collection using the Allmaps CLI and GDAL.

---

## Source Information

- **AGSL Item Page**: [https://collections.lib.uwm.edu/digital/collection/agdm/id/5922/](https://collections.lib.uwm.edu/digital/collection/agdm/id/5922/)
- **IIIF Manifest URL**: [https://collections.lib.uwm.edu/iiif/info/agdm/5922/manifest.json](https://collections.lib.uwm.edu/iiif/info/agdm/5922/manifest.json)
- **Georeference Annotation**: [https://annotations.allmaps.org/images/82b3f8acb9a05d5b](https://annotations.allmaps.org/images/82b3f8acb9a05d5b)
- **Allmaps ID**: `afbbbc974346dbbb`
- **Image ID URL**: [https://collections.lib.uwm.edu/digital/iiif/agdm/5922](https://collections.lib.uwm.edu/digital/iiif/agdm/5922)
- **Image Filename**: `d30944a32ca34085.jpg`

---

### 1. Create a Working Directory

```bash
mkdir -p ~/allmaps/agsl-green-bay
cd ~/allmaps/agsl-green-bay
```

### 2. Download the IIIF Image

```bash
allmaps fetch full-image "https://collections.lib.uwm.edu/digital/iiif/agdm/5922"
mv full-image.jpg d30944a32ca34085.jpg
```

### 3. Download the Georeference Annotation

```bash
curl -L "https://annotations.allmaps.org/images/82b3f8acb9a05d5b" -o annotation.json
```

### 4. Generate the GeoTIFF Script

```bash
cat annotation.json | allmaps script geotiff > green_bay_geotiff.sh
```

### 5. Edit the Script

Open the script in VS Code or your editor of choice:

```bash
code green_bay_geotiff.sh
```

Make these adjustments:

- **Remove** any `-cutline_srs` flag if present.
- **Add** `-multi -wm 2048` to the `gdalwarp` command.
- **Ensure** the image filename matches: `d30944a32ca34085.jpg`

### 6. Run the Script

```bash
bash green_bay_geotiff.sh
```

### 7. Verify the Output

```bash
gdalinfo d30944a32ca34085_*.tif
```

Check:

- EPSG:3857 coordinate system
- Output dimensions and pixel size
- Geo bounding box and COG layout
