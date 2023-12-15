# Adventure-Wors---Power-BI https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms
Microsoft introduced the Adventure Works in 2005 as a fictional multinational bicycle manufacturing company. The company has its worldwide distribution channel. The data set has 7 schemas, which includes Sales, Production, Purchasing, Human Resource and Person. 
Adventure Works.
Introduction
Microsoft introduced the Adventure Works in 2005 as a fictional multinational bicycle manufacturing company. The company has its worldwide distribution channel. The data set has 7 schemas, which includes Sales, Production, Purchasing, Human Resource and Person. 
In order to visualize the data, set the “AdventureWorks2019.bak” data set is downloaded from the Microsoft site. Thereafter, “SQL Server 2022 Configuration Manager” was used to manage the network connectivity and configure it to the SQL server. As the second step by using “Microsoft SQL Server Management Studio 18” connected to the SQL server. Thereafter under the object explorer restored the Adventure works data set to the SQL server.
 
Figure 1 Connection to SQL Server

To do the data cleaning, modeling, and visualization the data set was imported to Power BI. To load the data SQL Server option was selected and server address was given and imported. 

 
Figure 2 Power BI Loading Data through SQL
After the successful loading to Power BI, the data set is visible under the navigator. In this window, all the tables under each schema are visible. 
2.1 Introduction of new schema
Prior to selecting the additional schema, the Production, Person, and Sales were already loaded along with other related tables. 
For the analysis it was important to identify the relationship and how it influences human resource schema with the other three schemas. Therefore, the relevant schema was loaded along with the following tables. 
1.	Human Resources Employee
a.	This consists of the general information of employee details and remaining sick and vacation leave and other information.
2.	Human Resources Department
a.	The data that is available is only the department names and information.
3.	Human Resources Department History
a.	This includes start date of employees
4.	Human Resources Shift
a.	There were three shift types under the data set.
Apart from the above-mentioned schema additional new tables were introduced to analyze what employees are working and which department and some other information about each employee. In this data set, apart from the sales, production, and person a new scheme the Human Resource is introduced.
1.	Sales Territory (This data was introduced to identify the location sales take place.)
2.	Sales Customer (This was used to identify the customer purchase location in relation to the territory.)
3.	Sales Order Header (The data in this sheet included all general information order date to total due amount.)
4.	Sales Order detail (The data included all the information from cost to profit of products and order quantity.)
5.	Production Subcategory (Included all relevant information of product subcategory information.)
6.	Product Inventory. (This had the quantity that is relevant for the analysis. )
7.	Production Product (This data included product subcategory information.)
8.	Person (This was including all personal information name to person type.)
Apart from the above-mentioned tables and the schemas. A new table was created that included the date information. 
2.2 Data cleaning and preprocessing
The new data table “Date” needed a time series data that commenced from 2000.1.1 to 2025.12.31 (Appendix 2.2.a).  With the new column in place, needed the breakdown of the respective date to month, year, quarter, and month number (Appendix 2.2.b).
 
Figure 3 New Table with DAX for Dates
Under the Human Resource employee table there were columns of vacation and sick leave in hours as a total column wise. Therefore, needed to create new columns for each by days and total count (Appendix 2.2.c). After creating the new columns, Marital Status column had values as ‘m’ and ‘s’. Therefore, created a new column with appropriate values married or single (Appendix 2.2.d). Finally in the data sheet changing the gender from ‘m’ and ‘f’ to male or female for better understanding and visualizing the data set (Appendix 2.2.f). 
In the person data table, created a new column with full name of the person and concatenate the first and last name as one name. In addition, including a new column on email promotion and naming values (0,1,2) and converting each value and naming each value based on the corresponding number (Appendix 2.2.h). 
Values	Corresponding Text
0	Declined Email Promos
1	Accepted Email Promos
2	Accepted Selected Email Promos

2.3 Data Modeling
Based on the schemas and the tables the following data model is created. As per the below figure, the mentioned tables are modeled and created cardinality across the tables to visualize and generate insights. Thereafter created a new column and breaking each age group into 5 groups for further analysis (Appendix 2.2.e).
 
Figure 4 Adventure Works Model
As per the above figure there 4 fact tables Human resource employee, person, sales order header and product. The relationship among each supporting table is created in the below table along with the cardinality. 
 
Fact Table 1	Fact Table 2	Table 1	Table 2	Relationship	Cardinality
Human resource employee		Human resource employee history		Business entity ID	One to many
		Human resource employee history	Human Resource Department	Department ID	One to Many
		Human resource employee history	Human Resource Shift	Shift ID	One to Many
Person	Human resource employee			Business Entity ID	One to One
Person		Sales Customer		Business Entity ID	One to Many
		Sales Customer	Sales Territory	Territory ID	One to Many
Sales Order Header		Sales Customer		Customer ID	One to Many
Sales Order Header		Sales Order Detail		Sales order ID	One to Many
Production Product		Sales order detail		Product ID	One to Many
Production Product		Product Inventory		Product ID	One to Many

2.4 DAX Queries
In the Human Resource employee department history table created a measurement for average worked years and count of employees (Appendix 2.2.g). The sales customer table a measurement created to identify the customer count. On the sales order detail calculating the average profit and total profit (Appendix 2.2.i). In terms of new columns, including standard cost, revenue, profit, and cost (Appendix 2.2.j).
2.4 Visualization 
To visualize the model and the new calculations, the objective was to create an overview on product which included details of products, product quantity and product colors. The Product overview page included the decomposition tree analyzed the profit by product and sub product and the color by profit. This was able to visualize each product type and the profit. 
 
Figure 5 Decomposition tree
Under the product details a bar chart that included values of profit & standard cost against years and y axis average profit. This visualization help understand the year-on-year profit and standard cost again average profit. 
 
Figure 6 Line and Clustered Column chart
Under product quantity section a funnel chart that included top ten products and the order quantity to visualize what products were sold on specific timelines. 
 
Figure 7 Funnel Chart
Under the same section a bar chart representing all the months and the values are order quantity by month with the y axis visualized the average profit. This was able to showcase the month-on-month product order details and the profit. 
 
Figure 8 Line and clustered column chart
In the last section included information on the color of the products and the product quantity. To visualize the same on a scatter, plot the x axis represents the standard cost and the y axis represents the revenue, and the legend was the product type and finally the size visualized the profit. Through this visualization from an overall view, it is easy understand in comparison to revenue and standard cost which products are profitable. 
The same section included a donut pie chart that represents the order quantity by product color. The below chart represents the number of orders based on the color of the product. 


Figure 9 Donut Chart
Finally, under the product color section a world cloud is visually shown to highlight the product order quantity. The font size on the visual shows the large number of product type and the smallest font size shows the lowest ordered quantity for product. 
In the second page included two main parts amounts and email promotions. Under the first section of the regional sales the amounts section visualized the standard cost, sales orders, revenue, profit, and customers. All these values are visually represented on cards. 
Figure 10 Word Cloud
 
Figure 11 Cards
As the second section, the email promotions are important to determine if the type of email promo that the customer has subscribed makes an impact on the overall numbers. The email acceptance levels are broken down into three sections. 
1.	Declined Email promotions
2.	Accepted Email promotions
3.	Accepted selected email promotions
A donut chart is visualized with values by customer count and legend with the three types of acceptance level. 
 
Figure 12 Donut Chart
A slicer is included to with region names for easy user navigation.
 
Figure 13 Slicer
A stacked chart is visualized by region and revenue by email promotion. This helps identify the revenue that is generated by country against the type of email promotion that is accepted by the customers. 
 
Figure 14 100 Stacked Chart
The world map represents the regions and the order quantity to visualize the best regions that is performing in terms of market volume. 
 
Figure 15 Map Visualization
In the third and final page includes information on human resource by department and leave and employee information. As the first section of the dashboard, the donut chart visualizes the total number of employees by gender. 
Figure 16 Donut Chart sex
The second chart a funnel chart shows the marital status of the employee count if they are married or not. This visualization helps to understand the total number of married and unmarried employees against the type of department. 
Figure 17 Funnel Chart Marital Status
The third visual which is a tree map represents the number of employees working in each department. 
 
Figure 18 Tree map of departments
Clustered column chart is created to visualize the shift count of total number of employees. There are three shifts from day, evening, and night. This visual represents the total number of employees for the shifts. 

Figure 19 Clustered column chart Shift Type
In the second section leave information includes several visualizations. The first is a clustered bar chart with the three age brackets and to visualize which age group has the highest number of sick leaves and vacation days. This will help generate insights on types of leave a particular age group is more prone to take. 


Figure 20 Clustered bar chart Age Group
Following the clustered bar chart cards are included to visually represent the total number of leave and total of vacation leave and sick leave days along with the total employee count.
 
Figure 21 Leave Days
To further drill down to employee information a table is created with ID number and Full name of the employee and a search bar to search by employee name. 
 
Figure 22 Table and Search
Finally, the employee information section consists of the designation of the employee, organization level, employed years, marital status, shift and gender of a particular individual in the organization. 
2.5 Publishing
To publish the report, after compiling all the information simply applied the publishing option on the power bi services.  That published to My Workplace location. Thereafter, logging into power bi and created a personal gateway and refreshed the data. Below snapshot represents the successful completion of the data refresh.  
Figure 23 Successful data refresh screen shot

2.6 Raw Level Securities
To assign security levels, under the modeling tab the manage roles allows options based on the security level that is desired. Therefore, taking into consideration the roles by region. New regions are created by region and sales territory. For instance, if the sales territory is Australia, under the Sales Territory the name would be assigned to “Australia”. Similarly, all the remaining regions are assigned accordingly. 
In addition, creating additional roles under all departments. This will be able to generate insights better visually by department type. 
