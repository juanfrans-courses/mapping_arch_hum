## Tutorial 04 - Working with Projections

### Datasets
This tutorial will incorporate vector datasets provided by Natural Earth.
* ne_10m_admin_0_countries - Current country boundaries. Originally downloaded [here](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-admin-0-countries/).

### Projection, Datum, CRS
#### Datum
A datum defines the surface of the earth to which a given set of lat/lon coordinates is referenced. Examples include NAD83 (which we encountered in previous tutorials that used the NAD_1983_StatePlane_New_York_Long_Island_FIPS_3104_Feet projection), WGS84, and NAD27. If you open up the QGIS "Project Properties | CRS" menu, searching for "NAD83," for example, will bring up a long list of different projections. Two datasets that were originally referenced to different datums, but which are then rendered in the same projection, will not line up.
#### Projection
A projection refers to the set of transformations that converts a series of coordinates, which are locations on a curved surface (the datum), into locations on a flat surface.
#### Coordinate Reference System (CRS)
Both the projection and datum are attributes of a Coordinate Reference System (CRS). A CRS is used to describe geographic data. 