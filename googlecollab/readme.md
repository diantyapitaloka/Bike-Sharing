## PROYEK ANALISIS DATA
Nama: Diantya Pitaloka
Email: diantyantyaa@gmail.com
Id Dicoding: diantyap

## Menentukan Pertanyaan Bisnis
Hari apa yang paling banyak bekerja sepanjang musim?
Berapa kecepatan angin tertinggi sepanjang musim?

## MENYIAPKAN SEMUA LIBLARY YANG DIBUTUHKAN
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

## DATA WRAGLING 
# Gathering Data (Load Dataset)
import pandas as pd
from google.colab import files
import io

# Assessing Data (Missing Value)
import pandas as pd
day_df = pd.read_csv("day.csv")
day_df.isnull().sum()

import pandas as pd
hour_df = pd.read_csv("hour.csv")
hour_df.isnull().sum()



#Cleaning Data (Dropping mengatasi Missing Value)
import pandas as pd
day_df = pd.read_csv("day.csv")
day_df.dropna(axis=0, inplace=True)

import pandas as pd
hour_df = pd.read_csv("hour.csv")
hour_df.dropna(axis=0, inplace=True)

## EXPLORATORY DATA ANALYSIS (EDA)
#how to read data in google sheet

sheet_url = 'https://docs.google.com/spreadsheets/d/1_jEMQLR8CH_3ccQDPls0TuUOmX9I7BjWyp3EvxD5O90/edit#gid=251343836'
sheet_url_trf = sheet_url.replace('/edit#gid=','/export?format=csv&gid=')
print(sheet_url_trf)

df = pd.read_csv(sheet_url_trf)
df.head()

df.info()

df.columns

#change type date
df_cleaned = df.copy()

df_cleaned['dteday'] = pd.to_datetime(df_cleaned['dteday'])
df_cleaned['Total People'] = df_cleaned['casual'] + df_cleaned['registered']

print(df_cleaned.info())
df_cleaned.head()

#check typo
df_cleaned['season'].value_counts()

#replace
df_replaced = df_cleaned
df_replaced.head(10)

## VISUALIZATION & EXPLANATORY ANALYSIS

# Pertanyaan 1
Pada season berapa working day nya yang paling tinggi?

# Pertanyaan 2
Windspeed tertinggi sepanjang season?

# Jawaban Pertanyaan 1
agg_questionone = df_replaced.groupby('season',as_index=False)['Total People','workingday'].sum()
agg_questionone.head()

plt.rcParams["figure.figsize"] = (10,5)
sns.barplot(data=agg_questionone,x='season',y='workingday')

*Conclusion Pertanyaan 1 *
Working day yang paling tinggi yaitu terletak di season 3

# Jawaban Pertanyaan 2
agg_questiontwo = df_replaced.groupby('season',as_index=False)['Total People','windspeed'].sum()
agg_questiontwo.head()

plt.rcParams["figure.figsize"] = (20,5)

plt.plot('season','windspeed',data=agg_questiontwo)
plt.title('windspeed trend')
plt.xlabel('season')
plt.ylabel('windspeed')
plt.show()

*Conclusion Pertanyaan 2 *

Windspeed yang paling tinggi yaitu terletak di season 1