---
title: Introduction to Turf JS
subtitle: Geospatial Analysis for the Browser, Desktop & Server
layout: slides-big
theme: light
date: 2018-09-25
style: >-
  html {
    overflow: hidden;
  }
  .display-content {
    display: contents;
  }
  h1 {
    font-size: inherit
  }
  body.talk-mode, p, h1 {
    font-family: "Montserrat", "Rubik", "Segoe UI", sans-serif;
    font-weight: 600;
  }
  strong {
    color: #2ecc71;
    font-size: inherit;
  }
  input {
    width: 60%;
  }
  .input-group {
    margin: 10px 0;
  }
  .input-group button {
    width: 38%;
    float: right;
  }
  button, input {
    font-size: inherit;
  }
  @media screen and (min-width: 1440px) {
    .emoji {
      font-size: 256px!important; 
    }
  }
  .print-mode .emoji, .jump-mode .emoji {
    font-size: inherit!important;
  }
  code, pre code {
    box-shadow: none;
    font-size: inherit;
    background-color: white;
    padding: 10px;
    border: solid thin lightgray;
  }
  pre code {
    padding-right: 20px;
    padding-left: 20px;
  }
  .buttons {
    background: black;
    width:100%;
  }
  #buttons {
    position: absolute;
    top: 0;
    width: 100%;
    z-index: 1;
    left: 0;
    background: black;
  }
  .buttons button {
    float: left;
    font-size: 1.2rem;
  }
  .buttons > button:last-child {
    float: right;
  }
  .btn.btn-clear:hover {
    opacity: 1;
    background-color: lightgray;
  }

  .btn.btn-primary:not(.map-btn),
  .btn.btn-primary.map-btn {
    color: white;
    background: black;
    border-color: black;
    z-index: 600;
  }
  .btn.btn-link {
    color:#000;
  }
  .btn.btn-link:hover, .btn.btn-link:focus,.btn.btn-link:active {
    color:#000;
  }
  .btn.btn-primary:focus,
  .btn.btn-primary:hover,
  .btn.btn-primary:active, .btn.btn-primary.active {
    background: white;
    border-color: #000;
    color: #000;
    opacity: 1;
  }
  .btn.btn-primary .icon-location,
  .icon-arrow-right,
  .icon-arrow-left {
    width: 60px;
  }
  .map {
    position: relative;
    top: 0;
    left: 0;
    height: calc(65vh);
    width: 100%;
    background-color: whitesmoke;
    border: solid thin;
  }
  .print-mode .map, .jump-mode .map {
    height: 40px;
    width: 40px;
  }
  .mapboxgl-map .mapboxgl-popup .mapboxgl-popup-content {
    font-size: 1rem;
    padding: 1rem;
    max-width: 300px;
    word-break: break-all;
  }
  .img {
    width:90%;margin:0 auto;
  }
  .light {
    background-image: linear-gradient(to top right, #e6e6e6, white);
  }
  .jump-mode div.slide {
      width: inherit;
      overflow: hidden;
  }
  .slide a {
    color: #2ecc71;
    text-decoration: underline;
  }
head: >-
  <link rel="stylesheet" href="/montserrat/Montserrat.css" />
  <link rel="stylesheet" href="css/mapbox-gl.css">
  <script src="js/mapbox-bundle-min.js"></script>
  <script src="/assets/topojson.min.js"></script>
---
<div  style="width:90%;margin:0 auto;">

![](img/OhioGIS_Title_Page_2018.png)

</div>

<div class="emoji">👶👧👩
</div>

<div>What is <strong>TurfJS?</strong>
</div>

<div>Advanced <strong>geospatial analysis</strong> for browsers and Node.js
</div>

<div><strong>Modular => </strong> 
Area, Bounding Box, Buffer, Grids, Intersect, Isolines, Length, Random, Sample, Voroni, Within...
</div>

<div>JavaScript functions that speak <strong>GeoJSON</strong>
</div>

<div><strong>What</strong> is GeoJSON?</div>

<div><pre><code>
/** GeoJSON is a single JSON file containing one or more features */
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [-82, 39] /*WGS 84*/
      },
      "properties": {
        "field": "value"
      }
    }
  ]
}
</code></pre>
</div>

<div>GeoJSON is <strong>Everywhere</strong>
</div>

<div><em>

ArcGIS Feature to JSON</em> 
[USGS Earthquake Feed](https://earthquake.usgs.gov/fdsnws/event/1/)<strong>
DATA.GOV (1,600+ Datasets)</strong> <em>AGOL Query Response & Exports</em>
[geojson.xyz (Natural Earth Data+)](http://geojson.xyz)
<strong>Native Support in</strong> [QGIS](https://www.qgis.org/en/site/)

</div>

<div class="img"><h1>GitHub Support (2013)</h1>
<img src='img/github-geojson-2.png' width='100%'>
</div>

<div>Free & Open 

Source Software
[github.com/Turfjs](https://github.com/Turfjs)
</div>

<div ># Include in your HTML
<pre><code>https://cdnjs.cloudflare.com/ajax/libs/Turf.js/5.1.5/turf.min.js</code></pre>
<br><br>
# Install via NodeJS  
<pre><code>npm install @turf/turf --OR-- npm install @turf/bbox</code></pre>
</div>

<div>Why use <strong>TurfJS?</strong>
</div>

<div><strong>Simple geospatial queries</strong>
</div>

<div>Complex geospatial analysis <strong>(in NodeJS)</strong>
</div>

<div style="border: solid thick #2ecc71;">
Creating spatial metadata (bounding box)
</div>

<div>A Few Examples
</div>

<div>  Turf Within
  <pre><code>turf.booleanWithin(point, polygon)</code></pre>
</div>

<div><h1>Where am I?</h1>
<pre><code>
var result = "";
counties.features.map(function(county) {
  var point = turf.point([x,y]);
    if (turf.booleanWithin(point, county) {
      result = county.properties.NAME;
    }
});
</code></pre>
<div class="input-group">  <input type="text" class="form-input" value="-82,39">  <button class="btn btn-primary input-group-btn" id="withinSubmit">Submit</button>
</div>
</div>

<div id="formResult">Click the Submit button on the previous page</div>

<div class="emoji">🤯😵🧐</div>

<div class="emoji">🤨😭😕</div>

<div>  Practical Applications
</div>

<div>  Local <strong>Authoritative</strong> Open Data
</div>

<div>  Turf Nearest
  <pre><code>Array.filter()</code></pre>
  <pre><code>turf.nearestPoint(point, points)</code></pre>
</div>

<div ># Find the Closest Playground
<pre><code>
var data = amenities.features.filter(function(a) {
  return a.properties.TYPE === 'Playground' 
})

var playgrounds = turf.featureCollection(data);

var result = turf.nearestPoint(point, playgrounds)
</code></pre>

<div class="input-group">  <input type="text" value="-82.007054,39.942022">  <button class="btn btn-primary input-group-btn" id="nearestSubmit">Submit</button>
</div>
</div>

<div id='playgroundResult'>
Loading...
</div>


<div class="emoji">😍😍😍</div>

<div >Advanced Analysis in <strong>TurfJS</strong>
</div>

<div class="emoji">🐨😴💤</div>

<div>Visualizing <strong>Crashes</strong> in Muskingum County (>7k)
</div>

<div>Hexgrids
<pre><code>turf.hexGrid(bbox, size, opts)</code></pre>
Intersect
<pre><code>turf.intersect(a,b)</code></pre>
Collect
<pre><code>turf.collect(p, pts, field, name)</code></pre>
</div>

<div><h1>Turf Hexgrids</h1>
<pre><code>
var bbox = [-82.5, 39.7, -81.5, 40.18];
var size = 1;
var options = {
  units: 'miles'
};

var hexgrid = turf.hexGrid(bbox, size, options)
</code></pre>
</div>
<div >
Turf Intersect 
<pre><code>
// loop through each grid
// add the intersecting areas to the clippedGrid
// calculate the area in sq miles

var clippedGrid = { "type":"FeatureCollection", "features":[] }

hexgrid.features.map(function(grid) {
  var toFt = 0.00000386102159
  var intersect = turf.intersect(grid, muskingum);
  if (intersect) {
    intersect.properties.area = (turf.area(intersect)) * toFt;
    clippedGrid.features.push(intersect);
  }
});
</code></pre>

</div>

<div>  Turf Collect
  <pre><code>turf.collect(clippedGrid, crashes, "count", "total")</code></pre>
</div>

<div class="display-content">  <div id="map" class="map">    <div id="buttons" class="buttons"></div>
  </div>
</div>

<div >Turf in <strong>Node JS</strong>
</div>

<div>Find the Nearest 🏕️ National Park</div>
<div>45MB GeoJSON Park Boundary File
</div>

<div><pre><code>var points = turf.explode(polygon)</code></pre>

<pre><code>turf.nearestPoint(point, points)</code></pre>
</div>

<div>Query NodeJS
<form class="input-group">    <div class="input-group">      <input class="form-input" name="lng" type="text" id="lng" placeholder="Longitude" value="-82">
    </div>
    <div class="input-group">      <input class="form-input" type="text" id="lat" placeholder="Latitude" name="lat" value="39">    </div>    <button class="btn btn-primary form-input" id="nearestPolySubmit" style="float:left;">Submit</button>
  </form>
</div>

<div id="nearestPolyResult">No Node JS Server Running! Tested Benchmark ~ 2 seconds
</div>

<!--div>
Turf Center
<pre><code>
var center = {
  "type": "FeatureCollection",
  "features": []
};

/* Calculate the center for each grid */

hexgrid.features.map(function (feature) {
  center.features.push(turf.centerOfMass(feature));
});
</code></pre>
</div-->

<div >

No Coding
[Dropchop](http://dropchop.io/)

</div>

<div >

Support [TurfJS](https://opencollective.com/turf)

</div>

<div >

Thanks!
Malcolm Meyer
[@getbounds](https://twitter.com/getbounds)

</div>

<script>
var counties, map, labels, crashes;
var playgrounds = {
  type: "FeatureCollection",
  features: []
};
var muskingum;

function getJSON(url, callback) {
  var req = new XMLHttpRequest();
  req.overrideMimeType("application/json");
  req.open('GET', url, true);
  req.onload = function () {
    var jsonResponse = JSON.parse(req.responseText);
    callback(jsonResponse)
  };
  req.send(null);
}

fetch('/2018-intro-to-turfjs/data/crashes.json').then(function (res) {
  return res.json();
})
  .then(function (data) {
    crashes = data;
  })
  .catch(function (err) {
    console.log(err);
  });

fetch('/2018-intro-to-turfjs/data/counties.topojson').then(res => {
  return res.json();
}).then(data => {
  counties = topojson.feature(data, data.objects["counties_single_fixed"]);
  counties.features.map(function (f, i) {
    if (f.properties.NAME === "Muskingum") {
      muskingum = f;
    }
  })
  console.log(muskingum);
  buildMap();
  buildApp();
})
  .catch(function (err) {
    console.log(err);
  });

function getPosition() {

  var currentLocation;

  var options = {
    enableHighAccuracy: true,
    timeout: 5000,
    maximumAge: 0
  };

  function success(pos) {
    var crd = pos.coords;
    currentLocation = [crd.longitude, crd.latitude];
    console.log('Your current position is:');
    console.log(`Latitude : ${crd.latitude}`);
    console.log(`Longitude: ${crd.longitude}`);
    console.log(`More or less ${crd.accuracy} meters.`);
  }

  function error(err) {
    console.warn(`ERROR(${err.code}): ${err.message}`);
  }

  navigator.geolocation.getCurrentPosition(success, error, options);

  return currentLocation;
}

function buildApp() {
  var hexgrid = {},
    center = {},
    clippedGrid = {
      "type": "FeatureCollection",
      "features": []
    };

  function createButton(html, fn, id) {
    var button = document.createElement('button');
    button.innerHTML = html;
    button.className = className = "btn btn-primary map-btn";
    button.onclick = fn;
    button.addEventListener('click', function () {
      getLayers(map)
    })
    document.getElementById(id).appendChild(button)
  }

  createButton("Create Hex Grid", createHexgrid, "buttons")
  createButton("Clip Grid", clipGrid, "buttons")
  createButton("Collect", collect, "buttons");
  createButton("Center of Mass", getCenter, "buttons")
  createButton("Create Labels", createLabels, "buttons");
  createButton("Bounds", bounds, "buttons");
  createButton("Reset", reset, "buttons");

  function collect() {
    reset()
    if (!getLayers(map, "within")) {
      var l = ((clippedGrid.features).length) - 1;
      console.log(l);
      var within = turf.collect(clippedGrid, crashes, "count", "crashvalues");
      var counts = [];
      var checkTurf = setInterval(function () {
        if (within && within.features[l]) {
          clearTimeout(checkTurf);
          within.features.map(function (f) {
            f.properties.count = (f.properties.crashvalues).length;
            counts.push((f.properties.crashvalues).length);
            delete f.properties.crashvalues;
          });
          var limits = chroma.limits(counts, 'k', 5)
          console.log(limits);
          var scale = chroma.scale('OrRd').colors(limits.length);
          map.addLayer({
            id: "within",
            type: "fill",
            source: {
              type: "geojson",
              data: within
            },
            paint: {
              "fill-color": {
                "property": "count",
                stops: [
                  [limits[0], scale[0]],
                  [limits[1], scale[1]],
                  [limits[2], scale[2]],
                  [limits[3], scale[3]],
                  [limits[4], scale[4]]
                ],
              },
              "fill-outline-color": "white",
              "fill-opacity": 1
            }
          }, 'counties')
          console.log(within)
        }
      }, 500);
    }
  }

  function bounds() {
    var num = Math.floor((Math.random() * 3481))
    console.log(num)
    var bbox = turf.bbox(counties.features[num])
    console.log(bbox)
    map.fitBounds([
      [bbox[0] - .2, bbox[1] - .2],
      [bbox[2] + .2, bbox[3] + .2]
    ]);

  }

  function clipGrid() {
    reset()
    if (hexgrid.features.length > 0 && clippedGrid.features.length === 0) {
      console.log(true)
      hexgrid.features.map(function (feature) {
        var intersect = turf.intersect(feature, muskingum);
        if (intersect) {
          intersect.properties.area = ((turf.area(intersect)) * 0.00000386102159).toFixed(2);
          clippedGrid.features.push(intersect);
        }
      });
    }
    console.log(clippedGrid)
    if (hexgrid.features && !getLayers(map, "clippedGrid")) {
      console.log(true)
      map.addLayer({
        id: "clippedGrid",
        type: "fill",
        source: {
          type: "geojson",
          data: clippedGrid
        },
        paint: {
          "fill-color": 'rgba(212, 230, 241, 0.3)',
          "fill-outline-color": "#3498DB",
          "fill-opacity": 1
        }
      })
    }
  }

  function reset() {
    var layers = map.getStyle().layers
    for (l in layers) {
      if (layers[l].id != "counties" && layers[l].id != "background" && layers[l].id != "countiesFill") {
        console.log(layers[l].id)
        map.removeLayer(layers[l].id);
        map.removeSource(layers[l].source)
      }
    }
    map.flyTo({
      center: [-81.99, 39.93],
      zoom: 8.6
    })
  }

  function createHexgrid() {
    hexgrid = {};
    var bbox = [-82.5, 39.7, -81.5, 40.18];
    var cellSize = 1;
    var options = {
      units: 'miles'
    };

    hexgrid = turf.hexGrid(bbox, cellSize, options);

    map.addLayer({
      id: "hex",
      type: "fill",
      source: {
        type: "geojson",
        data: hexgrid
      },
      paint: {
        "fill-color": '#2ecc71',
        "fill-outline-color": "black",
        "fill-opacity": 0.6
      }
    })
    map.addLayer({
      id: "hexline",
      type: "line",
      source: {
        type: "geojson",
        data: hexgrid
      },
      paint: {
        "line-color": "#2ecc71",
        "line-width": 2
      }
    })

  }


  function getCenter() {
    if (!map.getLayer('center') && map.getLayer('hex') != "undefined") {
      center = {
        "type": "FeatureCollection",
        "features": []
      };
      hexgrid.features.map(function (f, i) {
        center.features.push(turf.centerOfMass(f));
      });

      map.addLayer({
        id: "center",
        type: "circle",
        source: {
          type: "geojson",
          data: center
        },
        paint: {
          "circle-radius": 10,
          "circle-blur": 2,
          "circle-opacity": 1,
          "circle-color": "black"
        }
      })
    } else {
      alert('error')
    }
  }

  function createLabels() {
    labels = {
      "type": "FeatureCollection",
      "features": []
    };
    counties.features.map(function (f) {
      var p = f.properties;
      // var xy = polylabel(f.geometry.coordinates);
      // if(!xy[0]) {
      //   xy = [0,0]
      // }
      // labels.features.push({
      //   "type":"Feature",
      //   "geometry": {
      //     "coordinates":[],
      //     "type":"Point"
      //   },
      //   "properties":{}
      // });
      // labels.features[i].geometry.coordinates = xy
      // labels.features[i].type = "Feature";
      // labels.features[i].properties = {"NAME":p.NAME};
      // console.log(polylabel(f.geometry.coordinates));
      labels.features.push(turf.centerOfMass(f, {
        "NAME": p.NAME
      }));
    });
    console.log(labels)
    map.addLayer({
      id: "labels",
      type: "symbol",
      source: {
        type: "geojson",
        data: labels
      },
      'minzoom': 6,
      'layout': {
        'visibility': 'visible',
        "text-field": "{NAME}",
        "text-anchor": "center",
        "text-size": 14,
        "text-font": ["Open Sans Regular"]
      }
    });

    map.flyTo({
      center: map.getCenter(),
      zoom: 7.2,
      speed: 0.1
    })

  }
}

function buildMap() {
  map = new mapboxgl.Map({
    container: 'map',
    style: {
      "version": 8,
      sources: {
        "counties": {
          type: "geojson",
          data: counties
        }
      },
      "glyphs": "/2018-intro-to-turfjs/{fontstack}/{range}.pbf",
      layers: [{
        id: "background",
        "type": "background",
        "paint": {
          "background-color": "lightblue"
        }
      }, {
        id: "countiesFill",
        type: "fill",
        source: "counties",
        paint: {
          "fill-color": "white",
          "fill-opacity": 1
        }
      },
      {
        id: "counties",
        type: "line",
        source: "counties",
        paint: {
          "line-color": "#333",
          "line-width": {
            stops: [
              [0, 1],
              [14, 3]
            ]
          },
          "line-opacity": 1
        }
      }
      ]
    },
    center: [-81.99, 39.93],
    zoom: 8.6,
  });

  var distanceContainer = document.getElementById('distance');

  var geojson = {
    "type": "FeatureCollection",
    "features": []
  };

  var linestring = {
    "type": "Feature",
    "geometry": {
      "type": "LineString",
      "coordinates": []
    }
  };

  map.on('load', function () {
    window.onhashchange = function () {
      map.resize();
      var div = document.body
      var hash = window.location.hash;
      var opt = {
        margin: 0,
        filename: hash + '.pdf',
        image: {
          type: 'jpeg',
          quality: 0.98
        },
        // html2canvas:  { scale: -1 },
        jsPDF: {
          unit: 'in',
          format: 'tabloid',
          orientation: 'landscape'
        }
      };
    }

    map.resize();
    map.addLayer({
      'id': "crashes",
      "type": "circle",
      source: {
        type: "geojson",
        "data": crashes
      },
      paint: {
        "circle-radius": 10,
        "circle-blur": 2,
        "circle-opacity": 1,
        "circle-color": "black"
      },
      layout: {
        "visibility": "none"
      }
    })
  });

  var inputs = document.querySelectorAll('input');
  for (var i = 0; i < inputs.length; i++) {
    inputs[i].addEventListener('click', function (e) {
      e.preventDefault();
      e.cancelBubble = true;
    });
  }

  var withinLoc = document.getElementById('withinSubmit');
  withinLoc.addEventListener('click', function (e) {
    e.preventDefault();
    // e.cancelBubble = true;
    // if (e.stopPropagation) e.stopPropagation
    console.log(this.parentElement)
    var loc = this.parentElement.children[0].value;
    var coord = loc.split(",")
    console.log(coord)
    var county = {};
    counties.features.map(function (f) {
      if (turf.booleanWithin(turf.point([Number(coord[0]), Number(coord[1])]), f)) {
        county = f;
      }
    });
    var result = document.getElementById("formResult");
    result.innerHTML = '<strong>' + county.properties.NAME + ' County, ' + county.properties.STNAME + '<strong>'
  });

  var nearestLoc = document.getElementById('nearestSubmit');

  nearestLoc.addEventListener('click', function (e) {
    e.preventDefault();
    var loc = this.parentElement.children[0].value;
      console.log(this)

    var coord = loc.split(",");
    var point = turf.point([Number(coord[0]), Number(coord[1])]);
    if (playgrounds.features.length == 0) {
      fetch('/2018-intro-to-turfjs/data/amenities.geojson')
        .then(function (res) {
          return res.json()
        })
        .then(function (data) {
          playgrounds.features = data.features.filter(function (d) {
            return d.properties.TYPE === 'Playground'
          });
          var test = data.features.filter(function (d) {
            return d.properties.TYPE === 'Playground'
          });
          console.log(turf.featureCollection(test))
          console.log(playgrounds)
          getNearest(point, playgrounds)
        })
    } else {
      getNearest(point, playgrounds)
    }
  })

  function getNearest(p, pts) {
    var playground = turf.nearestPoint(p, pts)
    var r = document.getElementById('playgroundResult');
    console.log(playground);
    r.innerHTML = '<strong>' + playground.properties.PARK + ' (' + Math.round((playground.properties.distanceToPoint * 0.621371) * 100) / 100 + ' mi)</strong>';
  }

  var nearestPolySubmit = document.getElementById('nearestPolySubmit');

  nearestPolySubmit.addEventListener('click', function (e) {
    e.preventDefault();
  });
  //   var loading = document.getElementById('findthenearestpolygon');
  //   var result = document.getElementById('nearestPolyResult');
  //   result.innerHTML = "Loading...";
  //   var lat = e.target.parentElement[1].value;
  //   var lng = e.target.parentElement[0].value;
  //   var url = 'http://127.0.0.1:3000/query/?lng=' + lng + '&lat=' + lat;
  //   getJSON(url, function (json) {
  //     result.innerHTML = '<strong>' + json.properties.PARKNAME + '</strong> (' + json.properties.secToFindPoint + ' sec)'
  //   })
  // })

  appUtils(map)
}


function appUtils(map) {

  map.on('render', afterChangeComplete); // warning: this fires many times per second!

  function afterChangeComplete() {
    if (!map.loaded()) {
      return
    } // still not loaded; bail out.

    // now that the map is loaded, it's safe to query the features:
    // map.queryRenderedFeatures(...);

    console.log('map rendered')

    var mapbuttons = document.querySelectorAll('.map-btn');
    for (var b = 0; b < mapbuttons.length; b++) {
      mapbuttons[b].addEventListener('click', function (e) {
        console.log('click');
        e.preventDefault();
        e.cancelBubble = true;
      });
    }

    var m = document.getElementById('map')
    m.addEventListener('click', function (e) {
      e.preventDefault();
      e.cancelBubble = true;
    });

    map.off('render', afterChangeComplete); // remove this handler now that we're done.
  }

  map.on('click', function (e) {
    var clickedFeatures = map.queryRenderedFeatures(e.point);
    console.log(clickedFeatures)
    new mapboxgl.Popup()
      .setLngLat(e.lngLat)
      .setHTML(JSON.stringify(clickedFeatures[0].properties, 0, 2))
      .addTo(map);
    // console.log(map.queryRenderedFeatures(e.point))
  })

}

function getLayers(m, l) {
  var layerList = [];
  var obj = m.getStyle().layers;
  obj.map(function (o, i) {
    layerList[i] = o.id
  })
  if (layerList.indexOf(l) > -1) {
    return true
  }
  console.log(layerList)
}

window.onhashchange = function () {
  map.resize();
  var div = document.body
  var hash = window.location.hash;
  var opt = {
    margin: 0,
    filename: hash + '.pdf',
    image: {
      type: 'jpeg',
      quality: 0.98
    },
    // html2canvas:  { scale: -1 },
    jsPDF: {
      unit: 'in',
      format: 'tabloid',
      orientation: 'landscape'
    }
  };
}
</script>