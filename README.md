
# Team 6 MIST 4610: Group Project 1

## Team Members
- Adriano Onate [@ado51234](https://github.com/ado51234)
- Maxwell Shank [@mshank10](https://github.com/MShank10)
- Kipras Kairys [@kipraskairys](https://github.com/KiprasKairys/62775_GroupProject1-Restaurant)
- Robert Backe  [@robertbacke](https://github.com/robertbacke)
- Kevin Behlke [@kwb95124](https://github.com/kwb95124)

## Project Description

This project models and builds a relational database for a restaurant’s daily operations. The central entity is Orders, which connects employees, tables, menu items, and payments. The OrderItems table manages the many-to-many relationship between orders/to-go orders and menu items, allowing multiple items per order. The database also tracks suppliers and ingredients to link inventory with restaurant activity. Once populated, it will support SQL queries that provide managerial insights on sales, employee performance, and inventory efficiency.


## Explanation of data model:

Our model is based on the structure of a full-service restaurant that manages reservations, employees, menu items, and inventory within a single system.

The Customers table stores basic customer information such as names and phone numbers. Each customer can make multiple Reservations, creating a one-to-many relationship between Customers and Reservations. Every reservation links to a specific Table, which stores details like table number, capacity, and style (Booth, High-top, Patio, or Normal). Since one table can host many reservations over time, Tables and Reservations also share a one-to-many relationship.

The Employees table contains details for all staff members, including their names, phone numbers, titles, and supervisors. Each employee can place multiple Orders for dine-in tables, while each table can have many orders over time—forming a many-to-many relationship between Employees and Tables, with Orders as the associative entity. Employees also have a self-referencing relationship, where one employee can supervise many others.

Each Order connects to Menu_Items through the associative entity Order_Items, which records every individual menu item included in an order. This structure allows multiple items per order and multiple orders per menu item. The Order_Items table has its own primary key (OrderItemID) and includes fields for special requests, linking orders to specific dishes while supporting detailed reporting on sales and kitchen activity.

The ToGoOrders table manages takeout transactions. Each to-go order links to one Customer, one Employee, and one Payment, and connects to Order_Items to list the menu items ordered. This mirrors the dine-in Orders structure but captures off-site activity, allowing the restaurant to analyze both dine-in and takeout performance.

The Payments table records transaction details such as amount and payment method. Each order or to-go order links to exactly one payment, creating a one-to-one relationship that supports accurate financial tracking and revenue analysis.
The Menu_Items table stores each dish’s name, calories, price, and category, while Menu_Categories defines those categories (e.g., Appetizers, Entrees, Soups) through a one-to-many relationship.

To manage kitchen operations, the Ingredients table lists all ingredients used in recipes and connects to Suppliers, forming a one-to-many relationship where each supplier provides multiple ingredients. The many-to-many relationship between Menu_Items and Ingredients is handled through Item_Ingredients, which specifies the quantity of each ingredient used in a dish.

Together, these entities form a complete operational model of the restaurant. Managers can track reservations, orders, payments, employee roles, and inventory in one place, supporting smoother coordination between the front-of-house, kitchen, and management teams—leading to better efficiency, accuracy, and decision-making.



## Datamodel

![App Screenshot](https://raw.githubusercontent.com/ado51234/MIST4610_Project1/main/SunDataModel.png)



## Data Dictionary


![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Customers.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Employees.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Ingredients.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Item_ingredients.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Menucategories.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Menuitems.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Orderitems.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Orders.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Payments.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Reservations.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Suppliers.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Tables.png?raw=1)

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Togo.png?raw=1)






















## Queries

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/matrix.png?raw=1)

### Query 1


Which tables in the restaurant have a capacity of 6 or more people? 

A manager or host needs this information to quickly identify tables for larger parties of 6 or more people to sit at.


```
SELECT tableNumber, capacity, style 
FROM Tables
WHERE capacity >= 6 
```
```
+ ---------------- + ------------- + ---------- +
| tableNumber      | capacity      | style      |
+ ---------------- + ------------- + ---------- +
| 1                | 8             | Normal     |
| 2                | 6             | Normal     |
| 3                | 6             | Normal     |
| 4                | 8             | High-top   |
| 5                | 7             | High-top   |
| 6                | 6             | Booth      |
| 7                | 6             | Patio      |
| 10               | 6             | High-top   |
| 13               | 7             | Patio      |
| 14               | 7             | High-top   |
| 15               | 7             | Patio      |
| 16               | 6             | Normal     |
| 17               | 8             | Patio      |
| 19               | 6             | Patio      |
| NULL             | NULL          | NULL       |
+ ---------------- + ------------- + ---------- +
15 rows

```

### Query 2

What are all the appetizers offered?

A manager would be interested in seeing which appetizers are currently on the menu so he can get his staff to sell them to customers.

```
SELECT name,categoryName, price, calories
FROM Menu_Items 
JOIN Menu_Categories ON Menu_Items.categoryId = Menu_Categories.categoryId
WHERE categoryName = 'Appetizer'
```

```
+ --------- + ----------------- + ---------- + ------------- +
| name      | categoryName      | price      | calories      |
+ --------- + ----------------- + ---------- + ------------- +
| Cheese Sticks | Appetizer     | 6          | 150           |
| Potato Skins | Appetizer      | 7          | 250           |
| Blooming Onion | Appetizer    | 7          | 180     
| Wings     | Appetizer         | 9          | 225           |
| Sliders   | Appetizer         | 13         | 300           |
+ --------- + ----------------- + ---------- + ------------- +
5 rows
```
### Query 3


What is the average payment amount across all customers?

A manager would like to know what the average check is at the restaurant because it would provide him good insight on if the restaurant is making enough money on average from each table.

```
SELECT AVG(amount)
FROM Payments
```

```
+ ---------------- +
| AVG(amount)      |
+ ---------------- +
| 23.4400          |
+ ---------------- +
1 rows
```

### Query 4

Which employees have more than 3 orders associated to them and what is their position?
 
This query helps managers gauge how productive their employees are, and lets them know which type of employee
is submitting the most orders. 
```
SELECT firstName,lastName,title,COUNT(orderId)
FROM Employees
JOIN Orders ON Orders.employeeId = Employees.employeeid
GROUP BY firstName,lastName,title
HAVING COUNT(orderId) >= 3
ORDER BY COUNT(orderId) DESC

+ -------------- + ------------- + ---------- + ------------------- +
| firstName      | lastName      | title      | COUNT(orderId)      |
+ -------------- + ------------- + ---------- + ------------------- +
| Chadwick       | Boseman       | Host       | 4                   |
| Bing           | Jellings      | Server     | 3                   |
| Alvis          | Pressley      | Host       | 3                   |
+ -------------- + ------------- + ---------- + ------------------- +
3 rows

```


### Query 5


What are the top ordered items?

A manager uses this to understand customer preferences. Popular items should be prioritized,
while unpopular items might be removed from the menu. 
This also helps inventory decisions when it comes to ingredients.

SELECT Menu_Items.itemId, Menu_Items.name, Menu_Categories.categoryName, COUNT(Order_Items.itemId) AS TimesOrdered
FROM Order_Items
JOIN Menu_Items ON Order_Items.itemId = Menu_Items.itemId
JOIN Menu_Categories ON Menu_Items.categoryId = Menu_Categories.categoryId
GROUP BY Menu_Items.itemId, Menu_Items.name, Menu_Categories.categoryName
ORDER BY TimesOrdered DESC
```
+ ----------- + --------- + ----------------- + ----------------- +
| itemId      | name      | categoryName      | TimesOrdered      |
+ ----------- + --------- + ----------------- + ----------------- +
| 2           | Cheeseburger | Entree         | 7                 |
| 1           | Hamburger | Entree            | 6                 |
| 7           | Clam Chowder | Soup           | 4                 |
| 10          | Chips     | Side              | 4                 |
| 12          | Water     | Drink             | 4                 |
| 8           | Seafood Boil | Entree         | 3                 |
| 3           | Nachos    | Entree            | 2                 |
| 5           | Burrito   | Entree            | 2                 |
| 4           | Cheese Sticks | Appetizer     | 2                 |
| 6           | Chicken Salad | Salad         | 2                 |
| 14          | Potato Skins | Appetizer      | 1                 |
| 9           | Fries     | Side              | 1                 |
| 13          | Soda      | Drink             | 1                 |
+ ----------- + --------- + ----------------- + ----------------- +
13 rows
```

### Query 6

What staff work under what supervisor?

The top manager uses this to see which employees are 
directly working under which other employees.
This shows hierarchy while also showing who is at the top of the chain.
```
SELECT E.firstName AS EmpFirstName, E.lastName AS EmpLastName, E.title , S.firstName AS ManagerFirstName, S.lastName
AS ManagerLastName, S.title
FROM Employees AS E
LEFT JOIN Employees AS S ON E.superVisor_ID = S.employeeId

+ ----------------- + ---------------- + ---------- + --------------------- + -------------------- + ---------- +
| EmpFirstName      | EmpLastName      | title      | ManagerFirstName      | ManagerLastName      | title      |
+ ----------------- + ---------------- + ---------- + --------------------- + -------------------- + ---------- +
| Jyoti             | Maitland         | General Manager |                       |                      |            |
| Chelsea           | Beamand          | Shift Manager | Jyoti                 | Maitland             | General Manager |
| Adrienne          | Munt             | Shift Manager | Jyoti                 | Maitland             | General Manager |
| Patrizio          | Mayall           | Kitchen Manager | Jyoti                 | Maitland             | General Manager |
| Marry             | Twitchettt       | Kitchen Manager | Jyoti                 | Maitland             | General Manager |
| Valery            | Wreath           | Cook       | Marry                 | Twitchettt           | Kitchen Manager |
| Gerard            | Cooper           | Cook       | Marry                 | Twitchettt           | Kitchen Manager |
| Myra              | Garber           | Cook       | Marry                 | Twitchettt           | Kitchen Manager |
| Leone             | Paulson          | Cook       | Patrizio              | Mayall               | Kitchen Manager |
| Grazia            | Homie            | Cook       | Patrizio              | Mayall               | Kitchen Manager |
| Therese           | Simeone          | Cook       | Patrizio              | Mayall               | Kitchen Manager |
| Bing              | Jellings         | Server     | Chelsea               | Beamand              | Shift Manager |
| Farrah            | Hane             | Server     | Chelsea               | Beamand              | Shift Manager |
| Edy               | Ross             | Server     | Chelsea               | Beamand              | Shift Manager |
| Donald            | Duck             | Server     | Chelsea               | Beamand              | Shift Manager |
| Peter             | Parker           | Server     | Chelsea               | Beamand              | Shift Manager |
| Steve             | Jobs             | Host       | Adrienne              | Munt                 | Shift Manager |
| Steve             | Rogers           | Host       | Adrienne              | Munt                 | Shift Manager |
| Chadwick          | Boseman          | Host       | Chelsea               | Beamand              | Shift Manager |
| Tony              | Stark            | Host       | Adrienne              | Munt                 | Shift Manager |
| Alvis             | Pressley         | Host       | Chelsea               | Beamand              | Shift Manager |
| Georgie           | Rose             | Busser     | Chelsea               | Beamand              | Shift Manager |
| Jose              | Gonsalez         | Busser     | Adrienne              | Munt                 | Shift Manager |
| Demetry           | Jones            | Busser     | Chelsea               | Beamand              | Shift Manager |
| Dewayne           | Waldon           | Busser     | Adrienne              | Munt                 | Shift Manager |
+ ----------------- + ---------------- + ---------- + --------------------- + -------------------- + ---------- +
25 rows

```


### Query 7


What items have never been ordered?
A manager would use this to see which items (if any) have never been ordered and should 
then be taken off the menu as it takes up inventory and a menu spot while providing no revenue.

```
SELECT itemId,name,price
FROM Menu_Items
WHERE NOT Exists (SELECT * FROM Order_Items WHERE Menu_Items.itemID = Order_Items.itemId)

+ ----------- + --------- + ---------- +
| itemId      | name      | price      |
+ ----------- + --------- + ---------- +
| 11          | Shrimp Salad | 10         |
| 15          | Blooming Onion | 7          |
| 16          | Wings     | 9          |
| 17          | Sliders   | 13         |
| 18          | Lemonade  | 2          |
| NULL        | NULL      | NULL       |
+ ----------- + --------- + ---------- +
6 rows
```


### Query 8

What ingredients go into each item and how are they supplied?

A chef or manager uses this to check stock levels for a specific dish, manage food costs by seeing all components, 
and coordinate purchasing by seeing all the suppliers involved in one dish.

Examples of Dishes are: Sliders,Shrimp Salad,Fries, Hamburger,Chicken Salad.

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/blob/main/Query%208.png?raw=1)



### Query 9

How often is each payment method used, and how much total revenue has each method seen?

A manager or owner uses this to understand cash flows and processing fees. If credit card revenue is high, 
they might renegotiate with their payment processor for lower credit card fees. 
Can also be used to compare between the different methods. It also confirms that the gift card redemptions are working.
```SELECT paymentMethod, COUNT(paymentId) AS NumberOfTransactions, SUM(amount) AS TotalRevenue
FROM Payments
GROUP BY paymentMethod
ORDER BY TotalRevenue DESC

+ ------------------ + ------------------------- + ----------------- +
| paymentMethod      | NumberOfTransactions      | TotalRevenue      |
+ ------------------ + ------------------------- + ----------------- +
| Card               | 13                        | 337               |
| Cash               | 7                         | 162               |
| Gift Card          | 5                         | 87                |
+ ------------------ + ------------------------- + ----------------- +
3 rows

```


### Query 10


What is the most expensive item in each category?

This query helps a menu engineer understand the price ceiling for each category. 
It highlights the "premium" items, which are often the most profitable.
A manager can check if these items are selling well or if their prices are turning customers away.

```
SELECT categoryName, Menu_Items.name AS ItemName, price
FROM Menu_Items 
JOIN Menu_Categories ON Menu_Items.categoryId = Menu_Categories.categoryId
WHERE (Menu_Items.categoryId, price) IN (SELECT categoryId, MAX(price) FROM Menu_Items
GROUP BY Menu_Items.categoryId)

+ ----------------- + ------------- + ---------- +
| categoryName      | ItemName      | price      |
+ ----------------- + ------------- + ---------- +
| Entree            | Seafood Boil  | 15         |
| Appetizer         | Sliders       | 13         |
| Salad             | Shrimp Salad  | 10         |
| Soup              | Clam Chowder  | 8          |
| Side              | Fries         | 6          |
| Drink             | Soda          | 4          |
+ ----------------- + ------------- + ---------- +
6 rows
```


## Database Information

Name of the Database: ns_ado51234

Each query listed above is marked in the database using stored procedures which can be called using the following format: CALL TP_Q1();
