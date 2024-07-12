# HNG Stage 2 Endpoint Definition

## Overview

API endpoints for stage 2 task

## Base URL

- Live URL: `https://example.com/api/v1`
- Staging URL: `https://staging.example.com/api/v1`

## Authentication
### Register

#### Create an account for a new user

- **Endpoint:** `/auth/register`
- **Method:** `POST`
- **Description:** Create an account for a new user

##### Body

```json
{
  "first_name": "Garfield",
  "last_name": "Shenko",
  "email": "garfield.shenko@gmail.com",
  "phone": "1234567890"
}
```
**Success Response:**

- **Code:** '201'
- **Content:**

```json
{
  "status": true,
  "message": "Your account has been created",
  "token": "access-token-here"
}
```

**Error Responses:**

- **Code:** 422
- **Content:**

```json
{
  "status": false,
  "message": "One or more required fields missing"
}
```
- **Code:** 409
- **Content:**

```json
{
  "status": false,
  "message": "Account with the email already exists"
}
```
### Login

#### Log a registered user into the app

- **Endpoint:** `/auth/login`
- **Method:** `POST`
- **Description:** Logs a registered user in

##### Body

```json
{
  "email": "garfield.shenko@gmail.com",
  "phone": "1234567890"
}
```
**Success Response:**

- **Code:** '200'
- **Content:**

```json
{
  "status": true,
  "message": "Login successful",
  "token": "access-token-here"
}
```

**Error Responses:**

- **Code:** 422
- **Content:**

```json
{
  "status": false,
  "message": "One or more required fields missing"
}
```
- **Code:** 401
- **Content:**

```json
{
  "status": false,
  "message": "Invalid credentials provided"
}
```
### Confirm token

#### Confirm token on registration

- **Endpoint:** `/auth/verify/{token}`
- **Method:** `POST`
- **Description:** This is used to verify a user's provided email during registration
> **NOTE**: A user has to verify their account before they can have access to the application

**Success Response:**

- **Code:** 200
- **Content:**

```json
{
  "status": true,
  "message": "Account verified successfully"
}
```

**Error Responses:**

- **Code:** 422
- **Content:**

```json
{
  "status": false,
  "message": "Invalid or expired token"
}
```

### Change password

#### Changes password for an authenticated user

- **Endpoint:** `/auth/change-password`
- **Method:** `POST`
- **Description:** Updates a user's password
- **Authorisation:** Required
  - **Type:** Bearer [JWT]
  - **Summary:** This endpoint requires a valid JWT token in the authorisation header


##### Body

```json
{
  "old_password": "12345",
  "new_password": "67890"
}
```
**Success Response:**

- **Code:** '200'
- **Content:**

```json
{
  "status": true,
  "message": "Password changed successfully"
}
```

**Error Responses:**

- **Code:** 422
- **Content:**

```json
{
  "status": false,
  "message": "One or more required fields missing"
}
```
- **Code:** 401
- **Content:**

```json
{
  "status": false,
  "message": "Invalid password provided, please check and try again"
}
```

### Google auth

#### Authenticate a user using google 

- **Endpoint:** `/auth/google-auth`
- **Method:** `POST`
- **Description:** Register or login a user using google auth



## [Section]

### [Endpoint]

#### [SubTitle]

- **Endpoint:** `/api/[version]/[endpoint]`
- **Method:** [HTTP-Method]
- **Description:** [Description]

**Body:**

```json
{
  "[Key]": "[value]"
}
```

**Success Response:**

- **Code:** [Code]
- **Content:**

```json
{
  "status": true,
  "message": "[Message]",
  "data": {
    "[Key]": "[value]"
  }
}
```

**Error Responses:**

- **Code:** [Status-Code]
- **Content:**

```json
{
  "status": false,
  "message": "[Message]"
}
```

## Versioning

This API is versioned to ensure backward compatibility and easy maintenance. The current version is [version].
