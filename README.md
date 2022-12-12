# Introduction

For this Machine Learning project I wanted to fit models that gave me information that I wish I had easy access to on a daily basis, something that I would use everyday and something others could potentially find useful as well. Almost every day during our Summer Breaks, at 6:30am on the dot, me and my friends routinely went for an early morning sunrise surf sessions to start our days. Whether it was projected to be amazing conditions or even if the surf was as flat as a pool, we made it an effort to at least go for an early morning drive hoping for even the possibility of some fun surf. However, on those days that one of us or all of us were too lazy to wake up to our alarms to drive 10-20 minutes and check the surf, we always had Surfline to give us a surf report and an early morning camera streaming of our break destination of the day.  

![Fig. 1: Surfline Application Poster](../131_Project_images/surfline-2019-fi.jpg)

For those who aren't familiar, Surfline is a popular app used among the surf community to check daily and future surf forecast and swell conditions, as well as access to live camera feeds of your local surf break of choice. However, as a subscription based service, Surfline requests a subscription fee in order for a user to access 7-day forecast reports, view camera feeds of certain popular surf breaks, and to remove a 3-time a week limit to check daily conditions. Although a great application that I still use today, sometimes it isn't the most easily accessible way to check the surf forecast 7 days in the future.  
  
So for this Machine Learning project, I've decided to take a little inspiration from Surfline, and make my own predictions of the surf for my hometown San Diego. Although the conditions of the surf are rapidly change by the week, day, hour, and even down to the minute, I thought why not take a peek into the process behind the Surf forecasting application I've spent my early mornings checking.  

# Dataset Overview

For this project, I've decided to base my prediction of surf in San Diego on historical daily data from NOAA's National Data Buoy Center, specifically on data from the Tanner Bank Buoy that is used for predicting the conditions for San Diego...  

## Data Source
The source of the database used in this project will be a set of concatenated **Historical Data**...

  1. **Historical Data Source**:  
      - [NOAA's National Data Buoy Center](https://www.ndbc.noaa.gov/historical_data.shtml#stdmet)  
          - Variables Codebook:  
              - YY - Year  
              - MM - Month  
              - DD - Day  
              - hh - Hour  
              - mm - Minutes  
              - WDIR - Wind Direction (degrees clockwise from true N)  
              - WSPD - Wind Speed (m/s)  
              - GST - Gust Speed (m/s)  
              - WVHT - Significant Wave Height (meters)  
              - DPD - Dominate Wave Period (seconds)  
              - APD - Average Wave Period (seconds)  
              - MWD - Direction of DPD (degrees clockwise from true N)  
              - PRES - Sea Level Pressure (hPa)  
              - ATMP - Air Temperature (Celsius)  
              - WTMP - Sea Surface Temperature (Celsius)  
              - DEWP - Dewpoint Temperature (Celsius)  
              - VIS - Station Visibility (nautical miles)  
              - PTDY - Pressure Tendency (plus or minus)  
              - TIDE - Water Level (feet)  
          - Station ID's and Locations Used:  
              - [46047 - Tanner Bank (San Diego)](https://www.ndbc.noaa.gov/data_availability/data_avail.php?station=46047)  
                  - [1991](https://www.ndbc.noaa.gov/download_data.php?filename=46047h1991.txt.gz&dir=data/historical/stdmet/), [1992](https://www.ndbc.noaa.gov/download_data.php?filename=46047h1992.txt.gz&dir=data/historical/stdmet/), [1993](https://www.ndbc.noaa.gov/download_data.php?filename=46047h1993.txt.gz&dir=data/historical/stdmet/), [1999](https://www.ndbc.noaa.gov/download_data.php?filename=46047h1999.txt.gz&dir=data/historical/stdmet/), [2000](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2000.txt.gz&dir=data/historical/stdmet/), [2001](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2001.txt.gz&dir=data/historical/stdmet/), [2002](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2002.txt.gz&dir=data/historical/stdmet/), [2003](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2003.txt.gz&dir=data/historical/stdmet/), [2004](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2004.txt.gz&dir=data/historical/stdmet/), [2005](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2005.txt.gz&dir=data/historical/stdmet/), [2006](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2006.txt.gz&dir=data/historical/stdmet/), [2007](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2007.txt.gz&dir=data/historical/stdmet/), [2008](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2008.txt.gz&dir=data/historical/stdmet/), [2009](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2009.txt.gz&dir=data/historical/stdmet/), [2010](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2010.txt.gz&dir=data/historical/stdmet/), [2011](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2011.txt.gz&dir=data/historical/stdmet/), [2012](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2012.txt.gz&dir=data/historical/stdmet/), [2013](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2013.txt.gz&dir=data/historical/stdmet/), [2014](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2014.txt.gz&dir=data/historical/stdmet/), [2015](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2015.txt.gz&dir=data/historical/stdmet/), [2016](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2016.txt.gz&dir=data/historical/stdmet/), [2017](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2017.txt.gz&dir=data/historical/stdmet/), [2018](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2018.txt.gz&dir=data/historical/stdmet/), [2019](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2019.txt.gz&dir=data/historical/stdmet/), [2020](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2020.txt.gz&dir=data/historical/stdmet/), [2021](https://www.ndbc.noaa.gov/download_data.php?filename=46047h2021.txt.gz&dir=data/historical/stdmet/)  

## Observations and Variables

From [NOAA's National Data Buoy Center](https://www.ndbc.noaa.gov/historical_data.shtml#stdmet), I have decided to take data from Station ID 46047 which is NOAA's Tanner Banks Buoy. After scanning the station data, I found I have access to the buoy's data for the years; 1991, 1992, 1993, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, and 2021. It is important to note that in the span of roughly 3 decades, the names of variables changed, new variables were added, and some variables were comprised of mostly null values for some years or even nonexistent for other years. Based on that notion, I have decided to deselect certain variables and only read in the variables: "YY", "MM", "DD", "hh", "mm", "WDIR", "WSPD", "WVHT", "APD", "PRES", "ATMP", "WTMP".  

## Python Modules

Although this project was begun for UCSB's PSTAT 131 Course: Statistical Machine Learning, a class that is taught entirely in the language `R`, I have decided to try and expand my understanding of Machine Learning by completing this project in `Python`.  

For this project, in order to clean my data, explore my data, visualize my analysis, build and evaluate my models, and make my predictions, I have chosen to utilize the `Python` Modules below.  

```{python class.source="fold-show"}
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sb
import scipy as sp
import patsy as pat
import statsmodels as stmd
import random
from yellowbrick.regressor import PredictionError, ResidualsPlot

import sklearn
from sklearn.model_selection import (
  train_test_split, 
  RepeatedStratifiedKFold, 
  cross_val_score
  )
from sklearn.decomposition import PCA
from sklearn.feature_selection import SelectKBest
from sklearn.preprocessing import MinMaxScaler
from sklearn.linear_model import Ridge
from sklearn.svm import SVR
from sklearn.neighbors import KNeighborsRegressor
from sklearn.ensemble import HistGradientBoostingRegressor
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
from sklearn.metrics import accuracy_score
from sklearn.pipeline import (
  Pipeline, 
  FeatureUnion
  )
```
