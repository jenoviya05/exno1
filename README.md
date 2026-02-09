# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

import pandas as pd

import numpy as np

from scipy import stats

import seaborn as sns

import matplotlib.pyplot as plt

df1 = pd.read_csv('Loan_data.csv')
df1.head()


<img width="1636" height="243" alt="Screenshot 2026-02-05 094735" src="https://github.com/user-attachments/assets/7600647c-099c-4842-a601-9c13422e38c3" />

df1.info()
df1.describe()

<img width="958" height="800" alt="Screenshot 2026-02-05 094842" src="https://github.com/user-attachments/assets/25706548-dd4f-4531-be0a-5ee46bebb907" />

df1.isnull()
df1.isnull().sum()

<img width="316" height="322" alt="Screenshot 2026-02-05 094944" src="https://github.com/user-attachments/assets/a185ed1a-7e4b-43c3-907c-a1a50bcfa4ab" />

df1_fill_0 = df1.fillna(0)
df1_fill_0

<img width="1655" height="479" alt="Screenshot 2026-02-05 095737" src="https://github.com/user-attachments/assets/f94ecd85-2543-4617-a57f-eeb4ac81f958" />

df1_ffill = df1.ffill()
df1_ffill

<img width="1688" height="483" alt="Screenshot 2026-02-05 095820" src="https://github.com/user-attachments/assets/08300b1e-a636-4324-ad97-bdc05495ad56" />

df1_bfill = df1.bfill()
df1_bfill

<img width="1688" height="496" alt="Screenshot 2026-02-05 095902" src="https://github.com/user-attachments/assets/832be426-9846-4e82-bb2e-248881ead0ac" />

df1['CoapplicantIncome'] = df1['CoapplicantIncome'].fillna(df1['CoapplicantIncome'].mean())
df1

<img width="1697" height="489" alt="Screenshot 2026-02-05 100319" src="https://github.com/user-attachments/assets/1b5458ad-72fd-4177-9e1c-9329fd92d840" />

df1_dropna = df1.dropna()
df1_dropna

<img width="1742" height="499" alt="Screenshot 2026-02-05 100401" src="https://github.com/user-attachments/assets/ff9494b8-b76d-423b-8cb7-f62a203a8d8c" />

df1_dropna.to_csv('clean_data_new.csv', index=False)
df2 = pd.read_csv('clean_data_new.csv')
df2.head()
df2.info()
df2.describe()
sns.boxplot(x=df2['ApplicantIncome'])
plt.show()

<img width="764" height="582" alt="Screenshot 2026-02-05 100539" src="https://github.com/user-attachments/assets/d61951bb-147e-480c-b141-bd317c0049c0" />

Q1 = df2['ApplicantIncome'].quantile(0.25)
Q3 = df2['ApplicantIncome'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR)

<img width="1669" height="62" alt="Screenshot 2026-02-09 101635" src="https://github.com/user-attachments/assets/acd06087-83cc-48b8-b706-e933031c3763" />

outliers_iqr = df2[
    (df2['ApplicantIncome'] < (Q1 - 1.5 * IQR)) |
    (df2['ApplicantIncome'] > (Q3 + 1.5 * IQR))
]
outliers_iqr

<img width="1703" height="792" alt="Screenshot 2026-02-09 101805" src="https://github.com/user-attachments/assets/51704b22-0707-469b-aa2d-a1e8ba937d37" />

data_cleaned = df2[
    ~((df2['ApplicantIncome'] < (Q1 - 1.5 * IQR)) |
      (df2['ApplicantIncome'] > (Q3 + 1.5 * IQR)))
]
data_cleaned

<img width="1690" height="498" alt="Screenshot 2026-02-09 102017" src="https://github.com/user-attachments/assets/6a12c1bd-6ede-4e1c-bf1e-719b9e81d5f1" />

data = [1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,
        54,57,60,63,66,69,72,75,78,81,84,87,90,93]

df3 = pd.DataFrame(data, columns=['values'])
df3

z_scores = np.abs(stats.zscore(df3))
z_scores

threshold = 3
outliers_z = df3[z_scores > threshold]
print("Outliers:")
outliers_z

df3_cleaned = df3[z_scores <= threshold]
df3_cleaned


# Result
          Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method
