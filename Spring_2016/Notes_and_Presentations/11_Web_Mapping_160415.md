## Notes - Web Mapping - Part 2 (04/15/2016)

### 1. Open a Mapbox account:
* Sing up [here](https://www.mapbox.com/)

### 2. Blog

### 3. Other CSR Tutorials
* You will find other CSR tutorials [here](https://github.com/mym2107/CSR-Conflict-Urbanism-Aleppo/tree/master/Tutorials). They deal mostly with building webmaps through Mapbox but they also have some HTML and CSS components. Make sure you check them out.

### 3. Overview of Mapbox
* [Mapbox Studio](https://www.mapbox.com/mapbox-studio/):
  * Is a modern design platform for managing your spatial data and creating custom map styles. Use Mapbox Studio to design a map to your exact specifications by using Mapbox-provided tilesets, uploading your own vector or raster data, adding custom fonts and images, or simply refining the built-in template map styles.
  * Browser application.
* [Mapbox Editor](https://www.mapbox.com/editor/#style):
  * Is an online interface where you can choose a Mapbox classic style as a basemap, drag and drop features, and share your project. Editor requires no coding skills and can be easily integrated into a web template. You can import GeoJSON, CSV, KML, or GPX files into Mapbox Editor. You can also export data in GeoJSON or KML format.
  * Browser application.
  * To customize the basemaps you need to use either Mapbox Studio or Mapbox Studio Classic.
* [Mapbox Studio Classic](https://www.mapbox.com/mapbox-studio-classic/#darwin):
  * Is a desktop application for designing world maps. It allows you to design maps by using vector tiles and CartoCSS. Mapbox Studio Classic allows you to upload your map directly to your Mapbox account and then use your map style with our Developer tools.
  * Desktop application.
  * Seems like it's being replaced by Mapbox Studio (web application).
* Styles:
  * 



### 3. Webmapping concepts and tools:
* Tiling:
  * Examples:
	* [Bing Maps Tile System](https://msdn.microsoft.com/en-us/library/bb259689.aspx)
	* [MapTiler](http://www.maptiler.org/google-maps-coordinates-tile-bounds-projection/)
  * At the most zoomed out level (0), the whole world is a tile, and then, as you zoom in, that tile becomes four, and so on.
  * However, some parts of the world don’t have the same resolution as others, and often, webmaps only allow limited zooming in in these parts.
* Projection:
  * Most of the platforms to do mapping online use a modified version of the Mercator projection. However, as we know, that projection has severe problems in terms of depicting areas at a large scale.
  * The two main reasons why they use it is that it works very well at a local (street) level, and it is computationally efficient in terms of zooming in and panning.
* Tools:
  * [CartoDB](https://cartodb.com/gallery/): 'CartoDB is an open source tool that allows for the storage and visualization of geospatial data on the web.' Mostly used to upload and visualize geographic data. However, it has many advanced features. [Open source](https://github.com/CartoDB/cartodb).
  * [Mapbox](https://www.mapbox.com/gallery/): 'Mapbox is a mapping platform for developers.' Mostly used to create base maps (tiles) and then overlay your data on top of them. [Open source](https://github.com/mapbox)
  * [Mapbox Studio](https://www.mapbox.com/mapbox-studio/): 'A modern map design platform.' This is now the platform where you create your *vector* tiles in Mapbox.
  * [TileMill](https://www.mapbox.com/tilemill/): 'TileMill is the design studio to create stunning interactive maps.' **Deprecated** (no longer supported). TileMill is the program created by Mapbox where you used to create your *raster* tiles. It has been replaced by Mapbox Studio.
  * [Leaflet](http://leafletjs.com/): 'An open-source JavaScript library for mobile-friendly interactive maps.' Leaflet is the most popular javascript library to create maps directly on your site (without embeding 'iframes' from CartoDB or Mapbox or others). [Open source](https://github.com/Leaflet/Leaflet)
  * [Mapzen](https://mapzen.com/): 'Mapzen builds open-source mapping tools and collaborates on open geodata initiatives.' Multiple tools, from rendering OSM data tiles, to geocoding search service, to routing.
  * [Google Fusion Tables](https://sites.google.com/site/fusiontablestalks/stories): 'Fusion Tables is an experimental data visualization web application to gather, visualize, and share data tables.' Google tool to visualize and map data using Google Maps as the base layer.
  * [d3](https://d3js.org/): 'a JavaScript library for manipulating documents based on data.' Used for data visualization and for mapping.

### 4. Tutorial