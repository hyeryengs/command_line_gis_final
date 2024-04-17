# FINAL PROJECT OF COMMAND LINE GIS
SPINRG 2024

BY HYERYENG SHIN

## SYNOPSIS

**Scale and Location** All counties in New Jersey

**Topic** Good neighborhood to live

**Research Question** To identify the county offering the most favorable living conditions, I will selectively assess **10 key factors** from [laurushomes](https://www.laurushomes.co.uk/blog/posts/how-to-decide-where-to-live/)

**Mapping** I aim to apply suitability analysis techniques learned from my Topics in GIS class using command-line tools. For the static maps, I will generate choropleth maps and components for the suitability analysis, and eventually produce the final suitability analysis map. Furthermore, I intend to integrate this final map with an appropriate base map to create an interactive visualization

## STRATEGIES TO GET CRUCIAL FACTORS AND THEIR DATA SOURCES

1. **House price and affordability**: Calculate Housing price/median household income (or rental price/median household income) from [U.S. Census Bureau](https://data.census.gov/) API and check the county's housing price is appropriate in proportion to income level
2. **Amenities**: [Hospital](https://njogis-newjersey.opendata.arcgis.com/datasets/296e4de9d55640ffb9bb766f9606363b_1/explore) accessibility. Compare the average distance between the centroids of the counties and the top 3 nearest hospitals
3. **Rail accessibility**: Station accessibility ([Rail Stations of NJ Transit](https://njogis-newjersey.opendata.arcgis.com/datasets/NJTRANSIT::rail-stations-of-nj-transit/), [Bus Stops of NJ Transit by Line](https://njogis-newjersey.opendata.arcgis.com/datasets/NJTRANSIT::bus-stops-of-nj-transit-by-line/), [Light Rail Stations of NJ Transit](https://njogis-newjersey.opendata.arcgis.com/datasets/NJTRANSIT::light-rail-stations-of-nj-transit/), [Path Station Locations](https://data.cityofnewyork.us/City-Government/Path-Station-Locations/acxp-7ep7), [Passenger Rail Stations](https://njogis-newjersey.opendata.arcgis.com/datasets/dvrpcgis::passenger-rail-stations/) ). Compare the average distance between the centroids of the counties and the top 3 nearest stations or bus stops
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
   - visualize the results in various ways like a bar chart
7. Validation
   - validate the results with different sources such as median household income level, website surveys like [2024 Best Counties to Live in New Jersey](https://www.niche.com/places-to-live/search/best-counties/s/new-jersey/)

## 10 CRUCIAL FACTORS OUTPUTS
1. House price and affordability
   - Simply divide the median house price (median rental price) by the median household income of each county
   - The higher the index, the harder to afford housing price or rental prices (not good)
   ![Alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.1%20housing%20affordability%202.png)

2. Amenities
   - For amenities, I chose to analyze the accessibility of hospitals in case of emergency
   - Calculate the average distance between the centroid of each county and the distance of the top 3 nearest hospitals to the centroid
   - Employed BallTree function for calculation
   - The lower the index, the easier for the residents to access the service
  ![Alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.2%20amenities%202.png)

3. Rail accessibility
   - I chose to analyze the accessibility of all the public transit including bus stops
   - Similar to the above strategy, calculate the average distance between the centroid of each county and the distance of the top 3 nearest stations/stops to the centroid
   - The lower the index, the easier for the residents to access the service
   ![Alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.3%20rail%20accessibility%203.png)

4. School quality
   - Using buffer and unary union, I counted the schools that are within the 1-mile boundary of the cannabis dispensary shops
   - The lower the index, the better for students away from the opportunities to get exposed to cannabis
![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.4%20school%20quality%202.png)
   - For the web map, click [here](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.4%20school%20quality.html)

5. Commute time
   - Simply draw a choropleth map of commute time from the website's statistics
   - Though the commute time might be different depending on where we work, the lower, the better
  ![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.5%20commute%20time.png)
   
6. Access to green areas
   - Count the number of parks that are accessible to the public (excluding private parks) by county
   - The higher, the more opportunities to experience different parks and closer accessibility to parks
  ![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.6%20access%20to%20green%20areas.png)
     
7. Local environment
   - Count the number of contaminated sites by county
   - The lower, the better
  ![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.7%20local%20environment.png)
   
8. Air quality
   - Count the number of air quality permitted facilities by county
   - The lower, the better
  ![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.8%20air%20quality.png)
   - For the web map, click [here](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/air_quality.html)
     
9. Flood risks
    - According to [US Dept of Commerce
National Oceanic and Atmospheric Administration
National Weather Service](https://www.weather.gov/ffc/floods#:~:text=Areas%20most%20susceptible%20to%20flash,%2C%20storm%20drains%2C%20and%20culverts.), the flood-prone areas include mountainous streams and rivers, urban areas, low-lying area, storm drains, and culverts. From my data, I'll select the data that are 'Stream/River', 'Sea/Ocean' and have 0 elevation
    - Count the number of flood-prone sites that are either stream/river of sea/ocean and zero-elevation
    - The lower, the better
  ![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.9%20flood%20prone.png)
      
10. Crime rates and anti-social behavior
    - Compare the crime rate per 100k and the percentage of cases cleared
    - For the former factor, the lower, the better
    - For the latter one, I think it's better if higher (the ideal would be low cases occurred)
   ![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/2.10%20crime%20rate.png)
      
   
## Data Integration
```
# Merge all the data in Step 2
total_merged['COUNTY'] = nj_counties['COUNTY']
total_merged['housing_affordability'] = housing_and_rental_merged['housing_affordability_ratio']
total_merged['rental_affordability'] = housing_and_rental_merged['rental_affordability_ratio']
total_merged['hospital_accessibility'] = nj_counties_njsp['average_distance_to_nearest_hospitals']
total_merged['rail_accessibility'] = nj_counties_njsp['average_distance_to_nearest_stations']
total_merged['school_quality'] = nj_counties['schools']
total_merged['commute_time'] = commute_merged['COMMUTE_TIME']
total_merged['park_accessibility'] = parks_by_county_merged['park_count']
total_merged['contaminated_sites'] = contaminated_by_county_merged['value']
total_merged['air_facilities'] = nj_counties_with_air['num_facilities']
total_merged['flood_prone'] = nj_counties_with_flood['flood_sites']
total_merged['crime_per_100k'] = crime_merged['RATE_PER_100K']
total_merged['case_cleared'] = crime_merged['PERCENT_CLEARED']
```

![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/combined%20output%201.png)
![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/combined%20output%202.png)

## Redirection
Most factors represent better when the indices are lower but for 2 factors - park accessibility and case cleared, they are better when the indices are higher
To change the direction of the index meaning, reverse the direction of park accessibility and case cleared by deducting from the max value of each factor

```
# Reverse the direction of park_accessibility and case_cleared
modified_total_merged['park_accessibility'] = modified_total_merged['park_accessibility'].max() + 1 - modified_total_merged['park_accessibility']
modified_total_merged['case_cleared'] = modified_total_merged['case_cleared'].max() + 1 - modified_total_merged['case_cleared']
```

## Weighting
Give different amout of weights to each factor depending on what I think is more important and combine all the scores at once regardless of units (because the lower the number, the better it means after all)

```
# Define attribute weights
attribute_weights = {
    'housing_affordability': 0.1,
    'rental_affordability': 0.05,
    'hospital_accessibility': 0.05,
    'rail_accessibility': 0.05,
    'school_quality': 0.1,
    'commute_time': 0.1,
    'park_accessibility': 0.1,
    'contaminated_sites': 0.1,
    'air_facilities': 0.1,
    'flood_prone': 0.05,
    'crime_per_100k': 0.1,
    'case_cleared': 0.1
}
```

## Visualization
![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/result.png)

## Validation
1. Compare the suitability score with the median household income of each county
![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/validation%201.png)
![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/validation%201%20-1.png)

2. Compare the suitability score with the rank from the website's survey
![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/validation%202.png)
![alt text](https://github.com/hyeryengs/command_line_gis_final/blob/main/images/validation%202%20-1.png)

## Conclusion

In the scatter plot of suitability score vs median household income, the left upper corner is represented as wealthy with a good suitability score. These include MORRIS, BERGEN, and SOMERSET counties. The left lower corner represents low income but with good suitability scores. These include HUDSON, CAMDEN, and ESSEX counties.

In another scatter plot of suitability score vs rank, the left lower corner is represented as a higher rank in the real world reflecting actual residents' opinions. These include HUDSON, MORRIS, BERGEN, MERCER, MIDDLESEX, and SOMERSET counties.

By combining these two results, the overlapping counties are MORRIS and SOMERSET counties.

## Refleciton

Through my suitability analysis final project, I've gained valuable insights into geographic analysis and neighborhood characteristics. While my approach was simplified compared to complex tools like ArcGIS, it provided a foundational understanding of suitability analysis and its implications.

**Simplified Approach**: In contrast to ArcGIS's sophisticated tools, my project used straightforward calculations to determine suitability. While it may not capture all nuances, this simplified approach still yielded valuable insights and served as an accessible entry point into geographic analysis.

**Consideration of Factors**: I have to admit that my project needs further  consideration of various factors in suitability analysis, from housing affordability to crime rates. Each factor contributes uniquely to neighborhood suitability, and striking a balance requires thoughtful consideration of their interplay.

**Insight Generation**: Despite its simplicity, my project offered valuable insights into neighborhood environments. By examining factors, I was able to discern trends and draft insights about the friendliness of different neighborhoods.

**Flexibility and Customization**: A notable strength of my project is its flexibility and customization. By allowing users to adjust attributes and weights according to their preferences, it empowers exploration and analysis tailored to specific needs and interests.

**Alignment with Socioeconomic Factors**: Though not perfect, the outcomes of my project exhibited notable correspondence with median household income levels and online rankings of the best counties to reside in New Jersey. While the regression models did not demonstrate significant slope coefficients, the overall trends observed were remarkably consistent with expectations based on socioeconomic factors

Overall, my final insights reflect a thoughtful reflection on the suitability analysis process and its implications for community well-being. While my project may be simplified, it has provided a solid foundation for further exploration and analysis in the realm of geographic analysis.
