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


# CODE

Program developed by : Mirudhula D

Register number : 212221230060

## Loading the dataset:
~~~
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
~~~

## Removing unnecessary data variables:
~~~
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

~~~

## Detecting and removing outliers in current numeric data:

~~~
plt.figure(figsize=(12,10))
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
~~~

## Data visualization

## Line plots

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

## Bar plots:

~~~
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

~~~
## Histogram

~~~
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
~~~
## count plot
~~~
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
~~~

## Barplot
~~~
sns.boxplot(x="Sub-Category",y="Discount",data=df)
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
~~~
#KDE plot
~~~
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
~~~

#violin plot
~~~
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
~~~

#point plot
~~~
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
~~~

#Pie Chart
~~~
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
~~~

#HeatMap
~~~
df4=df.copy()
~~~

#encoding
~~~
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
~~~

#scaling
~~~
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])
~~~

#Heatmap
~~~
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
~~~


# OUPUT

## Initial Dataset:

## Cleaned Dataset:

![image](https://user-images.githubusercontent.com/94828147/204740004-5fb89c26-cc5b-44e0-9d55-258ff9537c9a.png)

![image](https://user-images.githubusercontent.com/94828147/204740034-c5fff03a-7e23-40bd-bd35-ada90a196eae.png)

## Removing Outliers:

![image](https://user-images.githubusercontent.com/94828147/204740111-7914e9c3-7870-4b3f-8257-b9f5785825c6.png)

![image](https://user-images.githubusercontent.com/94828147/204740150-60d1e364-3c3a-4b30-92ae-b887974cbfb2.png)

## Line PLot:

![image](https://user-images.githubusercontent.com/94828147/204740219-44b472e3-4576-4ff6-929c-127e9d88578e.png)

![image](https://user-images.githubusercontent.com/94828147/204740246-5bd08571-ee14-4014-9904-b4a11c8848ce.png)

![image](https://user-images.githubusercontent.com/94828147/204740282-b8afd0cc-f3b4-494a-8f34-4e0465c7f5b6.png)

![image](https://user-images.githubusercontent.com/94828147/204740297-ecbc1434-3d71-47e2-84a9-1cb02f7d6ee8.png)

![image](https://user-images.githubusercontent.com/94828147/204740320-90446021-b432-4044-924a-03e34527f480.png)

![image](https://user-images.githubusercontent.com/94828147/204740347-f2c7398b-4aab-45af-96ca-4c26edd90aa4.png)

## Bar Plots:

![image](https://user-images.githubusercontent.com/94828147/204740411-83a63b03-eeb8-47d6-81ea-5a2a0daaa8f4.png)

![image](https://user-images.githubusercontent.com/94828147/204740465-d4b90913-500a-4201-b9e7-b2acc4c79378.png)

![image](https://user-images.githubusercontent.com/94828147/204740526-9b512a18-5dbc-4cda-a8bf-5a470189dfe8.png)

![image](https://user-images.githubusercontent.com/94828147/204740547-cd81768c-77eb-4ec2-b0ce-842afb7e8593.png)

![image](https://user-images.githubusercontent.com/94828147/204740600-cb55b56a-7423-436b-ac9d-39e8ff7bd50f.png)

## Histograms:

![image](https://user-images.githubusercontent.com/94828147/204740674-4216250c-e08d-4d2e-bb46-266f0503c477.png)

![image](https://user-images.githubusercontent.com/94828147/204740692-55d22986-4a12-40e9-aae2-b07796b954cb.png)

![image](https://user-images.githubusercontent.com/94828147/204740767-85cb8771-eba7-415d-8f97-a1f023bddd18.png)

![image](https://user-images.githubusercontent.com/94828147/204740794-7e256e05-1d75-4415-9af0-d423446e3371.png)

![image](https://user-images.githubusercontent.com/94828147/204740823-b332dc27-85f7-4dde-a347-dcf9480d71a1.png)

## Count plots:

![image](https://user-images.githubusercontent.com/94828147/204740885-2b6dacd3-94db-462a-a00f-c91fd11e7270.png)

![image](https://user-images.githubusercontent.com/94828147/204740906-6874b2dd-bafd-4317-85ce-abc1b5554230.png)

![image](https://user-images.githubusercontent.com/94828147/204740933-5201f3b5-1dfa-4c2d-b71f-41ba7fb952ad.png)

![image](https://user-images.githubusercontent.com/94828147/204740985-ff1c8aff-e129-4155-9be6-df700981d3be.png)

![image](https://user-images.githubusercontent.com/94828147/204741006-a7583001-365b-4e10-ad72-4b75d2580a1d.png)

## Bar Charts:

![image](https://user-images.githubusercontent.com/94828147/204741058-40fbd7cd-d27e-4861-9f9d-0d9dcdaca5c0.png)

![image](https://user-images.githubusercontent.com/94828147/204741090-12a14e4c-fea0-42dc-be54-d08320642b50.png)

![image](https://user-images.githubusercontent.com/94828147/204741122-864cbdc3-96f8-422c-8dcc-ec0619c4c378.png)

![image](https://user-images.githubusercontent.com/94828147/204741165-1afdb564-774a-4672-a2cb-111cee6d6cc0.png)

![image](https://user-images.githubusercontent.com/94828147/204741216-31d10697-fdfa-4323-98cd-0261a970c14f.png)

![image](https://user-images.githubusercontent.com/94828147/204741244-0a86383e-c39c-41f0-b36f-0e74fe845cb0.png)

![image](https://user-images.githubusercontent.com/94828147/204741264-c4ae01c1-97b4-4583-8cbd-33a39f105d3a.png)

## KDE Plots:

![image](https://user-images.githubusercontent.com/94828147/204741326-0338d1d3-1f6a-411e-949f-d50c4d4c1f62.png)

![image](https://user-images.githubusercontent.com/94828147/204741346-be06374f-e2ac-4dca-9859-7ad18f7d1431.png)

## Violin Plot:

![image](https://user-images.githubusercontent.com/94828147/204741413-f28aad3c-4109-4397-9704-d4fe229f3eb9.png)

## Point Plots:

![image](https://user-images.githubusercontent.com/94828147/204741487-326a308d-a246-42e7-90aa-af784c8729e3.png)

![image](https://user-images.githubusercontent.com/94828147/204741510-813bf645-9dce-4b95-8cf8-e6398792ca91.png)

## Pie Charts:

![image](https://user-images.githubusercontent.com/94828147/204741570-cc798342-bc0b-4c67-a16c-2dd620db201c.png)

![image](https://user-images.githubusercontent.com/94828147/204741699-fbb7d0f2-f243-429b-b3e0-78d6abb9c112.png)

![image](https://user-images.githubusercontent.com/94828147/204741745-53f9e4a1-305a-4b7b-91e0-2735fe23ab20.png)

![image](https://user-images.githubusercontent.com/94828147/204741793-86ef6646-642b-41cc-aefb-bd5d17eb71b1.png)

![image](https://user-images.githubusercontent.com/94828147/204741839-712825d0-7f1b-4f79-8ec6-adcc1784d798.png)

![image](https://user-images.githubusercontent.com/94828147/204741817-6aa018f9-9b71-4009-a8f1-c2e49c8a4bf8.png)

## HeatMap:

![image](https://user-images.githubusercontent.com/94828147/204741911-afa42ef6-b08a-4ca0-bfdb-3d063e2c8f98.png)

## Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.


