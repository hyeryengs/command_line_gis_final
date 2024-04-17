# FINAL PROJECT OF COMMAND LINE GIS
SPINRG 2024
BY HYERYENG SHIN

## SYNOPSIS

**Scale and Location** All counties in New Jersey

**Topic** Good neighborhood to live

**Research Question** To identify the county offering the most favorable living conditions, I will selectively assess **10 key factors** from [laurushomes website](https://www.laurushomes.co.uk/blog/posts/how-to-decide-where-to-live/)

**Mapping** I aim to apply suitability analysis techniques learned from my Topics in GIS class using command-line tools. For the static maps, I will generate choropleth maps and components for the suitability analysis, and eventually produce the final suitability analysis map. Furthermore, I intend to integrate this final map with an appropriate base map to create an interactive visualization

## STRATEGIES TO GET CRUCIAL FACTORS FROM [LAURUSHOMES](https://www.laurushomes.co.uk)

1. **House price and affordability**: Calculate Housing price/median household income (or rental price/median household income) from U.S. Census Bureau API and check the county's housing price is appropriate in proportion to income level
2. **Amenities**: [Hospital](https://njogis-newjersey.opendata.arcgis.com/datasets/296e4de9d55640ffb9bb766f9606363b_1/explore) accessibility. Compare the average distance between the centroids of the counties and the top 3 nearest hospitals
3. **Rail accessibility**: Station accessibility ([Rail Stations of NJ Transit](https://njogis-newjersey.opendata.arcgis.com/datasets/NJTRANSIT::rail-stations-of-nj-transit/), [Bus Stops of NJ Transit by Line](https://njogis-newjersey.opendata.arcgis.com/datasets/NJTRANSIT::bus-stops-of-nj-transit-by-line/), [Light Rail Stations of NJ Transit](https://njogis-newjersey.opendata.arcgis.com/datasets/NJTRANSIT::light-rail-stations-of-nj-transit/), [Path Station Locations](https://data.cityofnewyork.us/City-Government/Path-Station-Locations/acxp-7ep7) (NYC Open Data), [Passenger Rail Stations](https://njogis-newjersey.opendata.arcgis.com/datasets/dvrpcgis::passenger-rail-stations/) ). Compare the average distance between the centroids of the counties and the top 3 nearest stations or bus stops
4. **School quality**: Buffer the dispensary location and spatial join with [school locations](https://njogis-newjersey.opendata.arcgis.com/datasets/6f5ebca854234638953a9342f5b3d620_0/explore) and check which county has more schools exposed to cannabis dispensary within 1 mile
5. **Commute time**: Make a new table for [New Jersey Average Commute Time by County](https://www.indexmundi.com/facts/united-states/quick-facts/new-jersey/average-commute-time#table) and compare which county has the longest average commute time.
6. **Access to green areas**: [Park](https://njogis-newjersey.opendata.arcgis.com/datasets/ac19884cc71741ff91b808da50219ec2_62/explore) provisions. Count the number of parks in each county and compare them.
7. **Local environment**: Density of [known contaminated sites](https://njogis-newjersey.opendata.arcgis.com/datasets/b167bb2ae09c43f8ab9e954700be45d9_0/explore). Count the number of known contaminated sites in each county and compare them.
8. **Air quality**: Density of [Air quality permitted facility](https://njogis-newjersey.opendata.arcgis.com/maps/44f775eb03544c56a3545c0403db8b14/about). Count the number of air quality permitted facility sites in each county and compare them.
9. **Flood risks**: [Precipitation amount](https://njdep.rutgers.edu/rainfall/#data). Calculate the precipitation amount by county for the 2023 period.
10. **Crime rates and anti-social behavior**: Make a new table for each county’s [Crime Data](https://www.nj.gov/njsp/ucr/pdf/current/2021_UCR_Jan%20-%20March.xlsx) from [New Jersey State Police](https://www.nj.gov/njsp/ucr/current-crime-data1.shtml?agree=0) and compare which county has the highest crime rate per 100K and clearance rate

## Workflow
1. Setup
   - install and import basic libraries
   - initialize the census API
2. Data Preparation
   - process the data for analysis of 10 factors
   - plot choropleth maps or web maps to visualize the analysis results
3. Data Integration
   - combine all the processed data in one data frame for suitability analysis
4. Redirection
   - process the data so that all the data can face the same direction; the lower the better, the higher not good
5. Weighting
   - give weights to each factor depending on the weights that I think are more important
6. Visualization
   - visualize the results in various ways like bar chart
7. Validation
   - validate the results with different sources such as median household income level, website surveys like [2024 Best Counties to Live in New Jersey](https://www.niche.com/places-to-live/search/best-counties/s/new-jersey/)

