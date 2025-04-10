# HeyHomie NestJS Architecture

## Overview

The HeyHomie NestJS application is built as a microservices-oriented backend for an e-commerce platform, integrating with Medusa commerce, payment providers, and various third-party services.

## Core Architecture

### Module Structure

The application follows NestJS's modular architecture with a feature-based organization:

```bash
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

### Database Structure

The application uses:

- **PostgreSQL**: Main relational database for transactional data
- **ClickHouse**: For analytical queries and event storage
- **Redis**: For caching and queue management

## Integration Points

### Medusa Commerce

The application integrates with Medusa for core e-commerce functionality:

- Products and inventory management
- Orders and fulfillment
- Customer management

### Payment Systems

- **Razorpay**: Primary payment processor with full integration

### Third-Party Services

- **Facebook/Instagram**: For social commerce integration
- **ShipRocket**: For shipping and fulfillment
- **Gumlet**: For image processing and optimization

## Data Flow

1. API requests come through NestJS controllers
2. Services process business logic
3. Data is stored in PostgreSQL or ClickHouse
4. External service integrations are handled through dedicated modules

## System Architecture Diagram

```bash
┌─────────────────┐     ┌───────────────┐     ┌────────────────┐
│  Client Apps    │────▶│  NestJS API   │────▶│  Core Services │
└─────────────────┘     └───────┬───────┘     └────────┬───────┘
                                │                       │
                                ▼                       ▼
                        ┌───────────────┐     ┌────────────────┐
                        │   Database    │     │ External APIs  │
                        │  PostgreSQL   │     │   - Medusa     │
                        │  ClickHouse   │     │   - Razorpay   │
                        │    Redis      │     │   - ShipRocket │
                        └───────────────┘     └────────────────┘
```

## Key Design Decisions

1. **Feature-based Module Organization**: Each business domain has its own module with controllers, services, and DTOs
2. **Separation of Database Logic**: DB services are separated from business logic services
3. **Environment-based Configuration**: Using environment variables for flexible deployment
4. **Error Handling Strategy**: Custom exception filters with detailed error messages
5. **Medusa Integration Approach**: Using Medusa as a commerce engine while extending its functionality
