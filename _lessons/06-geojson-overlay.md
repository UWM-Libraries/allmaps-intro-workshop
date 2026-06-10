---
layout: lesson
title: "Lesson 6: Overlaying GeoJSON on a IIIF Image"
position: 6
permalink: /lessons/geojson-overlay/
---

# Lesson 6: Overlaying GeoJSON on a IIIF Image

Before starting, make sure you have completed [Lesson 4: Command Line Setup]({{ '/lessons/command-line-setup/' | relative_url }}) or already have the required tools installed.

The georeference metadata produced by Allmaps Editor can be used to convert geospatial coordinates to pixel coordinates.
In this lesson, we will use that transformation to draw GeoJSON on the original unwarped map image.

The result is not new GeoJSON.
It is an SVG graphic whose coordinates match the pixel grid of the original IIIF image.

## Paris Example

For the main walkthrough, this example overlays the medieval road network from around 1300 on the 1821 AGSL map of Paris.
This uses the same Paris map as [Lesson 5: Exporting a GeoTIFF with Allmaps CLI]({{ '/lessons/geotiff-export/' | relative_url }}).

| Resource | Location / URL |
| --- | --- |
| AGSL Map of Paris, 1821 | [https://collections.lib.uwm.edu/digital/collection/agdm/id/1550/](https://collections.lib.uwm.edu/digital/collection/agdm/id/1550/) |
| IIIF Manifest URL | [https://collections.lib.uwm.edu/iiif/info/agdm/1550/manifest.json](https://collections.lib.uwm.edu/iiif/info/agdm/1550/manifest.json) |
| Viewer URL | [https://viewer.allmaps.org/?url=https%3A%2F%2Fannotations.allmaps.org%2Fimages%2Fadeae8a56aaf59fb](https://viewer.allmaps.org/?url=https%3A%2F%2Fannotations.allmaps.org%2Fimages%2Fadeae8a56aaf59fb) |
| Georeference annotation | [https://annotations.allmaps.org/images/adeae8a56aaf59fb](https://annotations.allmaps.org/images/adeae8a56aaf59fb) |
| Allmaps Image ID | `adeae8a56aaf59fb` |
| Image ID URL | [https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550](https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550) |
| Image Dimensions | `10784 x 6941` |
| Lesson-ready GeoJSON | [voiries1300_2009_clean.json]({{ '/assets/data/paris-overlay/voiries1300_2009_clean.json' | relative_url }}) |
| Prepared geometry stream | [voiries1300_2009_clean.geometries.ndjson]({{ '/assets/data/paris-overlay/voiries1300_2009_clean.geometries.ndjson' | relative_url }}) |
| Frozen annotation file | [annotation.json]({{ '/assets/data/paris-overlay/annotation.json' | relative_url }}) |
| HTML starter | [paris-road-overlay.html]({{ '/assets/data/paris-overlay/paris-road-overlay.html' | relative_url }}) |
| Lesson file package | [lesson-06-paris-overlay-files.zip]({{ '/assets/downloads/lesson-06-paris-overlay-files.zip' | relative_url }}) |

### Data Note

The road network was originally [published by ALPAGE](https://alpage.huma-num.fr/ancient-urban-fabric/) as "Road network in 1300" by Caroline Bourlet and Anne-Laure Bethe.

[Download original data](https://alpage.huma-num.fr/documents/ressources/shapes/52-voieries1300_2009.zip) (optional)

The cleaned teaching version included in this workshop is `voiries1300_2009_clean.json`, where each `MultiLineString` has already been split into separate `LineString` features.
The file `voiries1300_2009_clean.geometries.ndjson` contains one geometry per line, ready to be piped into Allmaps CLI.

## Process Overview

1. Start with a historical map georeferenced with Allmaps.
2. Use the frozen georeference annotation for that image.
3. Inspect the prepared GeoJSON.
4. Convert the GeoJSON from longitude/latitude into SVG coordinates measured in the original image space.
5. Display the transformed SVG as an overlay on the original, unwarped IIIF image.

Allmaps is not changing the GeoJSON into a new map projection for display in a web map.
It is converting the GeoJSON into image-space coordinates so the shapes can be drawn directly on the scanned map image.

## 1. Create a Working Directory

Create a new directory for the overlay work:

```bash
mkdir -p ~/allmaps/agsl-paris-overlay
cd ~/allmaps/agsl-paris-overlay
```

## 2. Download the Lesson Files

Download the frozen annotation, the cleaned GeoJSON, the prepared geometry stream, and the HTML starter as one ZIP package:

<a class="btn" href="{{ '/assets/downloads/lesson-06-paris-overlay-files.zip' | relative_url }}">Download lesson files</a>

If you download the ZIP file in your browser, unzip it and place the four files in your `~/allmaps/agsl-paris-overlay` working directory.

From the command line, download and unzip the package:

```bash
curl -L "{{ site.url }}{{ site.baseurl }}/assets/downloads/lesson-06-paris-overlay-files.zip" -o lesson-06-paris-overlay-files.zip
unzip lesson-06-paris-overlay-files.zip
```

Because Allmaps georeferencing data can be edited, this lesson uses a frozen local copy of the Paris georeference annotation.
That keeps the command-line results stable during the workshop.

## 3. Confirm the Georeference Annotation

The file `annotation.json` contains:

- the IIIF image identifier
- the image dimensions
- the ground control points
- the transformation type

Inspect it with:

```bash
allmaps annotation parse annotation.json
```

You should see output that includes the Paris image service:

```json
[
  {
    "type": "GeoreferencedMap",
    "resource": {
      "id": "https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550",
      "width": 10784,
      "height": 6941,
      "type": "ImageService2"
    }
  }
]
```

That command translates the annotation into Allmaps' internal `GeoreferencedMap` format.
This is the moment where the CLI learns how the Paris image relates to real-world coordinates.

## 4. Inspect the Prepared GeoJSON

Before transforming the GeoJSON, inspect the prepared file in two ways.

First, open [https://geojson.io](https://geojson.io) in your browser and use the open/import function to load `voiries1300_2009_clean.json`.
You should see the medieval road network drawn over the modern basemap.
This confirms that the file is valid GeoJSON with geographic longitude/latitude coordinates.

Then use `jq` to check what kinds of geometry appear in the file:

```bash
jq -r '[.features[].geometry.type] | unique[]' voiries1300_2009_clean.json
```

For this dataset, the result is:

```bash
LineString
```

This matters because the next steps assume each feature can be transformed and drawn as a line, rather than as mixed geometry types that would need extra cleanup or styling.

## 5. Transform GeoJSON into Image-Space SVG

Now run the Allmaps transformation:

```bash
allmaps transform geojson \
  -a annotation.json \
  < voiries1300_2009_clean.geometries.ndjson \
  > voiries1300_2009.svg
```

If this runs without error, expect not to see anything output to your shell.

This command is worth unpacking carefully:

- `transform geojson` takes geographic geometry and converts it into resource coordinates
- `-a annotation.json` supplies the georeference annotation
- `< voiries1300_2009_clean.geometries.ndjson` sends the prepared geometries into the command through standard input
- `> voiries1300_2009.svg` saves the transformed output as SVG
- `\` is a line continuation character. It tells the shell to treat the next line as part of the same command.

The result is an SVG graphic whose coordinates match the pixel grid of the 1821 Paris image.

## 6. Overlay the SVG on the IIIF Image

Once `voiries1300_2009.svg` exists, the hard part is done.
You now have:

- the historical image served via IIIF
- an SVG whose coordinates line up with that image

The downloaded `paris-road-overlay.html` starter creates an SVG with the IIIF image first, then adds the transformed road lines on top.

Open the file in your editor and look for the image dimensions:

```js
const width = 10784
const height = 6941
```

Then look for the IIIF image URL:

```js
const imageUrl =
  'https://cdm17272.contentdm.oclc.org/iiif/2/agdm:1550/full/full/0/default.jpg'
```

The page uses `fetch()` to load `voiries1300_2009.svg`, styles the road lines in cyan, and draws both layers together in the same pixel coordinate space.

## 7. Preview the Overlay

Because the page uses `fetch()` to load `voiries1300_2009.svg`, open it through a small local web server.

If Python 3 is installed, use its built-in server:

```bash
python3 -m http.server 8000
```

Alternatively, use Node/npm:

```bash
npx http-server . -p 8000
```

Then open [http://localhost:8000/paris-road-overlay.html](http://localhost:8000/paris-road-overlay.html) in your browser.
You should see the 1821 Paris map with the medieval road network drawn over it in bright cyan.

Allmaps gives us a transformation between geographic coordinates and map image pixels.
In this example, we use that transformation to move GeoJSON into the image's own coordinate space, then draw the resulting SVG on top of the original IIIF image.
