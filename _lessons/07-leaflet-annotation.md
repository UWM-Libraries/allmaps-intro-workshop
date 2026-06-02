---
layout: lesson
title: "Lesson 7: Using an Allmaps Annotation in Leaflet"
position: 7
permalink: /lessons/leaflet-annotation/
---

# Lesson 7: Using an Allmaps Annotation in Leaflet

Before starting, make sure you have completed [Lesson 4: Command Line Setup]({{ '/lessons/command-line-setup/' | relative_url }}) or already have the required tools installed.

This lesson is adapted from a Programming Historian lesson by Stephen Appel and Ian Spangler that is currently in review.
The Leaflet workflow and demo structure here draw especially on Ian Spangler's contribution to that lesson.

Allmaps provides libraries for loading georeferenced maps as web map layers in Leaflet, OpenLayers, and MapLibre.
This lesson focuses on the [Allmaps Leaflet plugin](https://allmaps.org/docs/packages/leaflet/#_top), which lets us add an Allmaps georeference annotation as an overlay in a Leaflet web map.

## Demo Files

This workshop includes a local demo folder:

[assets/allmaps-leaflet-demo/]({{ '/assets/allmaps-leaflet-demo/' | relative_url }})

The folder contains three files:

- `index.html`: the web page structure for the map
- `script.js`: the JavaScript that creates the Leaflet map, base map, and Allmaps overlay
- `style.css`: the CSS that makes the map visible

Open the folder in a text editor such as VS Code.

To download a local copy from the workshop site, create a working directory and fetch the files:

```bash
mkdir -p ~/allmaps/allmaps-leaflet-demo
cd ~/allmaps/allmaps-leaflet-demo

curl -L "{{ site.url }}{{ site.baseurl }}/assets/allmaps-leaflet-demo/index.html" -o index.html
curl -L "{{ site.url }}{{ site.baseurl }}/assets/allmaps-leaflet-demo/script.js" -o script.js
curl -L "{{ site.url }}{{ site.baseurl }}/assets/allmaps-leaflet-demo/style.css" -o style.css
```

## Preview the Map

Because the demo loads JavaScript modules and remote map tiles, preview it through a small local web server.

If Python 3 is installed, use its built-in server:

```bash
python3 -m http.server 8000
```

Alternatively, use Node/npm:

```bash
npx http-server . -p 8000
```

Then open [http://localhost:8000/index.html](http://localhost:8000/index.html) in your browser.

You can also view the workshop-hosted copy:

<iframe src="{{ '/assets/allmaps-leaflet-demo/index.html' | relative_url }}" width="100%" height="500px"></iframe>

[View sample map in a new window]({{ '/assets/allmaps-leaflet-demo/index.html' | relative_url }}){:target="_blank"}

## Review `index.html`

Open `index.html`.
This file contains the structure for the web page and loads the external libraries.

The local stylesheet loads near the top of the page:

```html
<link rel="stylesheet" href="style.css" />
```

Leaflet and the Allmaps Leaflet plugin load from external CDNs:

```html
<script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>
<script type="module" src="https://cdn.jsdelivr.net/npm/@allmaps/leaflet/dist/bundled/allmaps-leaflet-1.9.umd.js"></script>
```

Leaflet's CSS also loads from a CDN:

```html
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" />
```

Finally, the page loads the local JavaScript file where we create the map:

```html
<script type="module" src="script.js"></script>
```

The body of the page contains a wrapper and an empty map container:

```html
<body>
  <div id="wrapper">
    <h1>Hi, Allmaps Leaflet Plugin!</h1>
    <div id="map"></div>
  </div>
</body>
```

Leaflet will use `<div id="map"></div>` as the container for the interactive map.

## Review `style.css`

Open `style.css`.
The most important rule is the one that gives the map a visible size:

```css
#map {
  width: 100%;
  height: 100vw;
  z-index: 1;
}
```

Without a width and height, the Leaflet map may technically exist but appear invisible on the page.

The wrapper stretches across the browser window:

```css
#wrapper {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
}
```

## Review `script.js`

The Allmaps Leaflet plugin uses georeference annotations to overlay maps.
This demo uses the annotation:

[https://annotations.allmaps.org/manifests/cfb327e4b43395e3](https://annotations.allmaps.org/manifests/cfb327e4b43395e3)

That annotation corresponds to [T.G. Bradford's 1838 map of Boston](https://collections.leventhalmap.org/search/commonwealth:3f463198b).

### Map Setup

To instantiate a Leaflet map, define a variable with `L.map("map", { ... })`.
The `map` string points to the `<div id="map"></div>` container in `index.html`.

```js
const map = L.map("map", {
  center: [42.3518, -71.05],
  zoom: 13,
  minZoom: 7,
  maxZoom: 24,
  zoomControl: false,
});
```

The `center` array uses latitude and longitude.
If you use a different Allmaps annotation, you will likely need to update the center and zoom values.

### Add a Base Map

The demo uses OpenStreetMap tiles as the base map.

First, it defines tile options:

```js
let tileLayerDetails = {
  tileSize: 512,
  zoomOffset: -1,
  minZoom: 14,
  maxZoom: 24,
  crossOrigin: true,
};
```

Then it adds the tile layer to the map:

```js
let streets_base = L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", tileLayerDetails).addTo(map);
```

### Add the Allmaps Annotation Layer

Next, the script defines the georeference annotation URL:

```js
let annotationUrl = 'https://annotations.allmaps.org/manifests/cfb327e4b43395e3';
```

Then it creates a new `WarpedMapLayer` from that annotation and adds it to the Leaflet map:

```js
let warpedMapLayer = new Allmaps.WarpedMapLayer(annotationUrl).addTo(map);
```

In this plain JavaScript setup, call `WarpedMapLayer` by prefixing it with `Allmaps.`.
The syntax is different if you install `@allmaps/leaflet` with npm and import it in a front-end framework.

### Add the Layer Control

Finally, the script adds a layer control so you can toggle the base map and Allmaps overlay:

```js
let base = { "OpenStreetMap": streets_base };
let overlay = { "Allmaps overlay": warpedMapLayer };
let layerControl = L.control.layers(base, overlay).addTo(map);
```

In Leaflet, these are called layer controls.
You can read more in the [Leaflet layer control documentation](https://leafletjs.com/examples/layers-control/).

## Try Another Annotation

To adapt the demo, replace `annotationUrl` with another Allmaps annotation URL.
Then update the map's `center` and `zoom` values so the map starts near the georeferenced image.

For example, you could experiment with the Paris annotation used in the previous lessons:

```js
let annotationUrl = 'https://annotations.allmaps.org/images/adeae8a56aaf59fb';
```

You will also need to update the map center to Paris:

```js
center: [48.8566, 2.3522],
```
