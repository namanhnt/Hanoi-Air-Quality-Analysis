# Hanoi Air Quality Analysis
![hoguom](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/ff3fa853-5be3-4ed9-8b22-bec9b6a01bfe)

*By Nam Aaron Nguyen*
## I. Introduction
My desire for researching Hanoi's air quality was sparked last year when I returned to Hanoi in October, during the worst AQI levels of the year. The air was thick and hard to breathe, and I found myself constantly checking the AQI on the IQAir app before going outside. Around that time, I also read an article from the [World Economic Forum](https://www.weforum.org/agenda/2020/10/as-a-chest-surgeon-i-see-the-effects-of-air-pollution-inside-every-patient/?utm_source=linkedin&utm_medium=social_video&utm_term=1_1&utm_content=28072_Indian_surgeon_polluted_lungs&utm_campaign=social_video_2023) that highlighted how air pollution affects every cell in the body. This could explain why so many residents of Hanoi experienced sore throats and illnesses from October to December 2023. Observing the severe impact of air pollution inspired me to start this project on Hanoi air quality analysis. My goal is to provide insights into the city's air pollution in the hope of helping people in my hometown become more aware and take appropriate measures in time to reduce their exposure to harmful air.

The project focuses on analyzing the Hanoi's Air Quality Index (AQI) and PM2.5 level from March 2023 to March 2024. Specifically, we will explore the effects of different weather conditions, seasonal variations, hourly patterns of pollution, and finally the time series analysis using ARIMA model. This README file acts as an abstract of the project. For further details on the methods and insights, please feel free to access my three Jupyter Notebooks.

## II. Background Study
For the past 45 years, the Air Quality Index (AQI), developed by [the United States Environmental Protection Agency (USEPA)](https://www.epa.gov/outdoor-air-quality-data/air-data-basic-information), has been offering vital information to the public about the state of air pollution. The Air Quality Index is based on measurement of Carbon Monoxide (CO), Nitrogen Dioxide (NO2), Ozone (O3), particulate matter (PM2.5 and PM10), Sulfur Dioxide (SO2). 

PM2.5, denoting particulate matter with a diameter of 2.5 micrometres or less, represents the primary health hazard and is frequently utilized as a criterion in regulatory air quality guidelines. According to [VnExpress](https://e.vnexpress.net/news/environment/hanoi-s-air-quality-dropping-over-large-scales-4719205.html), a research conducted by the Vietnam Ministry of Natural Resources and the Environment indicated that the air pollution in Hanoi mainly came from PM2.5 dusts which serverely impacted people's health.

According to 2019 World Air Quality Report by [IQAir](https://www.iqair.com/world-most-polluted-cities/world-air-quality-report-2019-en.pdf), the levels of PM2.5 have been grouped to determine the air quality status as follow:

![aqi](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/7a85dc63-d9f7-473b-821f-27769ef3d62d)

## III. Data Gathering
In this project, I will use data from [Weatherbit](https://www.weatherbit.io/), which offers a comprehensive suite of APIs providing high-resolution weather data. This data is sourced from satellites, radars, weather stations, and various sensors.

For air quality data and weather data, Weatherbit's API can retrieve historical AQI data on an hourly basis, with a custom date range of up to 30 days for any location. Specifically, I will be retrieving AQI data and weather data for Hanoi, Vietnam.

Regarding data gathering, I have set up a seperate notebook for this part named [Part 1 - Extract and Clean Data from API](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/blob/main/Part%201%20-%20Extract%20and%20Clean%20Data%20from%20API.ipynb). Feel free to access it to see my data extraction and wrangling process.

## IV. Results
### Exploratory Data Analysis
- **Hanoi Hourly AQI Level (From March 2023 to March 2024)**
![Hourlt AQI ](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/1fb4f644-fdf6-4831-95a5-462e212a3a88)

*From the graph, it can be seen that Hanoi's AQI fluctuates mostly in the range of 50-150 (Moderate to Unhealthy for Sensitive Groups). The figure rarely stayed in the Good level area (0-50). The index also had a high frequency of exceeding Unhealthy benchmark. Espescially, the figure was in Hazardous level (>300) at different timestamps from November to mid February, reaching its highest point throughout the year at 7pm February 2nd, 2024.*
*In general, Hanoi faced critical air poluttion in the last year, which might servely impact its cityzens' health.*

- **Hourly PM2.5 Concentration In the Day**
![Hourly PM2 5 Concentration](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/d5903994-b4f0-4c06-83df-15998ca61648)

*To identify the peak hours of PM2.5 concentration throughout the day, I first segmented the dataset by hour and computed the mean PM2.5 concentration for each hour. Based on this estimation, the peak PM2.5 levels were observed at 8 AM, 9 AM, 7 PM, 8 PM, and 9 PM. These hours coincide with peak traffic periods, suggesting that vehicular emissions significantly contribute to PM2.5 pollution. Notably, the PM2.5 concentration steadily accumulated over the course of the day, culminating in its highest peaks at 7 PM, 8 PM, and 9 PM, with levels reaching 55.19 μg/m³, 57.75 μg/m³, and 54.89 μg/m³ respectively.*


### Impact of Weather Conditions on Hanoi Air Quality

### PM2.5 Time Series Analysis

## V. Air Pollution Advisory



