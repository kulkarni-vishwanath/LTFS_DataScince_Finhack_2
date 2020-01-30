![LTFS_Data_Science_FinHack_2_-_1920x480-thumbnail-1200x1200-90](https://user-images.githubusercontent.com/25604111/72835886-8ebf4880-3cb1-11ea-8545-111b958d2e3a.jpg)

# LTFS_DataScince_Finhack_2

## Problem Statement
LTFS receives a lot of requests for its various finance offerings that include housing loan, two-wheeler loan, real estate financing and micro loans. The number of applications received is something that varies a lot with season. Going through these applications is a manual process and is tedious. Accurately forecasting the number of cases received can help with resource and manpower management resulting into quick response on applications and more efficient processing.

You have been appointed with the task of forecasting daily cases for **next 3 months for 2 different business segments** aggregated at the country level keeping in consideration the following major Indian festivals (inclusive but not exhaustive list): Diwali, Dussehra, Ganesh Chaturthi, Navratri, Holi etc. (You are free to use any publicly available open source external datasets). Some other examples could be:
* Weather.
* Macro Economic Variables.

## Data Dictionary
The train data has been provided in the following way:

* For business segment 1, historical data has been made available at branch ID level.
* For business segment 2, historical data has been made available at State level.

## Train File

| Variable             |  Definition        |
| ---------------------| -------------------|
| application_date     | Date of application     |
| segment              | Business Segment (1/2)     |
| branch_id            | Anonymised id for branch at which application was received     |
| state                | State in which application was received (Karnataka, MP etc.)     |
| zone                 | Zone of state in which application was received (Central, East etc.)     |
| case_count           | (Target) Number of cases/applications received  |

## Test File
Forecasting needs to be done at country level for the dates provided in test set for each segment.

| Variable             |  Definition        |
| ---------------------| -------------------|
| id                   | Unique id for each sample in test set     |
| application_date     | Date of application     |
| segment              | Business Segment (1/2)     |

## Sample Submission
This file contains the exact submission format for the forecasts. Please submit csv file only.

| Variable             |  Definition        |
| ---------------------| -------------------|
| id                   | Unique id for each sample in test set     |
| application_date     | Date of application     |
| segment              | Business Segment (1/2)     |
| case_count           | (Target) Predicted values for test set  |

## Evaluation
The evaluation metric for scoring the forecasts is MAPE (Mean Absolute Percentage Error) M with the formula:

<img width="205" alt="MAPE" src="https://user-images.githubusercontent.com/25604111/73197021-a46fba80-4156-11ea-97ac-ebf05638f8a7.png">

Where At is the actual value and Ft is the forecast value.
The Final score is calculated using MAPE for both the segments using the formula:

<img width="498" alt="FINAL" src="https://user-images.githubusercontent.com/25604111/73197100-c701d380-4156-11ea-98f9-ab3759769e2e.png">

## Public and Private Split
Test data is further divided into Public (1st Month) and Private (Next 2 months)
Your initial responses will be checked and scored on the Public data.
The final rankings would be based on your private score which will be published once the competition is over.

## Approach to Problem Solving
This competition was the perfect case of the fact that Simple models sometime work better than complicated ones. This problem statement could've been considered as a Time Series as well as a Regression problem and I chose the later. Although the data was time based, the Train set had some variables that were not provided in the Test set, and this created problems of it's own as these variables couldn't be used to build the model. The best option was to create as many datetime features as possible and that is what worked. Some of the models that I built and were not so successful are ,
- Building Models for two separate segments using Random Forests.
- Building Models for two separate segments using LightGBM. 
- Single model with extensive Hyperparameter Tuning using RF.
- Cross Validation with TimeSeries split and KFold cross validation with RF.

Finally the one approach that worked best was a simple Random Forest model with no cross validation.

## Leaderboard
- Public Leaderboard: 64/883 
- Private Leaderboard: 13/883


