# HeyHomie Frontend Deployment

This guide outlines the deployment process for the HeyHomie Next.js frontend application.

## Deployment Environments

HeyHomie supports the following deployment environments:

- **Development**: For testing new features
- **Staging**: For pre-production verification
- **Production**: Live customer-facing environment

## Deployment Infrastructure

The application is deployed on Google Cloud Platform (GCP) using the following services:

- **Cloud Run**: For serverless container deployment
- **Cloud Storage**: For static assets
- **Cloud CDN**: For content delivery
- **Cloud Load Balancing**: For traffic distribution

## Deployment Process

### Prerequisites

Before deploying, ensure you have:

1. GCP account with appropriate permissions
2. Google Cloud SDK installed locally
3. Docker installed locally
4. Access to the HeyHomie container registry

### Deployment Steps

#### 1. Build the Application

```bash
yarn build
```

#### 2. Build and Tag the Docker Image

```bash
docker build -t gcr.io/heyhomie/frontend:latest .
```

#### 3. Push the Image to Container Registry

```bash
docker push gcr.io/heyhomie/frontend:latest
```

#### 4. Deploy to Cloud Run

```bash
gcloud run deploy heyhomie-frontend \
  --image gcr.io/heyhomie/frontend:latest \
  --platform managed \
  --region asia-south1 \
  --allow-unauthenticated
```

## Continuous Integration/Continuous Deployment (CI/CD)

The application uses GitHub Actions for CI/CD:

- **Pull Request**: Builds and tests the application
- **Merge to Main**: Deploys to Staging environment
- **Release Tag**: Deploys to Production environment

## Rollback Procedure

To rollback to a previous version:

1. Identify the previous stable version tag
2. Deploy that specific image version:

```bash
gcloud run deploy heyhomie-frontend \
  --image gcr.io/heyhomie/frontend:[VERSION_TAG] \
  --platform managed \
  --region asia-south1 \
  --allow-unauthenticated
```

## Environment Variables

The following environment variables must be configured in each environment:

- `NEXT_PUBLIC_API_URL`: Backend API URL
- `NEXT_PUBLIC_IMAGE_DOMAIN`: Image domain for Next.js Image optimization
- `NEXT_PUBLIC_GA_ID`: Google Analytics ID
- `NEXT_PUBLIC_RAZORPAY_KEY`: Razorpay public key

## Deployment Verification

After deployment, verify:

1. The application loads correctly
2. API endpoints are accessible
3. Authentication flows work
4. Core features function as expected

## Monitoring and Logging

- **Cloud Monitoring**: For system metrics and uptime
- **Cloud Logging**: For application logs
- **Error Reporting**: For tracking client-side errors

## Contact

<!-- For deployment issues, contact the DevOps team at devops@heyhomie.me. -->
