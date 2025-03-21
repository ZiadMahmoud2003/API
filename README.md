# Flask Ecommerce API

This is a simple ecommerce API built with Flask and SQLAlchemy. It supports user registration, login, product creation, updating, fetching, and deletion. The API is protected by JSON Web Tokens (JWT) for secure access.

## Features

- User signup and login
- Secure password hashing
- JWT authentication
- CRUD operations for products
- Database interaction using SQLAlchemy

## Technologies Used

- Python
- Flask
- Flask-SQLAlchemy
- PyJWT
- MySQL
- Werkzeug for password hashing

## Getting Started

### Prerequisites

Make sure you have the following installed:

- Python 3.x
- MySQL Server
- `pip` for installing Python packages

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/flask-ecommerce-api.git
   cd flask-ecommerce-api
   ```

2. **Create and activate a virtual environment**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. **Install the required packages**

   ```bash
   pip install Flask Flask-SQLAlchemy PyJWT Werkzeug pymysql
   ```

4. **Set up the MySQL database**

   Run the following SQL commands in your MySQL server:

   ```sql
   CREATE DATABASE IF NOT EXISTS ecommerce;
   USE ecommerce;

   CREATE TABLE IF NOT EXISTS users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(80) NOT NULL,         
       username VARCHAR(80) NOT NULL UNIQUE, 
       password VARCHAR(200) NOT NULL     
   );

   CREATE TABLE IF NOT EXISTS product (
       pid INT AUTO_INCREMENT PRIMARY KEY, 
       pname VARCHAR(80) NOT NULL,        
       description TEXT,                  
       price DECIMAL(10, 2) NOT NULL,     
       stock INT NOT NULL,               
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP 
   );
   ```

5. **Configure the application**

   Update the `SECRET_KEY` in the application code if necessary.

### Running the Application

Run the application with the following command:

```bash
python app.py
```

The server will start at `http://127.0.0.1:5000`.

### API Endpoints

#### User Operations

- **Signup**: `POST /signup`
  - Request body: `{ "name": "John Doe", "username": "johndoe", "password": "yourpassword" }`
  - Response: User details (without the password)

- **Login**: `POST /login`
  - Request body: `{ "username": "johndoe", "password": "yourpassword" }`
  - Response: `{ "token": "your_jwt_token" }`

- **Update User**: `PUT /users/<user_id>`
  - Request header: `Authorization: Bearer <token>`
  - Request body: `{ "name": "John Doe Updated", "password": "newpassword" }`
  - Response: Updated user details

#### Product Operations

- **Create Product**: `POST /products`
  - Request header: `Authorization: Bearer <token>`
  - Request body: `{ "pname": "Product Name", "description": "Product Description", "price": 19.99, "stock": 10 }`
  - Response: Created product details

- **Get All Products**: `GET /products`
  - Request header: `Authorization: Bearer <token}`
  - Response: List of all products

- **Get Single Product**: `GET /products/<product_id>`
  - Request header: `Authorization: Bearer <token}`
  - Response: Product details

- **Update Product**: `PUT /products/<product_id>`
  - Request header: `Authorization: Bearer <token}`
  - Request body: `{ "pname": "Updated Product Name", "description": "Updated Description", "price": 29.99, "stock": 5 }`
  - Response: Updated product details

- **Delete Product**: `DELETE /products/<product_id>`
  - Request header: `Authorization: Bearer <token}`
  - Response: `{ "result": true }`

## Contributing

Feel free to fork the repository, make changes and submit pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
