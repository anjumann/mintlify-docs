# Useful Commands

This document provides a reference of useful commands for working with the HeyHomie Next.js application.

## Project Setup

```bash
# Clone the repository
git clone <repository-url>
cd heyhomie-next-app

# Install dependencies with Yarn (recommended)
yarn install

# Install dependencies with npm
npm install --legacy-peer-deps
```

## Development

```bash
# Start development server
yarn dev
# or
npm run dev

# Start development server with TypeScript checking
yarn dev:ts
# or
npm run dev:ts
```

## Code Quality

```bash
# Run TypeScript type checking
yarn ts
# or
npm run ts

# Run TypeScript type checking in watch mode
yarn ts:watch
# or
npm run ts:watch

# Run ESLint
yarn lint
# or
npm run lint

# Fix ESLint issues
yarn lint:fix
# or
npm run lint:fix

# Format code with Prettier
yarn prettier
# or
npm run prettier

# Check types before commit
yarn check-types
# or
npm run check-types
```

## Building and Deployment

```bash
# Build for production
yarn build
# or
npm run build

# Start production server
yarn start
# or
npm run start

# Clean, reinstall dependencies, and start development
yarn re:start
# or
npm run re:start

# Clean, reinstall dependencies, and build for production
yarn re:build
# or
npm run re:build

# Clean, reinstall dependencies with npm, and build for production
yarn re:build-npm
# or
npm run re:build-npm
```

## Clean Up

```bash
# Remove all build artifacts and dependencies
yarn rm:all
# or
npm run rm:all
```

## Docker

```bash
# Build Docker image for development
docker build -t heyhomie-next-app .

# Build Docker image for production
docker build -f Dockerfile.prod -t heyhomie-next-app-prod .

# Run Docker container
docker run -p 8083:8083 heyhomie-next-app

# Run Docker container with environment variables
docker run -p 8083:8083 -e NEXT_PUBLIC_API_URL=<api-url> heyhomie-next-app
```

## Git

```bash
# Create a new branch
git checkout -b feature/feature-name

# Pull latest changes
git pull origin main

# Add all changes
git add .

# Commit changes
git commit -m "feat: description of the changes"

# Push changes
git push origin feature/feature-name

# Merge main into your branch
git merge main

# Resolve conflicts
git mergetool

# Squash commits
git rebase -i HEAD~<number-of-commits>
```

## Bundle Analysis

```bash
# Analyze bundle size
ANALYZE=true yarn build
# or
ANALYZE=true npm run build
```

## Environment Variables

```bash
# Create .env file
cp .env.example .env

# Edit .env file
nano .env
# or
code .env
```

## Troubleshooting

```bash
# Check Node.js version
node -v

# Check Yarn version
yarn -v

# Check npm version
npm -v

# Kill process using port 8083
lsof -i :8083
kill -9 <PID>
# or on Windows
netstat -ano | findstr :8083
taskkill /PID <PID> /F

# Clear npm cache
npm cache clean --force

# Clear yarn cache
yarn cache clean
```

## Testing

```bash
# Run tests (if configured)
yarn test
# or
npm run test

# Run tests in watch mode (if configured)
yarn test:watch
# or
npm run test:watch

# Run tests with coverage (if configured)
yarn test:coverage
# or
npm run test:coverage
```

## Performance Optimization

```bash
# Run Lighthouse audit
npx lighthouse https://localhost:8083 --view

# Check for unused dependencies
npx depcheck

# Find large dependencies
npx find-unused-dependencies
```

## Logging and Debugging

```bash
# Enable verbose logging in Next.js
NODE_OPTIONS='--inspect' yarn dev
# or
NODE_OPTIONS='--inspect' npm run dev

# Enable debug mode for SWR
localStorage.setItem('swr-debug', 'true')
```

## Common Git Workflow

```bash
# Start new feature
git checkout main
git pull
git checkout -b feature/new-feature

# Work on feature
# ... Make changes ...
git add .
git commit -m "feat: add new feature"

# Keep branch up to date with main
git fetch origin
git rebase origin/main

# Push feature and create PR
git push -u origin feature/new-feature

# After PR review, squash and merge in GitHub UI
# Then clean up
git checkout main
git pull
git branch -d feature/new-feature
```
