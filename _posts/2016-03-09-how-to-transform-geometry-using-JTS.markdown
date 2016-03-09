---
layout: post
title: How to transform geometry using JTS
categories: Java
excerpt: Here is conversion of geometry objects between custom defined CRS using JTS(Geotools)
---

Here is conversion of geometry objects between custom defined CRS using JTS(Geotools)

{% highlight java %}
    try {

        String customLocal = "PROJCS[\"TUREF / TM39\", " + //
            " GEOGCS[\"TUREF\", " + //
            "   DATUM[\"Turkish National Reference Frame\"," + // 
            "     SPHEROID[\"GRS 1980\", 6378137.0, 298.257222101, AUTHORITY[\"EPSG\",\"7019\"]]," + // 
            "     TOWGS84[0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0], " + //
            "     AUTHORITY[\"EPSG\",\"1057\"]], " + //
            "   PRIMEM[\"Greenwich\", 0.0, AUTHORITY[\"EPSG\",\"8901\"]]," + // 
            "   UNIT[\"degree\", 0.017453292519943295], " + //
            "   AXIS[\"Geodetic longitude\", EAST], " + //
            "   AXIS[\"Geodetic latitude\", NORTH], " + //
            "   AUTHORITY[\"EPSG\",\"5252\"]], " + //
            " PROJECTION[\"Transverse_Mercator\", AUTHORITY[\"EPSG\",\"9807\"]]," + // 
            " PARAMETER[\"central_meridian\", 39.0], " + //
            " PARAMETER[\"latitude_of_origin\", 0.0], " + //
            " PARAMETER[\"scale_factor\", 1.0], " + //
            " PARAMETER[\"false_easting\", 500000.0]," + // 
            " PARAMETER[\"false_northing\", 0.0], " + //
            " UNIT[\"m\", 1.0], " + //
            " AXIS[\"Easting\", EAST]," + // 
            " AXIS[\"Northing\", NORTH], " + //
            " AUTHORITY[\"EPSG\",\"5257\"]]";
        
        String customDisplay=" PROJCS[\"WGS84 / Google Mercator\", "+//
            " GEOGCS[\"WGS 84\",  "+//
            " DATUM[\"World Geodetic System 1984\", "+// 
            " SPHEROID[\"WGS 84\", 6378137.0, 298.257223563, AUTHORITY[\"EPSG\",\"7030\"]], "+// 
            " AUTHORITY[\"EPSG\",\"6326\"]],  "+//
            " PRIMEM[\"Greenwich\", 0.0, AUTHORITY[\"EPSG\",\"8901\"]], "+// 
            " UNIT[\"degree\", 0.017453292519943295],  "+//
            " AXIS[\"Longitude\", EAST],  "+//
            " AXIS[\"Latitude\", NORTH],  "+//
            " AUTHORITY[\"EPSG\",\"4326\"]],  "+//
            " PROJECTION[\"Mercator_1SP\"],  "+//
            " PARAMETER[\"semi_minor\", 6378137.0], "+// 
            " PARAMETER[\"latitude_of_origin\", 0.0],  "+//
            " PARAMETER[\"central_meridian\", 0.0],  "+//
            " PARAMETER[\"scale_factor\", 1.0],  "+//
            " PARAMETER[\"false_easting\", 0.0],  "+//
            " PARAMETER[\"false_northing\", 0.0],  "+//
            " UNIT[\"m\", 1.0],  "+//
            " AXIS[\"x\", EAST],  "+//
            " AXIS[\"y\", NORTH],  "+//
            " AUTHORITY[\"EPSG\",\"900913\"]] ";


        
        CRSFactory factory = ReferencingFactoryFinder.getCRSFactory(null);
        CoordinateReferenceSystem localCRS = factory.createFromWKT(customLocal);
        CoordinateReferenceSystem displayCRS = factory.createFromWKT(customDisplay);

        MathTransform transform;
        transform = CRS.findMathTransform(localCRS, displayCRS);
        WKTReader fromText = new WKTReader();
        Geometry geom = null;
        if (wktPoint != null) {
        geom = fromText.read(wktPoint);
        geom = JTS.transform(geom, transform);
        }
        return geom;
    } catch (FactoryException | MismatchedDimensionException | TransformException e) {
        throw new RuntimeException("Unknown crs defination was found");
    }catch (ParseException  e) {
        throw new RuntimeException("Not a WKT string:" + wktPoint);
    }
{% endhighlight %}