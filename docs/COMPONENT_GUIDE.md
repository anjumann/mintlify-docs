# Component Development Guide

This guide explains how to build components in the HeyHomie Next.js application following established patterns and best practices.

## Component Structure

Components in our application are organized in a feature-based manner:

1. **Shared Components** - Located in `src/components/`
2. **Feature-specific Components** - Located in their respective feature directories
3. **Page Components** - Located in `src/app/*/page.tsx`

## Component Creation Guidelines

### Basic Component Structure

```tsx
import { FC } from 'react';
import Box from '@mui/material/Box';
import Typography from '@mui/material/Typography';

// Define component props interface
interface ExampleComponentProps {
  title: string;
  description?: string;
}

// Component definition
const ExampleComponent: FC<ExampleComponentProps> = ({ title, description }) => {
  return (
    <Box sx={{ p: 2 }}>
      <Typography variant="h6">{title}</Typography>
      {description && (
        <Typography variant="body2" color="text.secondary">
          {description}
        </Typography>
      )}
    </Box>
  );
};

export default ExampleComponent;
```

### Component with State

```tsx
import { FC, useState } from 'react';
import Button from '@mui/material/Button';
import Box from '@mui/material/Box';

interface CounterProps {
  initialCount?: number;
}

const Counter: FC<CounterProps> = ({ initialCount = 0 }) => {
  const [count, setCount] = useState(initialCount);

  const handleIncrement = () => {
    setCount((prev) => prev + 1);
  };

  return (
    <Box sx={{ display: 'flex', alignItems: 'center', gap: 2 }}>
      <Button variant="contained" onClick={handleIncrement}>
        Increment
      </Button>
      <span>Count: {count}</span>
    </Box>
  );
};

export default Counter;
```

### Using Custom Hooks

```tsx
import { FC } from 'react';
import Box from '@mui/material/Box';
import CircularProgress from '@mui/material/CircularProgress';
import Alert from '@mui/material/Alert';
import useProductData from 'src/hooks/useProductData';

interface ProductViewProps {
  productId: string;
}

const ProductView: FC<ProductViewProps> = ({ productId }) => {
  const { data, isLoading, error } = useProductData(productId);

  if (isLoading) {
    return <CircularProgress />;
  }

  if (error) {
    return <Alert severity="error">Failed to load product</Alert>;
  }

  return (
    <Box>
      <h1>{data.name}</h1>
      <p>{data.description}</p>
      <span>${data.price}</span>
    </Box>
  );
};

export default ProductView;
```

## Styling Components

We use Material UI's `sx` prop for styling components:

```tsx
import { FC } from 'react';
import Box from '@mui/material/Box';
import Typography from '@mui/material/Typography';

const StyledComponent: FC = () => {
  return (
    <Box
      sx={{
        p: 2,
        bgcolor: 'background.paper',
        borderRadius: 1,
        boxShadow: 1,
        '&:hover': {
          boxShadow: 3,
        },
      }}
    >
      <Typography
        variant="h6"
        sx={{
          color: 'primary.main',
          fontWeight: 'bold'
        }}
      >
        Styled Heading
      </Typography>
      <Typography variant="body2" sx={{ color: 'text.secondary' }}>
        This component uses the sx prop for styling
      </Typography>
    </Box>
  );
};

export default StyledComponent;
```

## Component Organization

### File Structure

For complex components, use the following structure:

```bash
src/features/example/
├── components/           # Feature-specific components
│   ├── ExampleList.tsx
│   ├── ExampleItem.tsx
│   └── ExampleForm.tsx
├── hooks/                # Feature-specific hooks
│   └── useExampleData.ts
├── types.ts              # Feature-specific types
└── index.ts              # Public API
```

### Exporting Components

Use barrel exports:

```tsx
// src/features/example/index.ts
export { default as ExampleList } from './components/ExampleList';
export { default as ExampleItem } from './components/ExampleItem';
export { default as ExampleForm } from './components/ExampleForm';
export * from './types';
```

## Performance Optimization

### Memoization

Use `React.memo` for components that render often but with the same props:

```tsx
import { FC, memo } from 'react';

interface ExpensiveComponentProps {
  data: string;
}

const ExpensiveComponent: FC<ExpensiveComponentProps> = ({ data }) => {
  // Expensive rendering logic here
  return <div>{data}</div>;
};

export default memo(ExpensiveComponent);
```

### Callback Memoization

Use `useCallback` for functions passed as props:

```tsx
import { FC, useCallback } from 'react';
import Button from '@mui/material/Button';

interface ActionButtonProps {
  onAction: (id: string) => void;
  itemId: string;
}

const ParentComponent: FC = () => {
  const handleAction = useCallback((id: string) => {
    console.log(`Action performed on item ${id}`);
  }, []);

  return <ActionButton onAction={handleAction} itemId="123" />;
};

const ActionButton: FC<ActionButtonProps> = ({ onAction, itemId }) => {
  return (
    <Button onClick={() => onAction(itemId)}>
      Perform Action
    </Button>
  );
};

export default ParentComponent;
```

## Testing Components

We use Jest and React Testing Library for component testing:

```tsx
// ExampleComponent.test.tsx
import { render, screen } from '@testing-library/react';
import ExampleComponent from './ExampleComponent';

describe('ExampleComponent', () => {
  it('renders the title correctly', () => {
    render(<ExampleComponent title="Test Title" />);
    expect(screen.getByText('Test Title')).toBeInTheDocument();
  });

  it('renders the description when provided', () => {
    render(<ExampleComponent title="Test Title" description="Test Description" />);
    expect(screen.getByText('Test Description')).toBeInTheDocument();
  });
});
```

## Best Practices

1. **Keep components focused** - Each component should do one thing well
2. **Use TypeScript** - Define props interfaces for all components
3. **Follow naming conventions** - Use PascalCase for component names
4. **Keep components pure** - Minimize side effects
5. **Use composition** - Compose complex UIs from simpler components
6. **Avoid large components** - Split large components into smaller ones
7. **Reuse existing components** - Check if a component already exists before creating a new one
8. **Follow Material UI patterns** - Use Material UI components and styling conventions
