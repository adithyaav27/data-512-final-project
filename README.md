# Health Impacts of Wildfire Smoke in Farmington, NM
## DATA512 Human Centered Data Science
## Goal
In recent times, the narrative of summer in the western United States has been increasingly dominated by wildfires, with plumes of smoke enveloping multiple states. Several factors are implicated in this development, including climate change, forestry management policies of the United States, and a heightened collective consciousness of such events. Irrespective of their origins, the consequences of these fires extend far and wide, affecting numerous facets of life. Studies are consistently highlighting the adverse effects of smoke on human health, tourism, property values, and the socioeconomic fabric at large.

The primary aim of this initiative is to scrutinize the health impacts of wildfire smoke on Farmington, New Mexico, with the objective of deriving actionable insights to guide diverse interested parties. Our preliminary step involves an examination of historical wildfire data to derive estimates of smoke penetration within the city's confines. Subsequently, leveraging these findings, we aim to forecast the likely smoke patterns for the forthcoming quarter-century. We then analyse how the health factors are impacted my the smoke.

## Licenses & API Information

The software code utilized for this initiative is distributed under the terms of the MIT license. For additional details, refer to the license document located in the repository's root directory. Data pertaining to Wildland Fires, provided by the USGS, are publicly available and not subject to copyright restrictions. Considering the size of the data, I have not included the file in the repository.
- Fire data: [USGS Wildfire data](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
- AQS API: [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)
- AQS API Key: Code 1.3_AQI_Data has instruction to create an account and make API calls. Please refer to that. Make sure to change the use your own USERNAME & APIKEY
- Mortality & Medicare Enrollees Data: [Dartmouth Atlas Data Terms of Use](https://data.dartmouthatlas.org/terms-of-use/) 
- Fertility Data: [U.S. Census Bureau's website](https://data.census.gov/table/ACSST1Y2022.S1301)

## Code
There are in total of 6 notebooks that are exected to run one after the other.
If you are reading the .json file, make sure to point the directory where the data resides by changing this line found in code 1.1: C:/Users/adith/Documents/data-512-common-analysis/Data/GeoJson_Exports/USGS_Wildland_Fire_Combined_Dataset.json
- [1.1_Data_Acquisition.ipynb](https://github.com/adithyaav27/data-512-common-analysis/blob/main/1.1_Data_Acquisition.ipynb) : Gets fire information for 1963-2020 within 1250 mile of Farmington, NM.
- [1.2_SmokeEstimateCalculation.ipynb](https://github.com/adithyaav27/data-512-common-analysis/blob/main/1.2_SmokeEstimateCalculation.ipynb) : Ideates and creates the Smoke Estimate for 1963-2020.
- [1.3_AQI_Data.ipynb](https://github.com/adithyaav27/data-512-common-analysis/blob/main/1.3_AQI_Data.ipynb) : Call the AQS API to get the Air Quality Index for Farmington and compares it with the Smoke Estimate.
- [1.4_Modelling.ipynb](https://github.com/adithyaav27/data-512-common-analysis/blob/main/1.4_Modelling.ipynb) : Creates a predictive model of the Smoke Estimate and forcasts the estimates for the next 25 years.
- [1.5_Report_Visualizations.ipynb](https://github.com/adithyaav27/data-512-common-analysis/blob/main/1.5_Report_Visualizations.ipynb) : Answers the Questions asked in Step 2 of common analysis Assignment on Canvas.
- [2_ImpactAnalysis](https://github.com/adithyaav27/data-512-final-project/blob/main/2_ImpactAnalysis.ipynb): Reads health realted variables, compares it with Smoke Estimate to understand the impact of smoke on the health of the people.
  
A dependant library class is available in [/wildfire](https://github.com/adithyaav27/data-512-common-analysis/tree/main/wildfire). This is imported within the notebooks.

## Inputs
- USGS_Wildland_Fire_Combined_Dataset.json: This dataset from the US Geological Survey (USGS) offers a detailed record of wildfire occurrences in the United States since 1963. It includes wildfire polygons and associated metadata, essential for analyzing and predicting smoke impact on Farmington. Utilizing historical fire data and ARIMA modeling, we aim to assess smoke impact metrics crucial for forecasting future air quality trends in Farmington. The dataset, a consolidation of 40 wildland fire datasets, focuses on fires within a 1250-mile radius of Farmington post-1963. It is freely redistributable, requiring only proper metadata and source acknowledgment to the USGS. 
  One can bbtain this JSON file from [USGS Wildfire data](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81).
  Retrieve the 'GeoJSON Files.zip' file.
  Extract the contents of this archive into a directory of your choice. You are expected to change the directory from which this particular data is read to run the codes.

- Air Quality Index: This dataset, accessed via an API from the EPA's Air Quality System database, contains historical and present Air Quality Index (AQI) measurements across the U.S. The AQI, ranging from 0 to 500, covers ground-level ozone, particle pollution, carbon monoxide, sulfur dioxide, and nitrogen dioxide levels. Focusing on AQI readings from San Juan County during fire seasons, this dataset is pivotal for correlating smoke estimates with actual air quality and potential health impacts. Usage guidelines and terms are available on the dataset's website listed above.

-  Fertility Data: Fertility data from the [U.S. Census Bureau's website](https://data.census.gov/table/ACSST1Y2022.S1301), specifically the American Community Survey (ACS), offers valuable insights into the potential health impacts of smoke exposure on maternal health and birth outcomes. Covering Farmington, NM from 2010 to 2021, this dataset provides detailed demographic information, including fertility rates. This data was downloaded manually. You can go to the website, filter for the City and select the year. Hit the download option to download the file. Each year has its own Excel file which we can extract. Data is available in this repository under /FOLDER. Key columns: Label (Name of the parameter), Estimate (Fertility Rate %).
  
- Mortality & Medicare Enrollees Data: This comprehensive dataset from the [Dartmouth Atlas Data Website](https://data.dartmouthatlas.org/mortality/#by-year) includes both Mortality Data and Medicare Enrollees Data, crucial for assessing healthcare impacts in Farmington related to smoke exposure. The Mortality Data, spanning from 1999 to 2019, provides detailed insights into death rates in Farmington, enabling an understanding of the health challenges and severity of smoke events. Meanwhile, the Medicare Enrollees Data for the same period offers a clear picture of the elderly population in Farmington. This is vital for evaluating the healthcare system’s capacity, especially during smoke events when elderly individuals are more susceptible to health effects. Every year has an excel file for all cities. We filter using a python program. Data is available in this repository under /FOLDER. Key columns: HSA Name (City name), Medicare Enrollees, Total Moratality Rate (%).

## Intermediate outputs
All of these files can be found under /intermediate folder. These are placed there because this is just part 1 of a project that will have a clearer deliverable.
1. [distance.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/distance.csv) - Produced by code 1.1, this has been generated by measuring the proximity of each fire within the composite USGS wildland fire dataset to Farmington, NM. It comprises two fields:
- OBJECTID, which denotes the unique identifier of the respective fire incident.
- shortest_dist, which indicates the minimum span separating the periphery of the fire from Farmington.

2. [closefires.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/closefires.csv) - Produced by code 1.1, this possesses identical categories to the previously mentioned one, however, it exclusively encompasses fire incidents that are situated within a 1250-mile radius of Farmington.

3. [features.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/features.csv) - Produced by code 1.1, this document extracts pertinent data regarding fire incidents post-1963 from the combined wildfire database maintained by the USGS, intended for subsequent utilization in generating smoke predictions. The dataset is structured with specific columns that include:
-  OBJECTID: A unique identifier for each fire event.
-  FireType: The category of the fire event recorded, with classifications such as wildfire, likely wildfire, uncertain but likely wildfire, prescribed fire, and uncertain but likely prescribed fire.
-  FireYear: The calendar year in which the fire occurred.
-  GISAcres: The measured area of the fire's geographic footprint, calculated via the Calculate Geometry function in ArcGIS Pro.
-  OverlapFlags: A designation for regions where there has been a recurrence of burning, exceeding 10% overlap of the original fire's area, within a one- or two-year timespan, as analyzed by the ArcGIS Tabulate Intersection Tool.

4. [finalfiresdata.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/finalfiresdata.csv): Produced by code 1.1, this document consolidates information regarding distances and characteristics to isolate specific data on fires that are situated within a 1250-mile radius of Farmington and transpired after 1963, including and beyond that year. The data fields included are:
-  OBJECTID: This is the unique identifier of each recorded fire event.
-  FireType: The category of the fire event recorded, with classifications such as wildfire, likely wildfire, uncertain but likely wildfire, prescribed fire, and uncertain but likely prescribed fire.
-  FireYear: The calendar year in which the fire occurred.
-  GISAcres: The measured area of the fire's geographic footprint, calculated via the Calculate Geometry function in ArcGIS Pro.
-  OverlapFlags: A designation for regions where there has been a recurrence of burning, exceeding 10% overlap of the original fire's area, within a one- or two-year timespan, as analyzed by the ArcGIS Tabulate Intersection Tool.
-  shortest_dist: It represents the minimum distance from the perimeter of the fire incident to Farmington, NM.

5. [annual_smoke_estimate.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/annual_smoke_estimate.csv): Created by code 1.2, this file provides yearly assessments of smoke levels for Farmington, NM. A reading of 0 signifies either an absence of smoke or a non-applicable measurement. The data is organized in two main columns:
- FireYear: Specifies the year of the fires.
- SmokeEstimate: Represents the average annual smoke calculations derived from periodic estimates throughout the corresponding year.
  
6. [daily_aqi.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/daily_aqi.csv): Produced within code 1.3, this is the raw data that is obtained from the API.
- site_number: Site location of each sensor.
- parameter_code: Which gas/particulate matter the sensor collects data for.
- sample_duration: The duration of the sample, 24 hour average data in out case.
- date_local: Timestamp of sample collection.

7. [yearly_aqi.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/yearly_aqi.csv): Produced within code 1.3, this file includes consolidated annual average Air Quality Index (AQI) data from all monitoring devices throughout San Juan County. The data is structured into 2 columns:
- year: Holds the specific twelve-month period in which AQI readings were gathered.
- yearly_avg_aqi: The mean AQI level calculated from all detectors in the county.

8. [SmokeEstimate_Features.csv](https://github.com/adithyaav27/data-512-final-project/blob/main/intermediate/SmokeEstimate_Features.csv): Result of code 2_ImpactAnalysis which is designed to assess the health effects of smoke estimates in Farmington, NM. This file includes the year wise values of SmokeEstimate, Average AQI, Medicare Enrollees data, Mortality Rate, Fertility Rate. It totally has 6 columns:
- year: Holds the specific Year value of the metric.
- SmokeEstimate: Smoke Estimates from [annual_smoke_estimate.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/annual_smoke_estimate.csv).
- yearly_avg_aqi: Air Quality Index from [yearly_aqi.csv](https://github.com/adithyaav27/data-512-common-analysis/blob/main/intermediate/yearly_aqi.csv).
- MedicareEnrollees: Total Number of people enrolled with Medicare.
- MortalityRate: Number of Deaths/Mortality Rate as a Percentage.
- FertilityRate: Number of births/Fertility Rate as a Percentage.

# Known Data Issues and Special Considerations
- The dataset from the United States Geological Survey (USGS) contains approximately 130,000 records of wildfires, with about 94,774 of these incidents taking place since 1963 and occurring within a 1,250-mile radius of Farmington, New Mexico.
- The USGS Wildland Fire Combined Dataset includes approximations of fire perimeters, with data pre-1980 likely underreporting fire occurrences.
- Fire boundaries are considered estimates, with the potential for numerous recording errors or omissions.
- The USGS dataset assumes land burns once per year; areas reported as burned more than once are counted as a single event.
- Fires in the dataset are classified as wild or prescribed based on the best available information, with some remaining uncertainties.
- A unified set of fields was created to standardize data from multiple sources, despite potential inconsistencies.
- Fire attributes in the dataset include a count of how often each entry appears to indicate data confidence levels.
- Data collection for the USGS dataset concluded in 2020.
- The fire distance calculation tool is limited to "ring" shaped fires; 36 "curve ring" shaped fires are incompatible and thus omitted.
- Air Quality Index (AQI) records from earlier periods can be intermittent. It has been observed that consistent and dependable AQI measurements from stations in Farmington, NM, commenced from 2005 onwards.
- AQI data is also restricted to the fire season for comparison with smoke estimates.
- The Fertility Rate data from the US Census might not of sampling errors. Especially during the 2020 COVID Pandemic.
- The Medicare Enrollees & Mortality data might have some sampling errors with a potential of bias. 

## Outputs
- [Q1.png](https://github.com/adithyaav27/data-512-common-analysis/blob/main/Images/Q1.png) : This graph depicts the cumulative acreage affected by wildfires each year within a 1,250-mile radius of Farmington, NM, over the period from 1963 to 2020.
- [Q2.png](https://github.com/adithyaav27/data-512-common-analysis/blob/main/Images/Q2.png) : This is a graphical representation that illustrates the spatial distribution of wildfires in relation to Farmington, NM, spanning the years 1963 to 2020.
- [Q3.png](https://github.com/adithyaav27/data-512-common-analysis/blob/main/Images/Q3.png) : This is a graph illustrating the comparison between the estimated yearly smoke levels and the annual Air Quality Index (AQI) during fire seasons, spanning from 2005 to 2020.
- [Step 3 Report.pdf](https://github.com/adithyaav27/data-512-common-analysis/blob/main/Step%203%20Report.pdf) This is a document containing in-depth analysis of the initial trio of diagrams presented, accompanied by a commentary reflecting on the findings.
