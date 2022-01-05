# Leaflet.Draw.Svg

This is a plugin to Leaflet.Draw to allow adding/moving/removing custom SVG files on a leaflet map.
It allows to define a SVG as XML text, and converts it into an SVG object that can be displayed by leaflet as
an editable feature.
 
## requirements
Leaflet version 0.7
Leaflet.Draw version 0.4

## Demo
see example

# including the plugin

```
<script src='lib/leaflet.draw.svg.js' crossorigin=''></script>
<link href='css/leaflet.draw.svg.css' rel='stylesheet' crossorigin=''/>
```

# usage example

Ensure L.map uses the L.svg renderer;


Initialise the L.Draw.Svg.enable function with the svg we want to draw. here we can also include a dialog and such for selection
```var leafletmap = L.map('map', { 
    renderer: L.svg()
  });
```

You can override the L.Draw.Svg class, to hook into the draw-routine and add your own data, or dialog box, like so;
```
L.Draw.Svg.include({
  enable: function(){
    this._svgViewBox = "calculate";
    this._svgFitBounds = true;
    this._scale = 0.006;
    this._template = "<line y2=\"153.934719\" x2=\"266\" y1=\"93.434721\" x1=\"266\" stroke-width=\"1.5\" stroke=\"#ffffff\" fill=\"none\"/>\n\n<g>\n<title>PTR</title>\n<ellipse ry=\"18\" rx=\"18\" cy=\"171.753014\" cx=\"266\" fill-opacity=\"null\" stroke-width=\"1.5\" stroke=\"#ffffff\" fill=\"none\"/>\n<text stroke=\"#ffffff\"  xml:space=\"preserve\" text-anchor=\"start\" font-family=\"Helvetica, Arial, sans-serif\" font-size=\"24\" y=\"186.66199\" x=\"296\" stroke-width=\"null\" fill=\"#ffffff\">T1</text>\n<ellipse id=\"svg_T1_b\" ry=\"18\" rx=\"18\" cy=\"196.290907\" cx=\"266\" fill-opacity=\"null\" stroke-width=\"1.5\" stroke=\"#ffffff\" fill=\"none\"/>\n</g>\n\n<line stroke=\"#ffffff\" stroke-linecap=\"undefined\" stroke-linejoin=\"undefined\" y2=\"256.43483\" x2=\"266\" y1=\"214.934859\" x1=\"266\" stroke-width=\"1.5\" fill=\"none\"/>";

    // call the actual enable function to allow drawing on the map
    L.Draw.SimpleShape.prototype.enable.call(this);
  }
});
```

## options

### L.SvgObject
L.SvgObject(svgString, bounds, uuid, options)
viewBox: false, // viewbox can be "x y w h" to directly set viewBox attribute of svg, 'false' to use bounds instead, or "calculate" to derive from svg bbox
fitBounds: false, // false means bounds are used directly, true means only center latlng of bounds are used, and actual bounds are fit to bbox of svg
scaleBounds: 1.0 // scale the size of the svg bounds on the map

fitBounds()
setLatLng()
getLatLng()
all other methods inherited from L.SVGOverlay

### L.Draw.Svg
this._templateBounds = [[0,0],[100,100]]; bounds of the svg object on the map
this._svgViewBox = "calculate"; viewbox can be "x y w h" to directly set viewBox attribute of svg, 'false' to use bounds values instead, or "calculate" to derive from svg bbox
this._svgFitBounds = true; false means bounds are used directly, true means only center latlng of bounds are used, and actual bounds are fit to bbox of svg
this._scale: scale the size of the svg bounds on the map
this._template: containts SVG data

