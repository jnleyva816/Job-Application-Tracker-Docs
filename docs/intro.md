---
sidebar_position: 1
---

# Introduction

Welcome to the Job Application Tracker API documentation. This documentation will guide you through the available endpoints and how to use them effectively.

## Overview

The Job Application Tracker API provides a comprehensive set of endpoints for managing:
- User accounts and authentication
- Job applications
- Interviews
- Professional contacts

## Getting Started

1. **Authentication**: Most endpoints require authentication using JWT tokens
2. **Base URL**: All API endpoints are prefixed with `/api`
3. **Response Format**: All responses are in JSON format

## API Categories

### User Management
- User registration and authentication
- Profile management
- Password management

### Applications
- Create and manage job applications
- Track application status
- View application statistics

### Interviews
- Schedule and manage interviews
- Track interview status
- View upcoming interviews

### Contacts
- Manage professional contacts
- Associate contacts with applications
- Track company-specific contacts

## Error Handling

The API uses standard HTTP status codes and returns error messages in a consistent format:

```json
{
  "message": "Error description"
}
```

Common status codes:
- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 500: Internal Server Error

## Rate Limiting

The API implements rate limiting to ensure fair usage. Rate limit information is included in the response headers:
- `X-RateLimit-Limit`: Maximum number of requests per time window
- `X-RateLimit-Remaining`: Number of requests remaining in the current time window
- `X-RateLimit-Reset`: Time when the rate limit will reset 