import pandas as pd
import matplotlib.pyplot as plt

# 1. Load Dataset
df = pd.read_csv("sales_data.csv")

# 2. Data Cleaning
df.dropna(inplace=True)  # Handle missing values
df['Date'] = pd.to_datetime(df['Date'])

# 3. Key Metrics Calculation

# Total Sales
total_sales = df['Total_Sales'].sum()

# Total Quantity Sold
total_quantity = df['Quantity'].sum()

# Best-Selling Product (by revenue)
best_product = df.groupby('Product')['Total_Sales'].sum().idxmax()

# Sales by Product
product_sales = df.groupby('Product')['Total_Sales'].sum()

# Sales by Region
region_sales = df.groupby('Region')['Total_Sales'].sum()

# 4. Visualization

# Bar Chart: Sales by Product
plt.figure()
product_sales.plot(kind='bar')
plt.title("Total Sales by Product")
plt.xlabel("Product")
plt.ylabel("Total Sales")
plt.show()

# Pie Chart: Sales by Region
plt.figure()
region_sales.plot(kind='pie', autopct='%1.1f%%')
plt.title("Sales Distribution by Region")
plt.ylabel("")
plt.show()

# 5. Print Summary
print("Total Sales:", total_sales)
print("Total Quantity Sold:", total_quantity)
print("Best-Selling Product:", best_product)
