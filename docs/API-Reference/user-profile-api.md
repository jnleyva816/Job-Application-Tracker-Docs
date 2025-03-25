---
sidebar_position: 2
---

# User Profile API Reference 

This document provides information on how to use the User Profile API endpoints of the JobTracker backend.

## Base URL

All API endpoints are prefixed with the following base URL:
```
http://your-server/api/profile
```

## Authentication

The API uses JWT (JSON Web Token) authentication. The token should be included in the Authorization header of all requests to these endpoints.

## API Endpoints

### 1. Get Current User Profile

**Endpoint:** `GET /`

**Description:** Retrieves the profile of the currently authenticated user.

**Authorization:** Requires a valid JWT token.

**Response:**
- **200 OK:** Returns the User object representing the current user's profile (with the password field set to null).
```json
{
    "id": "integer",
    "username": "string",
    "email": "string",
    "firstName": "string",
    "lastName": "string",
    // ... other user properties,
    "password": null
}
```

### 2. Update Current User Profile

**Endpoint:** `PUT /`

**Description:** Updates the profile of the currently authenticated user.

**Authorization:** Requires a valid JWT token.

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
- **200 OK:** Returns the updated User object (with the password field set to null).
```json
{
    "id": "integer",
    "username": "string",
    "email": "string",
    "firstName": "string",
    "lastName": "string",
    // ... other user properties,
    "password": null
}
```

### 3. Change Password

**Endpoint:** `PUT /change-password`

**Description:** Changes the password of the currently authenticated user.

**Authorization:** Requires a valid JWT token.

**Request Body:**
```json
{
    "newPassword": "string"
}
```

**Response:**
- **200 OK:** Returns a PasswordChangeResponse object.
```json
{
    "message": "Password changed successfully"
}
```

## Request and Response Objects

### PasswordChangeRequest
```json
{
    "newPassword": "string"
}
```

### PasswordChangeResponse
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
    "password": "string" // Note: This is set to null in the responses for GET and PUT in this controller.
}
```
