# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 4: West Nile Virus - Outsmarting Outbreaks


Liyena | Marko | Munah | Tiffany

## Introduction



West Nile Virus is most commonly spread to humans through infected female mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from a persistent fever, to serious neurological illnesses that can result in death.

In 2002, the first human cases of West Nile virus were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today.

There are multiple ways to screen mosquitoes for WNV infection, cell culture is used to screen for the presence of cytopathic effect (CPE), a particular type of cell death that is a marker of viral infection. Collected mosquitoes are sorted by sex species, and pools of up to 50 mosquitoes per species per site are assembled. These mosquitoes are ground and inoculated into Vero cell cutlures. Cultures are checked days 3-7 post inoculation for signs of CPE.


## Problem Statement


The Chicago Department of Public Health has engaged our team, a Data Science Consultant, to develop a data-driven approach to optimize resource allocation and improve public health outcomes by evaluating the impact of interventions (such as spraying insecticides, larvicides and traps) on reducing the prevalence of West Nile virus. The objective is to develop a classification model to accurately predict the likelihood of West Nile Virus, and conduct a cost benefit analysis which will guide decisions on where and when to deploy resources. Hence, this will reduce the presence of West Nile Virus.

## Success Metrics

**AUC ROC** was selected as the success metric, as it shows how well the model distinguishes between areas with and without West Nile VIrus. It also considers inherent imbalances in the data set.

## Workflow Documentation


Project management was managed via Github Projects: https://git.generalassemb.ly/munah/Project4/projects/1

## Datasets Used


For the purpose of the analysis, we are provided with the `train`, `test`, `spray` and `weather` datasets. 

1. `train` dataset consists of data from 2007, 2009, 2011 and 2013. Dataset will be used for building of machine learning model
2. `test` dataset consists of data from 2008, 2010, 2012 and 2014. Dataset will be used for evaluation of model. 
3. `spray` dataset consists of Geographic Information Mapping (GIS) data for the spray efforts in 2011 and 2013. Spraying can reduce the number of mosquitos in the area, and therefore might eliminate the appearance of West Nile virus. 
4. `weather` dataset consists of weather conditions of 2007 to 2014, during the months of the tests. It is believed that hot and dry conditions are more favorable for West Nile virus than cold and wet. 

Please refer to data dictionaries below for the full infomation found in the datasets.



## Summary of Findings

**Light GBM** was the best model, with ROC-AUC score of 0.88 for `train` and 0.84 for `test` dataset


| **Model**                  | **Train Accuracy**   | **Test Accuracy**   |
|------------------------|--------------------|-------------------|
| **Light GBM**         | 0.88               | 0.84              |
| **XGBoost**            | 0.95               | 0.85              |
| **Random Forest**      | 0.99               | 0.84              |
| **Support Vector Machine** | 0.89            | 0.84              |
| **AdaBoost**           | 0.86               | 0.84              |
| **K-Nearest Neighbors** | 0.96             | 0.82              |
| **Logistic Regression** | 0.80              | 0.80              |
| **Gaussian Naive Bayes** | 0.79            | 0.79              |
| **Decision Trees (Baseline)** | 0.89        | 0.78              |

### Feature Importance

![](https://raw.git.generalassemb.ly/munah/Project4/main/images/prooject-4-feature-impt.png?token=AAAMBI3WYNUVXQUWZMNSR23FIOJY6 ) 

1. `Species`: Certain mosquito species like Culex Pipiens and Culex Restuans are more likely to carry the virus. Targeting their breeding grounds and spraying them may help to reduce the presence of west nile virus.
2. `Sunrise`: Sunrise times can affect daylight hours which may in turn affect mosquito activity and breeding patterns. This information can be used to time sprayings to coincide with peak mosquito activity periods.
3. `AddressAccuracy`: This feature suggests that areas with higher geolocation accuracy may be associated with more reliable data on WNV cases. This can lead to more effective targeting of resources.
4. `Direction`: To recap, direction is an engineered feature that captures the direction of the street. The orientation of the street may affect wind patterns and/or exposure to sunlight. Understanding these pattenrs may help in predicting outbreak locations and allow the health deapartment to focus on preventive measures.
5. `Year`: The year could show the effectiveness of spraying.

## Cost Benefit Analysis

A Cost Benefit Analysis was conducted to understand the importance of using a data-driven approach to tackle West Nile Virus.

|            | **$$ Per Year** |  |
|------------|--------------|---|
| Approach | **Current** | **Model-Driven** |
| **Cost of Spraying** | -1.2 MM USD (entire Chicago) | -0.0052 MM USD (5% of Chicago) |
| **Cost of Traps** | -0.045 MM USD | -0.045 MM USD |
| **Benefits from Medical Bills + Productivity** | +56 MM USD | +56 MM USD |
| **Net Benefit** | **+54.8 MM USD** | **+55.9 MM USD** |

Source: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3945683/


## Recommendations: Multiprong Approach to Combat WnV
1. Targeted Tier Response based on probability of Wnv
2. Impactful Public Education and Campaigns
3. Leveraging Technology: Drone Sprays

## Data Dictionary


<br>**Dataset name: `train`**

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|date|datetime|train| Date that the WNV test is performed.|
|address|string|train| Approximate address of the location of trap. This is used to send to the GeoCoder. |
|species|string|train| The species of mosquitos.|
|block|integer|train| Block number of address.|
|street|string|train| Street name.|
|trap|string|train| Id of the trap.|
|addressnumberandstreet|string|train| Approximate address returned from GeoCoder.|
|latitude|float|train| Latitude returned from GeoCoder.|
|longitude|float|train| Longitude returned from GeoCoder.|
|addressaccuracy|integer|train| Accuracy returned from GeoCoder.|
|nummosquitos|integer|train| Number of mosquitoes caught in this trap.|
|wnvpresent|integer|train| Whether West Nile Virus was present in these mosquitos. 1 means WNV is present, and 0 means not present.|

<br>**Dataset name: `test`**

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|id|string|test| The id of the record.|
|date|datetime|test| Date that the WNV test is performed.|
|address|string|test| Approximate address of the location of trap. This is used to send to the GeoCoder. |
|species|string|test| The species of mosquitos.|
|block|integer|test| Block number of address.|
|street|string|test| Street name.|
|trap|string|test| Id of the trap.|
|addressnumberandstreet|*string*|test| Approximate address returned from GeoCoder.|
|latitude|float|test| Latitude returned from GeoCoder.|
|longitude|float|test| Longitude returned from GeoCoder.|
|addressaccuracy|integer|test| Accuracy returned from GeoCoder.|

<br>**Dataset name: `spray`**

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|date|datetime|spray|The date and time of the spray.|
|time|string|spray|The date and time of the spray.|
|Latitude|string|spray|The Latitude of the spray.|
|Longitude|string|spray|The Longitude of the spray.|


<br>**Dataset name: `weather`**

| Feature | Type | Dataset | Description |
|:--|:-:|:-:|:--|
|station|integer|weather|Station ID.|
|date|datetime|weather|Date of the weather data.|
|tmax|integer|weather|Maximum temperature in Degrees Fahrenheit.|
|tmin|integer|weather|Minimum temperature in Degrees Fahrenheit.|
|tavg|integer|weather|Average temperature in Degrees Fahrenheit.|
|depart|integer|weather|Departure from normal temperature in Degrees Fahrenheit.|
|dewpoint|integer|weather|Average dew point in Degrees Fahrenheit.|
|wetbulb|integer|weather|Average wet bulb in Degrees Fahrenheit.|
|heat|integer|weather|Absolute temperature difference of average temperature (Tavg) from base 65 deg Fahrenheit for Tavg >=65|
|cool|integer|weather|Absolute temperature difference of average temperature (Tavg) from base 65 deg Fahrenheit for Tavg <=65|
|sunrise|string|weather|Sunrise timing in 24H format. (Calculated, not observed)|
|sunset|string|weather|Sunset timing in 24H format. (Calculated, not observed)|
|codesum|string|weather|Significant weather types.|
|depth|integer|weather|Snowfall in inches.|
|water1|integer|weather|Amount of water equivalent from melted snow.|
|snowfall|float|weather|Snowfall in precipitation.|
|preciptotal|float|weather|Water equivalent(Inches & Hundredths(2400 Local Standard Time). Rainfall & melted snow.|
|stnpressure|float|weather|Average station pressure. Inches of HG.|
|sealevel|float|weather|Average sea level pressure. Inches of HG.|
|resultspeed|float|weather|Resultant wind speed. Speed in miles per hour.|
|resultdir|float|weather|Resultant wind direction. To tens of degrees. Whole degrees.|
|avgspeed|float|weather|Average wind speed. Speed in miles per hour.|

---
