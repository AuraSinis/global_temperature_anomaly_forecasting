## Global Temperature Anomaly: Time Series Modeling
#### Lucas Dwyer
##### https://github.com/AuraSinis/global_temperature_anomaly_forecasting
## Executive Summary
#### Problem Statement
         The potential impacts of climate change affect many facets of our everyday lives. <br>
         One important metric one can use to keep track of exactly how severely the climate has changed is the Global Temperature Anomaly (GTA), which is the rise in the global average temperature over the past few decades.<br>
         Forecasting the GTA years in advance is necessary in order to give prompt insight to policy makers regarding timetables for green climate policy changes. 
##### Objective
         Forecasting the annual global temperature anomaly and change in annual global temperature anomaly.
##### Data
    The data was free to download from government and educational entitites.
   <br> [Global Temperature Anomalies Dataset (NOAA)](https://www.ncdc.noaa.gov/cag/global/time-series/globe/land_ocean/ytd/12/1880-2020/data.csv)<br>
   <br> [World Methane Emissions Dataset (World Bank)](http://api.worldbank.org/v2/en/indicator/EN.ATM.METH.KT.CE?downloadformat=csv)<br>
   <br> [Global Annual Carbon ppm Historical Dataset (IAC)](ftp://data.iac.ethz.ch/CMIP6/input4MIPs/UoM/GHGConc/CMIP/yr/atmos/UoM-CMIP-1-1-0/GHGConc/gr3-GMNHSH/v20160701/mole_fraction_of_carbon_dioxide_in_air_input4MIPs_GHGConcentrations_CMIP_UoM-CMIP-1-1-0_gr3-GMNHSH_0000-2014.csv)
   <br>

##### Data Dictionary <br>
 This is the data dictionary (once the data has been aggregated in the $aggr$ dataframe.) 
<br>
| Feature                         | Feature              | Data Type | Description                                                                                                                   |   |
|---------------------------------|----------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------|---|
| Temporal Anomaly                | temp_anom            | float64   | Global Average Temporal Anomaly (Annual) ($ºC$)                                                                               |   |
| Temporal Anomaly 1st Difference | temp_a_diff_1        | float64   | Yearly Change in Global Average Temporal Anomaly (Annual) ($ºC/year$)                                                         |   |
| Temporal Anomaly 2nd Difference | temp_a_diff_2        | float64   | Yearly Change in the Yearly Change in Global Average Temporal Anomaly (Annual) ($ºC/(year^2)$)                                |   |
| World Methane                   | world_methane        | float64   | Global Methane emissions in equivalence to kilotons of CO2 (Annual) ($kt$)                                                    |   |
| World Methane 1st Difference    | world_methane_diff_1 | float64   | Yearly Change in the Global Methane emissions in equivalence to kilotons of CO2 (Annual) ($kt/year$)                          |   |
| World Methane 2nd Difference    | world_methane_diff_2 | float64   | Yearly Change in the Yearly Change in the Global Methane emissions in equivalence to kilotons of CO2 (Annual) ($kt/(year^2)$) |   |
| World Carbon                    | world_carbon         | float64   | Global Carbon levels in parts per million (Annual) ($ppm$)                                                                    |   |
| World Carbon 1st Difference     | world_carbon_diff_1  | float64   | Yearly Change in the Global Carbon levels in equivalence to kilotons of CO2 (Annual) ($ppm/year$)                             |   |
| World Carbon 2nd Difference     | world_carbon_diff_2  | float64   | Yearly Change in the Yearly Change in the Global Carbon levels in equivalence to kilotons of CO2 (Annual) ($ppm/(year^2)$)    |   |
| Target                          | target               | float64   | The Temporal Anomaly 1st Difference, shifted once (to be predicted). (For example, 2002 has 2003's _temp_a_diff_1_ as it's _target_.            |   |
##### Performance Metrics <br>
Mean Squared Error (MSE) is the primary metric considered for model benchmarking. <br>
##### Results <br>
A simple ridge regression model on some engineered dataset did well in predicting the change in annual global temperature anomaly, as well as annual global temperature anomaly itself. <br>
##### Limitations <br>
The model, while performing well, is fairly overfit.<br>
#### Technical Pertinents <br>
Jupyter Labs, statsmodels, and sklearn were the primary libraries used for the implementation. 
Models were evaluated by comparing their MSE scores against each other, and the R^2 values of each model on the testing and training data sets were used to examine for over/under fitting.

There are limited _novel_ inferential deductions to be made; the correlation between methane and carbon emissions, and global temperature anomalies, are well documented.


The first and second differences were taken of the three original features (global temperature anomaly, methane emissions, and carbon levels), and the target feature was taken as the shifted first difference of the global temporal anomaly (how much the global temporal anomaly will change between one year and the year after).
The ridge model was finally selected as it out-performed all the other models (although realistically it tied with the non-PCA implemented LASSO model).
Hyperparameters were tuned manually and through GridSearch().
