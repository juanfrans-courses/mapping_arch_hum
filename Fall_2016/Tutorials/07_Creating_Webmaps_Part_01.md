## Tutorial 07 - Creating Webmaps - Part 01
*Tutorial created by Juan Francisco Saldarriaga (jfs2118@columbia.edu) for the [Mapping for Architecture, Urbanism and the Humanities](https://github.com/juanfrans-courses/mapping_arch_hum) class at Columbia University*

This is part 1 of a 2 part tutorial. In this first part you will create multiple web maps using CartoDB. In the second part, you will create different *base maps* using Mapbox and then use those *base maps* with your CartoDB maps.

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