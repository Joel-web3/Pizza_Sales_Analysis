# Pizza Sales Analysis

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Pizza%20Sales%20Visualization-1.png)

## Introduction
This project represents a meticulous exploration of sales data from a pizza store, aiming to uncover insights that drive its commercial performance. 
Using a combination of Excel & SQL for data extraction and manipulation, coupled with the robust visualization capabilities of Power BI, this analysis presents findings that range from revenue calculations to sales distribution across pizza categories.

## Problem Statement
- **Total Revenue**: The sum total of all pizza orders.
  
- **Average Order Value**: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
  
- **Total Pizzas Sold**: The sum of the quantities of all pizzas sold.
  
- **Total Orders**: The sum total of all orders.
  
- **Average Pizzas Per Order**: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by total number of orders.

## Charts Requirements

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Pizza%20Sales%20Visualization-2.png)

- **Daily Trend for Total Orders**: A bar chart that displays the daily trend of total orders over a specific time period. This chart will help me identify any patterns or fluctuations in order volumes on a daily basis.
  
- **Monthly Trend for Total Orders**: A line chart that illustrates the hourly trend of total orders throughout the day. This chart will help me identify peak hours or periods of high-order activity.
  
- **Percentage of Sales by Pizza Category**: A pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.
  
- **Percentage of Sales by Pizza Size**: A pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help me understand customer preferences for pizza sizes and their impact on sales.
  
- **Total Pizzas Sold by Pizza Category**: A funnel chart that represents the total number of pizzas sold for each pizza category. This chart will help me compare the sales performance of different pizza categories.
  
- **Top 5 Best-Sellers by Revenue, Total Quantity and Total Orders**: A bar chart highlighting the top 5 best-selling pizzas based on the Revenue, Total Quantity, and Total Orders. This chart will help me identify the most popular pizza options.
  
- **Bottom 5 Sellers by Revenue, Total Quantity and Total Orders**: A bar chart showcasing the bottom 5 worst-selling pizzas based on Revenue, Total Quantity, and Total Orders. This chart will help me identify the less popular pizza options.

## SQL Queries
**A. KPI’s**

**1. Total Revenue:**

SELECT SUM(total_price) Total_Revenue

FROM pizza_sales_excel_file;

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Total%20Revenue.png)

**2. Average Order Value:**

SELECT SUM(total_price) / COUNT(DISTINCT order_id) Average_Order_Value

FROM pizza_sales_excel_file;

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Average%20Order%20Value.png)

**3. Total Pizzas Sold:**

SELECT SUM(quantity) Total_Pizzas_Sold

FROM pizza_sales_excel_file;

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Total%20Pizzas%20Sold.png)

**4. Total Pizza Orders:**

SELECT COUNT(DISTINCT order_id) Total_Pizzas_Orders

FROM pizza_sales_excel_file;

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Total%20Pizza%20Orders.png)

**5. Average Pizzas Per Order:**

SELECT CAST (CAST (SUM(quantity) AS DECIMAL (10,2)) / 

CAST (COUNT(DISTINCT order_id) AS DECIMAL (10, 2)) AS DECIMAL (10,2)) Average_Pizzas_Per_order

FROM pizza_sales_excel_file;

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Average%20Pizzas%20Per%20Order.png)

**6. Daily Trend of Orders:**

SELECT DATENAME(DW, order_date) Order_Day,

COUNT(DISTINCT order_id) Total_Orders

FROM pizza_sales_excel_file

GROUP BY DATENAME(DW, order_date);

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Daily%20Trend%20of%20Orders.png)

**7. Monthly Trend of Orders:**

SELECT DATENAME(MONTH, order_date) Month_Name,

COUNT(DISTINCT order_id) Total_Orders

FROM pizza_sales_excel_file

GROUP BY DATENAME(MONTH, order_date)

ORDER BY Total_Orders DESC

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Monthly%20Trend%20of%20Orders.png)

**8. Percentage of Sales by Pizza Category:**

SELECT pizza_category, SUM(total_price) Total_Sales, SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales_excel_file) Percentage_of_Sales

FROM pizza_sales_excel_file

GROUP BY pizza_category

ORDER BY Percentage_of_Sales DESC;

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Percentage%20of%20Sales%20by%20Pizza%20Category.png)

**9. Percentage of Sales by Pizza Size:**

SELECT pizza_size, CAST (SUM(total_price) AS DECIMAL(10,2))  Total_Sales, CAST (SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales_excel_file) AS DECIMAL(10,2)) Percentage_of_Sales

FROM pizza_sales_excel_file

GROUP BY pizza_size

ORDER BY Percentage_of_Sales DESC;

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Percentage%20of%20Sales%20by%20Pizza%20Size.png)

**NB**: I can also get the data above per quarter using the query below (with 1 referring to the 1st quarter)

SELECT pizza_size, CAST (SUM(total_price) AS DECIMAL(10,2)) Total_Sales, CAST (SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales_excel_file WHERE DATEPART(QUARTER, order_date)=1) AS DECIMAL(10,2)) Percentage_of_Sales

FROM pizza_sales_excel_file

WHERE DATEPART(QUARTER, order_date)=1

GROUP BY pizza_size

ORDER BY Percentage_of_Sales DESC

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Percentage%20of%20Sales%20by%20Quarter.png)

**10. Top 5 Pizzas by Revenue:**

SELECT TOP 5 pizza_name, SUM(total_price) Total_Revenue

FROM pizza_sales_excel_file

GROUP BY pizza_name

ORDER BY Total_Revenue DESC 

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Top%205%20Pizzas%20by%20Revenue.png)

**11. Bottom 5 Pizzas by Revenue:**

SELECT TOP 5 pizza_name, SUM(total_price) Total_Revenue

FROM pizza_sales_excel_file

GROUP BY pizza_name

ORDER BY Total_Revenue ASC 

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Bottom%205%20Pizzas%20by%20Revenue.png)

**12. Top 5 Pizzas by Quantity:**

SELECT TOP 5 pizza_name, SUM(quantity) Total_Quantity

FROM pizza_sales_excel_file

GROUP BY pizza_name

ORDER BY Total_Quantity DESC 

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Top%205%20Pizzas%20by%20Quantity.png)

**13. Bottom 5 Pizzas by Quantity:**

SELECT TOP 5 pizza_name, SUM(quantity) Total_Quantity

FROM pizza_sales_excel_file

GROUP BY pizza_name

ORDER BY Total_Quantity ASC 

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Bottom%205%20Pizzas%20by%20Quantity.png)

**14. Top 5 Pizzas by Total Orders:**

SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) Total_Orders

FROM pizza_sales_excel_file

GROUP BY pizza_name

ORDER BY Total_Orders DESC 

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Top%205%20Pizzas%20by%20Total%20Orders.png)

**15.  Bottom 5 Pizzas by Total Orders:**

SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) Total_Orders

FROM pizza_sales_excel_file

GROUP BY pizza_name

ORDER BY Total_Orders ASC 

![](https://github.com/Joel-web3/Joel-s_Portfolio/blob/main/Bottom%205%20Pizzas%20by%20Total%20Orders.png)

## Key Insights From the Data Analytics

📅 There's an influx of customers on Fridays and Saturdays. So allocating more resources such as staff and inventory to match anticipated demands on these days will help improve service delivery and increase sales.

🍕 The Classic category, especially the Classic Deluxe Pizza, is already a hit amongst customers. Hence, augmenting marketing efforts around the Classic Deluxe Pizza with highlighted promotions and creative bundles will further enhance its visibility and increase sales.

🥇 With a pronounced preference for large-size pizzas, one can introduce attractive upselling (or upsizing) offers and combo deals that incentivize choosing large pizzas.

🏆 As the Thai Chicken Pizza is a significant revenue generator, one can explore price elasticity to find the optimal price point that maximizes revenue without deterring buyers.

🐌 Finally, the underperformance of Brie Carre Pizza presents an opportunity for a strategic revamp, either through marketing efforts, pricing adjustments, or a customer survey that can foster product modification. I’m a staunch advocate for robust two-way communication channels because, when done right, can lead to enhanced customer satisfaction and retention.
