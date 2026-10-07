# Analyzing & Formatting PostgreSQL Sales Data (SQL)

**Background:** A superstore is interested in retrieving insights pertaining to day-to-day retail business questions such as what are the top performing products & the top categories based on profit margins, & how missing data can be imputed for quantity of products per order. To do so, the provided dataset will need to be cleaned & reformatted using SQL skills & concepts.  
Four data tables were provided: `orders`, `returned_orders`, `people`, & `products`.

There were two primary objectives in this project.
- Find the top five products from each category based on highest total sales.
- Calculate the quantity for orders with missing values in the `quantity` column by determining the unit price for each `product_id` using available order data, considering relevant pricing factors such as discount, market, or region. Then, use this unit price to estimate the missing quantity values.

The project was done in September, 2025. Note that the accompanying dataset was unable to be retrieved from the platform in which the project originated.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Brief Summary
This project utilized arithmetic & SQL tools to evaluate the most popular products sold & identify & impute orders with missing data points. More specifically, common table expressions (CTEs), window functions, type casting, joins, & subqueries were utilized to manipulate the provided data. The two sections of analyses primarily dealt with the `orders` table, but the `products` table was also utilized. The former contained 51,290 data points.

The first section examined the top-selling products across each of the three categories according to total sales. By manipulating data types & utilizing a subquery, window function, & left join, these items were obtained & sorted according to their category & total sales.  
Generally, technology items yielded the most in terms of sales & profits, whereas office-supplies items generated the least.
- Of the fifteen items obtained in this exercise, the item that generated the most in terms of sales was the "Apple Smart Phone, Full Size" (~ 86,935); however, these orders only generated the ninth most profits (~ 5,921).
- The item that generated the most in terms of profits was the "Canon imageCLASS 2200 Advanced Copier" (~ 25,199); however, these orders only generated the fifth most sales (~ 61,599).


Lastly, there were five data points in the `orders` table that possessed missing quantity values. To impute them, some particular arithmetic & SQL tools were utilized.  
Firstly, in order to obtain the quantity of items bought in an order, the unit price of an item needed to be obtained. Given that this variable was not present in the provided data, it needed to be built. To obtain the unit price, the following formula was used: (sales / (1-discount)) / (quantity); however, for orders with a missing quantity, this would yield a missing unit price too. As such, a unit-price imputation value needed to be obtained.

To build these imputation values, other variables were considered. More specifically, of the five data points with a missing quantity, each corresponded to a unique product id. Each of these product id's accounted for between 5-10 orders. The non-missing sales, discount, & quantity values for each of these five product id's were used to calculate an associated unit price for each order. This data was assembled into a CTE. Next, a window function was used in second CTE to obtain the average unit price for each product id using these new unit prices. These averages then acted as the basis for the imputed quantity values, the calculations of which used the following formula: ( (sales / (1-discount)) / (imp_unit_price) ).
