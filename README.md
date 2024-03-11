<div align="center"> <h1>PIZZA SALES ANALYSIS</h1>
</div>

<div align="center">
    
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/9ac41c33-bd49-4c78-8124-4fc5b3c091ec)

</div>     


----

__Tools used : Excel,MS SQL Server,Power BI__

[Dataset used](https://1drv.ms/x/s!AmKU00K1sOXkiXYGCmYAQfrCOGMJ?e=lz8diP)

[SQL Analysis-code](sql_analysis)

[Power BI Dashboard- click to view](https://github.com/sharanya-27/Pizza_Sales_Analysis_SQL/files/14561723/Pizza_Sales_BI_Dashboard.pdf)

[Power BI Dashboard- click to interact](https://app.powerbi.com/view?r=eyJrIjoiMWQzOWNmNDItNzZhYS00MDMxLWI5ZDYtM2FmOWUwMzk3ZWIxIiwidCI6IjZmMTFlMWQzLTEyMTAtNDk5YS1iMjY0LTU2NzA0NTY4OGUyNyJ9)


__Business Problem__
-------
A pizza company needs a robust and scalable data analytics solution to handle the vast amount of data(approximately 50k rows of data combined) to effectively analyze and extract meaningful insights like trends, order patterns, menu performance, customer preferences and other key business metrics. Visualizations must also be created to identify trends and insights related to daily and monthly order volume, sales by pizza type and size, and top/bottom sellers. The end goal is to equip the business with data-driven insights that inform strategic decisions to improve operations and profitability.

__Solution Plan__
-------
  + In helping the pizza company gain valuable insights from their sales data CSV file, I will utilize SQL and data visualization with Power BI to extract relevant information and conduct insightful analyses.
    Data cleaning/processing, data transformation and analysis shall be done.
  + By leveraging SQL's functions, I can uncover key metrics like total revenue, average order size, and best/worst selling menu items.
  + Once the data has been extracted and prepared, I will leverage Power BI to present the findings through interactive visualizations. This will allow stakeholders at the pizza company to gain actionable 
    insights 
    into sales trends, order patterns, and menu performance through visually compelling charts, graphs, and reports.
  + I plan on creating a dynamic Power BI dashboard that enables users to explore details on daily order volume, sales by pizza type/size, or top/bottom selling items. The end goal is equipping the business with 
    data-driven insights to inform strategic decisions that improve operations and profitability.

__Execution__
---------

__Questions Answered from the Dataset__

__1) What are the Key Performance Indicators obtained from the Dataset?__

+ __Total Revenue:__
  
      SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
   
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/958d5555-d9d8-4446-8ac5-30ce775f7afe)

This metric provides a clear measure of the overall financial performance of the pizza sales. It indicates the total amount of money generated from pizza 
orders over a specific period, reflecting the revenue potential of the business.
      
+ __Average Order Value:__
    
        SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales
    
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/e20ff23a-8905-426e-87eb-2c4f96dc355c)

Average order value helps in understanding customer spending habits and the effectiveness of marketing strategies. A higher average order value indicates that 
customers are spending more per transaction, which can contribute to increased revenue and profitability.

+ __Total Pizzas Sold:__
    
        SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
     
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/4eb1e79e-a2ab-4aad-9323-1fd33a7b2383)
    
Total pizzas sold is a fundamental metric that directly reflects product demand. It provides insights into consumption patterns and helps in inventory management and production planning. Understanding total pizzas sold enables businesses to meet customer demand efficiently.
    
+ __Total Orders:__
    
        SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
     
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/bc9cebcf-3b72-4bcf-8e00-2e73690efc84)

Total orders represent the volume of transactions processed within a specific period. Tracking total orders helps in evaluating sales performance and 
identifying trends in customer behavior. It provides a basis for assessing business growth and operational efficiency.

+ __Average Pizzas Per Order:__
    
        SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
        CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
        AS Avg_Pizzas_per_order
        FROM pizza_sales
        
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/bc8604a6-f70c-4c4f-8e35-62509a774473)

Average pizzas per order indicates the average quantity of pizzas purchased in each transaction. This metric offers insights into customer preferences and 
ordering behavior. Higher average pizzas per order may indicate upselling opportunities or popular menu items.
    
__2) Daily Trend for Total Orders__

        SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
        FROM pizza_sales
        GROUP BY DATENAME(DW, order_date)
        
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/260571ce-94b2-422d-862b-bda5239ba55c)

By analyzing the daily trend of total orders over a specific time period, we can identify patterns and fluctuations in order volumes on a daily basis. This 
helps in understanding the demand patterns throughout the week or month, enabling better inventory management and resource allocation.

 __3) Monthly Trend for Orders__

        select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
        from pizza_sales
        GROUP BY DATENAME(MONTH, order_date)

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/01f1620f-1370-445a-9ccf-4205d9800a30)

The monthly trend of total orders offers insights into the overall order activity throughout the month. Identifying peak periods of high order activity can aid in resource allocation, production planning, and promotional efforts. By recognizing monthly trends, businesses can adjust their operations to capitalize on high-demand periods and optimize efficiency during slower periods.

__4) % of Sales by Pizza Category__

        SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
        CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
        FROM pizza_sales
        GROUP BY pizza_category

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/f994347f-e9e4-4b21-881a-d0259076d310)

The distribution of sales across different pizza categories helps in understanding the popularity of each category and its contribution to overall sales. This 
insight informs menu optimization strategies, marketing campaigns, and inventory management decisions to maximize revenue and customer satisfaction.

 __5) % of Sales by Pizza Size__

        SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
        CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
        FROM pizza_sales
        GROUP BY pizza_size
        ORDER BY pizza_size

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/dfbb62af-e7ba-4735-9f95-e5d120ddff96)

The chart depicting the percentage of sales attributed to different pizza sizes provides insights into customer preferences regarding pizza size. 
Understanding these preferences allows for better inventory management and menu optimization to meet customer demand effectively.

__6) Total Pizzas Sold by Pizza Category__

        SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
        FROM pizza_sales
        WHERE MONTH(order_date) = 2
        GROUP BY pizza_category
        ORDER BY Total_Quantity_Sold DESC

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/55e05420-3ed8-4d08-a1fa-e622d4200d34)

The metric showing total number of pizzas sold for each pizza category enables comparison of sales performance across different categories. This 
visualization helps in identifying popular and less popular pizza options, informing marketing strategies and menu adjustments accordingly.

__7) Top 5 Pizzas by Revenue__

        SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Revenue DESC
        
![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/69f9c56f-509c-4eaa-b938-2321ac706c2a)

The chart highlighting the top 5 best-selling pizzas based on revenue, total quantity, and total orders identifies the most popular pizza options. This 
insight aids in understanding customer preferences and allows for targeted promotions or menu enhancements to capitalize on high-demand items.

 __8) Bottom 5 Pizzas by Revenue__

        SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Revenue ASC

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/d3edfbcb-576d-4a4c-9020-467d0bfe9c92)

Conversely, the chart showcasing the bottom 5 worst-selling pizzas based on revenue, total quantity, and total orders helps identify underperforming or less 
popular pizza options. This information is valuable for making strategic decisions such as discontinuing unpopular items or adjusting pricing and marketing 
strategies to boost sales.
 
__9) Top 5 Pizzas by Quantity__

        SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Pizza_Sold DESC

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/41b9170d-9f41-4fdc-a04b-cfdf57ba1351)

Identifying the top 5 pizzas by quantity sold provides insight into the most popular pizza varieties among customers. This information helps in understanding 
customer preferences and allows for targeted marketing efforts or menu optimizations to capitalize on high-demand items.
 
__10) Bottom 5 Pizzas by Quantity__

        SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Pizza_Sold ASC

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/1f8ff33c-92e4-48a5-a270-5fdf4f0ae844)

Conversely, identifying the bottom 5 pizzas by quantity sold highlights less popular or underperforming pizza options. This insight can inform menu 
adjustments, promotional strategies, or inventory management decisions to minimize waste and maximize profitability.
  
__11) Top 5 Pizzas by Total Orders__

        SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Orders DESC

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/f34f168f-d7c1-4558-b234-da33b847f527)

Identifying the top 5 pizzas by total orders sheds light on the most frequently ordered pizza varieties. This information helps in understanding customer 
behavior and preferences, enabling businesses to tailor marketing campaigns and menu offerings to meet customer demand effectively.

 __12) Bottom 5 Pizzas by Total Orders__

        SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Orders ASC

![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/7823e838-30e7-4cbb-b0f9-115952bdb2c8)

Identifying the bottom 5 pizzas by total orders reveals less popular or niche pizza options that may require attention or adjustments. Understanding these trends allows businesses to make informed decisions regarding menu adjustments, promotional strategies, or inventory management to optimize sales and customer satisfaction.

__13) Generated various Charts and Visuals on Power BI to identify trends/patterns and gain more insights into the data.__

![image](https://github.com/sharanya-27/Pizza_Sales_Analysis_SQL/assets/142989454/03741982-c1aa-469d-9408-b61c75ea3ae3)
![image](https://github.com/sharanya-27/Pizza_Sales_Analysis_SQL/assets/142989454/17549e8d-69f6-42c8-89ed-aa589a706239)






__Conclusion__
---------

By delving into various facets of the pizza sales dataset, a comprehensive understanding of consumer behavior and market trends was attained. The analysis unveiled key insights, including the identification of peak and off-peak periods based on daily and monthly order trends. This knowledge equips businesses with the ability to optimize staffing and inventory management to meet varying demand levels effectively. Additionally, the examination of sales distribution across different pizza categories shed light on customer preferences, aiding in menu optimization and marketing strategies to enhance sales performance.

Moreover, calculating the average number of pizzas sold per order provided valuable insights into consumer behavior and consumption patterns, enabling businesses to tailor pricing strategies and portion sizes to maximize profitability and customer satisfaction. Overall, this analysis empowers the pizza establishment to make data-driven decisions, streamline operations, and enhance the overall customer experience, ensuring continued success in the competitive pizza market.
