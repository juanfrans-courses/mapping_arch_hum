## Tutorial 04 - Working with Projections
The WGS84 Geographic Coordinate System is the default projection in QGIS. 

### Datasets
This tutorial will incorporate vector datasets provided by Natural Earth.
* ne_10m_admin_0_countries (Admin 0 - Countries) - Current country boundaries. Originally downloaded [here](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-admin-0-countries/).

### Datum, Projection, CRS
#### Datum
A datum defines the surface to which a given set of lat/lon coordinates is referenced, as well as the position of that surface in relation to the center of the earth. Examples include NAD83 (which we encountered in previous tutorials that used the NAD_1983_StatePlane_New_York_Long_Island_FIPS_3104_Feet projection), WGS84, and NAD27. If you open up the QGIS "Project Properties | CRS" menu, for example, and search for "NAD83," QGIS will generate a long list of different projections referenced to the NAD83 datum. 

Two datasets that were originally referenced to different datums, but which are then rendered in the same projection, will therefore not line up.
#### Projection / CRS
A projection, or Coordinate Reference System (CRS), is used to describe geographic data. A projection is the set of transformations that converts a series of geographic coordinates, which are locations on a curved surface (the datum), into locations on a flat surface.
#### A note re: QGIS 'on the fly' CRS Transformation
*_The layer you currently have selected when you check, or uncheck this option, determines its effects._*
* If you _uncheck_ "Enable 'on the fly' CRS Transformation," whether or not you currently have a layer selected does not matter: any layers that started off in a different projection but were transformed to correspond to the first layer you added to the project will be un-transformed, and rendered in the projection associated with the data file.
* If you _check_ "Enable 'on the fly' CRS Transformation," you must have the first layer, which determined the projection of the project, selected in the left panel.  

### Creating a U.S. Map from a Different Projection
* First, open a new project in QGIS and add the Natural Earth countries data. The data is referenced to the WGS84 datum, which we can see by navigating to the "Metadata" section under "Layer Properties."

![Layer Projection Metadata](https://github.com/juanfrans-courses/mapping_arch_hum/blob/master/Spring_2016/Tutorials/Images/04_Working_with_Projections/01_Layer_Projection_Metadata.png)
