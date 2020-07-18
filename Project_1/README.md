# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) 

# Project 1: SAT & ACT Analysis

## Problem Statement

New format for the SAT was released in March 2016. As an employee of the College Board - the organization that administers the SAT, I am part of a team that tracks statewide participation rate and to recommends where money is best spent to improve SAT participation rates. 


## Executive Summary

In this project, I gathered the datasets of SAT and ACT. Next, analyze the aggregate SAT and ACT scores and participation rates from each state in the United States. Identify the trend observed from year 2017 to year 2018. Perform outside research to correlate the trends seen in the data. Then, recommendations were made to the College Board in order to increase the participation rate in Iowa.


### Contents

- [2017 Data Import & Cleaning](#Data-Import-and-Cleaning)
- [2018 Data Import and Cleaning](#2018-Data-Import-and-Cleaning)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Data Visualization](#Visualize-the-data)
- [Descriptive and Inferential Statistics](#Descriptive-and-Inferential-Statistics)
- [Outside Research](#Outside-Research)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)


### 2017 Data Import & Cleaning
Import the SAT & ACT 2017 datasets, review the datasets to identify issues (incomplete data, wrong datatypes, abnormal data value, drop unnecessary data) and correct them according. Combine the cleaned SAT and ACT in 2017 datasets. 
- [2017 SAT ACT Scores](../output/combined_2017.csv)


### 2018 Data Import and Cleaning
Do the same for the SAT & ACT 2018 datasets. Merge the cleaned 2018 datasets with 2017 datasets to perform data analysis.
- [2017 and 2018 SAT ACT Scores](../output/final.csv)


### Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|**state**|*object*|ACT/SAT|State in US| 
|**participation**|*float*|ACT/SAT|Participation rate| 
|**sat_erw**|*float*|SAT|Average score for Evidence-Based Reading and Writing| 
|**sat_math**|*float*|SAT|Average score for Math| 
|**sat_total**|*float*|SAT|Total of average score for erw and Math| 
|**act_english**|*float*|ACT|Average score for English| 
|**act_math**|*float*|ACT|Average score for Math| 
|**act_reading**|*float*|ACT|Average score for Reading| 
|**act_science**|*float*|ACT|Average score for Science| 
|**act_composite**|*float*|ACT|Average of Math,Reading, & Science mean score| 


### EDA 
Reviewed descriptive statistics of the data and identified the trend of data.

#### Participation rate for SAT
Highest:
- 2017: Connecticut, Delaware, Michigan, District of Columbia (100%)
- 2018: Connecticut, Delaware, Michigan (100%)
Lowest:
- 2017:North Dakota, Iowa, Mississippi (only at 2%)
- 2018: North Dakota (2%), Iowa, Mississippi (3%)

#### Participation rate for ACT:
Highest:
- 2017: 17 states with 100% participation rate.
- 2018: 15 states with 100% participation rate.
Lowest:
- 2017: Maine (8%)
- 2018: Maine (7%)

The data indicates that ACT is having higher participation rate compared to SAT.
There are only 4 - 5 states are with high participation rate (> 50%) in both SAT & ACT. Other state mostly dominated by either SAT or ACT.


### Visualize the data
#### Correlation matrix to visualize the correlations between participation rate and scores
- Positive correlation: SAT score is positive correlated between year 2017 and 2018. Same goes to ACT score.
- Negative correlation: SAT participation rate is negative correlated with ACT participation rate.
                        SAT participation having negative correlation with its' score. Same goes to ACT score.
- Low correlation: No strong relationship between SAT and ACT score observed.

#### Data distribution
- Participation rate: Not normally distributed. Two peaks observed in the distribution plot. In addition, the mean median, and mode are not the same. In addition, the data is having wide spreading.
- SAT score in general are mostly not normally distributed. 
- ACT score in general is relatively closer to normal distribution, as the mean, median, mode are closer to each other.


### Descriptive and Interential Statistics
#### Relationship between SAT and ACT participation rates in 2017: 
The hypothesis testing resulted in showing that it is likely to say that SAT participation cohort is not coming from the same ACT cohort.

#### Relationship between SAT and ACT scores:
It is not feasible to compare the SAT and ACT scores as they are having different scoring system. 


### Outside Research
#### Spike in SAT participation rate
- Colorado and Illinois participation rate surge in 2018 as shown in above table.
- Contrary, ACT participation rate shrink about 60%-70% in these two states in year 2018.

This was due to the states are contracted with the College Board to administer the SAT to some or all high school juniors for free.
1. 2016-17 school year, all Colorado juniors in public schools will take the SAT.
2. Beginning with the 2016-17 school year, all Illinois juniors must take the SAT.

Other than Colorado and Illinois, those states that were working with the College Board to administer the SAT are having high participation rates. Those states includes: Connecticut, Delaware, District of Columbia, Idaho, Maine, Michigan, New Hampshire.


### Conclusions and Recommendations
#### Key takeaways:
- Participants only take one test, either SAT or ACT not both.
- State education departments or local education agencies testing system or policy. State that requires SAT test as college admission test will spur the participation rate.

#### Recommandation
- Work with local authority to make SAT as a mandatory test for college entrance exam testing requirements.
- Full or partial funding for the test. Fee waiver for low-income students.
- Free and high quality study material, free resource to better prepare high school student for the test.
- Expand the SAT school day to more state, which it allows students to take the SAT in their own school on a weekday, rather than taking it on a Saturday at different school.