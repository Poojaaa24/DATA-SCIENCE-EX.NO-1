#EX.NO:1
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
```
import pandas as pd
import numpy as np
from scipy import stats

# STEP 1: Read the given Data

df = pd.read_csv("Loan_data.csv")

print("Original Dataset")
print(df.head())

# STEP 2: Get information

print("\nDataset Information")
print(df.info())

print("\nMissing Values")
print(df.isnull().sum())

# STEP 3: Remove null values

df['Gender'] = df['Gender'].fillna(df['Gender'].mode()[0])
df['Dependents'] = df['Dependents'].fillna(df['Dependents'].mode()[0])
df['Self_Employed'] = df['Self_Employed'].fillna(df['Self_Employed'].mode()[0])
df['LoanAmount'] = df['LoanAmount'].fillna(df['LoanAmount'].median())
df['Loan_Amount_Term'] = df['Loan_Amount_Term'].fillna(df['Loan_Amount_Term'].median())
df['Credit_History'] = df['Credit_History'].fillna(df['Credit_History'].mode()[0])

# Remove duplicates
df = df.drop_duplicates()

print("\nCleaned Dataset")
print(df.head())

print("\nMissing Values After Cleaning")
print(df.isnull().sum())

# STEP 4: Save cleaned data

df.to_csv("Cleaned_Loan_data.csv", index=False)

print("\nCleaned data saved successfully")

# STEP 5: Remove Outliers using IQR

data = pd.read_csv("heights.csv")

print("\nHeights Dataset")
print(data)

Q1 = data['height'].quantile(0.25)
Q3 = data['height'].quantile(0.75)
IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

print("\nLower Limit =", lower_limit)
print("Upper Limit =", upper_limit)

# Detect outliers
iqr_outliers = data[
    (data['height'] < lower_limit) |
    (data['height'] > upper_limit)
]

print("\nOutliers using IQR")
print(iqr_outliers)

# Remove IQR outliers
iqr_clean = data[
    (data['height'] >= lower_limit) &
    (data['height'] <= upper_limit)
]

print("\nDataset after IQR Removal")
print(iqr_clean)

# STEP 6: Remove Outliers using Z-score

z = np.abs(stats.zscore(iqr_clean['height']))

zscore_clean = iqr_clean[z < 3]

print("\nDataset after Z-score Removal")
print(zscore_clean)
```
<img width="1140" height="742" alt="image" src="https://github.com/user-attachments/assets/760123c3-8880-43c7-937f-8314f6174062" />
<img width="1140" height="630" alt="image" src="https://github.com/user-attachments/assets/841cfd1f-981c-42cf-8a1a-9b6043010879" />
<img width="1141" height="719" alt="image" src="https://github.com/user-attachments/assets/2a5c1a14-6b39-41b1-8e23-16e958036d29" />
<img width="1141" height="509" alt="image" src="https://github.com/user-attachments/assets/8ef365be-0978-4e13-b9e4-8cc790d247e2" />

# Result
Thus the given dataset was read successfully, null values and duplicate values were removed, and the cleaned data was saved successfully. Outliers were detected and removed using both IQR and Z-score methods using Python.
