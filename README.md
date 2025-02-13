# Python-EDA-Project
EDA project on Google Play Store Dataset

---

## **Project Overview: Google Play Store EDA**
### **Objective**
This project analyzes the **Google Play Store dataset** to uncover insights about app ratings, categories, pricing, reviews, and other key metrics.

---

## **1. Importing Necessary Libraries**
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```
### **Explanation**
- `numpy`: Used for numerical operations.
- `pandas`: Handles data manipulation and analysis.
- `matplotlib.pyplot`: Creates visualizations.
- `seaborn`: Provides enhanced visualization capabilities.

---

## **2. Loading the Dataset**
```python
df = pd.read_csv("googleplaystore.csv")
df.head()
```
### **Explanation**
- Reads the dataset from a CSV file into a Pandas DataFrame.
- `df.head()` displays the first few rows of the dataset.

---

## **3. Checking Data Information & Cleaning**
```python
df.info()
df.isnull().sum()
df.duplicated().sum()
df.drop_duplicates(inplace=True)
```
### **Explanation**
- `df.info()`: Checks data types and non-null counts.
- `df.isnull().sum()`: Identifies missing values.
- `df.duplicated().sum()`: Counts duplicate rows.
- `df.drop_duplicates(inplace=True)`: Removes duplicate records.

---

## **4. Handling Missing Values**
```python
df.dropna(inplace=True)
```
### **Explanation**
- Drops all rows containing missing values to ensure a clean dataset.

---

## **5. Data Type Conversion**
```python
df['Reviews'] = pd.to_numeric(df['Reviews'], errors='coerce')
df['Size'] = df['Size'].str.replace('M', '').str.replace('k', '').replace('Varies with device', np.nan).astype(float)
df['Installs'] = df['Installs'].str.replace(',', '').str.replace('+', '').astype(float)
```
### **Explanation**
- Converts **Reviews** column to numeric values.
- Cleans the **Size** column by removing 'M' and 'k' and replacing non-numeric values.
- Cleans **Installs** column by removing commas and '+' signs and converting it to numeric.

---

## **6. Exploring Data Distribution**
```python
plt.figure(figsize=(10,5))
sns.histplot(df['Rating'].dropna(), bins=30, kde=True)
plt.title("Distribution of App Ratings")
plt.xlabel("Rating")
plt.ylabel("Count")
plt.show()
```
### **Explanation**
- Creates a histogram of app ratings.
- Uses `sns.histplot()` for a clear visual representation.
- The **KDE (Kernel Density Estimation)** line shows the data distribution.

---

## **7. Most Common Categories**
```python
plt.figure(figsize=(12,6))
sns.countplot(y=df['Category'], order=df['Category'].value_counts().index)
plt.title("App Categories Distribution")
plt.xlabel("Count")
plt.ylabel("Category")
plt.show()
```
### **Explanation**
- Counts the number of apps in each category.
- Uses `sns.countplot()` for a horizontal bar chart.
- Orders categories from most to least frequent.

---

## **8. Relationship Between Reviews & Ratings**
```python
plt.figure(figsize=(8,5))
sns.scatterplot(x=df['Reviews'], y=df['Rating'])
plt.xscale('log')
plt.title("Reviews vs Rating")
plt.xlabel("Number of Reviews (Log Scale)")
plt.ylabel("Rating")
plt.show()
```
### **Explanation**
- **Scatter plot** shows the correlation between reviews and ratings.
- **Log scale** makes large numbers easier to visualize.

---

## **9. Free vs Paid Apps**
```python
df['Type'].value_counts().plot(kind='bar', color=['blue', 'orange'])
plt.title("Free vs Paid Apps")
plt.xlabel("App Type")
plt.ylabel("Count")
plt.xticks(rotation=0)
plt.show()
```
### **Explanation**
- Compares the count of **Free vs Paid apps** using a bar chart.

---

## **10. Top 10 Most Installed Apps**
```python
top_installed = df[['App', 'Installs']].sort_values(by='Installs', ascending=False).head(10)
plt.figure(figsize=(10,5))
sns.barplot(x=top_installed['Installs'], y=top_installed['App'], palette='coolwarm')
plt.title("Top 10 Most Installed Apps")
plt.xlabel("Number of Installs")
plt.ylabel("App Name")
plt.show()
```
### **Explanation**
- Sorts apps by the highest **Installs** and selects the top 10.
- Uses a **bar chart** to display the most popular apps.

---

## **Key Findings**
1. **Rating Distribution**: Most apps have a rating between **4.0 and 4.5**.
2. **Categories**: Some categories dominate the Play Store (e.g., **Tools, Entertainment, and Productivity**).
3. **Free vs Paid**: Most apps are **free**.
4. **Top Apps**: The most installed apps are **social media and communication-related**.

---
**Thank You!**
