## Notes - Census and Joining Tables (2/19/2016)

### 1. Tutorial 02 (Recap)
* Download 311 and census block group boundaries
* Open qGIS new map
* Add boroughs layer (to give the right projection to the map)
* Add block group boundaries
* Select by attribute:
  * `"COUNTYFP"  = '005' OR  "COUNTYFP"  = '061' OR  "COUNTYFP"  = '081' OR  "COUNTYFP"  = '047' OR  "COUNTYFP"  = '085'`
  * Export as new layer with the right projection
  * Save only selected features
* Add 311 csv file:
  * WGS 84 projection
* Select by attributes:
  * `"Location" is Null`
  * Invert selection
  * Export as a new layer with the right projection (NAD 1983)
  * Export only selected features
* Points in Polygon
  * Notice the Null vs. 0
  * Two options:
    * Make it the same as the background color
    * Change the null values to 0:
      * Select null values
      * Open field calculator
      * Update field
      * Only selected values
      * Save edits
* Symbolize
  * Natural breaks
  * Add a class with 0 as its value
  * Change colors and stroke
  * Change values (round)
* Finish map
  * Hydropol (definition query)
  * Background
  * Or state
* Print composer:
  * Composition:
    * Presets, export settings
    * [Paper size chart](https://en.wikipedia.org/wiki/Paper_size)
  * Item properties:
    * Grids
* Group layers:
  * Lock layers for map item
* Legend:
  * Auto update
  * Hidden
  * Background
* Export as raster w/ lower resolution if file is too big

### 2. Census tutorial

### Various
* Refining your own dataset (adding attributes and symbolizing)
* Sit down with each group and talk about final project
* [Changing color and size - symbology](http://qgis.spatialthoughts.com/2012/02/styling-vector-data-in-qgis-using-size.html)
* Right-click and zoom to layer