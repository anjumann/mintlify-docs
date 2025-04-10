# HeyHomie Frontend Development Setup

This guide will walk you through setting up the HeyHomie Next.js frontend application for local development.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js**: v18 or later
- **Yarn**: Package manager (v1.22.x or later)
- **Git**: Version control

## Setting Up Your Development Environment

### 1. Clone the Repository

```bash
git clone https://github.com/heyhomie/frontend.git
cd frontend
```

### 2. Install Dependencies

```bash
yarn install
```

### 3. Set Up Environment Variables

Copy the template environment file to create your local environment configuration:

```bash
cp .env.example .env.local
```

Edit `.env.local` to configure:
- API endpoint URLs
- Razorpay settings
- Other environment-specific settings

### 4. Start the Development Server

```bash
yarn dev
```

This will start the development server on `http://localhost:3000`.

## Project Structure

The HeyHomie frontend follows a feature-based folder structure:

```
src/
├── components/          # Reusable UI components
│   ├── common/          # Common components used across features
│   ├── layouts/         # Layout components
│   └── [feature]/       # Feature-specific components
├── hooks/               # Custom React hooks
├── pages/               # Next.js pages and API routes
├── services/            # API services and external integrations
├── store/               # State management
├── styles/              # Global styles and Tailwind configuration
├── types/               # TypeScript type definitions
└── utils/               # Utility functions
```

## Development Workflow

1. **Create a Feature Branch**: Create a branch from `main` for your feature or fix
2. **Implement Changes**: Develop your feature or fix
3. **Run Tests**: Ensure your changes pass all tests
4. **Create a Pull Request**: Submit a PR to merge your changes into `main`

## Common Development Tasks

### Adding a New Page

1. Create a new file in `pages/` directory or a subdirectory
2. Use appropriate layout components
3. Connect to API services as needed

### Creating a Reusable Component

1. Add component in the appropriate directory under `components/`
2. Include PropTypes or TypeScript interfaces
3. Add tests if needed

### Connecting to Backend API

1. Use the API client from `utils/axios.ts`
2. Create service functions in the appropriate file under `services/`
3. Use SWR for data fetching when appropriate

## Troubleshooting

### Common Issues

**Build Error: Module Not Found**
- Check that all dependencies are installed correctly
- Ensure import paths are correct (case sensitivity matters)

**API Connection Issues**
- Verify that your `.env.local` contains the correct API URLs
- Check that the backend server is running and accessible

## Getting Help

If you encounter issues or have questions, please:

1. Check the existing documentation
2. Ask in the #frontend Slack channel
3. Contact the development team lead
