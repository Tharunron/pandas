# 🐼 Pandas Data Cleaning & Analysis Guide

Welcome to this concise guide and template for **data cleaning and analysis** using **Pandas** — the go-to Python library for data manipulation. This repository demonstrates essential steps and best practices to load, clean, explore, and prepare datasets for further analysis or modeling.

---

## 🚀 Features

- Loading datasets with pandas
- Handling missing data efficiently
- Dropping irrelevant columns
- Detecting and treating outliers using the IQR method
- Simple data visualization setup
- Writing clean and reproducible pandas code

---

## 📋 Table of Contents

1. [Setup](#setup)  
2. [Loading Data](#loading-data)  
3. [Exploring Data](#exploring-data)  
4. [Handling Missing Values](#handling-missing-values)  
5. [Dropping Irrelevant Columns](#dropping-irrelevant-columns)  
6. [Detecting and Removing Outliers](#detecting-and-removing-outliers)  
7. [Basic Visualization](#basic-visualization)  
8. [Saving Cleaned Data](#saving-cleaned-data)  
9. [Tips & Best Practices](#tips--best-practices)  

---

## Setup

Make sure you have pandas, numpy, matplotlib, and seaborn installed:

```bash
pip install pandas numpy matplotlib seaborn
import pandas as pd

df = pd.read_csv('path/to/your/dataset.csv')
print(df.head())
print(df.info())
print(df.describe())         # Summary statistics for numeric columns
print(df.isnull().sum())     # Count missing values per column
print(df.columns)            # List all columns
print(df.shape)              # Get number of rows and columns
Handling Missing Values
Drop columns with too many missing values

Fill missing numeric values with median or mean

Fill missing categorical values with mode
# Drop column with many missing values
df.drop(columns=['Cabin'], inplace=True, errors='ignore')

# Fill missing Age with median
df['Age'] = df['Age'].fillna(df['Age'].median())

# Fill missing Embarked with mode
df['Embarked'] = df['Embarked'].fillna(df['Embarked'].mode()[0])
df.drop(columns=['PassengerId', 'Name', 'Ticket'], inplace=True)
Q1 = df['Fare'].quantile(0.25)
Q3 = df['Fare'].quantile(0.75)
IQR = Q3 - Q1

filtered_df = df[(df['Fare'] >= Q1 - 1.5 * IQR) & (df['Fare'] <= Q3 + 1.5 * IQR)]
df.to_csv('cleaned_data.csv', index=False)

