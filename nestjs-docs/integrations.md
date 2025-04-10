# Third-Party Integrations

This document provides details about the third-party services integrated with the HeyHomie NestJS application.

## Medusa Commerce

### Medusa Overview

Medusa is the core e-commerce engine used for product management, cart functionality, order processing, and customer management.

### Medusa Integration Details

- **Integration Type**: Direct API integration
- **Configuration**: Environment variables for Medusa URL and credentials
- **Key Functionality**:
  - Product management
  - Order processing
  - Cart management
  - Customer handling

### Medusa Setup Requirements

Follow the Medusa region setup instructions in the main README.md file to configure:

1. Currency (INR)
2. Region (India)
3. Payment providers
4. Shipping options

## Razorpay

### Razorpay Overview

Razorpay is used as the primary payment processor for the application.

### Razorpay Integration Details

- **Integration Type**: API with NestJS module
- **Configuration**:

  ```typescript
  RazorpayModule.forRoot({
    key_id: Environments.get('RAZORPAY_ID'),
    key_secret: Environments.get('RAZORPAY_KEY'),
  })
  ```

- **Key Functionality**:
  - Payment processing
  - Payment status verification
  - Refund handling

### Razorpay Setup Requirements

1. Create a Razorpay account
2. Configure Razorpay API keys in the environment variables
3. Set up webhook endpoints for payment events

## ShipRocket

### ShipRocket Overview

ShipRocket is used for shipping and logistics management.

### ShipRocket Integration Details

- **Integration Type**: API integration
- **Configuration**: Environment variables for ShipRocket email and password
- **Key Functionality**:
  - Shipping rate calculation
  - Order fulfillment
  - Shipping label generation
  - Shipment tracking

### ShipRocket Setup Requirements

1. Create a ShipRocket account
2. Configure ShipRocket credentials in environment variables
3. Set up shipping options as described in the README

## Facebook/Instagram

### Facebook/Instagram Overview

Facebook and Instagram integration for social commerce and messaging.

### Facebook/Instagram Integration Details

- **Integration Type**: OAuth and API integration
- **Configuration**: App ID, Secret, and Bearer Token in environment variables
- **Key Functionality**:
  - Login with Facebook
  - Message handling
  - Webhook processing

### Facebook/Instagram Setup Requirements

1. Create a Facebook Developer account
2. Set up a Facebook App with appropriate permissions
3. Configure webhook endpoints
4. Add Facebook App ID and Secret to environment variables

## Gumlet

### Gumlet Overview

Gumlet is used for image processing and optimization.

### Gumlet Integration Details

- **Integration Type**: API integration
- **Configuration**: API key and collection ID in environment variables
- **Key Functionality**:
  - Image uploading
  - Image optimization
  - Image transformation

### Gumlet Setup Requirements

1. Create a Gumlet account
2. Configure API keys in environment variables

## ClickHouse

### ClickHouse Overview

ClickHouse is used for analytics and event data storage.

### ClickHouse Integration Details

- **Integration Type**: Direct database connection
- **Configuration**: URL, username, and password in environment variables
- **Key Functionality**:
  - Event storage
  - Analytics queries
  - Performance metrics

### ClickHouse Setup Requirements

1. Set up ClickHouse database
2. Configure connection details in environment variables
3. Run database migrations

## Redis

### Redis Overview

Redis is used for caching, session management, and queue handling.

### Redis Integration Details

- **Integration Type**: Direct connection and Bull queue integration
- **Configuration**:

  ```typescript
  BullModule.forRoot({
    redis: {
      host: Environments.get('REDIS_HOST'),
      password: Environments.get('REDIS_PASSWORD'),
    },
  })
  ```

- **Key Functionality**:
  - Job queues with Bull
  - Caching
  - Session storage

### Redis Setup Requirements

1. Set up Redis server
2. Configure connection details in environment variables
