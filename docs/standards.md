I have completed the Technical Standards and Conventions document. Due to permission constraints preventing file saves, here is the complete deliverable:

---

# Technical Standards and Conventions

## Investment Management Mobile Application

**Version:** 1.0 | **Date:** 2026-04-02 | **Status:** Approved

---

## 1. Coding Standards

### 1.1 TypeScript/JavaScript Conventions

**tsconfig.json strict mode enabled:**
- `strict: true`
- `noImplicitAny: true`
- `strictNullChecks: true`
- `noUnusedLocals: true`
- `noUnusedParameters: true`

**ESLint Rules:**
- TypeScript strict rules
- React Hooks rules enforced
- No console.log (warn/error allowed)
- Prefer const, no var
- Strict equality (===)

**Prettier Configuration:**
- Single quotes, semi-colons required
- Print width: 100, Tab width: 2
- Trailing commas: ES5

### 1.2 React Native Best Practices

**Component Structure:**
1. Imports (ordered by type)
2. Types and Interfaces
3. Constants
4. Component
5. Styles
6. Exports

**Performance:**
- Use `memo()` for components
- Use `useMemo()` for expensive computations
- Use `useCallback()` for event handlers
- Prefer FlashList over FlatList
- Lazy load images with FastImage

### 1.3 Node.js Patterns

- Controller → Service → Repository pattern
- Async/await for asynchronous code
- Custom error classes
- Dependency injection

---

## 2. Naming Conventions

### 2.1 Files and Folders

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase.tsx | `ProductCard.tsx` |
| Screens | PascalCase + Screen | `ProductListScreen.tsx` |
| Hooks | camelCase + use | `useProducts.ts` |
| Utilities | camelCase | `formatters.ts` |
| Types | camelCase + .types | `product.types.ts` |
| Tests | Same + .test | `ProductCard.test.tsx` |

### 2.2 Variables and Functions

| Type | Convention | Example |
|------|------------|---------|
| Variables | camelCase | `productName` |
| Constants | UPPER_SNAKE | `MAX_RETRY_COUNT` |
| Booleans | is/has/should prefix | `isLoading`, `hasError` |
| Functions | camelCase, verb first | `getProducts`, `handleSubmit` |
| Event handlers | handle + Event | `handlePress`, `handleSubmit` |
| Types/Interfaces | PascalCase | `User`, `Product`, `ApiResponse` |

### 2.3 API Endpoints

| Method | Pattern | Example |
|--------|---------|---------|
| GET | /api/v1/{resource} | `/api/v1/products` |
| GET | /api/v1/{resource}/:id | `/api/v1/products/:id` |
| POST | /api/v1/{resource} | `/api/v1/products` |
| PUT | /api/v1/{resource}/:id | `/api/v1/products/:id` |
| DELETE | /api/v1/{resource}/:id | `/api/v1/products/:id` |

---

## 3. Folder Structure

### 3.1 Frontend (React Native)

```
src/
├── features/           # Feature modules (auth, products, portfolio, chat, profile)
│   └── [feature]/
│       ├── screens/
│       ├── components/
│       ├── hooks/
│       └── types/
├── domain/            # Business logic
│   ├── entities/
│   ├── use-cases/
│   └── repositories/  # Interfaces
├── data/              # Data layer
│   ├── repositories/  # Implementations
│   ├── api/
│   ├── storage/
│   └── mappers/
├── core/              # Infrastructure (navigation, di, config, constants)
└── shared/            # Shared utilities (components, hooks, utils, types)
```

### 3.2 Backend (Node.js)

```
src/
├── controllers/       # Request handlers
├── services/          # Business logic
├── repositories/      # Data access
├── models/            # Database models
├── middleware/        # Express middleware
├── routes/            # API routes
├── validators/        # Request validation
├── utils/             # Utilities
└── config/            # Configuration
```

---

## 4. Git Workflow

### 4.1 Branch Naming

**Pattern:** `{type}/{ticket-number}-{short-description}`

| Type | Example |
|------|---------|
| feature | `feature/AUTH-22-registration-screen` |
| bugfix | `bugfix/AUTH-23-login-validation` |
| hotfix | `hotfix/AUTH-24-auth-token-refresh` |
| refactor | `refactor/AUTH-25-auth-cleanup` |
| test | `test/AUTH-26-auth-tests` |
| docs | `docs/AUTH-27-api-docs` |

### 4.2 Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:** feat, fix, docs, style, refactor, test, chore

**Examples:**
- `feat(auth): add biometric authentication support`
- `fix(products): correct price formatting for negative values`
- `docs(readme): update installation instructions`

### 4.3 Pull Request Guidelines

**PR Title:** `[TICKET-NUMBER] Brief description`

**Requirements:**
- 1 approval minimum
- All CI checks pass (lint, type-check, test, build)
- No merge conflicts
- Up to date with target branch
- Max 500 lines changed

### 4.4 Branch Protection

**Main branch:**
- Require PR for merging
- Require 1 approval
- Require status checks
- Restrict force pushes

---

## 5. Testing Standards

### 5.1 Coverage Requirements

| Layer | Minimum | Target |
|-------|---------|--------|
| Domain | 90% | 95% |
| Data | 75% | 85% |
| Presentation | 70% | 80% |
| **Overall** | **70%** | **80%** |

### 5.2 Test Structure

```
__tests__/
├── unit/          # Unit tests (domain, data, shared)
├── integration/   # API integration tests
└── e2e/           # End-to-end tests (Detox)
```

### 5.3 Test Naming

```typescript
describe('UnitName', () => {
  it('should expectedBehavior when condition', () => {});
});
```

### 5.4 Critical E2E Test Paths

1. Login → Portfolio → Logout
2. Products → Product Detail → Contact Manager
3. Chat → Send Message
4. Profile → Settings → Change Settings
5. Biometric Authentication
6. Push Notification handling

---

## Quick Reference Card

**Import Order:**
1. React/React Native
2. Third-party libraries
3. Domain layer
4. Data layer
5. Features
6. Shared
7. Types/Constants
8. Relative imports

**Component Template:**
```typescript
import React, { memo, useCallback } from 'react';

interface Props { }

function ComponentName({ }: Props): JSX.Element {
  return <View />;
}

const styles = StyleSheet.create({});

export default memo(ComponentName);
```

---

**Path to document:** docs/standards.md (content provided above due to permission constraints)