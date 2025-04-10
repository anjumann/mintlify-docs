# Code Conventions

This document outlines the coding conventions and best practices for the HeyHomie Next.js application.

## General Guidelines

- Use TypeScript for type safety
- Follow ESLint and Prettier configurations
- Write self-documenting code with clear naming
- Keep functions small and focused on a single responsibility
- Use meaningful variable and function names

## Naming Conventions

### Files and Directories

- **React Components**: PascalCase (e.g., `ProductCard.tsx`)
- **Hooks**: camelCase with 'use' prefix (e.g., `useProductData.ts`)
- **Utility Functions**: camelCase (e.g., `formatDate.ts`)
- **Constants**: UPPER_SNAKE_CASE for values, PascalCase for object-like constants
- **Types and Interfaces**: PascalCase with relevant suffix (e.g., `ProductType.ts`, `UserInterface.ts`)

### Variables and Functions

- **Variables**: camelCase (e.g., `userData`, `productList`)
- **Boolean Variables**: Use prefixes like 'is', 'has', 'should' (e.g., `isLoading`, `hasError`)
- **Functions**: camelCase, use verbs (e.g., `fetchData`, `updateUser`)
- **Event Handlers**: camelCase with 'handle' prefix (e.g., `handleSubmit`, `handleInputChange`)
- **React Components**: PascalCase (e.g., `ProductList`, `CheckoutForm`)

## Code Organization

### Component Structure

```tsx
// Imports
import { FC, useState, useEffect } from 'react';
import { useRouter } from 'next/navigation';

// Types
interface ComponentProps {
  // ...
}

// Component
const ExampleComponent: FC<ComponentProps> = ({ prop1, prop2 }) => {
  // State declarations
  const [data, setData] = useState(null);

  // Hooks
  const router = useRouter();

  // Effects
  useEffect(() => {
    // ...
  }, []);

  // Event handlers
  const handleClick = () => {
    // ...
  };

  // Render helpers
  const renderItems = () => {
    // ...
  };

  // Main render
  return (
    <div>
      {/* JSX */}
    </div>
  );
};

export default ExampleComponent;
```

### Import Order

1. React/Next.js imports
2. Third-party libraries
3. Absolute imports from the application
4. Relative imports from the current directory
5. CSS/SCSS imports

Example:

```tsx
// 1. React/Next.js imports
import { useState, useEffect } from 'react';
import { useRouter } from 'next/navigation';

// 2. Third-party libraries
import { format } from 'date-fns';
import { useForm } from 'react-hook-form';

// 3. Absolute imports from the application
import { Button } from 'src/components/Button';
import { useAuth } from 'src/hooks/useAuth';

// 4. Relative imports from the current directory
import { ProductForm } from './ProductForm';
import { productValidation } from './utils';

// 5. CSS imports
import './styles.css';
```

## TypeScript Guidelines

### Type Definitions

- Use interfaces for object shapes that will be implemented or extended
- Use type aliases for unions, primitives, and complex types
- Add explicit return types to functions, especially exported ones

```tsx
// Interface for objects with implementation
interface User {
  id: string;
  name: string;
  email: string;
}

// Type for union or complex types
type Status = 'idle' | 'loading' | 'success' | 'error';
type UserMap = Record<string, User>;

// Function with explicit return type
function formatUser(user: User): string {
  return `${user.name} (${user.email})`;
}
```

### Use Type Inference Where Appropriate

```tsx
// Type inference is clear here, no need for explicit type
const [count, setCount] = useState(0);

// For complex types, provide explicit type
const [users, setUsers] = useState<User[]>([]);
```

## Material UI Guidelines

### Styling

- Use the `sx` prop for component-specific styling
- Create theme extensions for reusable styles
- Use theme values instead of hard-coded values

```tsx
// Good: Using theme values
<Box
  sx={{
    p: 2,
    mt: 3,
    bgcolor: 'background.paper',
    borderRadius: 1,
  }}
>
  <Typography color="primary.main">Content</Typography>
</Box>

// Bad: Hard-coded values
<Box
  sx={{
    padding: '16px',
    marginTop: '24px',
    backgroundColor: '#ffffff',
    borderRadius: '4px',
  }}
>
  <Typography style={{ color: '#1976d2' }}>Content</Typography>
</Box>
```

### Component Props

- Spread props at the end to allow overrides
- Destructure only the props you need
- Use meaningful default values

```tsx
interface ButtonProps {
  variant?: 'contained' | 'outlined' | 'text';
  children: React.ReactNode;
  disabled?: boolean;
}

const CustomButton: FC<ButtonProps> = ({
  variant = 'contained',
  disabled = false,
  children,
  ...props
}) => {
  return (
    <Button variant={variant} disabled={disabled} {...props}>
      {children}
    </Button>
  );
};
```

## State Management

### Local State

- Use `useState` for component-specific state
- Use `useReducer` for complex state logic

### Global State

- Use React Context for global state that doesn't change often
- Use SWR for server state

### Form State

- Use React Hook Form for form state management
- Use Yup for schema validation

## Error Handling

- Use try/catch for async operations
- Provide meaningful error messages
- Log errors to the console or monitoring service
- Display user-friendly error messages

```tsx
try {
  await api.post('/endpoint', data);
} catch (error) {
  console.error('Failed to post data:', error);
  // User-friendly message
  setError('Unable to save data. Please try again later.');
}
```

## Comments

- Use comments to explain "why", not "what"
- Use JSDoc for exported functions and components
- Keep comments updated with code changes

```tsx
/**
 * Formats a date string into a localized date display
 *
 * @param dateString - ISO date string to format
 * @param locale - Locale to use for formatting (defaults to user's locale)
 * @returns Formatted date string
 */
function formatDate(dateString: string, locale?: string): string {
  // Implementation
}
```

## Testing

- Test components in isolation
- Focus on user interactions and outcomes
- Use meaningful test descriptions
- Write maintainable tests

```tsx
describe('ProductCard', () => {
  it('displays product name and price', () => {
    // Arrange
    const product = { name: 'Test Product', price: 99.99 };

    // Act
    render(<ProductCard product={product} />);

    // Assert
    expect(screen.getByText(product.name)).toBeInTheDocument();
    expect(screen.getByText(`$${product.price}`)).toBeInTheDocument();
  });
});
```

## Git Commit Guidelines

- Use conventional commit messages
- Keep commits focused on a single change
- Write descriptive commit messages

Format: `type(scope): subject`

Examples:

- `feat(product): add product search functionality`
- `fix(auth): resolve login redirect issue`
- `docs(readme): update installation instructions`
- `refactor(cart): simplify cart calculation logic`

## Code Review Checklist

- Does the code follow the project's style guide?
- Is the code type-safe?
- Are there any potential performance issues?
- Is the code well-tested?
- Is error handling implemented properly?
- Is the component structure sensible?
- Are variable/function names clear and descriptive?
- Is the code DRY (Don't Repeat Yourself)?
