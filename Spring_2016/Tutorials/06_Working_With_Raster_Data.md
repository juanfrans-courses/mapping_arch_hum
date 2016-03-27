## Tutorial 06 - Working With Raster Data
This tutorial will show you how to work with raster data in qGIS. We will do two things: first, we will download a raster dataset with the population of the world and we will extract information from it; and second, we will download satellite images from Landsat and combine them to form true and false color composites.

### Part 01 - Gridded Population of the World
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
* The symbology for a raster dataset works differently than the symbology for a vector file. The raster doesn't have multiple fields; only one value is associated with each pixel in the raster dataset. This value corresponds to the 'brightness' value of the pixel, or if you are working with color raster, to the 'rgb' value of the pixel.
* If you click on the `Identify Features` button (the one with the 'i' icon) and you click anywhere on the raster you will see the value associated with that specific pixel. The value will appear as the value for `Band 1`. In our case, this value represents people in this 1km x 1km cell.

![Identify Results](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/02_Identify_Results.png)

* Now, go to the properties of the raster and go to the `Style` tab. You will see that it is different than the symbology for a normal vector dataset.

![Symbology](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/03_Symbology.png)

* Here you will see that the default style is of a `Singleband gray`, which means that it's only symbolizing in grayscale based on one band (rasters can be made up of multiple bands, as we will see in the second part of this tutorial).
* The color gradient is 'Black to white' but that can be switched to 'White to black'.
* And it is symbolizing based on the minimum value, in this case '0' and on the maximum value, '281.706'.
* Now, that's not actually the maximum value of the raster dataset. If you look at the right-hand panel (`Load min/max` values), which is where the min and max values come from, you will notice that the min/max values are being calculated based on a `Cumulative count cut`, which is used to get rid of the outliers. The `Cumulative count cut` means that qGIS is only taking into account the values between 2% and 98%, in the default cases.
* You could change that and use the option `Min / max` to use the actual minimum and maximum values. If you choose this one, you have to click on the `Load` button to load the new values. Do this and click on `Apply` to see how the image changes. Now the minimum is still '0' but the maximum is '140853'. Because of this new maximum value, most of the image appears black.
* Another way to get the value is to use the `Mean +/- standard deviation x` option, which will calculate the minimum and maximum values based on the mean and the standard deviation. Try that one, changing the factor too. Remember to press the `Load` button every time you change this.
* Now change the `Render type` to `Singleband pseudocolor` to get something similar to a symbology we would do for a vector file.
* On the right-hand panel you will see the `Mode` of classification (`Continuous` or `Equal Interval`) and below, again, the `Load min/max values` panel.
* Click on the `Classify` button to load the values and then hit `OK` to see it on the map.
* Now you can see clearly the regions of the world with the highest population density.

![GPW Symbolized](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/04_GPW_Symbolized.png)

#### Extracting Information from Raster
Finally, if we want to extract information from the raster file we can do it in two ways: one, by creating a new raster with the selected data; or two, by sampling the raster with points or polygons. In this case, sampling means using points or polygons to extract information from the raster file based on their location. In this tutorial we will do both.

##### Raster Calculator Tool
* Let's say we want to extract those areas of the dataset that have more than 100 inhabitants. To do this we will use the raster calculator and 'reclassify' the raster so that the pixels with more than 100 people get a value of '1' and the rest get a value of '0'.
* On your map go to `Raster` / `Raster Calculator`.
* Here, you will see the raster we are using in the `Raster bands` panel and below, where it says `Raster calculator expression` we will write the expression to select the data. Let's do this first.
* Double-click on the raster. It should automatically go to the `Raster calculator expression`.
* After the raster, write `> 100`. The full expression should look like this: `"gpw-v4-population-count_2010@1" > 100`
* Next, select the `Output layer`, the new file where you will save this new data.
* The format should stay as a GeoTiff.
* And finally, let's change the resolution. If you leave it as it is you might have problems with the raster and it will create a huge file (more than 3GBs). So change it to half of the current size: 21,600 x 8,700.
* Make sure the `Add results to project` option is checked.
* Click `OK`.

![Raster Calculator](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/05_Raster_Calculator.png)

* After the calculation you should get a new raster that has the densely populated places in white and the rest in black.
* However, to better symbolize this let's go to the properties of the new raster.
* First, in the `Style` tab, change the color gradient to `White to black` instead of `Black to white`
* And second, in the `Transparency` tab, in the `No data value` panel, in the `Additional no data value` add the number '0' so that qGIS treats '0' as no values and makes it transparent.
* Click `OK`.
* Now you should see the areas with more than 100 people as black pixels and the rest should be transparent.
* If turn off the other layer your map should look something like this:

![Selected Areas](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/06_Selected_Areas.png)

A couple of things here before we move further:
* One, if you compare the new raster with the original one you will notice that in the new one the pixels are much larger than in the old one. This is because when we exported the new raster we changed the number of rows and columns. The problem with this is that it makes the new raster less detailed than the old one. However, it also makes the file size smaller.
* Two, we could have just changed the symbology of the original layer to create the same effect. In this case we would have just manually created two symbols (with the `+` and `-` buttons), one going up to 99.99999, in white, and the other starting at 100 in black. Here is how that symbology option would look like:

![Manual Symbology](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/07_Manual_Symbology.png)

#### Sampling Raster Data
We can 'absorb' the raster data into a vector file by 'sampling' the raster data. This can be done at specific locations, with points, or over specific areas, with polygons.

First, let's talk about sampling with points. If we had a points file for different locations around the world we could use that, and this could, for example, be a point file with world cities. However, because we are dealing with a raster file, our sampling with those points wouldn't necessarily be that precise. The sampling **only** takes the value at the specific location of the point and not over the whole area of a city. For example, in the case of New York, if our point was located over Central Park, we would only 'absorb' the value of the pixel at Central Park, and not over the whole city. In the case of our population dataset, we would only get a value of around 9,000 people, which is the value of the population in the square kilometer in which Central Park is located. For this reason, sampling raster data with points works much better with continuous data, like temperature or pollution, smoother data, data that doesn't change that much from one location to the next.

Nevertheless, having said that, we will do some point sampling with this raster, and instead of using a point file of world cities we will create a grid of points and use that to sample the raster:
* To create a grid of points go to `Vector` / `Research Tools` / `Regular Points` (you could also use `Random Points` if your intention was to sample at random locations).
* As the `Input Boundary Layer` select the original raster file (gpw-v4...).
* And instead of using a specific spacing, select `Use this number of points` and choose 200000 (two hundred thousand).

![Regular Points](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/08_Regular_Points.png)

* Press `OK` and you should get a layer with a grid of points over your raster.
* Now, before we can proceed with the sampling we need to load the plugin that has the tool (the sampling tool doesn't come pre-installed in the default version of qGIS). To do this go to `Plugins` / `Manage and Install Plugins...` This will take a little bit to load but you should end up in the 'Plugins' repository.
* In the `Search` bar, type 'Point sampling' and you should see in the panel right below this the tool.
* Select the tool and click on the `Install plugin` button.

![Point Sampling Plugin](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/09_Point_Sampling_Plugin.png)

* Once the tool is installed, close your plugins manager and go to `Plugins` / `Analyses` / `Point Sampling Tool`.
* Select your the layer containing your points first and then highlight the original raster containing the values that we want to sample.
* Select your output file and make sure `Add created layer to the TOC` is checked.
* Click `OK`. This process might take a little while.

![Point Sampling Tool](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/10_Point_Sampling_Tool.png)

* Once you have your new points, open the attribute table to make sure they have 'absorbed' some data. A lot of them are going to be 'NULL' (the ones over the water) but some of them are going to have values.
* Open the properties of this file and go to the `General` tab.
* There, write a filter to exclude all the points that have 'NULL' as a value. The query should be something like this: `"gpw-v4-pop" IS NOT NULL`

![Query Builder](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/11_Query_Builder.png)

* Once you've done this, go to the style tab and change the symbology to visualize the points based on their values. You should get something like this:

![Population Points](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/12_Population_Points.png)

* Finally, just a word of warning: you can see here how the sampling, even though we used 200,000 points at regular intervals, missed a lot of the data in the raster. For example, in my case, it didn't really capture New York City. This is the problem with having a very detailed raster and sampling it with a layer that is not as dense.

Now, you can also sample using polygons. For example, in our case, we could use the country vector file to 'absorb' the values from the raster. This process takes in the values from all the pixels that fall within each polygon and can perfomr mathematical operations on those values, like calculating the sum, the mean, median, standard deviation, maximum and minimum. **However, when you have a very dense raster, like the one we have here, this process takes a very long time. For this reason I will go through the steps but unless you have a lot of time, don't try to do it.**

The process is actually very simple:
* First, go to `Raster` / `Zonal Statistics` / `Zonal Statistics`.
* There, choose the original raster (gpw...) as the 'Raster layer' and the countries file as the 'Polygon layer'
* In the 'Output column prefix' write 'Pop'.
* And make sure 'Count', 'Sum', 'Mean', 'Median', 'Minimum' and 'Maximum' are checked.
* Click `OK`.

![Zonal Statistics](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/13_Zonal_Statistics.png)

##### Deliverable
The deliverable for this part of the tutorial is a map of the world showing population **change** from 2000 to 2010 (based on the 'Gridded Population of the World' datasets). You can build either a dot map or a polygon map. **Very important, however, your map needs to be in a projection that is not the default one. Choose a world projection that represents area well ('equal area projection'), for example, the Mollweide projection.** As always, choose your colors, fonts, layouts carefully and be sure to add a legend and a scale.

Here's an example of a final map, although this only shows population and not population **change** as yours should:

![Dot Population](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/14_Final_Map_DotMatrix.png)

### Part 02 - Landsat Satellite Images
Another great thing about working with raster data is the ability to take satellite images of the Earth and extract information from them. One of the most useful datasets for this are the images taken by the Landsat satellites. The Landsat program is operated by the U.S Geological Survey and NASA and has been in activity since the 1970s. The Landsat 8 (the current version of the Landsat satellites) is constantly circling the Earth, taking images of most areas every 2 weeks and these images are available for download for free. To find out more about the Landsat program go [here](http://landsat.usgs.gov//about_project_descriptions.php) and [here](https://en.wikipedia.org/wiki/Landsat_program).

#### Downloading Landsat Images
There are multiple ways of downloading Landsat images. The most common one is through the USGS (U.S. Geological Survey). However, to download images from their site you will need to sign up for a free account [here](https://ers.cr.usgs.gov/login/?RET_ADDR=http%3A%2F%2Fearthexplorer.usgs.gov%2Ffilelist). Another easy way of downloading Landsat images is through [Libra](http://libra.developmentseed.org/), a project by Development Seed. Downloading images through Libra is much easier than through the Earth Explorer (USGS), but Earth Explorer gives you access to much more data, including old Landsat images. In this tutorial we will download images through the Earth Explorer, but know that Libra is also a very good and easy option.

* First you need to sign up for a free account with the USGS. Once you've signed up for an account and you've logged in you can go to the main download [page](http://earthexplorer.usgs.gov/).
* Next, click on the `Data Sets` tab at the top left-hand part of the page.
* There, expand the `Landsat Archive` option and check the first option, `L8 OLI/TIRS`. This gives you access to the latest Landsat satellite images from the Landsat 8 satellite.
* Now, in the map part of the page, navigate to the southern-most tip of Colombia, and click on Leticia, the only major city there.

![Earth Explorer](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/15_Earth_Explorer.png)

* Then, click on `Results` at the bottom of the page. On the left-hand panel you should see a list of images from that specific area and satellite.
* If you click on the little foot icon next to one of the images, the map should show you the footprint of the image. It should match your selection and cover Leticia.
* Click on the `Show Metadata and Browse` button (the text icon three buttons right of the footprint one) to see a preview of the image and to see data about it.
* If you scroll down you will see all the data associated with the image. One important thing we are looking for is low `Scene Cloud Cover`, the amount of cloud visible in the image.
* Go through the images on the panel and select the one that has the least `Scene Cloud Cover`. We are looking for a value of less than 5 (this is percentage of the image).
* I found an image from July 3rd 2015 that has only 1.03 cloud cover. Once you find an image that works, click on the `Download Options` button, at the right of the `Show Metadata and Browse` one.
* Click on the `Download` option for the `Level 1 GeoTIFF Data Product`.
* Once the file finishes downloading, unzip it and take a look. You should see 12 .TIF files, each one of them corresponding to a different band (different wavelength), and one .txt file.
* Each of the bands means the following:
  * Band 1: Coastal aerosol
  * Band 2: Blue
  * Band 3: Green
  * Band 4: Red
  * Band 5: Near Infrared
  * Band 6: Shortwave Infrared 1
  * Band 7: Shortwave Infrared 2
  * Band 8: Panchromatic
  * Band 9: Cirrus
  * Band 10: Thermal Infrared 1
  * Band 11: Thermal Infrared 2
  * Band QA: Quality Assessment

#### Creating True and False Composites in qGIS
Now that you have the images you can load them into qGIS and combine the different bands to create images that underline different aspects of the Earth. For example, you can combine bands 4, 3 and 2 to create a 'True Color' composite, showing the true colors; or you can combine bands 7, 5 and 2 to create a 'Urban False Color' composite that highlights urban areas; you can also create an [NDVI](https://en.wikipedia.org/wiki/Normalized_Difference_Vegetation_Index) image with bands 5 and 4, highlighting vegetation; or you can combine bands 3, 4 and 5 to create a standard 'False Color Composite' that will highlight water and vegetation.

* First, open a new qGIS map and add your satellite images.
* Next, rename them so that it's easier to identify each band. Instead of 'LC80040632015184LGN00_B1' it should be 'Band_1'. To rename, right-click on the layer and choose `Rename`.
* Sort the layers so that the top one is 1 and the last one is QA.
* Explore the different bands and see what features come up better in each of them.
* Notice that Band_8 (Panchromatic) actually has a better resolution than the other ones. This band is often used to 'Pansharpen' (increase the resolution of) the other bands.
* For example, Band_5 (Near Infrared) is very good at highlighting water:

![Band 5](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/17_Band_5.png)

##### True Color Composite
* First we will create a 'True Color Composite', which will give us an image with 'standard' colors.
* Go to `Raster` / `Miscellaneous` / `Merge`.
* In the `Input files` select bands 2, 3 and 4.
* As the `Output file` name your new image 'True_Color_234' and make sure the format is `GeoTIFF`.
* Make sure the `Layer stack` option is checked and make sure the `Load into canvas when finished` option is also checked.
* Click `OK`.

![Merge Raster](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/16_Merge_Raster.png)

**Warning, the order in which the files are listed matters. And this influences the symbology process!!!!**

* Once the process is done, close the windows.
* You should see your new raster on your map. Initially, it will not look like 'true colors'.
* Go to the properties of this new raster and go to the `Style` tab.
* There, change the `Red band` to `Band 3` and change the `Blue band` to `Band 1`. Remember, we loaded Band_2 (Blue), Band_3 (Green) and Band_4 (Red); because of the order, Band_2 became Band 1, Band_3 became Band 2 and Band_4 became Band 3. So now we are matching the `Red band` with Band 3 (which was Band_4 and the red), and so on and so forth.
* Also, change the `Load min/max values` to `Min / max` and click on the `Load` button.
* Once you've made this changes click `OK`.

![True Color Properties](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/18_True_Color_Properties.png)

* Your new image should get more 'realistic' colors.
* You can also symbolize it with the `Mean +/- standard deviation x` values. This can make the colors brighter.
* And if you play around with the settings in the `Color Rendering` panel below (brightness, saturation and contrast) you will achieve better results.

![True Color](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/19_True_Color.png)

Now let's create 'False Color Composites'. These are images that portray colors in different ways in order to highlight specific aspects of the natural environment, be it urban agglomerations, water or vegetation. The process to create these images is basically the same as creating a 'True Color Composite', the difference is just the bands that are used and the order in which they are displayed.

##### False Color Composite
* First, let's create a traditional 'False Color Composite'.
* Merge bands 3, 4 and 5. In this composite we are using the green and red bands plus the near infrared. This will highlight water as well as vegetation.
* In the properties, use Band 3 as the `Red band`, Band 2 as the `Green band` and Band 1 as the `Blue band` and, again, symbolize them using the `Min / max` option.
* You can also adjust the `Color Rendering` options.
* You will see all the vegetation turn red and the water turn dark.

![False Color](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/20_False_Color.png)

* In this image, red represents vegetation, but the darker reds represent tree coverage while the brighter reds represent grass or crops.
* Here we can see how around the city we have a lot of de-forestation but further in the jungle is still present.

##### Urban False Color
* Now, to create the 'Urban False Color Composite' use bands 2, 5 and 7.
* In the properties of this new image your bands should be:
  * Red - Band 3
  * Green - Band 2
  * Blue - Band 1
* You can also adjust the `Color Rendering` options.
* This image highlights urban land use as pink/red.

![False Urban](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/21_False_Urban.png)

* In these two links you will also find useful information about Landsat bands and more types of 'False Color Composites':
  * [Mapbox](https://www.mapbox.com/blog/putting-landsat-8-bands-to-work/)
  * [ESRI](https://blogs.esri.com/esri/arcgis/2013/07/24/band-combinations-for-landsat-8/)

##### Deliverable
The deliverable for this part of the tutorial is 3 different 'False Color Composite' images of a different part of the world (not Leticia in Colombia). You should label each one of them properly and make sure to add a scale bar. As always, choose your colors, fonts, layouts carefully. Each of the three maps should be in its own page.

Here's an example of one of the final maps for this section:

![Final Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/06_Raster_Data/22_False_Composite.png)
