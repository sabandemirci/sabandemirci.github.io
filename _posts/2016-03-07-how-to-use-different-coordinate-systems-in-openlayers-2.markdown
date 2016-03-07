---
layout: post
title: How to use different coordinate systems in OpenLayers 2
categories: Android
excerpt: In order to use different coordinate systems in openlayers you need to add you map object projection and displayProjection attributes.
---

In order to use different coordinate systems in openlayers you need to add you map object projection and displayProjection attributes. Here is sample code of usage

{% highlight html %}
<link rel="stylesheet" href=".http://dev.openlayers.org/theme/default/style.css" type="text/css">
<script src="http://dev.openlayers.org/OpenLayers.js"></script>
<script src="http://maps.google.com/maps/api/js?v=3&amp;sensor=false"></script>
<script src="proj4js.js"></script>

<script>
    Proj4js.defs["EPSG:900913"]= "+title=GoogleMercator +proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +no_defs";
    Proj4js.defs["EPSG:5257"]= "+proj=tmerc +lat_0=0 +lon_0=39 +k=1 +x_0=500000 +y_0=0 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs";
    var geographic = new OpenLayers.Projection("EPSG:900913");
    var mercator = new OpenLayers.Projection("EPSG:5257");
    var map;
    function init() {
        var layer=new OpenLayers.Layer.WMS( "Different Layer", "SERVER_URL",
            {
                layers:'LAYER_NAME',
                type: 'png', 
                isBaseLayer: false, 
                projection:geographic, 
                transitionEffect: 'resize',
                transparent:true
            },
            {
                transparent:false,
                isBaseLayer: true, 
                projection:geographic, 
                transitionEffect: 'resize'
            } 
        );

        map = new OpenLayers.Map({
            div: "map",
            projection:geographic ,
            displayProjection: geographic,
            numZoomLevels: 18        
        });

         var ghyb = new OpenLayers.Layer.Google(
            "Google Hybrid",
            {type: google.maps.MapTypeId.SATELLITE, numZoomLevels: 20}
        );

        map.addLayers([
        	new OpenLayers.Layer.Google(
                "Google SATELLITE",
                {type: google.maps.MapTypeId.SATELLITE, numZoomLevels: 20}
            ),
            new OpenLayers.Layer.Google(
                "Google HYBRID",
                {type: google.maps.MapTypeId.HYBRID, numZoomLevels: 20}
            ),
            layer]);
        //now add the required controls:
        map.addControl(new OpenLayers.Control.LayerSwitcher());
        map.addControl(new OpenLayers.Control.Permalink());
        map.addControl(new OpenLayers.Control.MousePosition());

        var lonLat = new OpenLayers.LonLat(483334.40155, 4196011.14304).transform(mercator, displayProjection);
        map.setCenter (lonLat, 9);
    }

</script>
{% endhighlight %}