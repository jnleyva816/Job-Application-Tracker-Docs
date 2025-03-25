---
sidebar_position: 5
---

# Interview API Reference 

This document provides information on how to use the Interview API endpoints of the JobTracker backend.

## Base URL

All API endpoints are prefixed with the following base URL:
```
http://your-server/api/applications/{applicationId}/interviews
```

## Authentication

The API uses standard authentication and authorization mechanisms (e.g., JWT) to secure access to these endpoints. Specific roles or permissions might be required to access certain endpoints. Consult the application's security configuration for details.

## API Endpoints

### 1. Get All Interviews for an Application

**Endpoint:** `GET /`

**Description:** Retrieves all interviews for a specific application.

**Path Variable:**
- `applicationId`: The ID of the application.

**Authorization:** Requires appropriate permissions to view interviews for the application.

**Response:**
- **200 OK:** Returns a list of Interview objects.
```json
[
    {
        "id": "integer",
        "applicationId": "integer",
        "date": "string",
        "notes": "string",
        // ... other interview properties
    },
    ...
]
```

### 2. Get Interview by ID

**Endpoint:** `GET /{interviewId}`

**Description:** Retrieves a specific interview by its ID for a given application.

**Path Variables:**
- `applicationId`: The ID of the application.
- `interviewId`: The ID of the interview.

**Authorization:** Requires appropriate permissions to view the interview for the application.

**Response:**
- **200 OK:** Returns the Interview object.
```json
{
    "id": "integer",
    "applicationId": "integer",
    "date": "string",
    "notes": "string",
    // ... other interview properties
}
```
- **404 Not Found:** The interview with the given ID was not found for the application.

### 3. Create Interview

**Endpoint:** `POST /`

**Description:** Creates a new interview for a specific application.

**Path Variable:**
- `applicationId`: The ID of the application.

**Request Body:** The Interview object to create.
```json
{
    "date": "string",
    "notes": "string",
    // ... other interview properties (excluding id and applicationId)
}
```

**Authorization:** Requires appropriate permissions to create interviews for the application.

**Response:**
- **201 Created:** Returns the created Interview object, including the generated ID.
```json
{
    "id": "integer",
    "applicationId": "integer",
    "date": "string",
    "notes": "string",
    // ... other interview properties
}
```

### 4. Update Interview

**Endpoint:** `PUT /{interviewId}`

**Description:** Updates an existing interview for a specific application.

**Path Variables:**
- `applicationId`: The ID of the application.
- `interviewId`: The ID of the interview to update.

**Request Body:** The updated Interview object.
```json
{
    "date": "string",
    "notes": "string",
    // ... other interview properties
}
```

**Authorization:** Requires appropriate permissions to update interviews for the application.

**Response:**
- **200 OK:** Returns the updated Interview object.
```json
{
    "id": "integer",
    "applicationId": "integer",
    "date": "string",
    "notes": "string",
    // ... other interview properties
}
```

### 5. Delete Interview

**Endpoint:** `DELETE /{interviewId}`

**Description:** Deletes an interview for a specific application.

**Path Variables:**
- `applicationId`: The ID of the application.
- `interviewId`: The ID of the interview to delete.

**Authorization:** Requires appropriate permissions to delete interviews for the application.

**Response:**
- **204 No Content:** Indicates successful deletion.