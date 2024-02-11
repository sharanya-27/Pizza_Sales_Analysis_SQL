# Pizza Sales Analysis
__Tools used : Excel,MS SQL Server,Power BI__

[Dataset used](https://1drv.ms/x/s!AmKU00K1sOXkiXYGCmYAQfrCOGMJ?e=lz8diP)

[SQL Analysis-code](sql_analysis)

[Pizza Dashboard-Power BI](pizza_bi_dashboard.pdf.pdf)

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

       
  + Average Order Value:
    
        SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales    
    ![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/e20ff23a-8905-426e-87eb-2c4f96dc355c)

 
  + Total Pizzas Sold:
    
        SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales

    ![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/4eb1e79e-a2ab-4aad-9323-1fd33a7b2383)

 
  + Total Orders:
    
        SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales

    ![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/bc9cebcf-3b72-4bcf-8e00-2e73690efc84)

  
  + Average Pizzas Per Order:
    
        SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
        CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
        AS Avg_Pizzas_per_order
        FROM pizza_sales

    ![image](https://github.com/sharanya-27/pizza_sales_analysis/assets/142989454/bc8604a6-f70c-4c4f-8e35-62509a774473)

 






 


