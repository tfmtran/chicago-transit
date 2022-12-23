---
layout: default
hv-loader:
  hv-chart-1: ["charts/top-stations-hvplot.html", "500"] # second argument is the desired height
  hv-chart-2: ["charts/monthly-rider-hvplot.html", "800"] 
  hv-chart-3: ["charts/stations-rider-hvplot.html", "500"] 
altair-loader:
  altair-chart-1: "charts/monthly-rider-altair.json"
---

# Summary



# Background

Access to reliable and efficient public transportation is integral to a city’s livability but understanding transit demand is challenging. Mass transit can support economic growth and productivity by reducing congestion and travel time to employment centers. It also supports social connectivity, including that of low-income groups who may not have the means for a private vehicle. Increasingly, mass transit also offers a more environmentally sustainable mode of transportation in an increasingly warming planet. However, as demographics shift within a city, the demand for public transportation may change accordingly. Predicting transit demand is thus an important tool for policymakers. 

For half a century, the city of Chicago has promised to extend its subway system into the “Far South Side” neighborhoods to increase transit accessibility.  As of October 2022, the city is close to securing the required $3.6 billion to add 5.6 miles to the existing Red Line, extending it from 95th/Dan Ryan to 130th Street with four new stops near 103rd Street, 111th Street, Michigan Avenue, and 130th Street. The Red Line Extension Project claims to increase equity, economic opportunity, and sustainable transportation.  Yet critics say that the project “costs too much and does too little”.

To evaluate these claims, we examine the relationship between demographic characteristics and transit ridership. Using a supervised machine learning method called Random Forest, we predict transit ridership on Chicago’s subway system, the “L,” with particular attention to the proposed Red Line Extension Project. We combine US Census data at the census tract level, transit data from the Chicago Transit Authority (CTA), and data from Open Street Maps, relying on Python programming language throughout the analysis.

## Total Ridership at 'L' Rail Stations in 2019

Below is a chart of the total ridership for each 'L' station in 2019.

<div id="hv-chart-3"></div>

## Top 20 Stations with Highest Annual Ridership

The Red Line terminus at 95th/Dan Ryan was the 14th most transited station in 2019, out of 144 stations, with over 2.8 million riders.

<div id="hv-chart-1"></div>

## Monthly Ridership by Station

Below is a chart of the monthly ridership for each 'L' station in 2019.

<div id="hv-chart-2"></div>

## Notes

- See the [lecture 13A slides](https://musa-550-fall-2022.github.io/slideslecture-13A.html) for the code that produced these plots.

**Important: When embedding charts, you will likely need to adjust the width/height of the charts before embedding them in the page so they fit nicely when embedded.**

# Example: Embedding Folium charts

This post will show examples of embedding interactive maps produced using [Folium](https://github.com/python-visualization/folium).

## OSMnx and Street Networks

The shortest route between the Art Museum and the Liberty Bell:

<div id="folium-chart-1"></div>

<br/>

## Percentage of Households without Internet

The percentage of households without internet by county:

<div id="folium-chart-2"></div>

See the [lecture 9B slides](https://musa-550-fall-2022.github.io/slides/lecture-9B.html) and the [lecture 10A slides](https://musa-550-fall-2022.github.io/slides/lecture-10A.html) for the code that produced these plots.
