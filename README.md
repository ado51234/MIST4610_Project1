
# Repo for MIST4610 group project on restaurants.
# Team 6 MIST 4610: Group Project 1

## Team Members
- Adriano Onate [@ado51234](https://github.com/ado51234)
- Maxwell
- Kip
- Robert
- 

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


## Data Model

![App Screenshot](https://github.com/ado51234/MIST4610_Project1/raw/main/FinalModel.png)


