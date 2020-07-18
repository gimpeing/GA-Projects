# ![GA Logo](https://camo.githubusercontent.com/6ce15b81c1f06d716d753a61f5db22375fa684da/68747470733a2f2f67612d646173682e73332e616d617a6f6e6177732e636f6d2f70726f64756374696f6e2f6173736574732f6c6f676f2d39663838616536633963333837313639306533333238306663663535376633332e706e67) 


# Project 4: Kaggle Competition: West Nile Virus Prediction


Group 6: Wilson, Joey, GimPei


---

## Context and Problem Statement

West Nile virus is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from a persistent fever, to serious neurological illnesses that can result in death. 

In 2002, the first human cases of West Nile virus were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today. 

Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

There is a great deal of variation in outbreaks of West Nile Virus (WNV) intensity and duration year to year, which makes it difficult to predict outbreaks and concentrate on containing the spread of WNV.

Given weather, location, testing, and spraying data, the goal of this project is to build a **classification model** to **predict outbreaks of WNV from mosquitos**. This will help the City of Chicago and CDPH more efficiently and effectively allocate resources towards preventing transmission of this potentially deadly virus.


## Executive Summary

### Contents

- [Data Collection](#Data-Collection)
- [Data Cleaning and Exploratory Data Analysis (EDA)](#Data-Cleaning-and-Exploratory-Data-Analysis-(EDA))
- [Preprocessing](#Preprocessing)
- [Modelling](#Modelling)
- [Model Evaluation](#Model-Evaluation)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [Sources](#Sources)

### Data Collection
**Data Collection** is done by retrieving the datasets in Kaggle and upload it into our github's directory name's **assets/west_nile**. We can import the datasets for data cleaning, EDA and modelling.

### Data Cleaning and Exploratory Data Analysis (EDA)
Cleaning involved imputing missing value with mean data, converting `Date` to `datetime` datatype for time series data exploration, dropping unwanted prediction variables, which does not appear in test dataset.

EDA is carried out on the train dataset, and weather dataset. The train dataset is highly imbalanced as the WNV infection is only make-up to about **5%** of the dataset. Remaining datasets are without WNV infection. 

|WnvPresent|Normalized Counts|
|---|---|
|1|0.052446|
|0|0.947554|

Number of mosquitos increases the probability of WNV infection. The number of mosquitos peaks on June and reduces as the summer progresses. In addition, different years have different number of mosquitos detected with highest record in 2007. 

Among the 6 mosquitos' species detected, only 3 species are prevalent and 2 species (**Culex Pipiens, Culex Restuans**) have high number of WNV infection. In fact, species **Culex Pipens / Restuans** while classfied as the 3rd species, might only be a mixture of the 2 species, wherein it is difficult to determine which species the mosquito belongs to.

Higher temperature, lower rainfall, and lower wind speed tends to have more WNV infection.

Cleaning, EDA and Munging of Spray Data together with Train Data revealed the following:

1.  There were about 541 purely duplicated datarows of spray data, which were removed.

2a. Using a mixture of geo-mapping, timestamps and coordinate distance, as the coords of spray points seem to differ fully even across different dates, there do not seem to be fixed spray points.

2b. Based on some preliminary data of travel speed of 400m every 10 secs, travel speed works out to ~14.4km/h. Assumption is made that it is a land vehicle, and given the regularity of the data of seemingly 10 secs apart, it seems likely that spray is continuous while the vehicle is active, and each row is merely a gps reading of the coordinates.

3. Some traps, specifically T009 and T035 had different coordinates for different dates. This could indicate a misreading of location, human typo error, or a decision being made to move them. However, the traps should be given a different ID then. Hence, in the absence of additional information, and as such traps were only a minor component of the dataset, data of such traps was removed when comparing spray with train.

4. With the given spray data and traps, there was insufficient physical overlap. This meant that many traps did not appear to have pesticide sprayed. If indeed they were actually sprayed, the lack of data hinders any correlation to be determined. In addtion, spray data was only a scant 10 days' over the course of years of train data. To make matters worse, the spray data did not seem to repeat itself over the same areas. This also limits the accuracy of any models due to the lack of sufficient consistent data for comparison.


### Preprocessing
- treating the unbalance class by upsample the minority class, that is WnvPresent = 1 through `bootstraping` (random sampleing wiht replacement).
- `feature engineering` on weather dataset, which include parsing the date feature into year, month, day, day of year, and workweek. In addition, we are also exploring the interaction among the weather features as well.
- encode categorical variable into indicator variables using `get_dummies` to make it numerical predictor and included in modelling as well.
- Preparing the `X features` (predictors/ variables) and `y-target` (`WnvPresent`).
- `Train test split` the data.


### Modelling
This is supervised classification (2 categories/ binary) machine learning problem.
Two models are selected:
1. Random Forest
2. XGBoost (eXtreme Gradient Boosting)

**Baseline Accuracy**:

In EDA, we observed that we have imbalanced class. However, we still count the majority class, use this as null model to get our naive baseline accuracy score, which is **94.8%**
Thus, we proceed to build a basic model (default setting, without hyperparameters optimization) as our baseline model.

Model optimization was done by using GridSearchCV to identify the optimal hyperparameters and were built into the classificaiton models.

### Model Evaluation
Metrics used to evaluate: **accuracy, recall, roc_auc**

The **recall** (sensitivity) is the ratio tp / (tp + fn). The recall is intuitively the ability of the classifier to find all the positive samples, that is in this project, to predict WNV infected (WnvPresent = 1).

Thus, reducing fn is important as we would like to predict if there is WNV infection as accurately as possible. fn means, predict there is NO WNV infection, but in actual case there WNV is present.

**AUC - ROC** curve on the other hand, is a performance measurement for classification problem at various thresholds settings. ROC is a probability curve and AUC represents degree or measure of separability. It tells how much model is capable of distinguishing between classes. In our case, the capability to distinguish WNV present (1) or NOT present (0). Higher the AUC, better the model is at predicting between mosquitos with WNV infection and no WNV infection.


### Conclusions and Recommendations
**Results summary and conclusion:**

|Classifier Model|Accuracy|roc_auc|Recall|Kaggle roc_aucvscore|
|---|---|---|---|---|
|RandomForest w GridSearchCV|81.5%|81.5%|83.1%|63%
|RandomForest w feature engineering|98.3%|98.5%|99.7%|70%
|XGBoost|84.1%|91.3%|91.1%|70.7%
|**XGBoost w GridSearchCV**|**94.7%**|**98%**|**99.4%**|**75.9%**
|XGBoost w feature engineering|94.6%|98%|99.4%|75%


In general, results from modeling (with optimum hyperparameter) are out-perform our baseline model accuracy score, that is >95%. 
In addition, they have high roc_auc score and recall score as well. This means, the models are able to **separate the WNV infection from no infection** quite well, and at the same time, have relatively **low fn** (low type II error). 

Among the models, **XGBoost** is having the highest Kaggle score on the un-labeled test dataset. Thus, our team propose to use this model for predicting the presence of WNV. 

**Recommendations :**

For further improvements,  we could use shapely or some other python geolibrary to:

1. Classify traps within the spray region;
2. In conjunction with timeseries lag functions/models, iterate based on different values of 'radius/distance from spray border' parameter to identify effective distance of spray, with criteria being significant drop in mosquito population. (particularly if there is drop in effectiveness beyond a certain 'radius/distance from spray border')
3. Stationarity tests could be done on lagging data, to identify a number of days effectiveness parameter, before the mosquito cycle and population reverts to pre-sprays.

Aside from exploring more advanced libraries, we could also check further on:

1. It is also noted wind conditions on spray dates are likely to affect, spray spread, which bears further investigation.
2. In order to determine cost-effectiveness, we need to know population density, as well as the typical cost of pesticides.
3. To further evaluate this, we need to compare effectiveness of different pesticides, and other alternatives, such as no stagnant water campaigns, impact of fines on mosquito breeding in houses.
4. Related to this is also the need for more data, via more traps laid out in a more geo-zonal format where possible. Sprays or other stimulus should also be repeated on the same areas, with results used for comparison and further modeling.

From external literature:

1. We have discovered that humans are not the main mammals which the mosquitos transmit the West Nile Virus through. The main vector is actually the American robin, the preferred food source for the mosquito vectors. Hence, looking at data on American robin populations and migratory patterns could inflence our model too.
2. The shortest mosquito cycle could be as fast as 7 days, from egg-form to mating. For cost-effective mosquito control, sprays could be done every 7 days, which would break the mosquito mating cycle.


### Sources
1. [West Nile Virus Prediction](https://www.kaggle.com/c/predict-west-nile-virus)
2. Geo-Distance Calculator in km, with given coordinates: (https://www.geodatasource.com/distance-calculator)
3. American Society for Microbiology: West Nile Virus: Biology, Transmission, and Human Infection
Tonya M. Colpitts, Michael J. Conway, Ruth R. Montgomery, Erol Fikrig (https://cmr.asm.org/content/25/4/635)
4. National Environment Agency of Singapore: https://www.nea.gov.sg/dengue-zika/prevent-aedes-mosquito-breeding/aedes-mosquito

