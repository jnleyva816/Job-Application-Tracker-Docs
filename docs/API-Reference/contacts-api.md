---
sidebar_position: 4
---

# Contacts API Reference

This document outlines the available endpoints for managing contacts in the Job Application Tracker.

## Base URL

All API endpoints are prefixed with `/api`

## Authentication

All endpoints require authentication using a JWT token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

## Endpoints

### Create Contact

```http
POST /api/contacts
```

Create a new contact.

#### Request Body

```json
{
  "name": "string",
  "email": "string",
  "phone": "string",
  "company": "string",
  "position": "string",
  "notes": "string",
  "applicationId": "string (optional)"
}
```

#### Response

- **Success (201 Created)**
```json
{
  "id": "string",
  "name": "string",
  "email": "string",
  "phone": "string",
  "company": "string",
  "position": "string",
  "notes": "string",
  "applicationId": "string",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Get All Contacts

```http
GET /api/contacts
```

Retrieve all contacts for the current user.

#### Query Parameters

- `company` (optional): Filter contacts by company
- `applicationId` (optional): Filter contacts by application ID
- `page` (optional): Page number for pagination (default: 0)
- `size` (optional): Number of items per page (default: 10)

#### Response

- **Success (200 OK)**
```json
{
  "content": [
    {
      "id": "string",
      "name": "string",
      "email": "string",
      "phone": "string",
      "company": "string",
      "position": "string",
      "notes": "string",
      "applicationId": "string",
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

### Get Contact by ID

```http
GET /api/contacts/{id}
```

Retrieve a specific contact by its ID.

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "name": "string",
  "email": "string",
  "phone": "string",
  "company": "string",
  "position": "string",
  "notes": "string",
  "applicationId": "string",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Update Contact

```http
PUT /api/contacts/{id}
```

Update an existing contact.

#### Request Body

```json
{
  "name": "string",
  "email": "string",
  "phone": "string",
  "company": "string",
  "position": "string",
  "notes": "string",
  "applicationId": "string"
}
```

#### Response

- **Success (200 OK)**
```json
{
  "id": "string",
  "name": "string",
  "email": "string",
  "phone": "string",
  "company": "string",
  "position": "string",
  "notes": "string",
  "applicationId": "string",
  "updatedAt": "string"
}
```

### Delete Contact

```http
DELETE /api/contacts/{id}
```

Delete a contact.

#### Response

- **Success (200 OK)**
```json
{
  "message": "Contact deleted successfully"
}
```

### Get Contacts by Company

```http
GET /api/contacts/company/{companyName}
```

Get all contacts associated with a specific company.

#### Response

- **Success (200 OK)**
```json
{
  "contacts": [
    {
      "id": "string",
      "name": "string",
      "email": "string",
      "phone": "string",
      "company": "string",
      "position": "string",
      "notes": "string",
      "applicationId": "string",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ]
}
```

### Get Contacts by Application

```http
GET /api/contacts/application/{applicationId}
```

Get all contacts associated with a specific job application.

#### Response

- **Success (200 OK)**
```json
{
  "contacts": [
    {
      "id": "string",
      "name": "string",
      "email": "string",
      "phone": "string",
      "company": "string",
      "position": "string",
      "notes": "string",
      "applicationId": "string",
      "createdAt": "string",
      "updatedAt": "string"
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
  "message": "Contact not found"
}
```

- **500 Internal Server Error**
```json
{
  "message": "An unexpected error occurred"
}
``` 