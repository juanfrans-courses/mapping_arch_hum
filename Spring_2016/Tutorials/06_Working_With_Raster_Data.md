## Tutorial 06 - Working With Raster Data
This tutorial will show you how to work with raster data in qGIS. We will do two things: first, we will download a raster dataset with the population of the world and we will extract information from it; second, we will download satellite images from Landsat, combine them to form true and false color composites, and analyze them to also extract information from them.

### Gridded Population of the World
The 'Gridded Population of the World' dataset is a project by the Columbia University Center for International Earth Science Information Network (CIESIN) in collaboration with the Centro Internacional de Agricultura Tropical (CIAT). It aggregates data from census surveys all over the world into a single raster file, which has been divided into grids of 1km x 1km. This makes it probably the most comprehensive population dataset in the world. However, this dataset is only produced every ten years. You can find more information about it [here](http://sedac.ciesin.columbia.edu/data/collection/gpw-v3).

We will use this dataset to extract population data of the world and create a map displaying the most densely populated areas of the world.

#### Datasets:
* You will find the latest version of the 'Gridded Population of the World', (GPW, v4) [here](http://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-count/data-download). However, you will need to create an account in order to download the dataset. Once you've created an account and logged in, go to the 'Data Download' tab and download the dataset for 2010. It is a pretty big dataset so it will take a while to download.
* In addition to that dataset we will also use a world shapefile from Natural Earth. You can download the 'Admin 0 - Countries' dataset from [here](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/)

#### Loading the Datasets:
* First, of course, open a new qGIS map and add your countries shapefile.
* Next, add the GPW raster file. The one you need to choose is the one with the .tif extension. Remember that to add a raster you need to click on the `Add Raster Layer` button.
* You will see that the raster appears in black and white, with the population centers in white:

![Raster Population](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/01_Raster_Population.png)

#### Symbolizing a Raster Dataset:
* The symbology for a raster dataset works differently than the symbology for a vector file. The raster doesn't have multiple fields; only one value is associated with each pixel in the raster dataset.
* If you click on the `Identify Features` button (the one with the 'i' icon) and you click anywhere on the raster you will see the value associated with that specific pixel. The value will appear as the value for 'Band 1'.

![Identify Results](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/02_Identify_Results.png)

* In this case, the value for that pixel I clicked (in the middle of the US) is 9.2, and since we are looking at a population dataset we can say that in that pixel representing 1km x 1km there are 9.2 people.
* Now, go to the properties of the raster and go to the `Style` tab. You will see that it is different than the symbology for a normal vector dataset.

![Symbology](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/03_Symbology.png)

* Here you will see that the default style is of a 'Singleband gray', which means that it's only symbolizing in grayscale based on one band (rasters can be made up of multiple bands, as we will see in the second part of this tutorial).
* The color gradient is 'Black to white' but that can be switched to 'White to black'.
* And it is symbolizing based on the minimum value, in this case '0' and on the maximum value, '281.706'.
* Now, that's not actually the maximum value of the raster dataset. If you look at the right-hand panel ('Load min/max' values), which is where the min and max values come from, you will notice that the min/max values are being calculated based on a 'Cumulative count cut', which is used to get rid of the outliers. The 'Cumulative count cut' means that qGIS is only taking into account the values between 2% and 98%, in the default cases.
* You could change that and use the option 'Min / max' to use the actual minimum and maximum values. If you choose this one, you have to click on the `Load` button, to load the values. Do this and click on `Apply` to see how the image changes. Now the minimum is still '0' but the maximum is '140853'. Because of this new maximum value, most of the image appears black.
* Another way to get the value is to use the 'Mean +/- standard deviation x' option, which will calculate the minimum and maximum values based on the mean and the standard deviation. Try that one, changing the factor too. Remember to press the `Load` button every time you change this.
* Now change the 'Render type' to 'Singleband pseudocolor' to get something similar to a symbology we would do for a vector file.
* On the right-hand panel you will see the 'Mode' of classification ('Continuous' or 'Equal Interval') and below, again, the 'Load min/max values' panel.
* Click on the `Classify` button to load the values and then hit `OK` to see it on the map.
* Now you can see clearly the regions of the world with the highest population density.

![GPW Symbolized](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/04_GPW_Symbolized.png)

#### Extracting Information from Raster
Finally, if we want to extract information from the raster file we can do it in two ways: one, by creating a new raster with the selected data; or two, by sampling the raster with points or polygons. In this case, sampling means using points or polygons to extract information from the raster file based on their location. In this tutorial we will do both.

##### Raster Calculator Tool
* Let's say we want to extract those areas of the dataset that have more than 100 inhabitants. To do this we will use the raster calculator and 'reclassify' the raster so that the pixels with more than 100 people get a value of '1' and the rest get a value of '0'.
* On your map go to `Raster` / `Raster Calculator`.
* Here, you will see the raster we are using in the 'Raster bands' panel and below, where it says 'Raster calculator expression' we will write the expression to select the data. Let's do this first.
* Double-click on the raster. It should automatically go to the 'Raster calculator expression'.
* After the raster, write '> 100'. The full expression should look like this: `"gpw-v4-population-count_2010@1" > 100`
* Next, select the 'Output layer', the new file where you will save this new data.
* The format should stay as a GeoTiff.
* And finally, let's change the resolution. If you leave it as it is you might have problems with the raster and it will create a huge file (more than 3GBs). So change it to half of the current size: 21,600 x 8,700.
* Make sure the 'Add results to project' option is checked.
* Click `OK`.

![Raster Calculator](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/05_Raster_Calculator.png)

* After the calculation you should get a new raster that has the densely populated places in white and the rest in black.
* However, to better symbolize this let's go to the properties of the new raster.
* First, in the 'Style' tab, change the color gradient to 'White to black' instead of 'Black to white'
* And second, in the 'Transparency' tab, in the 'No data value' panel, in the 'Additional no data value' add the number '0' so that qGIS treats '0' as no values and makes it transparent.
* Click `OK`.
* Now you should see the areas with more than 100 people as black pixels and the rest should be transparent.
* If turn off the other layer your map should look something like this:

![Selected Areas](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/06_Selected_Areas.png)

A couple of things here before we move further:
* One, if you compare the new raster with the original one you will notice that in the new one the pixels are much larger than in the old one. This is because when we exported the new raster we changed the number of rows and columns. The problem with this is that it makes the new raster less detailed than the old one. However, it also makes the file size smaller.
* Two, we could have just changed the symbology of the original layer to create the same effect. In this case we would have just manually created two symbols (with the '+' and '-' buttons), one going up to 99.99999, in white, and the other starting at 100 in black. Here is how that symbology option would look like:

![Manual Symbology](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/07_Manual_Symbology.png)



We will actually re-project this dataset to display it in a projection that's more suitable for a world map.
* 

1. Download Landsat data:
* USGS
* Libra development
* Explanation of different bands

2. Adding Raster data to qGIS
* Combining to create a true color composite
* Combining to create a false color composite:
  * Different combinations
  * Pansharpening

3. Extracting data from color composites

4. GWP
* Extract data from this image

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
* Change the tolerance to 10 and make sure the units are 'map units'. This means that our snapping will have a tolerance of 10ft (our map units are feet).
* These settings are not fixed and depending on what you are doing or how you prefer to edit you can change them. The key though is to get them right for how you want to edit and the types of layers you want to use as reference.
* Once you've set your 'Snapping options' click `OK`.

![Snapping Options](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/09_Snapping_Options.png)

* Finally, click on the `Add Feature` button, to the right of the `Toggle Editing` one, and you will see your cursor change to a cross-hair icon. Also, as you approach a vertex from the street centerline file you will see a purple '+' appear, that means that your line will snap to that vertex.
* Now choose a 'green' bike lane in the bike lane map and start tracing it by clicking on the vertices of the street centerline file. You will see a red line being drawn.
* Once you finish with one bike lane, right-click anywhere on the map and you will get a menu with the option to type in the attributes for that line you just created.
* In this menu leave the 'id' field as 'NULL' (we won't be needing that field) but fill in the 'Type' field with 'Protected Bicycle Path', which is the type of bike lane we are currently digitizing.
* Click `OK` and your new bike lane will be digitized.

* Remember to save your edits often. To do this click on the `Save Layer Edits` button (disk with pencil icon), right next to the `Toggle Edits` (pencil icon).
* If you make a mistake while creating a new feature, you can push the `Delete` (or `Backspace`) button to undo your last click.
* Also, if you want to move or delete any 'nodes' after you've digitized a segment you can click on the `Node Tool` at the right of the `Add Feature` tool and click on the polyline you wish to edit. This will allow you to move or delete the vertices. Or, if you double click on the line with the `Node Tool` you will add a new vertex.
* Editing a polyline with the `Node Tool` will look like this:

![Editing Nodes](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/10_Editing_Nodes.png)

* Using these tools go ahead and digitize multiple bike lanes. Make sure you digitize more than one type, and that in the panel where you input the attributes you give them their corresponding types.
* Remember to save your edits often.
* Also, while editing you can always open the attribute table to see your data and/or to change any attributes.
* Finally, once you are done digitizing multiple bike lanes (of multiple types), click on the `Toggle Edit` (pencil icon) button again to stop editing. While you are editing, your lines will have little red 'x' marks on their vertices. Once you stop editing these marks will disappear.
* Then you can change the symbology to match the different types of bike lanes in the city (based on the bike lane map).

Once you are finished with this go ahead and adjust colors, strokes and layer order. And finally, create a print composer, add a legend, title, explanation, source and a scale bar, and export your map as a PDF file. Your final map should look something like this:

![Final Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/05_Georeferencing/08_Final_Map.png)

#### Deliverables
Upload one (PDF) map to Courseworks. The map should be of something different than bike lanes. It could be a historical map or something current, the point is for you to georeference an image and to create a new shapefile based on it. Your map should include proper legend, scale bar, title, explanation and source. Choose colors, line weights and fonts wisely.

