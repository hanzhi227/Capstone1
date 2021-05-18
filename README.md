# Air Quality and Life Span Analysis in India

#### Galvanize DSI Capstone 1

#### Hanzhi Guo
------

<p align="center">
  <img width=100% src="https://github.com/hanzhi227/India-Air-Quality/blob/main/images/pollution.gif">
</p>


## Motivation

The concern over air pollution's effects on health is a widely debated topic. The WHO estimates [7 million premature deaths annually due to air pollution](http://www.who.int/mediacentre/news/releases/2014/air-pollution/en/). The most common metrics measured are SPM, RSPM, PM<sub>2.5</sub>, SO<sub>2</sub>, and NO<sub>2</sub>. Health issues tend to arise when these metrics become high. Let's see if air pollution has any effect on life span. Should there be drastic/urgent measures taken to lower pollution?

------
## What we are looking for?

1. What specific factors may correlate with life span?
2. Is there any correlation between air pollution and life span?
3. Is there statistically significant correlations between air pollution and life span?
4. How has India's air quality changed over the years of 1987 and 2015?
------

## Data

* SO<sub>2</sub>: [Sulfur Dioxide](https://www.cdc.gov/niosh/topics/sulfurdioxide/default.html)
  * Exposure may cause nasal mucus, choking, cough, and reflex bronchi constriction
* NO<sub>2</sub>: [Nitrogen Dioxide](https://www.epa.gov/no2-pollution/basic-information-about-no2)
  * Exposure may cause asthma and potentially increase susceptibility to respiratory infections
* PM<sub>2.5</sub>: [Particulate Matter less than 2.5 micron](https://drsiew.com/beating-the-haze-understanding-psi-pm-2-5/)
  * This is the most important indicator of air pollution that affects health
* RSPM: Respirable Suspended Particulate Matter (up to 100 micron)
  * RSPM and PM<sub>2.5</sub> can be inferred from SPM
* SPM: Suspended Particulate Matter (greater than 100 micron)
  * [More information on Suspended Particulates](http://www.dust-monitoring-equipment.com/suspended-particulate-matter-definition.pdf)
* Actual_Span: Actual Life Span of the avg citizen in India by state

------

## Methods Used
* Bootstrap
* Correlations
* Linear Regression
* Prediction

## Tools
* Numpy
* Pandas
* Matplotlib
* Geopandas
* Sklearn
------

## General Findings

Let's start with some GeoPandas heatmap map of SO<sub>2</sub>, NO<sub>2</sub>, and Life Span in each state in India. 

![India Life Span Map](images/life_span_map.png)

![India SO2 Map](images/so2_map.png)

![India NO2 Map](images/no2_map.png)

It is not clear whether there is any patterns/correlations just by looking at the map. The SO2 and NO2 map seem to not align visually with the Life Span map. Below is all of the states of India sorted by SPM measurement. 

![Air Quality By State](images/state_air_pollution.png)

![Air Quality Over Time](images/air_quality_over_time.png)

Looking at the data we see that RSPM and PM<sub>2.5</sub> are not quite full. RSPM is 100 microns and PM<sub>2.5</sub> is 2.5 microns. It seems that the tools for measuring smaller particulates were not available until recently. Widespread measurement of RSPM started around 2003 and PM<sub>2.5</sub> started by 2014; both of those metrics are better guages for health.

![Scatter Matrix](images/scatter_matrix.png)

Now we can see clearly that there is a correlation between NO2 and SO2 along with some other light correlations between the pollution measurements.

![Air Quality Life Correlation by State](images/life_air_corr.png)

![RPSM vs PM2.5 Linear Regression](images/RPSMvsPM2_5LinReg.png)

By using linear regression, I was able to calculate the scaling factor between SPM, RSPM, and PM<sub>2.5</sub>

![Air Quality Over Time Predicted](images/air_quality_over_time_filled.png)

Let's see if we can predict the RSPM and PM<sub>2.5</sub> using the nice full SPM data. From the reasearch I did about By using the linear scaling factors, RSPM and PM<sub>2.5</sub> be calculated if the ratios to SPM are known. Utilizing Linear Regression, fit and trained the model with SPM, RSPM, and PM<sub>2.5</sub> data, then I predicted the history data for RSPM and PM<sub>2.5</sub> using the model.


## Statistical Analysis of Correlations

![Correlations after prediction](images/life_air_corr_with_pm25_filled.png)

Looking at the correlations between Life Span and the different air pollution factors, it's clear that SO<sub>2</sub> has the strongest correlation and NO<sub>2</sub> has the weakest correlation. As a data scientist, we cannot rely on a correlation number to make statistical claims. Correlations have central tendency. We need to bootstrap the data and find the 95% confidence interval for the correlations. 

H<sub>0</sub>: There is not a correlation between Sulfur Dioxide and Life Span

H<sub>a</sub>: There is a correlation between Sulfur Dioxide and Life Span

![SO2 Life Correlation](images/bootstrap_SO2.png)

After bootstrapping 3000 samples and finding the correlations, we get this pearson r distribution. Even though there is a 87% chance that r < 0, 
r = 0 correlation lies within the 95% confidence interval thus we __fail to reject__ the __null__ hypothesis.

------
H<sub>0</sub>: There is not a correlation between Nitrogen Dioxide and Life Span

H<sub>a</sub>: There is a correlation between Nitrogen Dioxide and Life Span

![NO2 Life Correlation](images/bootstrap_NO2.png)

r = 0 correlation lies within the 95% confidence interval thus we __fail to reject__ the __null__ hypothesis.

------

## Conclusion

Within this data set, we cannot say with confidence that air pollution has any correlation with actual life span in India. 

------
## Further Investigations

There are so many factors that may be attributing to the Omitted Variable Bias. It is difficult to pinpoint the specific variables that may be affecting life span when the life span is given by state, thus it would be beneficial to look into more granular health data such as lung diseases, asthma, and life span by cities. 

------

## Data Sources
[India Air Quality](https://www.kaggle.com/shrutibhargava94/india-air-quality-data)

[India Life Expectancy](https://www.kaggle.com/nimishukey/life-expectancy-in-india)

[India Map](https://github.com/datta07/INDIAN-SHAPEFILES)

