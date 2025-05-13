# project-201781208
Spatial analysis of crime and deprivation in Leeds using open data

# Project Summary
This project analyses the spatial relationship between deprivation and crime rates in the city of Leeds, UK, using crime data and the Index of Multiple Deprivation (IMD) for the first quarter (January–March) of 2025.

# Data Sources
To enhance the credibility and reproducibility of the study, all data used in this project were obtained from official sources:

1. Crime records from January to March 2025 were obtained from West Yorkshire data provided by POLICE.UK.

2. The Index of Multiple Deprivation (IMD) data was published in 2019 by the UK Ministry of Housing, Communities and Local Government to reflect area-level deprivation.

3. To match the 2011 LSOA version used in the IMD data, the shapefile of Leeds LSOA boundaries (2011) was downloaded from the Office for National Statistics and used as the geographic basis for spatial analysis.

# Technologies Used
Before cleaning the four original datasets, records related to the city of Leeds were first extracted from the IMD dataset using the district name. Then, the LSOA code field from the extracted IMD data was used to filter Leeds-specific crime records for January to March.

The extracted data was checked using isnull().sum(), info(), duplicated(), head(), and describe() to identify missing values, duplicates, and outliers. Since each area may have multiple valid crime records, duplicate rows were not removed. Instead, crime counts were aggregated by LSOA to calculate total crimes for each area.

After initial cleaning, the three monthly crime datasets were merged with the IMD data using LSOA code as the common key. The merged table retained the following fields: LSOA code, area_name, crime_Jan, crime_Feb, and crime_Mar.

The combined dataset was then rechecked for duplicates and statistical anomalies. A heatmap was created to visually inspect missing values. For LSOAs with missing crime records after aggregation, fillna(0) was used to represent zero crimes in those areas. This approach reflects real-world conditions and helps maintain completeness in spatial visualisation.

A new column, total_crime, was created to indicate the total number of crimes from January to March. A boxplot was also drawn to identify potential outliers. Since high crime values can result from real-life events, these outliers were not removed.

# Visualisation and Analysis Methods
For non-spatial visualisation, a bar chart was used to show the relationship between the Index of Multiple Deprivation (IMD Decile, x-axis) and the average number of crimes (y-axis). Before plotting, the data was grouped by IMD Decile using groupby(), and the mean crime count was calculated for each group. To improve readability and support accessibility for colour-blind users, the ‘plasma’ colour palette was applied, transitioning from dark to light to represent different levels of deprivation.

For spatial visualisation, choropleth maps were used to display the spatial distribution of both variables. To better compare the spatial relationship between crime and deprivation, two side-by-side maps were created: one showing the total number of crimes per LSOA during the first quarter, and the other showing the IMD Decile distribution. Titles, legends, a north arrow, and a scale bar were added to enhance map readability and interpretation. Both maps used the BuPu (blue-purple) colour scheme for better visual contrast. The IMD Decile map used a reversed colour scale, where darker shades represent higher deprivation (Decile = 1), to visually align with the crime map.

Both the non-spatial and spatial visualisations show a clear trend: areas with lower deprivation indices (i.e., more deprived areas) tend to have higher average crime levels.

# Modelling and Result Validation
To further verify the results observed in the visualisations, a Poisson regression model was applied. The results showed that the regression coefficient for IMD decile was -0.1402, with a p-value of 0 (p < 0.001), indicating a significant negative relationship between deprivation level and crime count.

# Conclusion and Practical Implications
The results of this study provide a reference for future urban safety management in Leeds. The findings show that improving local economic and living conditions can help reduce crime rates and enhance the overall quality of life in communities.

# Project Structure
The project repository contains the following files:

1. project.ipynb: Main analysis file (Jupyter Notebook)

2. crime_data_01.csv, crime_data_02.csv, crime_data_03.csv: Crime records for January to March 2025

3. imd.xlsx: IMD 2019 dataset

4. leeds_LSOA_2011.shp: 2011 Leeds LSOA boundary shapefile
