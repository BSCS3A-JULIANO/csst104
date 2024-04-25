import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sne

**1.Data Loading**

df = pd.read_csv('hardwareStore.csv')
df

**2. initial data analysis**

df_stats = df.describe()
print(df_stats)

unique = df['CATEGORY_NAME'].value_counts()
print(unique)


**3.category analysis**

category_name_counts = df["CATEGORY_NAME"].value_counts()
plt.figure(figsize=(6,6))
category_name_counts.plot(kind = 'bar' )
plt.title("distribution of products")
plt.xlabel('category')
plt.ylabel('number of products')
plt.show()

**4. cost and price analysis**

sc = df["STANDARD_COST"].mean()
alp = df["LIST_PRICE"].mean()
hsc = df["STANDARD_COST"].max()
hlp = df["LIST_PRICE"].max()

print("average standard cost:",[sc])
print("average list price:",[alp])
print("highest standard cost:",[hsc])
print("highest list price:",[hlp])




**5. location analysis**

grouped = df.groupby (['CATEGORY_NAME','COUNTRY_NAME']).size().reset_index(name='quality')
highest_qty = grouped['quality'].idxmax()
highest_qty
location_with_highest_stock = grouped.loc[highest_qty]

**6. insights and reporting**

report = f"""
***Exploratory Data Analysis Report***
***Summary statistics***
{df_stats}
***Category Count***
{unique}

***Highest Product Count***
{category_name_counts}

***Average Standard Count***
{sc}
***Average List Price***
{alp}
***Highest Standard Cost***
{hsc}
***Highest List Price***
{hlp}

***Location With Highest Quantity of Products In Stock***
{location_with_highest_stock}
"""

print(report)
with open('report.text','w') as f:
  f.write(report)
