# Getting Started with HeyHomie Backend

This guide will help you set up the HeyHomie NestJS backend application for local development.

## Prerequisites

- **Node.js**: v20 or higher
- **Yarn**: Package manager
- **PostgreSQL**: Database (v15 recommended)
- **ClickHouse**: Analytics database
- **Redis**: For caching and queue management
- **Docker**: For containerized services (optional but recommended)

## Setting Up Your Development Environment

### 1. Clone the Repository

```bash
git clone https://github.com/heyhomie/backend.git
cd backend
```

### 2. Install Dependencies

```bash
yarn install
```

### 3. Configure Environment Variables

Copy the provided `.env.example` file to create your own `.env` file:

```bash
cp .env.example .env
```

Configure the variables in the `.env` file based on your local setup.

### 4. Database Setup

#### PostgreSQL

Ensure PostgreSQL is running locally or accessible through the configured connection details in your `.env` file.

To create the database:

```bash
createdb heyhomie_dev
```

#### ClickHouse Setup

For ClickHouse, you can run it using Docker:

```bash
docker run -d --name clickhouse-server -p 8123:8123 -p 9000:9000 clickhouse/clickhouse-server
```

#### Redis Setup

For Redis, you can run it using Docker:

```bash
docker run -d --name redis -p 6379:6379 redis
```

#### Database Migrations

Run the database migrations to set up your schema:

```bash
yarn migration:run
```

### 5. Starting the Application

#### Development Mode (with auto-reload)

```bash
yarn start:dev
```

#### Debug Mode

```bash
yarn start:debug
```

#### Production Mode

```bash
yarn build
yarn start:prod
```

## Accessing the Application

Once running, the application will be available at:

- **API**: [http://localhost:3000/api](http://localhost:3000/api)
- **API Documentation**: [http://localhost:3000/api/system/docs](http://localhost:3000/api/system/docs)

## Project Structure

The application follows a modular structure:

```
src/
├── ads/              # Advertisement related features
├── analytics/        # Analytics and tracking features
├── auth/             # Authentication and authorization
├── collection/       # Product collections
├── common/           # Shared utilities and services
├── cron/             # Scheduled tasks
├── discount/         # Discount and promotion features
├── dropship/         # Dropshipping functionality
├── lib/              # Core library code
├── messaging/        # Communication services
├── orders/           # Order management
├── payments/         # Payment processing
├── product/          # Product management
├── review/           # Product reviews
├── shipping/         # Shipping services
├── store/            # Store management
├── types/            # TypeScript type definitions
├── upload/           # File upload services
├── webhook/          # Webhook handling
├── app.module.ts     # Main application module
└── main.ts           # Application entry point
```

## Key Components and Services

### Medusa Integration

The application integrates with Medusa commerce platform. For working with Medusa-related features:

1. Review the Medusa API documentation
2. Understand how Medusa entities are mapped to HeyHomie models
3. Configure Medusa-specific environment variables

### Authentication

Authentication is handled through the Auth module, supporting:

- Phone-based OTP authentication
- JWT tokens for session management
- User roles and permissions

## Development Workflow

1. Create a feature branch from `main`
2. Implement your changes following the code standards
3. Write unit tests for your code
4. Submit a pull request for code review

## Troubleshooting

### Common Issues

1. **Database Connection Issues**: 
   - Verify PostgreSQL and ClickHouse connection details in `.env`
   - Check that the databases are running and accessible

2. **Redis Connection**: 
   - Ensure Redis is running and connection details are correct

3. **Medusa Integration**: 
   - If facing issues with Medusa integration, check Medusa URL and authentication tokens

## Getting Help

If you need assistance:

1. Check the documentation in the `docs/` folder
2. Review the codebase for examples of similar functionality
3. Reach out to the development team through Slack
