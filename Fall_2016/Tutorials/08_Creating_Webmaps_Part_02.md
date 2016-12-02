## Tutorial 08 - Creating Webmaps - Part 02
*Tutorial created by Juan Francisco Saldarriaga (jfs2118@columbia.edu) for the [Mapping for Architecture, Urbanism and the Humanities](https://github.com/juanfrans-courses/mapping_arch_hum) class at Columbia University*

This is part 2 of a 2 part tutorial. In this second part you will create web maps (basemaps and standalone maps) using Mapbox.

#### Other Tutorials
You will find other webmapping tutorials [here](https://github.com/mym2107/CSR-Conflict-Urbanism-Aleppo/tree/master/Tutorials). These were prepared for the [Conflict Urbanism: Aleppo class](http://www.c4sr.columbia.edu/conflict-urbanism-aleppo/) and they deal mostly with building webmaps through Mapbox, but they also have some HTML and CSS components. Make sure you check them out.

### Creating a webmap using an existing basemap
This first exercise guides you through the steps for creating a webmap of Green Cab destinations using an existing basemap provided by Mapbox.

#### Datasets
The only dataset we will use in this tutorial is a smaller version of the Green Cab destinations file for June 10th, 2015. The original file contains around 48,000 records but it's too big to upload to Mapbox (Mapbox has a limit of 5MB for any upload). This smaller file includes the first 25,000 records only:
* Green_Trips_150610_Small.csv - You can find this dataset [here](https://github.com/juanfrans-courses/mapping_arch_hum/tree/master/Spring_2016/Class_Data/07_Web_Mapping).

#### Creating a new "Style" in Mapbox
First, we will create a new "Style" in Mapbox and explore the interface a little bit, just to get an idea of how things work here.
* Once you log into your Mapbox account, use the tab on the left-hand side of the page to go to your "Home".
* In your "Home" you will see the different components of your Mapbox account:
  * "Styles": here you will see the maps that you've created. By "styles" Mapbox means both datasets and the styling that has been applied to those datasets.
  * "Tilesets": tilesets are your datasets, which can be either raster or vector datasets. These datasets can also be made up from other types of files (csv, shapefiles, geojson, etc) that have been converted to vector tiles.
  * "Develop": here you will find the developer tools, for when you are building your maps for applications (mobile or web). And you will also find other services like the routing or geocoding APIs.
* To create a new "Style" simply go to the "Style" section and click on `New style`:
  * Here you will see a set of pre-made "styles" as well as an option for creating an empty one.

![Styles Selection](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/11_Styles_Selection.png)

  * Select one of the basic ones and give your new "style" a title.
  * I will select the "Light" one and will name my "style" "Green_Cabs_Destinations".
  * Click `Create`.
* The first thing you will see once your new "style" is created is a map of the world in the center, in the left-hand panel you will get all the layers that make up this "style" and in the upper right-hand corner you will get a menu with your zoom level, your position, an option to see the history of your changes and a debugger.
* Notice how many layers make up this simple map.
* Notice also how many of the layers are repeated, there's one that ends with "labels" and another one without that. This is because in order to create labels in Mapbox you need to add the layer you want to label again, and symbolize it only with the labels. In other words, you add your layer once and style it to get the vectors (points, lines or polygons) and then you add it again and get the labels.
* Also, if you click anywhere on the map you will get a popup window showing the different layers shown in that location:

![Layer Difference](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/12_Layer_Difference.png)

* Now, zoom into New York and you will see other layers appear in the map (streets and labels for example). One of the main things you can do in Mapbox is have some layers only show up at specific zoom levels. That way you will only have the information you really need visible at each moment. If you zoom even more you will see every street label and even building footprints.

![Zoom Levels](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/13_Zoom_Levels.png)

#### Importing your data
In this part of the tutorial we will not modify any of the pre-set layers but we will import our own layer and style it.
* Click on the `+ New layer` button at the top left-hand corner of the page. Once you click here a new sub-panel will open and your map will change. You will now be able to see all your layers without styling. You don't have to do anything with these layers.
* Click where it says `No tileset` next to `Source` and you will be able to select the file that you want to upload. A new sub-panel will open with a list of layers that are already available to you, some of them from Mapbox, others owned by you if you have already uploaded anything.
* Since we are uploading something totally new, click on `New tileset` at the top of that panel and choose `Select a file`. Notice all the formats you can upload files in: MBTiles (Mapbox tiles built with Tilemil), KML (files used by Google Earth), GPX (files produced by some GPS devices), Shapefiles (zipped), CSV or even GeoTIFF (rasters).
* Navigate to the location of your Green_Trips_150610_Small.csv file and select it.
* A word of warning here: CSV files should be under 5MB and should have a column named "latitude" and another one named "longitude" with the geographic information. I have slightly modified the file we used in the previous tutorial to fit the size requirements and the headers. I used the "dropoff_latitude" and the "dropoff_longitude" as the columns for the lat/lon information. For more information see [problems uploading csv files](https://www.mapbox.com/help/troubleshoot-csv/).
* Click `Upload`. This might take a little time. You will see another small panel opening on the bottom right-hand corner that will show the upload progress and then the analyzing progress (you will see a little bar rotating while it's still analyzing your data).
* Once it's done (you will get a little green light) you will see your new data in the "Pick a tileset" panel, below the Mapbox provided layers. Click on your new dataset to add it to your map. You should see a lot of points appear on your map.
* If for some reason you go to another screen you can go to your "Tilesets", select your Green_Trips which if the uploading was successful should be there and click on `Add to style`. Select the "Style" you want to add this layer too. In this case it should be the "Green_Cabs_Destinations" one.

![New Layer](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/14_New_Layer.png)

* In the "New layer" panel you will see your file as the source and the "Type" should be circles.
* Next you should choose at what zoom levels your dataset will be visible:
  * To do this correctly zoom out in your map until a point where you think your dataset should no longer be visible(you can see what zoom level you are at in the small panel at the top right-hand corner of your page).
  * In this case I think the dataset should only appear once you pass zoom level 7.
  * Now zoom in as much as you think you should in your map and determine the maximum zoom level. I think it should be 18.
  * In the panel set your zoom levels to 7 for "min" and 18 for "max" or whatever numbers you think should be there.
  * Now when you zoom in and out past your maximum and minimum settings you will see your points turn gray.
* Finally, if you wanted to only use a subset of your data you could create a filter where it says `+ Add filter`.
* Once you are done with this click on `Create layer`. You will return to normal view and your layer will appear at the top in the left-hand side panel.
* Remember that the order in which the layers are listed determines the order in which they will be drawn. The top layer will be drawn last, so if you want your layer to be on top of everything except the labels you should move your new layer below the one called "Waterway labels":
  * To do this grab your layer from the little "hamburger" icon that appears to its right when you hover over it and drag it to where you want it to be.

![Layer Position](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/15_Layer_Position.png)

#### Style your data
Finally, we can begin really styling our data. You should be in the sub-panel called "Style" with your green-trips-15610-small layer selected.
* First we need to adjust the size (radius) of our points:
  * You could just change the overall size here, for example to 3. However, if you do this and zoom out you will notice that at zoom level 10 your points overlap a lot and everything becomes a mess. Similarly, when you zoom past level 16 your points become too small.
  * So, what you need here is different sizes at different zoom levels. And this is what Mapbox is great at. Instead of just changing the value there, click on the slider to the right of the "Radius" value and a new panel will appear. Click on `Enable editing by zoom level`.
  * Here you can choose a starting value at a specific zoom level and an ending value at another level, and you can choose the rate of change.
  * First of all, zoom out to zoom level 7 to determine the starting value.
  * Adjust the first slider to 7 and then the size to 0.3 px (which seems like a good value for this zoom level).
  * Now zoom in to level 18 to see what seems like a good radius for that level.
  * Adjust the bottom slider to 18 and then the value to 7 px.
  * Now when you zoom in and out you will see the radius changing.
  * However, zoom levels like 9, 10 or 11 it's still a bit too much. So, to change that without changing the start and end values we will adjust the rate of change. Right now it's '1', which means it's linear. Change it to 1.4 and zoom in and out and see how the radius changes.
  * Adjust everything again if you think it's necessary.

![Raidus Values](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/16_Radius.png)

* Now let's change the color. We could also change it depending on the zoom level but that would be a little too much. In this one, just click on the hex number and pick a color for your points.
* If you wanted you could also blur your data or change it's opacity. You could even translate it, that is, offset it by a specific distance. I'm not going to change any of this.

![Styling](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/17_Styling.png)

#### Add labels to your data
The last step is to add labels to your data. In this case, I want to show what was the final fare for each of the taxi trips. To do this, however, we need to duplicate our layer; we need to have one for the points and another one for the labels.
* On your left hand panel, click on `+ New layer` and then click on the `Source` panel. Choose your "Green_Trips_150610_Small" dataset from the list that appears.
* And before you click `Create layer` make sure you select "T Symbol" as the data type.
* You should also choose your zoom levels. Note that these might not be the same as the ones for the points. We don't need to see the labels when we are all the way zoomed out at level 8 or 9. I will set the min zoom level to 15 and the max to 18.
* Once you've set these parameters click `Create layer`.
* In the new panel that opens up, click the "Text field" field and you will see a smaller panel with the different fields associated with the data.
* Scroll down until you see {Total_amount} and select it. You should now see the total amount paid on your map. However, we need to style it to make it look good:
  * First, let's put a $ sign. In the "Text field", before {Total_amount} insert a "$".
  * Next, change the color of the text.
  * Change the font, if you want.
  * And adjust the size of the text. This one you can also do it with a ramp, like we adjusted the size of the radius.
  * You can also change the letter spacing, the line height and the max width.
  * Finally, if you wanted, you could add a "halo" around the text, to make it more easy to read. In this map, I don't think that's necessary.
  * Zoom in and out testing your settings and adjust whatever you think is necessary.

![Text Settings](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/18_Text_Settings.png)

* Now you will notice that the text is actually placed on top of our points. We should change that:
  * In the same panel, click on the `Position` option at the top of the panel.
  * Set the "Text anchor" at the "Left".
  * Finally, offset the text by 0.4 em in the x direction.

![Text Placement](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/19_Text_Placement.png)

* There are other parameters you could change for your text, such as allowing for overlaps or not, or setting up some padding between different texts (both of those in the "Placement" tab) but this should be fine for now.

#### Export your map
Finally, we need to export our map.
* The first thing you should do is click on the `Position` option in the little menu at the top right-hand corner of the page:
  * Here we will set the default position and zoom level for the map, the starting point.
  * Zoom to a good level and center the map on the screen. Then click on `Lock default position` to mark it.

![Map Position](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/20_Map_Position.png)

* Now click on the `Publish` button at the top left-hand corner of the page.
* You can see the changes you've made to the "Style" with the slider. If you are satisfied with your changes click on `Publish` to make your "Style" public.
* Finally, click on `Share and use style` to get the URL or codes to embed your style. Here you have multiple links:
  * URL: This is a standalone URL that you can share. Test it to see how your map looks and reacts.
  * Style URL and Access token: these codes are used when you are building an application or website that uses this style.
  * Use style in other apps: here are the codes to use this style in Tableau, ArcGIS or CartoDB (this is the one we will use in the next part of the tutorial).

![Final Map Mapbox](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/21_Final_Map_Part_01.png)

#### Deliverables
The deliverable for this tutorial is the web version of your sound map or your humanities dataset map. This webmap needs to include the following:
* A 100% custom basemap created in Mapbox.
* This map can use pre-loaded Mapbox layers or custom layers that you upload, but those layers need to be styled by you.
* You should have at leas 3 different layers and some labels in this basemap.
* In addition, you should use CartoDB to add your own data (sound or humanities) on top of this Mapbox map.
* Your submission needs to be two links:
  * Basemap from Mapbox
  * Full map from CartoDB (remember, the CartoDB map needs to be built on top of the Mapbox basemap).
* Finally, be sure to explore different map styles. Look at the blog and look at the examples provided by [Mapbox](https://www.mapbox.com/gallery/) and [CartoDB](https://cartodb.com/gallery/) and be creative with your map.