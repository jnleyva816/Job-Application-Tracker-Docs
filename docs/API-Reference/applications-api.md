---
sidebar_position: 2
---

# Applications API Reference

This document outlines the available endpoints for managing job applications in the Job Application Tracker.

## Base URL

All API endpoints are prefixed with `/api`

## Authentication

All endpoints require authentication using a JWT token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

## Endpoints

### Create Application

```http
POST /api/applications
```

Create a new job application.

#### Request Body

```json
{
  "companyName": "string",
  "positionTitle": "string",
  "applicationDate": "string (ISO date)",
  "status": "string (PENDING, INTERVIEW_SCHEDULED, OFFER_RECEIVED, REJECTED, ACCEPTED)",
  "jobDescription": "string",
  "applicationUrl": "string",
  "notes": "string"
}
```

#### Response

- **Success (201 Created)**
```json
{
  "id": "string",
  "companyName": "string",
  "positionTitle": "string",
  "applicationDate": "string",
  "status": "string",
  "jobDescription": "string",
  "applicationUrl": "string",
  "notes": "string",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Get All Applications

```http
GET /api/applications
```

Retrieve all job applications for the current user.

#### Query Parameters

- `status` (optional): Filter applications by status
- `companyName` (optional): Filter applications by company name
- `page` (optional): Page number for pagination (default: 0)
- `size` (optional): Number of items per page (default: 10)

#### Response

- **Success (200 OK)**
```json
{
  "content": [
    {
      "id": "string",
      "companyName": "string",
      "positionTitle": "string",
      "applicationDate": "string",
      "status": "string",
      "jobDescription": "string",
      "applicationUrl": "string",
      "notes": "string",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "currentPage": "number",
  "size": "number"
}
```

### Get Application by ID

```http
GET /api/applications/{id}
```

Retrieve a specific job application by its ID.

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "companyName": "string",
  "positionTitle": "string",
  "applicationDate": "string",
  "status": "string",
  "jobDescription": "string",
  "applicationUrl": "string",
  "notes": "string",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Update Application

```http
PUT /api/applications/{id}
```

Update an existing job application.

#### Request Body

```json
{
  "companyName": "string",
  "positionTitle": "string",
  "applicationDate": "string",
  "status": "string",
  "jobDescription": "string",
  "applicationUrl": "string",
  "notes": "string"
}
```

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "companyName": "string",
  "positionTitle": "string",
  "applicationDate": "string",
  "status": "string",
  "jobDescription": "string",
  "applicationUrl": "string",
  "notes": "string",
  "updatedAt": "string"
}
```

### Delete Application

```http
DELETE /api/applications/{id}
```

Delete a job application.

#### Response

- **Success (200 OK)**
```json
{
  "message": "Application deleted successfully"
}
```

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