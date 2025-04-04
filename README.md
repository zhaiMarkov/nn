# Frappuccino - PostgreSQL Migration 🍵📊🖥️

Done by dabektur and basagitz

## Overview 📌📝🔍
This project entails the systematic migration of the Frappuccino API to a PostgreSQL-based architecture. The API framework facilitates the seamless orchestration of order management, inventory control, menu structuring, and comprehensive analytics for a coffee shop enterprise.

## Prerequisites 🔧📦🖥️
- Docker & Docker Compose
- PostgreSQL
- Go (for development)

## Setup 🏗️🖥️🚀
1. Clone the repository:
```sh
   git clone <git@git.platform.alem.school:basagitz/frappuccino.git>
   cd frappuccino
```
2. Ensure `init.sql` resides in the root directory, encompassing requisite table schemas and seed data.
3. Deploy the application via Docker:
```sh
   docker-compose up --build
```
4. The API will be accessible at `http://localhost:8080` or use Postman(prefered way)'
5. Additionally, if you want to check database use `http://localhost:5050`

## Database Connection 🔑🗄️🔗
Configure PostgreSQL credentials as follows:
- **Host:** `db`
- **Port:** `5432`
- **User:** `latte`
- **Password:** `latte`
- **Database:** `frappuccino`

## API Endpoints 🌐🔀📡
### Orders 🛒📦💳
- **`POST /orders`** - Create a new order
```json
  {
    "customer_name": "John Do",
    "customer_info": {
        "phone_number": "123-456-789",
        "preferences": {
            "likes": ["latte", "muffin"]
        }
    },
    "items": [
      {
        "product_id": "Latte",
        "quantity": 2,
        "customization": {
          "sugar": "without"
        }
      },
      {
        "product_id": "Croissant",
        "quantity": 1,
        "customization": {}
      }
    ],
    "payment_method": "cash",
    "special_instructions": {
        "pickup_time": "12:30"
    }
  }
```
- **`GET /orders`** - Retrieve all orders
- **`GET /orders/{id}`** - Fetch an order by its unique identifier
- **`PUT /orders/{id}`** - Modify an existing order
- **`DELETE /orders/{id}`** - Remove an order record
- **`POST /orders/{id}/close`** - Finalize and close an order

### Menu Items 🍽️📜🛠️
- **`POST /menu`** - Insert a new menu item
```json
  {
      "product_id": "Natte", 
      "description": "A creamy coffee drink",
      "category": "beverage",
      "tags": [
          "hot",
          "coffee"
      ],
      "price": 3.5,
      "metadata": {
              "size": [
                  "small",
                  "medium",
                  "large"
              ]
          },
      "ingredients": [
          {
              "ingredient_id": "Milk",
              "quantity": 0.2
          },
          {
              "ingredient_id": "Espresso_Beans",
              "quantity": 0.05
          }
      ]
  }
```
- **`GET /menu`** - Retrieve all menu items
- **`GET /menu/{id}`** - Fetch a menu item by ID
- **`PUT /menu/{id}`** - Update an existing menu item
- **`DELETE /menu/{id}`** - Remove a menu entry

### Inventory 📦📊🔄
- **`POST /inventory`** - Add a new inventory item
```json
  {
      "ingredient_id": "anything",
      "quantity": 100,
      "unit": "ml",
      "retails_price": 0.01
  }
```
- **`GET /inventory`** - Retrieve all inventory records
- **`GET /inventory/{id}`** - Fetch inventory details by ID
- **`PUT /inventory/{id}`** - Update inventory data
- **`DELETE /inventory/{id}`** - Remove an inventory record

### Reports & Analytics 📊📈🧐
- **`GET /reports/total-sales`** - Compute total revenue metrics
- **`GET /reports/popular-items`** - Identify high-demand menu items
- **`GET /orders/numberOfOrderedItems?startDate={startDate}&endDate={endDate}`** - Get all of ordered items by period
```
GET /numberOfOrderedItems?startDate=10.11.2024&endDate=11.11.2024
HTTP/1.1 200 OK
Content-Type: application/json
```
- **`GET /reports/search?q={query}`** - Execute full-text search across orders, menu, and customer datasets
```
GET /reports/search?q=Latte&filter=menu,orders&minPrice=0
HTTP/1.1 200 OK
Content-Type: application/json
```
- **`GET /reports/orderedItemsByPeriod?period={day|month}&month={month}`** - Retrieve statistical insights into ordered items over specific time frames
```
GET /orderedItemsByPeriod?period=day&month=october
HTTP/1.1 200 OK
Content-Type: application/json

GET /orderedItemsByPeriod?period=month&year=2023
HTTP/1.1 200 OK
Content-Type: application/json
```
- **`GET /inventory/getLeftOvers?sortBy={value}&page={page}&pageSize={pageSize}`** - Query remaining inventory stock with sorting and pagination functionality
```
GET /getLeftOvers?sortBy=quantity&page=1&pageSize=4
HTTP/1.1 200 OK
Content-Type: application/json
```
- **`POST /orders/batch-process`** - Process multiple orders concurrently
```json
  {"orders":[
    {
  "customer_name": "John Do",
  "customer_info": {
      "phone_number": "123-456-789",
      "preferences": 
              {
              "likes": ["latte", "muffin"]
              }
  },
  "items": [
    {
      "product_id": "Latte",
      "quantity": 2,
      "customization": {
      "sugar": "without"
    }
    },
    {
      "product_id": "Croissant",
      "quantity": 1,
      "customization": {}
    }
  ],
  "payment_method": "cash",
  "special_instructions": {
      "pickup_time": "12:30"
  }
},
{
  "customer_name": "John Dicker",
  "customer_info": {
      "phone_number": "123-456-789",
      "preferences": 
              {
              "likes": ["latte", "muffin"]
              }
  },
  "items": [
    {
      "product_id": "Latte",
      "quantity": 2,
      "customization": {
      "sugar": "without"
    }
    },
    {
      "product_id": "Croissant",
      "quantity": 1,
      "customization": {}
    }
  ],
  "payment_method": "cash",
  "special_instructions": {
      "pickup_time": "12:30"
  }
}
    ]
    }
```

## Features 🚀💡🔧
- Robust and scalable order processing mechanism.
- Real-time inventory monitoring and stock adjustment.
- Dynamic menu customization with precise ingredient tracking.
- Advanced analytics and sales forecasting capabilities.
- API-first architecture enabling seamless third-party integrations.

## Development Guidelines 📜🔍🛠️
- Adherence to `gofumpt` for consistent code formatting.
- Exclusive utilization of built-in Go libraries alongside PostgreSQL drivers.
- Ensure the system is fully deployable via `docker compose up`.
- Implement efficient indexing, constraints, and relational mapping within PostgreSQL.

## ERD and Database Schema 🏗️📊📄
![alt text](image.png)

## Coding Standards 📏📌💻
- Maintain idiomatic Go code practices.
- Enforce uniform and descriptive naming conventions.
- Develop extensive unit test coverage for core functionalities.
- Provide clear, maintainable, and well-documented codebases.
