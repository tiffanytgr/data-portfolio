# Optimizing Manpower Allocation for STB 

<img src="https://git.generalassemb.ly/tiffanytgr/dsif-tiffany/blob/557e20c56a52fba2d42c41de16a09cfd9cfbc1bc/Homework/project_1_optimizing-manpower-expenses-using-rainfall/data/Singapore_Tourism_Board_text_logo.svg.png" alt="Singapore Tourism Board Logo" width="200"/>

# Introduction

Singapore Tourism Board (STB) faces a significant increase in operating expenses, leading to a growing deficit. To avoid potential attraction closures, STB aims to reduce manpower costs, particularly at the Singapore Zoo and Science Center. The objective is to **explore the correlation between weather data and visitor numbers, to adjust number of staff on shift**. This enables STB to optimize expenditure on manpower while maintaining same customer service quality levels.

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Problem Statement](#problem-statement)
- [Data Processing / EDA](#data-processing--eda)
- [Limitations](#limitations)
- [Conclusions / Recommendations](#conclusions--recommendations)
- [Author](#author)

# Problem Statement
This project aims to understand the correlation between the weather (rainfall, humidity, temperature) and the number visitors to the Singapore Zoo and Science Centre.

- **Correlation**: Is there any correlation between total rainfall and the number visitors to the Singapore Zoo and Science Centre?
- **Difference in Impact**: Given that the Singapore Zoo is an outdoor attraction, does the total rainfall have a greater influence on its number of visitors as compared to the Science Centre?
- **Other Predictors**: Are there any other weather features that might be a predictor of number of visitors to both attractions?


[(Back to top)](#table-of-contents)

All weather datasets come from [Data.gov.sg](#https://beta.data.gov.sg/), and outdoor activities dataset come from [Singstat](#https://www.singstat.gov.sg/find-data/search-by-theme/society/culture-and-recreation/latest-data).

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**year_month**|*float*|all|Year and month of data collection|
|**year**|*integer*|all|Year of data collection| 
|**month**|*integer*|all|Month of data collection| 
|**no_of_rainy_days**|*integer*|number-of-rainy-days|Number of days that rained (day with rainfall amount of 0.2mm or more) in a month recorded at the Changi Climate Station| 
|**total_rainfall**|*float*|rainfall-monthly-total|Total rainfall in mm recorded at the Changi Climate Station| 
|**mean_rh**|*float*|relative-humidity-monthly-mean|Monthly mean relative humidity recorded at the Changi Climate Station (units in percentage, where 80 represents 80%)| 
|**temp_mean_daily_min**|*float*|surface-air-temp-monthly-mean|Monthly mean air temperature recorded at the Changi Climate Station (units in degrees celcius)| 
|**mean_sunshine_hrs**|*float*|sunshine-duration-monthly-mean-daily-duration|Monthly mean sunshine hours in a day recorded at the Changi Climate Station| 
|**zoo_visitor_ct**|*float*|outdoor-activites-singapore|Total number of visitors to the zoo (units in thousands, where 2.5 represents 2500 people)| 
|**sci_centre_visitor_ct**|*float*|outdoor-activites-singapore|Total number of visitors to the science centre (units in thousands, where 2.5 represents 2500 people)| 



[(Back to top)](#table-of-contents)

# Data Processing / EDA
- No null values so no rows were dropped
- Filtered data to only 2010 to 2019 due to Covid
- Filtered data to exclude holiday months (June and December) as number of visitors is independent of weather data, and remains consistently high due to people's availability (school holiday for locals, increase in tourism during these months*)

[(Trend of number of tourists across months)](#https://stan.stb.gov.sg/public/sense/app/877a079c-e05f-4871-8d87-8e6cc1963b02/sheet/3df3802e-2e5b-4c79-950d-d7265c4c07a9/state/analysis) 

[(Back to top)](#table-of-contents)

# Limitations
- **Black Swan Events**: Covid-19 resulted in a closure of tourist attractions across Singapore, slow economic recovery and limited global travel. Might have long term effects too.
- **Marketing Campaigns**: Successful marketing efforts might have the potential to influence visitors' arrivals despite bad weather. Not accounted for in data.


[(Back to top)](#table-of-contents)

# Conclusions / Recommendations
#### Conclusions
  -  Strong negative correlation between total rainfall and  no. of visitors to the zoo.
- Removing holiday months (June and Dec) strengthens the negative rainfall-visitor correlation
- Positive Correlation between Mean sunshine hours and visitors to the Zoo

#### Recommendations
- Focus on optimising manpower in the zoo using rainfall data as there is a strong negative correlation between rainfall and zoo
- Other than holiday months, assign less manpower during wetter months
- Cut costs by reducing outdoor shows during wetter months as these require specialized trainers and are expensive
- For drier months and holiday months with expected high number of visitors, STB can leverage technology to empower staff such as through digitising ticketing counters & employing robot navigators, etc.

[(Back to top)](#table-of-contents)


## Author

- [Tiffany Tan](https://www.linkedin.com/in/tiffanytan-gr/)


