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

Once we have the 'empty' geography boundaries for the census tracts we need to download the actual data. For this we will use the [American FactFinder](http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml) which is one of the portals where you can download census data.

Once you are on the American FactFinder website, click on the `ADVANCED SEARCH` tab. Here we will search for the data at multiple levels:
* Geography: census tracts for New York City counties
* Dataset: American Community Survey (ACS) 2014 5-year estimates
* Topic: Place of birth by nativity and citizenship status

First, let's narrow down the options by dataset. The U.S. Census has two main surveys, the Decennial Census and the American Community Survey. The [Decennial Census](https://www.census.gov/history/www/programs/demographic/decennial_census.html) is the major census survey, carried out every 10 years and attempting to count every person in the country. However, it has two major disadvantages: one, it only happens every 10 years, so for the years in between, like where we are now, the last census might be too outdated and the next one too far away; and two, because it is not using any sampling techniques, it often under-represents minorities. More information about it can be found here *****************************

The second main survey is called the [American Community Survey (ACS)](https://www.census.gov/history/www/programs/demographic/american_community_survey.html) and happens continuously. Its questionnaire is sent to 295,000 addresses monthly and it gathers data on topics such as ancestry, educational attainment, income, language proficiency, migration, disability, employment, and housing characteristics. Its results come in 3 forms: 1-year estimates, 3-year estimates and 5-year estimates. The 1-year estimates are the most current but the least reliable. The 5-year estimates are not as current but are much more reliable. For this exercise we will be using the 2014 ACS 5-year estimate data.

In the left hand side of the `ADVANCED SEARCH` window, expand the `Topics` tab, and expand the `Dataset` option. Here, choose the `2014 ACS 5-year estimates`. You should see that dataset move to the top right-hand panel called `Your Selections`.

![ACS 2014 5-year estimates](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/03_Datasets.png)

Next, let's select the geography. Click on the `Geographies` tab and set the following parameters:
* Geographic type: Census Tract - 140
* State: New York
Once you've done this you will have the option to select the county. Select 'Bronx' and once the window below populates, highlight 'All Census Tracts Within Bronx County, New York' and click `ADD TO YOUR SELECTIONS`. Again, you should see this item added to your selections window. Do the same thing for all the census tracts in the rest of the counties in the city: New York (Manhattan), Kings (Brooklyn), Queens and Richmond (Staten Island).

![Geographies](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/04_Geographies.png)

Finally, we need to select the tables that we will be exporting. In this tutorial we will be using the table for 'Place of birth by nativity and citizenship status (B05002)'. To select this table click on the 'Topics' tab again, and expand 'People' and 'Origins' and click on 'Citizenship'. Once it's been added to your selections you can close that little window. Now you should see a list of all the tables that match your selection criteria. Click on the 'PLACE OF BIRTH BY NATIVITY AND CITIZENSHIP STATUS (B05002)' table. You should now see the selected table with the data for the selected census tracts.

As you can see this table has data on where everyone was born and it comes in the following form:
* Total
  * Native
    * Born in state of residence
    * Born in other state in the United States
      * Northeast
      * Midwest
      * South
      * West
    * Born outside the United States
      * Puerto Rico
      * U.S. Island Areas
      * Born abroad of American parent(s)
  * Foreign born
    * Naturalized U.S. citizen
    * Not a US citizen

On the top, we have every single census tract with the corresponding value and a margin of error. It is important to note that these are not exact values, they are estimates based on the statistical methods the census is using. That's also why they include the margin of error. However, even though these numbers are not 100% accurate they still give us a pretty good idea of what is happening no the ground.

The last thing we need to do is modify the table so that it fits the way data is organized in qGIS. If you remember when we opened attribute tables in qGIS, every row represented a feature and every column a different field. Here, it's the other way around, so we need to 'transpose' the table to make it match qGIS. To do this click on `Modify Table` at the top left and then on `Transpose Rows/Columns`. Now you should see the table with the census tracts on the left-hand column and the fields on the first row.

![Final table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/05_Final_Table.png)

Finally, click on `Download` and make sure you are selecting 'Comma delimited (.csv) format (data rows only)', 'Data and annotations in a single file' and 'Include descriptive data element names'. Click `OK` and then once your files are ready `Download` again.

#### Formatting Census Data
In order to bring this census data into qGIS we need to re-format the table, so that it is correctly read by the program and we can join it to its geographic boundaries. This is a two step process: first, we will format the actual table in Excel, Google Spreadsheet or a simple text editor and, second, we will create a .csvt file, which will tell qGIS the exact format for each of the fields in the table.

Again, as with many things GIS, there are multiple ways of formatting the data. In our case we could do it using Excel, Google Documents (Spreadsheet) or even a simple text editor. Here, though, I will show you how to do it both through Excel and through a text editor. If you know how to do it in Excel you should be able to figure out how to re-format the data using a Google Docs Spreadsheet.

The great advantage of using Excel (or Google Docs) is that if you need to, you can add and **calculate** new fields into your data; for example, in our case, you would be able to calculate what percentage of the total population was foreign born and add that as a field (you could also do that inside qGIS). However, if you were to do that in a text editor, you would need to manually calculate the value for every single row. On the other hand, doing the re-formating through a simple text editor means that you can control the format of the data much more and that you won't have any problems with Excel auto-converting your data into other types, for example, from text into numbers or vice versa.

Another great advantage of using Excel or Google Docs is that if you need to delete multiple fields (for example, all the margin of error fields), you can easily do it. Doing it in the text editor would be a nightmare. That being said, there are options, when downloading the data from American FactFinder, to not get the margin of error fields.

* Re-formating data in Excel:
  * First, open a new file in Excel.
  * Once you've opened it, click on `File`, `Open...` and navigate to the folder where you saved your downloaded census tables.
  * Make sure you are able to open `All Files` not just `All Readable Files`. In my Mac, that option is called `Enable` and in Windows you should select the option `All Files (*.*)` instead of `All Excel Files (...)`.
  * Once you've done this you will be able to select the file called 'ACS_14_5YR_B05002_with_ann.csv' and open it.
  * Here's a preview of the raw file:

  ![Excel Table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/06_Excel_Table.png)

  * What we need to do now is two things: One, to rename the field names (header) and get rid of the second row, which is also a kind of header. And two, delete all the margin of error fields since we are not going to use them.
  * In terms of renaming the fields, ArcGIS is pretty peculiar about field names and although I haven't tested it, I assume qGIS is too. In any case it's better to be on the safe side and rename the fields to match the ArcGIS requirements. These are: maximum 8 characters, no spaces, no weird characters and start with a letter, not a number.
  * So first, delete all the margin of error columns. Just right-click on the column and say `Delete`. You should be left with 18 columns.
  * Now, rename the fields in the following way:
    * GeoID
    * GeoID2
    * GeoDisplay
    * TotalPop
    * Native
    * InState
    * OtherSt
    * OtherNE
    * OtherMW
    * OtherS
    * OtherW
    * N_Out
    * PuertoR
    * USIsland
    * AbroadAP
    * Foreign
    * FrgNat
    * FrgNonC
  * The names don't necessarily need to be like these ones. There's no standard way of naming these fields. The only thing I would recommend is to name them as close as possible to something you can actually read, so that you and the other people who use these files can easily understand what they mean. In the end, that is what metadata is there for, to tell you exactly what each of the fields means.
  * Once you've renamed your fields, delete the second row. Now you are left with only one header field and the actual data.

  ![Excel Final Table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/07_Excel_Final_Table.png)

  * Finally, save your file as a .csv file. If you are on a Mac, make sure you save your file as `Windows Comma Separated (.csv)`. There seems to be a problem with the line endings when you save it as the default .csv format. I am saving my file as `B05002.csv`.
* Re-formating in a text editor:
  * If you don't have Excel, or you don't want to use it, you can also re-format your file in a simple text editor. Here, I'll use the default Mac TextEdit application. You can also use your Windows Notepad or Sublime Text. As a side note, I highly recommend [Sublime Text](https://www.sublimetext.com/) as a text editor, specially if you are going to be doing some coding.
  * First, open the original census table ('ACS_14_5YR_B05002_with_ann.csv') with your text editor.

  ![Text Edit Table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/08_Text_Edit_Table.png)

  * Next, before you modify the file, save it as something else, so that you don't overwrite the original one. In my case I will save it as B05002_Text_Edit. TextEdit or Notepad will automatically save it as a .txt file, which is fine.
  * Next, you need to replace the first line (the one that goes from 'GEO.id' to 'HD02_VD15') with the right headers. However, since we are not deleting the columns for the margins of error we need to add those headers. The new first line should be something like this:
    * `GeoID,GeoID2,GeoDisplay,TotalPop,MOTotP,Native,MONat,InState,MOIS,OtherSt,MOOthS,OtherNE,MONE,OtherMW,MOMW,OtherS,MOS,OtherW,MOW,N_Out,MONatO,PuertoR,MOPR,USIsland,MOIsl,AbroadAP,MOAbr,Foreign,MOFrg,FrgNat,MOFrgNt,FrgNonC,MOFrgNC`
    * Notice all the MO (margin of error) and the commas separating all the headers. These are very important.
  * Now delete the second line, the one that goes from 'Id' to 'Not a U.S. citizen'.
  * Your new file should look something like this:

  ![Text Edit Final Table](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/09_Text_Edit_Final_Table.png)

* Creating the .csvt file:
  * In both cases you need to create also a .csvt file. This file will tell qGIS exactly what type of data each of the fields is in. The different types of data your fields can take are:
    * String - Represents text
    * Integer - Represents whole numbers
    * Real - Represents both negative and positive numbers, with decimal points
    * Date - Date in the format YYYY-MM-DD
    * Time - Time in the format HH:MM:SS+nn
    * DateTime - Date and time in the format YYYY-MM-DD HH:MM:SS+nn
  * So, for every column we need to specify what type the data is in.
  * In your text editor, open a new file.
  * Now, for every field, write the type of data it takes in quotation marks. So, for the Excel file, where we don't have the margin of error fields you would write: `"String","String","String","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer","Integer"` Note that every item is separated by a comma and that the first three fields, even though they seem like they are numbers, are actually text fields. This is very important, since we are going to use those fields to join our census table to the census boundaries, which also contain those fields as text. If we have one file with text and another with integers or real numbers, the program won't be able to match it.
  * If you are working on Mac's TextEdit you need to format your file as 'Plain Text'. To do this click on `Format` and then `Make Plain Text`. This will change your file from an .rtf to a simple .txt.
  * Save your file with the same name as the table but with a different extension. It is important to do this so that qGIS understands that this .csvt file corresponds to the other .csv or .txt file. In both Windows Notepad and in Mac TextEdit you need to manually type the extension (.csvt) and in TextEdit you need to un-check the option that says 'If no extension is provided, use .txt'.
  * If you are using the table we modified with Excel your .csvt file would be named `B05002.csvt`
  * If you were using the table we modified with TextEdit or Notepad you would name your file `B05002_Text_Edit.csvt`

  * Your final file should look something like this:

  ![CSVT File](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/10_CSVT_File.png)

* Now that the files are ready we can move into qGIS and bring everything together.

#### Importing tables into qGIS
* First open qGIS and add the boroughs (nybb) file we've been working with in past tutorials. The reason this is the first file we add is so that the map takes on that file's projection. This is important because the census boundaries come in a different projection so if we add those first our final map will have a projection that's not the normal New York City one.
* Now add the census boundaries that we downloaded at the beginning of the tutorial.
* Once you've loaded the census boundaries, open it's attribute table. You will notice that the fourth column is called 'GEOID'. That's the one we will use to join our census table to. Close the attribute table.
* Now, to add the census table click on the 'Add a delimited text layer' button:

![Add .csv file](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/11_Add_CSV.png)

* Select the .csv or .txt file with our data.
* If you added the .csv file the `CSV (Comma Separated Values)` option should be checked.
* If you added the .txt file the `Custom delimiters` option should be checked, as well as the `Comma` option, so that the program know we are delimiting our data using commas.
* In both cases the option `First record has field names` should be checked so that the program recognizes our headers and in the 'Geometry definition' the option `No geometry (attribute only table)` should be selected too (our files don't contain coordinates or geometrical attributes).
* Your import options should look something like this (for the .csv file):

![Import options .csv file](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/12_Import_Options.png)

* The ones for the .txt file should look like this:

![Import options .txt file](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/13_Import_Options_Txt.png)

* Click `OK` to import the table, and once you do it you should have it listed on your 'Layers Panel'. If you right-click on the table and open the attribute table you should see all your values there.

#### Joining tables to shapefiles
* To join the census table to the shapefile with the geographic boundaries right-click on the census boundaries and go to the properties panel. There, choose the `Joins` tab.
* In the `Joins` tab, click on the button with the plus sign to create a new join with the following settings:
  * Join layer: B05002 (the census table)
  * Join field: GeoID2 (the field that contains the unique identifier for each census tract)
  * Target field: GEOID (the filed in the census boundaries that contains the unique identifier)
  * Custom field name prefix: checked and delete what is in there. This is useful when you want to add a prefix for the fields that are joined, for example, when you are joining multiple tables and you want to differentiate them. In our case, since we are only joining one table we don't need this prefix.
  * The menu should look something like this:

  <img src="https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/14_Join_Menu.png" width=400/>

  * Click `OK` and then `OK` again.

* Now, if you open the attribute table of the census boundaries you will notice that a lot of the census tracts have the information from the table that we added. The ones that have `NULL` values are the ones outside New York City. Remember that we downloaded census tract boundaries not just for New York City but for New York State, so now we need to filter those census tracts out.
* An easy way to do this is to select all the census tracts that are not `NULL` for one of our main field, for example the GeoDisplay field.
* To do this, go to the attribute table and create a selection expression that says `"GeoDisplay" IS NOT NULL` and click `Select`. You should have now 2,167 features selected and if you click `Close` and close the attribute table too, these selected features should correspond to New York City.

![Selected Features](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/15_Selected_Features.png)

* Now export these selected features as a new shapefile and make sure it takes the right projection for New York City. Make sure also that when you are exporting you check the option that says `Save only selected features`, otherwise you will export all features, including the ones that don't have any census data.
* Now you have a shapefile only with New York City census tracts with all the data that we downloaded.

#### Symbolizing the data
The last part in our process is to finally symbolize the data and see what comes out of it. For this tutorial we will symbolize the number of people who are foreign born in each census tract. However, it is very important to **normalize** the data. Since not all census tracts have the same number of people living in them, showing just total count of foreign born people would not be useful; the census tracts with more inhabitants would probably have more foreigners too. That's why we should normalize by the total number of people living in each census tract.

In general, you should always try to normalize your data and this is usually going to be either by population or by area. Some examples are, cars per inhabitant, murders per 1,000 people, cell phones per person, built square footage per acre of land, income per capita. Always ask yourself if it wouldn't make more sense to view the data normalized by something else instead of just raw numbers.

First, just so you can see the difference between the different classification methods, let's classify the census data. We will do it with the raw numbers, knowing that for our final map we will normalize the data based on the total population in each census tract:
* Equal Interval classification:
  * Go to the properties of your census data shapefile and then to the style tab.
  * Change the classification from `Single Symbol` to `Graduated`.
  * In the column field, choose 'Foreign' and click on the `Classify` button. The panel in the middle should populate with 5 different ranges of values.
  * The default mode of classification is `Equal Interval`.
  * You will notice that the breaks start from 0 and advance in increments of 1660.2. The `Equal Interval` takes the full range of the *values* and divides it into the number of classes (in our case, 5).
  * If you click on the `Histogram` option and then on the `Load values` button you will see how the program divides the data.
  * Click `OK` and take a look at the map:

  ![Equal Interval](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/16_Equal_Interval.png)

  * You will notice that most census tracts fall within the first or second class and that there are only a handful of them in the third, fourth or fifth.
  * With this classification method we see the effect an extreme value can have on the graphic representation of data: the census tract in the Bronx that represents Co-Op City is skewing the data towards the top so that there are too few census tracts in the intermediate classes.

* Quantile (Equal Count)
  * Now return to the classification option in the properties of the dataset.
  * Choose `Quantile (Equal Count)` as the classification mode.
  * This classification method gets the total number of features and divides it by the number of classes, so that each class has an equal number of features. The problem with this method is that features that might be very far apart in terms of their values might end up in the same class.
  * Go to the `Histogram` option and click on `Load values` to see how this classification method splits the data.
  * Click `OK` and take a look at the map:

  ![Quantiles](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/17_Quantiles.png)

  * Here you see how every class has an equal number of features, but for example the census tract for Co-Op City, which we know has one of the highest counts of foreigners in the city, gets lumped up with many other census tracts, some of which might not have that many foreigners.

* Natural Breaks (Jenks)
  * Now change the classification method to `Natural Breaks (Jenks)`.
  * This classification method looks at the data and tries to maximize the difference between classes while minimizing the difference inside each class.
  * Take a look at the `Histogram` to see how this classification method treats the data.
  * You see how the divisions in the data follow the general pattern of the histogram.
  * Click `OK` and take a look at the map:

  ![Natural Breaks](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/03_Joining_Tables_and_Census_Data/18_Natural_Breaks.png)

  * This map is probably the most balanced one, clearly underlining the census tracts that have high values but still showing the variation in the rest of the census tracts.






Once you are finished with this go ahead and adjust colors, strokes and layer order. And finally, create a print composer, add a legend, title, explanation, source and a scale bar, and export your map as a PDF file. Your final map should look something like this:

![Final Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/02_Data_Types_and_311/11_Final_Map.png)

#### Deliverables
Upload two (PDF) 311 data maps to Courseworks. They should both be of something different than 'noise' complaints. One should be a qualitative map, showing the location of each complaint, and the other should be a quantitative map, showing the number of complaints per census block group in New York City. Your maps should include proper legends, scale bars, titles, explanations and sources. Choose colors, line weights and fonts wisely.

