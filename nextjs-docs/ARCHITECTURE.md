# HeyHomie Application Architecture

This document outlines the architecture and key technical decisions of the HeyHomie Next.js application.

## Overview

HeyHomie is a Next.js application built with TypeScript and Material UI. It follows a feature-based organization pattern where code is grouped by feature rather than by type.

## Architectural Layers

### 1. UI Layer

The UI layer is built with React components, organized in the following hierarchy:

- **Layouts** (`src/components/layouts`) - Define the overall page structure
- **Pages** (`src/app/**`) - Next.js App Router pages
- **Components** (`src/components/**`) - Reusable UI components
- **Theme** (`src/theme`) - Material UI theme customization

### 2. Application Layer

The application layer handles business logic and state management:

- **Hooks** (`src/hooks`) - Custom React hooks for shared logic
- **Context** (Various context providers) - For state management
- **Form Logic** (Using React Hook Form) - For form handling and validation

### 3. Data Layer

The data layer is responsible for data fetching and persistence:

- **API Clients** (`src/api`) - API service clients
- **SWR Hooks** - For data fetching, caching, and revalidation
- **Axios Configuration** (`src/utils/axios.ts`) - HTTP client setup

## Key Patterns

### Routing

The application uses Next.js App Router for routing, with route definitions centralized in `src/routes/paths.ts`.

### State Management

State management is primarily handled through:

- React Context for global state
- SWR for server state
- Local component state for UI state

### Data Fetching

The application uses SWR for data fetching, providing:

- Automatic revalidation
- Caching
- Optimistic updates
- Error handling

### Authentication

Authentication flows are handled in the `src/auth` directory, with protected routes and role-based access control.

### Error Handling

Error handling is implemented through:

- Sentry for error tracking and monitoring
- Custom error boundaries
- SWR error states for API errors

## Directory Structure Explained

```bash
src/
├── app/                   # Next.js pages using App Router
│   ├── dashboard/         # Dashboard pages
│   ├── auth/              # Authentication pages
│   └── [other routes]/    # Other application routes
├── api/                   # API clients
├── assets/                # Static assets
├── auth/                  # Authentication logic
├── components/            # Shared UI components
│   ├── animate/           # Animation components
│   ├── carousel/          # Carousel components
│   ├── chart/             # Chart components
│   ├── hook-form/         # Form components
│   ├── layouts/           # Layout components
│   └── [other components]/
├── dashboard/             # Dashboard specific components
├── hooks/                 # Custom React hooks
├── lib/                   # Utility libraries
├── routes/                # Routing definitions
├── theme/                 # Material UI theme
│   ├── customShadows.ts   # Custom shadow definitions
│   ├── index.ts           # Theme export
│   ├── options/           # Theme options
│   └── palette.ts         # Color palette
├── types/                 # TypeScript type definitions
└── utils/                 # Utility functions
    ├── axios.ts           # Axios configuration
    ├── format-*.ts        # Formatting utilities
    └── [other utils]/
```

## Design Decisions

### 1. Next.js and TypeScript

- **Why Next.js**: Server-side rendering, static site generation, file-based routing, API routes
- **Why TypeScript**: Type safety, better developer experience, easier refactoring

### 2. Material UI

- **Why Material UI**: Comprehensive component library, customizable theming, responsive design

### 3. SWR for Data Fetching

- **Why SWR**: Simple API, built-in caching, revalidation, optimistic updates

### 4. Feature-based Organization

- **Why Feature-based**: Better code co-location, easier navigation, improved encapsulation

### 5. React Hook Form + Yup

- **Why React Hook Form**: Performance, uncontrolled inputs, easy validation
- **Why Yup**: Schema-based validation, TypeScript integration

## Development Workflow

1. **Local Development**: `yarn dev` starts the development server
2. **Type Checking**: `yarn ts` checks TypeScript types
3. **Linting**: `yarn lint` runs ESLint
4. **Formatting**: `yarn prettier` formats code with Prettier
5. **Building**: `yarn build` builds for production
6. **Deployment**: Docker-based deployment with `Dockerfile` or `Dockerfile.prod`

## Performance Considerations

- Code splitting via dynamic imports
- Image optimization with Next.js Image component
- Bundle size optimization with `@next/bundle-analyzer`
- Server-side rendering for improved initial load
- Memoization for expensive calculations

## Security Considerations

- Authentication and authorization
- Environment variables for sensitive data
- Input validation
- HTTPS enforcement
- Content Security Policy

## Monitoring and Debugging

- Sentry for error tracking
- Custom logging
- Performance monitoring

## Extending the Application

When extending the application:

1. Follow the existing pattern for the feature type
2. Reuse existing components when possible
3. Add new routes to `src/routes/paths.ts`
4. Add new API clients to `src/api/`
5. Update types as needed in `src/types/`
