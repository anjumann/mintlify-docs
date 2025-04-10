# API Development Guidelines

This document outlines the standards and best practices for API development in the HeyHomie NestJS application.

## RESTful API Design

### URL Structure

- Use kebab-case for URLs
- Use plural nouns for resources
- Use sub-resources for relationships
- Group related operations under the same controller

Example:

```bash
GET /api/products                # List all products
GET /api/products/{id}           # Get a specific product
POST /api/products               # Create a new product
PUT /api/products/{id}           # Update a product
DELETE /api/products/{id}        # Delete a product
GET /api/products/{id}/reviews   # Get reviews for a product
```

### HTTP Methods

- `GET`: Retrieve data
- `POST`: Create a new resource
- `PUT`: Update a resource (full update)
- `PATCH`: Partially update a resource
- `DELETE`: Remove a resource

### Response Codes

- `200 OK`: Successful request
- `201 Created`: Resource created successfully
- `204 No Content`: Success with no response body
- `400 Bad Request`: Invalid request parameters
- `401 Unauthorized`: Authentication failure
- `403 Forbidden`: Authorization failure
- `404 Not Found`: Resource not found
- `500 Internal Server Error`: Server-side error

## Swagger Documentation Standards

All APIs should be documented using Swagger annotations to ensure consistency and provide clear documentation.

### Controller Documentation

```typescript
import { Controller, Get } from '@nestjs/common'
import { ApiTags, ApiOperation, ApiResponse } from '@nestjs/swagger'

@ApiTags('products') // Tag group for the controller
@Controller('products')
export class ProductController {
  // Controller methods...
}
```

### Endpoint Documentation

```typescript
@ApiOperation({
  summary: 'Get product by ID',
  description: 'Retrieves detailed information about a specific product',
})
@ApiResponse({
  status: 200,
  description: 'Product found',
  type: ProductResponseDTO,
})
@ApiResponse({ status: 404, description: 'Product not found' })
@Get(':id')
async getProduct(@Param('id') id: string) {
  // Method implementation...
}
```

### DTO Documentation

```typescript
import { ApiProperty } from '@nestjs/swagger'

export class CreateProductDTO {
  @ApiProperty({
    description: 'The name of the product',
    example: 'Organic Cotton T-Shirt',
  })
  @IsString()
  @IsNotEmpty()
  name: string

  @ApiProperty({
    description: 'The product price in cents',
    example: 2500, // $25.00
  })
  @IsNumber()
  @IsPositive()
  price: number

  // Other properties...
}
```

### Common Documentation Practices

1. **Use ApiTags** to group endpoints in the Swagger UI
2. **Provide meaningful summaries and descriptions** for each endpoint
3. **Document all possible response status codes**
4. **Include examples** in ApiProperty decorators
5. **Document query parameters, path parameters, and body schemas**

## Error Handling

### Standard Error Response Format

```typescript
{
  "statusCode": 400,
  "message": ["Validation error: name should not be empty"]
}
```

### Validation

Use class-validator and class-transformer to validate request data:

```typescript
@Post()
async createProduct(@Body() createProductDto: CreateProductDTO) {
  // The DTO will be automatically validated based on class-validator annotations
}
```

## Security Guidelines

- Use appropriate Guards for authentication and authorization
- Use DTOs to validate and sanitize input data
- Never expose sensitive information in responses
- Implement rate limiting for public endpoints
- Use proper content security headers

## Versioning

When making breaking changes, version the API:

```typescript
@Controller('v2/products')
export class ProductV2Controller {
  // New controller methods...
}
```
