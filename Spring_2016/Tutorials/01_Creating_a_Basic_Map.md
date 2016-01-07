## Tutorial 01 - Creating a Basic Land Use Map
This tutorial will describe the necessary steps to create a basic land use map of Manhattan and export it as a PDF file in qGIS. If you haven't downloaded the program, you can find it [here](https://www.qgis.org/en/site/forusers/download.html). You can also find it's documentation [here](https://www.qgis.org/en/docs/index.html).

### Datasets:
To create this map, we will be using the following datasets:
* nybb - New York City boroughs. Originally downloaded from [here](http://www.nyc.gov/html/dcp/html/bytes/districts_download_metadata.shtml).
* MNMapPLUTO - Manhattan PLUTO file (version 15v1), containing all the lots in Manhattan and their attributes. The original PLUTO files can be downloaded [here](http://www.nyc.gov/html/dcp/html/bytes/dwn_pluto_mappluto.shtml).
* Roadbed - New York roadbed. Originally downloaded [here](https://data.cityofnewyork.us/City-Government/Roadbed/xgwd-7vhd).
* DOITT_SUBWAY_STATION_01_13SEPT2010 - New York subway stations. Originally downloaded [here](https://data.cityofnewyork.us/Transportation/Subway-Stations/arq3-7z49).
* HYDRO - New York hydrography. Originally downloaded [here](https://data.cityofnewyork.us/Environment/Hydrography/drh3-e2fd).
* hydropol - U.S. Hydrographic features. Originally downloadde from [here](http://www.rita.dot.gov/bts/sites/rita.dot.gov.bts/files/publications/national_transportation_atlas_database/2014/polygon).

### Creating a Basic Land Use Map of Manhattan
#### Open qGIS and add all the layers that you downloaded:
* To add *shapefiles* click on the `Add Vector Layer` button

### Notes
* If, after adding some dataset, you zoom in and some of the features disappear, you probably need to rebuild the dataset's "Spatial Index". To do this right-click on the layer, select `Properties` and go to `General`. Under `Coordinate reference system` click on `Create spatial index`. This should solve your problem. Sometimes, specially with the New York City PLUTO files, the "Spatial Index" is tied to one of the attribute fields and when you zoom in only the features with that specific attribute show up. "Spatial Index" are specially useful when doing operations over large datasets, for example see this [post](http://nathanw.net/2013/01/04/using-a-qgis-spatial-index-to-speed-up-your-code/).