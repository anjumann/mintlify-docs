# HeyHomie Deployment Guide

This document provides instructions for deploying the HeyHomie Next.js application to different environments.

## Deployment Environments

HeyHomie supports the following deployment environments:

- **Development**: For testing new features
- **Staging**: For pre-production verification
- **Production**: Live customer-facing environment

## Deployment Prerequisites

Before deployment, ensure you have:

1. Access to the HeyHomie GitHub repository
2. Docker installed locally (for testing container builds)
3. Access to the Google Cloud Platform console
4. Google Cloud SDK installed (for manual deployments)

## CI/CD Pipeline

The application uses GitHub Actions for continuous integration and deployment:

- **Pull Request**: Runs tests and linting
- **Merge to Development**: Builds and deploys to development environment
- **Merge to Main**: Builds and deploys to staging environment
- **Release Creation**: Deploys to production environment

## Manual Deployment

If you need to deploy manually:

```bash
# 1. Build the application
yarn build

# 2. Create Docker image
docker build -t gcr.io/heyhomie-project/frontend:latest .

# 3. Push to Google Container Registry
docker push gcr.io/heyhomie-project/frontend:latest

# 4. Deploy to Cloud Run
gcloud run deploy heyhomie-frontend \
  --image gcr.io/heyhomie-project/frontend:latest \
  --platform managed \
  --region asia-south1 \
  --allow-unauthenticated
```

## Rollback Procedure

To rollback to a previous version:

1. Go to Google Cloud Console > Cloud Run
2. Select the service (heyhomie-frontend)
3. Click "REVISIONS"
4. Find the stable revision you want to rollback to
5. Click "..." and select "Serve traffic"

Alternatively, use the gcloud command:

```bash
gcloud run services update-traffic heyhomie-frontend \
  --to-revisions=REVISION_ID=100 \
  --platform managed \
  --region asia-south1
```

## Environment Variables

Configure the following environment variables in your deployment:

- `NEXT_PUBLIC_API_URL`: Backend API endpoint
- `NEXT_PUBLIC_GA_ID`: Google Analytics ID
- `NEXT_PUBLIC_RAZORPAY_KEY`: Razorpay public key ID

## Post-Deployment Verification

After each deployment, verify:

1. Application loads without errors
2. Core functionality works properly
3. API integrations are functioning
4. Authentication flows work as expected

## Troubleshooting

Common issues:

1. **Deployment Failures**
   - Check build logs in GitHub Actions
   - Verify container registry permissions
   - Check Cloud Run service account permissions

2. **Runtime Errors**
   - Check Cloud Run logs
   - Verify environment variables are set correctly
   - Check API endpoint connectivity

## Deployment Schedule

- Development: As needed for feature testing
- Staging: Weekly releases (Thursdays)
- Production: Biweekly releases (alternate Mondays)

## Contact
