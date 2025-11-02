# FastAPI Posts API

A simple REST API built with FastAPI and PostgreSQL for managing blog posts.

## Features

- Create, read, update, and delete posts
- PostgreSQL database integration
- Input validation with Pydantic
- RESTful API endpoints

## Prerequisites

- Python 3.13+ (managed with pyenv)
- PostgreSQL
- pip

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd FASTAPI
```

2. Install dependencies:
```bash
pip install fastapi uvicorn psycopg2-binary
```

3. Set up PostgreSQL:
```bash
# Create user
psql -U postgres -c "CREATE USER fastapi WITH PASSWORD 'your_password_here';"

# Create database
psql -U postgres -c "CREATE DATABASE fastapi OWNER fastapi;"

# Create posts table
psql -U fastapi -d fastapi -c "CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    title VARCHAR NOT NULL,
    content VARCHAR NOT NULL,
    published BOOLEAN NOT NULL DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT NOW()
);"
```

4. Configure database credentials:
```bash
cp app/config.py.example app/config.py
# Edit app/config.py with your database credentials
```

## Running the Application

```bash
cd app
uvicorn main:app --reload
```

The API will be available at `http://127.0.0.1:8000`

## API Endpoints

### Get All Posts
```
GET /posts
```

### Get Single Post
```
GET /posts/{id}
```

### Create Post
```
POST /posts
Content-Type: application/json

{
    "title": "Post title",
    "content": "Post content",
    "published": true
}
```

### Update Post
```
PUT /posts/{id}
Content-Type: application/json

{
    "title": "Updated title",
    "content": "Updated content",
    "published": false
}
```

### Delete Post
```
DELETE /posts/{id}
```

## Project Structure

```
FASTAPI/
├── app/
│   ├── main.py           # FastAPI application
│   ├── config.py         # Database configuration (not tracked)
│   └── config.py.example # Configuration template
├── .vscode/
│   └── settings.json     # VS Code settings
├── .gitignore
└── README.md
```

## API Documentation

Once the server is running, you can access:
- Swagger UI: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

## Development

This project uses:
- **FastAPI**: Modern web framework for building APIs
- **Uvicorn**: ASGI server
- **PostgreSQL**: Relational database
- **Pydantic**: Data validation
- **psycopg2**: PostgreSQL adapter

## License

MIT
