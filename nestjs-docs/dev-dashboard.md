# Developer Dashboard

This document serves as a central hub for developers working on the HeyHomie NestJS application, providing quick links to essential resources and tools.

## Key Resources

### Documentation

| Resource | Description | Link |
|----------|-------------|------|
| Architecture | Architecture overview and design decisions | [architecture.md](./architecture.md) |
| Getting Started | Setup guide for new developers | [getting-started.md](./getting-started.md) |
| API Guidelines | Standards for API development | [api-guidelines.md](./api-guidelines.md) |
| Integrations | Third-party service integrations | [integrations.md](./integrations.md) |
| Code Standards | Coding standards and best practices | [code-standards.md](./code-standards.md) |
| Project README | Main project documentation | [../README.md](../README.md) |

### Development Tools

| Tool | Purpose | URL/Command |
|------|---------|-------------|
| Swagger UI | API Documentation | `http://localhost:3000/api/system/docs` |
| Bull Dashboard | Queue Management | `http://localhost:3000/queues` |
| ClickHouse UI | Analytics Database UI | `http://localhost:5521` |
| Database Migrations | Manage DB schema | `yarn run dbmate:{command}` |

## Common Commands

### Development

```bash
# Start development server
yarn start:dev

# Start with debugging
yarn start:debug

# Build for production
yarn build

# Run linting
yarn lint

# Run tests
yarn test
```

### Database Operations

```bash
# Create new migration
yarn run dbmate:new migration_name

# Run migrations
yarn run dbmate:up

# Rollback migrations
yarn run dbmate:down

# Check migration status
yarn run dbmate:status
```

## Modules Overview

| Module | Description | Key Files |
|--------|-------------|-----------|
| Auth | User authentication and authorization | `src/auth/` |
| Products | Product management | `src/product/` |
| Orders | Order processing | `src/orders/` |
| Payments | Payment processing | `src/payments/` |
| Analytics | User and system analytics | `src/analytics/` |
| Common | Shared utilities and services | `src/common/` |

## Environment Variables

Key environment variables required for development:

```bash
PORT=3000
POSTGRES_DB_NAME=heyhomie
POSTGRES_WRITER_URL=localhost
POSTGRES_READER_URL=localhost
POSTGRES_USERNAME=postgres
POSTGRES_DB_PASSWORD=your_password
REDIS_HOST=localhost
REDIS_PASSWORD=your_redis_password
MEDUSA_URL=http://localhost:9000
```

See `.env.example` for a complete list.

## API Endpoints

| Endpoint | Description |
|----------|-------------|
| `/api/auth` | Authentication endpoints |
| `/api/product` | Product management endpoints |
| `/api/orders` | Order management endpoints |
| `/api/payments` | Payment processing endpoints |
| `/api/collection` | Collection management endpoints |
| `/api/system/docs` | Swagger API documentation |
| `/queues` | Bull dashboard for queue management |

## Debugging Tips

1. Use the built-in debugging with `yarn start:debug`
2. Check logs in the console for detailed information
3. Use Swagger UI to test API endpoints
4. Monitor queue status using the Bull dashboard
5. Verify database migrations using the `dbmate:status` command

## Contribution Workflow

1. Create a feature branch from main
2. Implement changes following the code standards
3. Write tests for your changes
4. Update documentation if necessary
5. Submit a pull request

## Getting Help

If you encounter issues or need assistance:

1. Review the documentation in this dashboard
2. Check existing code for similar implementations
3. Discuss with the team on the project communication channels
4. Review logs and error messages for troubleshooting
