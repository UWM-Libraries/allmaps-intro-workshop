---
layout: default
title: Georeferencing in Allmaps
---

<link rel="stylesheet" href="assets/css/custom.css">

<div class="button-group"><a href="index.html" class="button">Back to Home</a></div>
<div class="button-group">
  <a href="Georef-and-IIIF.html" class="button">Previous Lesson: Georeferencing and IIIF</a>
  <a href="Viewer.html" class="button">Next Lesson: Doing More with Allmaps</a>
</div>

* * *

# Lesson 2: Georeferencing in Allmaps

In this lesson, we'll get hands-on experience georeferencing maps in **Allmaps**.

## Allmaps Editor

If you haven't already, launch the Allmaps Editor by going to [editor.allmaps.org](https://editor.allmaps.org).

You can choose a map by either:

1. Entering a **IIIF Manifest URL** in the text box at the top of the page
2. Scrolling down to find a map in one of the highlighted collections

![Start screen of the Allmaps Editor](images/georef_nz1_start.png)

## Masking

The first step is adding a **clipping mask**. This involves drawing a line around the "map" areas of the document to exclude the collar or marginalia. In other words, you're identifying the part of the scanned image that you want to georeference.

Use the **Draw Mask** tab to add a mask. Click to add points, and double-click to close the polygon. If you mess up, click **Cancel** to start over.

![Drawing a mask in Allmaps](images/georef_nz3_Mask.png)

It's possible your image includes multiple maps! Each map gets its own mask.

![Example of a scanned page with multiple maps](images/greenpoint.jpg)

Much of the time, your mask will simply be a rectangle drawn just inside the map's neatline.

![A rectangular mask drawn near the map corners](images/georef_nz4_MaskCorner.png)

## Ground Control Points

**Ground Control Points (GCPs)** guide Allmaps in aligning the scanned image (left side) with real-world geography (right side).

Use the **Georeference** tab to begin placing GCPs. To create one, find a location that clearly matches on both sides—such as a street intersection or the corner of a recognizable building. Click the same spot on both images.

![Adding ground control points in Allmaps](images/georef_nz2_GCP.png)

### GCP Best Practices for Urban Atlases:

- **Avoid water bodies** – they change too much over time to be reliable.
- **Use roads and buildings** – as long as they haven’t been torn down or significantly altered.
- **Check your progress** – sometimes only a few GCPs are needed. Too many can actually introduce unwanted distortion. A good check-in is after placing 5–10 points.

([Source](https://cartinal.leventhalmap.org/guides/georeferencing-with-allmaps.html#best-practices-for-creating-gcps))

Remember, landscapes change: roads shift, water levels fluctuate, buildings appear and disappear. For example, using Brown Deer Road may not always be ideal:

![Example showing problematic alignment using Brown Deer Road](images/MultiPage_BrownDeer.png)

### What is this doing?

Behind the scenes, placing GCPs in Allmaps creates a [**Georeference Annotation**](https://iiif.io/api/extension/georef/).

![Diagram of resource vs geometry coordinates](images/georef_nz2_2.png)

Each point creates a pair of values:
- **Resource coordinates** – pixel location in the image (e.g. 3017, 4367)
- **Geometry coordinates** – geographic location in longitude/latitude (e.g. 172.936215°E, 43.7589394°S)

Allmaps uses this data to calculate the warping or stretching needed to align the image over the map.

> 6-digit coordinate precision is probably overkill — any excuse to link this [XKCD comic on coordinate precision](https://xkcd.com/2170)!

## Results

The **Results** tab gives you a preview of the map with georeferencing applied. It's a great way to check alignment and see if you're on the right track.

![Preview of results in Allmaps](images/georef_nz5_result.png)

In the bottom right, you’ll see a drawer with more tools:

- **Information** – about the IIIF resource
- **GCP List** – lists all your points; delete ones that don't work
- **Code** – shows the actual Georeference Annotation (JSON format). You can copy and reuse this in the Viewer.
- **Share** – provides:
  - Link to view in Allmaps Viewer
  - Link to the annotation
  - GeoJSON download
  - XYZ tile link (usable in web maps or GIS software)

![The share menu in Allmaps](images/georef_nz6_Share.png)

We'll explore the Viewer in the next lesson. For now, click the **View in Allmaps Viewer** link in the share menu to continue.

* * *

<div class="button-group">
  <a href="Georef-and-IIIF.html" class="button">Previous Lesson: Georeferencing and IIIF</a>
  <a href="Viewer.html" class="button">Next Lesson: Doing More with Allmaps</a>
</div>
<div class="button-group"><a href="index.html" class="button">Back to Home</a></div>