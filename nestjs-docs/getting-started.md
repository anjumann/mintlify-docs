# Getting Started with HeyHomie NestJS App

This guide will help you set up the HeyHomie NestJS application for local development.

## Prerequisites

- Node.js v20 or higher
- Yarn package manager
- PostgreSQL database
- ClickHouse database (for analytics)
- Redis (for caching and queue management)

## Setting Up Your Development Environment

### 1. Clone the Repository

```bash
git clone <repository-url>
cd heyhomie-nest-app
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

#### ClickHouse Setup

For ClickHouse, you can run it using Docker:

```bash
docker run -p 5521:5521 ghcr.io/caioricciuti/ch-ui:latest
```

#### Database Migrations

Run the database migrations to set up your schema:

```bash
yarn run dbmate:up
```

### 5. Starting the Application

For development with auto-reload:

```bash
yarn start:dev
```

For debugging:

```bash
yarn start:debug
```

For production mode:

```bash
yarn build
yarn start:prod
```

### 6. API Documentation

Once the application is running, you can access the Swagger API documentation at:

```bash
http://localhost:3000/api/system/docs
```

## Key Components

### Medusa Integration

The application integrates with Medusa commerce platform. If you're working with Medusa-related features, you'll need to:

1. Understand the Medusa API and data models
2. Configure Medusa-specific environment variables
3. Follow the Medusa region setup instructions in the project README

### Auth Module

Authentication is handled through the Auth module, supporting:

- Phone-based OTP authentication
- JWT tokens for session management
- User roles and permissions

### Working with the Codebase

- Each feature is organized into its own module in the `src/` directory
- Controllers handle API endpoints
- Services contain business logic
- DTOs define data transfer objects
- Entity files define database models

## Troubleshooting

### Common Issues

1. **Database Connection Issues**: Verify your PostgreSQL and ClickHouse connection details in the `.env` file.

2. **Redis Connection**: Ensure Redis is running and the connection details are correct.

3. **Medusa Integration**: If you're facing issues with Medusa integration, check the Medusa URL and authentication tokens.

## Getting Help

If you need assistance:

1. Check the documentation in the `docs/` folder
2. Review the codebase for examples of similar functionality
3. Reach out to the development team
