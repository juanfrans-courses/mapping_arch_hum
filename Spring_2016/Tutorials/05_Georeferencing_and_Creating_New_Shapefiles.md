## Tutorial 05 - Georeferencing and Creating New Shapefiles
This tutorial will show you two things: one, how to georeference an image that has no geographic reference, and two, how to, from that image, create a new shapefile with associated data.

Often enough you will encounter raster files of maps or satellite images that don't have a geographic reference. And although you can add them to your map in qGIS, they will come in in the wrong location and at the wrong scale. In these cases, if you want to use these images you will have to georeference them, which means, based on other files with appropriate geographic data, move and scale these images until the fit the right location, the right orientation and the right size.

In addition, once you have georeferenced these images you will probably want to digitize some part of them, creating new vector shapefiles based on these images with associated data.

For more information about georeferencing take a look at this Wikipedia [article](https://en.wikipedia.org/wiki/Georeference).

### Datasets:
For this tutorial we will be georeferencing a map of New York City's bike lane system. You should download the map from [here](https://github.com/juanfrans-courses/mapping_arch_hum/tree/master/Spring_2016/Class_Data/05_Georeferencing).
In addition, we will also be using the following datasets:
* nybb - New York City boroughs. Originally downloaded from [here](http://www.nyc.gov/html/dcp/html/bytes/districts_download_metadata.shtml).
* HYDRO - New York hydrography. Originally downloaded [here](https://data.cityofnewyork.us/Environment/Hydrography/drh3-e2fd).
* hydropol - U.S. Hydrographic features. Originally downloaded from [here](http://www.rita.dot.gov/bts/sites/rita.dot.gov.bts/files/publications/national_transportation_atlas_database/2014/polygon).
* geo_export_03e863aa-c6a6-4ba9-b669-1955cfb51885 - New York City street centerline. Originally downloaded from [here](https://data.cityofnewyork.us/City-Government/NYC-Street-Centerline-CSCL-/exjm-f27b).

**Note:**
The bike lane system map for New York was originally downloaded from [here](http://www.nyc.gov/html/dot/html/bicyclists/bikemaps.shtml). However, the map comes in PDF format, which cannot be added to qGIS. I converted the map into .jpg format, which can be added to qGIS. For your reference, if you have a PDF file that you need to convert to .jpg or .tiff (formats that can be added to qGIS), you can use Preview (Mac), Adobe Acrobat or Photoshop to do this. Just make sure that the file you are producing is high enough resolution that it will be clear enough when you zoom in to digitize it.

### Georeferencing A Map
After you've downloaded the Bike map open up a new qGIS map and add the boroughs file. Remember, the reason why we are adding this file first is to give the map the right projection.

Next, just to see how an un-georeferenced file comes in, click on the `Add Raster Layer` button and add the bike map you downloaded. qGIS will ask you to choose a Coordinate Reference System, but since our image doesn't have one, you should just select the "Generated" one and click `OK`. Now, if you right-click on the image in the Layer Panel and select `Zoom to Layer` you will zoom into the image and be able to see it. However, the image will not match the boroughs in neither its location, nor in its scale.

![Wrong Location](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/01_Wrong_Location.png)

Now, remove that image from your map by right-clicking on the layer and choosing `Remove`. We will add the image through the Georeferencing panel.

To do this, go to `Raster` / `Georeferencer` / `Georeferencer`. This will bring up the Geoferencing window where we will add the image and choose the right anchor points.

In this window, choose `Open Raster` and add your NYC Bike map. Since the map doesn't have any geographic references, choose the 'Generated' coordinate reference system. You will see your map load on the screen.

The process now is to choose specific points on the bike map and match them with specific points on the other layers in our map so that qGIS knows exactly where to place our bike map and its correct size. Right now we only have the boroughs layer but to be more precise in choosing the points we should bring in the street centerline file. Go ahead and add that layer to your map (not to the georeferencing window). Now you should have your main map with the boroughs and the streets and the georeferencing window with your bike map. It should look something like this:

![Layers](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/02_Layers.png)

Now we need to start matching locations on our bike map to locations on the main map based on the boroughs and the streets. The idea is to choose around 5 comparison points, as far apart as possible from each other, that qGIS can then use to warp, scale and position the bike map:

* To do this click on the `Add Point` button on the georeferencing panel.

  ![Add Point](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/03_Add_Point.png)

* Now zoom in to the northern tip of Battery Park city (on the bike map) and place a point right at the north-west corner.
* Once you click there a new window will come up ('Enter map coordinates'). If we knew the coordinates for this point in the real world we could enter them here, but since we don't we will choose a point in the main map.
* To do this click on `From map canvas` and, in the main map, zoom into the same area. Once there, click on exactly the same point but on the main map.
* Once you click on the main map the right coordinates will populate the previous window. Click `OK`.
* You should now see one red point in each map, and the location of the points should be the same. In addition, in the bottom panel of the georeferencing window ('GCP table') you should see a line with the new point and it source and destination coordinates.

  ![Matching Points](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/04_Matching_Points.png)


* Repeat the same process for 4 more points, making sure you choose points that are as far apart as possible from each other.

* Once you have 4 or 5 points matched, click on the `Start Georeferencing` button (Play sign). This will ask you to set an output raster name and bring up the 'Transformation settings' window.
* There, choose a name and a location for your new raster (the geoferenced map we will export) and choose a coordinate reference system. In our case, choose the NAD_1983_StatePlane...
* Also, make sure `Load in QGIS when done` is checked.
* Click `OK` and then click on the `Start Georeferencing` button again to start the process.
* Once the process is done, you can close the Georeferencer window and you should have your georeferenced map as a layer in the main map window (you don't need to save your 'GCP' points).
* To test the location and scale of your map you can place your new bike map layer underneath the streets layer and you should see how, depending on how good of a job you did with your points, your streets align with the streets on the bike map image.

![Streets Aligned](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/05_Streets_Aligned.png)

### Digitizing A New Shapefile
Now that we have the bike lane map georeferenced (at the right location and at the right scale), we can create a new vector shapefile with bike lanes for New York City. We will use the bike lane map to trace the bike lanes and we will give them their proper classification in the attribute table:
* Protected Bicycle Path
* Bicycle Lane
* Shared Lane
* Signed Route

First we need to create a new empty shapefile. To do this go to `Layer` / `Create Layer` / `New Shapefile Layer...`. This will lead you to a menu where you will chose the type of data, the Coordinate Reference System and the attributes. Choose the following settings:
* `Line`
* `EPSG:102718 - NAD_1983_StatePlane...`
* In the 'New attribute' option we will add the attribute fields that this file will have. In our case we only need one type of attribute which will represent the type of bike lane. Select the following settings:
  * Name: 'Type'
  * Type: 'Text data'
  * Width: '80'
* Click on `Add to attributes list` and make sure your new attribute 'Type' is added to the list below.

![New Layer](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/06_New_Layer.png)

* Click `OK` and choose the location to save your new file.
* Your new file should be automatically added to your map.

Now we are ready to start digitizing. We will begin with the 'Protected Bicycle Path' (the green lines).
* To begin the process, highlight your new shapefile in the layer panel and click on the 'Toggle Editing' button (the pencil icon).

![Toggle Editing](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/07_Toggle_Editing.png)

* Next, before we can actually start editing, we should adjust our snapping settings. Snapping will allow us to snap our new features to the street centerline, making our digitizing much more precise. To do this go to `Settings` / `Snapping options`.
* Here, go to 'Snapping mode': Advanced
* Next, check the option to snap to the 'geo_export...' (the street centerline layer).
* Change the mode to 'to vertex' (we want to snap only to the vertices, not to any point in the segment).
* Change the tolerance to 10 and make sure the units are 'map units'.
* These settings are not fixed and depending on what you are doing or how you prefer to edit you can change them. The key though is to get them right for how you want to edit and the types of layers you want to use as reference.
* Once you've set your 'Snapping options' click `OK`.

* Finally, click on the `Add Feature` button, to the right of the `Toggle Editing` one, and you will see your cursor change to a cross-hair icon. Also, as you approach a vertex from the street centerline file you will see a purple '+' appear.
* Now choose a 'green' bike lane and start drawing it by clicking on the vertices of the street centerline file. You will see a red line being drawn.
* Once you finish with one bike lane, right-click anywhere on the map and you will get a menu with the option to type in the attributes for that line you just created.
* In this menu leave the 'id' field 'NULL' (we won't be needing that field) but fill in the 'Type' field with 'Protected Bicycle Path', which is the type of bike lane we are currently digitizing.
* Click `OK` and your new bike lane will be digitized.
* Remember to save your edits often. To do this click on the `Save Layer Edits` button, right next to the `Toggle Edits` (pencil icon).
* If you make a mistake while creating a new feature, you can push the `Delete` (or `Backspace`) button to undo your last click.
* Also, if you want to move any 'nodes' you can click on the `Node Tool` at the right of the `Add Feature` tool and click on the polyline you wish to edit. This will allow you to move the vertices. Or, if you double click on the line with the `Node Tool` you will add a new vertex.

* Using these tools go ahead and digitize multiple bike lanes. Make sure you digitize more than one type, and that in the panel where you input the attributes you give them their corresponding types.
* Remember to save your edits often.
* Also, while editing you can always open the attribute table to see your data and / or to change any attributes.
* Finally, once you are done digitizing multiple bike lanes (of multiple types), click on the `Toggle Edit` (pencil icon) button again to stop editing.
* Then you can change the symbology to match the different types of bike lanes in the city.

Once you are finished with this go ahead and adjust colors, strokes and layer order. And finally, create a print composer, add a legend, title, explanation, source and a scale bar, and export your map as a PDF file. Your final map should look something like this:

![Final Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/08_Final_Map.png)

#### Deliverables
Upload one (PDF) map to Courseworks. The map should be of something different than bike lanes. It could be a historical map or something current, the point is for you to georeference an image and to create a new shapefile based on it. Your map should include proper legend, scale bar, title, explanation and source. Choose colors, line weights and fonts wisely.

