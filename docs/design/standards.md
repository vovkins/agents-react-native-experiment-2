# Technical Standards and Conventions

## 1. Overview

This document defines the coding standards, naming conventions, folder structure, git workflow, and testing standards for the Investment Management Mobile Application project. All team members must follow these standards to ensure consistency, maintainability, and code quality.

---

## 2. Coding Standards

### 2.1 TypeScript/JavaScript Conventions

#### 2.1.1 TypeScript Configuration

```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "lib": ["ESNext"],
    "jsx": "react-native",
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "strictBindCallApply": true,
    "strictPropertyInitialization": true,
    "noImplicitThis": true,
    "alwaysStrict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "noUncheckedIndexedAccess": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "allowSyntheticDefaultImports": true
  }
}
```

#### 2.1.2 General TypeScript Rules

| Rule | Description | Example |
|------|-------------|---------|
| **No `any`** | Use `unknown` if type is truly unknown | `function parse(input: unknown)` |
| **Explicit return types** | Required for all public/exported functions | `export function fetch(): Promise<User>` |
| **Interface vs Type** | Interface for objects, Type for unions | See examples below |
| **No non-null assertions** | Handle null/undefined explicitly | Use optional chaining `?.` |
| **Const assertions** | Use `as const` for literal types | `const ROLES = ['admin', 'user'] as const` |

**Interface for object shapes:**
```typescript
// ✅ Good - Interface for objects
interface User {
  id: string;
  email: string;
  name: string;
}

// ✅ Good - Type for unions/primitives
type Status = 'pending' | 'active' | 'inactive';
type MaybeUser = User | null;
```

**Explicit return types:**
```typescript
// ✅ Good
export function calculateTotal(positions: Position[]): number {
  return positions.reduce((sum, pos) => sum + pos.value, 0);
}

// ❌ Bad
export function calculateTotal(positions: Position[]) {
  return positions.reduce((sum, pos) => sum + pos.value, 0);
}
```

#### 2.1.3 Variable Declarations

| Type | Convention | Example |
|------|------------|---------|
| **Constants** | `SCREAMING_SNAKE_CASE` | `const API_TIMEOUT_MS = 30000;` |
| **Variables** | `camelCase` | `const userCount = 10;` |
| **Private properties** | Prefix with `_` | `private _token: string;` |
| **Boolean variables** | Prefix with `is`, `has`, `should` | `isLoading`, `hasError`, `shouldFetch` |

```typescript
// ✅ Good
const API_BASE_URL = 'https://api.example.com';
const MAX_RETRIES = 3;

let currentUser: User | null = null;
let isLoading = false;
let hasError = false;

// ❌ Bad
const api_base_url = 'https://api.example.com';
const maxRetries = 3;
let loading = false;
let error = false;
```

#### 2.1.4 Function Declarations

**Prefer arrow functions for callbacks and simple functions:**
```typescript
// ✅ Good - Arrow function
const formatDate = (date: Date): string => {
  return date.toLocaleDateString('ru-RU');
};

// ✅ Good - Regular function for complex logic
function calculatePortfolioMetrics(
  positions: Position[],
  options: CalculationOptions
): PortfolioMetrics {
  // Complex logic here
}

// ✅ Good - Arrow function for callbacks
const activeUsers = users.filter((user) => user.isActive);
```

**Function signature ordering:**
```typescript
// Order: required params, optional params, rest params, return type
function fetchData(
  endpoint: string,
  options?: RequestOptions,
  ...headers: string[]
): Promise<Response> {
  // Implementation
}
```

#### 2.1.5 Async/Await Patterns

```typescript
// ✅ Good - Async/await with error handling
async function fetchUser(id: string): Promise<User> {
  try {
    const response = await apiClient.get(`/users/${id}`);
    return response.data;
  } catch (error) {
    if (error instanceof ApiError) {
      throw new UserNotFoundError(id);
    }
    throw error;
  }
}

// ❌ Bad - Nested promises
function fetchUser(id: string): Promise<User> {
  return apiClient
    .get(`/users/${id}`)
    .then((response) => response.data)
    .catch((error) => {
      throw error;
    });
}

// ✅ Good - Parallel requests
async function fetchDashboard(): Promise<Dashboard> {
  const [user, portfolio, messages] = await Promise.all([
    fetchUser(userId),
    fetchPortfolio(userId),
    fetchMessages(userId),
  ]);
  
  return { user, portfolio, messages };
}
```

### 2.2 React Native Best Practices

#### 2.2.1 Component Structure

```typescript
// Component file structure
// 1. Imports (grouped)
// 2. Types/Interfaces
// 3. Constants
// 4. Component
// 5. Styles (if not using NativeWind)
// 6. Export

import React, { memo, useCallback, useState } from 'react';
import { View, Text, TouchableOpacity } from 'react-native';
import { NativeWindStyleSheet } from 'nativewind';

// Types
interface ProductCardProps {
  product: Product;
  onPress: (product: Product) => void;
  isLoading?: boolean;
}

// Component
const ProductCard: React.FC<ProductCardProps> = memo(({
  product,
  onPress,
  isLoading = false,
}) => {
  const [isExpanded, setIsExpanded] = useState(false);

  const handlePress = useCallback(() => {
    onPress(product);
  }, [onPress, product]);

  if (isLoading) {
    return <ProductCardSkeleton />;
  }

  return (
    <TouchableOpacity onPress={handlePress} className="p-4 bg-white rounded-lg">
      <Text className="text-lg font-semibold">{product.name}</Text>
      <Text className="text-gray-600">{product.description}</Text>
    </TouchableOpacity>
  );
});

ProductCard.displayName = 'ProductCard';

export default ProductCard;
```

#### 2.2.2 Component Guidelines

| Guideline | Description |
|-----------|-------------|
| **Use memo sparingly** | Only for expensive renders or frequent parent updates |
| **Destructure props** | Always destructure in function signature |
| **Keep components small** | < 200 lines, extract subcomponents |
| **Use composition** | Prefer composition over inheritance |
| **Avoid inline functions** | Use useCallback for handlers passed to children |

```typescript
// ✅ Good - Destructured props, memo when needed
const PositionCard: React.FC<PositionCardProps> = memo(({
  position,
  onPress,
}) => {
  return (
    <TouchableOpacity onPress={() => onPress(position)}>
      {/* ... */}
    </TouchableOpacity>
  );
});

// ❌ Bad - Inline function creation
const Parent = () => {
  return <Child onClick={() => console.log('clicked')} />;
};
```

#### 2.2.3 Hooks Best Practices

| Hook | Usage |
|------|-------|
| `useState` | For local component state |
| `useCallback` | Memoize callbacks passed to children |
| `useMemo` | Expensive calculations, avoid for simple operations |
| `useEffect` | Side effects, always specify dependencies |
| `useRef` | DOM references, mutable values that don't trigger re-render |
| `useContext` | Access global context, prefer Zustand for complex state |

```typescript
// ✅ Good - Proper dependencies
useEffect(() => {
  fetchUser(userId);
}, [userId]); // Only re-run when userId changes

// ❌ Bad - Missing dependencies
useEffect(() => {
  fetchUser(userId);
}, []); // Will not update when userId changes

// ✅ Good - Cleanup
useEffect(() => {
  const subscription = eventEmitter.subscribe(handler);
  return () => subscription.unsubscribe();
}, [handler]);
```

#### 2.2.4 List Rendering

```typescript
// ✅ Good - FlatList with virtualization
import { FlatList } from 'react-native';

const ProductList: React.FC<ProductListProps> = ({ products }) => {
  const renderItem = useCallback(({ item }: { item: Product }) => (
    <ProductCard product={item} onPress={handleProductPress} />
  ), [handleProductPress]);

  const keyExtractor = useCallback((item: Product) => item.id, []);

  return (
    <FlatList
      data={products}
      renderItem={renderItem}
      keyExtractor={keyExtractor}
      getItemLayout={getItemLayout} // For performance
      initialNumToRender={10}
      maxToRenderPerBatch={10}
      windowSize={5}
    />
  );
};
```

#### 2.2.5 Performance Guidelines

| Area | Guideline |
|------|-----------|
| **Images** | Use `react-native-fast-image` with proper sizing |
| **Lists** | Always use `FlatList` or `SectionList`, never `.map()` |
| **State updates** | Use functional updates when possible |
| **Re-renders** | Profile with React DevTools, add memo only when needed |
| **Bundle size** | Lazy load screens, use dynamic imports for large modules |

```typescript
// ✅ Good - Functional state update
setCount((prev) => prev + 1);

// ✅ Good - Lazy loading
const ProductDetailScreen = React.lazy(() => import('./ProductDetailScreen'));
```

### 2.3 Node.js Patterns (Backend Reference)

#### 2.3.1 Module Structure

```typescript
// Module pattern for services
// services/AuthService.ts

import { injectable, inject } from 'tsyringe';

@injectable()
export class AuthService {
  constructor(
    @inject('IUserRepository') private userRepo: IUserRepository,
    @inject('ITokenService') private tokenService: ITokenService,
  ) {}

  async login(credentials: Credentials): Promise<AuthResult> {
    // Implementation
  }
}
```

#### 2.3.2 Error Handling

```typescript
// Custom error classes
class AppError extends Error {
  constructor(
    public message: string,
    public statusCode: number = 500,
    public code: string = 'INTERNAL_ERROR',
  ) {
    super(message);
    this.name = 'AppError';
  }
}

class ValidationError extends AppError {
  constructor(message: string) {
    super(message, 400, 'VALIDATION_ERROR');
  }
}

class UnauthorizedError extends AppError {
  constructor(message: string = 'Unauthorized') {
    super(message, 401, 'UNAUTHORIZED');
  }
}

// Error handling middleware
const errorHandler: ErrorRequestHandler = (err, req, res, next) => {
  if (err instanceof AppError) {
    return res.status(err.statusCode).json({
      error: {
        message: err.message,
        code: err.code,
      },
    });
  }
  
  // Log unexpected errors
  console.error(err);
  return res.status(500).json({
    error: { message: 'Internal server error', code: 'INTERNAL_ERROR' },
  });
};
```

---

## 3. Naming Conventions

### 3.1 Files and Folders

| Type | Convention | Example |
|------|------------|---------|
| **Component files** | `PascalCase.tsx` | `ProductCard.tsx` |
| **Screen files** | `PascalCase + Screen.tsx` | `PortfolioScreen.tsx` |
| **Hook files** | `camelCase.ts` with `use` prefix | `useAuth.ts` |
| **Service files** | `PascalCase + Service.ts` | `AuthService.ts` |
| **Adapter files** | `PascalCase + Adapter.ts` | `ProductAdapter.ts` |
| **Store files** | `camelCase + Store.ts` | `authStore.ts` |
| **Type files** | `PascalCase.ts` or `index.ts` | `User.ts`, `types/index.ts` |
| **Utility files** | `camelCase.ts` | `formatters.ts` |
| **Constant files** | `camelCase.ts` or `SCREAMING_SNAKE.ts` | `constants.ts`, `API_ENDPOINTS.ts` |
| **Test files** | Same as source + `.test.ts` | `ProductCard.test.tsx` |
| **Folders** | `kebab-case` or `PascalCase` | `product-list/`, `ProductCard/` |

### 3.2 Variables and Functions

| Type | Convention | Example |
|------|------------|---------|
| **Variables** | `camelCase` | `const currentUser = ...` |
| **Constants** | `SCREAMING_SNAKE_CASE` | `const API_TIMEOUT_MS = 30000;` |
| **Private variables** | Prefix with `_` | `private _token: string;` |
| **Boolean variables** | Prefix with `is`, `has`, `should`, `can` | `isLoading`, `hasError` |
| **Function names** | `camelCase`, verb-first | `fetchUser()`, `calculateTotal()` |
| **Event handlers** | Prefix with `handle` | `handleButtonClick()` |
| **Async functions** | No special prefix | `fetchUser()`, `saveData()` |
| **Getter functions** | No special prefix | `getUser()` |
| **Setter functions** | Prefix with `set` | `setUser()` |

```typescript
// ✅ Good
const userCount = 10;
const isLoading = false;
const hasUnreadMessages = true;
const API_BASE_URL = 'https://api.example.com';

function fetchUser() {}
function calculatePortfolioValue() {}
function handleLoginPress() {}
function setErrorMessage() {}

// ❌ Bad
const UserCount = 10;
const loading = false;
const unread = true;
const api_base_url = 'https://api.example.com';

function GetUser() {}
function CalculatePortfolio() {}
function onLoginPress() {}
function errorMessage() {}
```

### 3.3 Components

| Type | Convention | Example |
|------|------------|---------|
| **Component name** | `PascalCase` | `ProductCard` |
| **Props interface** | `ComponentNameProps` | `ProductCardProps` |
| **Props variable** | `props` (destructured) | `({ product, onPress })` |
| **Ref name** | `ref` | `const inputRef = useRef();` |
| **Forward ref** | `ComponentName` | `forwardRef((props, ref) => ...)` |

```typescript
// ✅ Good
interface ProductCardProps {
  product: Product;
  onPress: (product: Product) => void;
}

const ProductCard: React.FC<ProductCardProps> = ({ product, onPress }) => {
  return <View>{/* ... */}</View>;
};

// ✅ Good - Forward ref
const Input = forwardRef<HTMLInputElement, InputProps>(
  ({ value, onChange }, ref) => {
    return <input ref={ref} value={value} onChange={onChange} />;
  }
);
```

### 3.4 Types and Interfaces

| Type | Convention | Example |
|------|------------|---------|
| **Interface** | `PascalCase` | `User`, `Portfolio` |
| **Type alias** | `PascalCase` | `Status`, `MaybeUser` |
| **Enum** | `PascalCase` for name, `PascalCase` for values | `Status.Active` |
| **Generic types** | Single capital letter or descriptive | `T`, `TResponse`, `TData` |
| **Union types** | `PascalCase` | `MessageType`, `Status` |

```typescript
// ✅ Good - Interface
interface User {
  id: string;
  email: string;
}

// ✅ Good - Type for union
type Status = 'pending' | 'active' | 'inactive';

// ✅ Good - Enum
enum MessageStatus {
  Sending = 'SENDING',
  Sent = 'SENT',
  Delivered = 'DELIVERED',
  Read = 'READ',
}

// ✅ Good - Generic
interface ApiResponse<TData> {
  data: TData;
  status: number;
}

// ✅ Good - Descriptive generic
function fetchEntity<TModel extends BaseEntity>(id: string): Promise<TModel> {
  // Implementation
}
```

### 3.5 API Endpoints

| Type | Convention | Example |
|------|------------|---------|
| **REST endpoints** | `kebab-case`, plural nouns | `/products`, `/portfolio/positions` |
| **Endpoint IDs** | `:camelCase` | `/products/:id`, `/users/:userId` |
| **Query params** | `camelCase` | `?pageSize=10&sortBy=name` |
| **WebSocket events** | `snake_case` | `message_sent`, `typing_start` |

```
# ✅ Good REST endpoints
GET    /products
GET    /products/:id
GET    /products/categories
GET    /portfolio
GET    /portfolio/positions
POST   /chat/messages

# ❌ Bad
GET    /product
GET    /product/:ID
GET    /product-categories
GET    /getPortfolio
POST   /chat/send-message
```

### 3.6 Zustand Stores

| Type | Convention | Example |
|------|------------|---------|
| **Store name** | `featureStore` | `authStore`, `chatStore` |
| **State interface** | `FeatureState` | `AuthState`, `ChatState` |
| **Actions** | `camelCase`, verb-first | `login()`, `fetchMessages()` |
| **Selectors** | `useFeatureValue` | `useIsAuthenticated()` |

```typescript
// ✅ Good
interface AuthState {
  isAuthenticated: boolean;
  user: User | null;
  
  // Actions
  login: (credentials: Credentials) => Promise<void>;
  logout: () => Promise<void>;
}

export const useAuthStore = create<AuthState>((set, get) => ({
  isAuthenticated: false,
  user: null,
  
  login: async (credentials) => { /* ... */ },
  logout: async () => { /* ... */ },
}));

// Selector hook
export const useIsAuthenticated = () => useAuthStore((state) => state.isAuthenticated);
```

---

## 4. Folder Structure

### 4.1 Frontend Structure (React Native)

```
investment-app/
├── android/                      # Android native project
│   ├── app/
│   ├── build.gradle
│   └── gradle.properties
├── ios/                          # iOS native project
│   ├── InvestmentApp/
│   ├── InvestmentApp.xcodeproj
│   └── Podfile
├── src/                          # Source code
│   ├── view/                     # View Layer
│   │   ├── screens/              # Screen components
│   │   │   ├── auth/             # Authentication screens
│   │   │   │   ├── LoginScreen.tsx
│   │   │   │   ├── PINScreen.tsx
│   │   │   │   ├── BiometricSetupScreen.tsx
│   │   │   │   └── index.ts
│   │   │   ├── products/         # Product screens
│   │   │   │   ├── ProductListScreen.tsx
│   │   │   │   ├── ProductDetailScreen.tsx
│   │   │   │   └── index.ts
│   │   │   ├── portfolio/        # Portfolio screens
│   │   │   │   ├── PortfolioOverviewScreen.tsx
│   │   │   │   ├── PositionDetailScreen.tsx
│   │   │   │   └── index.ts
│   │   │   ├── chat/             # Chat screens
│   │   │   │   ├── ChatScreen.tsx
│   │   │   │   ├── ConversationListScreen.tsx
│   │   │   │   └── index.ts
│   │   │   └── profile/          # Profile screens
│   │   │       ├── ProfileScreen.tsx
│   │   │       ├── SettingsScreen.tsx
│   │   │       └── index.ts
│   │   ├── components/           # Reusable components
│   │   │   ├── common/           # Common UI components
│   │   │   │   ├── Button/
│   │   │   │   │   ├── Button.tsx
│   │   │   │   │   ├── Button.styles.ts
│   │   │   │   │   ├── Button.test.tsx
│   │   │   │   │   └── index.ts
│   │   │   │   ├── Input/
│   │   │   │   ├── Card/
│   │   │   │   ├── Skeleton/
│   │   │   │   ├── Loading/
│   │   │   │   ├── ErrorBoundary/
│   │   │   │   └── index.ts
│   │   │   ├── products/         # Product-specific components
│   │   │   │   ├── StrategyCard/
│   │   │   │   ├── ProductCategoryFilter/
│   │   │   │   └── index.ts
│   │   │   ├── portfolio/        # Portfolio-specific components
│   │   │   │   ├── PositionCard/
│   │   │   │   ├── ValueDisplay/
│   │   │   │   ├── MetricCard/
│   │   │   │   └── index.ts
│   │   │   ├── chat/             # Chat-specific components
│   │   │   │   ├── MessageBubble/
│   │   │   │   ├── MessageInput/
│   │   │   │   ├── StatusIndicator/
│   │   │   │   └── index.ts
│   │   │   └── layout/           # Layout components
│   │   │       ├── ScreenWrapper/
│   │   │       ├── Header/
│   │   │       ├── TabBar/
│   │   │       └── index.ts
│   │   ├── navigation/           # Navigation configuration
│   │   │   ├── AppNavigator.tsx
│   │   │   ├── AuthNavigator.tsx
│   │   │   ├── MainNavigator.tsx
│   │   │   ├── linking.ts
│   │   │   ├── types.ts
│   │   │   └── index.ts
│   │   └── hooks/                # Custom hooks
│   │       ├── useAuth.ts
│   │       ├── useProducts.ts
│   │       ├── usePortfolio.ts
│   │       ├── useChat.ts
│   │       ├── useNetworkStatus.ts
│   │       └── index.ts
│   ├── domain/                   # Domain Layer
│   │   ├── entities/             # Domain entities
│   │   │   ├── User.ts
│   │   │   ├── Product.ts
│   │   │   ├── Portfolio.ts
│   │   │   ├── Position.ts
│   │   │   ├── Message.ts
│   │   │   ├── Conversation.ts
│   │   │   └── index.ts
│   │   ├── services/             # Business logic services
│   │   │   ├── AuthService.ts
│   │   │   ├── ProductService.ts
│   │   │   ├── PortfolioService.ts
│   │   │   ├── ChatService.ts
│   │   │   ├── SyncService.ts
│   │   │   └── index.ts
│   │   ├── usecases/             # Use cases
│   │   │   ├── LoginUseCase.ts
│   │   │   ├── FetchProductsUseCase.ts
│   │   │   ├── CalculatePortfolioMetricsUseCase.ts
│   │   │   └── index.ts
│   │   ├── calculators/          # Calculation logic
│   │   │   ├── PortfolioCalculator.ts
│   │   │   ├── ReturnsCalculator.ts
│   │   │   └── index.ts
│   │   ├── validators/           # Validation logic
│   │   │   ├── authValidator.ts
│   │   │   ├── productValidator.ts
│   │   │   └── index.ts
│   │   ├── utils/                # Domain utilities
│   │   │   ├── formatters.ts
│   │   │   ├── dateUtils.ts
│   │   │   ├── currencyUtils.ts
│   │   │   └── index.ts
│   │   └── index.ts
│   ├── adapters/                 # Adapter Layer
│   │   ├── api/                  # REST API adapters
│   │   │   ├── ApiClient.ts
│   │   │   ├── AuthAdapter.ts
│   │   │   ├── ProductAdapter.ts
│   │   │   ├── PortfolioAdapter.ts
│   │   │   ├── ChatAdapter.ts
│   │   │   ├── types.ts
│   │   │   └── index.ts
│   │   ├── websocket/            # WebSocket adapters
│   │   │   ├── WebSocketClient.ts
│   │   │   ├── ChatWebSocket.ts
│   │   │   ├── types.ts
│   │   │   └── index.ts
│   │   ├── storage/              # Storage adapters
│   │   │   ├── SecureStorageAdapter.ts
│   │   │   ├── CacheAdapter.ts
│   │   │   ├── MessageStorageAdapter.ts
│   │   │   └── index.ts
│   │   ├── platform/             # Platform adapters
│   │   │   ├── BiometricAdapter.ts
│   │   │   ├── NetworkAdapter.ts
│   │   │   ├── NotificationAdapter.ts
│   │   │   └── index.ts
│   │   └── index.ts
│   ├── stores/                   # Zustand stores
│   │   ├── authStore.ts
│   │   ├── productStore.ts
│   │   ├── portfolioStore.ts
│   │   ├── chatStore.ts
│   │   ├── syncStore.ts
│   │   ├── uiStore.ts
│   │   └── index.ts
│   ├── db/                       # Database configuration
│   │   ├── schema.ts
│   │   ├── migrations/
│   │   │   ├── 001_initial.ts
│   │   │   └── index.ts
│   │   └── index.ts
│   ├── shared/                   # Shared utilities
│   │   ├── types/                # Shared types
│   │   │   ├── api.ts
│   │   │   ├── errors.ts
│   │   │   ├── utils.ts
│   │   │   └── index.ts
│   │   ├── constants/            # App constants
│   │   │   ├── api.ts
│   │   │   ├── app.ts
│   │   │   ├── errors.ts
│   │   │   └── index.ts
│   │   ├── utils/                # Shared utilities
│   │   │   ├── logger.ts
│   │   │   ├── errorHandler.ts
│   │   │   └── index.ts
│   │   └── index.ts
│   ├── config/                   # App configuration
│   │   ├── app.config.ts
│   │   ├── api.config.ts
│   │   ├── env.ts
│   │   └── index.ts
│   ├── App.tsx                   # App entry point
│   └── index.ts                   # Root export
├── docs/                         # Documentation
│   ├── adr/                      # Architecture Decision Records
│   ├── design/                   # Design documents
│   └── requirements/             # Requirements
├── e2e/                          # E2E tests
│   ├── auth.test.ts
│   ├── products.test.ts
│   ├── portfolio.test.ts
│   └── chat.test.ts
├── scripts/                      # Build and utility scripts
│   ├── build.sh
│   ├── test.sh
│   └── lint.sh
├── .eslintrc.js                  # ESLint configuration
├── .prettierrc.js                # Prettier configuration
├── .gitignore                    # Git ignore rules
├── app.json                      # Expo/App configuration
├── babel.config.js               # Babel configuration
├── jest.config.js                # Jest configuration
├── metro.config.js               # Metro bundler configuration
├── package.json                  # NPM configuration
├── tsconfig.json                 # TypeScript configuration
└── README.md                     # Project README
```

### 4.2 Module Structure (Individual Feature)

```
src/view/components/products/StrategyCard/
├── StrategyCard.tsx           # Main component
├── StrategyCard.styles.ts     # Styles (if not using NativeWind)
├── StrategyCard.test.tsx      # Unit tests
├── StrategyCard.stories.tsx   # Storybook stories (optional)
├── types.ts                   # Local types
├── hooks.ts                   # Local hooks
├── utils.ts                   # Local utilities
└── index.ts                   # Public exports
```

### 4.3 Shared Code Organization

```
src/shared/
├── types/
│   ├── api.ts              # API types (Request, Response, etc.)
│   ├── errors.ts           # Error types
│   ├── utils.ts            # Utility types (DeepPartial, etc.)
│   └── index.ts
├── constants/
│   ├── api.ts              # API constants (endpoints, timeouts)
│   ├── app.ts              # App constants (name, version)
│   ├── errors.ts           # Error codes and messages
│   ├── storage.ts          # Storage keys
│   └── index.ts
└── utils/
    ├── logger.ts           # Logging utility
    ├── errorHandler.ts     # Error handling utility
    ├── async.ts            # Async utilities (retry, timeout)
    └── index.ts
```

---

## 5. Git Workflow

### 5.1 Branch Naming

| Branch Type | Pattern | Example |
|-------------|---------|---------|
| **Feature** | `feature/TASK-ID-description` | `feature/TASK-247-login-screen` |
| **Bugfix** | `bugfix/TASK-ID-description` | `bugfix/TASK-123-fix-auth-error` |
| **Hotfix** | `hotfix/TASK-ID-description` | `hotfix/TASK-456-crash-fix` |
| **Release** | `release/v1.0.0` | `release/v1.0.0` |
| **Develop** | `develop` | `develop` |
| **Main** | `main` | `main` |

**Branch naming rules:**
- Use lowercase letters and hyphens
- Include task ID from GitHub issues
- Keep description short but descriptive
- Maximum 50 characters

### 5.2 Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

#### Commit Types

| Type | Description | Example |
|------|-------------|---------|
| `feat` | New feature | `feat(auth): add biometric login support` |
| `fix` | Bug fix | `fix(chat): resolve message ordering issue` |
| `docs` | Documentation | `docs: update API documentation` |
| `style` | Code style (no logic change) | `style: format code with prettier` |
| `refactor` | Code refactoring | `refactor(auth): extract token validation logic` |
| `perf` | Performance improvement | `perf(list): optimize FlatList rendering` |
| `test` | Adding/modifying tests | `test(auth): add login unit tests` |
| `chore` | Maintenance tasks | `chore: update dependencies` |
| `ci` | CI/CD changes | `ci: add GitHub Actions workflow` |

#### Scopes

| Scope | Description |
|-------|-------------|
| `auth` | Authentication module |
| `products` | Product showcase module |
| `portfolio` | Portfolio module |
| `chat` | Chat module |
| `nav` | Navigation |
| `store` | State management |
| `api` | API adapters |
| `ui` | UI components |
| `db` | Database |

#### Examples

```bash
# Feature commit
feat(auth): add PIN code authentication

Implements PIN code entry screen and validation logic.
Includes secure storage for PIN hash and lockout mechanism.

Closes #247

# Bug fix commit
fix(chat): resolve message duplication on reconnect

Messages were being duplicated when WebSocket reconnected
due to missing message ID deduplication.

Fixes #123

# Breaking change
feat(api)!: update API response format

BREAKING CHANGE: API responses now use `data` instead of `result`
for the response body.

# Multiple issues
feat(portfolio): add position detail view

Adds new position detail screen with charts and metrics.

Closes #267, #268
```

### 5.3 Pull Request Guidelines

#### PR Title Format
```
<type>(<scope>): <description> (#issue-number)
```

Example: `feat(auth): implement biometric authentication (#252)`

#### PR Description Template

```markdown
## Description
<!-- Brief description of changes -->

## Type of Change
- [ ] 🚀 New feature (feat)
- [ ] 🐛 Bug fix (fix)
- [ ] 📝 Documentation (docs)
- [ ] 🎨 Style change (style)
- [ ] ♻️ Refactoring (refactor)
- [ ] ⚡ Performance (perf)
- [ ] ✅ Tests (test)
- [ ] 🔧 Chore (chore)

## Related Issues
<!-- Link to related issues -->
Closes #123
Related to #456

## Changes Made
<!-- List of changes -->
- Added biometric authentication service
- Implemented biometric prompt UI
- Added secure storage for biometric preference

## Testing
- [ ] Unit tests added/updated
- [ ] E2E tests added/updated
- [ ] Manual testing completed

## Screenshots (if applicable)
<!-- Add screenshots for UI changes -->

## Checklist
- [ ] Code follows project coding standards
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
- [ ] No new warnings introduced
- [ ] Tests pass locally
- [ ] Branch is up to date with develop

## Additional Notes
<!-- Any additional information for reviewers -->
```

#### PR Review Process

1. **Author**: Create PR, fill description template
2. **CI**: Automated checks (lint, tests, build)
3. **Reviewers**: At least 1 approval required
4. **Author**: Address review comments
5. **Merge**: Squash and merge to develop

### 5.4 Git Workflow Diagram

```
main (production)
  │
  └── release/v1.0.0 ──────────► main (tag v1.0.0)
         │
develop ─┴────────────────────────► develop
  │                                   ▲
  ├── feature/TASK-247-login ◄────────┤
  │         │                         │
  │         └── PR #1 ────────────────┘
  │
  ├── feature/TASK-256-products
  │         │
  │         └── PR #2 ────────────────┘
  │
  └── bugfix/TASK-123-auth-fix
            │
            └── PR #3 ────────────────┘
```

---

## 6. Testing Standards

### 6.1 Unit Test Requirements

| Type | Coverage | Description |
|------|----------|-------------|
| **Domain Layer** | 80% minimum | All services, calculators, validators |
| **Adapter Layer** | 70% minimum | API adapters, storage adapters |
| **Components** | 60% minimum | Critical components with complex logic |
| **Hooks** | 80% minimum | All custom hooks |

#### Test File Structure

```
src/domain/services/AuthService.ts
src/domain/services/__tests__/AuthService.test.ts

src/view/components/ProductCard/ProductCard.tsx
src/view/components/ProductCard/ProductCard.test.tsx
```

#### Test Naming Convention

```typescript
// Pattern: describe -> context -> it
describe('AuthService', () => {
  describe('login', () => {
    context('with valid credentials', () => {
      it('should return user and tokens', async () => {
        // Test implementation
      });
    });

    context('with invalid credentials', () => {
      it('should throw AuthenticationError', async () => {
        // Test implementation
      });
    });
  });
});
```

#### Unit Test Examples

```typescript
// Service test
import { AuthService } from '../AuthService';
import { AuthAdapter } from '../../../adapters/api/AuthAdapter';
import { TokenStorage } from '../../../adapters/storage/SecureStorageAdapter';

// Mocks
jest.mock('../../../adapters/api/AuthAdapter');
jest.mock('../../../adapters/storage/SecureStorageAdapter');

describe('AuthService', () => {
  let authService: AuthService;
  let mockAuthAdapter: jest.Mocked<AuthAdapter>;
  let mockTokenStorage: jest.Mocked<TokenStorage>;

  beforeEach(() => {
    mockAuthAdapter = {
      login: jest.fn(),
      logout: jest.fn(),
      refreshToken: jest.fn(),
    } as any;
    
    mockTokenStorage = {
      storeTokens: jest.fn(),
      getTokens: jest.fn(),
      clearTokens: jest.fn(),
    } as any;
    
    authService = new AuthService(mockAuthAdapter, mockTokenStorage);
  });

  describe('login', () => {
    context('with valid credentials', () => {
      it('should return user and tokens', async () => {
        // Arrange
        const credentials = { email: 'test@example.com', password: 'password' };
        const mockResponse = {
          user: { id: '1', email: 'test@example.com' },
          tokens: { accessToken: 'token', refreshToken: 'refresh' },
        };
        mockAuthAdapter.login.mockResolvedValue(mockResponse);

        // Act
        const result = await authService.login(credentials);

        // Assert
        expect(result).toEqual(mockResponse);
        expect(mockTokenStorage.storeTokens).toHaveBeenCalledWith(mockResponse.tokens);
      });
    });

    context('with invalid credentials', () => {
      it('should throw AuthenticationError', async () => {
        // Arrange
        const credentials = { email: 'test@example.com', password: 'wrong' };
        mockAuthAdapter.login.mockRejectedValue(new Error('Invalid credentials'));

        // Act & Assert
        await expect(authService.login(credentials)).rejects.toThrow('Invalid credentials');
      });
    });
  });
});
```

```typescript
// Component test
import { render, fireEvent, waitFor } from '@testing-library/react-native';
import { ProductCard } from '../ProductCard';

describe('ProductCard', () => {
  const mockProduct = {
    id: '1',
    name: 'Test Product',
    description: 'Test description',
    riskLevel: 'medium',
  };

  const mockOnPress = jest.fn();

  beforeEach(() => {
    jest.clearAllMocks();
  });

  describe('rendering', () => {
    it('should render product name and description', () => {
      const { getByText } = render(
        <ProductCard product={mockProduct} onPress={mockOnPress} />
      );

      expect(getByText('Test Product')).toBeTruthy();
      expect(getByText('Test description')).toBeTruthy();
    });

    it('should show loading skeleton when isLoading is true', () => {
      const { queryByText } = render(
        <ProductCard product={mockProduct} onPress={mockOnPress} isLoading />
      );

      expect(queryByText('Test Product')).toBeNull();
    });
  });

  describe('interactions', () => {
    it('should call onPress with product when pressed', () => {
      const { getByTestId } = render(
        <ProductCard product={mockProduct} onPress={mockOnPress} />
      );

      fireEvent.press(getByTestId('product-card'));

      expect(mockOnPress).toHaveBeenCalledWith(mockProduct);
      expect(mockOnPress).toHaveBeenCalledTimes(1);
    });
  });
});
```

### 6.2 E2E Test Guidelines

#### E2E Test Structure

```
e2e/
├── auth.test.ts          # Authentication flows
├── products.test.ts      # Product browsing flows
├── portfolio.test.ts    # Portfolio viewing flows
├── chat.test.ts         # Chat functionality
└── config.ts            # Test configuration
```

#### E2E Test Examples (Detox)

```typescript
// e2e/auth.test.ts
describe('Authentication', () => {
  beforeAll(async () => {
    await device.launchApp();
  });

  beforeEach(async () => {
    await device.reloadReactNative();
  });

  describe('Login', () => {
    it('should login successfully with valid credentials', async () => {
      await element(by.id('email-input')).typeText('test@example.com');
      await element(by.id('password-input')).typeText('password123');
      await element(by.id('login-button')).tap();

      // Wait for navigation
      await waitFor(element(by.id('portfolio-screen')))
        .toBeVisible()
        .withTimeout(5000);
    });

    it('should show error with invalid credentials', async () => {
      await element(by.id('email-input')).typeText('wrong@example.com');
      await element(by.id('password-input')).typeText('wrongpassword');
      await element(by.id('login-button')).tap();

      await waitFor(element(by.id('error-message')))
        .toBeVisible()
        .withTimeout(2000);
    });
  });

  describe('PIN Authentication', () => {
    it('should authenticate with valid PIN', async () => {
      // Assume user is logged in and PIN is set
      await device.launchApp({ newInstance: false });
      
      await element(by.id('pin-input')).typeText('123456');
      
      await waitFor(element(by.id('portfolio-screen')))
        .toBeVisible()
        .withTimeout(3000);
    });
  });
});
```

```typescript
// e2e/chat.test.ts
describe('Chat', () => {
  beforeAll(async () => {
    await device.launchApp();
    await loginAsTestUser();
  });

  describe('Sending Messages', () => {
    it('should send and receive messages', async () => {
      // Navigate to chat
      await element(by.id('chat-tab')).tap();
      await waitFor(element(by.id('chat-screen')))
        .toBeVisible()
        .withTimeout(3000);

      // Send message
      const testMessage = `Test message ${Date.now()}`;
      await element(by.id('message-input')).typeText(testMessage);
      await element(by.id('send-button')).tap();

      // Verify message appears in list
      await waitFor(element(by.text(testMessage)))
        .toBeVisible()
        .withTimeout(2000);
    });
  });
});
```

### 6.3 Test Configuration

#### Jest Configuration

```javascript
// jest.config.js
module.exports = {
  preset: 'react-native',
  setupFiles: ['./jest.setup.js'],
  transform: {
    '^.+\\.tsx?$': 'ts-jest',
  },
  transformIgnorePatterns: [
    'node_modules/(?!(react-native|@react-native|@nozbe)/)',
  ],
  moduleNameMapper: {
    '^@/(.*)$': '<rootDir>/src/$1',
    '^@view/(.*)$': '<rootDir>/src/view/$1',
    '^@domain/(.*)$': '<rootDir>/src/domain/$1',
    '^@adapters/(.*)$': '<rootDir>/src/adapters/$1',
    '^@stores/(.*)$': '<rootDir>/src/stores/$1',
    '^@shared/(.*)$': '<rootDir>/src/shared/$1',
  },
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts',
    '!src/**/*.test.{ts,tsx}',
    '!src/**/__tests__/**',
    '!src/**/__mocks__/**',
  ],
  coverageThreshold: {
    global: {
      branches: 70,
      functions: 70,
      lines: 70,
      statements: 70,
    },
  },
  testMatch: ['**/*.test.{ts,tsx}'],
  moduleFileExtensions: ['ts', 'tsx', 'js', 'jsx', 'json'],
};
```

#### Jest Setup

```javascript
// jest.setup.js
import '@testing-library/jest-native/extend-expect';

// Mock native modules
jest.mock('react-native/Libraries/Animated/NativeAnimatedHelper');

// Mock react-native-reanimated
jest.mock('react-native-reanimated', () => {
  const Reanimated = require('react-native-reanimated/mock');
  Reanimated.default.call = () => {};
  return Reanimated;
});

// Mock AsyncStorage
jest.mock('@react-native-async-storage/async-storage', () =>
  require('@react-native-async-storage/async-storage/jest/async-storage-mock')
);

// Silence console warnings in tests
global.console = {
  ...console,
  warn: jest.fn(),
  error: jest.fn(),
};
```

### 6.4 Coverage Requirements

| Layer | Branches | Functions | Lines | Statements |
|-------|----------|-----------|-------|------------|
| **Domain** | 80% | 80% | 80% | 80% |
| **Adapters** | 70% | 70% | 70% | 70% |
| **Components** | 60% | 60% | 60% | 60% |
| **Hooks** | 80% | 80% | 80% | 80% |
| **Overall** | 70% | 70% | 70% | 70% |

#### Coverage Commands

```bash
# Run tests with coverage
npm run test:coverage

# Check coverage thresholds
npm run test:coverage -- --coverageThreshold='{"global":{"branches":70}}'

# Generate coverage report
npm run test:coverage -- --coverageReporters=text,html
```

---

## 7. Code Quality Tools

### 7.1 ESLint Configuration

```javascript
// .eslintrc.js
module.exports = {
  root: true,
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaVersion: 2021,
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true,
    },
  },
  plugins: [
    '@typescript-eslint',
    'react',
    'react-hooks',
    'react-native',
    'import',
    'prettier',
  ],
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:@typescript-eslint/recommended-requiring-type-checking',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'plugin:react-native/all',
    'plugin:import/errors',
    'plugin:import/warnings',
    'plugin:import/typescript',
    'plugin:prettier/recommended',
  ],
  env: {
    'react-native/react-native': true,
    jest: true,
  },
  rules: {
    // TypeScript rules
    '@typescript-eslint/no-explicit-any': 'error',
    '@typescript-eslint/explicit-function-return-type': ['warn', {
      allowExpressions: true,
      allowTypedFunctionExpressions: true,
    }],
    '@typescript-eslint/no-unused-vars': ['error', {
      argsIgnorePattern: '^_',
      varsIgnorePattern: '^_',
    }],
    '@typescript-eslint/no-floating-promises': 'error',
    '@typescript-eslint/await-thenable': 'error',
    '@typescript-eslint/strict-boolean-expressions': 'warn',

    // React rules
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'off',
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',

    // Import rules
    'import/order': ['error', {
      groups: [
        'builtin',
        'external',
        'internal',
        'parent',
        'sibling',
        'index',
      ],
      'newlines-between': 'always',
      alphabetize: { order: 'asc' },
    }],
    'import/no-unresolved': 'error',
    'import/no-cycle': 'error',

    // General rules
    'no-console': ['warn', { allow: ['warn', 'error'] }],
    'prefer-const': 'error',
    'no-var': 'error',
    'eqeqeq': ['error', 'always'],
    'curly': ['error', 'all'],
  },
  settings: {
    react: {
      version: 'detect',
    },
    'import/resolver': {
      typescript: {},
    },
  },
};
```

### 7.2 Prettier Configuration

```javascript
// .prettierrc.js
module.exports = {
  printWidth: 100,
  tabWidth: 2,
  useTabs: false,
  semi: true,
  singleQuote: true,
  quoteProps: 'as-needed',
  trailingComma: 'es5',
  bracketSpacing: true,
  bracketSameLine: false,
  arrowParens: 'always',
  endOfLine: 'lf',
  jsxSingleQuote: false,
};
```

### 7.3 Editor Configuration

```json
// .vscode/settings.json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit",
    "source.organizeImports": "explicit"
  },
  "typescript.tsdk": "node_modules/typescript/lib",
  "typescript.enablePromptUseWorkspaceTsdk": true,
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

```json
// .vscode/extensions.json
{
  "recommendations": [
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "ms-vscode.vscode-typescript-next",
    "dsznajder.es7-react-js-snippets",
    "formulahendry.auto-rename-tag",
    "bradlc.vscode-tailwindcss"
  ]
}
```

---

## 8. Import Organization

### 8.1 Import Order

```typescript
// 1. React and React Native
import React, { useState, useEffect, useCallback } from 'react';
import { View, Text, TouchableOpacity } from 'react-native';

// 2. Third-party libraries
import { useQuery } from '@tanstack/react-query';
import { create } from 'zustand';

// 3. Internal imports (by layer)
import { Button, Card } from '@/view/components/common';
import { useAuth } from '@/view/hooks/useAuth';
import { ProductService } from '@/domain/services/ProductService';
import { ProductAdapter } from '@/adapters/api/ProductAdapter';
import { useProductStore } from '@/stores/productStore';
import { API_ENDPOINTS } from '@/shared/constants';
import { formatCurrency } from '@/shared/utils';

// 4. Types
import type { Product, ProductFilters } from '@/domain/entities/Product';
import type { NativeStackScreenProps } from '@react-navigation/native-stack';

// 5. Styles/assets
import styles from './ProductList.styles';
```

### 8.2 Path Aliases

```json
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@view/*": ["src/view/*"],
      "@domain/*": ["src/domain/*"],
      "@adapters/*": ["src/adapters/*"],
      "@stores/*": ["src/stores/*"],
      "@shared/*": ["src/shared/*"],
      "@components/*": ["src/view/components/*"],
      "@screens/*": ["src/view/screens/*"],
      "@hooks/*": ["src/view/hooks/*"],
      "@navigation/*": ["src/view/navigation/*"],
      "@config/*": ["src/config/*"]
    }
  }
}
```

---

## 9. Documentation Standards

### 9.1 Code Comments

```typescript
/**
 * Calculates the total value of a portfolio based on its positions.
 * 
 * @param positions - Array of portfolio positions
 * @param options - Calculation options
 * @returns Portfolio metrics including total value and returns
 * 
 * @example
 * ```ts
 * const metrics = calculatePortfolioMetrics(positions, { currency: 'RUB' });
 * console.log(metrics.totalValue); // 1000000
 * ```
 */
export function calculatePortfolioMetrics(
  positions: Position[],
  options?: CalculationOptions,
): PortfolioMetrics {
  // Implementation
}

// TODO: Add support for multi-currency portfolios
// FIXME: Performance optimization needed for >500 positions
// HACK: Temporary workaround for API inconsistency
// NOTE: This assumes positions are pre-sorted by value
```

### 9.2 README Structure

```markdown
# Project Name

Brief description of the project.

## Requirements

- Node.js 18+
- React Native CLI
- iOS 13.0+ / Android 8.0+

## Installation

\`\`\`bash
npm install
# iOS
cd ios && pod install
\`\`\`

## Running

\`\`\`bash
# iOS
npm run ios

# Android
npm run android
\`\`\`

## Testing

\`\`\`bash
npm run test
npm run test:coverage
npm run e2e
\`\`\`

## Project Structure

See [docs/design/system-design.md](docs/design/system-design.md)

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md)
```

---

## 10. Summary

This standards document defines the conventions and best practices for the Investment Management Mobile Application. All team members must:

1. **Follow naming conventions** consistently across all code
2. **Adhere to TypeScript standards** with strict type checking
3. **Write tests** meeting minimum coverage requirements
4. **Use proper Git workflow** with meaningful commits and PR descriptions
5. **Maintain code quality** through linting and formatting

**Key Principles:**
- **Consistency** over personal preference
- **Readability** over cleverness
- **Explicitness** over implicit behavior
- **Testing** is not optional
- **Documentation** should be maintained

---

*Technical Standards Document - Version 1.0*  
*Created by System Architect Agent*  
*Date: 2026-04-17*