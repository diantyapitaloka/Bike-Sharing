# 🍊🍋🍐🍓 DATA ANALYSIS PROJECT 🍓🍐🍋🍊
- Nama: Diantya Pitaloka
- Email: diantyantyaa@gmail.com
- Id Dicoding: diantyap


# 🍊🍋🍐🍓 DETERMINE BUSINESS QUESTIONS 🍓🍐🍋🍊
- What is the most working day of the season?
- What is the highest wind speed throughout the season?


# 🍊🍋🍐🍓 PREPARE ALL NEEDED LIBRARY 🍓🍐🍋🍊
- Normally, a library is a collection of books or is a room or place where many books are stored to be used later. Similarly, in the programming world, a library is a collection of precompiled codes that can be used later on in a program for some specific well-defined operations. Other than pre-compiled codes, a library may contain documentation, configuration data, message templates, classes, and values, etc.
- import pandas as pd
- import numpy as np
- import matplotlib.pyplot as plt
- import seaborn as sns
- import plotly.express as px


# 🍊🍋🍐🍓 DATA WRAGLING 🍓🍐🍋🍊
- Data wrangling stage, starting with the data collection process. In this process we will collect all the data needed to answer all the questions or business problems we want to face.
## Gathering Data (Load Dataset)
- import pandas as pd
- from google.colab import files
- import io

## Assessing Data (Missing Value)
- import pandas as pd
- day_df = pd.read_csv("day.csv")
- day_df.isnull().sum()
- import pandas as pd
- hour_df = pd.read_csv("hour.csv")
- hour_df.isnull().sum()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/b45f87cf-84b7-4623-8381-a7432e78b6bf)


## Cleaning Data (Dropping Overcomes Missing Value)
- import pandas as pd
- day_df = pd.read_csv("day.csv")
- day_df.dropna(axis=0, inplace=True)
- import pandas as pd
- hour_df = pd.read_csv("hour.csv")
- hour_df.dropna(axis=0, inplace=True)


# 🍊🍋🍐🍓 EXPLORATORY DATA ANALYSIS (EDA) 🍓🍐🍋🍊
- From the perspective of data practitioners, the EDA process is one of the most interesting stages in a data analysis project. This process allows data practitioners to explore and experiment with data to look for patterns, gain insight, answer various business challenges, and draw conclusions based on the analysis results.
- As a prospective future data practitioner, you will definitely enjoy this EDA process. As an illustration, in the next few materials, we will discuss various tools and techniques that can help you carry out the EDA process effectively. However, before discussing all of these things, it would be better if we understood the difference between exploratory analysis and explanatory analysis first.
- Exploratory analysis and explanatory analysis are two terms often encountered in data analysis projects. Apart from their pronunciation being quite similar, the two terms also represent quite similar processes. This is what makes it difficult for novice data practitioners to differentiate between the two terms.
- Conclusion, exploratory analysis is a data analysis process that aims to explore and get to know data. The process often starts with defining questions or just digging into the data to find some interesting insights from the data. In this process, we sometimes also apply simple data visualizations aimed at validating the insights obtained. If analogous, the exploratory analysis process is like a mining process that collects 100 stones to find one or two valuable diamonds.
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/084f20c6-f4a6-4cb9-b7c1-2b06168d9a77)

## How To Read Data Via Google Sheet
- sheet_url = 'https://docs.google.com/spreadsheets/d/1_jEMQLR8CH_3ccQDPls0TuUOmX9I7BjWyp3EvxD5O90/edit#gid=251343836'
- sheet_url_trf = sheet_url.replace('/edit#gid=','/export?format=csv&gid=')
- print(sheet_url_trf)
- df = pd.read_csv(sheet_url_trf)
- df.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/459021e2-2339-4722-bd50-60a0dfb3fd6f)
- df.info()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/b526b84c-996f-4e4b-9c2c-6c7c86deff22)
- df.columns
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/142984f0-afef-4069-b21f-2933124a919b)

## Change Type Date
- df_cleaned = df.copy()
- df_cleaned['dteday'] = pd.to_datetime(df_cleaned['dteday'])
- df_cleaned['Total People'] = df_cleaned['casual'] + df_cleaned['registered']
- print(df_cleaned.info())
- df_cleaned.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/77949889-f81e-4dfb-80be-9dce08dfdf46)
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/4520a6de-bce7-40b8-9982-0d152ff3f6cf)

## Check Typo
- df_cleaned['season'].value_counts()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/34166abe-d7c4-41cb-a471-ef78ec3cc79e)

## Check Replace
- df_replaced = df_cleaned
- df_replaced.head(10)
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/fa2cd24b-03b1-4c79-aa30-d22ef0b6254d)


# 🍊🍋🍐🍓 VISUALIZATION & EXPLANATORY ANALYSIS 🍓🍐🍋🍊
- If examined fundamentally, data visualization is the process of transforming data into visual form using various visual elements. The following are some visual elements that are commonly used to create data visualizations.
- Position: this element will help us represent data points using certain axes (such as the X, Y, and Z axes) as a reference.
- Size: size (length or width) is a visual element that we generally use to differentiate and compare values from certain categories or data points.
- Shape: shape is a visual element that can be used to distinguish certain categories or data points.
- Color: apart from shape, color is also another visual element that can be used to differentiate certain categories or data points. When using this element, we must remember that not everyone has the ability to distinguish colors well.
- Texture: adding certain textures or patterns can be another alternative in distinguishing certain categories or data points.
- Angle: in several forms of data visualization, angle is one of the visual elements used to represent the value of data.
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/5c00e0a3-372d-45a2-aaa1-79649d1ad31b)


## Question 1
- In what season are working days the highest?
## Question 2
- Highest windspeed throughout the season?

## Answer to Question 1
- agg_questionone = df_replaced.groupby('season',as_index=False)['Total People','workingday'].sum()
- agg_questionone.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/7e086000-a5db-4a07-9e03-b2f82a9715c2)
- plt.rcParams["figure.figsize"] = (10,5)
- sns.barplot(data=agg_questionone,x='season',y='workingday')
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/eddfabfc-1ece-437a-aafe-b6b1dbb2afb4)

- *Conclusion Question 1*
- The highest working day is in season 3


## Answer to Question 2
- agg_questiontwo = df_replaced.groupby('season',as_index=False)['Total People','windspeed'].sum()
- agg_questiontwo.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/96d92c55-3b55-4020-bac0-441e30a8c5fa)
- plt.rcParams["figure.figsize"] = (20,5)
- plt.plot('season','windspeed',data=agg_questiontwo)
- plt.title('windspeed trend')
- plt.xlabel('season')
- plt.ylabel('windspeed')
- plt.show()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/3525a56b-9e00-43e2-9fc8-7b940fcf1c73)

- *Conclusion Question 2*
- The highest windspeed is located in season 1

# 🍊🍋🍐🍓 LICENSE 🍓🍐🍋🍊
- Copyright by Diantya Pitaloka
