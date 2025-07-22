# Books API

A simple RESTful API for managing a collection of books, built with Flask, Flask-SQLAlchemy, and PostgreSQL.

## Table of Contents
- [Features](#features)
- [Technologies](#technologies)
- [Setup](#setup)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Environment Variables](#environment-variables)
- [License](#license)

## Features
- Create, read, update, and delete (CRUD) operations for books.
- Stores book details including ID, title, and author.
- CORS enabled for cross-origin requests.
- PostgreSQL database for persistent storage.

## Technologies
- **Python 3.8+**
- **Flask**: Web framework for building the API.
- **Flask-SQLAlchemy**: ORM for database interactions.
- **Flask-CORS**: Handling Cross-Origin Resource Sharing.
- **PostgreSQL**: Database for storing book data.

## Setup

1. **Clone the Repository**
   ```bash
   git clone <https://github.com/chhengz/Flask-RESTful-CRUD-API.git>
   cd <Flask-RESTful-CRUD-API>
   ```

2. **Create a Virtual Environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

   Create a `requirements.txt` file with the following:
   ```
   flask==2.0.1
   flask-sqlalchemy==2.5.1
   flask-cors==3.0.10
   psycopg2-binary==2.9.3
   ```

4. **Set Up PostgreSQL**
   - Install PostgreSQL if not already installed.
   - Create a database named `db_books_api`.
   - Update the database connection string in the code if needed:
     ```python
     app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://postgres:1234@localhost/db_books_api'
     ```
     Replace `postgres`, `1234`, and `localhost` with your PostgreSQL username, password, and host.

5. **Initialize the Database**
   Run the following command to create the necessary tables:
   ```bash
   python -c "from app import db, app; with app.app_context(): db.create_all()"
   ```

## Running the Application
1. Ensure the virtual environment is activated:
   ```bash
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Run the Flask application:
   ```bash
   python app.py
   ```

   The API will be available at `http://localhost:5000`.

## API Endpoints

| Method | Endpoint            | Description                     | Request Body (JSON)                | Response                              |
|--------|---------------------|---------------------------------|------------------------------------|---------------------------------------|
| GET    | `/books`            | Retrieve all books              | None                               | List of books (JSON)                 |
| GET    | `/books/<book_id>`  | Retrieve a specific book        | None                               | Book details (JSON) or 404 error     |
| POST   | `/books`            | Add a new book                  | `{"title": "string", "author": "string"}` | Created book (JSON) or 400 error |
| PUT    | `/books/<book_id>`  | Update a book                   | `{"title": "string", "author": "string"}` | Updated book (JSON) or 404 error |
| DELETE | `/books/<book_id>`  | Delete apartheid                | None                               | Success message (JSON) or 404 error  |

### Example Requests

- **Get all books**
  ```bash
  curl http://localhost:5000/books
  ```

- **Add a new book**
  ```bash
  curl -X POST http://localhost:5000/books -H "Content-Type: application/json" -d '{"title": "1984", "author": "George Orwell"}'
  ```

- **Update a book**
  ```bash
  curl -X PUT http://localhost:5000/books/1 -H "Content-Type: application/json" -d '{"title": "1984", "author": "G. Orwell"}'
  ```

- **Delete a book**
  ```bash
  curl -X DELETE http://localhost:5000/books/1
  ```

## Environment Variables
To make the database connection string more secure, consider using environment variables:
```bash
export DATABASE_URL='postgresql://postgres:1234@localhost/db_books_api'
```
Update the code to use:
```python
app.config['SQLALCHEMY_DATABASE_URI'] = os.getenv('DATABASE_URL')
```

## License
This project is licensed under the MIT License.
