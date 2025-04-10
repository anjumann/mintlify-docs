# API Integration Guide

This guide explains how to interact with backend services in the HeyHomie Next.js application.

## API Client Setup

Our application uses Axios for API requests. The base configuration is in `src/utils/axios.ts`.

## Making API Requests

### Using the API Client

```tsx
import { api } from 'src/utils/axios';

// GET request
const fetchData = async () => {
  try {
    const response = await api.get('/endpoint');
    return response.data;
  } catch (error) {
    console.error('Error fetching data:', error);
    throw error;
  }
};

// POST request
const createItem = async (data) => {
  try {
    const response = await api.post('/endpoint', data);
    return response.data;
  } catch (error) {
    console.error('Error creating item:', error);
    throw error;
  }
};

// PUT request
const updateItem = async (id, data) => {
  try {
    const response = await api.put(`/endpoint/${id}`, data);
    return response.data;
  } catch (error) {
    console.error('Error updating item:', error);
    throw error;
  }
};

// DELETE request
const deleteItem = async (id) => {
  try {
    const response = await api.delete(`/endpoint/${id}`);
    return response.data;
  } catch (error) {
    console.error('Error deleting item:', error);
    throw error;
  }
};
```

### Server-Side API Calls

For server-side API calls, use the `getInternal` function to bypass DNS resolution and call the local server directly in cloud environments:

```tsx
import { getInternal } from 'src/utils/axios';

// Server-side API call
export async function getServerSideProps() {
  try {
    // This bypasses DNS resolution in cloud environments
    const response = await getInternal('/internal-endpoint');

    return {
      props: {
        data: response.data,
      },
    };
  } catch (error) {
    console.error('Server-side API error:', error);
    return {
      props: {
        error: 'Failed to fetch data',
      },
    };
  }
}
```

The `getInternal` function connects directly to the local server in cloud environments, making it more efficient for server-to-server communication. **Always use this function for server-side API calls.**

## Data Fetching with SWR

We use SWR for data fetching and caching. Here's how to use it:

```tsx
import useSWR from 'swr';
import { api } from 'src/utils/axios';

// Fetcher function
const fetcher = async (url) => {
  const response = await api.get(url);
  return response.data;
};

// Using SWR hook
const useProduct = (id) => {
  const { data, error, isLoading, mutate } = useSWR(
    id ? `/products/${id}` : null,
    fetcher
  );

  return {
    product: data,
    isLoading,
    isError: error,
    mutate, // Function to revalidate data
  };
};

// Using the hook in a component
const ProductComponent = ({ id }) => {
  const { product, isLoading, isError } = useProduct(id);

  if (isLoading) return <div>Loading...</div>;
  if (isError) return <div>Error loading product</div>;

  return <div>{product.name}</div>;
};
```

## Creating API Services

For better organization, create dedicated API service files:

```tsx
// src/api/product.ts
import { api } from 'src/utils/axios';

export const ProductAPI = {
  getAll: async () => {
    const response = await api.get('/products');
    return response.data;
  },

  getById: async (id) => {
    const response = await api.get(`/products/${id}`);
    return response.data;
  },

  create: async (data) => {
    const response = await api.post('/products', data);
    return response.data;
  },

  update: async (id, data) => {
    const response = await api.put(`/products/${id}`, data);
    return response.data;
  },

  delete: async (id) => {
    const response = await api.delete(`/products/${id}`);
    return response.data;
  },
};
```

## Custom SWR Hooks

Create custom hooks for commonly used data:

```tsx
// src/hooks/useProducts.ts
import useSWR from 'swr';
import { api } from 'src/utils/axios';

const fetcher = async (url) => {
  const response = await api.get(url);
  return response.data;
};

export const useProducts = (options = {}) => {
  const { data, error, isLoading, mutate } = useSWR('/products', fetcher, options);

  return {
    products: data || [],
    isLoading,
    isError: error,
    mutate,
  };
};

export const useProduct = (id, options = {}) => {
  const { data, error, isLoading, mutate } = useSWR(
    id ? `/products/${id}` : null,
    fetcher,
    options
  );

  return {
    product: data,
    isLoading,
    isError: error,
    mutate,
  };
};
```

## Error Handling

Handle API errors consistently:

```tsx
try {
  const response = await api.get('/endpoint');
  return response.data;
} catch (error) {
  if (error.response) {
    // The request was made and the server responded with a status code
    // that falls out of the range of 2xx
    console.error('Server error:', error.response.status, error.response.data);

    // Handle specific status codes
    if (error.response.status === 401) {
      // Unauthorized, redirect to login
      // router.push('/auth/login');
    } else if (error.response.status === 404) {
      // Resource not found
      // Show not found message
    } else if (error.response.status === 500) {
      // Server error
      // Show server error message
    }
  } else if (error.request) {
    // The request was made but no response was received
    console.error('No response received:', error.request);
    // Show network error message
  } else {
    // Something happened in setting up the request
    console.error('Request setup error:', error.message);
    // Show general error message
  }

  throw error;
}
```

## API Mocking for Development

For development without a backend, use mock data:

```tsx
// src/_mock/products.js
export const products = [
  {
    id: '1',
    name: 'Product 1',
    price: 99.99,
    // ...other properties
  },
  // ...more products
];

// src/hooks/useProducts.ts with mock support
import { products as mockProducts } from 'src/_mock/products';

export const useProducts = (options = {}) => {
  const useMock = process.env.NEXT_PUBLIC_USE_MOCK === 'true';

  const { data, error, isLoading, mutate } = useSWR(
    '/products',
    useMock
      ? () => Promise.resolve(mockProducts)
      : fetcher,
    options
  );

  return {
    products: data || [],
    isLoading,
    isError: error,
    mutate,
  };
};
```

## Best Practices

1. **Centralize API logic** - Use dedicated service files for API calls
2. **Use SWR for data fetching** - Leverage SWR's caching and revalidation
3. **Handle errors consistently** - Create reusable error handling patterns
4. **Use TypeScript** - Define types for API responses and requests
5. **Create custom hooks** - Abstract away data fetching logic
6. **Mock data for development** - Create realistic mock data for development
7. **Implement proper loading states** - Show loading indicators during data fetching
8. **Validate user input** - Validate data before sending to the API
