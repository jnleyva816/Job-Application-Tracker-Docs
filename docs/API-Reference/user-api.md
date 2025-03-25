---
sidebar_position: 1
---

# User API Reference

This document outlines the available endpoints for user management in the Job Application Tracker.

## Base URL

All API endpoints are prefixed with `/api`

## Authentication

Most endpoints require authentication using a JWT token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

## Endpoints

### Register User

```http
POST /api/users/register
```

Register a new user in the system.

#### Request Body

```json
{
  "username": "string",
  "email": "string",
  "password": "string"
}
```

#### Response

- **Success (201 Created)**
```json
{
  "id": "string",
  "username": "string",
  "email": "string"
}
```

- **Error (400 Bad Request)**
```json
{
  "message": "Username or email already exists"
}
```

### Login User

```http
POST /api/users/login
```

Authenticate a user and receive a JWT token.

#### Request Body

```json
{
  "username": "string",
  "password": "string"
}
```

#### Response

- **Success (200 OK)**
```json
{
  "token": "string",
  "user": {
    "id": "string",
    "username": "string",
    "email": "string"
  }
}
```

- **Error (401 Unauthorized)**
```json
{
  "message": "Invalid credentials"
}
```

### Get User Profile

```http
GET /api/users/profile
```

Retrieve the current user's profile information.

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "username": "string",
  "email": "string",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Update User Profile

```http
PUT /api/users/profile
```

Update the current user's profile information.

#### Request Body

```json
{
  "username": "string",
  "email": "string"
}
```

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "username": "string",
  "email": "string",
  "updatedAt": "string"
}
```

### Change Password

```http
PUT /api/users/change-password
```

Change the current user's password.

#### Request Body

```json
{
  "currentPassword": "string",
  "newPassword": "string"
}
```

#### Response

- **Success (200 OK)**
```json
{
  "message": "Password updated successfully"
}
```

- **Error (400 Bad Request)**
```json
{
  "message": "Current password is incorrect"
}
```

### Delete User Account

```http
DELETE /api/users/profile
```

Delete the current user's account.

#### Response

- **Success (200 OK)**
```json
{
  "message": "User account deleted successfully"
}
```

## Error Responses

All endpoints may return the following error responses:

- **401 Unauthorized**
```json
{
  "message": "Unauthorized access"
}
```

- **403 Forbidden**
```json
{
  "message": "Access forbidden"
}
```

- **500 Internal Server Error**
```json
{
  "message": "An unexpected error occurred"
}
``` 
