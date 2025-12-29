# blinkit Analysis

## 📌 Project Overview

This project presents a comprehensive **sales, customer satisfaction,inventory distribuction and ** of **Blinkit** using **Python**.  
The goal is to identify key business insights, performance trends, and optimization opportunities using KPIs and interactive visualizations.

![Blinkit Dashboard](https://github.com/banapuram-mahidhar/blinkit-Analysis/blob/88bbba5d8a380d610a5804303cb08ca52abfee0d/Blinkit_project_img.png)


This dashboard helps stakeholders understand:
- Sales performance across products and outlets
- Customer preferences based on fat content
- Impact of outlet size, location, and establishment year on sales

  ## 🎯 Business Objective
To conduct a detailed analysis of:
- **Sales performance**
- **Customer satisfaction**
- **Inventory distribution**

and provide **data-driven insights** to support better business decisions.

## 📊 Key Performance Indicators (KPIs)
The dashboard focuses on the following KPIs:

- **Total Sales** – Overall revenue generated  
- **Average Sales** – Average revenue per transaction  
- **Number of Items** – Total items sold  
- **Average Rating** – Customer satisfaction score  


### importing liberies

```python
import pandas as pd
import numpy as np
import matplotlib .pyplot as plt
import seaborn as sns

import plotly.express as px
from plotly.express import colors
import plotly .graph_objects as go
import plotly .io as pio
import plotly.colors as cloors
pio.templates.default = "plotly_white"
```

### Loading data

```python
df = pd.read_csv(r"C:\Users\massm\OneDrive\New folder\python_in_VS\blinkit_data.csv")
df.head()
```

### Understanding the data

```python
print("size of the data :",df.shape)
df.columns
df.dtypes

```

### Data Cleaning

```python
print(df["Item Fat Content"].unique())

```

## Business Requirements

### KIP'S Requirements

```python
# Total_sales
total_sales =df["Sales"].sum()

#Average_sales
Average_sales =df["Sales"].mean()

#No_of_items_Sold
no_of_items_sold =df["Sales"].count()

#Average_rating
Average_rating = df["Rating"].mean()

#Display
print(f"Total sales : ${total_sales:,.0f}")
print(f"Average sales : {Average_sales:,.1f}")
print(f"no of items sold : {no_of_items_sold:,.0f}")
print(f"average rating :{Average_rating:,.0f}")

```

## Charts Requirements

### 1. Sales by fat content

```python
df.tail()

sales_by_fat =df.groupby("Item Fat Content")["Sales"].sum().reset_index()
fig = px.pie(sales_by_fat,values="Sales",names="Item Fat Content",
             hole = 0.5,color_discrete_sequence = px.colors.qualitative.Pastel)
fig.update_traces(textposition = "inside",textinfo ="percent+label")
fig.update_layout(title_text = "sales analysis by fat content",title_font=dict(size=24))
fig.show()

```

### 2.Total sales by items Types

```python
sales_by_items = (df.groupby("Item Type")["Sales"]
                  .sum()
                  .reset_index()
                  .sort_values(by="Sales", ascending=False))

fig = px.bar(sales_by_items,x="Item Type",
             y="Sales",title="Total sales by items Types")

# Rotate x-axis labels to 90 degrees
fig.update_layout(
    xaxis_tickangle=90)

fig.show()

```

### 3.Fat content by Outlet for Total Sales

```python
df.head()

fat_content_outlet = (
    df.groupby(["Outlet Location Type", "Item Fat Content"])["Sales"]
      .sum()
      .reset_index()
)

fig = px.bar(
    fat_content_outlet,
    x="Outlet Location Type",
    y="Sales",
    color="Item Fat Content",
    title="Total Sales by Fat Content across Outlet Locations",
    barmode="group"  #  side-by-side bars
)                    # if you want stack then mention "stack"

fig.show()
```

**For Better Understanding**

```python
fat_content_outlet_pivot = fat_content_outlet.pivot(
    index="Outlet Location Type",
    columns="Item Fat Content",
    values="Sales"
)
fat_content_outlet_pivot

```

### 4.Total sales by outlet Establishment

```python
Sales_by_Outlet_Establishment = (
    df.groupby("Outlet Establishment Year", as_index=False)["Sales"]
      .sum()
      .sort_values("Outlet Establishment Year")
)

fig = px.line(
    Sales_by_Outlet_Establishment,
    x="Outlet Establishment Year",
    y="Sales",
    markers=True,
    title="Total Sales by Outlet Establishment Year"
)

fig.show()

```

### 5.Sales by outlet size

```python
Sales_by_Outlet_size = df.groupby("Outlet Size")["Sales"].sum().reset_index()
fig = px.pie(Sales_by_Outlet_size,values="Sales",names="Outlet Size",
             hole = 0.5,color_discrete_sequence = px.colors.qualitative.Pastel)
fig.update_traces(textposition = "inside",textinfo ="percent+label")
fig.update_layout(title_text = "Sales_by_Outlet_size",title_font=dict(size=24))
fig.show()

```

### 6.Sales by Outlet Location

 **vartical bar chart**

```python
Sales_by_Outlet_location = df.groupby("Outlet Location Type")["Sales"].sum().reset_index()
fig = px.bar(
  Sales_by_Outlet_location,
    x="Outlet Location Type",
    y="Sales",
    title="Outlet_Location_Type",
    text_auto=True
)
fig.show()

```
**Horizontal bar chart**

```python
Sales_by_Outlet_location = (
    df.groupby("Outlet Location Type", as_index=False)["Sales"]
      .sum()
      .sort_values("Sales", ascending=True)  # best for horizontal
)

fig = px.bar(
    Sales_by_Outlet_location,
    x="Sales",                       
    y="Outlet Location Type",        
    title="Sales by Outlet Location Type",
    text_auto=True,
    orientation="h"                  #  horizontal bars
)

fig.show()

```

## Conclusion

This Blinkit Sales Analysis project provides a clear understanding of how different factors influence sales performance and customer behavior. 

The analysis shows that product fat content plays an important role in customer purchasing decisions, with certain categories generating higher sales.

Medium and large-sized outlets contribute the most to overall revenue, indicating better inventory handling and customer reach.


The study also reveals that outlet location and establishment year significantly impact sales, with well-established outlets and prime locations performing better. 

Additionally, top-performing item types consistently drive revenue, while customer ratings help highlight areas where product quality and service can be improved.

Overall, this dashboard enables stakeholders to identify growth opportunities, optimize product distribution, improve outlet performance, and make data-driven business decisions using meaningful KPIs and interactive visualizations.


## 👤 Author

**Banapuram Mahidhar**  

Aspiring Data Analyst 

📧 Email: banapurammahidhar@gmail.com 

🔗 LinkedIn: www.linkedin.com/in/banapuram-mahidhar-77914133a

# Thank you for taking the time to review this project.  
# I appreciate your interest and welcome any feedback or suggestions.

