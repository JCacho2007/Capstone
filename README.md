## Overview

For this project, we set out to create a classification model that could differentiate between songs that would chart on the Billboard Top 100 and songs that would not. We collected nearly 300,000 different songs across decades (1960s-2010s), including nearly 5,000 songs that charted the Billboard Top 100. We then used Spotify's API to gather 13 different acoustic features for each of the songs. With our dataset complete, we ran 8 different models and measured their performance. Our best model, a Bagging Classifier, was able to achieve 98.6% accuracy on unseen test data. 


## EDA Methodology

We downloaded over half-a-million songs from [here](https://components.one/datasets/billboard-200/) and we downloaded ~5,000 songs that charted the Billboard Top 100 from [here](https://github.com/kevinschaich/billboard). The larger dataset already included acoustic features taken from Spotify's API. To make the Top 100 dataset match the larger dataset, we queried the Spotify API to obtain 13 different acoustic features for each song. 

After downloading all this data, a few steps were taken to clean it.
    1. Songs from 1950-1963 and from 2015-2019 were removed because our Top 100 dataset did not include these years
    2. Any incorrect results from Spotify's API (e.g. a karaoke version of a song) were removed from the dataset
    3. Any rows with null values were removed 
    
Our final clean dataset included 291,630 observations, including 4,521 songs that charted the Billboard Top 100. 

The data was then scaled using StandardScaler.

Due to the class imbalance, we opted to use SMOTE to bootstrap/oversample the hit song observations until we had a 50/50 distribution between hits and non-hits. 

A Train/Test split of 75/25 was then conducted. 

## Modeling

After EDA, we chose to use 8 classification models:
    * Logistic Regression
    * KNN
    * Decision Trees
    * Bagging
    * Random Forest
    * AdaBoost
    * Gradient Boosting
    * Voting Classifier
    
## Results

Of the 8 models, the Bagging Classifier performed the best, with a test accuracy of 98.6%.
The remaining results are as follows:

| Model               | Training Accuracy | Testing Acccuracy|
|---------------------|------------------ |------------------|
| Logistic Regression | 66.00%            | 65.65%           |
| KNN                 | 87.83%            | 82.27%           |
| Decision Trees      | 99.99%            | 97.01%           |
| Bagging             | 99.82%            | 98.65%           |
| Random Forest       | 99.88%            | 98.18%           |
| AdaBoost            | 86.04%            | 85.86%           |
| Gradient Boosting   | 95.11%            | 95.11%           |
| Voting Classifier   | 99.82%            | 98.43%           |


The 13 features are shown below, with their coefficients:

| Feature          | Coefficient |
|------------------|-------------|
| acousticness     | 0.112218    |
| danceability     | 0.070404    |
| duration_ms      | 0.05618     |
| energy           | 0.05787     |
| instrumentalness | 0.043434    |
| key              | 0.214133    |
| liveness         | 0.042887    |
| loudness         | 0.035769    |
| mode             | 0.170644    |
| speechiness      | 0.061317    |
| tempo            | 0.037828    |
| time_signature   | 0.04598     |
| valence          | 0.051336    |

Based on the above coefficients, we can ascertain that the most important feature in determining if a song would chart on the Billboard Top 100 is `key`, followed by `mode` and `acousticness`. 






