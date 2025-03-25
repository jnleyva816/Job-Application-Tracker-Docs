---
sidebar_position: 3
---

# Application API Reference 

This document describes how to use the Application API endpoints in the JobTracker backend.

## Base URL

All API endpoints are prefixed with the following base URL:
```
http://your-server/api/applications
```

## Authentication

The API uses JWT (JSON Web Token) authentication. The token should be included in the Authorization header of all requests to these endpoints. Additionally, many endpoints enforce authorization based on the user's role (ADMIN) and the ownership of the application being accessed.

## API Endpoints

### 1. Get All Applications

**Endpoint:** `GET /`

**Description:** Retrieves all job applications.

**Authorization:**
- If the user has the ADMIN role, retrieves all applications.
- Otherwise, retrieves only the applications associated with the currently authenticated user.

**Response:**
- **200 OK:** Returns a list of Application objects. The structure of the Application object is shown below.
- **401 Unauthorized:** If the user is not authenticated.
```json
[
    {
        "id": "integer",
        "company": "string",
        "jobTitle": "string",
        "location": "string",
        "url": "string",
        "description": "string",
        "compensation": "string",
        "status": "string",
        "applicationDate": "string",
        "user": {
            "id": "integer",
            "username": "string",
            // other user properties, but typically not the password
        }
        // ... other application properties
    },
    ...
]
```

### 2. Get Application by ID

**Endpoint:** `GET /{id}`

**Description:** Retrieves a specific job application by its ID.

**Path Variable:**
- `id`: The ID of the application to retrieve.

**Authorization:**
- If the user has the ADMIN role, can retrieve any application.
- Otherwise, can only retrieve applications associated with the currently authenticated user.

**Response:**
- **200 OK:** Returns the Application object.
- **401 Unauthorized:** If the user is not authenticated.
- **403 Forbidden:** If the user is not authorized to access the specified application.
- **404 Not Found:** If the application with the given ID does not exist.
```json
{
    "id": "integer",
    "company": "string",
    "jobTitle": "string",
    "location": "string",
    "url": "string",
    "description": "string",
    "compensation": "string",
    "status": "string",
    "applicationDate": "string",
    "user": {
        "id": "integer",
        "username": "string",
        // other user properties
    }
    // ... other application properties
}
```

### 3. Create Application

**Endpoint:** `POST /`

**Description:** Creates a new job application.

**Request Body:** The Application object to create. The user field in the request body is ignored; the application is automatically associated with the currently authenticated user.
```json
{
    "company": "string",
    "jobTitle": "string",
    "location": "string",
    "url": "string",
    "description": "string",
    "compensation": "string",
    "status": "string",
    "applicationDate": "string",
    // ... other application properties (excluding id and user)
}
```

**Authorization:** Requires a valid JWT token.

**Response:**
- **201 Created:** Returns the created Application object, including the generated ID and the user it was assigned to.
```json
{
    "id": "integer",
    "company": "string",
    "jobTitle": "string",
    "location": "string",
    "url": "string",
    "description": "string",
    "compensation": "string",
    "status": "string",
    "applicationDate": "string",
    "user": {
        "id": "integer",
        "username": "string",
    },
    // ... other application properties
}
```

### 4. Update Application

**Endpoint:** `PUT /{id}`

**Description:** Updates an existing job application.

**Path Variable:**
- `id`: The ID of the application to update.

**Request Body:** The Application object containing the updated information. The user field in the request body is ignored; the application remains associated with its original user.
```json
{
    "company": "string",
    "jobTitle": "string",
    "location": "string",
    "url": "string",
    "description": "string",
    "compensation": "string",
    "status": "string",
    "applicationDate": "string"
    // ... other application properties
}
```

**Authorization:**
- If the user has the ADMIN role, can update any application.
- Otherwise, can only update applications associated with the currently authenticated user.

**Response:**
- **200 OK:** Returns the updated Application object.
- **401 Unauthorized:** If the user is not authenticated.
- **403 Forbidden:** If the user is not authorized to update the specified application.
- **404 Not Found:** If the application with the given ID does not exist.
```json
{
    "id": "integer",
    "company": "string",
    "jobTitle": "string",
    "location": "string",
    "url": "string",
    "description": "string",
    "compensation": "string",
    "status": "string",
    "applicationDate": "string",
    "user": {
        "id": "integer",
        "username": "string",
    },
    // ... other application properties
}
```

### 5. Delete Application

**Endpoint:** `DELETE /{id}`

**Description:** Deletes a job application.

**Path Variable:**
- `id`: The ID of the application to delete.

**Authorization:**
- If the user has the ADMIN role, can delete any application.
- Otherwise, can only delete applications associated with the currently authenticated user.

**Response:**
- **204 No Content:** Indicates successful deletion.
- **401 Unauthorized:** If the user is not authenticated.
- **403 Forbidden:** If the user is not authorized to delete the specified application.
- **404 Not Found:** If the application with the given ID does not exist.

### Get Application Statistics

```http
GET /api/applications/statistics
```

Get statistics about the user's job applications.

#### Response

- **Success (200 OK)**
```json
{
  "totalApplications": "number",
  "applicationsByStatus": {
    "PENDING": "number",
    "INTERVIEW_SCHEDULED": "number",
    "OFFER_RECEIVED": "number",
    "REJECTED": "number",
    "ACCEPTED": "number"
  },
  "applicationsByMonth": [
    {
      "month": "string",
      "count": "number"
    }
  ]
}
```

## Error Responses

All endpoints may return the following error responses:

- **400 Bad Request**
```json
{
  "message": "Invalid request data"
}
```

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

- **404 Not Found**
```json
{
  "message": "Application not found"
}
```

- **500 Internal Server Error**
```json
{
  "message": "An unexpected error occurred"
}
``` 