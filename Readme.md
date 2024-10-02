Here’s an updated `README.md` with a link to the Swagger documentation:

---

# Todo REST API in Go

This is a simple Todo REST API built using Go with [Fiber](https://gofiber.io/), MongoDB, and [godotenv](https://github.com/joho/godotenv) for environment variable management.

## Prerequisites

- Go installed (version 1.16 or above)
- MongoDB running
- Docker (optional for running the app in a container)

## Project Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd <project-directory>
```

### 2. Install dependencies

```bash
go mod tidy
```

### 3. Create `.env` file

Create a `.env` file in the root directory of your project with the following variables:

```env
DB_URL=mongodb://localhost:27017
PORT=5000
```

Make sure `DB_URL` points to your running MongoDB instance.

### 4. Run the project

Start the application using [Air](https://github.com/cosmtrek/air) for live reloading, or just use Go directly.

Using Air:

```bash
air
```

Using Go:

```bash
go run main.go
```

By default, the server will run on port `5000`. You can change this in the `.env` file.

## API Documentation

The API documentation is available in the [Swagger](https://swagger.io/) format.

### Access the Swagger documentation

1. You can explore the API endpoints and test the API interactively using Swagger. 
2. To view the Swagger documentation locally, install [Swagger UI](https://swagger.io/tools/swagger-ui/) or use [ReDoc](https://github.com/Redocly/redoc).
3. The API documentation is defined in the `swagger.yaml` file in the project. You can use the following link to view it in Swagger UI:

- [Swagger Documentation](swagger.yaml)

## API Endpoints

### Get All Todos

- **URL**: `/api/todos`
- **Method**: `GET`
- **Response**: JSON array of all todos in the database

#### Example Request:

```bash
curl -X GET http://localhost:5000/api/todos
```

#### Example Response:

```json
[
  {
    "id": "63419d9a0f9e7f9a9f7e1234",
    "completed": false,
    "body": "Write documentation"
  },
  {
    "id": "63419d9a0f9e7f9a9f7e1235",
    "completed": true,
    "body": "Setup project"
  }
]
```

### Create a Todo

- **URL**: `/api/todos`
- **Method**: `POST`
- **Request Body**:

  ```json
  {
    "body": "Todo content here",
    "completed": false
  }
  ```

- **Response**: Created Todo object with its MongoDB ID

#### Example Request:

```bash
curl -X POST http://localhost:5000/api/todos -H "Content-Type: application/json" -d '{"body": "New Todo", "completed": false}'
```

#### Example Response:

```json
{
  "id": "63419d9a0f9e7f9a9f7e1236",
  "completed": false,
  "body": "New Todo"
}
```

### Update a Todo

- **URL**: `/api/todos/:id`
- **Method**: `PATCH`
- **Request Params**:
  - `id` - ID of the todo to update (as URL parameter)
- **Request Body**:
  - This endpoint is designed to mark a todo as completed, so no request body is needed.
- **Response**: Success message upon successful update

#### Example Request:

```bash
curl -X PATCH http://localhost:5000/api/todos/63419d9a0f9e7f9a9f7e1234
```

#### Example Response:

```json
{
  "update success": true
}
```

### Delete a Todo

- **URL**: `/api/todos/:id`
- **Method**: `DELETE`
- **Request Params**:
  - `id` - ID of the todo to delete (as URL parameter)
- **Response**: Success message upon successful deletion

#### Example Request:

```bash
curl -X DELETE http://localhost:5000/api/todos/63419d9a0f9e7f9a9f7e1234
```

#### Example Response:

```json
{
  "delete success": true
}
```

## Error Handling

The API handles errors by returning a JSON object with an appropriate HTTP status code and a descriptive error message.

Example error responses:

- **Invalid ID**:

  ```json
  {
    "error": "Invalid ID"
  }
  ```

- **Empty Todo Body**:

  ```json
  {
    "error": "Todo body cannot be empty"
  }
  ```
