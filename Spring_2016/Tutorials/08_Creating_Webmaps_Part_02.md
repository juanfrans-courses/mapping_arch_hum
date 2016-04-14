## Tutorial 08 - Creating Webmaps - Part 02
*Tutorial created by Juan Francisco Saldarriaga (jfs2118@columbia.edu) for the [Mapping for Architecture, Urbanism and the Humanities](https://github.com/juanfrans-courses/mapping_arch_hum) class at Columbia University*

This is part 2 of a 2 part tutorial. In this second part you will create web maps (basemaps and standalone maps) using Mapbox and integrate them with other CartoDB maps.

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
* A word of warning here: CSV files should be under 5MB and should have a column named "latitude" and another one named "longitude" with the geographic information. I have slightly modified the file we used in the previous tutorial to fit the size requirements and the headers. I used the "dropoff_latitude" and the "dropoff_longitude" as the columns for the lat/lon information.
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


1. Create new style using taxi data:
  * Explore the interface
  * Add data
  * Filter it or not
  * Style it
  * Add labels
  * Add custom markers?
  * Export it (publish)

2. Create full new style and add buildings in CartoDB

3. Deliverable:
  * Full basemap
  * Add personal data


* [Problems uploading csv files](https://www.mapbox.com/help/troubleshoot-csv/)
* 2 things I had to do:
  * Change the name of the headers: there needs to be a `latitude` and a `longitude`
  * Reduce the size of the file to under 5MB
  * Takes its time loading

################

In this tutorial we will create maps using two different types of datasets. We will upload a shapefile and two csv files. The idea here is that you learn how these different types of datasets are imported into and visualized in CartoDB.

### Datasets
We will be using three different datasets:
* PLUTO for Manhattan - Originally downloaded from [here](http://www1.nyc.gov/site/planning/data-maps/open-data/dwn-pluto-mappluto.page)
* Trees for Manhattan - Originally downloaded from [here](https://data.cityofnewyork.us/Environment/Street-Tree-Census-Manhattan-/e6n3-m3vc)
* Green taxi trips (6/10/2015) - You can find the dataset [here](https://github.com/juanfrans-courses/mapping_arch_hum/tree/master/Spring_2016/Class_Data/07_Web_Mapping) *Note: this file contains a subset of taxi trips (those for the 10th of June, 2015) of a much larger dataset that can be downloaded [here](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). However, for this tutorial, please use this sample. The whole dataset is too large for the purposes of this tutorial.*

### Creating a building age map of Manhattan
#### Importing and loading your data into CartoDB
* Once you've downloaded the data and created your CartoDB account, longin into CartoDB. You will land on your 'dashboard'.
* Here, click on `NEW MAP`, which will take you to your datasets.
* In there, you need to upload the PLUTO dataset, so click on `Connect dataset`.
* Here, you can browse for your files or you can just drag and drop them. The important thing to keep in mind when uploading shapefiles is that they need to be zipped. Fortunately, when you downloaded the PLUTO dataset from Bytes of the Big Apple it came in zipped, so you already have it in the right format. However, if for some reason you don't have your shapefiles zipped, you need to compress them into a single archive. Remember that shapefiles are actually made up of multiple files (4, 5 or 6 usually), so you need to make sure these are all included in your zip file.
* Interestingly enough, if you uploaded the zip file that was directly downloaded from Bytes of the Big Apple, you actually uploaded two shapefiles: 'mnmappluto' which is the actual PLUTO file for Manhattan, and 'mn_dcp_mappinglot' which is a secondary file that comes with the PLUTO file.
* Once your file is uploaded and processed you will see it in the list of datasets.
* Click on the 'mnmappluto' file to see it's content:

![Table View](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/01_Table_View.png)

* You will see here all your data:
  * First of all, know that CartoDB rearranges your columns alphabetically (except for the first two), so don't worry if they appear in a different order to what you saw in qGIS or in another program.
  * Second, notice that the second column, the one called `the_geom` has a little orange `GEO` tag next to it. This is very important: this means that CartoDB has identified this field as the one that contains the actual geometry and geographic reference for this file. This is what is going to be plotted as the base geometry. When we upload other datasets we will see how to modify this.
  * Third, notice that below the header of each column CartoDB notes the type of data for that column, be it 'string', 'number', 'geometry', etc. If by some reason CartoDB has misclassified any columns you can click on that label and change the type to something else.
  * Finally, scroll all the way to the right of the table until you see a field called `yearbuilt`. This is the field we will use to symbolize our data based on the year the building was built for every lot. Make sure this field is of the type 'number'. If it isn't, change it to 'number'.
* Once you've checked your data, click on the `MAP VIEW` button at the top of the page. You will be taken to a map view and you will be able to see your data:

![Map View](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/02_Map_View.png)

* You can pan around and zoom in and out of your map. And if you click on a lot you will get a popup window but it won't have any information because we haven't set that yet.

#### Symbolizing your map
* On the right hand side of your map you will see a series of tabs:
  * The first one, with a '+' sign, allows you to add another dataset to the same map.
  * The second one, the one that has the '1', allows you to choose one dataset when you have multiple in your map. Since we only have one, that's the only one you can choose. If we had multiple you would see a '2', a '3', etc.
  * The third one, the one that says 'SQL', allows you to filter your data using 'SQL' language. For example, you could write something like this `SELECT * FROM mnmappluto WHERE yearbuilt > 1990` to show only the lots where buildings where built after 1990. Try a couple of commands here. SQL is a fairly easy language but it's also very powerful. There are many tutorials out there, [here](https://www.codecademy.com/learn/learn-sql) is one from Codecademy.
  * Clear your query by clicking `Clear view` from the bottom of the SQL panel.
  * The next tab, the one that has a little paint brush, is where you will find all the basic symbolization options. We will return to this one in soon.
  * The following one, the one that has a little popup, is the `Infowindow` tab, where you will choose what fields will appear in the popup that comes up when you click on a feature.
  * The tab that says 'CSS' is the one where you can manually symbolize your data using a variation of CSS called 'CartoCSS'.
  * Then there's the legends tab where, clearly, you can customize your map's legend.
  * And finally, there's the filters layer where you can filter your data in an interactive way based on histograms, although it's not as precise as working in SQL. If you create any filters, make sure you clear them.
* So, to symbolize your dataset based on the `yearbuilt` field, go to the `wizards` tab (the one with the paint brush).
* Here, select cloropleth. I encourage you to explore the other symbology methods. Some of them could be interesting for this dataset but others will not work that well.
* In the column option select `yearbuilt`.
* 7 buckets is fine.
* And change the `Quantification` to `Jenks`.
* You should change your color ramp. If you want to use divergent color ramps that's fine, but know that those types of color ramps are usually used for values that diverge and building age is not really that kind of value.
* You can also change the transparency of your colors, the stroke, the stroke weight and the transparency of the stroke.
* Finally, you could choose a `Composite operation`, which is basically how your layer's color or brightness would interact with the color or brightness of the layer below; and you could also add some `Label Text` but that will not be necessary for this map.

![Symbology](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/03_Symbology.png)

* Now click on the `Infowindow` tab.
* Here, turn on the `yearbuilt`. You will see now that when you click on a lot the popup window will contain the `yearbuilt` data.
* Now click on the `CartoCSS` tab. Here, we will fine tune our symbology to make our breaks cleaner.
* This is my CartoCSS code (note that your colors might be different and feel free to choose your own breaks):
```
/** choropleth visualization */

#mnmappluto{
  polygon-fill: #005824;
  polygon-opacity: 1;
  line-color: #000000;
  line-width: 0.1;
  line-opacity: 0.5;
}
#mnmappluto [ yearbuilt <= 2040] {
   polygon-fill: #EDF8FB;
}
#mnmappluto [ yearbuilt <= 1990] {
   polygon-fill: #D7FAF4;
}
#mnmappluto [ yearbuilt <= 1960] {
   polygon-fill: #CCECE6;
}
#mnmappluto [ yearbuilt <= 1935] {
   polygon-fill: #66C2A4;
}
#mnmappluto [ yearbuilt <= 1910] {
   polygon-fill: #41AE76;
}
#mnmappluto [ yearbuilt <= 1900] {
   polygon-fill: #238B45;
}
#mnmappluto [ yearbuilt <= 1800] {
   polygon-fill: #005824;
}
```
* The colors are actually in HEX form. If you want different HEX codes you can always go to [Adobe Kuler](https://color.adobe.com/) or to [ColorBrewer](http://colorbrewer2.org/) and pick colors from there.
* Remember once you've changed the CartoCSS to click on `Apply style`.
* Finally, click on the `Legend` tab to customize the legend of your map.
* Add a title to your legend and, if necessary, change the labels and the colors.
* Once all of this is done, click on the `Basemap` dropdown menu at the top left-hand corner of the map and choose a basemap that you like. However, note that certain basemaps work only at specific zoom levels, so choose one that allows you to zoom to a good level without loosing resolution.
* Also note that there's an option to add your own basemaps (the `+` sign at the bottom of the menu). This is where we will add the basemaps that we will design with Mapbox.
* Now, for the final stage click on the `Visualize` button at the top right-hand corner of the page, and then click on `OK, CREATE MAP` to create your map.

![After Symbology](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/04_After_Symbology.png)

#### Final customization of your map
* Once you've `Visualized` your map you can do the final customization.
* With the `Add Element` drop down menu, add a title, explanation and source to your map.
* And with the `Options` button at the bottom of the page customize the elements that you want to show in your map, such as `Search box`, `Share options`, etc.
* Once you are done with this, click on `PUBLISH` at the top right-hand corner of the page to get the different sharing options:
  * `Get the link` will give you the link to the map in CartoDB.
  * `Embed it` will give you the code to create an `iframe` and embed your map in a website.
  * `CartoDB.js` will give you the link to the 'json' files that you can use in your applications or website.
* For this tutorial you will only need the basic CartoDB link.
* Here's how my final map looks using the link:

![Final Map 01](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/05_Final_Map_01.png)

### Creating a map of healthy street trees in Manhattan
Now we are going to use a different dataset to create a street tree map of Manhattan. This map should be pretty straight forward now that you know the basic workings of CartoDB.
#### Importing and exploring the data
* First, import your tree dataset.
* As opposed to the PLUTO dataset we used in the previous map, this dataset is a csv file, not a shapefile. However, CartoDB automatically identifies the field containing geographic coordinates and uses that to create the map.
* If after uploading the file CartoDB takes you directly to the map, go back to the dataset view, using the `DATA VIEW` button at the top of the page, just to take a look at the fields in your dataset.
* First will symbolize the trees by their condition. If you move to the right of the table you will see a field called `treecondit`, this is the one we will use.
* Later, for our final tree map, we will sybolize them by density of healthy trees.
* Return to the `MAP VIEW`.

#### Symbolizing
* First, go to the `Wizards` tab and choose the `CATEGORY` symbology.
* Choose `treecondit` as the column to symbolize.
* Notice how most of the street trees are in the '1', '2' or '3' categories. Most of them are in good health. However, just to check this go to the `Filters` tab.
* Here, you will see a small histogram of the data. Choose `treecondit` as the column to analyze.
* Notice how the histogram confirms what we were seeing in the map: the categories with the most trees are '1', '2' and '3'; after that the other categories don't have that many trees.

![Histogram](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/06_Histogram.png)

* Now, since we are building a density map of healthy trees in Manhattan, we should get rid of the trees that are not that healthy. To do this clear any filters in the `filters` tab and go to the `SQL` tab.
* We need to write a SQL query saying something like "From all the trees, select only the ones that have a tree condition of '1' '2' or '3'". In SQL this looks like this: `SELECT * FROM manhattantree_1 WHERE treecondit = '1' or treecondit = '2' or treecondit = '3'`.
* Write that query, hit `Apply query` and you should see your map filter the 'unhealthy' trees out.
* Now we can create a density map just using the healthy trees.
* In the `wizards` tab, select the `DENSITY` option (the last one on the right).
* You will see your layer change to hexagons colored by how many trees are in each cell.
* This is a neat visualization, however, there is no way to choose different classification methods (such as 'Jenks', 'Quantiles', etc). So we will need to go into the actual CSS to modify the cutoff values.
* First, change your `Buckets` to 7 and, if you want, reduce your polygon size to 10.
* Also, choose your color ramp.
* Now, go to the `CSS` tab.
* Here, you can change the cutoff values in a much more precise way.
* After a couple of tries I settled on this classification
```
/** density visualization */

#manhattantree_1{
  polygon-fill: #005824;
  polygon-opacity: 0.7;
  line-color: #FFFFFF;
  line-width: 0.25;
  line-opacity: 1;
}
#manhattantree_1{
  [points_density <= 0.0507169782056104] { polygon-fill: #005824;  }
  [points_density <= 0.02] { polygon-fill: #238B45;  }
  [points_density <= 0.015] { polygon-fill: #41AE76;  }
  [points_density <= 0.01] { polygon-fill: #66C2A4;  }
  [points_density <= 0.0075] { polygon-fill: #CCECE6;  }
  [points_density <= 0.005] { polygon-fill: #D7FAF4;  }
  [points_density <= 0.0025] { polygon-fill: #EDF8FB;  }

}
```
* Feel free to experiment with different classifications but note that if you go back to the `wizards` tab and change the number of buckets or the color ramp, or anything else for that matter, your classification modifications will be lost.
* Also, note that in the `CSS` tab you can also modify your polygon fill, it's opacity, the line color, the line width and the line opacity, so once you've chosen your symbology you can actually do all of the other changes in the `CSS` tab.

![CSS](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/07_CSS.png)

* Finish this part by making sure your legend has the right information.

#### Final touches
* Just as in the previous map, choose your basemap, your options, add a title and an explanation and `PUBLISH` your map once it's done.
* Your final map should look something like this:

![Final Map 02](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/08_Final_Map_02.png)

* One last thing to take into account when using the density symbology: you will notice that if you zoom in or out your symbology changes. One of the things that happens is that when you change the zoom level your cell size increases or decreases, so the cutoff values that you selected do not fit anymore to the shape of the data. This is a problem for these types of maps. You could eventually code the specific cutoff values for every zoom level, but that's a more advanced feature.

### Building an animated map of green taxi trips
The last part of this tutorial involves building an animated map of green taxi pickups in the city. The two new things we will see here is how to assign and change the geometry field and how to create an animated symbology using the `Torque` and `Heatmap` tools.
#### Importing and loading the file
* As with the previous datasets, add your Green_Trips_150610.csv file to your CartoDB account and go to the `DATA VIEW` of that new dataset.
* When you first get to the `DATA VIEW` you will notice that the `the_geom` field contains only 'null' values. That's because CartoDB doesn't recognize any of the fields in this dataset as containing geographic data it can use to geocode the data. For this reason we need to assign the specific fields.
* There are multiple ways of doing this but they all basically lead to the same place. You can click on the `MAP VIEW` button at the top of the page or click on the orange `GEO` tag next to the `the_geom` header. You will end in a page that lets you choose the columns that you want to use to geocode your data. If your data already has a geographic reference and you want to change it, you can also click on the `GEO` tag and change the geographic fields.
* We want to visualize taxi trips by their pickup location, so choose `pickup_longitude` and `pickup_latitude` as the columns to use to geocode the data.
* If you had address data, here's the place where you would also choose those columns to geocode. However, note that geocoding based on addresses has a cost. Initially, you have something like 100 credits but once you run out of those credits you need to pay.
* Once you've chosen the right columns click `Continue`.
* If you chose `MAP VIEW` instead of clicking on the `GEO` tag and you ended up in the map, click on the `DATA VIEW`, just to make sure `the_geom` column is filled now with actual coordinates. Once you've verified this you can go back to `MAP VIEW`.
* In the `MAP VIEW` you will notice that there are some points in the middle of the Atlantic and some points near New York. Don't worry about the points in the Atlantic, those are just GPS errors. Zoom into New York to see your data:

![Green Trips](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/09_Green_Trips.png)

#### Creating the animated map
* Creating an animated map in CartoDB is extremely easy. First, go the `wizards` tab.
* Here, choose the `TORQUE` tool and you will see animation right away.
* Change the `Time Column` to the pickup time (`lpep_pickup_datetime`).
* You should experiment with the other settings so you understand what each of them do. [Here](http://docs.cartodb.com/cartodb-editor/maps/#torque) you will find the documentation for the `Torque` tool.
* Animating the individual points is interesting but we want to animate the density of pickups. To do this choose the `HEATMAP` tool. [Here](http://docs.cartodb.com/cartodb-editor/maps/#heatmap) is the documentation.
* And to animate the heatmap turn on the `Animated` option.
* Again, change the `Time Column` to the pickup time field.
* And play around with the settings until you get something that works for you.

![Animation](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/07_Web_Mapping/10_Animation.png)

* Finally, do all the final changes to the map: choose a basemap, add titles and explanations, and get your link. You can see my final map [here](https://jfs2118.cartodb.com/viz/a2b08ec0-fd0f-11e5-889f-0ea31932ec1d/public_map)