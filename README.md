# Pizza_sales_SQL-EXCEL
You can Compare Values with Excel Using these SQL Queries
### A. KPI’s
1. Total Revenue:
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```
 ![image](https://github.com/user-attachments/assets/666ec943-675f-4f1c-a554-af2004a836d5)
2. Average Order Value
```sql
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales
 ```
![image](https://github.com/user-attachments/assets/ca18cad1-6a8b-43cd-8e94-0c94b6766217)
3. Total Pizzas Sold
```sql
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
 ```
![image](https://github.com/user-attachments/assets/bf7bc226-79e0-4273-bbe1-dfbb0f222a32)

5. Total Orders
```sql
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
 ```
![image](https://github.com/user-attachments/assets/fcef50cd-a5a3-404e-94ce-a72888edaf12)

6. Average Pizzas Per Order
```sql
SELECT SUM(quantity)/COUNT(DISTINCT order_id) AS Avg_pizza_per_order FROM pizza_sales;
```
![image](https://github.com/user-attachments/assets/e2802401-fae3-469e-8992-71804fb373d2)

### B. Daily Trend for Total Orders
```sql
SELECT 
    DAYNAME(STR_TO_DATE(order_date, '%d-%m-%Y')) AS order_day,
    COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
GROUP BY DAYNAME(STR_TO_DATE(order_date, '%d-%m-%Y'));
```
Output:

![image](https://github.com/user-attachments/assets/e757788c-50eb-4e2e-adc6-930e2caded73)

### C. Hourly Trend for Orders
```sql
SELECT HOUR(order_time) AS order_hours,COUNT(DISTINCT order_id) AS Total_orders
from pizza_sales
group by HOUR(order_time)
order by HOUR(order_time);
```
Output

![image](https://github.com/user-attachments/assets/57deec5e-9aec-4356-a570-a299b8a4d507)

### D. % of Sales by Pizza Category
```sql
SELECT pizza_category,SUM(total_price) AS Total_Sales,sum(total_price)*100/(select sum(total_price ) from pizza_sales) as PCT
from pizza_sales 
group by pizza_category;
```
Output

![image](https://github.com/user-attachments/assets/bc37a87c-3639-440c-9d03-00935d48760a)

 
### E. % of Sales by Pizza Size
```sql
SELECT pizza_category,SUM(total_price) AS Total_Sales,sum(total_price)*100/(select sum(total_price ) from pizza_sales) as PCT
from pizza_sales 
group by pizza_category;
```
Output

![image](https://github.com/user-attachments/assets/1a3cd694-c1b6-4adb-8233-ffaa5d06661a)


### F. Total Pizzas Sold by Pizza Category
```sql
SELECT pizza_category,SUM(quantity) as Total_pizzas_sold 
from pizza_sales 
group by pizza_category;
```
Output

![image](https://github.com/user-attachments/assets/18177c5d-43e8-4f8e-a56f-a11c87a7b056)

### G. Top 5 Best Sellers by Total Pizzas Sold
```sql
select pizza_name,SUM(quantity) as Total_pizzas_sold 
from pizza_sales 
group by pizza_name
order by Total_pizzas_sold desc 
limit 5;
```
Output
 
![image](https://github.com/user-attachments/assets/2d6b449a-7450-4e71-bcfc-75184cb7aba3)



### H. Bottom 5 Best Sellers by Total Pizzas Sold
```sql
select pizza_name,SUM(quantity) as Total_pizzas_sold 
from pizza_sales 
group by pizza_name
order by Total_pizzas_sold 
limit 5;
```
Output

![image](https://github.com/user-attachments/assets/b35dc58b-1d62-4079-8dec-32bbfcc7da1f)
