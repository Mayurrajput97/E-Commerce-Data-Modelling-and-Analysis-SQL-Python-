# E-Commerce-Data-Modelling-and-Analysis-SQL-Python-
Hey this is my First MySQL Project on E-Commerce Data Modelling and Analysis (SQL + Python) 
import pandas as pd
import mysql.connector
from sqlalchemy import create_engine


order_df = pd.read_csv("orders.csv").sample(1000)

aisles_df = pd.read_csv("aisles.csv")

departments_df = pd.read_csv("departments.csv")

order_products_df = pd.read_csv("order_products.csv").sample(1000)

products_df = pd.read_csv("products.csv")

aisles_df.head()
departments_df.head()
order_products_df.head()
products_df.head()
order_df.head()

connection = mysql.connector.connect(
    user='root',
    password='Dvenster@7875',
    host='127.0.0.1',
    database='ecommerce_db'
)

cursor = connection.cursor()

engine = create_engine('mysql+mysqlconnector://root:Dvenster@7875@127.0.0.1/ecommerce_db')

order_schema = "CREATE TABLE IF NOT EXISTS `order` (order_id INT, user_id INT, order_number INT, order_dow INT, order_hour_of_day INT, days_since_prior_order INT);"
aisles_schema = "CREATE TABLE IF NOT EXISTS `aisles` (aisle_id INT, aisle TEXT);"
departments_schema = "CREATE TABLE IF NOT EXISTS `departments` (department_id INT, department TEXT);"
order_products_schema = "CREATE TABLE IF NOT EXISTS `order_products` (order_id INT, product_id INT, add_to_cart_order INT, reordered INT);"
products_schema = "CREATE TABLE IF NOT EXISTS `products` (product_id INT, product_name TEXT, aisle_id INT, department_id INT);"

cursor.execute(order_schema)
cursor.execute(aisles_schema)
cursor.execute(departments_schema)
cursor.execute(order_products_schema)
cursor.execute(products_schema)

connection.commit()

engine = create_engine('mysql+mysqlconnector://root:Mayur@127.0.0.1/ecommerce_db')

aisles_df.to_sql('aisles', con=engine, if_exists='append', index=False)


