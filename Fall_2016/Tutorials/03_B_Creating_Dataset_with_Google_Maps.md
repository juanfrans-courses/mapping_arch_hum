## Tutorial 03 - Creating a Dataset with Google Maps
*Tutorial created by Emily Fuhrman (ef2512@columbia.edu) for the [Mapping for Architecture, Urbanism and the Humanities](https://github.com/juanfrans-courses/mapping_arch_hum) class at Columbia University*

Google Maps (or Google Earth) is a helpful tool for manually extrapolating the latitude and longitude coordinates for a list of geographic locations. In this tutorial, we will walk through how to generate a KML (or KMZ) file from Google Maps, which you can then import into QGIS. 

### Creating a Dataset of NYC Landmarks with Google Maps
#### Creating a New Map
The first step is to navigate to [Google Maps](https://www.google.com/maps). In the top left corner of the window next to the searchbar, you should see a hamburger menu.

![Start Menu](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/01_Start_Menu.png)

Click the menu to open up a left navigation panel. Select `Your places`.

![Menu Open](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/02_Menu_Open.png)

You should see four categories along the top menu of the panel: `LABELED`, `SAVED`, `VISITED`, and `MAPS`. Select `MAPS` to bring up a list of any maps you have already created and saved. 

![Your Places Maps](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/03_Your_Places_Maps.png)

Navigate to the very bottom of the panel, and select `CREATE MAP`. This should open a new tab in your browser, centered by default on the United States. 

![Create Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/04_Create_Map.png)

The left hand panel in this new view contains a title (currently `Untitled map`) and a layer for saved locations (currently `Untitled layer`). Click on the title to change it to a more sensible designation, if you like. Use the stacked three dots to the right of the `Untitled layer` row if you would like to change the name of the layer. I am going to change the name of `Untitled layer` to `Locations`, and the name of my map to `Sample map`. 

![Rename](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/05_Rename.png)