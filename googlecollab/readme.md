## PROYEK ANALISIS DATA
1. Nama: Diantya Pitaloka
2. Email: diantyantyaa@gmail.com
3. Id Dicoding: diantyap


## Menentukan Pertanyaan Bisnis
1. Hari apa yang paling banyak bekerja sepanjang musim?
2. Berapa kecepatan angin tertinggi sepanjang musim?


## MENYIAPKAN SEMUA LIBLARY YANG DIBUTUHKAN
- import pandas as pd
- import numpy as np
- import matplotlib.pyplot as plt
- import seaborn as sns
- import plotly.express as px


## DATA WRAGLING
- Tahap data wrangling, dimulai dengan proses pengumpulan data. Pada proses ini kita akan mengumpulkan semua data yang dibutuhkan untuk menjawab semua pertanyaan atau masalah bisnis yang ingin kita hadapi.
# Gathering Data (Load Dataset)
- import pandas as pd
- from google.colab import files
- import io

# Assessing Data (Missing Value)
- import pandas as pd
- day_df = pd.read_csv("day.csv")
- day_df.isnull().sum()
- import pandas as pd
- hour_df = pd.read_csv("hour.csv")
- hour_df.isnull().sum()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/b45f87cf-84b7-4623-8381-a7432e78b6bf)


# Cleaning Data (Dropping mengatasi Missing Value)
import pandas as pd
day_df = pd.read_csv("day.csv")
day_df.dropna(axis=0, inplace=True)

import pandas as pd
hour_df = pd.read_csv("hour.csv")
hour_df.dropna(axis=0, inplace=True)


## EXPLORATORY DATA ANALYSIS (EDA)
# how to read data in google sheet
sheet_url = 'https://docs.google.com/spreadsheets/d/1_jEMQLR8CH_3ccQDPls0TuUOmX9I7BjWyp3EvxD5O90/edit#gid=251343836'
sheet_url_trf = sheet_url.replace('/edit#gid=','/export?format=csv&gid=')
print(sheet_url_trf)

df = pd.read_csv(sheet_url_trf)
df.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/459021e2-2339-4722-bd50-60a0dfb3fd6f)

df.info()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/ea7104b8-3dbf-4c12-90e3-b5c6806be46f)

df.columns
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/142984f0-afef-4069-b21f-2933124a919b)

# change type date
df_cleaned = df.copy()
df_cleaned['dteday'] = pd.to_datetime(df_cleaned['dteday'])
df_cleaned['Total People'] = df_cleaned['casual'] + df_cleaned['registered']
print(df_cleaned.info())
df_cleaned.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/77949889-f81e-4dfb-80be-9dce08dfdf46)
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/4520a6de-bce7-40b8-9982-0d152ff3f6cf)

# check typo
df_cleaned['season'].value_counts()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/34166abe-d7c4-41cb-a471-ef78ec3cc79e)

# replace
df_replaced = df_cleaned
df_replaced.head(10)
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/fa2cd24b-03b1-4c79-aa30-d22ef0b6254d)


## VISUALIZATION & EXPLANATORY ANALYSIS

# Pertanyaan 1
Pada season berapa working day nya yang paling tinggi?
# Pertanyaan 2
Windspeed tertinggi sepanjang season?

# Jawaban Pertanyaan 1
agg_questionone = df_replaced.groupby('season',as_index=False)['Total People','workingday'].sum()
agg_questionone.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/7e086000-a5db-4a07-9e03-b2f82a9715c2)


plt.rcParams["figure.figsize"] = (10,5)
sns.barplot(data=agg_questionone,x='season',y='workingday')
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/eddfabfc-1ece-437a-aafe-b6b1dbb2afb4)

*Conclusion Pertanyaan 1 *
Working day yang paling tinggi yaitu terletak di season 3


# Jawaban Pertanyaan 2
agg_questiontwo = df_replaced.groupby('season',as_index=False)['Total People','windspeed'].sum()
agg_questiontwo.head()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/96d92c55-3b55-4020-bac0-441e30a8c5fa)

plt.rcParams["figure.figsize"] = (20,5)

plt.plot('season','windspeed',data=agg_questiontwo)
plt.title('windspeed trend')
plt.xlabel('season')
plt.ylabel('windspeed')
plt.show()
![image](https://github.com/diantyapitaloka/Bike-Sharing/assets/147487436/3525a56b-9e00-43e2-9fc8-7b940fcf1c73)

*Conclusion Pertanyaan 2 *
Windspeed yang paling tinggi yaitu terletak di season 1
