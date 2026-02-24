# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING

### Step 1 : Import required packages

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

### Step 2 : Load the Dataset

data = pd.read_csv("titanic_dataset.csv")
print("\nDataset Loaded Successfully\n")
print(data.head())
print("\nDataset Info:\n")
print(data.info())
print(data.describe())

### Step 3 : Data cleansing - Handling missing values

for column in data.columns:
    if pd.api.types.is_numeric_dtype(data[column]):
        data[column] = data[column].fillna(data[column].median())
    else:
        data[column] = data[column].fillna(data[column].mode()[0])
print("\nMissing values handled successfully.\n")

### Step 4 : Box plot to analyse outliers (Age & Fare)

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Age"])
plt.title("Boxplot - Age")
plt.show()

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Fare"])
plt.title("Boxplot - Fare")
plt.show()

### Step 5 : Remove outliers using IQR method

def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

data = remove_outliers_iqr(data, "Age")
data = remove_outliers_iqr(data, "Fare")

print("Outliers removed using IQR method.\n")

### Step 6 : Countplot for categorical data

plt.figure(figsize=(6,4))
sns.countplot(x="Survived", data=data)
plt.title("Countplot - Survival Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Sex", data=data)
plt.title("Countplot - Gender Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Pclass", data=data)
plt.title("Countplot - Passenger Class Distribution")
plt.show()

### Step 7 : Displot for univariate 

sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()

sns.displot(data["Fare"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Fare Distribution")
plt.show()

### Step 8 : Cross tabulation

print("\nCross Tabulation: Sex vs Survived\n")
print(pd.crosstab(data["Sex"], data["Survived"]))

print("\nCross Tabulation: Pclass vs Survived\n")
print(pd.crosstab(data["Pclass"], data["Survived"]))

###  Step 9 : Heatmap for Correlation analysis

plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()

## OUTPUT

<img width="918" height="771" alt="image" src="https://github.com/user-attachments/assets/9367f8ab-2a54-4a5a-9304-0b6b4e192a14" />
<img width="1033" height="788" alt="Screenshot 2026-02-21 093421" src="https://github.com/user-attachments/assets/d02201fe-8654-417b-b236-ef3dd48fa38d" />
<img width="1038" height="509" alt="Screenshot 2026-02-21 102428" src="https://github.com/user-attachments/assets/21da6485-886b-416b-93b1-3a904b3ac1f1" />
<img width="1784" height="762" alt="Screenshot 2026-02-24 151542" src="https://github.com/user-attachments/assets/b72f36d2-67b7-4e75-a7f2-3a27ffab817a" />
<img width="1051" height="781" alt="Screenshot 2026-02-24 154457" src="https://github.com/user-attachments/assets/1df62c59-35c0-436b-9abf-8916d715665d" />
<img width="1037" height="361" alt="Screenshot 2026-02-24 160325" src="https://github.com/user-attachments/assets/d68ab579-1360-4ea8-ac67-7c35330d43f7" />
<img width="949" height="831" alt="Screenshot 2026-02-24 160415" src="https://github.com/user-attachments/assets/8e805d2a-fa8c-4933-9600-821c3775ee9b" />
<img width="802" height="210" alt="Screenshot 2026-02-24 160424" src="https://github.com/user-attachments/assets/a005cc04-ba54-49a1-91c3-1fd516940601" />
<img width="903" height="348" alt="Screenshot 2026-02-24 160440" src="https://github.com/user-attachments/assets/7436abd2-3121-4912-a1bb-1ee8c1562923" />
<img width="800" height="852" alt="Screenshot 2026-02-24 160456" src="https://github.com/user-attachments/assets/3ef021b6-eb10-4dfc-ba5e-f25286f38b9f" />
<img width="644" height="535" alt="Screenshot 2026-02-24 160505" src="https://github.com/user-attachments/assets/233b0691-8247-4279-ba43-93cf59664015" />
<img width="644" height="535" alt="Screenshot 2026-02-24 160505" src="https://github.com/user-attachments/assets/b91aac68-f838-4742-839c-41047808819e" />
<img width="803" height="459" alt="Screenshot 2026-02-24 160522" src="https://github.com/user-attachments/assets/25eba6c1-b23e-41df-815b-a36c5002682a" />
<img width="723" height="525" alt="Screenshot 2026-02-24 160530" src="https://github.com/user-attachments/assets/7ad03409-f4b7-47de-a879-1569b45ac727" />
<img width="699" height="517" alt="Screenshot 2026-02-24 160536" src="https://github.com/user-attachments/assets/a4132a90-0e71-4015-9ce1-db15fb14aee5" />
<img width="718" height="524" alt="Screenshot 2026-02-24 160542" src="https://github.com/user-attachments/assets/bf507710-28d4-4b7d-a95b-602481e422ae" />
<img width="876" height="841" alt="Screenshot 2026-02-24 160550" src="https://github.com/user-attachments/assets/09066b41-2aa1-4c92-a757-7a7b233b9e4f" />
<img width="773" height="554" alt="Screenshot 2026-02-24 160600" src="https://github.com/user-attachments/assets/d26bb775-11a0-4461-bc9c-127b7c555e26" />
<img width="571" height="631" alt="Screenshot 2026-02-24 160608" src="https://github.com/user-attachments/assets/f1bb3ead-cccb-461b-8f2e-705d9d5a747b" />
<img width="571" height="631" alt="Screenshot 2026-02-24 160608" src="https://github.com/user-attachments/assets/f266ef40-b5c6-470b-a69c-bb151d9bd4bc" />
<img width="918" height="771" alt="Screenshot 2026-02-24 160649" src="https://github.com/user-attachments/assets/cc60ed80-2cf3-4ce8-a82a-adfbb4089a1c" />


# RESULT
        Thus , the EDA Analysis using Python is completed successfully
