# 🍕 Pizza Sales Analysis

## 📌 Overview
This project analyzes pizza sales data to derive meaningful insights using SQL for data processing and Tableau for visualization. The key performance indicators (KPIs) and visualizations help in understanding sales trends, customer preferences, and product performance.

## 📂 Table of Contents
1. [Problem Statement](#problem-statement)
2. [KPI Requirements](#kpi-requirements)
3. [Charts Requirement](#charts-requirement)
4. [Data Analysis using MySQL](#data-analysis-using-mysql)
5. [Data Import](#data-import)
6. [Build Dashboard using Tableau](#build-dashboard-using-tableau)
7. [Tools, Software, and Libraries](#tools-software-and-libraries)
8. [References](#references)

---

## 📝 Problem Statement
The objective of this project is to analyze pizza sales data to understand revenue, order patterns, and sales performance. The insights will help optimize inventory, pricing strategies, and marketing efforts.

---

## 📊 KPI Requirements
- **Total Revenue**: The total sales generated.
- **Average Order Value**: Total revenue divided by the total number of orders.
- **Total Pizzas Sold**: The total quantity of pizzas sold.
- **Total Orders**: The number of unique orders placed.
- **Average Pizzas Per Order**: The average number of pizzas per order.

---

## 📈 Charts Requirement
1. **Hourly Trend for Total Pizzas Sold**: Stacked bar chart.
2. **Weekly Trend for Total Orders**: Line chart.
3. **Percentage of Sales by Pizza Category**: Pie chart.
4. **Percentage of Sales by Pizza Size**: Pie chart.
5. **Total Pizzas Sold by Pizza Category**: Funnel chart.
6. **Top 5 Best Sellers**: Based on revenue, total quantity, and total orders.
7. **Bottom 5 Best Sellers**: Based on revenue, total quantity, and total orders.

---

## 🛠 Data Analysis using MySQL
SQL queries are used to:
- Calculate **Total Revenue**:
   ```sql
   SELECT SUM(total_price) AS total_revenue FROM pizza_sale;
   ```
- Calculate **Average Order Value**:
   ```sql
   SELECT SUM(total_price) / COUNT(DISTINCT(order_id)) AS avg_order_value FROM pizza_sale;
   ```
- Calculate **Total Pizzas Sold**:
   ```sql
   SELECT SUM(quantity) AS total_pizza_sold FROM pizza_sale;
   ```
- Calculate **Total Orders**:
   ```sql
   SELECT COUNT(DISTINCT(order_id)) AS total_orders FROM pizza_sale;
   ```
- Calculate **Average Pizzas Per Order**:
   ```sql
   SELECT ROUND(SUM(quantity) / COUNT(DISTINCT order_id), 2) AS avg_pizza_per_order FROM pizza_sale;
   ```
- Analyze **Hourly Trend for Total Pizzas Sold**:
   ```sql
   SELECT HOUR(order_time) AS order_hours, SUM(quantity) AS total_pizza_sold
   FROM pizza_sale GROUP BY HOUR(order_time) ORDER BY HOUR(order_time);
   ```
- Analyze **Weekly Trend for Orders**:
   ```sql
   SELECT WEEK(order_date, 3) AS WeekNumber, YEAR(order_date) AS Year,
         COUNT(DISTINCT order_id) AS Total_orders
   FROM pizza_sale
   GROUP BY WEEK(order_date, 3), YEAR(order_date)
   ORDER BY Year, WeekNumber;
   ```
- Calculate **Percentage of Sales by Pizza Category**:
   ```sql
   SELECT pizza_category,
   ROUND(SUM(total_price),2) AS total_revenue,
   ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sale),2) AS PCT
   FROM pizza_sale 
   GROUP BY pizza_category;
   ```
- Calculate **Percentage of Sales by Pizza Size**:
   ```sql
   SELECT pizza_size, 
   ROUND(SUM(total_price),2) AS total_revenue,
   ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sale),2) AS PCT
   FROM pizza_sale
   GROUP BY pizza_size;
   ```
- Analyze **Total Pizzas Sold by Pizza Category**:
   ```sql
   SELECT pizza_category,
   SUM(quantity) AS  Total_Quantity_Sold
   FROM pizza_sale GROUP BY pizza_category ORDER BY Total_Quantity_Sold DESC;
   ```
- Identify **Top 5 Pizzas by Revenue**:
   ```sql
   SELECT pizza_name, ROUND(SUM(total_price),2) AS Total_revenue 
   FROM pizza_sale GROUP BY pizza_name ORDER BY Total_revenue DESC LIMIT 5;
   ```
- Identify **Bottom 5 Pizzas by Revenue**:
   ```sql
   SELECT pizza_name, ROUND(SUM(total_price),2) AS Total_revenue 
   FROM pizza_sale GROUP BY pizza_name ORDER BY Total_revenue ASC LIMIT 5;
   ```
- Identify **Top 5 Pizzas by Quantity**:
   ```sql
   SELECT pizza_name, SUM(quantity) AS Total_pizza_sold 
   FROM pizza_sale GROUP BY pizza_name ORDER BY total_pizza_sold DESC LIMIT 5;
   ```
- Identify **Top 5 Pizzas by Total Orders**:
   ```sql
   SELECT pizza_name, COUNT(DISTINCT(order_id)) As Total_order
   FROM pizza_sale GROUP BY pizza_name ORDER BY Total_order DESC LIMIT 5;
   ```
- Identify **Bottom 5 Pizzas by Total Orders**:
   ```sql
   SELECT pizza_name, COUNT(DISTINCT(order_id)) As Total_order
   FROM pizza_sale GROUP BY pizza_name ORDER BY Total_order ASC LIMIT 5;
   ```

---

## 📥 Data Import
- Load the pizza sales dataset into MySQL.
- Use SQL queries to preprocess data before visualization.

---

## 📊 Build Dashboard using Tableau
A comprehensive dashboard is created in **Tableau**, featuring:
- KPI summaries.
- Interactive charts and visualizations.
- Sales trend analysis.
- Example dashboard
- Home page
![image alt](https://github.com/BandhanHardiya/Pizza_sale_analysis/blob/main/pizza_dashboard.png?raw=true)

- Best/worst seller page
![image alt](https://github.com/BandhanHardiya/Pizza_sale_analysis/blob/main/pizza_dashboard2.png?raw=true)

- This is link of my Tableau Public Dashboard
- Dashboard: [Tableau Public](https://public.tableau.com/views/Book1_17402919623000/Dashboard1?:language=en-GB&:sid=&:display_count=n&:origin=viz_share_link)
---

## 🛠 Tools, Software, and Libraries
- **SQL (MySQL)**: Data extraction and transformation.
- **Tableau**: Data visualization and dashboard building.
- **Excel/CSV**: Data storage and preprocessing.
- **GitHub**: Version control and project sharing.

---

## 📚 References
- SQL Documentation: [MySQL](https://dev.mysql.com/doc/)
- Tableau Tutorials: [Tableau](https://www.tableau.com/learn)
- GitHub Guide: [GitHub Docs](https://docs.github.com/)

---

## 📌 How to Use
1. Clone this repository:
   ```sh
   git clone https://github.com/yourusername/pizza_sales_analysis.git
   ```
2. Import the dataset into MySQL.
3. Run the SQL queries provided.
4. Load the processed data into Tableau.
5. Explore the interactive dashboard.

Feel free to contribute, suggest improvements, or report issues! 🚀
