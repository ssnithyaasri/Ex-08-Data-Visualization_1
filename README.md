# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.

#PROGRAM

Developed by: NITHYAA SRI SS
Register no: 212222230100

# CODE
```
# loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
```

# removing unnecessary data variables
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
detecting and removing outliers in current numeric data
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()

```
# data visualization

# line plots
```
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```
# Histogram
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```
# count plot
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```
# Barplot
```
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
# KDE plot
```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
```
# violin plot
```
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
# Pie Chart
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
```
# HeatMap
```
df4=df.copy()
encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])
scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])
  ```                                             
# Heatmap
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()

```
# OUPUT
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/e445ba74-f877-4309-a424-cf2e07721ba5)

![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/5d061db5-c6e8-48e0-856b-eaa01252d489)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/8d0347f0-256a-48ed-b2f8-42db2c5b9f8f)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/b09fbd05-051f-4ddc-8f5b-2b2a763a97dc)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/a38fcda0-b194-42b4-a6ea-192a321678f7)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/234606e5-b955-4230-a3fe-d965b305ff39)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/310bd4e2-559e-4ab0-96f5-60ec7588c1c9)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/89a70d33-e0e0-4a12-93c8-647fdb6bb2b7)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/f04e1889-4a6b-4aa4-8250-b82836d846e5)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/11f91410-001d-4885-93c0-40c195d3db94)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/aadec94c-5e95-4f9b-a7d5-3a9a77f8fc85)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/f36bbbfc-7dc6-4a6f-b5ae-819476ee1d67)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/6392f846-215a-4b48-80b4-c449cab2586f)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/cc2bc0d6-4e68-48e8-ae34-b2fa93d25bd9)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/3c9b2060-7135-4037-a53e-0285f4b5f8ac)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/10800f38-0675-4b08-9d0c-18f2cc16613c)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/40223a08-eeed-40ac-8208-8b28bf2406a4)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/b5893f5b-ef97-4654-94e0-106491038a2b)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/3ecbc41c-17d6-4f74-bfed-830e0e65c090)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/d4af010e-a3e0-411f-8182-05e2a96c0990)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/152ce382-8aae-4aed-a74f-88c78d1089b9)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/1fb95fc7-c6d4-4c29-bdcf-d94f01904760)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/fcfbff9e-17d4-470c-a3c9-dd12a236c0bf)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/01d40ae2-9ef3-4c00-8b98-44b27d650973)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/5f19dc46-e92c-41aa-9e0a-7ab5c64dd1ee)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/55246205-903f-477e-abdc-61b5363f91ec)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/7e781eed-cf0a-4b5a-a4d8-6fe501726be6)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/e935a7e9-b27c-4985-9712-6536e172980a)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/2c7506f1-74cc-41b7-8906-4948727a36a8)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/9c6a18fd-16d2-430d-abfc-7c9c32198665)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/a9693b51-6f3e-4b95-b4b8-39177343c492)
![image](https://github.com/premalatha-sureshbabu/Ex-08-Data-Visualization_1/assets/120620842/51c8f78b-3e49-4c8f-ae82-7ef086700abc)

# Result:

Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.












