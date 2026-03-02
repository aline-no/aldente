# API Wiring

## Purpose

Standard pattern for connecting a frontend to a REST API. Covers the typed client, query hooks, error handling, auth token injection, and mock data. Ensures every project wires APIs the same way.

## When to Use

- Phase 4/5 (data model and DB flow)
- When adding a new API endpoint to an existing project
- When an agent needs to fetch, mutate, or paginate data

## Patterns

### 1. API Client Setup

Create a single Axios instance with interceptors. One file, one instance.

```typescript
// src/api/client.ts
import axios from 'axios';

const apiClient = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL,
  timeout: 30_000,
});

// Auth token injection (pattern depends on {{AUTH_PROVIDER}})
apiClient.interceptors.request.use(async (config) => {
  const token = await getAccessToken();
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Error normalization
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    const normalized = {
      status: error.response?.status ?? 0,
      message: error.response?.data?.message ?? error.message,
      code: error.response?.data?.code ?? 'UNKNOWN',
    };
    return Promise.reject(normalized);
  }
);

export { apiClient };
```

### 2. Type Definitions

Types go in `src/api/types/`. One file per domain entity. Types must match `docs/data-models.md`.

```typescript
// src/api/types/{{entity}}.ts
export interface {{Entity}} {
  id: string;
  // ... match the API response exactly
}
```

For paginated responses, use a generic wrapper:

```typescript
// src/api/types/pagination.ts
export interface PagedResponse<T> {
  items: T[];
  total: number;
  page: number;
  pageSize: number;
}

export interface PaginationParams {
  page: number;
  pageSize: number;
  sortBy?: string;
  sortOrder?: 'asc' | 'desc';
}
```

### 3. Query Hooks

One hook per endpoint or logical group. Use TanStack Query. Hooks go in `src/api/hooks/`.

```typescript
// src/api/hooks/use-{{entity}}.ts
import { useQuery } from '@tanstack/react-query';
import { apiClient } from '../client';
import type { {{Entity}}, PagedResponse, PaginationParams } from '../types';

export function use{{Entity}}s(params: PaginationParams) {
  return useQuery({
    queryKey: ['{{entity}}s', params],
    queryFn: () =>
      apiClient
        .get<PagedResponse<{{Entity}}>>('/{{entity}}s', { params })
        .then((res) => res.data),
  });
}
```

**Query key convention:** `[entity, ...params]`. Always include filter/pagination params in the key so TanStack Query caches correctly.

### 4. Mutations

For create/update/delete, use `useMutation` with cache invalidation:

```typescript
export function useCreate{{Entity}}() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: (data: Create{{Entity}}Payload) =>
      apiClient.post('/{{entity}}s', data).then((res) => res.data),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['{{entity}}s'] });
    },
  });
}
```

### 5. Error Handling in Components

Use the normalized error shape from the interceptor:

```typescript
const { data, error, isLoading } = use{{Entity}}s(params);

if (error?.status === 504) {
  return <TimeoutMessage />;
}
```

### 6. Mock Data for Development

Use MSW (Mock Service Worker) so agents can verify data flow without a live backend. MSW intercepts requests at the network level -- components and hooks don't know the difference.

**Setup:**

```typescript
// src/mocks/handlers.ts
import { http, HttpResponse } from 'msw';

export const handlers = [
  http.get('*/{{entity}}s', ({ request }) => {
    const url = new URL(request.url);
    const page = Number(url.searchParams.get('page') ?? 1);

    return HttpResponse.json({
      items: mockEntities,
      total: mockEntities.length,
      page,
      pageSize: 20,
    });
  }),
];
```

```typescript
// src/mocks/browser.ts
import { setupWorker } from 'msw/browser';
import { handlers } from './handlers';

export const worker = setupWorker(...handlers);
```

```typescript
// src/main.tsx (conditional start)
async function bootstrap() {
  if (import.meta.env.DEV && import.meta.env.VITE_MOCK_API === 'true') {
    const { worker } = await import('./mocks/browser');
    await worker.start({ onUnhandledRequest: 'warn' });
  }
  // ... render app
}
bootstrap();
```

**Env var:** Add `VITE_MOCK_API=true` to `.env.example`. Enable mocks when the real backend is unavailable.

**Mock data files:** Keep in `src/mocks/data/`. One file per entity. Use realistic shapes that match types in `src/api/types/`. Include edge cases: empty arrays, long strings, null optional fields.

**When to use mocks:**
- Phases 1-3 (setup, layouts, structure): always. No backend dependency.
- Phases 4-5 (data model, DB flow): start with mocks, switch to real API when wiring is confirmed.
- Phase 10 (design system): mocks for consistent screenshots and visual testing.

### File Structure

```
src/api/
  client.ts          # Axios instance + interceptors
  types/
    {{entity}}.ts
    pagination.ts
  hooks/
    use-{{entity}}.ts
src/mocks/
  browser.ts         # MSW worker setup
  handlers.ts        # Request handlers
  data/
    {{entity}}.ts    # Mock data per entity
```

## Rules

1. One Axios instance per project. Never create ad-hoc fetch calls.
2. Types must match `docs/data-models.md`. If the API returns a field, type it. Don't use `any`.
3. Every query hook returns the TanStack Query result object. Don't wrap it in custom abstractions.
4. Query keys must include all params that affect the response.
5. Auth token injection happens in the interceptor, never in individual hooks.
6. Timeout should match what the API contract specifies (default: 30s).
7. Don't cache-bust manually. Use `invalidateQueries` after mutations.
