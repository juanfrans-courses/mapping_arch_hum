## Tutorial 01 - Creating a Basic Land Use Map
This tutorial will describe the necessary steps to create a basic land use map of Manhattan and export it as a PDF file in qGIS. If you haven't downloaded the program, you can find it [here](https://www.qgis.org/en/site/forusers/download.html). You can also find it's documentation [here](https://www.qgis.org/en/docs/index.html).

### Datasets:
To create this map, we will be using the following datasets:
* nybb - New York City boroughs. Originally downloaded from [here](http://www.nyc.gov/html/dcp/html/bytes/districts_download_metadata.shtml).
* MNMapPLUTO - Manhattan PLUTO file (version 15v1), containing all the lots in Manhattan and their attributes. The original PLUTO files can be downloaded [here](http://www.nyc.gov/html/dcp/html/bytes/dwn_pluto_mappluto.shtml).
* Roadbed - New York roadbed. Originally downloaded [here](https://data.cityofnewyork.us/City-Government/Roadbed/xgwd-7vhd).
* DOITT_SUBWAY_STATION_01_13SEPT2010 - New York subway stations. Originally downloaded [here](https://data.cityofnewyork.us/Transportation/Subway-Stations/arq3-7z49).
* HYDRO - New York hydrography. Originally downloaded [here](https://data.cityofnewyork.us/Environment/Hydrography/drh3-e2fd).
* hydropol - U.S. Hydrographic features. Originally downloaded from [here](http://www.rita.dot.gov/bts/sites/rita.dot.gov.bts/files/publications/national_transportation_atlas_database/2014/polygon).

### Creating a Basic Land Use Map of Manhattan
First you need to open qGIS and add the layers you downloaded:
* To add *shapefiles* click on the `Add Vector Layer` button. Other types of data will be added using the other buttons, but in this tutorial we will only be using vector data (shapefiles). Other types of data include *rasters*, *csv* (comma separated values), and *postGIS* layers.
![Add Layer](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/01_Creating_a_Basic_Map/01_Adding_Layers.png)
* Make sure you select the files with the extension `.shp`. Remember that a *shapefile* is actually made up of 5 or 6 individual files with different extensions. Normally, these individual files are the following:
  * .shp - The main file that stores the feature geometry (required).
  * .shx - The index file that stores the index of the feature geometry (required).
  * .dbf - The dBASE table that stores the attribute information of features (required).
  * .sbn and .sbx - The files that store the spatial index of features (these might get corrupted, see note at the end of this tutorial).
  * .prj - The file that stores the coordinate system information.
  * For more information on these extensions and others see [this explanation by ESRI](http://webhelp.esri.com/arcgisdesktop/9.2/index.cfm?TopicName=Shapefile_file_extensions).
* Once you've added all the layers you downloaded, you need to organize them in the layer panel. Remember that the layers will be drawn in the same order they appear in the panel: the top layer will be drawn last, on top of the other ones.
* The final order of the layers should be something like this (from top to bottom):
  * DOITT_SUBWAY_STATION_01_13SEPT2010
  * HYDRO
  * ROADBED
  * MNMapPLUTO
  * nybb
  * hydropol
* If when you zoom in to one of the layers some of its features disappear see the note at the end of the tutorial.

As you may have seen, qGIS assigns random colors to each of the layers you add. To change the appearance of each layer do the following:
* First, since we are interested in creating a land use of Manhattan, you should zoom in into this layer. To do this, right-click on the MNMapPLUTO layer and click `Zoom to Layer`.
![Zoom to Layer](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/01_Creating_a_Basic_Map/02_Zoom_To_Layers.png)
* There are multiple ways of changing the appearance of a layer. The easiest (and simplest) is to double-click on the icon (point, line or polygon) next to the layer name on the layer panel. This brings up the `Style` tab in the `Layer Properties` panel. In there you can change the fill (color), stroke weight and fill (outline) and the size of the icon (if using points or icons).
![Style Tab](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/01_Creating_a_Basic_Map/03_Style_Layer_Properties.png)
* In this panel change the style for the following layers in the following ways (we will leave the DOITT_SUBWAY and the MNMapPLUTO for the end):
  * hydropol:
    * Border style: No Pen
    * Fill: #cccccc (HTML notation)
  * nybb:
    * Border style: No Pen
    * Fill: #ffffff (HTML notation)
  * HYDRO:
    * Border style: No Pen
    * Fill: #cccccc (HTML notation)
  * RORADBED:
    * Border style: No Pen
    * Fill: #999999 (HTML notation)
* To change the appearance of the background, select the `Project` menu, and in there select `Project Properties`. Then, in the `General` tab you can change the `Background color` to #ffffff (HTML notation).
![Project Properties](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/01_Creating_a_Basic_Map/04_Project_Properties.png)

Next we need to change the appearance of the MNMapPLUTO layer based on each lot's land use designation. This is called *symbolizing by category*. We will use data stored in the layer's attribute table to assign a symbology (fill and stroke) to each land use category.
* Fist, to get an idea of the data that we will use to symbolize, right-click on the MNMapPLUTO layer and select `Open Attribute Table`. The attribute table has all the data that's associated with each of the features. Each line of data corresponds to one feature in the dataset. As you can see, the MNMapPLUTO layer has a lot of data associated with it.
![MNMapPLUTO Attribute Table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/01_Creating_a_Basic_Map/05_Attribute_Table.png)
* Some of the most useful fields are:
  * ZoneDist1 - The main zoning district classification of the lot.
  * BldgClass - A code describing the major use of structures on the tax lot.
  * LandUse - A code for the tax lot's land use category (this is the one we will use for this map).
  * LotArea - Total area of the lot.
  * BldgArea - Total gross area in square feet.
  * NumBldgs - Number of buildings on the lot.
  * NumFloors - Number of floors in the primary building on the lot (this filed is sometimes used to do a very approximate calculation of the height of the buildings on the lot. You could assume that each floor is 12ft high and multiply the number of floors by 12. Again, this is not an accurate measurement, just a rough approximation).
  * YearBuilt - The year construction of the building was completed.
  * BuiltFAR - The total building floor area divided by the area of the tax lot.
  * You will find a further explanation of all the fields in the [PLUTO Data Dictionary](http://www.nyc.gov/html/dcp/pdf/bytes/pluto_datadictionary.pdf?r=2).

### Notes
* If, after adding some dataset, you zoom in and some of the features disappear, you probably need to rebuild the dataset's "Spatial Index". To do this right-click on the layer, select `Properties` and go to `General`. Under `Coordinate reference system` click on `Create spatial index`. This should solve your problem. Sometimes, specially with the New York City PLUTO files, the "Spatial Index" is tied to one of the attribute fields and when you zoom in only the features with that specific attribute show up. "Spatial Index" are specially useful when doing operations over large datasets, for example see this [post](http://nathanw.net/2013/01/04/using-a-qgis-spatial-index-to-speed-up-your-code/).