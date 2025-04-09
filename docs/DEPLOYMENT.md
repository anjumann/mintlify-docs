# Deployment Guide

This document provides instructions for deploying the HeyHomie Next.js application to different environments.

## Prerequisites

### Setting Up Google Cloud CLI

1. **Install Google Cloud CLI**:

   **For Debian/Ubuntu**:

   ```bash
   echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
   curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
   sudo apt-get update && sudo apt-get install google-cloud-sdk
   ```

   **For macOS**:

   ```bash
   brew install --cask google-cloud-sdk
   ```

   **For Windows**:
   Download the installer from <https://cloud.google.com/sdk/docs/install#windows>

2. **Initialize and Log In**:

   ```bash
   gcloud init
   gcloud auth login
   ```

3. **Set Project**:

   ```bash
   gcloud config set project heyhomie-project
   ```

## Deployment Environments

### Development Environment

The development environment is used for testing new features before they are promoted to production. All team members can deploy to this environment.

To deploy to the development environment:

```bash
./scripts/deploy.sh
```

This script will:

1. Build the application
2. Run unit tests
3. Package the application
4. Deploy to Google Cloud Run

You can monitor the deployment in the Google Cloud Console or using:

```bash
gcloud run services list
```

After deployment, the application will be available at: <https://dev.heyhomie.app>

### Production Environment

⚠️ **IMPORTANT**: Only senior team members should deploy to the production environment.

To deploy to production (restricted to senior developers):

```bash
./scripts/deploy-prod.sh
```

After deployment, the application will be available at: <https://app.heyhomie.com>

## Deployment Scripts

### deploy.sh

The `deploy.sh` script handles deployment to the development environment:

```bash
#!/bin/bash
set -e

echo "Building application..."
yarn build

echo "Running tests..."
yarn test

echo "Packaging application..."
docker build -t gcr.io/heyhomie-project/heyhomie-app:dev .

echo "Pushing Docker image..."
docker push gcr.io/heyhomie-project/heyhomie-app:dev

echo "Deploying to development environment..."
gcloud run deploy heyhomie-app-dev \
  --image gcr.io/heyhomie-project/heyhomie-app:dev \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated

echo "Deployment complete! Application is available at:"
gcloud run services describe heyhomie-app-dev --platform managed --region us-central1 --format='value(status.url)'
```

### deploy-prod.sh

The `deploy-prod.sh` script handles deployment to the production environment:

```bash
#!/bin/bash
set -e

# This script is restricted to senior team members

echo "Building application for production..."
yarn build

echo "Running tests..."
yarn test

echo "Packaging application..."
docker build -f Dockerfile.prod -t gcr.io/heyhomie-project/heyhomie-app:prod .

echo "Pushing Docker image..."
docker push gcr.io/heyhomie-project/heyhomie-app:prod

echo "Deploying to production environment..."
gcloud run deploy heyhomie-app-prod \
  --image gcr.io/heyhomie-project/heyhomie-app:prod \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated

echo "Deployment complete! Application is available at:"
gcloud run services describe heyhomie-app-prod --platform managed --region us-central1 --format='value(status.url)'
```

## Monitoring Deployments

### Viewing Deployment History

To view deployment history:

```bash
gcloud run revisions list --service heyhomie-app-dev --platform managed --region us-central1
```

### Rollback to Previous Version

If issues are detected after deployment, you can roll back to a previous version:

```bash
gcloud run services update-traffic heyhomie-app-dev --to-revisions=REVISION_ID=100 --platform managed --region us-central1
```

Replace `REVISION_ID` with the ID of the revision you want to roll back to.

## Environment Variables

The deployment scripts use environment variables defined in Google Cloud Run. These are sourced from the `.env.development` and `.env.production` files for the respective environments.

To add or update environment variables:

```bash
gcloud run services update heyhomie-app-dev --set-env-vars KEY=VALUE --platform managed --region us-central1
```

## Deployment Best Practices

1. **Always Test Locally First**: Ensure your changes work locally before deploying
2. **Deploy to Development First**: Always test in the development environment before production
3. **Check Logs After Deployment**: Verify logs for any errors after deployment
4. **Perform Smoke Tests**: Validate critical functionality after deployment
5. **Be Ready to Rollback**: Know how to quickly rollback if issues are detected
6. **Deploy During Low-Traffic Periods**: Schedule production deployments during low-traffic periods
7. **Communicate Deployments**: Inform the team before and after deployments
8. **Monitor Performance**: Watch for performance degradation after deployment

## Troubleshooting

### Common Deployment Issues

1. **Build Failures**:
   - Check for TypeScript errors
   - Verify all dependencies are correctly installed

2. **Docker Build Issues**:
   - Ensure Docker is running
   - Verify Dockerfile syntax

3. **Deployment Failures**:
   - Check Google Cloud permissions
   - Verify Google Cloud service account configuration

4. **Post-Deployment Issues**:
   - Check application logs:

     ```bash
     gcloud logging read "resource.type=cloud_run_revision AND resource.labels.service_name=heyhomie-app-dev" --limit=10
     ```

## Continuous Integration/Continuous Deployment (CI/CD)

For automated deployments, we use GitHub Actions. The workflow files are located in `.github/workflows/`:

- `dev-deploy.yml`: Triggers deployment to the development environment on pushes to the `develop` branch
- `prod-deploy.yml`: Triggers deployment to the production environment on pushes to the `main` branch (requires approval)
