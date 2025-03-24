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

## Results

Allmaps Viewer offers a little more functionalities to reflect the result:

- Via the "space" button you can make the map transparent.
- Via the "B" button or the right button you can partially remove the background color.
- You can display the mask via the M key.
- You can change the transformation algorithm via the "T" key.
- Via the "G" key you can display a grid over the image.
- Via the "D" key you can display distortions: surface deformation, angle distortion, or no distortion.
- You can browse through the "[" and] keys through the different maps (for compound objects).
- Via a right click on a card you can adjust the order of the map layers.

 