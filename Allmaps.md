# Georeferencing in Allmaps

In this lesson, we will actually get some hands-on experince georeferencing in Allmaps.

## Allmaps Editor

If you haven't already, launch the Allmaps editor by going to [editor.allmaps.org](https://editor.allmaps.org).

You can choose a map by either...

1. Enter a IIIF Manifest URL in the text box at the top of the page
2. Scroll down to find a map in one of the highlighted collections. 

![Image](images/georef_nz1_start.png)

## Masking

The first step is adding a clipping mask.
This involves drawing a line around the "map" areas of the document to exclude the map collar.
In other words, it's identifying the part of the scanned image that we want to georeference.

![Image](images/georef_nz3_Mask.png)

It's possible your map image includes multiple maps! Each map will get it's own mask!

![Image](images/weymouth.png) (img src https://cartinal.leventhalmap.org/guides/georeferencing-with-allmaps.html#what-is-masking)

Much of the time, your mask will be one rectangle just inside the neatline.

![Image](images/georef_nz4_MaskCorner.png)

## Ground Control Points

Ground control points (GCPs) guide Allmaps in aligning the scanned map on the left side of the screen with the real-world geography on the right side.

To create a GCP, find a location that clearly matches on both sides—like an unchanged street intersection or the corner of a lasting building. Click that same spot on both sides of the editor.

![Image](images/georef_nz2_GCP.png)

### GCP Best Practices:

**Avoid water bodies**—they change too much over time to trust for georeferencing

**Roads and buildings are useful**—as long as roads and buildings haven't been torn down or paved over, these are your safest bet for identifying a shared location between past and present

**Check your progress**—sometimes it only takes a few points to successfully georeference a map. Furthermore, adding too many points can actually create undesirable distortions in the warped image. As you georeference your map, check your progress along the way (for example, maybe at 5 GCPs and again at 10 GCPs)

(From https://cartinal.leventhalmap.org/guides/georeferencing-with-allmaps.html#best-practices-for-creating-gcps)

### What is this doing?




## Results



 