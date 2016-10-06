## Notes - Census and Joining Tables (10/07/2016)

### 1. Blog

### 2. Readings
* Alves, Exploring Literary Landscapes
* Problems with geographic literacy:
  * Projections
  * **Spatial heterogeneity**: tendency for phenomena distributed in many spaces to be statistically non-stationary. Therefore, you cannot really generalize from spatial samples, because they are always limited to the study area.
  * **Spatial dependence (autocorrelation)**: tendency of spatial data to exhibit short-run spatial autocorrelation. For example, real estate prices.
* Non-quantitative GIS (Marianna Pavlovskaya)
  * GIS as actually not that quantitative (power, negotiations)
  * Can a GIS view space in non-Cartesian terms?
  * Combining spatial data with qualitative data (p. 15)
  * Using ethnographic information in combination with spatial data
  * Mapping underprivileged ontologies
  * Importance of mixing methods (p. 16)
  * Challenge:
    * Complex relationships
    * Non-quantifiable properties
    * Unprivileged ontologies
    * Fluid human worlds
    * Create diverse human geographies
    * Use non-quantitative and non-conventional data in combination with more standard datasets (census)
    * It can represent unprivileged social ontologies
    * Enable mixed-methods

### 3. Questions about the 311 tutorial?

### 4. Assignment for next week
* Create your own dataset and map from a humanities text

### 5. Emily tutorial
* How to create dataset with Google Earth or Google Maps

### 6. Other
* Create an indicator map (2nd data frame) tutorial step 20 [here](http://www.qgistutorials.com/en/docs/making_a_map.html)
* How to package maps with layers through [QConsolidate](http://plugins.qgis.org/plugins/qconsolidate/)
* [Changing color and size - symbology](http://qgis.spatialthoughts.com/2012/02/styling-vector-data-in-qgis-using-size.html)

### 7. Census tutorial
* Margin of error in the ACS:
  * “A margin of error (MOE) is the difference between an estimate and its upper or lower confidence bounds. Confidence bounds can be created by adding the margin of error to the estimate (for the upper bound) and subtracting the margin of error from the estimate (for the lower bound). All published ACS margins of error are based on a 90-percent confidence level” (U.S. Census Bureau, 2008, p. 30).
  * [The American Community Survey - ESRI](http://www.esri.com/~/media/Files/Pdfs/library/whitepapers/pdfs/the-american-community-survey.pdf#page=6):
    * The margin of error enables data users to measure the range of uncertainty around each estimate. This range can be calculated with 90 percent confidence by taking the estimate +/- the MOE. For example, if the ACS reports an estimate of 100 +/- 20, then there is a 90 percent chance that the value for the total population falls between 80 and 120. The larger the MOE, the lower the precision of the estimate and the less confidence one should have that the estimate is close to the true population value.
    * The MOE measures the variability of an estimate due to sampling error. Simply, sampling error occurs when only part of the population is surveyed to estimate the total population. There will always be differences between the sample and the total. Statistically, sampling error measures the differences between multiple samples of the same population and differences within a sample of the population. Sampling error is directly related to sample size. The larger the sample size, the smaller the sampling error. Different areas are sampled at different rates to make the sample representative of the total population. Due to these complex sampling techniques, estimates in some areas have more sampling error than estimates in other areas. All MOEs are approximations of the true sampling error in an area and should not be considered exact. In addition, MOEs do not account for nonsampling error in the data and therefore should be thought of as a lower bound of the total error in a survey estimate.
    * The ACS reports MOEs with estimates for most standard census geographies. ACS estimates of total population and collapsed age, sex, and Hispanic origin estimates are controlled to annual estimates from the census' Population Estimates Program (PEP) for counties or groups of less populous counties. Since these estimates are directly controlled to independent estimates, there is no sampling error, and MOEs are zeroes. However, controlling a period estimate to the average of five point estimates imparts additional errors in the data that are not measured by MOEs.
    * In some areas, missing values are prevalent for medians and the aggregate estimates used to calculate averages. When estimates are zero, the Census Bureau models the MOE calculation by comparing ACS estimates to the most recent census counts and deriving average weights for states and the country.2 At the state, county, tract, or block group level, state-specific MOEs for zero estimates will be the same regardless of the base of the table.