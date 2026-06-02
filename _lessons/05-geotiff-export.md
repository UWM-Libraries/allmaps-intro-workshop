---
layout: lesson
title: "Lesson 5: Exporting a GeoTIFF with Allmaps CLI"
position: 5
permalink: /lessons/geotiff-export/
---

# Lesson 5: Exporting a GeoTIFF with Allmaps CLI

In this lesson we will download a IIIF image to our local machine,
download the IIIF georeference annotation from Allmaps,
and use command line tools to generate a Cloud-Optimized GeoTIFF
to use in GIS.

This lesson focuses on one Allmaps CLI workflow: GeoTIFF export.
We will use the CLI for other advanced workflows in the next lessons.

Before starting, make sure you have completed [Lesson 4: Command Line Setup]({{ '/lessons/command-line-setup/' | relative_url }}) or already have the required tools installed.

<a class="btn" href="{{ '/lessons/command-line-setup/' | relative_url }}">Command line setup</a>
<a class="btn" href="{{ '/lessons/geojson-overlay' | relative_url }}">Next CLI workflow: GeoJSON overlay</a>
<a class="btn" href="{{ '/lessons/fun' | relative_url }}">🕹️ Have fun instead</a>

## Generating a GeoTIFF using Allmaps CLI

In this section, you will generate a georeferenced Cloud Optimized GeoTIFF (COG) from an Allmaps annotation.

This format is commonly used for web maps and allows efficient access to large raster datasets.

For an introduction to COGs and how they enable efficient, web-based access to raster data, see [https://cogeo.org/](https://cogeo.org/).

For the main walkthrough, this example exports a GeoTIFF from the 1821 AGSL map of Paris used in the next two lessons.
It is helpful to keep a record of the URLs for the resources you are working with, particularly if you are using an example other than the one provided.

### Paris Example

| Resource | Location / URL |
| --- | --- |
| AGSL Map of Paris, 1821 | [https://collections.lib.uwm.edu/digital/collection/agdm/id/1550/](https://collections.lib.uwm.edu/digital/collection/agdm/id/1550/) |
| IIIF Manifest URL | [https://collections.lib.uwm.edu/iiif/info/agdm/1550/manifest.json](https://collections.lib.uwm.edu/iiif/info/agdm/1550/manifest.json) |
| Georeference annotation | [https://annotations.allmaps.org/images/adeae8a56aaf59fb](https://annotations.allmaps.org/images/adeae8a56aaf59fb) |
| Allmaps Image ID | `adeae8a56aaf59fb` |
| Image ID URL | [https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550](https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550) |
| Image Dimensions | `10784 x 6941` |
| Expected Image Filename | `adeae8a56aaf59fb.jpg` |

The public item page and manifest use `collections.lib.uwm.edu`.
The IIIF Image API URL used by Allmaps is the canonical `cdm17272.contentdm.oclc.org` URL.
Use that image service URL in the command-line steps below so the generated filenames match the Allmaps annotation.

### 1. Create a Working Directory

Create a new directory for your image to keep it isolated from other images as you practice generating GeoTIFFs from Allmaps.

```bash
mkdir -p ~/allmaps/agsl-paris
cd ~/allmaps/agsl-paris
```

### 2. Download the Georeference Annotation

```bash
curl -L "https://annotations.allmaps.org/images/adeae8a56aaf59fb" -o annotation.json
```

If you are using a different map, use the annotation for that map instead.
You can confirm that the annotation is readable with:

```bash
allmaps annotation parse annotation.json
```

### 3. Download the IIIF Image

GeoTIFF export is fussier than the GeoJSON workflow because the generated script expects local image filenames and source-image dimensions to match the Allmaps annotation.

```bash
allmaps fetch full-image "https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550"
ls -lh *.jpg
```

For this example, the downloaded file should be named `adeae8a56aaf59fb.jpg`.
If your file has a different name, rename it before continuing:

```bash
mv current-filename.jpg adeae8a56aaf59fb.jpg
```

> **Warning:**
>
> Unless you are working with the same map, your filename will be different.
> What matters is that the local image filename matches what the generated script expects.
>
{: .callout .warning }

By default, `allmaps fetch full-image` may not download the highest-resolution version.

To see which sizes the IIIF server can provide, inspect the image service metadata:

```bash
curl -s https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550/info.json | jq '.sizes'
```

For this example, the largest size listed should be `10784 x 6941`, matching the dimensions in the Allmaps annotation.
If your local JPEG is smaller than the largest size, it will not match the pixel coordinates in the Allmaps annotation.
In that case, use `dezoomify-rs` to download the full-resolution image:

```bash
dezoomify-rs "https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550" full.jpg
mv full.jpg adeae8a56aaf59fb.jpg
```

### 4. Generate the GeoTIFF Script

```bash
cat annotation.json | allmaps script geotiff > paris_geotiff.sh
```

This will generate a shell script file `paris_geotiff.sh` that you will run soon.

The generated script expects a specific filename.
If yours differs, it will fail.

### 5. Edit the Script

Open the script in VS Code or your text editor of choice:

```bash
# Visual Studio Code:
code paris_geotiff.sh

# nano
nano paris_geotiff.sh

#etc.
```

Look for this `gdalwarp` block:

```bash
gdalwarp \
  -of COG -co COMPRESS=JPEG -co QUALITY=75 \
  -dstalpha -overwrite \
  -r cubic \
  -cutline ./adeae8a56aaf59fb_2543dadd9c2fa8b1.geojson -crop_to_cutline -cutline_srs "EPSG:4326" \
  -s_srs 'EPSG:3857' \
  -t_srs 'EPSG:3857' \
  -ts 9819 6706 \
  -order 1 \
  ./adeae8a56aaf59fb_2543dadd9c2fa8b1.vrt \
  ./adeae8a56aaf59fb_2543dadd9c2fa8b1-warped.tif
```

This command uses [`gdalwarp`](https://gdal.org/en/stable/programs/gdalwarp.html) to apply the georeferencing from the annotation and generate a georeferenced raster.

Before running the script, make the following adjustment:

**Remove** the `-cutline_srs` flag.
This option is not supported in all GDAL versions and may cause the script to fail.

Before:

```bash
-cutline ./adeae8a56aaf59fb_2543dadd9c2fa8b1.geojson -crop_to_cutline -cutline_srs "EPSG:4326" \
```

After:

```bash
-cutline ./adeae8a56aaf59fb_2543dadd9c2fa8b1.geojson -crop_to_cutline \
```

If you have sufficient available memory (RAM), you can speed up processing by adding `-multi -wm 2048`.
On low-memory systems, this may cause the command to fail.

**Add** `-multi -wm 2048` to the `gdalwarp` command.

Each line in a multi-line command must end with `\`, except the final line.
If a line is missing `\`, the command will terminate early and cause errors such as `command not found` or `No target filename specified`.

Your updated `gdalwarp` command block should read like this:

```bash
gdalwarp \
  -of COG -co COMPRESS=JPEG -co QUALITY=75 \
  -dstalpha -overwrite \
  -r cubic \
  -cutline ./adeae8a56aaf59fb_2543dadd9c2fa8b1.geojson -crop_to_cutline \
  -multi -wm 2048 \
  -s_srs 'EPSG:3857' \
  -t_srs 'EPSG:3857' \
  -ts 9819 6706 \
  -order 1 \
  ./adeae8a56aaf59fb_2543dadd9c2fa8b1.vrt \
  ./adeae8a56aaf59fb_2543dadd9c2fa8b1-warped.tif
```

Save the script file:

**VS Code**: File > Save or <kbd>Ctrl+S</kbd> to save.

**nano**: <kbd>Ctrl+O</kbd> to save, <kbd>Enter</kbd> to confirm the filename, <kbd>Ctrl+X</kbd> to exit nano.

> **Note:**
>
> There is [an issue](https://github.com/allmaps/allmaps/issues/261) related to the `-cutline_srs` flag on the Allmaps repository.
>
{: .callout .note }

### 6. Run the Script

```bash
bash paris_geotiff.sh
```

If the script runs successfully, the output file is now georeferenced using the control points from the Allmaps annotation.

> **Warning:**
>
> Troubleshooting script failures and errors:
>
> - See the "Download the IIIF Image" step if your image size is wrong.
> - Ensure you have made the appropriate adjustments in the generated shell script in the "Edit the Script" step above. Regenerate the script to start over if you need to.
> - Triple check your filenames and ensure they match what the shell script expects.
>
{: .callout .warning }

### 7. Verify the Output with GDAL

```bash
gdalinfo *-warped.tif
```

**Check for the following in the output:**

- `EPSG:3857` - confirms the map is in Web Mercator
- `Size is ...` - shows the pixel dimensions of the output image
- `LAYOUT=COG` - confirms the file is a Cloud Optimized GeoTIFF

You do not need to understand the full output; just confirm these values appear.

You have now generated a georeferenced GeoTIFF from an Allmaps annotation.
This file can be used in GIS software or served as a web-accessible raster.
