# DAX Processes for Ben's Pizzeria: Order Activity and Inventory Management

After completing the data import, cleaning, and transformation in PostgreSQL, the processed data has been connected into Power BI. The data now includes calculated views for key areas like Order Activity and Inventory Management. The DAX processes are designed to provide clear insights into Order Activity and Inventory Management. The goal is to identify key trends in customer orders, sales, and inventory usage, and to pinpoint areas where efficiency can be improved. 

Simple DAX measures are used to address key questions. These measures include:
1. [Calculated Columns](#calculated-columns) 
2. [DAX Measures](#dax-measures)

## Calculated Columns
These columns classify or calcutale values at the row level, prior to aggregating the data:

- **Item Name & Category**: Combines the item name and its category for better readability in visualizations.
```DAX
item_name_cat = order_activity[item_name] & " (" & order_activity[item_cat] & ")"
```

- **Delivery Type**: Categorizes orders as either Delivery or Pick Up based on order activity.
```DAX
Delivery = IF(order_activity[delivery_1] = "True", "Delivery", "Pick Up")
```

- **Stock Remaining**: Calculates the proportion of remaining stock in relation to total inventory.
```DAX
Stock Remaining = DIVIDE(inventory_management_2[inventory_balance], inventory_management_2[total_inventory], 0)
```

## DAX Measures
These measures summarize data to answer key business questions related to order activity and inventory management.

- **Total Orders**: Counts the total number of orders.
```DAX
Total Orders = COUNT(order_activity[quantity]) 
```

- **Total Sold**: Sums the total quantity of items sold.
```DAX
Total Sold = SUM(order_activity[quantity])
```

- **Total Revenue**: Calculates total revenue by multiplying quantity by price.
```DAX
Total Revenue = SUMX(order_activity, order_activity[quantity] * order_activity[item_price])
```

- **Average Order Value**: Divides total revenue by total orders to find the average value.
```DAX
Average Order Value = DIVIDE([Total Revenue], [Total Orders], 0)
```

- **Total Cost**: Sums the total cost of ingredients used.
```DAX
Total Cost = SUM(inventory_management_1[ingredients_cost])
```

- **Item Cost**: Calculates the total cost for each item based on unit cost and quantity.
```DAX
Item Cost = SUMX(inventory_management_1, inventory_management_1[unit_cost] * inventory_management_1[recipe_quantity])
```

- **Stock %**: Calculates the percentage of stock remaining.
```DAX
Stock % = DIVIDE(SUM(inventory_management_2[inventory_balance]), SUM(inventory_management_2[total_inventory]))
```
---
These calculated columns and DAX measures will help Ben's Pizzeria spot trends and make better decisions to improve their new pizzeria.

<table style="width:100%; border-collapse: collapse; text-align: center;">
  <tr>
    <td style="width:50%; padding:10px; text-align: left;">
      ⬅️ <a href="https://mramadhankesapi.github.io/Data-Preparation-Processes_for_Bens-Pizzeria...Sales-and-Inventory-Analytics/" style="text-decoration: none; font-weight: bold; color: #007bff;">Data Preparation on PostgreSQL</a>
    </td>
    <td style="width:50%; padding:10px; text-align: right;">
      <a href="https://mramadhankesapi.github.io/Bens-Pizzeria...Sales-and-Inventory-Analytics/" style="text-decoration: none; font-weight: bold; color: #007bff;">📊 PhoneNow: Customer Churn Analytics</a> ➡️
    </td>
  </tr>
</table>
