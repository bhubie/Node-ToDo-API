# Node-ToDo-API
Simple RESTful ToDo API with User Authentication built with Node.js and MongoDB as the backend database

User authentication is done via JWT

## Running the API Server
1.) Clone/Download Repository

2.) Create config.json file in server/config with the below values
``` bash
{
  "test": {
    "PORT": 3000,
    "MONGODB_URI": "mongodb://localhost:27017/TodoAppTest",
    "JWT_SECRET": "SecretForTesting"
  },
  "development": {
    "PORT": 3000,
    "MONGODB_URI": "mongodb://localhost:27017/TodoApp",
    "JWT_SECRET": "SecretForProduction"
  }
}
```

3.) Download and start MongoDB Community Server if not already installed

4.) CD into the repository via the terimal

5.) Run NPM Start to start the server - you are now able to make API Calls

## API Routes and Examples

### POST /users
- creates a new user
- JWT is sent back in response header

Request:
``` bash
Body:
{
	"email": "example@example.com",
	"password": "123456789"
}
```
Response:
``` bash
Header: 
x-auth: generatedToken
Body:
{
    "_id": "5aa895bc91847c75aaa40e2b",
    "email": "example@example.com"
}
```

### POST users/login
- creates a new user
- JWT is sent back in response header

Request:
``` bash
{
	"email": "example@example.com",
	"password": "123456789"
}
```
Response:
``` bash
Header:
x-auth: generatedToken
Body:
{
    "_id": "5aa895bc91847c75aaa40e2b",
    "email": "example@example.com"
}
```

### DELETE users/me/token
- Logs out a user

Request:
``` bash
Header:
x-auth: generatedJsonWebToken
```
Response:
``` bash
Satus: 200 Ok
```

### POST /todos
- creates a new ToDo for a user
- JWT is sent back in response header

Request:
``` bash
Header:
x-auth: generatedJsonWebToken
Body:
{
	"text": "example To Do Task"
}
```
Response:
``` bash
Body:
{
    "__v": 0,
    "text": "example To Do Task",
    "_creator": "5aa895bc91847c75aaa40e2b",
    "_id": "5aa8a03791847c75aaa40e2f",
    "completedAt": null,
    "completed": false
}
```

### GET /todos/{id}
- returns a specific ToDo for a user

Request:
``` bash
Header:
x-auth: generatedJsonWebToken
```
Response:
``` bash
Body:
{
    "todo": {
        "_id": "5aa8a03791847c75aaa40e2f",
        "text": "example To Do Task",
        "_creator": "5aa895bc91847c75aaa40e2b",
        "__v": 0,
        "completedAt": null,
        "completed": false
    }
}
```

### DELETE /todos/{id}
- Deletes a specific ToDo for a user

Request:
``` bash
Header:
x-auth: generatedJsonWebToken
```
Response:
``` bash
Status: 200 Ok
```

### PATCH /todos/{id}
- Updates a specific ToDo for a user

Request:
``` bash
Header:
x-auth: generatedJsonWebToken
Body:
{
	"text": "example To Do Task",
  "completed": true
}
Response:
``` bash
Body: 
{
    "todo": {
        "_id": "5aa8a03791847c75aaa40e2f",
        "text": "example To Do Task",
        "_creator": "5aa895bc91847c75aaa40e2b",
        "__v": 0,
        "completedAt": 1521000997092,
        "completed": true
    }
}
```
