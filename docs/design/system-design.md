# System Design Document

## 1. Overview

**Project:** Mobile Application for Investment Management Company Clients  
**Platform:** React Native (iOS + Android)  
**Architecture Pattern:** Clean Architecture (3-Layer)  
**Version:** 1.0  
**Date:** 2026-04-17  

---

## 2. Architecture Pattern Selection

### 2.1 Chosen Pattern: Clean Architecture

We adopt **Clean Architecture** with three distinct layers, as specified in the PRD requirements. This pattern was chosen for the following reasons:

| Criteria | Clean Architecture | Assessment |
|----------|-------------------|------------|
| **Separation of Concerns** | Strict layer boundaries | ✅ Excellent |
| **Testability** | Domain layer has no dependencies | ✅ Excellent |
| **Maintainability** | Changes isolated to specific layers | ✅ Excellent |
| **Scalability** | Modular, can grow with features | ✅ Good |
| **Learning Curve** | Requires discipline | ⚠️ Moderate |

### 2.2 Layer Definition

```
┌─────────────────────────────────────────────────────────────────┐
│                        VIEW LAYER                                │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │  Screens    │  │ Components  │  │ Navigation  │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐                                 │
│  │   Hooks    │  │State Stores │                                 │
│  └─────────────┘  └─────────────┘                                 │
├─────────────────────────────────────────────────────────────────┤
│                       DOMAIN LAYER                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │  Entities   │  │  Services   │  │  Use Cases  │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐                                                  │
│  │   Utils     │                                                  │
│  └─────────────┘                                                  │
├─────────────────────────────────────────────────────────────────┤
│                       ADAPTER LAYER                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │  API Adapters│ │ WebSocket   │  │   Storage   │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│  ┌─────────────┐  ┌─────────────┐                                 │
│  │  External   │  │  Platform   │                                 │
│  └─────────────┘  └─────────────┘                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Dependencies flow inward:** View → Domain ← Adapters  
**Domain layer has ZERO external dependencies** (pure TypeScript/JavaScript)

---

## 3. C4 Model Diagrams

### 3.1 Context Diagram (Level 1)

Shows the system in its environment with users and external systems.

```mermaid
graph TB
    subgraph "External Actors"
        Client[Client User<br/>High-net-worth Investor]
        Manager[Portfolio Manager<br/>Company Employee]
    end
    
    subgraph "External Systems"
        Backend[Backend API Server]
        APNs[Apple Push Notification Service]
        FCM[Firebase Cloud Messaging]
    end
    
    subgraph "System Boundary"
        App[Investment Management<br/>Mobile App]
    end
    
    Client -->|Uses| App
    Manager -.->|Communicates via| Backend
    App <-->|REST API + WebSocket| Backend
    App -->|Push Notifications| APNs
    App -->|Push Notifications| FCM
    
    style App fill:#4A90D9,stroke:#2E5A8C,color:#fff
    style Client fill:#5BA55B,stroke:#3D7A3D,color:#fff
    style Manager fill:#5BA55B,stroke:#3D7A3D,color:#fff
    style Backend fill:#E5A84D,stroke:#B8843A,color:#fff
```

### 3.2 Container Diagram (Level 2)

Shows the high-level containers within the system.

```mermaid
graph TB
    subgraph "Mobile Application"
        subgraph "View Layer"
            Screens[Screens<br/>React Components]
            Nav[Navigation<br/>React Navigation]
            UI[UI Components<br/>shadcn/ui]
        end
        
        subgraph "Domain Layer"
            Entities[Domain Entities<br/>TypeScript Types]
            Services[Business Services<br/>Pure Logic]
            UseCases[Use Cases<br/>Orchestrators]
        end
        
        subgraph "Adapter Layer"
            APIAdapters[API Adapters<br/>Axios/Fetch]
            WSAdapter[WebSocket Adapter<br/>Socket.io]
            StorageAdapter[Storage Adapter<br/>Realm/MMKV]
            PlatformAdapter[Platform Adapter<br/>Native Modules]
        end
        
        subgraph "State Management"
            Zustand[Zustand Stores<br/>Auth, Portfolio, Chat]
        end
    end
    
    Screens --> Zustand
    Nav --> Zustand
    UI --> Zustand
    Zustand --> Services
    Services --> Entities
    UseCases --> Services
    Services --> APIAdapters
    Services --> WSAdapter
    Services --> StorageAdapter
    Services --> PlatformAdapter
    
    style Screens fill:#6BB5E0,stroke:#4A8BC4,color:#fff
    style Entities fill:#7BC47F,stroke:#5BA05F,color:#fff
    style APIAdapters fill:#E5A84D,stroke:#B8843A,color:#fff
    style Zustand fill:#B57BC4,stroke:#8F5A9F,color:#fff
```

### 3.3 Component Diagram (Level 3)

Detailed component breakdown for each major module.

```mermaid
graph TB
    subgraph "View Layer Components"
        subgraph "Authentication Module"
            LoginScreen[Login Screen]
            PINScreen[PIN Screen]
            BiometricPrompt[Biometric Prompt]
        end
        
        subgraph "Product Module"
            ProductListScreen[Product List Screen]
            ProductDetailScreen[Product Detail Screen]
            StrategyCard[Strategy Card Component]
        end
        
        subgraph "Portfolio Module"
            PortfolioScreen[Portfolio Overview Screen]
            PositionDetailScreen[Position Detail Screen]
            PositionList[Position List Component]
            ValueDisplay[Value Display Component]
        end
        
        subgraph "Chat Module"
            ChatScreen[Chat Screen]
            MessageList[Message List Component]
            MessageInput[Message Input Component]
            StatusIndicator[Manager Status Indicator]
        end
    end
    
    subgraph "Domain Layer Services"
        AuthService[Auth Service]
        ProductService[Product Service]
        PortfolioService[Portfolio Service]
        ChatService[Chat Service]
        SyncService[Sync Service]
        CalculatorService[Portfolio Calculator]
    end
    
    subgraph "Adapter Layer"
        AuthAdapter[Auth Adapter]
        ProductAdapter[Product Adapter]
        PortfolioAdapter[Portfolio Adapter]
        ChatAdapter[Chat Adapter]
        WebSocketAdapter[WebSocket Adapter]
        TokenStorage[Token Storage]
        MessageStorage[Message Storage]
    end
    
    LoginScreen --> AuthService
    ProductListScreen --> ProductService
    ProductDetailScreen --> ProductService
    PortfolioScreen --> PortfolioService
    PositionDetailScreen --> PortfolioService
    ChatScreen --> ChatService
    
    AuthService --> AuthAdapter
    AuthService --> TokenStorage
    ProductService --> ProductAdapter
    PortfolioService --> PortfolioAdapter
    PortfolioService --> CalculatorService
    ChatService --> ChatAdapter
    ChatService --> WebSocketAdapter
    ChatService --> MessageStorage
    SyncService --> ProductAdapter
    SyncService --> PortfolioAdapter
    SyncService --> ChatAdapter
```

---

## 4. Layer Details

### 4.1 View Layer

The View Layer contains all UI-related code and has NO direct contact with external systems.

| Component | Responsibility | Dependencies |
|-----------|---------------|--------------|
| **Screens** | Page-level components, orchestrate UI | Stores, Hooks |
| **Components** | Reusable UI elements | Props only |
| **Navigation** | Screen routing, deep links | React Navigation |
| **Hooks** | UI-specific logic, event handlers | Stores, Services |
| **Stores** | UI state, view models | Domain Services |

**View Layer Structure:**
```
src/view/
├── screens/
│   ├── auth/
│   │   ├── LoginScreen.tsx
│   │   ├── PINScreen.tsx
│   │   └── BiometricSetupScreen.tsx
│   ├── products/
│   │   ├── ProductListScreen.tsx
│   │   └── ProductDetailScreen.tsx
│   ├── portfolio/
│   │   ├── PortfolioOverviewScreen.tsx
│   │   └── PositionDetailScreen.tsx
│   ├── chat/
│   │   ├── ChatScreen.tsx
│   │   └── ConversationListScreen.tsx
│   └── profile/
│       ├── ProfileScreen.tsx
│       └── SettingsScreen.tsx
├── components/
│   ├── common/
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   ├── Card.tsx
│   │   └── Skeleton.tsx
│   ├── products/
│   │   ├── StrategyCard.tsx
│   │   └── CategoryFilter.tsx
│   ├── portfolio/
│   │   ├── PositionCard.tsx
│   │   ├── ValueDisplay.tsx
│   │   └── MetricCard.tsx
│   └── chat/
│       ├── MessageBubble.tsx
│       ├── MessageInput.tsx
│       └── StatusIndicator.tsx
├── navigation/
│   ├── AppNavigator.tsx
│   ├── AuthNavigator.tsx
│   └── TabNavigator.tsx
└── hooks/
    ├── useAuth.ts
    ├── useProducts.ts
    ├── usePortfolio.ts
    └── useChat.ts
```

### 4.2 Domain Layer

The Domain Layer is the **heart of the application**. It contains pure business logic with NO external dependencies.

| Component | Responsibility | Dependencies |
|-----------|---------------|--------------|
| **Entities** | Core business objects, types | None |
| **Services** | Business logic, calculations | Entities |
| **Use Cases** | Orchestrate complex flows | Services, Entities |
| **Utils** | Helper functions, formatters | None |

**Domain Layer Structure:**
```
src/domain/
├── entities/
│   ├── User.ts
│   ├── AuthTokens.ts
│   ├── Product.ts
│   ├── Strategy.ts
│   ├── Portfolio.ts
│   ├── Position.ts
│   ├── Message.ts
│   └── Conversation.ts
├── services/
│   ├── AuthService.ts
│   ├── ProductService.ts
│   ├── PortfolioService.ts
│   ├── ChatService.ts
│   ├── SyncService.ts
│   └── NotificationService.ts
├── usecases/
│   ├── LoginUseCase.ts
│   ├── RefreshTokenUseCase.ts
│   ├── LoadProductDetailUseCase.ts
│   ├── CalculatePortfolioMetricsUseCase.ts
│   └── SendMessageUseCase.ts
├── calculators/
│   ├── PortfolioCalculator.ts
│   └── ReturnsCalculator.ts
└── utils/
    ├── formatters.ts
    ├── validators.ts
    └── dateUtils.ts
```

### 4.3 Adapter Layer

The Adapter Layer handles all external communication and implements interfaces defined by the Domain layer.

| Component | Responsibility | Dependencies |
|-----------|---------------|--------------|
| **API Adapters** | HTTP communication | Axios/Fetch |
| **WebSocket Adapter** | Real-time communication | Socket.io |
| **Storage Adapter** | Local persistence | Realm/MMKV/SQLite |
| **Platform Adapter** | Native features | Native modules |

**Adapter Layer Structure:**
```
src/adapters/
├── api/
│   ├── ApiClient.ts
│   ├── AuthAdapter.ts
│   ├── ProductAdapter.ts
│   ├── PortfolioAdapter.ts
│   └── ChatAdapter.ts
├── websocket/
│   ├── WebSocketClient.ts
│   └── ChatWebSocketAdapter.ts
├── storage/
│   ├── SecureStorageAdapter.ts
│   ├── CacheAdapter.ts
│   └── MessageStorageAdapter.ts
├── platform/
│   ├── BiometricAdapter.ts
│   ├── NetworkAdapter.ts
│   └── NotificationAdapter.ts
└── types/
    ├── ApiTypes.ts
    ├── WebSocketTypes.ts
    └── StorageTypes.ts
```

---

## 5. State Management Design

### 5.1 Chosen Solution: Zustand

After evaluating options, **Zustand** is selected for state management:

| Criteria | Zustand | Redux Toolkit | MobX |
|----------|---------|---------------|------|
| **Bundle size** | ~1KB | ~11KB | ~16KB |
| **Learning curve** | Low | Medium | Medium |
| **Boilerplate** | Minimal | Moderate | Minimal |
| **TypeScript support** | Excellent | Good | Good |
| **DevTools** | Good | Excellent | Good |
| **Performance** | Excellent | Good | Good |

### 5.2 Store Architecture

```mermaid
graph TB
    subgraph "State Stores"
        AuthStore[Auth Store<br/>isAuthenticated, user, tokens]
        ProductStore[Product Store<br/>products, categories, filters]
        PortfolioStore[Portfolio Store<br/>portfolio, positions, metrics]
        ChatStore[Chat Store<br/>messages, conversations, status]
        SyncStore[Sync Store<br/>lastSync, pending, status]
        UIStore[UI Store<br/>theme, loading, modals]
    end
    
    subgraph "Persistence"
        SecureStorage[Secure Storage<br/>Tokens, PIN]
        LocalCache[Local Cache<br/>Products, Portfolio]
        MessageDB[Message DB<br/>Chat History]
    end
    
    AuthStore --> SecureStorage
    ProductStore --> LocalCache
    PortfolioStore --> LocalCache
    ChatStore --> MessageDB
    SyncStore --> LocalCache
```

### 5.3 Store Definitions

```typescript
// Auth Store
interface AuthState {
  isAuthenticated: boolean;
  user: User | null;
  tokens: AuthTokens | null;
  loading: boolean;
  error: string | null;
  
  // Actions
  login: (credentials: Credentials) => Promise<void>;
  logout: () => Promise<void>;
  refreshTokens: () => Promise<void>;
  setUser: (user: User) => void;
  clearError: () => void;
}

// Product Store
interface ProductState {
  products: Product[];
  categories: Category[];
  selectedProduct: Product | null;
  filters: ProductFilters;
  loading: boolean;
  error: string | null;
  
  // Actions
  fetchProducts: () => Promise<void>;
  fetchProductDetail: (id: string) => Promise<void>;
  setFilters: (filters: ProductFilters) => void;
  clearFilters: () => void;
}

// Portfolio Store
interface PortfolioState {
  portfolio: Portfolio | null;
  positions: Position[];
  metrics: PortfolioMetrics | null;
  loading: boolean;
  error: string | null;
  lastUpdated: Date | null;
  
  // Actions
  fetchPortfolio: () => Promise<void>;
  fetchPositions: () => Promise<void>;
  calculateMetrics: () => void;
}

// Chat Store
interface ChatState {
  conversations: Conversation[];
  activeConversation: Conversation | null;
  messages: Message[];
  managerStatus: ManagerStatus;
  unreadCount: number;
  loading: boolean;
  sending: boolean;
  error: string | null;
  
  // Actions
  fetchMessages: (conversationId: string) => Promise<void>;
  sendMessage: (text: string) => Promise<void>;
  markAsRead: (messageIds: string[]) => void;
  addMessage: (message: Message) => void;
  updateManagerStatus: (status: ManagerStatus) => void;
}

// Sync Store
interface SyncState {
  lastSync: Date | null;
  syncStatus: 'idle' | 'syncing' | 'error' | 'offline';
  pendingOperations: PendingOperation[];
  
  // Actions
  sync: () => Promise<void>;
  addToQueue: (operation: PendingOperation) => void;
  processQueue: () => Promise<void>;
  setSyncStatus: (status: SyncStatus) => void;
}
```

### 5.4 State Flow Diagram

```mermaid
sequenceDiagram
    participant UI as UI Component
    participant Store as Zustand Store
    participant Service as Domain Service
    participant Adapter as API Adapter
    participant API as Backend API
    
    UI->>Store: Call action
    Store->>Store: Set loading = true
    Store->>Service: Execute business logic
    Service->>Adapter: Make API call
    Adapter->>API: HTTP Request
    API-->>Adapter: Response
    Adapter-->>Service: Parsed data
    Service-->>Store: Domain entities
    Store->>Store: Update state
    Store->>Store: Set loading = false
    Store-->>UI: Re-render with new state
```

---

## 6. Data Flow Design

### 6.1 Unidirectional Data Flow

The application follows a strict unidirectional data flow pattern:

```mermaid
graph LR
    Action[User Action] --> Store[State Store]
    Store --> Service[Domain Service]
    Service --> Adapter[Adapter]
    Adapter --> External[External System]
    External --> Adapter
    Adapter --> Service
    Service --> Store
    Store --> UI[UI Update]
```

### 6.2 Authentication Flow

```mermaid
sequenceDiagram
    participant User
    participant LoginScreen
    participant AuthStore
    participant AuthService
    participant AuthAdapter
    participant TokenStorage
    
    User->>LoginScreen: Enter credentials
    LoginScreen->>AuthStore: login(credentials)
    AuthStore->>AuthStore: Set loading = true
    AuthStore->>AuthService: authenticate(credentials)
    AuthService->>AuthService: Validate credentials
    AuthService->>AuthAdapter: login(credentials)
    AuthAdapter->>AuthAdapter: POST /auth/login
    AuthAdapter-->>AuthService: AuthTokens
    AuthService->>TokenStorage: storeTokens(tokens)
    AuthService-->>AuthStore: AuthTokens + User
    AuthStore->>AuthStore: Set isAuthenticated = true
    AuthStore-->>LoginScreen: Navigate to main app
```

### 6.3 Product Browsing Flow

```mermaid
sequenceDiagram
    participant User
    participant ProductList
    participant ProductStore
    participant ProductService
    participant ProductAdapter
    participant Cache
    
    User->>ProductList: Open products tab
    ProductList->>ProductStore: fetchProducts()
    ProductStore->>ProductStore: Set loading = true
    
    alt Cache available
        ProductStore->>Cache: getCachedProducts()
        Cache-->>ProductStore: Cached products
        ProductStore->>ProductList: Render cached data
    end
    
    ProductStore->>ProductService: loadProducts()
    ProductService->>ProductAdapter: getProducts()
    ProductAdapter-->>ProductService: Product[]
    ProductService-->>ProductStore: Domain products
    ProductStore->>Cache: cacheProducts(products)
    ProductStore->>ProductList: Render fresh data
```

### 6.4 Portfolio Data Flow

```mermaid
sequenceDiagram
    participant User
    participant PortfolioScreen
    participant PortfolioStore
    participant PortfolioService
    participant PortfolioAdapter
    participant Calculator
    
    User->>PortfolioScreen: Open portfolio tab
    PortfolioScreen->>PortfolioStore: fetchPortfolio()
    PortfolioStore->>PortfolioService: loadPortfolio()
    PortfolioService->>PortfolioAdapter: getPortfolio()
    PortfolioAdapter-->>PortfolioService: Portfolio data
    PortfolioService->>Calculator: calculateMetrics(portfolio)
    Calculator-->>PortfolioService: PortfolioMetrics
    PortfolioService-->>PortfolioStore: Portfolio + Metrics
    PortfolioStore-->>PortfolioScreen: Render portfolio
```

### 6.5 Chat Message Flow (Real-time)

```mermaid
sequenceDiagram
    participant User
    participant ChatScreen
    participant ChatStore
    participant ChatService
    participant ChatAdapter
    participant WebSocket
    participant MessageDB
    
    User->>ChatScreen: Type message
    User->>ChatScreen: Press send
    ChatScreen->>ChatStore: sendMessage(text)
    
    Note over ChatStore: Optimistic update
    ChatStore->>ChatStore: Add message (status: sending)
    ChatStore->>ChatScreen: Immediate render
    
    ChatStore->>ChatService: send(message)
    ChatService->>ChatAdapter: sendMessage(message)
    
    alt WebSocket connected
        ChatAdapter->>WebSocket: emit('message', payload)
        WebSocket-->>ChatAdapter: ack
    else WebSocket disconnected
        ChatAdapter->>ChatAdapter: Queue message
        ChatAdapter->>MessageDB: Store pending
    end
    
    ChatAdapter-->>ChatService: MessageSent
    ChatService-->>ChatStore: Update status (sent)
    
    Note over WebSocket: Manager replies
    WebSocket->>ChatAdapter: onMessage(received)
    ChatAdapter->>ChatService: handleNewMessage
    ChatService->>MessageDB: Store message
    ChatService->>ChatStore: addMessage(message)
    ChatStore->>ChatScreen: Render new message
```

### 6.6 Offline Sync Flow

```mermaid
sequenceDiagram
    participant App
    participant SyncStore
    participant SyncService
    participant NetworkAdapter
    participant QueueStorage
    
    Note over App: Network disconnects
    App->>NetworkAdapter: onDisconnect()
    NetworkAdapter->>SyncStore: setSyncStatus('offline')
    
    Note over App: User sends message
    App->>SyncStore: sendMessage()
    SyncStore->>QueueStorage: addToQueue(operation)
    SyncStore->>App: Show pending indicator
    
    Note over App: Network reconnects
    App->>NetworkAdapter: onConnect()
    NetworkAdapter->>SyncStore: setSyncStatus('syncing')
    SyncStore->>SyncService: sync()
    
    SyncService->>QueueStorage: getPendingOperations()
    QueueStorage-->>SyncService: Pending ops
    
    loop For each operation
        SyncService->>SyncService: processOperation(op)
        SyncService->>QueueStorage: removeOperation(op)
    end
    
    SyncService-->>SyncStore: syncComplete()
    SyncStore->>SyncStore: setSyncStatus('idle')
```

---

## 7. Component Boundaries

### 7.1 Module Boundaries

Each module has clear boundaries and communication interfaces:

```mermaid
graph TB
    subgraph "Authentication Module"
        AuthView[View: Login, PIN, Biometric UI]
        AuthDomain[Domain: Auth Logic, Session]
        AuthAdapter[Adapter: Auth API, Token Storage]
    end
    
    subgraph "Product Module"
        ProdView[View: Product List, Detail]
        ProdDomain[Domain: Products, Categories]
        ProdAdapter[Adapter: Products API]
    end
    
    subgraph "Portfolio Module"
        PortView[View: Portfolio, Positions]
        PortDomain[Domain: Portfolio, Metrics]
        PortAdapter[Adapter: Portfolio API]
    end
    
    subgraph "Chat Module"
        ChatView[View: Chat, Messages]
        ChatDomain[Domain: Messages, Conversations]
        ChatAdapter[Adapter: Chat API, WebSocket]
    end
    
    AuthDomain --> AuthView
    AuthAdapter --> AuthDomain
    
    ProdDomain --> ProdView
    ProdAdapter --> ProdDomain
    
    PortDomain --> PortView
    PortAdapter --> PortDomain
    
    ChatDomain --> ChatView
    ChatAdapter --> ChatDomain
    
    AuthDomain -.->|Auth Token| ProdAdapter
    AuthDomain -.->|Auth Token| PortAdapter
    AuthDomain -.->|Auth Token| ChatAdapter
```

### 7.2 Dependency Rules

| From | To | Allowed? | Reason |
|------|-----|----------|--------|
| View | Domain | ✅ Yes | View depends on domain for logic |
| View | Adapters | ❌ No | View should not know about adapters |
| Domain | View | ❌ No | Domain has no UI knowledge |
| Domain | Adapters | ❌ No | Domain defines interfaces, adapters implement |
| Adapters | Domain | ✅ Yes | Adapters implement domain interfaces |
| Adapters | View | ❌ No | Adapters have no UI knowledge |

### 7.3 Interface Contracts

```typescript
// Domain defines interfaces (ports)
interface IAuthAdapter {
  login(credentials: Credentials): Promise<AuthTokens>;
  logout(): Promise<void>;
  refreshToken(refreshToken: string): Promise<AuthTokens>;
}

interface IProductAdapter {
  getProducts(): Promise<Product[]>;
  getProductDetail(id: string): Promise<Product>;
  getCategories(): Promise<Category[]>;
}

interface IPortfolioAdapter {
  getPortfolio(): Promise<Portfolio>;
  getPositions(): Promise<Position[]>;
  getPositionDetail(id: string): Promise<Position>;
}

interface IChatAdapter {
  getMessages(conversationId: string, cursor?: string): Promise<Message[]>;
  sendMessage(message: NewMessage): Promise<Message>;
  markAsRead(messageIds: string[]): Promise<void>;
}

interface IStorageAdapter {
  get<T>(key: string): Promise<T | null>;
  set<T>(key: string, value: T): Promise<void>;
  remove(key: string): Promise<void>;
  clear(): Promise<void>;
}

interface IWebSocketAdapter {
  connect(token: string): Promise<void>;
  disconnect(): void;
  send(event: string, data: unknown): void;
  on(event: string, handler: Function): void;
  off(event: string, handler: Function): void;
}
```

---

## 8. Navigation Architecture

### 8.1 Navigation Structure

```mermaid
graph TB
    subgraph "Navigation Graph"
        Root[Root Navigator]
        
        subgraph "Auth Flow"
            AuthStack[Auth Stack Navigator]
            Login[Login Screen]
            PIN[PIN Screen]
            Biometric[Biometric Prompt]
        end
        
        subgraph "Main App Flow"
            MainTabs[Tab Navigator]
            
            subgraph "Products Tab"
                ProductsStack[Products Stack]
                ProdList[Product List]
                ProdDetail[Product Detail]
            end
            
            subgraph "Portfolio Tab"
                PortfolioStack[Portfolio Stack]
                PortOverview[Portfolio Overview]
                PosDetail[Position Detail]
            end
            
            subgraph "Chat Tab"
                ChatStack[Chat Stack]
                ChatMain[Chat Screen]
            end
        end
    end
    
    Root --> AuthStack
    Root --> MainTabs
    
    AuthStack --> Login
    Login --> PIN
    PIN --> Biometric
    Biometric --> MainTabs
    
    MainTabs --> ProductsStack
    MainTabs --> PortfolioStack
    MainTabs --> ChatStack
    
    ProductsStack --> ProdList
    ProdList --> ProdDetail
    
    PortfolioStack --> PortOverview
    PortOverview --> PosDetail
    
    ChatStack --> ChatMain
```

### 8.2 Deep Linking Map

```typescript
const linkingConfig = {
  prefixes: ['investapp://', 'https://app.investcompany.com'],
  config: {
    screens: {
      Auth: {
        screens: {
          Login: 'login',
        },
      },
      Main: {
        screens: {
          ProductsTab: {
            screens: {
              ProductList: 'products',
              ProductDetail: 'products/:id',
            },
          },
          PortfolioTab: {
            screens: {
              PortfolioOverview: 'portfolio',
              PositionDetail: 'portfolio/positions/:id',
            },
          },
          ChatTab: {
            screens: {
              ChatScreen: 'chat',
            },
          },
        },
      },
    },
  },
};
```

---

## 9. Data Models

### 9.1 Core Domain Entities

```typescript
// User Entity
interface User {
  id: string;
  email: string;
  firstName: string;
  lastName: string;
  phone?: string;
  managerId?: string;
  createdAt: Date;
}

// AuthTokens Entity
interface AuthTokens {
  accessToken: string;
  refreshToken: string;
  expiresAt: Date;
  tokenType: 'Bearer';
}

// Product Entity
interface Product {
  id: string;
  name: string;
  description: string;
  categoryId: string;
  type: 'strategy' | 'individual';
  riskLevel: 'low' | 'medium' | 'high';
  minimumInvestment: number;
  currency: string;
  expectedReturn?: number;
  historicalReturn?: number;
  parameters: ProductParameter[];
  conditions: ProductCondition[];
}

// Category Entity
interface Category {
  id: string;
  name: string;
  description?: string;
  productCount: number;
}

// Portfolio Entity
interface Portfolio {
  id: string;
  userId: string;
  totalValue: number;
  currency: string;
  change24h: number;
  changePercent24h: number;
  lastUpdated: Date;
}

// Position Entity
interface Position {
  id: string;
  assetId: string;
  assetName: string;
  assetSymbol: string;
  assetType: 'stock' | 'bond' | 'fund' | 'cash';
  quantity: number;
  averagePrice: number;
  currentPrice: number;
  currentValue: number;
  profitLoss: number;
  profitLossPercent: number;
  weight: number;
}

// Message Entity
interface Message {
  id: string;
  conversationId: string;
  senderId: string;
  senderType: 'client' | 'manager';
  text: string;
  timestamp: Date;
  status: 'sending' | 'sent' | 'delivered' | 'read' | 'failed';
}

// Conversation Entity
interface Conversation {
  id: string;
  participantId: string;
  participantName: string;
  lastMessage?: Message;
  unreadCount: number;
  updatedAt: Date;
}
```

### 9.2 Entity Relationships

```mermaid
erDiagram
    User ||--o{ Portfolio : owns
    User ||--o{ Conversation : participates
    User ||--o| Manager : assigned
    
    Portfolio ||--o{ Position : contains
    
    Product ||--o| Category : belongs_to
    Product ||--o{ ProductParameter : has
    Product ||--o{ ProductCondition : has
    
    Conversation ||--o{ Message : contains
    
    User {
        string id PK
        string email
        string firstName
        string lastName
        string phone
        string managerId FK
    }
    
    Portfolio {
        string id PK
        string userId FK
        number totalValue
        string currency
        number change24h
    }
    
    Position {
        string id PK
        string portfolioId FK
        string assetId
        number quantity
        number currentValue
    }
    
    Product {
        string id PK
        string name
        string categoryId FK
        string type
        string riskLevel
    }
    
    Message {
        string id PK
        string conversationId FK
        string senderId
        string text
        datetime timestamp
    }
```

---

## 10. Security Architecture

### 10.1 Authentication Architecture

```mermaid
graph TB
    subgraph "Client App"
        User[User]
        LoginUI[Login UI]
        AuthService[Auth Service]
        TokenStorage[Secure Token Storage]
        TokenManager[Token Manager]
        
        subgraph "Protected Resources"
            API[API Requests]
            Portfolio[Portfolio Data]
            Chat[Chat Messages]
        end
    end
    
    subgraph "Backend"
        AuthAPI[Auth API]
        ResourceAPI[Resource APIs]
        TokenValidator[Token Validator]
    end
    
    User --> LoginUI
    LoginUI --> AuthService
    AuthService --> AuthAPI
    AuthAPI --> AuthService
    AuthService --> TokenStorage
    TokenStorage --> TokenManager
    
    TokenManager --> API
    API --> ResourceAPI
    ResourceAPI --> TokenValidator
    
    TokenManager --> Portfolio
    TokenManager --> Chat
```

### 10.2 Token Management Flow

```mermaid
sequenceDiagram
    participant App
    participant TokenManager
    participant SecureStorage
    participant API
    
    Note over App: App startup
    App->>TokenManager: getAccessToken()
    TokenManager->>SecureStorage: retrieveToken()
    
    alt Token exists and valid
        SecureStorage-->>TokenManager: accessToken
        TokenManager-->>App: accessToken
    else Token expired
        TokenManager->>TokenManager: refreshToken()
        TokenManager->>SecureStorage: getRefreshToken()
        SecureStorage-->>TokenManager: refreshToken
        TokenManager->>API: POST /auth/refresh
        API-->>TokenManager: newTokens
        TokenManager->>SecureStorage: storeTokens(newTokens)
        TokenManager-->>App: newAccessToken
    else No token
        TokenManager-->>App: null (redirect to login)
    end
```

### 10.3 Data Protection Layers

| Layer | Protection | Implementation |
|-------|------------|----------------|
| **Network** | TLS 1.2+ | HTTPS for all requests |
| **Authentication** | JWT + Refresh | Short-lived access tokens |
| **Token Storage** | Hardware-backed | iOS Keychain / Android Keystore |
| **PIN Storage** | Hashed | bcrypt with salt |
| **Local Cache** | Encrypted | SQLite with SQLCipher or Realm encryption |
| **Memory** | Sensitive data cleared | Clear on background/app lifecycle |

---

## 11. Scalability Considerations

### 11.1 Performance Optimization Strategies

| Area | Strategy | Implementation |
|------|----------|---------------|
| **List Performance** | Virtualization | FlatList with getItemLayout |
| **Image Loading** | Lazy loading + caching | react-native-fast-image |
| **State Updates** | Selective subscriptions | Zustand selectors |
| **Bundle Size** | Code splitting | Dynamic imports for features |
| **Memory** | Object pooling | Reuse message objects in chat |
| **Startup Time** | Lazy initialization | Defer non-critical services |

### 11.2 Caching Strategy

```mermaid
graph LR
    subgraph "Cache Layers"
        Memory[Memory Cache<br/>Hot data]
        Disk[Disk Cache<br/>Persistence]
        Network[Network<br/>Fresh data]
    end
    
    Request[Data Request] --> Memory
    
    alt Memory hit
        Memory --> Response[Return data]
    else Memory miss
        Memory --> Disk
        alt Disk hit
            Disk --> Response
            Disk --> Memory
        else Disk miss
            Disk --> Network
            Network --> Response
            Network --> Disk
            Network --> Memory
        end
    end
```

### 11.3 Message Storage Strategy

```mermaid
graph TB
    subgraph "Message Storage Tiers"
        Hot[Hot Storage<br/>Recent 100 messages<br/>Memory]
        Warm[Warm Storage<br/>Last 1000 messages<br/>Local DB]
        Cold[Cold Storage<br/>Older messages<br/>Server API]
    end
    
    ChatOpen[Chat Screen Opened] --> Hot
    
    ScrollUp[User Scrolls Up] --> Warm
    Warm --> Hot
    
    Older[Need older messages] --> Cold
    Cold --> Warm
    Cold --> Hot
```

---

## 12. Technology Stack Summary

### 12.1 Core Dependencies

| Category | Package | Version | Purpose |
|----------|---------|---------|---------|
| **Framework** | react-native | 0.73+ | Cross-platform mobile |
| **Language** | typescript | 5.0+ | Type safety |
| **State** | zustand | 4.4+ | Global state management |
| **Navigation** | @react-navigation/native | 6.x | Screen navigation |
| **Styling** | nativewind | 4.x | Tailwind CSS for RN |
| **HTTP** | axios | 1.6+ | API requests |
| **WebSocket** | socket.io-client | 4.x | Real-time chat |
| **Secure Storage** | react-native-keychain | 8.x | Token storage |
| **Local DB** | @nozbe/watermelondb | 0.27+ | Offline storage |
| **Biometrics** | react-native-biometrics | 3.x | Face ID/Touch ID |
| **Push** | @react-native-firebase/messaging | 18.x | Push notifications |
| **Network** | @react-native-community/netinfo | 11.x | Connection monitoring |
| **Forms** | react-hook-form | 7.x | Form handling |
| **Validation** | zod | 3.x | Schema validation |

### 12.2 Development Dependencies

| Category | Package | Purpose |
|----------|---------|---------|
| **Testing** | jest + @testing-library/react-native | Unit and component tests |
| **E2E** | detox | End-to-end testing |
| **Linting** | eslint + prettier | Code quality |
| **Types** | @types/* | TypeScript definitions |

---

## 13. Glossary

| Term | Definition |
|------|------------|
| **View Layer** | UI components, screens, and navigation |
| **Domain Layer** | Business logic, entities, and use cases |
| **Adapter Layer** | External integrations, API clients, storage |
| **Store** | Zustand state container for a specific domain |
| **Adapter** | Implementation of a domain interface for external systems |
| **Use Case** | Orchestrator for complex business workflows |
| **Entity** | Core business object with identity |
| **Service** | Domain logic coordinator |
| **Deep Link** | URL scheme to navigate directly to app content |
| **Token** | JWT authentication credential |

---

## 14. Appendix

### A. File Structure (Complete)

```
investment-app/
├── src/
│   ├── view/
│   │   ├── screens/
│   │   │   ├── auth/
│   │   │   ├── products/
│   │   │   ├── portfolio/
│   │   │   ├── chat/
│   │   │   └── profile/
│   │   ├── components/
│   │   │   ├── common/
│   │   │   ├── products/
│   │   │   ├── portfolio/
│   │   │   └── chat/
│   │   ├── navigation/
│   │   └── hooks/
│   ├── domain/
│   │   ├── entities/
│   │   ├── services/
│   │   ├── usecases/
│   │   ├── calculators/
│   │   └── utils/
│   ├── adapters/
│   │   ├── api/
│   │   ├── websocket/
│   │   ├── storage/
│   │   └── platform/
│   ├── stores/
│   │   ├── authStore.ts
│   │   ├── productStore.ts
│   │   ├── portfolioStore.ts
│   │   ├── chatStore.ts
│   │   └── syncStore.ts
│   ├── shared/
│   │   ├── types/
│   │   ├── constants/
│   │   └── utils/
│   └── App.tsx
├── android/
├── ios/
├── package.json
├── tsconfig.json
└── README.md
```

### B. Key Architectural Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Architecture Pattern | Clean Architecture | Separation of concerns, testability |
| State Management | Zustand | Minimal boilerplate, excellent TS support |
| Local Database | WatermelonDB | Performance, lazy loading, observability |
| WebSocket | Socket.io | Reliability, reconnection handling |
| Styling | NativeWind | Developer experience, consistency |

---

*Document generated by System Architect Agent*  
*Version 1.0 | Date: 2026-04-17*