---
layout: default
hv-loader:
  hv-chart-1: ["charts/top-stations-hvplot.html", "700"] # second argument is the desired height
  hv-chart-2: ["charts/monthly-rider-hvplot.html", "900"] 
  hv-chart-3: ["charts/stations-rider-hvplot.html", "600"] 
  hv-chart-4: ["charts/importance-hvplot.html", "500"] 
  hv-chart-5: ["charts/food-bev-hvplot.html", "600"] 
altair-loader:
  altair-chart-1: "charts/monthly-rider-altair.json"
---

# Summary

- To better understand transit demand for the “L”, we examine the relationship between transit ridership and demographic and neighborhood characteristics.
- The top five predictive features of annual “L” ridership are log mean distance to food and beverage, log median income, log mean distance to offices, log mean distance to schools, and percent of population commuting to work by car. 
- To expand public transportation, policymakers could evaluate census tracts across the five most important features and plan for improved transportation access in those tracts with high potential transit demand. Alternatively, to create transit demand around particular stations, policymakers could focus on economic development of the food and beverage industry in those areas.

# Background

Access to reliable and efficient public transportation is integral to a city’s livability but understanding transit demand is challenging. Mass transit can support economic growth and productivity by reducing congestion and travel time to employment centers. It also supports social connectivity, including that of low-income groups who may not have the means for a private vehicle. Increasingly, mass transit also offers a more environmentally sustainable mode of transportation in an increasingly warming planet. However, as demographics shift within a city, the demand for public transportation may change accordingly. Predicting transit demand is thus an important tool for policymakers. 

For half a century, the city of Chicago has promised to extend its subway system into the “Far South Side” neighborhoods to increase transit accessibility. As of October 2022, the city is close to securing the required $3.6 billion to add 5.6 miles to the existing Red Line on Chicago’s subway system, the “L,” extending it from 95th/Dan Ryan to 130th Street with four new stops near 103rd Street, 111th Street, Michigan Avenue, and 130th Street. The Red Line Extension Project claims to increase equity, economic opportunity, and sustainable transportation. Yet critics say that the project “costs too much and does too little”.  

To better understand transit demand for the “L”, we examine the relationship between transit ridership and demographic and neighborhood characteristics. Using a supervised machine learning method called random forest, we predict transit ridership with particular attention to the proposed Red Line Extension Project. We combine US Census data at the census tract level, transit data from the Chicago Transit Authority (CTA), and data from Open Street Maps, relying on Python programming language throughout the analysis.

# Exploratory Analysis

## Total Ridership at 'L' Rail Stations in 2019

Below is a map of all 'L' rail stations, colored by the total ridership in 2019. Lighter colors indicate higher ridership counts.

<div id="hv-chart-3"></div>

## Top 20 Stations with Highest Annual Ridership in 2019

The stations with the highest annual ridership are Lake, Clark/Lake, Chicago, Washington, and O’Hare. Except for O’Hare, four of the top five stations are located in the center of Chicago, an area with employment centers and where multiple rail lines converge (“The Loop”). The Red Line terminus at 95th/Dan Ryan was the 14th most transited station in 2019, out of 144 stations, with over 2.8 million riders.

<div id="hv-chart-1"></div>

## Monthly Ridership by Station

Below is a heatmap of the monthly ridership for each 'L' station in 2019. Lighter colors indicate higher ridership counts here as well.

<div id="hv-chart-2"></div>

# Overview of Methods

We use census tract level data all from 2019 to avoid any anomalies in travel patterns related to the COVID-19 pandemic. To load demographic data, we access the US Census API using the cenpy package and query 2019 data from the American Community Survey including:

- total population
- total number employed
- total population 25 years and older with college education
- estimated labor force population
- median income in the past 12 months
- household size by vehicles available
- number of vehicles used by workers ages 16 and older
- aggregate travel time to workplace in minutes
- total number commuting to workplace by car
- total number by means of transportation to work
- median house value in dollars
- total white population

The listed variables were chosen based on prevailing knowledge of the relationship between public transportation ridership in urban areas and certain indicators. For transit data, we accessed Chicago’s Open Data Portal through the API and filtered for 2019 data. We accessed the API for Open Street Maps and queried for several amenities within the Cook County boundary: restaurants, pubs, bars, schools, and offices. 

We rely on a variety of packages to visualize each variable, particularly hvplot and altair. To create a random forest model, we use RandomForestRegressor from the scikit-learn package. RandomForestRegressor is a meta estimator that fits classifying decision trees on various iterations of the input features (predictors). The estimator utilizes averaging to improve the predictive accuracy. Our label feature, or dependent variable, is Annual Ridership. 

To prepare the data for the random forest model, we use a preprocessor transformer from the scikit-learn package. We split the dataset into a training set and a test set. Because there are relatively few observations (n=144), we use a 60-40 split instead of 70-30 to give the test set more random variation. We develop and run three regression models (linear, two-step random forest, and optimized random forest) to understand the random forest model’s relative accuracy. 

# Results

Upon running the model, we found that including only demographic and transit data in the optimized random forest model resulted in a R2 (test score) of only 0.17. To potentially increase the accuracy of the model, we experimented with adding distance-based features from restaurants, pubs, bars, schools, and offices. Checking for multicollinearity among all features, we found that the following features did not have severe multicollinearity.

The optimized random forest model produced a best estimator of 0.171, with 200 estimators and a maximum depth of 5 in the decision tree. The optimized random forest model’s average absolute error (AAE) is 636736.63 with an accuracy of 25.86%. 

## Mean Percent Error

The highest percent errors (>400%) are for stations along the Purple Line, an extension of the Red Line. The lower percent errors are in areas known as food and beverage destinations, such as the Loop and West Loop, as well as near universities such as Northwestern University in Evanston, and the University of Chicago on the South Side. 

## Top 5 Importance Features

The top five predictive features of annual “L” ridership are log mean distance to food and beverage, log median income, log mean distance to offices, log mean distance to schools, and percent of population commuting to work by car. The distance to food and beverage holds the most predictive power compared to the other features in the model.

<div id="hv-chart-4"></div>

Below is a map of all 'L' rail stations, colored by the total ridership in 2019. Lighter colors indicate longer distances to the nearest restaurants, pubs, or bars from the station. Outside of the city center, stations in neighborhoods to the north are closer to food and drink places than those in neighborhoods to the south. The Red Line terminal station at 95th/Dan Ryan has the third farthest distance from the nearest food and drink places out of 144 stations.

<div id="hv-chart-5"></div>

# Policy Implications

The stations with the highest annual ridership are Lake, Clark/Lake, Chicago, Washington, and O’Hare. Except for O’Hare, four of the top five stations are located in the center of Chicago, an area with employment centers and where multiple rail lines converge (“The Loop”). The Clark/Lake station, for example, connects six different rail lines. To expand public transportation, policymakers could evaluate census tracts across the five most important features and plan for improved transportation access in those tracts with high potential transit demand. Alternatively, to create transit demand around particular stations, policymakers could focus on economic development of the food and beverage industry in those areas. 

Although the Red Line terminal station at 95th/Dan Ryan was the 14th most transited station in 2019, yet the 142nd closest to food and drink establishments, our model is unlikely to explain the predictors of ridership at this station.

## Limitations

The major limitation of the study relates to data wrangling. More datasets and feature engineering would improve the model’s accuracy and robustness. Features that could be included in future analysis are crime data, employment types, airport (O’Hare and Midway) locations, and rideshare data. Additionally, because Chicago has a robust bus and commuter rail system, these stops and stations could be added to the model to include more census tracts into the dataset and calculate the spatial lag of nearby stops and stations. Nonetheless, this analysis is useful as a starting point for further research into expanding public transit in Chicago and is timely in its discussion of the ongoing Red Line Expansion project. A model with increased accuracy and generalizability could enable predictive modeling across other comparable urban spaces.

### Sources
Chicago Transit Authority (CTA). (2022). Facts at a glance. Transit Chicago. https://www.transitchicago.com/facts/ 
Chicago Transit Authority (CTA). (2022). Red Line Extension Project. Transit Chicago. https://www.transitchicago.com/rle/ 
CURBED Chicago. (2019, March 10). Chicago’s traffic was the second worst in the nation in 2019, says report. CURBED. https://chicago.curbed.com/2019/2/14/18224967/chicago-traffic-report-worst-nation-transportation 
Evans, M. (2022, August 2). Far South Siders have been promised a Red Line extension for 50 years. Now, the CTA says it’s closer than ever to happening. Block Club Chicago. https://blockclubchicago.org/2022/08/02/far-south-siders-have-been-promised-a-red-line-extension-for-50-years-now-the-cta-says-its-closer-than-ever-to-happening/
Zotti, E. (2022, November 23). Opinion: The Red Line extension costs too much and does too little. CRAIN’s Chicago Business. https://www.chicagobusiness.com/opinion/opinion-cta-red-line-extension-too-expensive 


## Percentage of Households without Internet

The percentage of households without internet by county:

<div id="folium-chart-2"></div>

See the [lecture 9B slides](https://musa-550-fall-2022.github.io/slides/lecture-9B.html) and the [lecture 10A slides](https://musa-550-fall-2022.github.io/slides/lecture-10A.html) for the code that produced these plots.
