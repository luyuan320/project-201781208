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
During the cleaning of the four raw datasets, records related to the city of Leeds were first extracted. Functions such as isnull().sum(), info(), duplicated(), head() and describe() were used to check for missing values, duplicates, and outliers.

Since each area could contain multiple valid crime records, duplicate rows were not deleted. Instead, the records were aggregated by LSOA. A heatmap was used to assist in checking for missing values. For missing LSOA values after aggregation, fillna(0) was used to fill in zeros, indicating no recorded crimes in those areas during that month. This approach reflects real-world conditions and helps ensure the completeness of subsequent spatial visualisation.

After basic cleaning, the three months of crime data were merged with the IMD data using LSOA code as the common key. After merging, missing values were again filled with 0. The merged dataset retained the following fields: LSOA code, area_name, crime_Jan, crime_Feb, and crime_Mar. A new field, total_crime, was added to represent the total number of crimes from January to March. A boxplot was then created to help identify potential outliers.

# Visualisation and Analysis Methods
For non-spatial visualisation, a bar chart was used to show the relationship between the deprivation index (IMD Decile on the x-axis) and the average number of crimes (on the y-axis). Before plotting, the data was grouped by IMD Decile using groupby(), and the average crime count for each group was calculated. To improve readability and accommodate colour-blind users, the chart used the plasma colour palette, with colours ranging from dark to light to represent different levels of deprivation.

For spatial visualisation, choropleth maps were created to display the spatial distribution of both total crime and deprivation across LSOAs in Leeds. To allow direct comparison, two maps were placed side by side: one showing the total crime count in the first quarter, and the other showing the IMD Decile distribution. Titles, legends, a compass, and a scale bar were added to enhance the interpretability of the maps.
The two maps both used the BuPu (blue-purple) colour scheme, which is colour-blind-friendly. Additionally, the IMD Decile map was colour-reversed so that darker shades represent higher levels of deprivation (Decile = 1). This adjustment ensures visual consistency with the crime map and improves comparative clarity.

Overall, the results from both non-spatial and spatial visualisations indicate that lower deprivation indices (i.e. higher levels of deprivation) are associated with higher average crime levels

# Modelling and Result Validation
To further validate the visual findings, a Poisson regression model was used. The regression coefficient for IMD decile was -0.1386 with a p-value < 0.001, indicating a significant negative correlation between deprivation index and crime count.

# Conclusion and Practical Implications
The results of this study provide a reference for future urban safety management in Leeds. The findings show that improving local economic and living conditions can help reduce crime rates and enhance the overall quality of life in communities.

# Project Structure
The project repository contains the following files:

1. project.ipynb: Main analysis file (Jupyter Notebook)

2. crime_data_01.csv, crime_data_02.csv, crime_data_03.csv: Crime records for January to March 2025

3. imd.xlsx: IMD 2019 dataset

4. leeds_LSOA_2011.shp: 2011 Leeds LSOA boundary shapefile
