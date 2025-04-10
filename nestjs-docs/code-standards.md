# Code Standards and Best Practices

This document outlines the coding standards and best practices to follow when developing for the HeyHomie NestJS application.

## TypeScript Standards

```typescript
// Configuration
typescript.target = "ES2021"
typescript.strictNullChecks = true
typescript.noImplicitAny = true
typescript.useDecorators = true
typescript.includeNullChecks = true
typescript.emitDecoratorMetadata = true
typescript.experimentalDecorators = true
typescript.allowSyntheticDefaultImports = true
```

## Naming Conventions

- **camelCase** for:
  - Variables
  - Functions
  - Methods
  - Properties

- **PascalCase** for:
  - Classes
  - Interfaces
  - Types
  - Decorators
  - Enums

- **UPPER_CASE** for:
  - Constants

- **No prefix conventions** for interfaces (e.g., no 'I' prefix)

## Code Structure

### Import Organization

- Group and order imports:
  1. NestJS packages
  2. External packages
  3. Relative imports

```typescript
// NestJS imports
import { Controller, Get, Post, Body } from '@nestjs/common'
import { ApiTags, ApiOperation } from '@nestjs/swagger'

// External package imports
import { ulid } from 'ulid'
import * as _ from 'lodash'

// Relative imports
import { ProductService } from './product.service'
import { CreateProductDTO } from './dto/create-product.dto'
```

- Prefer named imports over default imports
- Use relative paths for imports within the same module

## NestJS Specific Guidelines

- Use controller decorators as specified by NestJS
- Use ValidationPipe globally
- Organize by feature rather than by layer
- Follow module organization pattern:
  1. Controllers
  2. Providers
  3. Imports
  4. Exports
- Implement Swagger annotations for API documentation

## Code Formatting

- Use single quotes for strings
- Include trailing commas in multiline lists
- Omit semicolons
- Set print width to 100 characters
- Use Prettier for consistent formatting

```typescript
// Example of preferred formatting
const userData = {
  name: 'John Doe',
  roles: [
    'admin',
    'user',
  ],
  active: true,
}
```

## API Design

- Use Data Transfer Objects (DTOs) for request and response data
- Implement validation using class-validator
- Include Swagger documentation for all endpoints
- Follow RESTful API design principles

## File Structure

Each module should follow this file structure pattern:

```bash
{name}.module.ts
{name}.controller.ts
{name}.service.ts
{name}.db.service.ts
dto/*.dto.ts
models/*.ts
strategy/*.strategy.ts
```

## Error Handling

- Use custom exceptions
- Implement global exception filters
- Include detailed error messages
- Use HTTP exceptions with appropriate status codes
- Check for previous exceptions to avoid duplicate error handling
- Log error details for monitoring

## Database Guidelines

- Use TypeORM as the ORM
- Name entity files as `{name}.entity.ts`
- Implement database migrations for schema changes
- Use snake_case for database column names

## Environment Configuration

- Use environment service for accessing environment variables
- Validate environment variables at startup
- Use typed environment variables where possible

## Asynchronous Operations

- Use Promise.all for parallel operations
- Handle parallel requests efficiently
- Use Promise.allSettled for operations that can partially fail
- Use async/await with map for sequential asynchronous operations
- Avoid nested callbacks

## Medusa Integration

- Separate admin functionality from store functionality
- Use axios instances for consistent headers
- Handle Medusa-specific errors appropriately
- Standardize headers based on token
- Map data to Medusa-expected format

## Code Organization

- Separate database logic from business logic
- Create utility functions for reusable operations
- Organize code by domain/feature
- Follow single responsibility principle
- Extract complex logic to dedicated services
- Create reusable helpers for common operations
