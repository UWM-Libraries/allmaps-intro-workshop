---
layout: lesson
title: "Lesson 6: Overlaying GeoJSON on a IIIF Image"
position: 6
permalink: /lessons/geojson-overlay/
---

# Lesson 6: Overlaying GeoJSON on a IIIF Image

This lesson will adapt the GeoJSON overlay workflow from `../ph-allmaps/part-3/01_geojson.md`.

The goal is to use an Allmaps georeference annotation to transform geographic GeoJSON into image-space SVG, then draw that SVG on top of the original unwarped IIIF image.

## Source Lesson

- PH draft: `../ph-allmaps/part-3/01_geojson.md`
- Example annotation: `../ph-allmaps/part-3/annotation.json`
- Example GeoJSON: `../ph-allmaps/part-3/voiries1300_2009_clean.json`
- Prepared geometry stream: `../ph-allmaps/part-3/voiries1300_2009_clean.geometries.ndjson`

## Planned Structure

1. Paris example source information
2. Process overview
3. Confirm the georeference annotation
4. Inspect the prepared GeoJSON
5. Transform GeoJSON into image-space SVG
6. Overlay the SVG on the IIIF image
7. Preview the result with a local web server

## Setup Note

This lesson uses the Allmaps CLI and `jq`.
Installation details live in [Lesson 4: Command Line Setup]({{ '/lessons/command-line-setup/' | relative_url }}) for now.

<!-- TODO: Decide whether to copy the Paris data files into this workshop repo or point learners to starter files. -->
<!-- TODO: Adapt the PH prose into this workshop voice without making this page as long as the publication lesson. -->
