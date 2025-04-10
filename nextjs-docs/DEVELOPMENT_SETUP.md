# Development Environment Setup

This guide will help you set up your development environment for working on the HeyHomie Next.js application.

## Prerequisites

Before you begin, make sure you have the following installed:

- **Node.js** - Version 16.x or 18.x
  - We strongly recommend using [NVM (Node Version Manager)](https://github.com/nvm-sh/nvm) to manage your Node.js installations
  - Install NVM:

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    # or with wget
    wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    ```

  - Install and use the correct Node.js version:

    ```bash
    nvm install 18
    nvm use 18
    ```

- **Yarn** (required)
  - Our project requires Yarn as the package manager
  - Install Yarn globally:

    ```bash
    npm install -g yarn
    ```

  - Verify installation:

    ```bash
    yarn --version
    ```

## Step 1: Clone the Repository

```bash
git clone <repository-url>
cd heyhomie-next-app
```

## Step 2: Set up Environment Variables

1. Create a `.env` file in the root directory
2. Copy the contents from `.env.example` (if it exists) or ask a team member for the required environment variables
3. Update the values as needed for your local development

## Step 3: Install Dependencies

**You must use Yarn for this project:**

```bash
yarn install
```

## Step 4: Start the Development Server

```bash
yarn dev
```

The application will be available at [http://localhost:8083](http://localhost:8083).

## Step 5: Additional Tools Setup

### Code Editor Setup

We recommend using Visual Studio Code with the following extensions:

- ESLint
- Prettier
- TypeScript and JavaScript Language Features
- Material Icon Theme
- Auto Import

### VS Code Settings

Add these settings to your VS Code workspace settings:

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "typescript.tsdk": "node_modules/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true
}
```

## Git Workflow

See [GIT_GUIDE.md](GIT_GUIDE.md) for detailed information on our Git workflow.

## Available Scripts

- **`yarn dev`** - Start the development server
- **`yarn build`** - Build the application for production
- **`yarn start`** - Start the production server
- **`yarn lint`** - Run ESLint to check for code issues
- **`yarn lint:fix`** - Fix ESLint issues automatically
- **`yarn prettier`** - Format code with Prettier
- **`yarn ts`** - Run TypeScript type checking
- **`yarn ts:watch`** - Run TypeScript in watch mode
- **`yarn re:start`** - Clean, reinstall dependencies, and start development server
- **`yarn re:build`** - Clean, reinstall dependencies, and build for production

## Troubleshooting

### Common Issues

1. **Node version mismatch**
   - Use `nvm` to switch to the correct Node.js version:

     ```bash
     nvm use 18
     ```

2. **Port already in use**
   - Change the port in the `package.json` dev script or kill the process using the port
   - On Linux/Mac:

     ```bash
     lsof -i :8083
     kill -9 <PID>
     ```

   - On Windows:

     ```bash
     netstat -ano | findstr :8083
     taskkill /PID <PID> /F
     ```

3. **Module not found errors**
   - Try cleaning and reinstalling node_modules:

     ```bash
     yarn re:start
     ```

4. **TypeScript errors**
   - Run `yarn ts` to see detailed TypeScript errors

### Getting Help

If you encounter any issues that you cannot resolve, please reach out to the team for assistance.
