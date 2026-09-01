# 🛒 E-Commerce REST API

A backend REST API for an e-commerce platform built with **Python, Django, Django REST Framework, and PostgreSQL**.

The system provides APIs for managing **users, categories, products, carts, cart items, orders, and order items**. It uses Django ORM to design and manage relational database models and implements backend validation, business logic, authentication, and API request/response handling.

---

## 🚀 Features

* User registration and authentication
* Product management
* Category management
* Cart management
* Add/remove products from cart
* Cart item quantity management
* Order creation and management
* Order item management
* Relational database models using Django ORM
* Request and serializer validation
* Backend business logic
* RESTful API architecture
* Authentication and permission handling
* API testing using Postman
* Object-Oriented Programming principles

---

## 🏗️ Project Architecture

The application follows a layered backend architecture:

```text
Client / Postman
       ↓
REST API Endpoints
       ↓
Django REST Framework
       ↓
Serializers & Validation
       ↓
Business Logic
       ↓
Django ORM
       ↓
PostgreSQL Database
```

---

## 🗄️ Main Entities

The application is built around the following relational entities:

```text
User
  │
  ├────────── Cart
  │             │
  │             └── CartItem ─── Product
  │
  └────────── Order
                │
                └── OrderItem ─── Product

Category
   │
   └────────── Product
```

### Core Models

#### User

Stores customer account information and authentication details.

#### Category

Represents product categories.

#### Product

Stores product information such as name, description, price, stock, and category.

#### Cart

Represents a user's shopping cart.

#### CartItem

Represents individual products and their quantities inside a cart.

#### Order

Stores customer order information and order status.

#### OrderItem

Stores the products, quantities, and prices associated with an order.

---

## 🧩 Object-Oriented Programming

The project applies core **OOP concepts** throughout the backend implementation.

### 1. Encapsulation

Models and serializers encapsulate related data and behavior.

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.PositiveIntegerField()
```

### 2. Abstraction

Django and Django REST Framework abstract complex operations such as:

* Database queries
* Serialization
* Request parsing
* Validation
* Authentication
* HTTP response handling

### 3. Inheritance

Django REST Framework allows API classes to inherit common functionality from framework classes.

```python
class ProductListCreateAPIView(
    generics.ListCreateAPIView
):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

### 4. Polymorphism

Different API views and serializers can implement framework-defined behavior while providing model-specific functionality.

---

## 🔗 Database Relationships

The project uses Django ORM to represent relational database relationships.

### User → Cart

```text
One User
   ↓
One Cart
```

### Category → Product

```text
One Category
   ↓
Many Products
```

### Cart → CartItem

```text
One Cart
   ↓
Many CartItems
```

### Product → CartItem

```text
One Product
   ↓
Many CartItems
```

### User → Order

```text
One User
   ↓
Many Orders
```

### Order → OrderItem

```text
One Order
   ↓
Many OrderItems
```

### Product → OrderItem

```text
One Product
   ↓
Many OrderItems
```

---

## 🛠️ Tech Stack

| Technology            | Purpose                       |
| --------------------- | ----------------------------- |
| Python                | Backend programming           |
| Django                | Web framework                 |
| Django REST Framework | REST API development          |
| Django ORM            | Database modeling and queries |
| PostgreSQL            | Relational database           |
| Postman               | API testing                   |
| Git & GitHub          | Version control               |

---

## 📁 Project Structure

```text
E-Commerce-REST-API/
│
├── manage.py
│
├── ecommerce/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
│
├── products/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── admin.py
│   └── migrations/
│
├── categories/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
│
├── carts/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
│
├── orders/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
│
├── users/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
│
├── requirements.txt
├── .gitignore
└── README.md
```

---

## 🔌 API Endpoints

### Users

| Method | Endpoint               | Description       |
| ------ | ---------------------- | ----------------- |
| POST   | `/api/users/register/` | Register a user   |
| POST   | `/api/users/login/`    | Authenticate user |
| GET    | `/api/users/profile/`  | Get user profile  |

### Categories

| Method | Endpoint                | Description     |
| ------ | ----------------------- | --------------- |
| GET    | `/api/categories/`      | List categories |
| POST   | `/api/categories/`      | Create category |
| GET    | `/api/categories/<id>/` | Get category    |
| PUT    | `/api/categories/<id>/` | Update category |
| DELETE | `/api/categories/<id>/` | Delete category |

### Products

| Method | Endpoint              | Description    |
| ------ | --------------------- | -------------- |
| GET    | `/api/products/`      | List products  |
| POST   | `/api/products/`      | Create product |
| GET    | `/api/products/<id>/` | Get product    |
| PUT    | `/api/products/<id>/` | Update product |
| DELETE | `/api/products/<id>/` | Delete product |

### Cart

| Method | Endpoint                | Description         |
| ------ | ----------------------- | ------------------- |
| GET    | `/api/cart/`            | View current cart   |
| POST   | `/api/cart/items/`      | Add product to cart |
| PATCH  | `/api/cart/items/<id>/` | Update quantity     |
| DELETE | `/api/cart/items/<id>/` | Remove item         |

### Orders

| Method | Endpoint            | Description         |
| ------ | ------------------- | ------------------- |
| POST   | `/api/orders/`      | Create order        |
| GET    | `/api/orders/`      | List user's orders  |
| GET    | `/api/orders/<id>/` | Get order details   |
| PATCH  | `/api/orders/<id>/` | Update order status |

> Endpoint paths may vary depending on the final project implementation.

---

## ✅ Validation & Business Logic

The API implements backend validation to prevent invalid data and maintain application consistency.

Examples include:

* Product price validation
* Stock quantity validation
* Required field validation
* Unique field validation
* Cart quantity validation
* Product availability checks
* Order validation
* User authentication
* Permission checks

Business logic is handled on the backend rather than relying only on client-side validation.

---

## 🛒 Order Flow

The basic order workflow is:

```text
User
 ↓
Browse Products
 ↓
Add Product to Cart
 ↓
Update Cart Quantity
 ↓
Checkout
 ↓
Create Order
 ↓
Create Order Items
 ↓
Update Stock
 ↓
Order Created
```

---

## 🔄 Example API Request

### Create Product

```http
POST /api/products/
Content-Type: application/json
```

Request:

```json
{
    "name": "Wireless Keyboard",
    "description": "Mechanical wireless keyboard",
    "price": "2499.00",
    "stock": 20,
    "category": 1
}
```

Response:

```json
{
    "id": 1,
    "name": "Wireless Keyboard",
    "description": "Mechanical wireless keyboard",
    "price": "2499.00",
    "stock": 20,
    "category": 1
}
```

---

## 🧪 API Testing

API endpoints were tested using **Postman**.

Testing included:

* Successful API requests
* Invalid request data
* Missing required fields
* Authentication
* Permission handling
* CRUD operations
* Cart operations
* Order creation
* HTTP status codes
* Request and response validation

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/E-Commerce-REST-API.git
```

### 2. Navigate to the Project

```bash
cd E-Commerce-REST-API
```

### 3. Create a Virtual Environment

```bash
python -m venv venv
```

### 4. Activate Virtual Environment

Windows:

```bash
venv\Scripts\activate
```

Linux / macOS:

```bash
source venv/bin/activate
```

### 5. Install Dependencies

```bash
pip install -r requirements.txt
```

### 6. Configure Database

Create a PostgreSQL database and update the database configuration in:

```text
settings.py
```

Example:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "ecommerce_db",
        "USER": "postgres",
        "PASSWORD": "your_password",
        "HOST": "localhost",
        "PORT": "5432",
    }
}
```

### 7. Run Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 8. Create Superuser

```bash
python manage.py createsuperuser
```

### 9. Start Development Server

```bash
python manage.py runserver
```

The API will be available at:

```text
http://127.0.0.1:8000/
```

---

## 🔐 Security

The backend follows common API security practices including:

* Authentication
* Permission-based access
* Server-side validation
* Protected endpoints
* Django security features
* Environment-based configuration for sensitive settings

---

## 📚 Key Concepts Demonstrated

This project demonstrates practical knowledge of:

* Python
* Object-Oriented Programming
* Django
* Django REST Framework
* REST API development
* Django ORM
* Database relationships
* PostgreSQL
* Serializers
* API validation
* Business logic
* Authentication & permissions
* CRUD operations
* HTTP methods and status codes
* Postman API testing
* Git & GitHub

---

## 🎯 Learning Objectives

The project was developed to gain practical experience in designing and implementing a production-style backend system using Django and Django REST Framework.

It focuses on understanding how different backend components work together:

```text
Python
  ↓
Django
  ↓
Django REST Framework
  ↓
ORM
  ↓
PostgreSQL
  ↓
REST APIs
  ↓
Client / Postman
```

---

## 👨‍💻 Author

**Chaitanya Modi**

Python Backend Developer | Django | Django REST Framework | FastAPI | PostgreSQL

---

## ⭐ Project Highlights

* Designed relational database models using Django ORM
* Built RESTful APIs using Django REST Framework
* Implemented backend validation and business logic
* Applied OOP principles in backend development
* Managed product, category, cart, and order workflows
* Tested API behavior using Postman
* Used PostgreSQL for persistent relational data
