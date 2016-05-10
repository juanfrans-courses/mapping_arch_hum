## Notes - Maps and Data (2/5/2016)

### 1. New Students, blog and software
* New students? If so, blog, assignments, final project and syllabus

### 2. Tutorial 01
* How did it go?
* Problems?
* Spatial index (rebuilding)
* Show examples

### 3. Blog

### 4. Readings
* What did you think?
* Difference between cartographer centered maps and user centered map (metrics and try to understand cognitive processes)
* Still different than trying to see maps as subjective
* Still different than trying to see maps as a sandbox for exploratory analysis (personal, interactive, multiple)
* Borges, Eco or Caroll
* For blog postings for the week, only “subjective”, “propaganda”, “fictional” maps
* Case study, Portuguese literature, what did you think?

### 5. Assignment and final project
* Two assignments (due February 17):
  * Create a map of 311 data
  * Create your own dataset and map it
* How’s the formation of the groups for final projects going?
* Proposal due on February 18 (group, topic, 1 paragraph)

### 6. Presentation
* Data types:
  * String
  * Integer
  * Real or Float
  * Boolean
  * Date or Time
* Data types (B):
  * Nominal or categorical (discrete): male/female, land use
  * Ordinal: quantities with order but no smooth transition between the categories (rankings, income levels, questionnaires)
  * Interval: like ordinal but with equal splits, so you can calculate differences (temperature F, distances)
  * Ratio: like interval but with an absolute zero (Kelvin)
* Methods of classification:
  * Categorized
  * Graduated:
    * Equal interval: divides the data into x number of categories with equal intervals (good for familiar data ranges, like temperature or percentages)
    * Quantile (equal count): divides the data into x number of categories each with an equal number of features (this one might really misrepresent the data, widely different values might be placed in the same category but no bucket will be empty)
    * Natural Breaks (Jenks): tries to account for the variation in the data, groups similar variables and maximizes the difference between classes (not useful for comparing different maps or datasets)
    * Standard Deviation (for a normal distribution the standard deviation is 68, 95, 99.7) (shows variation around the standard deviation, shows outliers)
    * Pretty Breaks