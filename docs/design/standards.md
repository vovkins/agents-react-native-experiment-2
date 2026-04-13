# Technical Standards and Conventions

## Document Information
| Field | Value |
|-------|-------|
| Project | Wealth Management Mobile App |
| Created | 2026-04-13 |
| Author | System Architect |
| Status | Draft |
| Version | 1.0 |

---

## Table of Contents
1. [Coding Standards](#1-coding-standards)
2. [Naming Conventions](#2-naming-conventions)
3. [Folder Structure](#3-folder-structure)
4. [Git Workflow](#4-git-workflow)
5. [Testing Standards](#5-testing-standards)
6. [Code Review Guidelines](#6-code-review-guidelines)
7. [Documentation Standards](#7-documentation-standards)
8. [Tooling Configuration](#8-tooling-configuration)

---

## 1. Coding Standards

### 1.1 TypeScript/JavaScript Conventions

#### 1.1.1 TypeScript Configuration

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
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "moduleResolution": "node",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "baseUrl": "./src",
    "paths": {
      "@/*": ["./*"],
      "@components/*": ["components/*"],
      "@screens/*": ["screens/*"],
      "@hooks/*": ["hooks/*"],
      "@utils/*": ["utils/*"],
      "@domain/*": ["domain/*"],
      "@data/*": ["data/*"],
      "@infrastructure/*": ["infrastructure/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "babel.config.js", "metro.config.js"]
}
```

#### 1.1.2 Type Definitions

```typescript
// ✅ Good: Explicit type definitions
interface User {
  id: string;
  email: string;
  firstName: string;
  lastName: string;
}

type UserRole = 'admin' | 'manager' | 'client';

// ✅ Good: Using type inference where obvious
const users = ['Alice', 'Bob', 'Charlie']; // string[] inferred

// ✅ Good: Generic types with constraints
interface ApiResponse<T extends object> {
  data: T;
  status: number;
  message: string;
}

// ✅ Good: Utility types
type ReadonlyUser = Readonly<User>;
type PartialUser = Partial<User>;
type UserKeys = keyof User;

// ❌ Bad: Using 'any'
const data: any = fetchData(); // Avoid!

// ✅ Good: Use 'unknown' when type is truly unknown
const data: unknown = fetchData();
if (typeof data === 'object' && data !== null) {
  // Type guard
}
```

#### 1.1.3 Null and Undefined

```typescript
// ✅ Good: Strict null checks
function getUser(id: string): User | null {
  // Return null if not found
}

// ✅ Good: Optional chaining
const userName = user?.profile?.name;

// ✅ Good: Nullish coalescing
const displayName = userName ?? 'Unknown';

// ✅ Good: Type guards
function isUser(obj: unknown): obj is User {
  return typeof obj === 'object' && obj !== null && 'id' in obj;
}

// ❌ Bad: Non-null assertion without check
const name = user!.name; // Dangerous!
```

#### 1.1.4 Functions

```typescript
// ✅ Good: Pure functions with explicit types
function formatCurrency(amount: number, currency: string): string {
  return new Intl.NumberFormat('ru-RU', {
    style: 'currency',
    currency,
  }).format(amount);
}

// ✅ Good: Arrow functions for callbacks
const doubled = numbers.map((n) => n * 2);

// ✅ Good: Default parameters
function greet(name: string, greeting: string = 'Hello'): string {
  return `${greeting}, ${name}!`;
}

// ✅ Good: Function overloads for different signatures
function parseValue(value: string): number;
function parseValue(value: number): string;
function parseValue(value: string | number): string | number {
  return typeof value === 'string' ? parseFloat(value) : value.toString();
}

// ❌ Bad: Function with side effects and no return type
function updateData(data) { // No types, side effects
  globalState = data;
}
```

#### 1.1.5 Async/Await

```typescript
// ✅ Good: Async/await with error handling
async function fetchUser(id: string): Promise<User | null> {
  try {
    const response = await api.get(`/users/${id}`);
    return response.data;
  } catch (error) {
    if (error instanceof ApiError) {
      logger.error('API Error:', error.message);
    }
    return null;
  }
}

// ✅ Good: Parallel async operations
const [users, products] = await Promise.all([
  fetchUsers(),
  fetchProducts(),
]);

// ❌ Bad: Nested promises (callback hell)
fetchUser(id)
  .then((user) => {
    fetchProfile(user.id)
      .then((profile) => {
        // ...
      });
  });
```

### 1.2 React Native Best Practices

#### 1.2.1 Component Structure

```typescript
// ✅ Good: Functional component with proper typing
interface ButtonProps {
  title: string;
  onPress: () => void;
  variant?: 'primary' | 'secondary' | 'outline';
  disabled?: boolean;
  loading?: boolean;
}

export const Button: React.FC<ButtonProps> = ({
  title,
  onPress,
  variant = 'primary',
  disabled = false,
  loading = false,
}) => {
  const styles = useStyles(variant);
  
  return (
    <TouchableOpacity
      onPress={onPress}
      disabled={disabled || loading}
      style={styles.container}
      activeOpacity={0.7}
    >
      {loading ? (
        <ActivityIndicator color={styles.text.color} />
      ) : (
        <Text style={styles.text}>{title}</Text>
      )}
    </TouchableOpacity>
  );
};
```

#### 1.2.2 Hooks Usage

```typescript
// ✅ Good: Custom hooks for reusable logic
function useUser(userId: string) {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);

  useEffect(() => {
    let mounted = true;
    
    async function fetchUser() {
      try {
        setLoading(true);
        const data = await userService.getById(userId);
        if (mounted) {
          setUser(data);
        }
      } catch (err) {
        if (mounted) {
          setError(err instanceof Error ? err : new Error('Unknown error'));
        }
      } finally {
        if (mounted) {
          setLoading(false);
        }
      }
    }
    
    fetchUser();
    
    return () => {
      mounted = false;
    };
  }, [userId]);

  return { user, loading, error };
}

// ✅ Good: useMemo for expensive calculations
const sortedProducts = useMemo(() => {
  return products.sort((a, b) => a.name.localeCompare(b.name));
}, [products]);

// ✅ Good: useCallback for event handlers passed to children
const handlePress = useCallback((id: string) => {
  navigation.navigate('ProductDetail', { id });
}, [navigation]);

// ❌ Bad: Missing dependency array
useEffect(() => {
  fetchUser(userId);
}); // Missing dependencies!
```

#### 1.2.3 Performance Optimizations

```typescript
// ✅ Good: Use memo for expensive component renders
export const ProductCard = memo(({ product }: ProductCardProps) => {
  return (
    <View style={styles.card}>
      <Text>{product.name}</Text>
    </View>
  );
});

// ✅ Good: Use FlashList for long lists
import { FlashList } from '@shopify/flash-list";

<FlashList
  data={products}
  renderItem={({ item }) => <ProductCard product={item} />}
  estimatedItemSize={100}
  keyExtractor={(item) => item.id}
/>

// ✅ Good: Lazy load screens
const ProductsScreen = lazy(() => import('./ProductsScreen'));

// ❌ Bad: Inline functions in render
<Button onPress={() => console.log('pressed')} /> // Creates new function on each render
```

#### 1.2.4 Styling

```typescript
// ✅ Good: Use NativeWind (Tailwind for React Native)
import { View, Text } from 'react-native';
import { styled } from 'nativewind";

const StyledView = styled(View);
const StyledText = styled(Text);

export const Card = () => (
  <StyledView className="bg-white rounded-lg p-4 shadow-md">
    <StyledText className="text-lg font-semibold text-gray-900">
      Title
    </StyledText>
  </StyledView>
);

// ✅ Good: StyleSheet for complex styles
import { StyleSheet } from 'react-native";

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#FFFFFF',
    padding: 16,
  },
  title: {
    fontSize: 18,
    fontWeight: '600',
    color: '#1A1A1A',
  },
});

// ❌ Bad: Inline styles
<View style={{ flex: 1, backgroundColor: 'white', padding: 16 }}>
```

#### 1.2.5 Platform-Specific Code

```typescript
// ✅ Good: Platform-specific styling
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.25,
        shadowRadius: 4,
      },
      android: {
        elevation: 4,
      },
    }),
  },
});

// ✅ Good: Platform-specific files
// Button.ios.tsx
// Button.android.tsx
// Button.tsx (default)

// ✅ Good: Platform-specific logic
if (Platform.OS === 'ios') {
  // iOS-specific code
}
```

### 1.3 Node.js Patterns

#### 1.3.1 Error Handling

```typescript
// ✅ Good: Custom error classes
class AppError extends Error {
  constructor(
    message: string,
    public code: string,
    public statusCode: number = 500
  ) {
    super(message);
    this.name = 'AppError';
  }
}

class ValidationError extends AppError {
  constructor(message: string) {
    super(message, 'VALIDATION_ERROR', 400);
    this.name = 'ValidationError';
  }
}

class NotFoundError extends AppError {
  constructor(resource: string) {
    super(`${resource} not found`, 'NOT_FOUND', 404);
    this.name = 'NotFoundError';
  }
}

// ✅ Good: Error handling middleware
app.use((err: Error, req: Request, res: Response, next: NextFunction) => {
  if (err instanceof AppError) {
    return res.status(err.statusCode).json({
      error: {
        code: err.code,
        message: err.message,
      },
    });
  }
  
  logger.error('Unhandled error:', err);
  return res.status(500).json({
    error: {
      code: 'INTERNAL_ERROR',
      message: 'An unexpected error occurred',
    },
  });
});
```

#### 1.3.2 Environment Configuration

```typescript
// ✅ Good: Environment configuration
import z from 'zod';

const envSchema = z.object({
  NODE_ENV: z.enum(['development', 'test', 'production']),
  PORT: z.string().transform(Number).default('3000'),
  DATABASE_URL: z.string(),
  JWT_SECRET: z.string().min(32),
  API_BASE_URL: z.string().url(),
});

type Env = z.infer<typeof envSchema>;

function loadEnv(): Env {
  const result = envSchema.safeParse(process.env);
  
  if (!result.success) {
    console.error('Invalid environment variables:', result.error.flatten());
    process.exit(1);
  }
  
  return result.data;
}

export const env = loadEnv();
```

---

## 2. Naming Conventions

### 2.1 Files and Folders

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `Button.tsx`, `ProductCard.tsx` |
| Screens | PascalCase + Screen suffix | `LoginScreen.tsx`, `ProductsScreen.tsx` |
| Hooks | camelCase + use prefix | `useAuth.ts`, `useProducts.ts` |
| Utilities | camelCase | `formatDate.ts`, `validators.ts` |
| Constants | camelCase or SCREAMING_SNAKE_CASE | `constants.ts`, `API_ENDPOINTS.ts` |
| Types/Interfaces | PascalCase | `User.ts`, `ApiResponse.ts` |
| Stores | camelCase + Store suffix | `authStore.ts`, `productsStore.ts` |
| API clients | camelCase + .api suffix | `auth.api.ts`, `products.api.ts` |
| Tests | Same as source + .test | `Button.test.tsx`, `useAuth.test.ts` |

#### Folder Naming

```
src/
├── components/           # kebab-case for subfolders
│   ├── product-card/
│   │   ├── ProductCard.tsx
│   │   ├── ProductCard.styles.ts
│   │   ├── ProductCard.types.ts
│   │   └── index.ts
│   └── user-avatar/
│
├── screens/              # kebab-case for subfolders
│   ├── product-detail/
│   │   ├── ProductDetailScreen.tsx
│   │   ├── ProductDetailScreen.styles.ts
│   │   └── index.ts
│
├── domain/
│   ├── entities/         # PascalCase for entity files
│   │   ├── User.ts
│   │   ├── Product.ts
│   │   └── Portfolio.ts
│   ├── usecases/         # camelCase for use case files
│   │   ├── loginUser.ts
│   │   ├── fetchProducts.ts
│   │   └── sendMessage.ts
│   └── validators/       # camelCase for validator files
│       ├── emailValidator.ts
│       └── passwordValidator.ts
```

### 2.2 Variables and Functions

| Type | Convention | Example |
|------|------------|---------|
| Variables | camelCase | `userName`, `totalAmount` |
| Constants | SCREAMING_SNAKE_CASE | `MAX_RETRY_COUNT`, `API_BASE_URL` |
| Boolean variables | camelCase + is/has/should prefix | `isLoading`, `hasError`, `shouldRender` |
| Functions | camelCase | `fetchUser`, `calculateTotal` |
| Event handlers | handle + Event name | `handlePress`, `handleSubmit`, `handleInputChange` |
| Async functions | verb describing action | `fetchUsers`, `saveData`, `deleteItem` |
| Private methods | _ prefix (optional) | `_validateInput`, `_formatData` |

```typescript
// ✅ Good
const isLoading = true;
const hasPermission = false;
const maxRetryCount = 3;
const API_BASE_URL = 'https://api.example.com';

function fetchUserById(id: string): Promise<User> { }
function handleButtonPress(): void { }
function formatCurrency(amount: number): string { }

// ❌ Bad
const loading = true; // Missing 'is' prefix for boolean
const MaxRetryCount = 3; // Should be SCREAMING_SNAKE_CASE for constant
const button_pressed = false; // Wrong convention

function getUser() { } // Async function without verb
function onClick() { } // Missing 'handle' prefix
```

### 2.3 Components

| Type | Convention | Example |
|------|------------|---------|
| Component name | PascalCase | `ProductCard`, `UserAvatar` |
| Props interface | Component + Props | `ProductCardProps`, `UserAvatarProps` |
| Ref interface | Component + Ref | `ProductCardRef`, `UserAvatarRef` |
| Component file | PascalCase.tsx | `ProductCard.tsx` |
| Styles file | Component.styles.ts | `ProductCard.styles.ts` |
| Types file | Component.types.ts | `ProductCard.types.ts` |

```typescript
// ProductCard.tsx
interface ProductCardProps {
  product: Product;
  onPress: (id: string) => void;
  variant?: 'compact' | 'full';
}

export const ProductCard: React.FC<ProductCardProps> = ({
  product,
  onPress,
  variant = 'full',
}) => {
  return (
    <TouchableOpacity onPress={() => onPress(product.id)}>
      {/* ... */}
    </TouchableOpacity>
  );
};
```

### 2.4 API Endpoints

| Type | Convention | Example |
|------|------------|---------|
| Endpoint path | kebab-case, plural nouns | `/api/users`, `/api/products` |
| Resource ID | :id param | `/api/users/:id` |
| Nested resources | parent/child | `/api/users/:id/portfolios` |
| Actions | verb after resource | `/api/users/:id/activate` |
| Query params | camelCase | `?pageSize=10&sortBy=name` |

```
# RESTful API Endpoints

POST   /api/auth/login
POST   /api/auth/logout
POST   /api/auth/refresh
POST   /api/auth/forgot-password

GET    /api/users/me
PATCH  /api/users/me
DELETE /api/users/me

GET    /api/products
GET    /api/products/:id
GET    /api/products/:id/documents

GET    /api/portfolio
GET    /api/portfolio/history
GET    /api/portfolio/assets/:assetId

GET    /api/chat/messages
POST   /api/chat/messages
PATCH  /api/chat/messages/:id/read
```

---

## 3. Folder Structure

### 3.1 Frontend (React Native) Structure

```
project-root/
├── src/
│   ├── components/
│   │   ├── ui/                      # Base UI components
│   │   │   ├── Button/
│   │   │   │   ├── Button.tsx
│   │   │   │   ├── Button.styles.ts
│   │   │   │   ├── Button.types.ts
│   │   │   │   ├── Button.test.tsx
│   │   │   │   └── index.ts
│   │   │   ├── Input/
│   │   │   ├── Card/
│   │   │   ├── Modal/
│   │   │   ├── Spinner/
│   │   │   └── index.ts             # Barrel export
│   │   │
│   │   ├── features/                # Feature-specific components
│   │   │   ├── auth/
│   │   │   │   ├── LoginForm.tsx
│   │   │   │   ├── RegisterForm.tsx
│   │   │   │   └── index.ts
│   │   │   ├── products/
│   │   │   │   ├── ProductCard.tsx
│   │   │   │   ├── ProductList.tsx
│   │   │   │   ├── ProductDetails.tsx
│   │   │   │   └── index.ts
│   │   │   ├── portfolio/
│   │   │   │   ├── PortfolioChart.tsx
│   │   │   │   ├── AssetList.tsx
│   │   │   │   └── index.ts
│   │   │   └── chat/
│   │   │       ├── MessageBubble.tsx
│   │   │       ├── MessageInput.tsx
│   │   │       └── index.ts
│   │   │
│   │   └── layout/                  # Layout components
│   │       ├── Header/
│   │       ├── TabBar/
│   │       ├── SafeAreaWrapper/
│   │       └── index.ts
│   │
│   ├── screens/                     # Screen components
│   │   ├── auth/
│   │   │   ├── LoginScreen.tsx
│   │   │   ├── RegisterScreen.tsx
│   │   │   ├── ForgotPasswordScreen.tsx
│   │   │   └── index.ts
│   │   ├── products/
│   │   │   ├── ProductsScreen.tsx
│   │   │   ├── ProductDetailScreen.tsx
│   │   │   └── index.ts
│   │   ├── portfolio/
│   │   │   ├── PortfolioScreen.tsx
│   │   │   ├── PortfolioHistoryScreen.tsx
│   │   │   └── index.ts
│   │   ├── chat/
│   │   │   ├── ChatScreen.tsx
│   │   │   └── index.ts
│   │   ├── profile/
│   │   │   ├── ProfileScreen.tsx
│   │   │   ├── SettingsScreen.tsx
│   │   │   └── index.ts
│   │   └── index.ts
│   │
│   ├── navigation/                  # Navigation configuration
│   │   ├── RootNavigator.tsx
│   │   ├── AuthNavigator.tsx
│   │   ├── MainNavigator.tsx
│   │   ├── linking.ts               # Deep linking config
│   │   ├── types.ts                 # Navigation types
│   │   └── index.ts
│   │
│   ├── domain/                      # Domain layer (business logic)
│   │   ├── entities/                # Business entities
│   │   │   ├── User.ts
│   │   │   ├── Product.ts
│   │   │   ├── Portfolio.ts
│   │   │   ├── Message.ts
│   │   │   └── index.ts
│   │   ├── usecases/                # Business logic / use cases
│   │   │   ├── auth/
│   │   │   │   ├── loginUser.ts
│   │   │   │   ├── logoutUser.ts
│   │   │   │   └── index.ts
│   │   │   ├── products/
│   │   │   │   ├── fetchProducts.ts
│   │   │   │   └── index.ts
│   │   │   ├── portfolio/
│   │   │   │   ├── fetchPortfolio.ts
│   │   │   │   └── index.ts
│   │   │   ├── chat/
│   │   │   │   ├── sendMessage.ts
│   │   │   │   ├── fetchMessages.ts
│   │   │   │   └── index.ts
│   │   │   └── index.ts
│   │   ├── validators/              # Input validation
│   │   │   ├── emailValidator.ts
│   │   │   ├── passwordValidator.ts
│   │   │   ├── phoneValidator.ts
│   │   │   └── index.ts
│   │   ├── types/                   # Shared types
│   │   │   ├── common.ts
│   │   │   ├── api.ts
│   │   │   └── index.ts
│   │   └── index.ts
│   │
│   ├── data/                        # Data layer
│   │   ├── stores/                  # Zustand stores
│   │   │   ├── authStore.ts
│   │   │   ├── productsStore.ts
│   │   │   ├── portfolioStore.ts
│   │   │   ├── chatStore.ts
│   │   │   ├── userStore.ts
│   │   │   ├── appStore.ts
│   │   │   └── index.ts
│   │   ├── repositories/            # Data repositories
│   │   │   ├── AuthRepository.ts
│   │   │   ├── ProductsRepository.ts
│   │   │   ├── PortfolioRepository.ts
│   │   │   ├── ChatRepository.ts
│   │   │   └── index.ts
│   │   ├── cache/                   # React Query cache
│   │   │   ├── queryClient.ts
│   │   │   ├── queryKeys.ts
│   │   │   └── index.ts
│   │   ├── storage/                 # Local storage
│   │   │   ├── mmkv.ts
│   │   │   ├── database.ts
│   │   │   ├── migrations/
│   │   │   │   ├── 001_initial.ts
│   │   │   │   └── index.ts
│   │   │   └── index.ts
│   │   └── index.ts
│   │
│   ├── infrastructure/              # Infrastructure layer
│   │   ├── api/                     # API clients
│   │   │   ├── client.ts            # Axios instance
│   │   │   ├── interceptors.ts
│   │   │   ├── auth.api.ts
│   │   │   ├── products.api.ts
│   │   │   ├── portfolio.api.ts
│   │   │   ├── chat.api.ts
│   │   │   ├── users.api.ts
│   │   │   └── index.ts
│   │   ├── websocket/               # WebSocket client
│   │   │   ├── client.ts
│   │   │   ├── handlers.ts
│   │   │   ├── types.ts
│   │   │   └── index.ts
│   │   ├── auth/                    # Auth services
│   │   │   ├── tokenManager.ts
│   │   │   ├── biometrics.ts
│   │   │   └── index.ts
│   │   ├── push/                    # Push notifications
│   │   │   ├── index.ts
│   │   │   ├── handlers.ts
│   │   │   └── permissions.ts
│   │   └── index.ts
│   │
│   ├── hooks/                       # Custom React hooks
│   │   ├── useAuth.ts
│   │   ├── useProducts.ts
│   │   ├── usePortfolio.ts
│   │   ├── useChat.ts
│   │   ├── useTheme.ts
│   │   ├── useNetwork.ts
│   │   └── index.ts
│   │
│   ├── utils/                       # Utility functions
│   │   ├── formatting.ts
│   │   ├── validation.ts
│   │   ├── network.ts
│   │   ├── helpers.ts
│   │   ├── constants.ts
│   │   └── index.ts
│   │
│   ├── config/                      # App configuration
│   │   ├── app.ts
│   │   ├── environment.ts
│   │   ├── theme.ts
│   │   └── index.ts
│   │
│   ├── i18n/                        # Internationalization
│   │   ├── ru/
│   │   │   ├── common.ts
│   │   │   ├── auth.ts
│   │   │   ├── products.ts
│   │   │   └── index.ts
│   │   └── index.ts
│   │
│   └── App.tsx                      # App entry point
│
├── android/                         # Android native code
│   ├── app/
│   ├── gradle/
│   └── build.gradle
│
├── ios/                             # iOS native code
│   ├── ProjectName/
│   └── Podfile
│
├── e2e/                             # E2E tests (Detox)
│   ├── auth.test.ts
│   ├── products.test.ts
│   ├── portfolio.test.ts
│   └── chat.test.ts
│
├── docs/                            # Documentation
│   ├── adr/                         # Architecture Decision Records
│   ├── design/                      # Design documents
│   └── requirements/                # Requirements documents
│
├── .github/                         # GitHub workflows
│   ├── workflows/
│   │   ├── ci.yml
│   │   └── deploy.yml
│   └── PULL_REQUEST_TEMPLATE.md
│
├── package.json
├── tsconfig.json
├── .eslintrc.js
├── .prettierrc.js
├── .gitignore
├── README.md
└── jest.config.js
```

### 3.2 Module Structure (Feature-Based)

For each feature module, follow this structure:

```
features/
└── products/
    ├── components/           # Feature-specific components
    │   ├── ProductCard.tsx
    │   ├── ProductList.tsx
    │   └── ProductFilters.tsx
    ├── screens/              # Feature screens
    │   ├── ProductsScreen.tsx
    │   └── ProductDetailScreen.tsx
    ├── hooks/                # Feature-specific hooks
    │   ├── useProducts.ts
    │   └── useProductFilters.ts
    ├── api/                  # Feature API calls
    │   └── products.api.ts
    ├── store/                # Feature state
    │   └── productsStore.ts
    ├── types/                # Feature types
    │   └── products.types.ts
    ├── utils/                # Feature utilities
    │   └── productHelpers.ts
    ├── __tests__/            # Feature tests
    │   ├── ProductCard.test.tsx
    │   └── useProducts.test.ts
    └── index.ts              # Public API (exports)
```

---

## 4. Git Workflow

### 4.1 Branch Naming

| Branch Type | Pattern | Example |
|-------------|---------|---------|
| Feature | `feature/ticket-id-description` | `feature/WM-123-add-login-screen` |
| Bug Fix | `fix/ticket-id-description` | `fix/WM-456-fix-auth-redirect` |
| Hotfix | `hotfix/ticket-id-description` | `hotfix/WM-789-crash-on-submit` |
| Release | `release/version` | `release/1.0.0` |
| Develop | `develop` | `develop` |
| Main | `main` | `main` |

### 4.2 Branch Strategy

```
main ─────●─────●─────●─────●─────●─────
          │           │           │
release ──└──●────●───┘           │
              v1.0.0              │
                                  │
develop ─────●─────●─────●─────●───┘
             │           │
feature ─────┘           │
  WM-123                  │
                         │
feature ─────────────────┘
  WM-456
```

**Workflow:**
1. Create branch from `develop`
2. Work on feature/fix
3. Create PR to `develop`
4. After approval, merge to `develop`
5. When ready for release, create release branch
6. Test on release branch
7. Merge release to `main` and `develop`
8. Tag release on `main`

### 4.3 Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

#### Types

| Type | Description |
|------|-------------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation changes |
| `style` | Code style changes (formatting, etc.) |
| `refactor` | Code refactoring |
| `perf` | Performance improvements |
| `test` | Adding or modifying tests |
| `chore` | Build process or auxiliary tool changes |
| `ci` | CI/CD configuration changes |
| `revert` | Reverting a previous commit |

#### Examples

```bash
# Feature
feat(auth): add biometric login support

Implement Face ID/Touch ID login for iOS and Android.
Users can now enable biometric authentication from settings.

Closes #WM-123

# Bug fix
fix(products): resolve pagination issue in product list

The product list was not loading subsequent pages when
scrolling. Added proper page tracking to the query.

Fixes #WM-456

# Breaking change
feat(api)!: change authentication endpoint response

The /auth/login endpoint now returns user profile data
along with tokens.

BREAKING CHANGE: Token structure has changed. Frontend
needs to be updated to handle new response format.

# Documentation
docs(readme): update installation instructions

Added Android setup instructions and troubleshooting tips.

# Refactoring
refactor(portfolio): extract chart rendering to separate component

Moved portfolio chart logic to PortfolioChart component
for better separation of concerns.
```

### 4.4 Pull Request Guidelines

#### PR Title Format

```
[WM-123] Add biometric login support
[WM-456] Fix pagination issue in product list
[WM-789] Refactor portfolio chart component
```

#### PR Description Template

```markdown
## Description
<!-- Brief description of changes -->

## Type of Change
- [ ] 🚀 New feature (feat)
- [ ] 🐛 Bug fix (fix)
- [ ] 📝 Documentation (docs)
- [ ] ♻️ Refactoring (refactor)
- [ ] ⚡ Performance improvement (perf)
- [ ] ✅ Test (test)
- [ ] 🔧 Chore (chore)

## Related Tickets
Closes #WM-123

## Screenshots
<!-- Add screenshots if applicable -->

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] E2E tests added/updated
- [ ] Manual testing completed

## Checklist
- [ ] Code follows coding standards
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
- [ ] No new warnings introduced
- [ ] Tests pass locally
- [ ] Code coverage maintained/improved

## Additional Notes
<!-- Any additional information for reviewers -->
```

#### PR Review Process

1. **Self-Review**: Author reviews their own code
2. **Automated Checks**: CI/CD pipeline runs tests, linting
3. **Code Review**: At least one approval required
4. **QA Review**: For significant changes
5. **Merge**: Squash and merge to develop

---

## 5. Testing Standards

### 5.1 Test File Organization

```
src/
├── components/
│   └── Button/
│       ├── Button.tsx
│       └── Button.test.tsx       # Co-located test file
│
├── hooks/
│   ├── useAuth.ts
│   └── __tests__/                # __tests__ folder for complex modules
│       ├── useAuth.test.ts
│       └── useAuth.mocks.ts
│
└── domain/
    └── validators/
        ├── emailValidator.ts
        └── emailValidator.test.ts
```

### 5.2 Unit Test Requirements

#### What to Test

| Layer | What to Test |
|-------|-------------|
| Domain | Use cases, validators, business logic |
| Data | Stores, repositories, cache logic |
| Infrastructure | API clients, services |
| Components | UI components (critical flows) |
| Hooks | Custom hooks |

#### Test Structure (AAA Pattern)

```typescript
describe('useAuth', () => {
  describe('login', () => {
    it('should set user and token on successful login', async () => {
      // Arrange
      const mockUser = { id: '1', email: 'test@example.com' };
      const mockToken = 'test-token';
      mockAuthAPI.login.mockResolvedValue({ user: mockUser, token: mockToken });

      // Act
      const { result } = renderHook(() => useAuth());
      await act(async () => {
        await result.current.login('test@example.com', 'password');
      });

      // Assert
      expect(result.current.user).toEqual(mockUser);
      expect(result.current.isAuthenticated).toBe(true);
    });

    it('should set error on failed login', async () => {
      // Arrange
      const mockError = new Error('Invalid credentials');
      mockAuthAPI.login.mockRejectedValue(mockError);

      // Act
      const { result } = renderHook(() => useAuth());
      await act(async () => {
        try {
          await result.current.login('test@example.com', 'wrong');
        } catch (error) {
          // Expected
        }
      });

      // Assert
      expect(result.current.error).toBe('Invalid credentials');
      expect(result.current.isAuthenticated).toBe(false);
    });
  });
});
```

#### Component Testing

```typescript
import { render, fireEvent, waitFor } from '@testing-library/react-native';
import { Button } from './Button';

describe('Button', () => {
  const defaultProps = {
    title: 'Click me',
    onPress: jest.fn(),
  };

  beforeEach(() => {
    jest.clearAllMocks();
  });

  it('should render title correctly', () => {
    const { getByText } = render(<Button {...defaultProps} />);
    
    expect(getByText('Click me')).toBeTruthy();
  });

  it('should call onPress when pressed', () => {
    const { getByText } = render(<Button {...defaultProps} />);
    
    fireEvent.press(getByText('Click me'));
    
    expect(defaultProps.onPress).toHaveBeenCalledTimes(1);
  });

  it('should not call onPress when disabled', () => {
    const { getByText } = render(<Button {...defaultProps} disabled />);
    
    fireEvent.press(getByText('Click me'));
    
    expect(defaultProps.onPress).not.toHaveBeenCalled();
  });

  it('should show loading indicator when loading', () => {
    const { queryByText, getByTestId } = render(
      <Button {...defaultProps} loading />
    );
    
    expect(queryByText('Click me')).toBeNull();
    expect(getByTestId('activity-indicator')).toBeTruthy();
  });
});
```

### 5.3 Integration Test Guidelines

```typescript
// tests/integration/auth.flow.test.ts
describe('Authentication Flow', () => {
  it('should allow user to login and access protected content', async () => {
    // Start from login screen
    const { getByPlaceholderText, getByText } = render(<App />);
    
    // Enter credentials
    fireEvent.changeText(
      getByPlaceholderText('Email'),
      'test@example.com'
    );
    fireEvent.changeText(
      getByPlaceholderText('Password'),
      'password123'
    );
    
    // Submit login
    fireEvent.press(getByText('Login'));
    
    // Wait for navigation to main screen
    await waitFor(() => {
      expect(getByText('Welcome, Test User')).toBeTruthy();
    });
  });
});
```

### 5.4 E2E Test Guidelines (Detox)

```typescript
// e2e/auth.test.ts
describe('Authentication', () => {
  beforeAll(async () => {
    await device.launchApp();
  });

  beforeEach(async () => {
    await device.reloadReactNative();
  });

  it('should login successfully with valid credentials', async () => {
    await element(by.id('email-input')).typeText('test@example.com');
    await element(by.id('password-input')).typeText('password123\n');
    await element(by.id('login-button')).tap();
    
    await expect(element(by.text('Welcome'))).toBeVisible();
  });

  it('should show error with invalid credentials', async () => {
    await element(by.id('email-input')).typeText('wrong@example.com');
    await element(by.id('password-input')).typeText('wrongpassword\n');
    await element(by.id('login-button')).tap();
    
    await expect(element(by.text('Invalid credentials'))).toBeVisible();
  });
});
```

### 5.5 Test Coverage Requirements

| Layer | Minimum Coverage | Target Coverage |
|-------|-----------------|-----------------|
| Domain | 90% | 95% |
| Data | 80% | 90% |
| Infrastructure | 70% | 80% |
| Components | 60% | 75% |
| Hooks | 80% | 90% |
| **Overall** | **70%** | **80%** |

#### Coverage Configuration

```javascript
// jest.config.js
module.exports = {
  preset: 'react-native',
  setupFiles: ['./jest.setup.js'],
  transform: {
    '^.+\\.tsx?$': 'ts-jest',
  },
  moduleFileExtensions: ['ts', 'tsx', 'js', 'jsx', 'json'],
  collectCoverage: true,
  coverageDirectory: 'coverage',
  coverageReporters: ['text', 'lcov', 'html'],
  coverageThreshold: {
    global: {
      branches: 70,
      functions: 70,
      lines: 70,
      statements: 70,
    },
    './src/domain': {
      branches: 90,
      functions: 90,
      lines: 90,
      statements: 90,
    },
  },
  moduleNameMapper: {
    '^@/(.*)$': '<rootDir>/src/$1',
    '^@components/(.*)$': '<rootDir>/src/components/$1',
    '^@screens/(.*)$': '<rootDir>/src/screens/$1',
  },
};
```

---

## 6. Code Review Guidelines

### 6.1 Code Review Checklist

#### Functionality
- [ ] Code does what it's supposed to do
- [ ] Edge cases are handled
- [ ] Error handling is appropriate
- [ ] No regressions introduced

#### Code Quality
- [ ] Follows coding standards
- [ ] DRY principle followed
- [ ] No code duplication
- [ ] Functions/methods are not too long
- [ ] Complex logic is documented
- [ ] No commented-out code

#### Performance
- [ ] No unnecessary re-renders (React)
- [ ] Appropriate use of memoization
- [ ] Efficient algorithms
- [ ] No memory leaks

#### Security
- [ ] No sensitive data exposed
- [ ] Input validation present
- [ ] Proper authentication/authorization
- [ ] No SQL injection vulnerabilities

#### Testing
- [ ] Tests are meaningful
- [ ] Test coverage maintained
- [ ] Edge cases tested
- [ ] Tests are not flaky

### 6.2 Review Process

1. **Author**: Create PR, fill template, self-review
2. **Reviewer**: Review within 24 hours
3. **Discussion**: Resolve comments constructively
4. **Approval**: At least one approval required
5. **Merge**: Author merges after approval

### 6.3 Review Comments Format

```markdown
# Question (for clarification)
**Question:** Is this the right approach for...?

# Suggestion (non-blocking)
**Suggestion:** Consider using useMemo here for performance.

# Issue (blocking)
**Issue:** This will cause a memory leak. The subscription needs to be cleaned up in useEffect return.

# Nitpick (non-blocking, minor)
**Nitpick:** Typo in variable name: `userNmae` should be `userName`.
```

---

## 7. Documentation Standards

### 7.1 Code Documentation

#### File Headers

```typescript
/**
 * @file Button component for the wealth management app
 * @description A reusable button component with multiple variants
 * @author Your Name
 * @created 2026-04-13
 * @lastModified 2026-04-13
 */
```

#### Function/Method Documentation

```typescript
/**
 * Formats a number as currency according to locale
 * 
 * @param amount - The numeric amount to format
 * @param currency - The ISO 4217 currency code (e.g., 'RUB', 'USD')
 * @param locale - The locale string (default: 'ru-RU')
 * @returns The formatted currency string
 * 
 * @example
 * ```typescript
 * formatCurrency(1234.56, 'RUB'); // '1 234,56 ₽'
 * formatCurrency(1234.56, 'USD', 'en-US'); // '$1,234.56'
 * ```
 */
export function formatCurrency(
  amount: number,
  currency: string,
  locale: string = 'ru-RU'
): string {
  // Implementation
}
```

#### Component Documentation

```typescript
/**
 * Button component with multiple variants and states
 * 
 * @example
 * ```tsx
 * <Button
 *   title="Submit"
 *   onPress={handleSubmit}
 *   variant="primary"
 *   loading={isLoading}
 * />
 * ```
 */
interface ButtonProps {
  /** The text to display on the button */
  title: string;
  /** Callback function called when button is pressed */
  onPress: () => void;
  /** Visual style variant */
  variant?: 'primary' | 'secondary' | 'outline';
  /** Whether the button is disabled */
  disabled?: boolean;
  /** Whether to show a loading indicator */
  loading?: boolean;
}
```

### 7.2 README Structure

```markdown
# Project Name

Brief description of the project.

## Table of Contents
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Running the App](#running-the-app)
- [Testing](#testing)
- [Project Structure](#project-structure)
- [Contributing](#contributing)

## Features
- Feature 1
- Feature 2

## Requirements
- Node.js >= 18.x
- React Native CLI
- Xcode (iOS)
- Android Studio (Android)

## Installation

\`\`\`bash
npm install
# iOS
cd ios && pod install
\`\`\`

## Running the App

\`\`\`bash
# iOS
npm run ios

# Android
npm run android
\`\`\`

## Testing

\`\`\`bash
npm test
npm run test:coverage
npm run test:e2e
\`\`\`

## Project Structure

Brief explanation of folder structure.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md)

## License

MIT
```

---

## 8. Tooling Configuration

### 8.1 ESLint Configuration

```javascript
// .eslintrc.js
module.exports = {
  root: true,
  extends: [
    'eslint:recommended',
    '@react-native-community',
    'plugin:react-hooks/recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:import/recommended',
    'plugin:import/typescript',
    'prettier',
  ],
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint', 'import'],
  settings: {
    react: {
      version: 'detect',
    },
    'import/resolver': {
      typescript: {},
    },
  },
  rules: {
    // TypeScript
    '@typescript-eslint/no-unused-vars': ['error', { argsIgnorePattern: '^_' }],
    '@typescript-eslint/explicit-function-return-type': 'off',
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    '@typescript-eslint/no-explicit-any': 'error',
    '@typescript-eslint/no-non-null-assertion': 'warn',

    // React
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
    'react-native/no-inline-styles': 'warn',
    'react-native/no-color-literals': 'off',
    'react-native/no-raw-text': 'off',

    // Import
    'import/order': [
      'error',
      {
        groups: ['builtin', 'external', 'internal', 'parent', 'sibling', 'index'],
        'newlines-between': 'always',
        alphabetize: { order: 'asc', caseInsensitive: true },
      },
    ],
    'import/no-duplicates': 'error',

    // General
    'no-console': ['warn', { allow: ['warn', 'error'] }],
    'prefer-const': 'error',
    'no-var': 'error',
    eqeqeq: ['error', 'always'],
  },
};
```

### 8.2 Prettier Configuration

```javascript
// .prettierrc.js
module.exports = {
  arrowParens: 'always',
  bracketSameLine: false,
  bracketSpacing: true,
  singleQuote: true,
  trailingComma: 'all',
  semi: true,
  printWidth: 100,
  tabWidth: 2,
  useTabs: false,
  endOfLine: 'lf',
};
```

### 8.3 Editor Configuration

```ini
# .editorconfig
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
indent_style = space
indent_size = 2

[*.md]
trim_trailing_whitespace = false

[*.{yml,yaml}]
indent_size = 2
```

### 8.4 VS Code Settings

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
  "files.associations": {
    "*.tsx": "typescriptreact"
  },
  "files.exclude": {
    "**/.git": true,
    "**/.DS_Store": true,
    "**/node_modules": true,
    "**/.idea": true
  },
  "search.exclude": {
    "**/node_modules": true,
    "**/coverage": true,
    "**/.git": true
  }
}
```

### 8.5 VS Code Extensions

```json
// .vscode/extensions.json
{
  "recommendations": [
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "ms-vscode.vscode-typescript-next",
    "dsznajder.es7-react-js-snippets",
    "formulahendry.auto-rename-tag",
    "naumovs.color-highlight",
    "streetsidesoftware.code-spell-checker",
    "usernamehw.errorlens",
    "eamodio.gitlens",
    "msjsdiag.vscode-react-native"
  ]
}
```

---

## 9. Enforcing Standards

### 9.1 Pre-commit Hooks (Husky)

```json
// package.json
{
  "scripts": {
    "prepare": "husky install",
    "lint": "eslint src --ext .ts,.tsx",
    "lint:fix": "eslint src --ext .ts,.tsx --fix",
    "format": "prettier --write \"src/**/*.{ts,tsx}\"",
    "test": "jest",
    "test:coverage": "jest --coverage",
    "type-check": "tsc --noEmit"
  },
  "lint-staged": {
    "*.{ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

```bash
# .husky/pre-commit
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
npm run type-check
```

```bash
# .husky/pre-push
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npm run test
```

### 9.2 CI/CD Checks

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run type-check

  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - run: npm run test:coverage
      - name: Upload coverage
        uses: codecov/codecov-action@v3

  build-android:
    runs-on: ubuntu-latest
    needs: [lint, test]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'
      - run: cd android && ./gradlew assembleRelease

  build-ios:
    runs-on: macos-latest
    needs: [lint, test]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - run: cd ios && pod install
      - uses: actions/cache@v4
        with:
          path: ~/Library/Developer/Xcode/DerivedData
          key: ${{ runner.os }}-xcode-${{ hashFiles('**/Podfile.lock') }}
      - run: |
          cd ios
          xcodebuild -workspace ProjectName.xcworkspace \
            -scheme ProjectName \
            -configuration Release \
            -destination 'generic/platform=iOS' \
            -archivePath build/ProjectName.xcarchive \
            archive
```

---

## 10. Summary

This standards document provides comprehensive guidelines for:

1. **Coding Standards**: TypeScript, React Native, and Node.js best practices
2. **Naming Conventions**: Consistent naming across all code elements
3. **Folder Structure**: Clear organization for maintainability
4. **Git Workflow**: Structured branching and commit practices
5. **Testing Standards**: Comprehensive testing requirements
6. **Code Review**: Quality assurance process
7. **Documentation**: Clear documentation requirements
8. **Tooling**: Automated enforcement through tooling

Adherence to these standards ensures:
- Consistent, readable code
- Maintainable codebase
- Easier onboarding for new developers
- Reduced bugs through testing
- Efficient collaboration through clear processes

---

## 11. Related Documents

- [System Design Document](./system-design.md)
- [Technical Requirements Analysis](./technical-requirements-analysis.md)
- ADR-001: Choose State Management
- ADR-002: Choose Real-Time Protocol
- ADR-003: Choose Local Storage

---

*Document created by System Architect*
*Date: 2026-04-13*