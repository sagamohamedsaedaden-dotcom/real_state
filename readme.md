# Overview

This analysis explores the real estate market in the United Arab Emirates, focusing on residential properties. It examines property types, sizes, locations, and prices to uncover trends and insights for buyers and investors.

The data, sourced from online listings, includes details such as number of bedrooms, bathrooms, floors, and price. Using Python, this project investigates city-wise pricing, popular property types, and how features influence market value, providing a clear picture of the United Arab Emirates housing market.

# The Questions

Below are the questions I want to answer in my project:

1. What is the typical number of bedrooms and bathrooms in UAE properties?
2. What percentage of UAE properties are sold furnished vs unfurnished?
3. How is off-plan vs ready property supply trending across emirates?
4. What are the most expensive cities for property in the UAE?

# Tools I Used

For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- **Python** : The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:

  - Pandas Library: This was used to analyze the data.
  - Matplotlib Library: I visualized the data.
  - Seaborn Library: Helped me create more advanced visuals.

- **Jupyter Notebooks** : The tool I used to run my Python scripts which let me easily include my notes and analysis.
- **Visual Studio Code**: My go-to for executing my Python scripts.
- **Git & GitHub**: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# Import Data

I start by importing necessary libraries and loading the dataset

```python
# Importing Libraries
import warnings

from warnings import filterwarnings;
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px
import seaborn as sns
plt.style.use('ggplot')
warnings.filterwarnings('ignore')

# Loading Datastes
df=pd.read_csv('world_real_estate_data(147k).csv')
UAE_Real_Estate=pd.read_csv('bayut_selling_properties.csv')

```

# Filter Real Estate in the UAE

To focus my analysis on the real estate market in UAE, I apply filters to the dataset, narrowing it down to properties in the United Arab Emirates

```python
df_UAE=df[df['country'] == 'UAE']
```

# The Analysis

Here’s how I approached each question:

## 1. What is the typical number of bedrooms and bathrooms in UAE properties?

To find the typical number of bedrooms and bathrooms in UAE properties,I filtered out invalid zero values for three columns.This query highlights the most common number of bedrooms, bathrooms, building sizes (in sqft)

View my notebook with detailed steps here: [UAE_real_state](UAE_real_state.ipynb)

## Visualize Data

```python
UAE_Real_Estate = UAE_Real_Estate[(UAE_Real_Estate[['baths', 'total_floors', 'total_building_area_sqft']] != 0).all(axis=1)]

columns_to_plot = ['beds', 'baths', 'total_building_area_sqft', 'total_floors']
fig, ax = plt.subplots(nrows=1, ncols=len(columns_to_plot), figsize=(14,8))

for i, col in enumerate(columns_to_plot):
    sns.boxplot(y=UAE_Real_Estate[col], ax=ax[i])
    ax[i].set_title(col)
```

## Results

![properties_in_UAE](images\properties.png)

Box plot visualizing UAE Property Features Distribution

## Insights:

- Most UAE properties feature compact 1–2 bedroom apartments with exactly 2 bathrooms as the dominant layout. The beds box shows 50% of listings fall between 1 and 2 beds. The baths box clusters tightly around 2, establishing the classic "1–2 bed, 2 bath" configuration as the clear market standard.

- Typical apartment sizes range from 600 to 1,000 sqft. The interquartile box for total_building_area_sqft centers between ~650 and ~950 sqft, confirming the dominance of efficient mid-size units perfectly suited for expats and golden-visa buyers.

- Buildings are predominantly mid-to-high-rise towers with 20 to 40 floors. The total_floors box sits solidly in this range with a median around 30, reflecting Dubai and Abu Dhabi's skyline of modern 20–50 storey developments. Rare outliers highlight iconic super-tall projects driving luxury premiums.

## 2. What percentage of UAE properties are sold furnished vs unfurnished?

To find the percentage of UAE properties sold furnished vs unfurnished, I counted the occurrences of each furnishing status in the dataset.

## Visualize Data

```python
furnishing_counts=UAE_Real_Estate['furnishing'].value_counts()
plt.pie(furnishing_counts,startangle=90,autopct='%.0f%%',labels=furnishing_counts.index)
plt.show()
```

## Results

![furnishing_counts](images\furnishing_counts.png)

Pie plot visualizing the Furnishing Status of Properties in UAE.

## Insights:

- Unfurnished properties dominate the UAE market with 76% of listings, indicating that most developers and sellers deliver shell-and-core units to allow buyers full customization for personal taste or rental flexibility.

- Furnished properties represent only 24% of the total supply, suggesting they command a significant price premium and are primarily targeted at ready-to-move-in expats or short-term investors seeking immediate rental income.

- The heavy skew toward unfurnished units highlights a clear buyer preference for cost-saving and personalization in the golden-visa segment, where investors prioritize long-term value over turnkey convenience.

## 3. How is off-plan vs ready property supply trending across emirates?

To find how How is off-plan vs ready property supply trending across emirates, I counted the occurrences of each completion status in the dataset.

## Visualize Data

```python
completion_status_counts =UAE_Real_Estate['completion_status'].value_counts()
plt.pie(completion_status_counts, labels=completion_status_counts.index, autopct='%1.0f%%')
plt.title('Property Completion Status in UAE')
plt.show()
```

## Results

![completion_status_counts](images\completion_status.png)
Pie plot visualizing the Property Completion Status in UAE.

## Insights

- Off-plan properties make up 40% of UAE listings, highlighting strong developer confidence and buyer appetite for payment-plan flexibility amid 2025's golden-visa boom.

- Ready properties dominate with 60% share, appealing to expats and investors seeking immediate occupancy or rental income without construction delays.

- The balanced split shows a maturing market where off-plan drives future growth (especially in RAK and Dubai South), while ready stock provides stability for risk-averse buyers.

## 4. What are the most expensive cities for property in the UAE?

To determine the most expensive cities for property in the UAE, I calculated the median property price for each city to identify which ones have the highest values.

## Visualize Data

```python
combined_df_average = combined_df.groupby('city')['price_in_USD'].median().sort_values(ascending=False)

sns.barplot(x=combined_df_average.values,
            y=combined_df_average.index,
            palette='dark:blue')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'${x/1000:.0f}k'))
```

## Results

![UAE_Median_Property_Price_by_City](images\UAE_Median_Property.png)
A bar plot visualizing UAE Median Property Price by City

## Insights

- Dubai commands the highest median property price in the plot at just under $600,000 USD, making it the clear leader among UAE cities for overall value.
- Abu Dhabi ranks second with a median close to $550,000 USD, showing a relatively small gap behind Dubai despite different market dynamics.
- Umm Al Quwain, Ras Al Khaimah, Sharjah, and Ajman cluster in a clear lower tier, offering the most affordable entry points outside the two major hubs.

# What I Learned

Throughout this project, I deepened my understanding of the UAE real estate market and enhanced my technical skills in Python, particularly in data cleaning, analysis, and visualization. Here are a few specific insights I gained:

- **Advanced Python Usage**: Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.
- **Data Cleaning Importance**: I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.

# Challenges I Faced

This project was not without its challenges, but it provided good learning opportunities:

- **Data Inconsistencies**: Handling missing or inconsistent data entries requires careful consideration and thorough data-cleaning techniques to ensure the integrity of the analysis.

- **Complex Data Visualization**: Designing effective visual representations of complex datasets was challenging but critical for conveying insights clearly and compellingly.

# Conclusion

This exploration into the real estate market in the United Arab Emirates has been incredibly informative. The insights I gained not only deepened my understanding but also provide actionable guidance for anyone looking to buy a home or invest in property in the UAE.
