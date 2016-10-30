## Tutorial 04 - Working with Projections
*Tutorial created by Emily Fuhrman (ef2512@columbia.edu) for the [Mapping for Architecture, Urbanism and the Humanities](https://github.com/juanfrans-courses/mapping_arch_hum) class at Columbia University*

Projections enable us to represent the earth on a flat surface. The WGS84 Geographic Coordinate System is the default projection in QGIS. This tutorial will walk through the process of creating a U.S. population density map in the Albers equal-area conic projection, a standard way of representing the United States with minimal distortion.

### Datasets
This tutorial will incorporate three datasets: one provided by Natural Earth, and two provided by the U.S. Census. First, download the current state administrative boundaries from Natural Earth, as well as 2016 state territories (both land and water) from the U.S. Census, listed below:

* ne_10m_admin_1_states_provinces (Admin 1 – States, Provinces) - Internal administrative boundaries. Originally downloaded [here](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/).
* tl_2016_us_state (States (and equivalent)) - Originally downloaded [here](https://www.census.gov/cgi-bin/geo/shapefiles/index.php).

Before we start, a brief overview of some terminology.

### Datum, Projection, CRS
#### Datum
A datum defines the spheroidal surface to which a given set of coordinates is referenced, as well as the position of that surface in relation to the center of the earth. Examples include NAD83 (which we encountered in previous tutorials that used the NAD_1983_StatePlane_New_York_Long_Island_FIPS_3104_Feet projection), WGS84, and NAD27. For more concrete evidence of this, open up the QGIS `Project` menu, select `Project Properties`, and navigate to the `CRS` section. If you search for `NAD83`, QGIS will generate a long list of different projections referenced to the NAD83 datum. 

![Layer Projection Metadata](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/01_NAD83_Projections.png)

Two datasets that were originally referenced to different datums, but which are then rendered in the same projection, will not line up.
#### Projection
A projection, or Coordinate Reference System (CRS), is used to describe geographic data. A projection is the set of transformations that converts a series of geographic coordinates, which are locations on a curved surface (the datum), into locations on a flat surface.

#### A note re: QGIS 'on the fly' CRS Transformation
The behavior for this option can be unpredictable, and QGIS has the annoying habit of resetting it after certain types of data manipulation. The layer you currently have selected when you check or un-check the 'on the fly' box (`Project` > `Project Properties` > `CRS`) impacts its effect. For this tutorial, you can avoid having to constantly check and un-check the box by closing the project that contains the original Natural Earth dataset and reopening a new project with the re-projected U.S. states as the first layer. This way, the project projection will be set by default to the Albers projection.

### Creating a thematic population map of the U.S.
#### Downloading Census state population data
The Natural Earth state boundaries will serve as the 'empty' geography files for this project, to which we will join both U.S. Census state area measurements and U.S. Census population counts. We will be mapping the population density for each U.S. state, and will therefore need the area of each state, as well as the number of people who live in each state.

To download the data for this project, we will be returning again to the [American Fact Finder](http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml) data portal. Navigate to the portal and click the `Advanced Search` option. Here we will select the following parameters within the `Topics` and `Geographies` levels:

* `Geography` > `State - 040` > `All States within United States and Puerto Rico`
* `Topics` > `Dataset` > `2015 Population Estimates`
* `Topics` > `People` > `Basic Count/Estimate` > `Population Total`

On the left side of the `Advanced Search` window, and open up the `Topics` tab. Click the `Dataset` section, and select `2015 Population Estimates`. 

![U.S. Census Data 2015 Population Estimates](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/02_Dataset_2015_Population_Estimates.png)

Next, open up the `Geographies` tab, and select `State - 040` from the dropdown menu. Select `All States within United States and Puerto Rico` from the window that pops up below, then click `ADD TO YOUR SELECTIONS`.

![U.S. Census Data State Geography](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/03_Geography_US_States.png)

Finally, open up the `Topics` tab again. Click on the `People` section, open `Basic Count/Estimate`, and select `Population Total`. Select the dataset listed as `PEPANNRES` in the search results window, entitled `Annual Estimates of the Resident Population: April 1, 2010 to July 1, 2015.`

![U.S. Census Data Population Estimates Table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/04_Population_Estimates_Table_Results.png)

Click the link to navigate to the table. This view should include a column listing the full name of every U.S. state, as well as subsequent columns containing population estimates for 2010, 2011, 2012, 2013, 2014, and 2015. To download the data in CSV format, click the `Download` button in the `Actions` bar. 

![U.S. Census Data Population Estimates Download](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/05_Population_Estimates_Table_Full.png)

Click `OK` when prompted to download the data, and then click the `Download` button once the popup window says the file is complete. The downloaded file will be named `PEP_2015_PEPANNRES`.

#### Transforming Census state population data
As always, there are many possible ways to transform data to fit the needs of your project. For this tutorial we will be working in Excel, or Google Sheets, to make the original file more manageable. We will reduce the dataset down to only the values we need, and then create a new column that will enable us to join the data to the Natural Earth shapefile.
* Unzip the `PEP_2015_PEPANNRES` file, and open up the CSV called `PEP_2015_PEPANNRES_with_ann.csv`. The file should look something like this:

![U.S. Census Data Population Estimates Excel](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/06_Population_Data_Excel.png)

* In order to create our map, the only data we need is state name, state ID, and population count. 
	* To narrow the dataset down to only these values, delete every column *except* for `GEO.id`, `GEO.display-label`, and the last column on the right, `respop72015`.
	* Next, delete the second row of the spreadsheet, which contains descriptions for the columns. 

	![Editing Population Estimates](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/07_Population_Data_Editing.png)

	* Rename the columns to `ID`, `Name`, and `Population`.

* We will be using [FIPS region codes](https://en.wikipedia.org/wiki/List_of_FIPS_region_codes_(S%E2%80%93U)#US:_United_States) to join the Natural Earth vector boundaries with the Census population data. The value in the `ID` column is a concatenated string that combines the Census table ID with individual state FIPS codes. We need to separate out the FIPS code portion of this ID so that this dataset can match up with the Natural Earth dataset, which already uses FIPS codes to identify each state. To do that, we need to create a new column that pulls *only the last four characters* in the `ID` column. We will use the `Right` function in Excel to do this.
	* Create a new column in Excel, and name it `FIPS_ID`.
	* In the first cell of the column, type the formula `=RIGHT(A2,4)`. This will pull the last four characters in the `ID` column, `A4`, into the new `FIPS_ID` column.

	![Excel FIPS Formula](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/08_Excel_FIPS_Formula.png)

	* After typing the formula, hit `Enter`. Double-click on the bottom right corner of the cell to populate the entire column with the new formula.

	![Excel Populated FIPS Column](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/09_Excel_Populated_FIPS_Column.png)
	
	* Name the file `StatePopulations.csv`, and save it to the a `Windows Comma Separated` format.

	![Excel Save New CSV](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/10_Excel_Save_New_CSV.png)

* As in Tutorial 03, we need to create a file that describes the data types in this new CSV before attempting to import it into QGIS. We will therefore use a text editor to create a `.csvt` file.
	* In your text editor of choice, open a new file.
	* In our CSV file, every column except for `Population` is a string. We therefore want to type, in order, `"String", "String", "Integer", "String"`.
	* Save the file with the same name as the CSV file, only with the `.csvt` extension: `StatePopulations.csvt`. It should look something like this:

	![Create CSVT file](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/11_Population_CSVT.png)

* Now we are ready to bring all of the data together in QGIS.

#### Re-projecting selected features from the Natural Earth dataset
We will begin by importing the Natural Earth boundary data into a new QGIS project. Because we are creating a thematic map of the United States, we only need the portions of the Natural Earth shapefile that represent U.S. administrative boundaries. We will isolate these areas, join them to corresponding TIGER state boundary data, and then re-project them to a projection more suitable for a U.S.-specific thematic map. 

* Open up a new project in QGIS and add the Natural Earth states and provinces data. The data is referenced to the WGS84 datum, which we can see by navigating to the `Metadata` section under `Layer Properties`. The definition for the layer's projection is under `Layer Spatial Reference System`.

![Layer Projection Metadata](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/12_Layer_Projection_Metadata.png)

* Since we are creating a map of the United States, the next step is to select all states and provinces that fall within U.S. administrative boundaries. Open up the attribute table for the states and provinces layer, click the `Select features using an expression` option, and build a query to select all features for which the `admin` value is equal to `United States of America`.

![Select U.S. States](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/13_Select_US.png)

* Hit `Select` and close the query builder. Navigating back to the map, only the U.S. should be selected.

![Selected U.S. States](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/14_Selected_US.png)

* Now, we want to re-project the United States to the Albers equal-area conic projection. The Albers projection is a popular choice for thematic maps of the U.S. Right-click the states and provinces layer, choose `Save As...`, choose `ESRI Shapefile`, and select `North_America_Albers_Equal_Area_Conic (ESPG:102008)` as the CRS. You may have to search for the specific projection by clicking on the small square icon next to the `CRS` dropdown menu.

![Set CRS to Albers Projection](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/15_CRS_Albers.png)

* Name the file `US_States_Albers`. Make sure to check the `Save only selected features` option, and hit `OK`.
* When added to your current project, the new layer will be automatically re-projected to the default WGS84 projection. Opening up the properties of `US_States_Albers` and navigating again to the `Metadata` panel, we can see that the `Layer Spatial Reference System` is _not_ WGS84, but the projection we selected in the previous step. It has been re-projected by QGIS to match the projection of the base layer.

![Check U.S. States Metadata](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/16_Check_US_Metadata.png)

* To prevent QGIS from automatically re-projecting the new layer to the current project CRS, select the `Project` dropdown in the top menu, select `Project Properties`, and _un-check_ `Enable 'on-the-fly' CRS transformation`. Now, select the `US_States_Albers` layer, right-click, and select `Zoom to Layer`. The features that fall within the administrative boundaries of the U.S. will have been re-projected to the Albers projection.

![U.S. States Albers Projection](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/17_Check_US_Albers.png)

* Go ahead and close this QGIS project and open a brand new one that contains only the re-projected Albers layer. This will prevent unexpected re-projection behavior from QGIS as you continue to create your map. 

#### Preparing the U.S. Albers layer for joins
Earlier, we transformed the Census population data in Excel to prepare it to be joined to the Natural Earth vector boundaries. Now, we have to make one more quick adjustment to the `US_States_Albers` layer, which contains an ambiguous FIPS reference for Minnesota. Once we fix this, we will derive a column that will enable us to join the Albers layer to the TIGER layer, to which we can then finally join our population CSV. 

![FIPS Alt Value for Minnesota](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/18_MN_FIPS_Alt.png)

The FIPS code for Minnesota needs to be `US27`, the value in Minnesota's `fips_alt` column. We are going to edit this manually. 

_**Note:** this is only required for Minnesota, despite the fact that other states also have a `fips_alt` value._

* Open up the attribute table for the `US_States_Albers` layer.
* Select the row that corresponds to Minnesota. Its value in the first `adm1_code` column is `USA-3514`.
* Click the abacus icon to open up the field calculator window. Make sure that `Only update 1 selected features` is checked.
* Check `Update existing field`.
* Select `fips` as the field to update.
* Open up the `Fields and Values` row in the middle panel, and select the `fips_alt` field.
* Double-click the field to add it to the field calculation panel. 

![Edit FIPS Alt Value for Minnesota](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/19_Editing_MN_FIPS.png)

* Click `OK`. The `fips` value for Minnesota should now be `US27`, the same as its `fips_alt` value.

_**Note:** This change may cause your project to re-project the `US_States_Albers` layer back to WGS84. To undo this, select the `ne_10m_admin_1_states_provinces` layer in the left panel, navigate to the top `Project` menu, go to `Project Properties...`, and check then un-check `Enable 'on the fly' CRS transformation`. Right-click the U.S. Albers layer and select `Zoom to Layer` in order to return to your previous view._

Now, we need to create a new column in the attribute table of this layer to prepare it to be joined to the TIGER layer. Though we are using the aforementioned FIPS codes for each of these joins, sometimes the codes are represented in different forms. In both the U.S. Albers layer and our downloaded CSV, the FIPS code is formatted in the following way: `US##`. In the TIGER shapefile, however, the FIPS code is located in a column labeled `STATEFP`, and is formatted without `US` in the front of the value: `##`. To facilitate our upcoming join, we will create a new column in the U.S. Albers layer with only the `##` part of the `US##` value. 

![Create a reformatted FIPS column](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/20_New_Column.png)

* Open up the attribute table for the `US_States_Albers` layer.
* Click the abacus icon to open up the field calculator window.
* Check `Create a new field`.
* In `Output field name`, enter `Join_FIPS`.
* In `Output field type`, enter `Text (string)`.
* In the `Expression` window, navigate to the `String` section in the middle panel, and select the `right` function. This will act in the same way as the function we entered in Excel. As explicated in the right panel, this function takes two values: the first is a string, and the second is a number specifying the number of characters to extract from the right side of the string. Our string will be the `STATEFP` column, and the number of characters will be `2`. This will enable us to create a new column wherein the FIPS ID, `US##`, will be represented as `##`.
* Open the `Fields and values` section in the middle panel, and select `fips`. This will be the first value for the `right` function.
* Next, type a comma (`,`), the number `2`, and a closing parenthesis (`)`). This tells the `right` function to represent only the last two digits of the value from the `fips` column. Your `Output preview` at the bottom should represent a two-digit number. Click `OK`.

#### Joining the TIGER shapefile to the U.S. Albers layer
Though Natural Earth data does not contain official state area measurements, the TIGER state boundaries do. On top of your newly projected U.S. Albers layer, add the `tl_2016_us_state` TIGER shapefile as a new vector layer. It should automatically adopt the Albers projection. If you open up the attribute table for the TIGER boundaries, you will see the columns `ALAND` and `AWATER`, which are the land and water areas in square meters for each polygon. These are the values that the Natural Earth dataset lacks.

#### Joining Census data to Natural Earth boundaries
Now that the `US_States_Albers` layer is ready, we can import the CSV file and join population values to each state. 
* Click the top `Layer` menu, navigate to `Add Layer`, and select `Add Delimited Text Layer...`.
* Select the previously-saved `StatePopulations.csv` file.
* Click the `No geometry (attribute only table)` option.
* Ensure the data looks correctly formatted, and click `OK`.

![Import Populations CSV](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/21_Import_CSV.png)

* Now, double-click on the `US_States_Albers` layer to bring up the `Layer Properties` panel.
* Navigate to the `Joins` section. 
* Click the `+` button at the bottom of the window to add a new join.
* Select `StatePopulations`, your imported CSV file, as the join layer.
* Select `FIPS_ID` as the `Join field`, which is the column name for the FIPS ID in the CSV file.
* Select `fips` as the `Target field`, which is the column name for the FIPS ID in the `US_States_Albers` layer.
* If you like, create a short `Custom field name prefix` to differentiate your joined columns from the original ones.

![Join CSV to the U.S. Albers Layer](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/22_Join_CSV_and_Albers.png)

* Click `OK`.
* Exit the `Layer Properties` panel, and open up the attribute table for the `US_States_Albers` layer. Confirm that three additional fields were added to the end.
* We now need to save the `US_States_Albers` layer as a new shapefile in order to retain the join. Right-click on the layer, choose `Save as...`, and name it `US_States_Albers_JOINED`. Make sure the selected CRS is still `North_America_Albers_Equal_Area_Conic (ESPG:102008)`, and keep `Add saved file to map` checked. Click `OK`. 

#### Representing population data
For our final print export, we will be creating a choropleth-_style_ map that represents raw population counts for each state. Now that the U.S. Albers shapefile has been joined to the Census data, this simply requires navigating to the `US_States_Albers_JOINED` `Layer Properties` panel, and selecting a graduated color scale for the population count column. Your map should look something like this:

![Population Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/23_Population_Map.png)

Once you are finished with this step, adjust colors and strokes as needed. Finally, create a new print composer. Add a legend, title, explanation, source, and scale bar. Add new layers for Alaska and Hawaii to approach a more 'stereotypical' Albers view, and make sure to include a scale bar for each one so as to be transparent about any distortion. Export your map as a PDF file. Your final map should look something like this:

![Final Map Example](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/Images/04_Working_with_Projections/24_Final_Map_Example.png)

#### Deliverables
#### Additional notes
[Here](https://medium.com/@joshuatauberer/how-that-map-you-saw-on-538-under-represents-minorities-by-half-and-other-reasons-to-consider-a-4a98f89cbbb1#.ih16rv26m) is an excellent piece on how choropleth maps underrepresent minorities.