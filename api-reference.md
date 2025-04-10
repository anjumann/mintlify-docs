# HeyHomie API Reference

This page provides an overview of the HeyHomie API and how to access the comprehensive API documentation.

## API Documentation

The complete API documentation is available through Swagger UI:

[**Access HeyHomie API Documentation**](https://heyhomie.me/api/system/docs)

## Key API Endpoints

The HeyHomie API includes the following major endpoint groups:

### Auth

- **POST /api/v1/auth/login**: Initiate login with phone number
- **POST /api/v1/auth/verify-otp**: Verify OTP and get authentication token
- **GET /api/v1/auth/me**: Get current user profile
- **POST /api/v1/auth/refresh**: Refresh authentication token

### Products

- **GET /api/v1/products**: List products with pagination and filtering
- **GET /api/v1/products/{id}**: Get detailed product information
- **GET /api/v1/products/collections**: Get product collections
- **GET /api/v1/products/search**: Search products by query

### Collections

- **GET /api/v1/collections**: List all collections
- **GET /api/v1/collections/{id}**: Get collection details with products

### Cart

- **POST /api/v1/cart**: Create a new cart
- **GET /api/v1/cart/{id}**: Get cart details
- **POST /api/v1/cart/{id}/line-items**: Add item to cart
- **DELETE /api/v1/cart/{id}/line-items/{item_id}**: Remove item from cart

### Orders

- **POST /api/v1/orders**: Create a new order
- **GET /api/v1/orders**: List user orders
- **GET /api/v1/orders/{id}**: Get order details
- **GET /api/v1/orders/{id}/status**: Get order status

### Payments

- **POST /api/v1/payments/razorpay/create**: Create a Razorpay payment order
- **POST /api/v1/payments/razorpay/verify**: Verify Razorpay payment
- **POST /api/v1/payments/razorpay/webhook**: Razorpay webhook endpoint

### Shipping

- **GET /api/v1/shipping/calculate**: Calculate shipping rates
- **GET /api/v1/shipping/methods**: Get available shipping methods
- **GET /api/v1/shipping/track/{tracking_number}**: Track shipment

### User

- **GET /api/v1/users/profile**: Get user profile
- **PUT /api/v1/users/profile**: Update user profile
- **GET /api/v1/users/addresses**: Get user addresses
- **POST /api/v1/users/addresses**: Add a new address

## Authentication

All API endpoints (except public ones) require authentication. The API uses JWT tokens for authentication:

1. Request an OTP to your phone number using `/api/v1/auth/login`
2. Verify the OTP using `/api/v1/auth/verify-otp` to receive a JWT token
3. Include the JWT token in the Authorization header for all subsequent requests:
   ```
   Authorization: Bearer YOUR_JWT_TOKEN
   ```

## Request Format

API requests should follow these conventions:

- Use proper HTTP methods (GET, POST, PUT, DELETE)
- Send data in JSON format
- Include appropriate headers:
  - `Content-Type: application/json`
  - `Authorization: Bearer YOUR_JWT_TOKEN` (for authenticated endpoints)

## Response Format

API responses follow a standard format:

```json
{
  "data": {
    // Response data specific to the endpoint
  },
  "meta": {
    // Metadata, such as pagination info
    "page": 1,
    "limit": 10,
    "total": 100
  }
}
```

Error responses:

```json
{
  "statusCode": 400,
  "message": ["Error message details"]
}
```

## Pagination, Sorting, and Filtering

Many list endpoints support pagination, sorting, and filtering:

### Pagination

```
GET /api/v1/products?page=2&limit=20
```

### Sorting

```
GET /api/v1/products?sort=createdAt:desc
```

### Filtering

```
GET /api/v1/products?filter[category]=electronics&filter[price_lt]=1000
```

## API Versioning

The current API version is v1. All endpoints are prefixed with `/api/v1/`.

## Rate Limiting

The API implements rate limiting to prevent abuse. The current limits are:

- 60 requests per minute for authenticated users
- 30 requests per minute for unauthenticated users

When a rate limit is exceeded, the API returns a 429 Too Many Requests response.

## Using the Swagger Documentation

The Swagger UI provides:

1. A complete list of all available endpoints
2. Request parameter details
3. Response schema information
4. The ability to try endpoints directly from the browser

To use the Swagger UI:

1. Navigate to [https://heyhomie.me/api/system/docs](https://heyhomie.me/api/system/docs)
2. Authenticate if needed for testing protected endpoints
3. Expand the endpoint you want to explore
4. Review parameters and response schemas
5. Use the "Try it out" feature to test endpoints 