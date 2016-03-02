## Tutorial 04 - Working with Projections
The WGS84 Geographic Coordinate System is the default projection in QGIS. 

### Datasets
This tutorial will incorporate two datasets, one provided by Natural Earth and one provided by the U.S. Census. First, download the current administrative boundaries of the U.S., listed below:
* ne_10m_admin_1_states_provinces (Admin 1 – States, Provinces) - Internal administrative boundaries. Originally downloaded [here](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-admin-0-countries/).

### Datum, Projection, CRS
#### Datum
A datum defines the surface to which a given set of lat/lon coordinates is referenced, as well as the position of that surface in relation to the center of the earth. Examples include NAD83 (which we encountered in previous tutorials that used the NAD_1983_StatePlane_New_York_Long_Island_FIPS_3104_Feet projection), WGS84, and NAD27. For more concrete evidence of this, open up the QGIS `Project` menu, select `Project Properties`, and navigate to the `CRS` section. If you search for `NAD83`, QGIS will generate a long list of different projections referenced to the NAD83 datum. 

![Layer Projection Metadata](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/01_NAD83_Projections.png)

Two datasets that were originally referenced to different datums, but which are then rendered in the same projection, will not line up.
#### Projection
A projection, or Coordinate Reference System (CRS), is used to describe geographic data. A projection is the set of transformations that converts a series of geographic coordinates, which are locations on a curved surface (the datum), into locations on a flat surface.

#### A note re: QGIS 'on the fly' CRS Transformation
*_The layer you currently have selected when you check or un-check this option impacts its effect._*
* Typically, when you _un-check_ `Enable 'on the fly' CRS Transformation`, you must have the _transformed_ layer highlighted in the left layer panel to undo its automatic re-projection.
* Likewise, if you _check_ `Enable 'on the fly' CRS Transformation`, you must typically have the layer with the projection you _want to match_ highlighted in the left panel.  

### Creating a thematic population map of the U.S.
#### Downloading Census state population data
The Natural Earth state boundaries will serve as the 'empty' geography files for this project. As in Tutorial 03, we need to decide on the units of measurement we plan to use before opening a new QGIS project. For this tutorial, we will be visualizing population count normalized by area for each state.

To download the data for this project, we will be returning again to the [American Fact Finder](http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml) data portal. Click the `Advanced Search` option. Here we will select the following parameters for the `Topics` and `Geographies` levels:

* Geography: All States within United States and Puerto Rico
* Dataset: 2015 Population Estimates
* Topic: Population Total

On the left side of the `Advanced Search` window, and open up the `Topics` tab. Click the `Dataset` section, and select `2015 Population Estimates`. 

![U.S. Census Data 2015 Population Estimates](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/02_Dataset_2015_Population_Estimates.png)

Next, open up the `Geographies` tab, and select `State - 040` from the dropdown menu. Select `All States within United States and Puerto Rico` from the window that pops up below, then click `ADD TO YOUR SELECTIONS`.

![U.S. Census Data state geography](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/03_Geography_US_States.png)

Finally, open up the `Topics` tab again. Click on the `People` section, open `Basic Count/Estimate`, and select `Population Total`. One dataset should remain in the search results window, entitled "Annual Estimates of the Resident Population: April 1, 2010 to July 1, 2015."

![U.S. Census Data state geography](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/04_Population_Estimates_Table.png)

Click the link to navigate to the table. It should include a column listing the full name of every U.S. state, as well as subsequent columns containing population estimates for 2010, 2011, 2012, 2013, 2014, and 2015. To download the data in CSV format, click the `Download` button in the `Actions` bar. 

![U.S. Census Data state geography](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/05_Population_Estimates_Table_Full.png)

Click `OK` when prompted to download the data, and then click the `Download` button once the popup window says the file is complete. The downloaded file will be named `PEP_2015_PEPANNRES`.

#### Transforming Census state population data
We will be using [FIPS region codes](https://en.wikipedia.org/wiki/List_of_FIPS_region_codes_(S%E2%80%93U)#US:_United_States) to join the Natural Earth vector boundaries with the Census population data. 

#### Re-projecting selected features from the Natural Earth dataset
* Open up a new project in QGIS and add the Natural Earth states and provinces data. The data is referenced to the WGS84 datum, which we can see by navigating to the `Metadata` section under `Layer Properties`. The definition for the layer's projection is under `Layer Spatial Reference System`.

![Layer Projection Metadata](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/01_Layer_Projection_Metadata.png)

* Since we are creating a map of the United States, the next step is to select all states and provinces that fall within U.S. administrative boundaries. Open up the attribute table for the states and provinces layer, click the `Select features using an expression` option, and build a query to select all features for which the `admin` value is equal to `United States of America`.

![Select U.S. States](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/02_Select_US.png)

* Hit `Select` and close the query builder. Navigating back to the map, only the U.S. should be selected.

![Select U.S. States](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/03_Selected_US.png)

* Now, we want to re-project the United States to the Albers equal-area conic projection. The Albers projection is a popular choice for thematic maps of the U.S. Right-click the states and provinces layer, choose `Save As...`, choose `ESRI Shapefile`, and select `North_America_Albers_Equal_Area_Conic (ESPG:102008)` as the CRS. You may have to search for the specific projection by clicking on the small square icon next to the `CRS` dropdown menu.

![Select U.S. States](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/04_CRS_Albers.png)

* Name the file `US_States_Albers`. Make sure to check the `Save only selected features` option, and hit `OK`.
* When added to your current project, the new layer will be automatically re-projected to the default WGS84 projection. Opening up the properties of `US_States_Albers` and navigating again to the `Metadata` panel, we can see that the `Layer Spatial Reference System` is _not_ WGS84, but the projection we selected in the previous step. It has been re-projected by QGIS to match the projection of the base layer.

![Select U.S. States](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/05_Check_US_Metadata.png)

* To prevent QGIS from automatically re-projecting the new layer to the current project CRS, select the `Project` dropdown in the top menu, select `Project Properties`, and _un-check_ `Enable 'on-the-fly' CRS transformation`. Now, select the `US_States_Albers` layer, right-click, and select `Zoom to Layer`. The features that fall within the administrative boundaries of the U.S. will have been re-projected to the Albers projection.

![Select U.S. States](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/06_Check_US_Albers.png)

#### Joining
Earlier in the tutorial, we transformed the Census population data in Excel to prepare it to be joined to the Natural Earth vector boundaries. 

#### Additional notes
[Here](https://medium.com/@joshuatauberer/how-that-map-you-saw-on-538-under-represents-minorities-by-half-and-other-reasons-to-consider-a-4a98f89cbbb1#.ih16rv26m) is an excellent piece on why this method of visualization can be misleading.




