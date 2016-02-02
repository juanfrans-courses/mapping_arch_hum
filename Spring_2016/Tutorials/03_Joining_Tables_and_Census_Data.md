## Tutorial 03 - Joining Tables and Census Data
Census data is often one of the most mapped datasets, and there are good reasons for this: not only does it provide insights about our current living conditions, like income, race, age, employment or commuting patterns, but it also serves as the backdrop for many other kinds of data. Without population data, for example, we wouldn't be able to 'normalize' cellphone usage or crimes, and without median household income or race patterns we wouldn't be able to identify social justice problems, like concentrations of environmental hazards in poor and or minority neighborhoods.

However, if not handled properly, mapping census data can be difficult and even problematic. Not only do you need to be able to correctly choose the right geographical level of analysis and download the right datasets, but you also need to be able to join these tables to existing shapefiles and symbolize them correctly. This tutorial will guide you through the process of downloading both the geographical boundaries and the census data, bringing them both into qGIS and joining them, and properly symbolizing it.

### Datasets:
This tutorial will be dealing with two main datasets, both provided by the U.S. Census Bureau. The first one will be the geographic boundaries of the census tracts and the second one will be census data itself in table form. As with our previous tutorials we will also use some of the other shapefiles we have downloaded for previous tutorials:
* nybb - New York City boroughs. Originally downloaded from [here](http://www.nyc.gov/html/dcp/html/bytes/districts_download_metadata.shtml).
* HYDRO - New York hydrography. Originally downloaded [here](https://data.cityofnewyork.us/Environment/Hydrography/drh3-e2fd).
* hydropol - U.S. Hydrographic features. Originally downloaded from [here](http://www.rita.dot.gov/bts/sites/rita.dot.gov.bts/files/publications/national_transportation_atlas_database/2014/polygon).

### Creating Place of Birth Maps with Census Data
#### Downloading Census Data
The first step will be to download the 'empty' geography files for our unit of analysis (by 'empty' I mean without any census attributes, apart from unique identifiers). However, before doing this we should actually decide what unit of analysis we will use.

The [American Community Survey](https://www.census.gov/programs-surveys/acs/), which is the statistical survey we will be using, provides data at multiple geographic levels, all the way from the whole country to the block group (which in Manhattan can be anywhere between 1 and 4 city blocks). Some of the other geographic units of analysis include regions, states, counties and metropolitan statistical areas. However, not all the data comes at every geographical level, so in general, we will try to find the smallest unit of analysis available for our dataset. In our case, that will be the census tract level, which roughly corresponds to 8 Manhattan city blocks, or four block groups.

The two images below show census block groups in orange and census tracts in blue over a portion of city blocks in Harlem.

![Census Block Groups](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/01_Census_Block_Groups.png)

![Census Tracts](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/02_Census_Tracts.png)

To download the census tracts boundaries for New York State go [here](https://www.census.gov/cgi-bin/geo/shapefiles/index.php) and choose `2015` and `Census Tracts` and then `New York` and download.

Once we have the 'empty' geography boundaries for the census tracts we need to download the actual data. For this we will use the [American FactFinder](http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml) which is one of the portals where you can download census data. However, note that this is not the only place to download census data. Some other resources are the [U.S. Census Bureau website](https://www.census.gov/en.html) and ***********************************************. For this exercise, though, we will use the [American FactFinder](http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml).

Once you are on the American FactFinder website, click on the `ADVANCED SEARCH` tab. Here we will search for the data at multiple levels:
* Geography: census tracts for New York City counties
* Dataset: American Community Survey (ACS) 2014 5-year estimates
* Topic: Place of birth for foreign born and place of birth by nativity and citizenship status

First, let's narrow down the options by dataset. The U.S. Census has two main surveys, the Decennial Census and the American Community Survey. The [Decennial Census](https://www.census.gov/history/www/programs/demographic/decennial_census.html) is the major census survey, carried out every 10 years and attempting to count every person in the country. However, it has two major disadvantages: one, it only happens every 10 years, so for the years in between, like where we are now, the last census might be too outdated and the next one too far away; and two, because it is not using any sampling techniques, it often under-represents minorities. More information about it can be found here *****************************

The second main survey is called the [American Community Survey (ACS)](https://www.census.gov/history/www/programs/demographic/american_community_survey.html) and happens continuously. Its questionnaire is sent to 295,000 addresses monthly and it gathers data on topics such as ancestry, educational attainment, income, language proficiency, migration, disability, employment, and housing characteristics. Its results come in 3 forms: 1-year estimates, 3-year estimates and 5-year estimates. The 1-year estimates are the most current but the least reliable. The 5-year estimates are not as current but are much more reliable. For this exercise we will be using the 2014 ACS 5-year estimate data.

In the left hand side of the `ADVANCED SEARCH` window, expand the `Topics` tab, and expand the `Dataset` option. Here, choose the `2014 ACS 5-year estimates`. You should see that dataset move to the top right-hand panel called `Your Selections`.

![ACS 2014 5-year estimates](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/03_Datasets.png)

Next, let's select the geography. Click on the `Geographies` tab and set the following parameters:
* Geographic type: Census Tract - 140
* State: New York
Once you've done this you will have the option to select the county. Select 'Bronx' and once the window below populates, highlight 'All Census Tracts Within Bronx County, New York' and click `ADD TO YOUR SELECTIONS`. Again, you should see this item added to your selections window. Do the same thing for all the census tracts in the rest of the counties in the city: New York (Manhattan), Kings (Brooklyn), Queens and Richmond (Staten Island).

![Geographies](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/04_Geographies.png)

* Place of birth for foreign born (B05006)
  * Census Tracts
    * Continents
      * Countries
* Place of birth by nativity and citizenship status (B05002)
  * Census Tracts
    * Native
      * Born in state of residence
      * Born in other state
        * Regions
      * Born outside US
        * Puerto Rico
        * US Island areas
        * Born abroad from American parents
    * Foreign born
      * Naturalized
      * Not a US citizen

### Datasets:
The main dataset we will be using in this tutorial is based on 311 data. For those of you who don't know, 311 is a service provided by the city of New York where people can call in (dialing 311) and submit complaints or ask questions about living in the city (the service also accepts complaints online). Some of the most popular complaints filed through 311 are about parking, noise, garbage, rodents, dead or damaged trees, air quality, construction permits, graffiti, homelessness, street conditions, taxis and water quality. There are other categories and each one of these has it's own subcategories. Furthermore, each entry in the dataset comes with the following fields (amongst others):
* Created date
* Closed date
* Agency
* Complaint type
* Descriptor
* Location type
* Incident zip code
* Incident address
* Street name
* City
* Landmark
* Facility type
* Status
* Due date
* Resolution description
* Community board
* X and Y coordinates
* Latitude and longitude

As you can see, the dataset is very interesting and a great resource for anyone studying New York. **Nevertheless, a word of caution is necessary**: many people use this dataset to describe and analyze conditions in New York; however, the 311 data doesn't describe the city, it describes the complaints people file, it is not about the city, it is about the complaints, and even though the complaints might tell us something about the city, the distinction is crucial. Every dataset has its own biases and the 311 dataset has very strong ones: it collects data ONLY about the people who complain and ONLY about what they choose to complain about. Again, this dataset is much more about the complaints and the people who complain than about the conditions in the city. There is no 1 to 1 relationship between the 311 complaints and the conditions in the ground. That being said, though, it is still a great resource and very fun to play with. You can find out more about the 311 service [here](http://www1.nyc.gov/311/).

Other datasets we will be using are (some of these you already downloaded for the first tutorial):
* nybb - New York City boroughs. Originally downloaded from [here](http://www.nyc.gov/html/dcp/html/bytes/districts_download_metadata.shtml).
* Roadbed - New York roadbed. Originally downloaded [here](https://data.cityofnewyork.us/City-Government/Roadbed/xgwd-7vhd).
* HYDRO - New York hydrography. Originally downloaded [here](https://data.cityofnewyork.us/Environment/Hydrography/drh3-e2fd).
* hydropol - U.S. Hydrographic features. Originally downloaded from [here](http://www.rita.dot.gov/bts/sites/rita.dot.gov.bts/files/publications/national_transportation_atlas_database/2014/polygon).
* tl_2015_36_bg - New York State census block groups. Originally downloaded from [here](https://www.census.gov/cgi-bin/geo/shapefiles/index.php). Here you should download the census block groups for New York state for 2015.
* state - U.S. State Boundaries. Originally downloaded from [here](http://www.rita.dot.gov/bts/sites/rita.dot.gov.bts/files/publications/national_transportation_atlas_database/2014/polygon)

### Creating Noise Maps of 311 Data in New York City
#### Downloading 311 Data
The first step in this tutorial is to select, filter and download the 311 data. The [NYC Open Data portal](https://nycopendata.socrata.com/) is a great resource for data related to New York City and it provides an easy way of accessing 311 data. In it's search bar type "311" and it should take you to a list of datasets related to 311 data. The one we are looking for is called "311 Service Requests from 2010 to Present". Alternatively, you might see a big yellow icon at the top of this page related to 311; this will also take you to the dataset.

Once you've accessed the dataset you will see something like this:

![311 Dataset](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/01_311_Dataset.png)
Here, we need to filter the database to download only the records regarding noise complaints for the last 6 months of 2015. You could attempt to download records for a longer period of time, but the files might get too large. To filter the data do the following:
* On the right-hand panel, where it says "Filter", create a small query with the drop-down menus. Where it says 'Unique Key', change it to 'Comolaint Type'. Keep the 'is' and then type in 'Noise' in the space below (The query should read 'Complaint type is noise'. Make sure there is a check-mark next to the word 'Noise'. You will see how the dataset is filtered and you only get the complaints of type 'Noise'.
* Next, click on 'Add a New Filter Condition' and create another query that reads 'Created Date' 'is between' '07/1/2015 12:00:00 AM' and '1/1/2016 12:00:00 AM'.
You should now see the data only for 'Noise' complaints created between the start of July and the end of December 2015.
* Your filters should look something like this:

![311 Filters](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/02_Filters.png)
* Finally, click on the 'Export' button at the top right-hand corner of the site and choose the 'CSV' format. Your file should start downloading then.
* If you open your .csv file in Excel you will see that there are about 30,380 records and that they have both X and Y coordinates and Latitude and Longitude. In the next steps we will use these fields to add the 311 data to a qGIS map.

#### Adding CSV data to qGIS
* First, open qGIS and add the following layers (downloaded for the first tutorial):
  * nybb
  * Roadbed
  * HYDRO
  * hydropol
* Organize your layers so that you have the roads on top, then water for New York, then boroughs and the last the water for the country.
* Now, to add the CSV file we downloaded, click on the `Add Delimited Text Layer` button on the top toolbar.

![Add CSV](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/03_Add_CSV.png)
* In the menu that comes up, look for your .csv (311 data) file. Once you've selected your file qGIS will automatically select some presets. You should have the following options selected:
  * File format: `CSV (comma separated values)` - (this is the format our data is in: each value is separated by a comma)
  * Record options: `First record has field names` - (the first row of our file contains the field names)
  * Geometry definition: `Point coordinates` - (our data has latitude and longitude data)
  * X field: `Longitude` and Y field: `Latitude` - (these are the columns in our dataset that contain our location coordinates)
  * Your menu should look something like this:

![CSV Menu](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/04_CSV_Menu.png)
* Once you click `OK` you will get a warning that says that 547 records were discarded because they didn't have geometry definitions. Click `Close`. These were some records in the dataset that we downloaded that for some reason didn't include location data.
* Next, qGIS will ask you to select a coordinate reference system (map projection) for this layer. Since we are adding this data based on the latitude and longitude information (decimal degrees, as opposed to feet) we need to select the `WGS 84`, which is the coordinate system that will correctly interpret this data. You will find it under `Geographic Coordinate Systems`. You will find more information on this coordinate system [here](https://en.wikipedia.org/wiki/World_Geodetic_System). Once you select the correct coordinate system, your points will appear on the map.
* Even though your points are already on the map, this is just a temporary layer. If you remove the layer, you will need to go through the whole importing process to add them again. To avoid this, export the points as a Shapefile:
  * Right-click on the new layer and select `Save As...`
  * In the menu choose the following:
    * Format: `ESRI Shapefile` - (this is the same format of our other layers)
    * Save as: choose the right location and name your file '311_Data'
    * CRS: `EPSG:102718 - NAD_1983_StatePlane_New_York_Long_Island_FIPS_3104_Feet` - (this is the coordinate system we are working with and we want this layer to have the same one)
    * Uncheck `Skip attribute creation` - (you still want to retain the attributes associated with each point)
    * Check `Add saved file to map` - (so that once you export the layer, the layer is added to your map)
  * Once you export your layer (and it's automatically added to your map) you can remove the original one by right-clicking and choosing `Remove`.

#### Symbolizing the Data
The last step in creating a qualitative map of the 311 data is a simple one: we need to symbolize each complaint using its subcategory. This is very similar to what we did in the previous tutorial when we were classifying the PLUTO dataset by land use.
* Right-click on the 311_Data layer and choose `Properties`.
* In the `Style` tab, change the drop-down menu that says `Single Symbol` to `Categorized` and then in the `Column` menu select `Descriptor` (this is the field we will symbolize).
* Now click on the `Classify` button at the bottom and you will get all the different sub-categories.
* Lastly, you should change the appearance of the dots: adjust their size, stroke and fill color like you did for the land use map.
* Once you've adjusted that, click 'OK'.
* Finally, you need to change the appearance of the other layers, create a print composer, add a scale bar, legend, title, source and brief description, and export your map as a PDF file.

#### Creating a Quantitative Map of 311 Data
Let's say you want to identify which census block group has the highest number of 311 noise complaints. To do this, you first have to join your 311 data to a layer containing the boundaries of New York City's census block groups.
* First, add the census block group shapefile (tl_2015_36_bg) you downloaded from the census website.
* Move this layer so that it's located below the HYDRO layer.
* If you zoom out, you will notice that this layer includes the census block groups for the whole State. However, we only need the ones for New York City. To select just these block groups we will use the 'select by attributes' method, which means selecting based on data in one of the fields of the layer. The census block group layer contains a field listing the specific county each block group is located in; we will use this field to select only the census block groups located in any of the 5 counties that make up New York City:
  * First, right-click on the census block group layer and select `Open Attribute Table`. Here you will see the data associated with each of the census block groups. The second column, the one called 'COUNTYFP', contains the county identifiers, and this is the one we will use to select only the New York City block group.
  * Now we need to select all the census block groups that have as their 'COUNTYFP' '005' (Bronx), '061' (Manhattan), '047' (Brooklyn), '081' (Queens) or '085' (Staten Island). To do this click on the `Select features using and expression` button. In this menu we will construct a query selecting only the features that have any of these numbers for their 'COUNTYFP' value.

  ![Attribute Table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/05_Attribute_Table.png)

  * The selecting by expression menu has three different panels: the left-hand one is where you will construct your query; the middle one is where you will find the different functions, operator and, more importantly, the attribute table fields; and the right-hand panel will have a description of whatever you select in the middle panel.
  * To build the query, expand the 'Fields and Values' drop-down menu in the middle panel and double-click on 'COUNTYFP'. You will notice the  "COUNTYFP" is added to the left-hand panel. Now type '=' after that and then click on the `all unique` button below the right-hand panel; this will show a list of all the unique values this field contains. Double-click on '005' to complete the first part of the query on the left-hand panel.
  * The query so far reads "COUNTYFP" = '005'. Notice that the '005' is under single quotation marks. This is because the value is a string (text), not a number. If it was a number you would only type 5, without quotations, and you would be able to do normal math operations with it. Instead, since it's a string, you have to type it with quotations and it behaves like text.
  * Now we need to add the other possibilities, with the operator `or` which we could type or select from the 'Operators' menu. Your final query should read something like this: `"COUNTYFP" = '005' or "COUNTYFP" = '047' or "COUNTYFP" = '061' or "COUNTYFP" = '081' or "COUNTYFP" = '085'`.

  ![Selection Query](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/06_Selection_Query.png)

  * Click the 'Select' button on the bottom-right side to select those features that match your query; then close your selection menu and your attribute table. You should see all the census block groups for New York City highlighted in yellow.

  ![Selected Block Groups](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/07_Selected_Block_Groups.png)

  * Finally, to create a shapefile with only the selected features, right-click on the census block group layer and select `Save As...`. In the next menu choose the following settings:
    * Format: `ESRI Shapefile`
    * Save as: choose the right location and name your file 'NYC_BlkGrp'
    * CRS: `EPSG:102718 - NAD_1983_StatePlane_New_York_Long_Island_FIPS_3104_Feet`
    * Check `Save only selected features` - (this one is very important; if you don't check it you will just export a copy of your original layer with all the features, selected or not)
    * Uncheck `Skip attribute creation` - (you still want to retain the attributes associated with each point)
    * Check `Add saved file to map` - (so that once you export the layer, the layer is added to your map)
  * Click `OK` and you should see a new layer with only New York City block groups.
* Now we need to join the 311 data to the census block groups and get a count of how many complaints are in each block group. To do this, click on `Vector` `Analysis Tools` `Points in Polygon...`

![Points in Polygon](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/08_Points_in_Polygon.png)

* In the 'Points in Polygon' menu choose the following settings:
  * Input polygon vector layer: 'NYC_BlkGrp' - (this is the polygon layer we will join the points to)
  * Input point vector layer: '311_Data' - (this is the layer containing the points that will be joined)
  * Output count field name: '311_Count' - (this is a new field that will be created and will contain the count of points that were joined to each block group)
  * Output shapefile: '311_BlkGrp'
  * Check `Add result to canvas` so the new shapefile is added to the map.
* Once you have all your settings ready, click `OK` and let it run. Once it's done, click `Close`. You will see your new layer on the map.
* If you right-click on the new layer (311_BlkGrp) and choose 'Open Attribute Table' you will see that the last field is called '311_Count' and it contains the number of points joined to each block group. We will use this field to symbolize the block groups.
* To actually symbolize the layer, right-click on it and choose `Properties`, and in the Style tab change the 'Single Symbol' drop-down menu to 'Graduated'.
* Next, in the 'Column' drop-down menu select the '311_Count' field to symbolize and click on the `Classify` button to load the values.
* You will notice that qGIS automatically classifies the values into 5 categories. Also, if you look at the settings on the top right-hand side you will see that the software uses an 'Equal Interval' method for this classification. However, if you click `OK` and look at the resulting map you will notice that most block groups fall within the first group, the one that goes from 0 - 145.8 and that very few are fall in the other ones. In fact, it seems like there is one single block group with more than 700 complaints (located in Queens), which is skewing the whole classification method upwards. This is clearly an outlier and the classification method should not be based on this particular block group.
* Instead, go back to the properties and change the classification method to 'Natural Breaks (Jenks)' which deals better with datasets that are not normally distributed. You can find out more about this classification method [here](https://en.wikipedia.org/wiki/Jenks_natural_breaks_optimization).
* You can change your color ramp or the individual colors or strokes of each of the classes. You can also change the number of classes the data is divided into but note that normally, we can only really differentiate between 5 or 6 classes.
* Once you are done with the classification, click `OK` to apply it to the layer and see your results on the map.

![Classification Methods](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/09_Classification_Methods.png)

Lastly, we need to hide the census block groups that fall outside of the New York City borough boundaries. If you look closely at the census block group layer, you will see that there are some block groups that fall inside the Hudson River and that shouldn't be included in our map.

There are a couple of ways of doing this: one option would be to clip the block group layer using the borough layer, in order to get rid of the census block groups that fall outside the boroughs. However, this option would permanently modify the block group layer and, if at any point the borough boundaries don't align perfectly with the block groups (which is entirely possible), the geometry of those block groups would be changed too. The best option then is to hide the block groups that fall inside the water and conveniently enough there is a field in the block group attribute table that has a specific value for these features.
* First, open the attribute table of the census block group layer. You will notice that there is a field called 'ALAND' and another called 'AWATER'. 'ALAND' one has a unique identifier for each of the block groups that has some land area; 'AWATER' has an identifier for those block groups that have some water. There problem is that some block groups have both water and land. So we will only show those block groups where the 'ALAND' field does not equal 0, meaning that they have some land.
* To do this we will create a 'Feature subset'. Open the layer properties and go to the `General` tab. At the bottom of this tab you will see the 'Feature subset' panel. Go to the bottom of this panel and click on the `Query Builder` button. This query builder will work in a similar way as the 'Selection by attributes' query builder.
* In the 'Fields' panel you will see the 'ALAND' field. Double-click on this to make it appear in the bottom panel ('Provider specific filter expression').
* Now add '!= 0' to the expression. ('!=' means 'does not equal').
* Your expression should look something like this:

![Query Builder](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/10_Query_Builder.png)

* Click `OK` in the 'Query Builder' and then `OK` again in the 'Properties' panel. Your map should now only show the census block groups that have land.

Once you are finished with this go ahead and adjust colors, strokes and layer order. And finally, create a print composer, add a legend, title, explanation, source and a scale bar, and export your map as a PDF file. Your final map should look something like this:

![Final Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/11_Final_Map.png)

#### Deliverables
Upload two (PDF) 311 data maps to Courseworks. They should both be of something different than 'noise' complaints. One should be a qualitative map, showing the location of each complaint, and the other should be a quantitative map, showing the number of complaints per census block group in New York City. Your maps should include proper legends, scale bars, titles, explanations and sources. Choose colors, line weights and fonts wisely.

