# Mapping for Architecture, Urbanism and the Humanities
* Columbia University | GSAPP and A&S | ARCHA4122 | Fall 2016
* Fridays 11am - 1pm | Studio @ Butler
* Office hours: Mondays 10am - 12pm (previous email required)
* Professor: Juan Francisco Saldarriaga (jfs2118)
* Teaching Assistant: Emily Fuhrman (ef2512)

## Course Overview
This course provides an introduction to mapping theory and geographic information systems tools. Through the use of open-source GIS software ([qGIS](http://www.qgis.org/en/site/)) and open data ([OpenStreetMap](https://www.openstreetmap.org/)) students will learn how to critically use mapping tools and geographic data for spatial analysis and representation. In this course, students will work through a series of web tutorials and hands-on in-class exercises to gain a better understanding of how these tools and data can be leveraged to analyze, represent and study past or present urban phenomena. In addition to using existing data, students will also be able to create or bring their own sets of data and questions from other courses and will be able to work with these in our class.

No prior experience in mapping, design or data analysis is required for this course. Open only to graduate students in GSAPP or Arts and Sciences.

## General Topics
* Basic mapping concepts and techniques
* Data types
* Census data
* Metadata
* Data creation
* Geocoding
* Georeferencing
* Vector and raster data
* Webmapping and crowdsourced data

## Evaluation and Grading
* 10% Class participation and discussion
* 20% Individual assignments and tutorials
* 15% Midterm presentation
* 20% Map critique
* 35% Final project and final presentation and report

## Resources and Materials
Course files, tutorials and presentations will be located on Courseworks, on the [Center for Spatial Research](http://c4sr.columbia.edu/) website and on this repository. In addition, students should also contact the Digital Social Science Center (DSSC) located in Lehman Library (SIPA) for extra information and data.

The readings for the class will be duly uploaded to Courseworks. Similarly, students will be required to submit their assignments by uploading them to Courseworks. Finally, the class will also rely heavily on submissions
to the blog. Students will be required to upload some of their own work as well as inspirational material, encouraging and developing a critical stance and visual skills.

[Link to the blog](http://mapping2016fall.tumblr.com/).

[Link to number of posts](https://docs.google.com/spreadsheets/d/106JrEOQ64bOK1pqhBBwC-_z5eOU_4yphc7Fz0otWysI/edit?usp=sharing).

## Schedule
### Week 1: Introduction to course
September 9
* Course administration and syllabus
* What is GIS?
* Working with geographic data (vectors and rasters)
* Mapping software (qGIS)
* What is a shapefile
* Readings:
	* *[Meirelles, Isabel. Design For Information, Chapters 4 and 5](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2013_meirelles_design_for_information_chp_4_5.pdf)* (Required)
	* *[Harley, J., Deconstructing the Map](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/1989_harley_deconstructing-the-map.pdf)* (Required)

### Week 2: Introduction to mapping concepts and techniques
September 16
* Emphasis on *metadata*
* Elements of cartography (notations and conventions)
* Creating and exporting basic maps
* Datasets:
	* Building footprints with PLUTO data
	* Streets (Lion)
	* Pavement edge
	* Point data (schools, public facilities, other?)
	* Raster image of Columbia area
	* Water
	* PLUTO Lots for this area
* ***Assignment: [Tutorial 01](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/01_Creating_a_Basic_Map.md) - Create and export a basic map with proper notation, labels and symbology***
* Readings:
	* *[Crampton, J., Maps as social constructions: power, communication and visualization](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2001_crampton_maps-as-social-constructions.pdf)* (Required)
	* *[Alves, D., Exploring Literary Landscapes: From Texts to Spatiotemporal Analysis Through Collaborative Work and GIS](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2015_alves_exploring-literary-landscapes.pdf)* (Required)
	* *[Harvey, F., Introduction: Critical GIS](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2005_harvey_introduction-to-critical-GIS.pdf)* (Optional)
	* *[Edney, M., Plus ça change: Defining Academic Cartography for the Twenty-First Century](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2012_edney_plus-ca-change.pdf)* (Optional)

### Weeks 3 & 4: Maps and data
September 23 & 30
* Data types
* Understanding different classification methods (qualitative and quantitative)
* Common design pitfalls ("How to Lie with Maps")
* Adding X & Y data
* Joining spatial data to existing shapefiles (join by location)
* Datasets:
	* 311 data
	* Community districts or census block groups
* ***Assignment: [Tutorial 02](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/02_Data_Types_and_311.md) - Create two different maps based on 311 data, one quantitative and one qualitative***
* ***Final project proposal due (September 30th)***
* Readings:
  * *[Goodchild, M., Toward critical spatial thinking in the social sciences and humanities](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2010_goodchild_toward-critical-spatial-thinking.pdf)* (Required)
  * *[Pavlovskaya, M., Non-quantitative GIS](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2009_pavlovskaya_non-quantitative-GIS.pdf)* (Required)

### Week 5: Working with census data 1
October 7
* Understanding census data (decennial, ACS, samples, margins of error, etc)
* Downloading census data and joining it to shapefiles
* Making new fields and calculating new values
* Datasets:
	* Census tracts and census block groups shapefiles
	* PLUTO dataset
* ***Assignment: Create your own dataset based on a humanities text and map it*** 
* Readings:
  * *[Caquard, S., Narrative Cartography: From Mapping Stories to the Narrative of Maps and Mapping](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Readings/2014_caquard_narrative-cartography.pdf)*

### Week 6: Working with census data 2
October 14
* Estimation methods
* Geoprocessing tools: buffers, clips, unions, update, dissolve, etc
* Advanced selection methods: select by location, select by attribute, etc
* ***Assignment: [Tutorial 03](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/03_Joining_Tables_and_Census_Data.md) - Create map of census data showing new fields***

### Week 7: Projections
October 21
* Understanding basic map projections concepts
* How to project or re-project existing datasets
* Link: [Comparing sizes across the globe](http://bl.ocks.org/zanarmstrong/raw/caa2da1ea1558cdc3357/#scale=471.85&center0=6.52865,20.3586336&center1=48.2392291,-98.9443219)
* Link: [North Korea's missile threat](https://www.google.com/search?biw=1440&bih=801&tbm=isch&sa=1&q=the+economist+north+korea+missile+range&oq=the+economist+north+korea+missile+range&gs_l=img.3...6324.13284.0.14152.43.20.0.0.0.0.0.0..0.0....0...1c.1.64.img..43.0.0.Ob_31RRRygY&bav=on.2,or.r_cp.&bvm=bv.112064104,d.eWE&dpr=2&ech=1&psi=JOeaVvH7CoXsmAHstqi4DA.1452992295091.3&ei=JOeaVvH7CoXsmAHstqi4DA&emsg=NCSR&noj=1)
* Link: [Gnomonic Projection](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=gnomonic%20projection)
* ***Assignment: [Tutorial 04](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/04_Working_with_Projections.md)***

### Week 8: Midterm presentations
October 28

### Week 9: Geocoding, georeferencing and editing
November 4
* Working with address data (APIs), address locator, other methods
* Georeferencing existing maps
* How to create and edit spatial data
* ***Assignment: [Tutorial 05](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/05_Georeferencing_and_Creating_New_Shapefiles.md) - Georeference an existing map (old or new) and create new dataset from it***
* ***Assignment: Create a sound map with data that you collect***

### Week 10: Working with raster data
November 11
* Understanding the difference between vector and raster data
* Understanding the different types of raster datasets
* understanding raster bands
* Downloading Landsat images
* Creating 'true color' and 'false color composite' images
* Extracting data from raster files
* ***Assignment: [Tutorial 06](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/06_Working_With_Raster_Data.md) - Create the following maps***:
  * Change in population (based on the Gridded Population of the World datasets)
  * 3 different 'False Color Composite' maps based on Landsat imagery

### Week 11: Webmapping and crowdsourced data (part 1)
November 18
* Concepts and tools of webmapping
* Overview of webmapping platforms
* Working with webmapping platforms (CartoDB, MapBox, Mapbox Studio, etc)
* Exporting files ready for webmapping
* [Tutorial 07](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/07_Creating_Webmaps_Part_01.md)
* ***Assignment: Written critique of a map***

### Week 12: Thanksgiving - No class

### Week 13: Webmapping and crowdsourced data (part 2)
December 2
* Concepts and tools of webmapping
* Overview of webmapping platforms
* Working with webmapping platforms (CartoDB, MapBox, Mapbox Studio, etc)
* Exporting files ready for webmapping
* [Tutorial 08](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Fall_2016/Tutorials/08_Creating_Webmaps_Part_02.md)
* ***Assignment: Create a webmap using both CartoDB and Mapbox Studio***

### Week 14: Lab work on final projects
December 9

### Week 15: Final review
December 16

### Assignment Schedule (Due Dates)
* **September 23:** Tutorial 1 - Create a land-use map
* **September 30:** Final project proposal
* **October 7:** Tutorial 2 - Create two different maps based on 311 data
* **October 14:** Assignment 1 - Create your own dataset and map based on a humanities text
* **October 21:** Tutorial 3 - Create demographic map with new calculated fields
* **October 28:** Midterm presentations
* **November 4:** Tutorial 4 - Working with projections
* **November 11:** Assignment 2 - Sound map
* **November 11:** Tutorial 5 - Georeference an existing (new or old) map and create dataset
* **November 18:** Tutorial 6 - Working with raster data
* **November 25:** Tutorial 7 - Webmapping (part 1)
* **December 2:** Assignment 3 - Map critique
* **December 9:** Tutorial 8 - Webmapping (part 2)
* **December 16:** Final review

## References
### Books
* Data Flow: Visualizing Information in Graphic Design
* Data Flow 2: Visualizing Information in Graphic Design
* Meirelles, Isabel, Design for Information
* Yau, Nathan, Data Points
* Bertin, Jaques, Semiology of Graphics
* Elke, Beyer, Atlas of Shrinking Cities
* Tufte, Edward, The Visual Display of Quantitative Information
* Tufte, Edward, Envisioning Information
* Tactical Technology Creative, Visualizing Information for Advocacy
* Orff, Kate, Petrochemical America
* Dodge, Martin, Kitchin, Rob and Perkins, Chris, [The Map Reader](http://onlinelibrary.wiley.com/book/10.1002/9780470979587)

### Blogs & Websites
* [Visualizing Data](http://www.visualisingdata.com/)
* [Flowingdata](http://flowingdata.com)
* [Periscopic](http://periscopic.com)
* [Visualizing.org](http://visualizing.org)
* [Accurat](http://accurat.it)
* [Moritz Stefaner](http://truth-and-beauty.net/)
* [Nocholas Felton](http://feltron.com)
* [Infosthetics](http://infosthetics.com)
* [Visualcomplexity](http://visualcomplexity.com)
* [The Economist - Graphic Detail](http://www.economist.com/blogs/graphicdetail)
* [New York Times - The Upshot](http://www.nytimes.com/upshot/)
* [Visualoop](http://visualoop.com/)
* [FiveThirtyEight](https://fivethirtyeight.com/datalab/our-33-weirdest-charts-from-2014/)
* [Huffington Post](http://www.huffingtonpost.com/2014/12/22/huffpost-infographics-201_n_6351828.html)
* [LA Times](http://graphics.latimes.com/2014-in-graphics/)
* [Wall Street Journal](http://graphics.wsj.com/wsj-interactives-2014/)
* [Washington Post](https://www.washingtonpost.com/graphics/national/2014-in-graphics/)
* [Quartz](http://qz.com/318339/all-of-the-charts-we-made-in-2014/)
* [New York Times - Interactive Storytelling](http://www.nytimes.com/interactive/2014/12/29/us/year-in-interactive-storytelling.html?_r=0#data-visualization)
* [Fathom](http://fathom.info/)
* [Data Canvas](http://map.datacanvas.org/#)
* [Waze Global Driver Satisfaction Index](http://blog.waze.com/2015/09/global-driver-satisfaction-index.html)
* [Lapham's Quaterly Maps](http://www.laphamsquarterly.org/archive/maps)
* [Lapham's Quaterly Charts and Graphs](http://www.laphamsquarterly.org/archive/charts-graphs)
* [Territory](http://themapisnot.com/)
* [Quartz Atlas Charts](https://www.theatlas.com/)
* [Sensory Maps](http://sensorymaps.com/)
* [Library of Congress - Maps](https://www.loc.gov/maps/collections/)
* [The National Geologic Map Database](http://ngmdb.usgs.gov/ngmdb/ngmdb_home.html)