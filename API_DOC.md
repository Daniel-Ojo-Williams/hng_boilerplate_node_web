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

### Google Authentication  

#### Register and Login  

- **Endpoint:** /api/v1/auth/google  
- **Method:** POST  
- **Description:** Register a new user and log in using Google authentication.  

**Body:**  

```json 
{
  "idToken": "user's Google ID token"
}
```

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "User registered and logged in successfully",
  "data": {
    "userId": "user's ID",
    "username": "user's username",
    "email": "user's email"
  }
}
```

**Error Responses:**  

**Code:** 400  
**Content:**  

```json
{
  "status": false,
  "message": "Invalid ID token"
}
```

### Magic Link Authentication  

### Login  

- **Endpoint:** /api/v1/auth/magic-link  
- **Method:** POST  
- **Description:** Log in using a magic link.  

**Body:**  

```json
{
  "email": "user's email"
}
```

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Magic link sent to email",
  "data": {
    "email": "user's email"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Invalid email"
}
```

### Email Messaging  

#### Send Email  

- **Endpoint:** /api/v1/email/send  
- **Method:** POST  
- **Description:** Send an email message using a default template. This operation is performed in the background.  

**Body:**  

```json
{
  "to": "recipient's email address",
  "templateId": "ID of the email template",
  "variables": {
    "variable1": "value1",
    "variable2": "value2"
    // other variables for the template
  }
}
```

**Success Response:**  


- **Code:** 202  
- **Content:**  

```json
{
  "status": true,
  "message": "Email is being sent",
  "data": {
    "to": "recipient's email address",
    "templateId": "ID of the email template"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Invalid input"
}
```

## Payments  

### Stripe Integration  

- **Endpoint:** /api/v1/payments/stripe  
- **Method:** POST  
- **Description:** Process a payment through Stripe.  

**Body:**  

```json
{
  "amount": "amount_in_cents",
  "currency": "currency_code",
  "source": "stripe_token"
}
```
**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Payment processed successfully",
  "data": {
    "payment_id": "stripe_payment_id"
  }
}
```
**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

### Flutterwave Integration

- **Endpoint:** /api/v1/payments/flutterwave  
- **Method:** POST  
- **Description:** Process a payment through Flutterwave.  

**Body:**  

```json
{
  "amount": "amount_in_cents",
  "currency": "currency_code",
  "payment_method": "flutterwave_token"
}
```

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Payment processed successfully",
  "data": {
    "payment_id": "flutterwave_payment_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

### LemonSqueezy Integration  

- **Endpoint:** /api/v1/payments/lemonsqueezy  
- **Method:** POST  
- **Description:** Process a payment through LemonSqueezy.  

**Body:**  

```json
{
  "amount": "amount_in_cents",
  "currency": "currency_code",
  "payment_method": "lemonsqueezy_token"
}
```

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Payment processed successfully",
  "data": {
    "payment_id": "lemonsqueezy_payment_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

### Users  

#### Create User  
- **Endpoint:** /api/v1/users  
- **Method:** POST  
- **Description:** Create a new user.  

**Body:**  

```json 
{
  "username": "username",
  "email": "email",
  "password": "password"
}
```

**Success Response:**  

- **Code:** 201  
- **Content:**  

```json
{
  "status": true,
  "message": "User created successfully",
  "data": {
    "user_id": "user_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Read User  

- **Endpoint:** /api/v1/users/{userId}  
- **Method:** GET  
- **Description:** Get a user’s details.  

**Success Response:**  

- **Code:** 200  
- **Content** :  

```json
{
  "status": true,
  "message": "User details retrieved successfully",
  "data": {
    "user": "user_details"
  }
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "User not found"
}
```

#### Update User  

- **Endpoint:** /api/v1/users/{userId}  
- **Method:** PUT  
- **Description:** Update a user’s details.  

**Body:**  

```json
{
  "username": "new_username",
  "email": "new_email"
}
```

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "User updated successfully",
  "data": {
    "user_id": "user_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Delete User  

- **Endpoint:** /api/v1/users/{userId}  
- **Method:** DELETE  
- **Description:** Delete a user.  

**Success Response:**  

**Code:** 200  
**Content:**  

```json
{
  "status": true,
  "message": "User deleted successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "User not found"
}
```

### Organisations  

#### Create Organisation  

- **Endpoint:** /api/v1/organisations  
- **Method:** POST  
- **Description:** Create a new organisation.  

**Body:**  

```json
{
  "name": "organisation_name",
  "description": "organisation_description"
}
```

**Success Response:**  

- **Code:** 201  
- **Content:**  

```json
{
  "status": true,
  "message": "Organisation created successfully",
  "data": {
    "organisation_id": "organisation_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Read Organisation  

- **Endpoint:** /api/v1/organisations/{organisationId}  
- **Method:** GET  
- **Description:** Get an organisation’s details.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Organisation details retrieved successfully",
  "data": {
    "organisation": "organisation_details"
  }
}
```
**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Organisation not found"
}
```

#### Update Organisation  

- **Endpoint:** /api/v1/organisations/{organisationId}  
- **Method:** PUT  
- **Description:** Update an organisation’s details.  

**Body:**  

```json
{
  "name": "new_organisation_name",
  "description": "new_organisation_description"
}
```

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json 
{
  "status": true,
  "message": "Organisation updated successfully",
  "data": {
    "organisation_id": "organisation_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Delete Organisation  

- **Endpoint:** /api/v1/organisations/{organisationId}  
- **Method:** DELETE  
- **Description:** Delete an organisation.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Organisation deleted successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Organisation not found"
}
```

#### Add User to Organisation  

- **Endpoint:** /api/v1/organisations/{organisationId}/users/{userId}  
- **Method:** POST  
- **Description:** Add a user to an organisation.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "User added to organisation successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "User or organisation not found"
}
```

#### Get Organisation a User Belongs To  

- **Endpoint:** /api/v1/users/{userId}/organisations  
- **Method:** GET  
- **Description:** Get the organisation a user belongs to.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Organisation retrieved successfully",
  "data": {
    "organisation": "organisation_details"
  }
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "User not found"
}
```

#### Remove User from Organisation
- **Endpoint:** /api/v1/organisations/{organisationId}/users/{userId}  
- **Method:** DELETE  
- **Description:** Remove a user from an organisation.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "User removed from organisation successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "User or organisation not found"
}
```

### Notifications  

#### Send Notification  

- **Endpoint:** /api/v1/notifications  
- **Method:** POST  
- **Description:** Send a notification to a user.  

**Body:**  

```json
{
  "userId": "user_id",
  "message": "notification_message"
}
```

**Success Response:**  

- **Code:** 201  
- **Content:**  

```json
{
  "status": true,
  "message": "Notification sent successfully",
  "data": {
    "notification_id": "notification_id"
  }
}
```
  
**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Delete Notification  

- **Endpoint:** /api/v1/notifications/{notificationId}  
- **Method:** DELETE  
- **Description:** Delete a notification.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Notification deleted successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Notification not found"
}
```

#### Mark Notification as Seen  

- **Endpoint:** /api/v1/notifications/{notificationId}/seen  
- **Method:** PUT  
- **Description:** Mark a notification as seen.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Notification marked as seen successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Notification not found"
}
```

### Email Template Management  

#### Create Email Template  

- **Endpoint:** /api/v1/email-templates  
- **Method:** POST  
- **Description:** Create a new email template. Only accessible by a superadmin.  

**Body:**  

```json
{
  "name": "template_name",
  "content": "template_content"
}
```
  
**Success Response:**  

- **Code:** 201  
- **Content:**  

```json
{
  "status": true,
  "message": "Email template created successfully",
  "data": {
    "template_id": "template_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Read Email Template  

- **Endpoint:** /api/v1/email-templates/{templateId}  
- **Method:** GET  
- **Description:** Get an email template’s details. Only accessible by a superadmin.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Email template details retrieved successfully",
  "data": {
    "template": "template_details"
  }
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Email template not found"
}
```

#### Update Email Template  

- **Endpoint:** /api/v1/email-templates/{templateId}  
- **Method:** PUT  
- **Description:** Update an email template’s details. Only accessible by a superadmin.  

**Body:**  

```json
{
  "name": "new_template_name",
  "content": "new_template_content"
}
```
  
**Success Response:**  

- **Code**: 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Email template updated successfully",
  "data": {
    "template_id": "template_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Delete Email Template  

- **Endpoint:** /api/v1/email-templates/{templateId}  
- **Method:** DELETE  
- **Description:** Delete an email template. Only accessible by a superadmin.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Email template deleted successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Email template not found"
}
```
### Content Edit Page  

#### Create Blog Page  

- **Endpoint:** /api/v1/blogs  
- **Method:** POST  
- **Description:** Create a new blog page. Only accessible by an authorized user.  

**Body:**  

```json
{
  "title": "blog_title",
  "content": "blog_content"
}
```

**Success Response:**  

- **Code:** 201  
- **Content:**  

```json
{
  "status": true,
  "message": "Blog page created successfully",
  "data": {
    "blog_id": "blog_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Read Blog Page  

- **Endpoint:** /api/v1/blogs/{blogId}  
- **Method:** GET  
- **Description:** Retrieve the content of a blog page. Only accessible by an authorized user.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Blog page retrieved successfully",
  "data": {
    "blog": "blog_content"
  }
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Blog page not found"
}
```


#### Update Blog Page  

- **Endpoint:** /api/v1/blogs/{blogId}
- **Method:** PUT  
- **Description:** Edit the content of a blog page. Only accessible by an authorized user.  

**Body:**  

```json
{
  "title": "new_blog_title",
  "content": "new_blog_content"
}
```

**Success Response:**  

- **Code:** 200  
- **Content**:  

```json
{
  "status": true,
  "message": "Blog page updated successfully",
  "data": {
    "blog_id": "blog_id"
  }
}
```

**Error Responses:**  

- **Code:** 400  
- **Content:**  

```json
{
  "status": false,
  "message": "Error message"
}
```

#### Delete Blog Page  

- **Endpoint:** /api/v1/blogs/{blogId}  
- **Method:** DELETE  
- **Description:** Delete a blog page. Only accessible by an authorized user.  

**Success Response:**  

- **Code:** 200  
- **Content:**  

```json
{
  "status": true,
  "message": "Blog page deleted successfully"
}
```

**Error Responses:**  

- **Code:** 404  
- **Content:**  

```json
{
  "status": false,
  "message": "Blog page not found"
}
```

## Versioning

This API is versioned to ensure backward compatibility and easy maintenance. The current version is [version].
