---
sidebar_position: 1
---

# JobTracker Backend User Documentation

This document provides information on how to use the User API endpoints of the JobTracker backend.

## Base URL

All API endpoints are prefixed with the following base URL:
```
http://your-server/api/users
```

## Authentication

The API uses JWT (JSON Web Token) authentication.
- Login: Upon successful login, the API returns a JWT token that must be included in the Authorization header of subsequent requests.
- Authorization: Certain endpoints are restricted to users with specific roles (e.g., ADMIN) or require the user to have specific permissions related to the data being accessed.

## API Endpoints

### 1. Login

**Endpoint:** `POST /login`

**Description:** Authenticates a user and returns a JWT token.

**Request Body:**
```json
{
    "username": "string",
    "password": "string"
}
```

**Response:**
- **200 OK:** Returns a LoginResponse object containing the JWT token.
```json
{
    "token": "string"
}
```
- **401 Unauthorized:** Invalid credentials. Returns an ErrorResponse object.
```json
{
    "message": "Invalid credentials"
}
```
- **403 Forbidden:** Account is locked. Returns an ErrorResponse
```json
{
    "message": "Account is temporarily locked. Please try again later."
}
```

**Error Handling:**
- The API will return a 401 status code if the username or password is incorrect.
- The API will return a 403 status code if the account is locked due to too many failed login attempts.
- The API resets failed login attempts after a successful login.

### 2. Register User

**Endpoint:** `POST /register`

**Description:** Registers a new user.

**Request Body:**
```json
{
    "username": "string",
    "password": "string",
    "email": "string",
    "firstName": "string", //optional
    "lastName": "string"  //optional
    // ... other user properties
}
```

**Response:**
- **201 Created:** Returns a UserResponse object containing the ID, username, and email of the created user.
```json
{
    "id": 123,
    "username": "string",
    "email": "string"
}
```
- **400 Bad Request:** Invalid input data. Returns an ErrorResponse object.
```json
{
    "message": "Invalid input data: ..."
}
```
- **409 Conflict:** Username or email already exists. Returns an ErrorResponse object.
```json
{
    "message": "Username or email already exists"
}
```

**Error Handling:**
- The API will return a 400 status code for invalid input data.
- The API will return a 409 status code if the username or email is already taken.

### 3. Get All Users

**Endpoint:** `GET /`

**Description:** Retrieves a list of all users.

**Authorization:** Requires the ADMIN role.

**Response:**
- **200 OK:** Returns a list of User objects.

### 4. Get User by ID

**Endpoint:** `GET /{id}`

**Description:** Retrieves a user by their ID.

**Authorization:** Requires the ADMIN role or the user making the request must have the same ID as the user being requested.

**Path Variable:**
- `id`: The ID of the user to retrieve.

**Response:**
- **200 OK:** Returns the User object.

### 5. Get User by Username

**Endpoint:** `GET /username/{username}`

**Description:** Retrieves a user by their username.

**Authorization:** Requires the ADMIN role or the user making the request must have the same username as the user being requested.

**Path Variable:**
- `username`: The username of the user to retrieve.

**Response:**
- **200 OK:** Returns the User object.

### 6. Get User by Email

**Endpoint:** `GET /email/{email}`

**Description:** Retrieves a user by their email.

**Authorization:** Requires the ADMIN role or the user making the request must have the same email as the user being requested.

**Path Variable:**
- `email`: The email of the user to retrieve

**Response:**
- **200 OK:** Returns the User object.

### 7. Update User

**Endpoint:** `PUT /{id}`

**Description:** Updates an existing user.

**Authorization:** Requires the ADMIN role or the user making the request must have the same ID as the user being updated.

**Path Variable:**
- `id`: The ID of the user to update.

**Request Body:**
```json
{
    "username": "string",
    "email": "string",
    "firstName": "string",
    "lastName": "string",
    // ... other user properties to update
}
```

**Response:**
- **200 OK:** Returns the updated User object.

### 8. Delete User

**Endpoint:** `DELETE /{id}`

**Description:** Deletes a user.

**Authorization:** Requires the ADMIN role or the user making the request must have the same ID as the user being deleted.

**Path Variable:**
- `id`: The ID of the user to delete.

**Response:**
- **204 No Content:** Indicates successful deletion.

### 9. Logout

**Endpoint:** `POST /logout`

**Description:** Logs out the current user.

**Authorization:** While the backend doesn't invalidate the token, the client should remove the token from storage.

**Response:**
- **200 OK:** Returns a MessageResponse object.
```json
{
    "message": "Successfully logged out"
}
```

## Request and Response Objects

### LoginRequest
```json
{
    "username": "string",
    "password": "string"
}
```

### LoginResponse
```json
{
    "token": "string"
}
```

### ErrorResponse
```json
{
    "message": "string"
}
```

### UserResponse
```json
{
    "id": "integer",
    "username": "string",
    "email": "string"
}
```

### MessageResponse
```json
{
    "message": "string"
}
```

### User
```json
{
    "id": "integer",
    "username": "string",
    "email": "string",
    "firstName": "string",
    "lastName": "string",
    // ... other user properties
    "accountLocked": "boolean"
}
``` 
