# West Nile Virus Prediction

GA Group Project 4 - Edward, Derrick, Tresha

### 1) Problem Statement

We are a group of data scientists working who just started work at the Disease And Treatment Agency, division of Societal Cures In Epidemiology and New Creative Engineering (DATA-SCIENCE). Due to the recent epidemic of West Nile Virus in the Windy City, we've been tasked by the Department of Public Health to build a classifer model to predict the possibility of west Nile Virus occuring on various locations of interest based on the data collected over time. It is our hope that with the model, we could make more informed decisions on the deployment of pesticides in the fight for public health and safety. While pesticides are a necessary evil in the fight against the West Nile Virus, it is very expensive. At such, we will also conduct a cost-benefit analysis regarding use of pesticides to manage the epidemic.

### 2) Background

According to the Centers for Disease Control and Prevention, the West Nile virus (WNV) is the leading mosquito-borne disease in the United States ([*Source: CDC, 2009*](https://www.cdc.gov/westnile/index.html)).It is most commonly spread to people by the bite of an infected mosquito. Cases of WNV occur during mosquito season, which starts in the summer and continues through fall. There are no vaccines to prevent or medications to treat WNV in people. Fortunately, most people infected with WNV do not feel sick. About 1 in 5 people who are infected develop a fever and other symptoms. About 1 out of 150 infected people develop a serious, sometimes fatal, illness. People can reduce their risk of WNV by using insect repellent and wearing long-sleeved shirts and long pants to prevent mosquito bites. This is essential as the medical costs can be outstanding especially if the disease progresses and causes neurological symptoms.

### 3) Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|Id|Int|Test.csv|ID number of the record|
|Date|Datetime|Train.csv/Test.csv|Date and time WNV test was performed|
|Address|Str|Train.csv/Test.csv|Approx. address for trap|
|Species|Str|Train.csv/Test.csv|Species of mosquitoes in trap|
|Block|Int|Train.csv/Test.csv|Block number of address|
|Street|Str|Train.csv/Test.csv|Street of address|
|Trap|Str|Train.csv/Test.csv|ID number of trap|
|AddressNumberAndStreet|Str|Train.csv/Test.csv|Approx. address|
|Latitude|Float|Train.csv/Test.csv|Latitude from GeoCoder|
|Longitude|Float|Train.csv/Test.csv|Longitude from GeoCoder|
|AddressAccuracy|Int|Train.csv/Test.csv|Accuracy of info from GeoCoder|
|NumMosquitos|Int|Train.csv|Number of mosquitoes in sample
|WnvPresent|Int|Train.csv|Whether WNV is present in a sample (1 = present; 0 = absent)|
|Date|Datetime|Spray.csv|Date of spray|
|Time|Datetime|Spray.csv|Time of spray|
|Latitude|Float|Spray.csv|Latitude of spray|
|Longitude|Float|Spray.csv|Longitude of spray|
|Station|Int|Weather.csv|Weather station (1 or 2)|
|Date|Datetime|Weather.csv|Date of measurement|
|Tmax|Int|Weather.csv|Maximum daily temperature (F)|
|Tmin|Int|Weather.csv|Minimum daily temperature (F)|
|Tavg|Int|Weather.csv|Average daily temperature (F)|
|Depart|Int|Weather.csv|Departure from normal temperature (F)|
|Dewpoint|Int|Weather.csv|Average dewpoint (F)|
|WetBulb|Int|Weather.csv|Average wet bulb|
|Heat|Int|Weather.csv|Heating degree days|
|Cool|Int|Weather.csv|Cooling degree days|
|Sunrise|Int|Weather.csv|Calculated time of sunrise|
|Sunset|Int|Weather.csv|Calculated time of sunset|
|CodeSum|Str|Weather.csv|Code of weather phenomena|
|Depth|Int|Weather.csv|Snow Depth in inches|
|Water1|Int|Weather.csv|Amount of water from melted snow|
|SnowFall|Int|Weather.csv|Snowfall(inch)|
|PrecipTotal|Str|Weather.csv|Total daily rainfall (inch)|
|StnPressure|Int|Weather.csv|Average atmospheric pressure (inch Hg)|
|SeaLevel|Int|Weather.csv|Average sea level pressure (inch Hg)|
|ResultSpeed|Float|Weather.csv|Resultant wind speed (mph)|
|ResultDir|Int|Weather.csv|Resultant wind direction (degrees)|
|AveSpeed|Int|Weather.csv|Average wind speed (mph)|

### 4) Notebooks
1) Notebook (1): Problem Statement and EDA
2) Notebook (2): Modelling, Cost-Benefit Analysis and Executive Summary

### 5) Modelling Summary

**Summary table for Models**

| Model| Train Accuracy|Test Accuracy|   Sensitivity | Baseline acc|True Pos |False Pos|False Neg|True Pos|
|:---------:|:---:|:--------:|:-------:|:----------:|:-----:|:----------:|:-----:|:-------:|
KNearest Neighbours|1.0|0.9476|0.0563|0.0539|5284|8|285|17|
Support Vector Machine|0.9471|0.9458|0.0033|0.0539|5290|8|301|1|
Logistic Regression|0.9488|0.9480|0.0762|0.0539|5280|12|279|23|
Random Forest| 0.9957|0.9544|0.4172|0.0539|5213|79|176|126|
Extra Trees| 0.9521|0.9097|0.6126|0.0539|4904|388|117|185|

### 6) Cost-Benefit Analysis and Executive Summary
**Costs**

Based on external research, we found that: 
- Spraying typically takes place around 8pm until 1am using trucks which dispense an ultra-low-volume spray [*(Source: Chicago city website)*](https://www.chicago.gov/city/en/depts/cdph/provdrs/healthy_communities/news/2020/aug[…]t/city-to-spray-insecticide-thursday-to-kill-mosquitoes0.html). With the spraying done at odd hours, the chances of human interaction with the insectide are greatly reduced.
-Spray rate is about 1.5 ounces per acre [*(Source: ABC7Chicago)*](https://abc7chicago.com/archive/9206273/)
- Cost per gallon (128 ounces) of Zenivex (i.e. insecticide used) is approximately USD300 [*(Source)*](http://www.gfmosquito.com/wp-content/uploads/2017/07/2017-ND-Mosq.-Control-Quotes-Tabulation.pdf)
- Size on entire chicago is about 149,800 acres in area

Assuming that we want to spray the whole of Chicago,(with an area of 149800 acres) we will need:
- spray amount = 149800/1.5 => 99866.67
- spray amount in gallons= 99866.67/128 => 780.21
- cost of procuring Zenivex = 780.21*300 => $234,062 (for spraying the whole of Chicago once)

If we want to spray the whole of Chicago once every fortnightly for a duration of 6 months (including the summer months), this works out to be: 

- Annual spray cost =  $2,808,744 (i.e. 234,062 * 12)

**Benefits**


|Cost category| Mean| 95% CI| Median |Range |Chicago Mean cost |Chicago cost range estimated |
|:---------:|:---:|:---------:|:---:|:---:|:---:|:---:|
|Total acute medical care |252,115,100 |158,022,000–458,998,400| 230,879,300| 115,644,400–2,822,846,000|2,068,705|948,908-23,162,580|
|Total acute lost productivity†| 22,081,260 |9,550,370–63,069,700| 16,144,050 |7,070,480–2,643,251,000|181,185|58,016-21,688,931|
|Total long-term medical care |27,570,280| 11,566,780–56,221,870| 25,468,510| 6,087,800–118,883,900|226,225|49,953-975,489|
|Total long-term lost productivity| 26,866,800 |13,526,800–48,279,320| 25,416,720| 7,790,800–85,567,700|220,452|63,927-702,117|
|Total lifetime lost productivity caused by deaths‡ |449,464,800| (NA)| 449,464,800 | (NA)|3,688,038|NA|

the important takeaway from our external research is that the benefits of fogging the entire City of Chicago greatly outweights the cost ($2.8mil vs $6.38)
. Specifically, there are huge savings re hospitalisation bills that we can reap if we manage to eradicate the West Nile Virus via fogging of entire Chicago city once every fortnightly for 6 months. 

**Executive summary**

Having evaluate five models for our classifier (i.e. KNN, SMV, Log Reg, Random Forest and Extra Trees), their respective scores are as such:

| Model| Train Accuracy|Test Accuracy|   Sensitivity | Baseline acc|True Pos |False Pos|False Neg|True Pos|
|:---------:|:---:|:--------:|:-------:|:----------:|:-----:|:----------:|:-----:|:-------:|
KNearest Neighbours|1.0|0.9476|0.0563|0.0539|5284|8|285|17|
Support Vector Machine|0.9471|0.9458|0.0033|0.0539|5290|8|301|1|
Logistic Regression|0.9488|0.9480|0.0762|0.0539|5280|12|279|23|
Random Forest| 0.9957|0.9544|0.4172|0.0539|5213|79|176|126|
Extra Trees| 0.9521|0.9097|0.6126|0.0539|4904|388|117|185|

As we are concerned about correctly identifying the presence of the West Nile Virus, we have predominantly used the test accuracy score to choose the best performing model. Notwithstanding this, we also looked at the sensitivity score so as to ensure that we keep our false positives to a minimum. Taking these two evaluation metrics into account, we observed that our Random Forest model is the most ideal (i.e. test accuracy of 0.9544 and sensitivity of 0.4172).

This goes to suggest that our model predicts 95.44% of the test observations correctly. Among obsevations that have the West Nile Virus, our model has 41.72% of them classified accurately.

Re cost-benefit analysis, our earlier paragraph shows that the cost of spraying the whole of Chicago fortnightly for 6 months (including the summer months) will cost about $2.8mil. This is far lower that the total estimated hospitalisation costs (see figures under "Chicago Mean Cost" from table above) from West Nile Virus and demonstrates a clear impetus for the city of Chicago to spray insecticide city-wide to reduce the spread of the virus.
