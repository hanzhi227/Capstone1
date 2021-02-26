# Air Quality and Life Span Analysis in India

#### Galvanize DSI Capstone 1

#### Hanzhi Guo
------
## Motivation

The concern over air pollution's effects on health is a widely debated topic. The WHO estimates [7 million premature deaths annually due to air pollution](http://www.who.int/mediacentre/news/releases/2014/air-pollution/en/). That is quite concerning so let's dive in!

------
## What we are looking for?

1. Is there any correlation between air pollution and life span?
2. What specific factors may correlate with life span?
3. How has India's air quality changed over the years of 1987 and 2015?
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

![India Life Span Map](images/life_span_map.png)

![India SO2 Map](images/so2_map.png)

![India NO2 Map](images/no2_map.png)

![Air Quality By State](images/state_air_pollution.png)

![Air Quality Over Time](images/air_quality_over_time.png)

It seems that the tools for measuring smaller particulates were not available until recently. Let's see if we can predict the RSPM and PM<sub>2.5</sub> values based on the SPM history.

![Scatter Matrix](images/scatter_matrix.png)

![Air Quality Life Correlation by State](images/life_air_corr.png)

![RPSM vs PM2.5 Linear Regression](images/RPSMvsPM2_5LinReg.png)

By using linear regression, I was able to calculate the scaling factor between SPM, RSPM, and PM<sub>2.5</sub>

![Air Quality Over Time Predicted](images/air_quality_over_time_filled.png)

By using the linear scaling factors, I filled in the history of RSPM and PM<sub>2.5</sub>

![Correlation after prediction](images/life_air_corr_with_pm25_filled.png)


## Hypotheses Results

H<sub>0</sub>: There is not a correlation between Sulfur Dioxide and Life Span

H<sub>a</sub>: There is a correlation between Sulfur Dioxide and Life Span

![SO2 Life Correlation](images/bootstrap_SO2.png)

Even though there is a 87% chance that r < 0, 
r = 0 correlation lies within the 95% confidence interval thus we __fail to reject__ the __null__ hypothesis.

------
H<sub>0</sub>: There is not a correlation between Nitrogen Dioxide and Life Span

H<sub>a</sub>: There is a correlation between Nitrogen Dioxide and Life Span

![NO2 Life Correlation](images/bootstrap_NO2.png)

r = 0 correlation lies within the 95% confidence interval thus we __fail to reject__ the __null__ hypothesis.

------

## Conclusion

Within this data set, there is not enough evidence to prove that air pollution correlates with life span.

------
## Further Investigations

It is difficult to pinpoint the specific variables that may be affecting life span when the life span is given by state, thus it would be beneficial to look into more granular health data such as lung diseases, asthma, and life span by cities. 

------

## Data Sources
[India Air Quality](https://www.kaggle.com/shrutibhargava94/india-air-quality-data)

[India Life Expectancy](https://www.kaggle.com/nimishukey/life-expectancy-in-india)

[India Map](https://github.com/datta07/INDIAN-SHAPEFILES)

