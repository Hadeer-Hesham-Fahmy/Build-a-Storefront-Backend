# API Requirements

The company stakeholders want to create an online storefront to showcase their great product ideas. Users need to be able to browse an index of all products, see the specifics of a single product, and add products to an order that they can view in a cart page. You have been tasked with building the API that will support this application, and your coworker is building the frontend.

These are the notes from a meeting with the frontend developer that describe what endpoints the API needs to supply, as well as data shapes the frontend and backend have agreed meet the requirements of the application.

## API Endpoints

#### Products

- Index '/product' [GET]
- Show '/product/:id' [GET]
- Create [token required] '/product' [POST]
- [OPTIONAL] Top 5 most popular products
- [OPTIONAL] Products by category (args: product category)

#### Users

- Index [token required] '/user' [GET]
- Show [token required] '/user/:id' [GET]
- Create N[token required] '/user' [POST]

#### Orders

- Current Order by user (args: user id)[token required] '/order/:id/product' [POST]
- [OPTIONAL] Completed Orders by user (args: user id)[token required] '/order' [GET]

## Data Shapes

#### Product

- id 
- name
- price
- [OPTIONAL] category

TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    price INTEGER NOT NULL,
    category VARCHAR(50) NOT NULL )

#### User

- id
- firstName
- lastName
- password

TABLE users (
    id SERIAL PRIMARY KEY,
    first_Name VARCHAR(50) NOT NULL,
    last_Name VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL )

#### Orders

- id
- id of each product in the order
- quantity of each product in the order
- user_id
- status of order (active or complete)

TABLE orders (
    id SERIAL PRIMARY KEY,
    status VARCHAR(50) NOT NULL,
    user_id INTEGER REFERENCES users(id) NOT NULL [forign key])

    #### Order_Products
    TABLE order_products (
    id SERIAL PRIMARY KEY,
    quantity INTEGER NOT NULL,
    product_id INTEGER REFERENCES products(id) NOT NULL,[forign key ]
    order_id INTEGER REFERENCES orders(id) NOT NULL [forign key] )
