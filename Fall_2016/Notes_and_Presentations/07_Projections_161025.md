## Notes - Projections (10/25/2016)

### 1. Various
* Go over blog
* Questions about midterm presentation (**Friday 28th**)
* [Inclusive Maps](http://interdisciplinarythings.com/msr/)
* [Visualizing Racial Divide](http://vallandingham.me/racial_divide/)

### 2. Downloading OSM data
* Online resources:
  * [Mapzen Metro Extracts](https://mapzen.com/data/metro-extracts/)
  * [Geofabrik Downloads](http://download.geofabrik.de/)
* Built-in OSM tool:
  * Vector > OpenStreetMap > Download data...
  * Vector > OpenStreetMap > Import Topology from XML...
  * Vector > OpenStreetMap > Export Topology to SpatiaLite...
  * Optional: export as new shapefile
* How to add north arrow (image) and link it to map rotation

### 3. Projections
* Links:
  * [Tissot Indicatrix](https://blogs.esri.com/esri/arcgis/2011/03/24/tissot-s-indicatrix-helps-illustrate-map-projection-distortion/)
  * [d3 projections](http://bl.ocks.org/mbostock/3711652)
  * [Distortion in map projections](http://bl.ocks.org/syntagmatic/ba569633d51ebec6ec6e)
  * [USGS Map Projections](http://egsc.usgs.gov/isb//pubs/MapProjections/projections.html)
  * [Map Projections & What They Say About You](http://brilliantmaps.com/xkcd/)
  * [Gnomic Projection](https://bl.ocks.org/mbostock/3795048)
* Geographic coordinate systems:
  * It's a coordinate system (lat/lon) based on a spheroidal (spherical or ellipsoidal) surface that approximates the surface of the earth.
  * The **datum** defines the surface and the position of the surface relative to the center of the earth.
  * Referencing coordinates to the wrong datum can result in positional errors of 10 to several hundred meters.
  * And, depending on the datum, different transformations are used to project the coordinate system.
  * Common datums:
    * North American Datum 1927 (NAD1927)
    * North American Datum 1983 (NAD1983)
    * World Geodetic System 1984 (WGS84)
* Projections:
  * Transformations that convert the locations of points on a curved surface (datum or reference surface) to locations on a **flat** plane.
  * Distortion and accuracy:
    * Conformal: Local angles and shapes are preserved but not necessarily sizes. (True shapes)
    * Equal-Area: Areas are preserved. (True areas)
    * Equidistant: Distances are preserved. (True distances)
    * Azimuthal: Directions from a single location to other locations are preserved. (True directions)
  * Types of projections:
    * Planar: Earth intersects the plane on a small circle.
    * Cylindrical: A cylinder is wrapped around the Equator.
    * Conic: A cone is wrapped around the earth (ie. the Lambert Conformal Conic projection is commonly used to map North America).
  * Common projections:
    * Azimuthal Equidistant (planar): air route distances, more distortion as you move away from the center point.
    * Cylindrical Equal Area (cylindrical): lat/lon are assigned to the x and y coordinates. Neither conformal nor equal area. Also called the "unprojected projection".
    * Peters (cylindrical): non-Eurocentric, equal area.
    * Mercator (cylindrical): for marine navigation, local angles preserved (Google Maps), highly distorted towards the poles.
    * Albers (conic): preserves areas, good for regions with longer east-west orientation, used by USGS and US Census.
    * Lambert (conic): good for mid-latitudes, used for North America, used in the State Plane system.
* Common coordinate systems:
  * UTM (Universal Transverse Mercator) (cylindrical):
    * Implemented as an international standard (military).
    * Uses 60 zones with a maximum distortion of 0.04%.
    * Each zone defines a different projection and two maps of adjacent zones will not fit along their common border.
    * Jurisdictions (ie. countries) might span two or more zones.
  * State Plane Coordinates.

### 4. Tutorial