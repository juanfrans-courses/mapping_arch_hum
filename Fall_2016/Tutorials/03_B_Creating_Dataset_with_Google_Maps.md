## Tutorial 03 - Creating a Dataset with Google Maps
*Tutorial created by Emily Fuhrman (ef2512@columbia.edu) for the [Mapping for Architecture, Urbanism and the Humanities](https://github.com/juanfrans-courses/mapping_arch_hum) class at Columbia University*

Google Maps (or Google Earth) enables you to easily extract the latitude and longitude coordinates from a list of geographic locations. In this tutorial, we will walk through how to generate a Keyhole Markup Language (KML) file (or its compressed form, a KMZ file) from Google Maps, which you can then import into QGIS. 

KML is an XML format used to represent geographic information in 2-D and 3-D web-based maps. To learn more about KML, check out this [helpful resource](https://developers.google.com/kml/).

### Creating a Dataset of NYC Landmarks with Google Maps
#### Creating a New Map
The first step is to navigate to [Google Maps](https://www.google.com/maps). In the top left corner of the window next to the searchbar, you should see a hamburger menu.

![Start Menu](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/01_Start_Menu.png)

Click the menu to open up a left navigation panel. Select `Your places`.

![Menu Open](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/02_Menu_Open.png)

You should see four categories along the top menu of the panel: `LABELED`, `SAVED`, `VISITED`, and `MAPS`. Select `MAPS` to bring up a list of any maps you have already created and saved. 

![Your Places Maps](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/03_Your_Places_Maps.png)

Navigate to the very bottom of the panel, and select `CREATE MAP`. This should open a new tab in your browser, centered by default on the United States. 

![Create Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/04_Create_Map.png)

The left hand panel in this new view contains a title (currently `Untitled map`) and a layer for saved locations (currently `Untitled layer`). Click on the title to change it to a more sensible designation, if you like. Use the stacked three dots to the right of the `Untitled layer` row if you would like to change the name of the layer. I am going to change the name of `Untitled layer` to `Locations`, and the name of my map to `Sample map`. 

![Rename](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/05_Rename.png)

Begin entering your list of locations into the search bar. Since I intend to map a list of landmarks in New York City, my first location will be `Columbia University`.

![Columbia University](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/06_Columbia.png)

Once Google Map finds the place you enter, an information box should show up above the pin marking its location. Select `+ Add to map` to save the location to the list in the left hand panel. 

![Columbia University Saved](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/07_Columbia_Saved.png)

Continue to enter locations in the search box, each time clicking `+ Add to map` to save the resultant pin to your growing list. I have entered and saved a series of locations in New York City of historic importance (`Columbia University`, `Empire State Building`, `Grand Central Terminal`, `New York Public Library`, and `Statue of Liberty`), for a total of five locations.

![Saved Locations](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/08_Saved_Locations.png)

Your dataset is ready for export. Select the menu to the right of the title of your map, and choose `Export to KML`.

![Export to KML](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/09_Export_to_KML.png)

Select the `Locations` layer that contains your saved list of places, and check the box below that says `Export to a .KML file`. Hit `Download`.

![Confirm](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/10_Confirm.png)

Open up a new project in QGIS, and import your downloaded .KML file as a vector layer. Your points should show up just as they did in the Google Maps interface. 

![Import Into QGIS](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/11_Import_Into_QGIS.png)

If you open up the attribute table of this new layer, you will notice that it does not explicitly include columns for latitude and longitude. We will add those manually. Navigate to the abacus button on the far right of the top menu of icons to open the Field Calculator view. 

![Attribute Table Field Calculator](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/12_Attribute_Table_Open_Field_Calculator.png)

Make sure `Create virtual field` is checked. To add a "Latitude" column, follow these steps:

* Change `Output field name` to "Latitude".
* Change `Output field type` to `Decimal number (real)`.
* Keep `Output field width` at `10`, but change `Precision` to `10` as well.

Open the `Geometry` section of the middle panel, where you can access the built-in variables storing the coordinates of each point.

![New Field](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/13_New_Field.png)

In the middle panel, scroll down to `$y` _(NOTE: **Not** the same as `y` without the dollar sign ($)!)_. Double click on `$y`. Your output preview at the bottom left corner of the expression panel should update to a decimal number. 

![New Field Latitude](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/14_New_Field_Latitude.png)

Click `OK`. A new `Latitude` column should appear on the far right of your attribute table. Repeat these same steps to add a "Longitude" column, only accessing the `$x` value. When finished, your attribute table should look something like this:

![Attribute Table Final](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/03_B_Creating_Dataset_with_Google_Maps/15_Attribute_Table_Final.png)

You may now export your data as a CSV file or a shapefile for further editing.