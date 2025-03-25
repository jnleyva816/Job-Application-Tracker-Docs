---
sidebar_position: 3
---

# Interviews API Reference

This document outlines the available endpoints for managing job interviews in the Job Application Tracker.

## Base URL

All API endpoints are prefixed with `/api`

## Authentication

All endpoints require authentication using a JWT token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

## Endpoints

### Create Interview

```http
POST /api/interviews
```

Create a new interview for a job application.

#### Request Body

```json
{
  "applicationId": "string",
  "interviewType": "string (PHONE, VIDEO, IN_PERSON, TECHNICAL, BEHAVIORAL, FINAL)",
  "interviewDate": "string (ISO date)",
  "interviewTime": "string (ISO time)",
  "interviewerName": "string",
  "interviewerEmail": "string",
  "interviewLocation": "string",
  "notes": "string",
  "status": "string (SCHEDULED, COMPLETED, CANCELLED)"
}
```

#### Response

- **Success (201 Created)**
```json
{
  "id": "string",
  "applicationId": "string",
  "interviewType": "string",
  "interviewDate": "string",
  "interviewTime": "string",
  "interviewerName": "string",
  "interviewerEmail": "string",
  "interviewLocation": "string",
  "notes": "string",
  "status": "string",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Get All Interviews

```http
GET /api/interviews
```

Retrieve all interviews for the current user.

#### Query Parameters

- `applicationId` (optional): Filter interviews by application ID
- `status` (optional): Filter interviews by status
- `interviewType` (optional): Filter interviews by type
- `page` (optional): Page number for pagination (default: 0)
- `size` (optional): Number of items per page (default: 10)

#### Response

- **Success (200 OK)**
```json
{
  "content": [
    {
      "id": "string",
      "applicationId": "string",
      "interviewType": "string",
      "interviewDate": "string",
      "interviewTime": "string",
      "interviewerName": "string",
      "interviewerEmail": "string",
      "interviewLocation": "string",
      "notes": "string",
      "status": "string",
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

### Get Interview by ID

```http
GET /api/interviews/{id}
```

Retrieve a specific interview by its ID.

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "applicationId": "string",
  "interviewType": "string",
  "interviewDate": "string",
  "interviewTime": "string",
  "interviewerName": "string",
  "interviewerEmail": "string",
  "interviewLocation": "string",
  "notes": "string",
  "status": "string",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Update Interview

```http
PUT /api/interviews/{id}
```

Update an existing interview.

#### Request Body

```json
{
  "interviewType": "string",
  "interviewDate": "string",
  "interviewTime": "string",
  "interviewerName": "string",
  "interviewerEmail": "string",
  "interviewLocation": "string",
  "notes": "string",
  "status": "string"
}
```

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "applicationId": "string",
  "interviewType": "string",
  "interviewDate": "string",
  "interviewTime": "string",
  "interviewerName": "string",
  "interviewerEmail": "string",
  "interviewLocation": "string",
  "notes": "string",
  "status": "string",
  "updatedAt": "string"
}
```

### Delete Interview

```http
DELETE /api/interviews/{id}
```

Delete an interview.

#### Response

- **Success (200 OK)**
```json
{
  "message": "Interview deleted successfully"
}
```

### Get Upcoming Interviews

```http
GET /api/interviews/upcoming
```

Get a list of upcoming interviews for the current user.

#### Query Parameters

- `