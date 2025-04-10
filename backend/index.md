# HeyHomie Backend Documentation

Welcome to the HeyHomie NestJS backend documentation. This documentation provides comprehensive information about the backend architecture, API standards, and development workflows.

## Backend Documentation

1. [Getting Started](getting-started.md) - Setup and run the backend application
2. [Architecture](architecture.md) - Backend architecture overview
3. [API Guidelines](api-guidelines.md) - Standards for API development
4. [Code Standards](code-standards.md) - Backend coding standards
5. [Integrations](integrations.md) - Third-party integrations

## API Documentation

The complete API documentation is available through Swagger UI:
[HeyHomie API Documentation](https://heyhomie.me/api/system/docs)

## Key Backend Features

- **User Authentication**: Phone-based OTP and JWT
- **Product Management**: Integrated with Medusa commerce
- **Order Processing**: Complete order lifecycle management
- **Payment Integration**: Razorpay integration
- **Shipping**: ShipRocket integration for logistics
- **Analytics**: ClickHouse for advanced analytics

## Technology Stack

- **Framework**: NestJS
- **Language**: TypeScript
- **Databases**: 
  - PostgreSQL (primary database)
  - ClickHouse (analytics)
  - Redis (caching and queues)
- **Integrations**:
  - Medusa Commerce
  - Razorpay
  - ShipRocket
  - Facebook/Instagram

## Development Workflow

1. Review the [Getting Started](getting-started.md) guide
2. Understand the [Architecture](architecture.md)
3. Follow the [API Guidelines](api-guidelines.md) when developing endpoints
4. Adhere to [Code Standards](code-standards.md) for consistency

## Common Tasks

- **Adding a new API endpoint**: Follow the RESTful design principles in the API Guidelines
- **Database migrations**: Use dbmate for schema changes
- **Third-party integration**: Check the Integrations document for patterns

## Getting Help

For questions about the backend development, please contact the HeyHomie development team. 