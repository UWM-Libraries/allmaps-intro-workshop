---
layout: default
title: Georeferencingt and IIIF
---

<link rel="stylesheet" href="assets/css/custom.css">

<div class="button-group">
    <a href="index.html" class="button">Back to Home</a>
    <a href="Allmaps.html" class="button">Next Lesson: Georeferencing in Allmaps</a>
</div>

# Lesson 1: Georeferencing and IIIF

## [here.allmaps.org](https://here.allmaps.org)

Go to [here.allmaps.org](https://here.allmaps.org) in your browser and, if prompted, allow the website to access your location.

The maps returned are maps that have been Georeferenced using the Allmaps platform. They're all maps held in digital collections, for example
the [AGSL Digital Map Collection](https://uwm.edu/lib-collections/agsl-digital-map-collection/).
In fact, any map in our collection can be used.
Furthermore, maps from any collection that uses IIIF, the International Image Interoperability Framework.


## Georeferencing

### What is Georeferencing?

[Georeferencing](https://en.wikipedia.org/wiki/Georeferencing) is the process of overlaying a digital image on a map by matching pixels on the image to real geographic locations. This is commonly done with aerial and satellite photography to transform photographs into usable spatial data.

The AGSL uses Georeferencing of aerial photography in our 
[Operation Birds Eye](https://uwm.maps.arcgis.com/apps/webappviewer/index.html?id=4e066bb8e5664d189ac3e77c26d21712)
discovery application. 
While anyone is welcome to flip through the nearly 300 photographs that make up this collection,
seeing them overlaid over modern satellite imagery adds additional context and the ability to make comparison over time.

Georeferencing scanned maps enables some useful analysis methods:
- One can extract information from a map, such as locations of topographic features like villages, mountains, rivers, or roads.
- Overlaid on top of one-another, two maps can be directly compared or verified.
- And for large sets of maps that use many sheets to cover a geographic area, georeferencing can help create a *mosaic* for viewing
multiple sheets at once.

The example below shows the South Carolina state line being overlaid on a historic map in GIS, a basic yet useful function made possible by georeferencing.

![image](images/georef_bok.png)
*The georeferencing process to place a digital image into a GIS* ([Source for image and caption.](https://gistbok-ltb.ucgis.org/page/27/concept/8131))

For objects with multiple sheets or pages, such as atlases of urban areas, georeferencing can make the experience easier and more fun.
We used georeferenced Sanborn Fire Insurance Maps to make our
[Sanborn Web Map](https://webgis.uwm.edu/agsl/sanborn/).
A similar project by our partners at Leventhal Map & Education Center at Boston Public Library (co-awardees of a NEH Digital Advancement Grant) used Allmaps
to georeference urban atlas sheets for their fantastic [Atlascope application](https://www.atlascope.org/).

Traditionally, georeferencing has been done with GIS--Geographic Information Systems.
With the proliferation of accessible and easy-to-use web mapping and GIS technology, 
products like Allmaps make the processes possible for non-experts in a browser environment.

There's a lot more that can be said about Georeferencing, but this is enough to get started!
For much more information, I recommend [*Georeferencing and Georectification*](https://gistbok-topics.ucgis.org/DC-01-030) in the GIS&T Body of Knowledge.

## What is IIIF?

IIIF (pronounced “triple-eye-eff”), or the [International Image Interoperability Framework](https://iiif.io/),  
is a set of open standards for delivering high-quality, attributed digital objects online at scale.  

IIIF provides a consistent way for institutions to share digital images, maps, manuscripts, artworks, and even audio/visual files across different platforms. Rather than locking media inside specific viewers or software tools, IIIF offers a **standardized, flexible way** to deliver these resources to any compatible application.

This means that:

- A digitized map from one library can be viewed side-by-side with one from another institution.
- A scholar can annotate or compare high-resolution images without downloading huge files.
- Tools like [Allmaps](https://allmaps.org/), [Mirador](https://projectmirador.org/), and [Universal Viewer](https://universalviewer.io/) can all read the same IIIF content.

At its core, IIIF allows for **interoperability** — making it easier for cultural heritage institutions, educators, and developers to **build rich user experiences around media** from all over the world.

Learn more about how it works at [iiif.io](https://iiif.io/get-started/how-iiif-works/).  
([source](https://iiif.io/get-started/how-iiif-works/))

Take a look at the AGSL's treasured [Leardo Mappamundi](https://collections.lib.uwm.edu/digital/collection/agdm/id/538/).
Clicking on the expand arrows allows us to view the map in stunning detail right in our browser, without the need to download large image files.
But beyond making images zoomable, IIIF does so much more...


### Finding IIIF maps to use in Allmaps

Allmaps works best with large geographic scale, such as maps of neighborhoods, cities, states, or countries. While you can georeference small scale maps like world maps, the distortion that can be introduced by the georeferencing process can make them harder to work with
(because the majority of web mapping applications use Web Mercator coordinate reference systems). Allmaps excels at georeferencing city atlases; city, county, and state maps; and topographic or thematic maps in a series. 

Any map that is hosted using IIIF will work in Allmaps.
The IIIF consortium lists some collections [at this link](https://iiif.io/guides/finding_resources/). Note some very well known map collections including 
the [Library of Congress](https://www.loc.gov/maps) and [The David Rumsey Map Collection](https://www.davidrumsey.com/luna/servlet/view/all).

If you launch the Allmaps Editor [(editor.allmaps.org)](https://editor.allmaps.org),
some maps hosted by some Allmaps partners (including the AGSL) that are waiting to be georeferenced are displayed.

If you're on the [AGSL Digital Map Collection](https://uwm.edu/lib-collections/agsl-digital-map-collection/)
site and have a particular map you would like to georefernece, you need to find its IIIF Manifest URL. 
You can find this at the bottom of the page of any object. 

![Image](images/manifestURL.png)

Other websites may require a bit more sluthing to find the URL. On the David Rumsey Collection you will find the URL under the share menu. Other websites may not expose their manifest URLs at all, but you can use tools like the [DetectIIIF browser](https://seige.digital/en/detektiiif/) extension to help.

![Screenshot of the menu option to find IIIF Manifessts in the David Rumsey Map Collection Luna Viewer](images/rumsey.png)

* * *

<div class="button-group">
    <a href="index.html" class="button">Back to Home</a>
    <a href="Allmaps.html" class="button">Next Lesson: Georeferencing in Allmaps</a>
</div>
