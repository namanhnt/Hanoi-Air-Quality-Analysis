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

- **Average PM2.5 Concentration per Season**
  
![Average PM2 5 Concentration per Season](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/75fb6eac-87dd-44d4-aeb6-66500ee17b21)

*To identify seasonal trends in PM2.5 level, I grouped the dataset by four seasons (**Spring**: February, March, April; **Summer**: May, June, July; **Autumn**: August, September, October; **Winter**: November, December, January) and computed the mean PM2.5 concentration for each season. Based on the estimation, winter observed the highest average PM2.5 concentration at 83.86 μg/m³ and it is the only season that has Pm2.5 level above Unhealthy benmarck. Spring and autumn figures are in Unhealthy for Sensitive Group range while summer average Pm2.5 level is in Moderate range.*
### Effect of Weather Conditions on Hanoi Air Quality
According to [VnExpress](https://e.vnexpress.net/news/environment/hanoi-s-air-quality-dropping-over-large-scales-4719205.html), it is indicated that the air pollution in Hanoi mainly came from PM2.5 dusts. Hence, I will choose PM2.5 as the variable measuring air quality. For the weather condition, I will choose precipitation, humidity, temperature, and wind speed as the weather condition variables.

- **Does Precipitation Affect Air Quality?**

***Relationship Between Precipitation Hours and PM2.5 Level***

![Precip Hours](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/e0ffc0cd-f761-4f84-8bf0-4f64452493fe)

**Observation:** *The visual representation illustrates a negative correlation coefficient of -0.12, suggesting a very low correlation, which may be considered insignificant. However, upon closer examination for trends and patterns, it becomes apparent that the more hours it rains, the less Pm2.5 pollutant it is. Thus, it can be inferred that as the duration of rainfall increases, the PM2.5 level tends to decrease.*

***Relationship Between Precipitation Amount and PM2.5 Level***

![Precip Amount](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/44f39e65-26b2-49d9-8f93-c03df719bfb6)

**Observation:** *The correlation between precipitation amount and PM2.5 is almost 0, this means that there is no linear relationship between the two variables. On looking for patterns, it is observed that for high amount of precipitation hours, there seem to be low level of PM2.5. It is safe to say that the more heavy it rains, the lower the PM2.5 level is.*

- **Does Pressure Affect Air Quality?**
  
![Pressure](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/f53eec3d-877e-48c6-ae69-9d70f559e75d)

**Observation:** *The correlation coefficient between atmospheric pressure and Pm2.5 level shows a figure of 0.3, indicating a moderate correlation. It becomes clear that the higher the pressure, the higher the Pm2.5 level. As explained by the [University Corporation for Atmospheric Research](https://scied.ucar.edu/learning-zone/air-quality/how-weather-affects-air-quality), low-pressure systems bring wet and windy conditions. A passing rain can wash pollutants out of the atmosphere or transport them to a new area, producing clear skies. In the contrary, high-pressure systems can lead to stagnant air, where pollutants such as vehicle and factory exhaust become concentrated as the air stops moving.*

- **Does Humidity Affect Air Quality?**
  
![Humidity](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/99104e87-7f8d-4eee-90e0-6eb00442741b)

**Observation:** *The correlation between humidity and the PM2.5 Level is almost zero, indicating no significant relationship. Upon examining the scatter plot, no clear pattern emerges, suggesting that humidity may not be a significant factor influencing PM2.5 levels.*

- **Does Temperature Affect Air Quality?**
  
![Temp](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/2673da09-9b3c-4939-8805-d64760b06afc)

**Observation:** *The graph depicted a negative correlation coefficient of -0.25, suggesting a low correlation between temperature and Pm2.5 index. However, upon closer examination for trends and patterns, the colder the temperature is, the higher the Pm2.5 level is.*
*[University Corporation for Atmospheric Research](https://scied.ucar.edu/learning-zone/air-quality/how-weather-affects-air-quality) explained that during the winter the layer of warm air acts like a lid, keeping cold air at the surface. This creates a thermal inversion, which forms when a layer of warm air above traps cool air and pollution close to the ground.*

- **Does Wind Speed Affect Air Quality?**
  
![Wind](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/e4d9a46d-c142-4a2f-a4cf-523b55954970)

**Observation:** *The graph showed a negative correlation coefficient of -0.16, suggesting a very low correlation, which may be considered insignificant. However, upon closer examination for trends and patterns, it illustrates that the more windy it is, the less Pm2.5 pollutant it is.*
*Explained by [IQAir](https://www.iqair.com/newsroom/wind-weather-air-pollution), when pollutants accumulate in an area, wind can play a crucial role in dispersing them, potentially reducing their concentration in that specific region. This process can also carry pollutants away from their original source, mitigating their impact over a larger area.*

### PM2.5 Time Series Analysis
ARIMA(5,1,1) was chosen as the best model for time series prediction. The model's mean absolute error (MAE) was lower than the MAE baseline. For evaluation, I used the Walk-forward Validation making predictions for the next time step and updating the model with the actual observation for that time step. The result is shown as the plot below:
![TIME SERIES](https://github.com/namanhnt/Hanoi-Air-Quality-Analysis/assets/139054152/a40b6e19-bf3f-49cd-bd5a-fb320183a986)

*The plot above shows the comparison between the PM2.5 test data and the Walk-Forward Prediction. The blue line represents the actual PM2.5 levels observed in the test dataset, while the orange line represents the predictions made by the ARIMA model using walk-forward validation.*

*From the graph, it is evident that the model's predictions closely follow the actual test data trends, capturing the significant peaks and troughs. This indicates that the model performs well in forecasting the PM2.5 levels, providing a robust and reliable prediction. The close alignment of the two lines suggests that the model is effective in capturing the underlying patterns and seasonality present in the time series data.*

## V. Air Pollution Advisory
According to [New York State Deparment of Health](https://www.health.ny.gov/environmental/indoors/air/pmq_a.htm#:~:text=Spend%20more%20time%20indoors.,air%20conditioning%20if%20you%20can.), if AQI is at unhealthy levels, several steps can be taken:

**If you are outdoor:**

- ***Wear masks:*** If going outdoors is unavoidable, consider wearing N95 or similar masks designed to filter out particulate matter from the air.

- ***Limit exertion:*** Avoid strenuous activities like running or cycling. Breathe shallowly if possible, as deep breaths bring in more polluted air.

- ***Carpool:*** Utilize personal vehicle sits to reduce PM2.5 in traffic.

**If you are indoor:**

- ***Close windows and doors:*** Windows and doors should be closed to prevent polluted air from outdoor entering.

- ***Use an air purifier:*** Consider using an air purifier in your home with a HEPA filter, which can effectively remove PM2.5 particles from the air.

<h1 align="center">**LASTLY, STAY SAFE AND KEEP OUR LUNGS HEALTHY EVERYONE!**</h1>
