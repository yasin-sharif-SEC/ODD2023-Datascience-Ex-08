# Ex-08-Data-Visualization-1
# AIM
To perform data visualization on a complex dataset and save the data to a file.

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
## STEP 1
Read the given data.

## STEP 2
Clean the data set using data cleaning process.

## STEP 3
Apply feature generation and selection techniques to all the features of the data set.

## STEP 4
Apply data visualization techniques to identify the patterns of the data.

# CODE
```python
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sb
import matplotlib.pyplot as plt

data=pd.read_csv('Superstore.csv')

# superstore file data cleaning
z=np.abs(stats.zscore(data['Sales']))
data=data[z<3]
z=np.abs(stats.zscore(data['Profit']))
data=data[z<3]

# 1.Which Segment has Highest sales?
segment=data.loc[:,["Segment","Sales"]]
segment=segment.groupby(by=["Segment"]).sum().sort_values(by="Sales")
plt.title('Segment with highest sales')
sb.barplot(x=segment.index,y="Sales",data=segment)
plt.show()

# 2.Which City has Highest profit?
city=data.loc[:,["City","Profit"]]
city=city.groupby("City").sum().sort_values(by="Profit")
city=city.query('Profit>2500')
plt.title('City with highest profit')
sb.barplot(x=city.index,y="Profit",data=city).set(ylabel='Profit')
plt.xticks(rotation=90)
plt.show()

# 3.Which ship mode is profitable?
ship=data.loc[:,["Ship Mode","Profit"]]
ship=ship.groupby(by=["Ship Mode"]).sum().sort_values(by="Profit")
plt.title('Profitable ship mode')
sb.barplot(x=ship.index,y="Profit",data=ship)
plt.show()

# 4.Sales of the product based on region.
region=data.loc[:,["Region","Sales"]]
region=region.groupby(by=["Region"]).sum().sort_values(by="Sales")
sb.barplot(x=region.index,y="Sales",data=region)
plt.show()

# 5.Find the relation between sales and profit.
plt.figure(figsize=(17,7))
sale_profit=data.query('Profit>0')
sb.scatterplot(x=sale_profit['Sales'],y=sale_profit['Profit'])
sale_loss=data.query('Profit<0')
sb.scatterplot(x=sale_loss['Sales'],y=sale_loss['Profit'])

# 6.Find the relation between sales and profit based on the following category.
# i) Segment
plt.figure(figsize=(17,7))
sp_segment=data.query('Sales<1000 and Profit>0')
sb.relplot(x=sp_segment['Sales'],y=sp_segment['Profit'],col=sp_segment['Segment'])

# ii) segment, ship mode
plt.figure(figsize=(17,7))
sp_segment=data.query('Sales<1000 and Profit>0')
sb.relplot(data=sp_segment,x='Sales',y='Profit',col='Segment',hue='Ship Mode',col_wrap=2)

# iii) segment, ship mode, region
plt.figure(figsize=(17,7))
sp_segment=data.query('Sales<1000 and Profit>0')
sb.relplot(data=sp_segment,x='Sales',y='Profit',col='Segment',hue='Ship Mode',style='Region',col_wrap=2)
```
# OUTPUT
### 1.Which Segment has Highest sales?
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/90073ca3-9e8f-4ae5-9654-d038aa448635)

### 2.Which City has Highest profit?
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/0cac11ce-2516-4cc1-8be1-007cac99b15c)

### 3.Which ship mode is profitable?
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/0251a780-488d-498f-b8c2-dc7a9eeae045)

### 4.Sales of the product based on region.
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/257b2c08-05ac-47ad-8be8-286fb82a12cb)

### 5.Find the relation between sales and profit.
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/acea44d6-7a86-4b07-b612-c07216f7d8f0)

### 6.Relation between sales and profit based on Segment
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/442ced72-3f39-4b87-9f01-88a2b61c8d93)

### 6.Relation between sales and profit based on Segment, Ship Mode
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/efbf4af8-3ef9-4c71-a7de-eaf59a63d51e)

### 6.Relation between sales and profit based on Segment, Ship Mode, Region
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-08/assets/142985837/e7302018-ce18-486f-8901-fd61dc06cfb1)

# Output
Thus, the given file is analyzed and various insights are discovered using data visualization.
