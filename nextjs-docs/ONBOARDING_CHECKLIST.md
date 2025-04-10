# Developer Onboarding Checklist

Welcome to the HeyHomie Next.js application development team! This checklist will guide you through the process of getting up to speed and becoming productive.

## Day 1: Environment Setup & Orientation

- [ ] Get access to the code repository
- [ ] Set up local development environment using [DEVELOPMENT_SETUP.md](DEVELOPMENT_SETUP.md)
- [ ] Configure your editor with recommended extensions and settings
- [ ] Run the application locally
- [ ] Install and configure Git hooks using Husky
- [ ] Review the project README and documentation
- [ ] Attend project introduction meeting with your mentor

## Day 2: Codebase Exploration

- [ ] Read through [ARCHITECTURE.md](ARCHITECTURE.md) to understand the project structure
- [ ] Review [CODE_CONVENTIONS.md](CODE_CONVENTIONS.md) to understand coding standards
- [ ] Explore the directory structure and understand feature organization
- [ ] Review existing components in `src/components`
- [ ] Review the routing structure in `src/routes/paths.ts`
- [ ] Understand the authentication flow in `src/auth`
- [ ] Review how API calls work using [API_GUIDE.md](API_GUIDE.md)

## Day 3: Deeper Understanding

- [ ] Understand Material UI theme customization in `src/theme`
- [ ] Review common UI components and their usage patterns
- [ ] Understand how SWR is used for data fetching
- [ ] Review how forms are handled with React Hook Form
- [ ] Explore state management patterns across the application
- [ ] Practice creating a simple component following established patterns
- [ ] Set up the deployment workflow with [Google Cloud CLI](#day-5-deployment-workflow)

## Day 4: First Task & Code Review

- [ ] Complete a simple bugfix or small enhancement (assigned by your mentor)
- [ ] Apply the Git workflow from [GIT_GUIDE.md](GIT_GUIDE.md)
- [ ] Write clean, well-documented code following our conventions
- [ ] Create a pull request following the project's workflow
- [ ] Participate in your first code review
- [ ] Incorporate feedback and improve your code
- [ ] Meet with your mentor to discuss progress and questions

## Day 5: Deployment Workflow

- [ ] Install Google Cloud CLI:

  ```bash
  # For Debian/Ubuntu
  echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
  sudo apt-get update && sudo apt-get install google-cloud-sdk

  # For macOS
  brew install --cask google-cloud-sdk
  ```

- [ ] Login to Google Cloud:

  ```bash
  gcloud auth login
  ```

- [ ] Deploy to development environment:

  ```bash
  ./scripts/deploy.sh
  ```

  > ⚠️ **IMPORTANT**: Only senior team members should deploy to production using other deployment scripts

- [ ] Monitor deployment in Google Cloud Console
- [ ] Verify your deployment in the development environment

## Learning Resources

### General Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [Material UI Documentation](https://mui.com/material-ui/getting-started/overview/)

### Project-Specific Resources

- [Project Technical Documentation](ARCHITECTURE.md)
- [Component Development Guide](COMPONENT_GUIDE.md)
- [API Integration Guide](API_GUIDE.md)
- [Code Conventions](CODE_CONVENTIONS.md)
- [Git Guide](GIT_GUIDE.md)

## Getting Help

- **Code Questions**: Reach out to the team through the development chat
- **Process Questions**: Ask your assigned mentor or team lead
- **Technical Issues**: Create a support ticket in the project management system

## Common Pain Points and Solutions

### Problem: Module not found errors

**Solution**: Make sure you've installed all dependencies and that import paths are correct. Check for typos in import statements.

### Problem: TypeScript errors

**Solution**: Run `yarn ts` to see detailed error messages. Ensure that your types are properly defined and imported.

### Problem: Component styling inconsistencies

**Solution**: Follow the styling guidelines in the COMPONENT_GUIDE.md document and use theme values for consistent styling.

### Problem: API calls not working

**Solution**: Check that the API endpoints are correct and that you're handling authentication properly. Console.log the request and response for debugging.

## Next Steps After Onboarding

As you become more comfortable with the codebase, start exploring these areas:

1. **Performance Optimization**: Look for ways to optimize component rendering and data fetching
2. **Accessibility**: Ensure that all components are accessible to users with disabilities
3. **Testing**: Improve test coverage and learn about testing patterns
4. **Documentation**: Help improve project documentation with clarifications and examples
