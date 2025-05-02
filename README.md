# 🍕 Pizza Sales SQL Analysis

This project showcases exploratory SQL analysis performed on a fictional pizza sales dataset. The goal is to uncover business insights such as revenue performance, customer ordering patterns, and product trends. 

---



---

## 📊 Key Performance Indicators (KPIs)

| Metric                    | Result        | SQL Logic Summary                                    |
|---------------------------|---------------|------------------------------------------------------|
| Total Revenue             | \$817,860.05   | `SUM(total_price)`                                  |
| Average Order Value       | \$38.31        | `SUM(total_price) / COUNT(DISTINCT order_id)`       |
| Total Pizzas Sold         | 49,574         | `SUM(quantity)`                                     |
| Total Orders              | 21,350         | `COUNT(DISTINCT order_id)`                          |
| Avg Pizzas Per Order      | 2.32           | `SUM(quantity) / COUNT(DISTINCT order_id)`          |

---

## 📈 Trend Analysis

### Daily Order Trend
Analyzes which days see the most activity.


SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
Monthly Order Trend
Evaluates order volume by month.


SELECT DATENAME(MONTH, order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date);
🧾 Category & Size Insights
Sales by Pizza Category
Shows revenue share by category.


SELECT pizza_category,
       CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
       CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
Sales by Pizza Size
Displays which pizza sizes generate the most revenue.


SELECT pizza_size,
       SUM(total_price) AS total_revenue,
       SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS pct
FROM pizza_sales
GROUP BY pizza_size;
🥇 Top & Bottom Performers
Top 5 Pizzas by Revenue

SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;
Bottom 5 Pizzas by Quantity Sold

SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;
