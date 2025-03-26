# Doing more with Allmaps

## Allmaps Viewer

Allmaps Viewer is used for viewing georeferenced maps in Allmaps. Similar to the results tab of editor, you can view the map overlaid on a web map.
Viewer has a vew more tools that you can use to change the appearance and functionality of the map.

The most common tools are on the bottom of the page and look like small dials. They control layer transparency/opacity and background removal.

Background Removal is particularly useful with historical maps because it allows us to overlay the map data while not showing the blank space on the paper.

![Image](images/georef_nz8_Background.png)

Other functionalities and keyboard shortcuts include:

- Toggle transparency on and off with `Space`
- Toggle background removal with `B`
- Display the mask with the `M`
- Change the transformation algorithm with `T`
- Display a grid over the image with `G`
- Use `D` to cycle display of distortions: surface deformation, angle distortion, or no distortion.

For objects with multiple maps:

- `[` and `]` keys cycle through the different maps
- `right click` on a map to adjust the order of the map layers

## Viewing stitched atlas sheets

I've been working on: https://collections.lib.uwm.edu/iiif/info/agdm/36112/manifest.json

You can see if a map in a set has already been georeferenced by looking for the green symbol:

![Image](images/MultiPageGreen.png)

And if someone has already created a mask but hasn't started Georeferencing, it will show a yellow warning:

![Image](images/MultiPageYellow.png)

Using viewer, you can see the pages stitched together:

![Image](images/MultiPageStitch.png)

## Changing Transformation Algorithm

![Image](images/transform.gif)

## XYZ Tiles in GIS

## More you can do