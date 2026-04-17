# Task Specifications

**Project:** Mobile Application for Investment Management Company Clients  
**Platform:** iOS and Android (React Native)  
**Architecture:** 3-layer (View, Domain, Adapters)  
**Tech Stack:** React Native, Node.js, Tailwind CSS, shadcn/ui  
**Generated:** 2026-04-17  

---

## Overview

This document contains detailed specifications for all tasks decomposed from the PM's epic-level backlog. Each task follows INVEST criteria and is sized for 2-5 days of work.

---

## Epic 1: Authentication & Onboarding

### TASK-1.1: Login Screen UI Implementation

**GitHub Issue:** [#247](https://github.com/vovkins/agents-react-native-experiment-2/issues/247)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** None  

#### Description
Implement the login screen UI with input fields for credentials, login button, and error display area. Include responsive layout for both iOS and Android platforms.

#### Acceptance Criteria
1. Login screen renders correctly on iOS and Android
2. Username/email input field with validation
3. Password input field with show/hide toggle
4. Login button with loading state
5. Error message display area
6. "Forgot password" link (non-functional placeholder)
7. Keyboard handling (avoid input occlusion)
8. Proper focus management between fields
9. Accessibility labels for screen readers

#### Technical Notes
- Use Tailwind CSS / shadcn/ui components
- Form validation with immediate feedback
- Secure text entry for password field
- Platform-specific keyboard avoidance
- Architecture: View layer

---

### TASK-1.2: Backend Authentication API Integration

**GitHub Issue:** [#248](https://github.com/vovkins/agents-react-native-experiment-2/issues/248)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-1.1  

#### Description
Implement the adapter layer for authentication API calls, including login endpoint integration, response handling, and error parsing.

#### Acceptance Criteria
1. AuthAdapter class/module created in adapters layer
2. Login API call with proper request formatting
3. Response parsing for success (token, user data)
4. Error response parsing (invalid credentials, account locked, etc.)
5. Network timeout handling
6. Request cancellation on unmount
7. Proper TypeScript types for request/response

#### Technical Notes
- Architecture: Adapter layer
- Use fetch or axios for HTTP calls
- Handle various HTTP status codes
- Implement retry logic for transient failures
- Define interfaces for AuthRequest, AuthResponse, AuthError

---

### TASK-1.3: Secure Token Storage Implementation

**GitHub Issue:** [#249](https://github.com/vovkins/agents-react-native-experiment-2/issues/249)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-1.2  

#### Description
Implement secure storage for authentication tokens using platform-specific secure storage mechanisms (Keychain on iOS, Keystore on Android).

#### Acceptance Criteria
1. TokenStorage service created
2. Save access token securely
3. Save refresh token securely
4. Retrieve tokens on app launch
5. Delete tokens on logout
6. Fallback to AsyncStorage if secure storage unavailable
7. Handle storage errors gracefully

#### Technical Notes
- Use react-native-keychain or expo-secure-store
- Consider encrypted AsyncStorage fallback
- Separate storage keys for access/refresh tokens
- Architecture: Data layer
- Implement singleton pattern for TokenStorage

---

### TASK-1.4: Session Management & Auth State

**GitHub Issue:** [#250](https://github.com/vovkins/agents-react-native-experiment-2/issues/250)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-1.3  

#### Description
Implement session management logic including auth state store, token validation, and app-wide auth context provider.

#### Acceptance Criteria
1. AuthContext/Store created for global auth state
2. Auth state: isAuthenticated, user, loading, error
3. Check token validity on app launch
4. Provide auth state to entire app via context
5. Hook for accessing auth state (useAuth)
6. Method to update auth state on login/logout
7. Loading state during auth check

#### Technical Notes
- Use React Context or state management library
- Singleton pattern for auth service
- Integration point for all other epics
- Architecture: Domain layer
- Define AuthState interface and AuthContext

---

### TASK-1.5: Token Refresh Mechanism

**GitHub Issue:** [#251](https://github.com/vovkins/agents-react-native-experiment-2/issues/251)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-1.3, TASK-1.4  

#### Description
Implement automatic token refresh logic to handle token expiration without user intervention.

#### Acceptance Criteria
1. Intercept 401 responses from API calls
2. Attempt token refresh using refresh token
3. Retry original request with new access token
4. Queue concurrent requests during refresh
5. Redirect to login if refresh fails
6. Handle refresh token expiration
7. Update stored tokens on successful refresh

#### Technical Notes
- Implement request interceptor pattern
- Handle race conditions during refresh (use mutex/flag)
- Clear tokens and redirect to login on failure
- Architecture: Adapter layer
- Consider using axios interceptors or custom fetch wrapper

---

### TASK-1.6: Biometric Authentication Module

**GitHub Issue:** [#252](https://github.com/vovkins/agents-react-native-experiment-2/issues/252)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-1.4  

#### Description
Implement biometric authentication (Face ID/Touch ID) for quick app access after initial login.

#### Acceptance Criteria
1. Check biometric hardware availability
2. Prompt for biometric auth on app launch (if enabled)
3. Handle successful biometric auth (auto-login)
4. Handle failed biometric auth (fallback to PIN/password)
5. Handle biometric not available/enrolled
6. Platform-specific implementations (iOS Face ID/Touch ID, Android fingerprint/face)
7. User preference setting for biometric auth

#### Technical Notes
- Use react-native-biometrics or expo-local-authentication
- iOS: Face ID/Touch ID (requires NSFaceIDUsageDescription in Info.plist)
- Android: BiometricPrompt API
- Require device passcode as fallback
- Store biometric preference in secure storage

---

### TASK-1.7: PIN Code Setup and Validation

**GitHub Issue:** [#253](https://github.com/vovkins/agents-react-native-experiment-2/issues/253)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-1.4  

#### Description
Implement PIN code functionality for quick re-entry to the app as an alternative to biometric auth.

#### Acceptance Criteria
1. PIN setup screen for first-time configuration
2. PIN confirmation screen (re-enter to confirm)
3. PIN entry screen for authentication
4. PIN validation logic (correct/incorrect)
5. PIN change functionality
6. PIN disable functionality (requires full auth)
7. Secure PIN storage
8. Account lockout after N failed attempts

#### Technical Notes
- Hash PIN before storage (never store plain text)
- Use bcrypt or PBKDF2 for hashing
- Consider rate limiting attempts
- Integrate with secure storage (Keychain/Keystore)
- 4-6 digit PIN standard
- Architecture: View + Domain layer

---

### TASK-1.8: Error Handling and Auth Flows

**GitHub Issue:** [#254](https://github.com/vovkins/agents-react-native-experiment-2/issues/254)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-1.1, TASK-1.2, TASK-1.4  

#### Description
Implement comprehensive error handling for all authentication scenarios with user-friendly messages.

#### Acceptance Criteria
1. Network error message (no internet)
2. Invalid credentials message
3. Account locked message
4. Server error message
5. Session expired handling
6. Retry mechanisms with user feedback
7. Error boundary for auth screens
8. Logging for debugging

#### Technical Notes
- Use consistent error message format
- Map error codes to user messages
- Consider localization for messages (Russian)
- Create ErrorCodes enum for mapping
- Architecture: View + Domain layer

---

### TASK-1.9: Logout Functionality

**GitHub Issue:** [#255](https://github.com/vovkins/agents-react-native-experiment-2/issues/255)  
**Size:** XS (<1 day)  
**Priority:** P0  
**Dependencies:** TASK-1.3, TASK-1.4  

#### Description
Implement complete logout flow including token cleanup, state reset, and navigation to login screen.

#### Acceptance Criteria
1. Logout button accessible from app
2. Clear all stored tokens
3. Reset auth state to unauthenticated
4. Clear any cached user data
5. Navigate to login screen
6. Show confirmation dialog (optional)
7. Handle logout API call if required

#### Technical Notes
- May need to call logout endpoint on server
- Ensure all sensitive data cleared
- Reset navigation stack
- Clear secure storage
- Architecture: Domain layer

---

## Epic 2: Product Showcase (Витрина продуктов)

### TASK-2.1: Product Domain Entities

**GitHub Issue:** [#256](https://github.com/vovkins/agents-react-native-experiment-2/issues/256)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** None (can start parallel with Epic 1)  

#### Description
Define domain entities for products, strategies, and categories in the domain layer.

#### Acceptance Criteria
1. Product entity with all fields (id, name, description, parameters, etc.)
2. Strategy entity with related fields
3. Category entity for product grouping
4. TypeScript interfaces/types defined
5. Entity validation logic
6. Factory functions for entity creation
7. Serialization/deserialization helpers

#### Technical Notes
- Architecture: Domain layer
- Follow clean architecture principles
- Include calculated fields if needed (e.g., formatted returns)
- Define Product, Strategy, Category, ProductParameters interfaces
- Use zod or io-ts for validation schemas

---

### TASK-2.2: Product API Adapter

**GitHub Issue:** [#257](https://github.com/vovkins/agents-react-native-experiment-2/issues/257)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-2.1, TASK-1.4  

#### Description
Implement adapter for fetching product and strategy data from backend API.

#### Acceptance Criteria
1. ProductAdapter created in adapters layer
2. Fetch product list endpoint
3. Fetch product detail endpoint
4. Fetch strategies list endpoint
5. Fetch strategy detail endpoint
6. Fetch categories endpoint
7. Response mapping to domain entities
8. Error handling and parsing

#### Technical Notes
- Architecture: Adapter layer
- Include auth token in requests (from TASK-1.4)
- Handle pagination if needed
- Define ProductApiService interface
- Use dependency injection for adapter

---

### TASK-2.3: Product List Screen UI

**GitHub Issue:** [#258](https://github.com/vovkins/agents-react-native-experiment-2/issues/258)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-2.1, TASK-2.2  

#### Description
Implement the main product showcase screen with list of products and categories.

#### Acceptance Criteria
1. Product list screen renders correctly
2. Products grouped by category (collapsible sections)
3. Search/filter functionality
4. Pull-to-refresh for data reload
5. Loading skeleton while fetching
6. Empty state when no products
7. Error state on fetch failure
8. Navigation to product detail on tap

#### Technical Notes
- Use FlatList or SectionList for performance
- Virtualized list for large datasets
- Implement search debounce
- Architecture: View layer
- Connect to ProductAdapter for data fetching

---

### TASK-2.4: Strategy Card Component

**GitHub Issue:** [#259](https://github.com/vovkins/agents-react-native-experiment-2/issues/259)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-2.1  

#### Description
Implement reusable strategy card component for displaying product summary in lists.

#### Acceptance Criteria
1. Card displays strategy name
2. Card displays key metrics (returns, risk level)
3. Card displays brief description
4. Card shows strategy icon/image
5. Tap handling for navigation
6. Consistent styling across states
7. Accessibility support
8. Responsive layout

#### Technical Notes
- Reusable component
- Optimize re-renders with React.memo
- Support for placeholder/loading state
- Architecture: View layer
- Props: strategy, onPress, isLoading

---

### TASK-2.5: Product Detail Screen UI

**GitHub Issue:** [#260](https://github.com/vovkins/agents-react-native-experiment-2/issues/260)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-2.1, TASK-2.2  

#### Description
Implement detailed product view screen showing full information about a strategy or product.

#### Acceptance Criteria
1. Product detail screen renders correctly
2. Display full product description
3. Display all parameters and conditions
4. Display historical performance (if available)
5. Display minimum investment amount
6. Display risk level and category
7. Back navigation to list
8. Share functionality (optional)
9. Loading and error states

#### Technical Notes
- Use ScrollView for long content
- Consider collapsible sections for details
- Image gallery if multiple images
- Architecture: View layer
- Route params: productId

---

### TASK-2.6: Product Categorization Logic

**GitHub Issue:** [#261](https://github.com/vovkins/agents-react-native-experiment-2/issues/261)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-2.1, TASK-2.2  

#### Description
Implement domain logic for categorizing and filtering products.

#### Acceptance Criteria
1. Products grouped by category
2. Filter by single category
3. Filter by multiple categories
4. Sort options (by name, by returns, by risk)
5. Search by product name
6. Clear filters functionality
7. Category count display

#### Technical Notes
- Architecture: Domain layer
- Pure functions for filtering/sorting
- Memoize computed results
- Define ProductFilter, ProductSort types
- Use createSelector pattern for performance

---

### TASK-2.7: Product Loading States and Skeletons

**GitHub Issue:** [#262](https://github.com/vovkins/agents-react-native-experiment-2/issues/262)  
**Size:** XS (<1 day)  
**Priority:** P0  
**Dependencies:** TASK-2.3, TASK-2.4  

#### Description
Implement loading skeleton components and empty states for product screens.

#### Acceptance Criteria
1. Product card skeleton component
2. Product detail skeleton component
3. Category section skeleton
4. Empty products state illustration
5. Error state with retry button
6. No search results state
7. Consistent styling with app theme

#### Technical Notes
- Use skeleton animation library or custom implementation
- Match exact dimensions of real components
- Consider shimmer effect
- Architecture: View layer

---

## Epic 3: Portfolio Dashboard (Портфель активов)

### TASK-3.1: Portfolio Domain Entities

**GitHub Issue:** [#263](https://github.com/vovkins/agents-react-native-experiment-2/issues/263)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** None (can start parallel with Epic 1)  

#### Description
Define domain entities for portfolio, assets, positions, and metrics.

#### Acceptance Criteria
1. Portfolio entity with total value, currency
2. Asset entity with name, symbol, type
3. Position entity with quantity, price, value
4. Metric entity for calculated values
5. TypeScript interfaces/types defined
6. Entity validation logic
7. Value formatting utilities (currency, percentage)

#### Technical Notes
- Architecture: Domain layer
- Include precision handling for financial values
- Support multiple currencies
- Use decimal.js or similar for precision
- Define Portfolio, Asset, Position, PortfolioMetric interfaces

---

### TASK-3.2: Portfolio API Adapter

**GitHub Issue:** [#264](https://github.com/vovkins/agents-react-native-experiment-2/issues/264)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-3.1, TASK-1.4  

#### Description
Implement adapter for fetching portfolio data from backend API.

#### Acceptance Criteria
1. PortfolioAdapter created in adapters layer
2. Fetch portfolio summary endpoint
3. Fetch portfolio positions endpoint
4. Fetch position details endpoint
5. Response mapping to domain entities
6. Error handling and parsing
7. Include auth token in requests

#### Technical Notes
- Architecture: Adapter layer
- Handle large response data efficiently
- Consider streaming for real-time updates
- Define PortfolioApiService interface
- Use dependency injection for adapter

---

### TASK-3.3: Portfolio Overview Screen UI

**GitHub Issue:** [#265](https://github.com/vovkins/agents-react-native-experiment-2/issues/265)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-3.1, TASK-3.2  

#### Description
Implement main portfolio screen showing total value, key metrics, and asset list.

#### Acceptance Criteria
1. Portfolio overview screen renders correctly
2. Display total portfolio value prominently
3. Display change (absolute and percentage)
4. Display key metrics (returns, etc.)
5. List of positions with brief info
6. Pull-to-refresh for data reload
7. Loading skeleton while fetching
8. Empty portfolio state for new clients
9. Error state on fetch failure

#### Technical Notes
- Performance critical - optimize renders
- Use FlatList for positions
- Consider charts for visualization
- Architecture: View layer
- Connect to PortfolioAdapter for data

---

### TASK-3.4: Portfolio Value Display Component

**GitHub Issue:** [#266](https://github.com/vovkins/agents-react-native-experiment-2/issues/266)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-3.1  

#### Description
Implement reusable component for displaying portfolio value with change indicators.

#### Acceptance Criteria
1. Displays total value with currency
2. Displays change (positive/negative with colors)
3. Displays percentage change
4. Animate value changes
5. Large text for prominent display
6. Color coding: green for positive, red for negative
7. Configurable precision
8. Accessibility support

#### Technical Notes
- Reusable component
- Consider animation library for number changes (react-native-reanimated)
- Format based on locale
- Architecture: View layer
- Props: value, change, changePercent, currency

---

### TASK-3.5: Position List Component

**GitHub Issue:** [#267](https://github.com/vovkins/agents-react-native-experiment-2/issues/267)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-3.1  

#### Description
Implement list component for displaying portfolio positions.

#### Acceptance Criteria
1. Position item displays name, symbol, value
2. Position item displays quantity and current price
3. Position item displays change indicator
4. Tap to view position details
5. Optimized for long lists
6. Sorted by value or configurable
7. Group by asset type option

#### Technical Notes
- Use FlatList with getItemLayout for performance
- Implement virtualization
- Memoize items with React.memo
- Architecture: View layer
- Props: positions, onPositionPress, sortBy

---

### TASK-3.6: Position Detail Screen UI

**GitHub Issue:** [#268](https://github.com/vovkins/agents-react-native-experiment-2/issues/268)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-3.1, TASK-3.2  

#### Description
Implement detailed position view showing full information about a single asset position.

#### Acceptance Criteria
1. Position detail screen renders correctly
2. Display asset name, symbol, type
3. Display quantity held
4. Display average purchase price
5. Display current price
6. Display current value
7. Display profit/loss (absolute and percentage)
8. Display position weight in portfolio
9. Back navigation to portfolio
10. Loading and error states

#### Technical Notes
- Consider mini-chart for price history
- May link to product details if applicable
- Architecture: View layer
- Route params: positionId

---

### TASK-3.7: Portfolio Metrics Calculation

**GitHub Issue:** [#269](https://github.com/vovkins/agents-react-native-experiment-2/issues/269)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-3.1  

#### Description
Implement domain logic for calculating portfolio metrics and returns.

#### Acceptance Criteria
1. Calculate total portfolio value
2. Calculate absolute profit/loss
3. Calculate percentage return
4. Calculate position weight percentage
5. Calculate daily/weekly/monthly returns (if data available)
6. Handle negative returns correctly
7. Handle currency formatting
8. Precision handling for financial calculations

#### Technical Notes
- Architecture: Domain layer
- Pure functions with test coverage
- Handle edge cases (zero values, new positions)
- Use decimal.js or similar for precision
- Define PortfolioCalculator service

---

### TASK-3.8: Portfolio Empty State

**GitHub Issue:** [#270](https://github.com/vovkins/agents-react-native-experiment-2/issues/270)  
**Size:** XS (<1 day)  
**Priority:** P0  
**Dependencies:** TASK-3.3  

#### Description
Implement empty state for users with no portfolio (new clients).

#### Acceptance Criteria
1. Empty portfolio illustration
2. Friendly message for new clients
3. Link or reference to products showcase
4. CTA to contact manager (link to chat)
5. Consistent styling with app theme

#### Technical Notes
- Consider onboarding hint
- Link to Epic 2 (Products) and Epic 4 (Chat)
- Architecture: View layer
- Use Lottie animation or static illustration

---

## Epic 4: Chat with Manager (Чат с менеджером)

### TASK-4.1: Chat Domain Entities

**GitHub Issue:** [#271](https://github.com/vovkins/agents-react-native-experiment-2/issues/271)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** None (can start parallel with Epic 1)  

#### Description
Define domain entities for messages, conversations, and chat participants.

#### Acceptance Criteria
1. Message entity (id, text, sender, timestamp, status)
2. Conversation entity (id, participants, last message)
3. Participant/User entity for chat context
4. Message status enum (sending, sent, delivered, read, failed)
5. TypeScript interfaces/types defined
6. Message sorting logic
7. Date grouping logic

#### Technical Notes
- Architecture: Domain layer
- Support future file attachments (out of MVP scope)
- Consider message types (text, system, etc.)
- Define Message, Conversation, ChatParticipant interfaces
- Define MessageStatus enum

---

### TASK-4.2: Chat API Adapter

**GitHub Issue:** [#272](https://github.com/vovkins/agents-react-native-experiment-2/issues/272)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-4.1, TASK-1.4  

#### Description
Implement adapter for chat REST API endpoints.

#### Acceptance Criteria
1. ChatAdapter created in adapters layer
2. Fetch conversation endpoint
3. Fetch messages endpoint (with pagination)
4. Send message endpoint
5. Mark messages as read endpoint
6. Response mapping to domain entities
7. Error handling and parsing
8. Include auth token in requests

#### Technical Notes
- Architecture: Adapter layer
- Handle message ordering
- Support pagination for history
- Define ChatApiService interface
- Use cursor-based pagination

---

### TASK-4.3: WebSocket Connection Management

**GitHub Issue:** [#273](https://github.com/vovkins/agents-react-native-experiment-2/issues/273)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-4.1, TASK-1.4  

#### Description
Implement WebSocket connection for real-time chat communication.

#### Acceptance Criteria
1. WebSocketService created in adapters layer
2. Connect to WebSocket endpoint
3. Handle connection events (open, close, error)
4. Reconnect on connection drop
5. Exponential backoff for reconnection
6. Authentication with WS (token passing)
7. Heartbeat/keep-alive mechanism
8. Clean disconnect on logout

#### Technical Notes
- Use react-native-url-polyfill or similar
- Handle network state changes
- Consider socket.io or native WebSocket
- Architecture: Adapter layer
- Define WebSocketEvent types

---

### TASK-4.4: Real-time Message Handling

**GitHub Issue:** [#274](https://github.com/vovkins/agents-react-native-experiment-2/issues/274)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-4.3, TASK-4.1  

#### Description
Implement real-time message sending and receiving logic.

#### Acceptance Criteria
1. Send message via WebSocket
2. Receive incoming messages via WebSocket
3. Message acknowledgment handling
4. Optimistic UI updates (show message immediately)
5. Message status updates (sent, delivered)
6. Handle message ordering
7. Handle duplicate messages
8. Queue messages when offline

#### Technical Notes
- Architecture: Domain + Adapter layer
- Use message IDs for correlation
- Handle race conditions
- Implement MessageService in domain layer
- Connect WebSocketService to ChatAdapter

---

### TASK-4.5: Chat Screen UI

**GitHub Issue:** [#275](https://github.com/vovkins/agents-react-native-experiment-2/issues/275)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-4.1, TASK-4.2, TASK-4.4  

#### Description
Implement main chat screen with message list and input.

#### Acceptance Criteria
1. Chat screen renders correctly
2. Message list displays conversation
3. Message input at bottom
4. Manager info header (name, status)
5. Auto-scroll to latest message
6. Loading state for initial load
7. Empty state for new conversation
8. Error state on connection failure
9. Keyboard handling for input

#### Technical Notes
- Use inverted FlatList for chat
- Handle keyboard show/hide
- Safe area insets for input
- Architecture: View layer
- Connect to ChatAdapter and WebSocketService

---

### TASK-4.6: Message List Component

**GitHub Issue:** [#276](https://github.com/vovkins/agents-react-native-experiment-2/issues/276)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-4.1  

#### Description
Implement message list with bubble styling, grouping, and infinite scroll.

#### Acceptance Criteria
1. Messages displayed in bubbles
2. Different styles for sent vs received
3. Timestamp display (on long press or visible)
4. Date separators for message groups
5. Avatar display for manager messages
6. Read/delivered status indicators
7. Infinite scroll for older messages
8. Smooth scrolling performance

#### Technical Notes
- Use FlatList with inverted prop
- Implement date grouping logic
- Optimize for large message lists
- Virtualization for performance
- Architecture: View layer
- Props: messages, onLoadMore, onMessageLongPress

---

### TASK-4.7: Message Input Component

**GitHub Issue:** [#277](https://github.com/vovkins/agents-react-native-experiment-2/issues/277)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-4.1  

#### Description
Implement message input with send button and character counter.

#### Acceptance Criteria
1. Text input with placeholder
2. Send button (enabled only when text present)
3. Character counter (optional limit)
4. Send on enter/return key
5. Auto-resize for multi-line
6. Disable while sending
7. Show sending indicator
8. Clear input after send

#### Technical Notes
- Use controlled input
- Handle keyboard actions
- Consider emoji support
- Architecture: View layer
- Props: onSend, placeholder, maxLength, disabled

---

### TASK-4.8: Manager Status Indicator

**GitHub Issue:** [#278](https://github.com/vovkins/agents-react-native-experiment-2/issues/278)  
**Size:** XS (<1 day)  
**Priority:** P0  
**Dependencies:** TASK-4.1  

#### Description
Implement component showing manager online/offline status.

#### Acceptance Criteria
1. Online indicator (green dot)
2. Offline indicator (gray dot)
3. Status text ("Online", "Offline", "Last seen...")
4. Display in chat header
5. Real-time status updates
6. Last seen timestamp when offline

#### Technical Notes
- Receive status via WebSocket
- Handle status changes gracefully
- Architecture: View layer
- Props: status, lastSeen

---

### TASK-4.9: Message Persistence Layer

**GitHub Issue:** [#279](https://github.com/vovkins/agents-react-native-experiment-2/issues/279)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-4.1, TASK-4.2  

#### Description
Implement local message storage for offline access and history.

#### Acceptance Criteria
1. Store messages locally (AsyncStorage or SQLite)
2. Retrieve messages for conversation
3. Store newest messages first
4. Handle storage limits (max messages stored)
5. Clear on logout
6. Query by conversation
7. Query by date range

#### Technical Notes
- Architecture: Data layer
- Consider Realm or SQLite for structured storage
- Implement storage limits/eviction policy
- Define MessageStorage interface
- Use watermelondb or realm for better performance

---

### TASK-4.10: Offline Message Queue

**GitHub Issue:** [#280](https://github.com/vovkins/agents-react-native-experiment-2/issues/280)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-4.4, TASK-4.9  

#### Description
Implement queue for messages sent while offline.

#### Acceptance Criteria
1. Queue messages when no connection
2. Store queued messages locally
3. Retry sending on connection restore
4. Show queued status in UI
5. Handle queue on logout (clear)
6. Limit queue size
7. Notify user of pending messages

#### Technical Notes
- Use message status "queued"
- Process FIFO queue on reconnect
- Handle send failures after retry
- Architecture: Domain layer
- Define OfflineMessageQueue service

---

### TASK-4.11: Chat History Pagination

**GitHub Issue:** [#281](https://github.com/vovkins/agents-react-native-experiment-2/issues/281)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-4.2, TASK-4.6  

#### Description
Implement pagination for loading older chat history.

#### Acceptance Criteria
1. Load initial batch of messages
2. Load more on scroll to top
3. Loading indicator for pagination
4. Handle end of history
5. Maintain scroll position
6. Cache loaded pages locally
7. Resume from last position

#### Technical Notes
- Cursor-based pagination
- Use before/after timestamps
- Merge paginated results with existing
- Architecture: Domain + View layer
- Integrate with ChatAdapter

---

## Epic 5: Navigation & App Structure

### TASK-5.1: Navigation Structure Setup

**GitHub Issue:** [#282](https://github.com/vovkins/agents-react-native-experiment-2/issues/282)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-1.4  

#### Description
Set up the main navigation structure with React Navigation including auth flow and main app flow.

#### Acceptance Criteria
1. NavigationContainer configured
2. Auth stack (login, etc.)
3. Main app tab navigator
4. Auth state controls navigation
5. Proper initial route based on auth
6. Transition between auth and main app
7. Navigation types defined

#### Technical Notes
- Use @react-navigation/native
- Stack navigator for auth
- Tab navigator for main app
- Consider navigation state persistence
- Architecture: View layer
- Define AppNavigation and AuthNavigation types

---

### TASK-5.2: Tab Bar Component

**GitHub Issue:** [#283](https://github.com/vovkins/agents-react-native-experiment-2/issues/283)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-5.1  

#### Description
Implement custom bottom tab bar with three main sections.

#### Acceptance Criteria
1. Three tabs: Products, Portfolio, Chat
2. Tab icons with labels
3. Active tab highlighting
4. Platform-appropriate styling
5. Safe area handling
6. Tab press handling
7. Haptic feedback on tab switch (optional)
8. Accessibility labels

#### Technical Notes
- Use @react-navigation/bottom-tabs
- Or custom tab bar component
- Consider react-native-reanimated for animations
- Architecture: View layer
- Define TabConfig interface

---

### TASK-5.3: Tab Icons and Styling

**GitHub Issue:** [#284](https://github.com/vovkins/agents-react-native-experiment-2/issues/284)  
**Size:** XS (<1 day)  
**Priority:** P0  
**Dependencies:** TASK-5.2  

#### Description
Create and implement tab icons with proper styling for both platforms.

#### Acceptance Criteria
1. Icons for Products, Portfolio, Chat tabs
2. Active and inactive icon variants
3. Consistent icon sizing
4. Platform-specific icons (iOS SF Symbols vs Android)
5. Proper icon colors
6. Smooth transition between states

#### Technical Notes
- Use react-native-vector-icons or SVG
- Consider platform-specific icon sets
- Optimize icon assets
- Architecture: View layer
- Use Ionicons or MaterialCommunityIcons

---

### TASK-5.4: Screen Wrappers and Layouts

**GitHub Issue:** [#285](https://github.com/vovkins/agents-react-native-experiment-2/issues/285)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-5.1  

#### Description
Implement screen wrapper components with consistent headers and layouts.

#### Acceptance Criteria
1. ScreenWrapper component created
2. Header component with title, back button
3. Safe area handling
4. Loading overlay capability
5. Error boundary integration
6. Scroll behavior standardization
7. Pull-to-refresh capability

#### Technical Notes
- Reusable for all screens
- Handle keyboard avoiding view
- Platform-specific header styles
- Architecture: View layer
- Props: title, showBack, loading, error

---

### TASK-5.5: Navigation State Preservation

**GitHub Issue:** [#286](https://github.com/vovkins/agents-react-native-experiment-2/issues/286)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-5.1, TASK-5.2  

#### Description
Implement state preservation when switching between tabs.

#### Acceptance Criteria
1. Tab screens maintain state on switch
2. Scroll position preserved
3. Form data preserved
4. Loading states preserved
5. Memory-efficient state storage
6. Reset state when needed (explicit action)
7. Handle low memory scenarios

#### Technical Notes
- Use screen unmount prevention
- Consider lazy loading
- Balance memory vs UX
- Architecture: View layer
- Use React Navigation's state preservation

---

### TASK-5.6: Deep Linking Configuration

**GitHub Issue:** [#287](https://github.com/vovkins/agents-react-native-experiment-2/issues/287)  
**Size:** M (2-3 days)  
**Priority:** P0  
**Dependencies:** TASK-5.1  

#### Description
Configure deep linking for push notifications and external links.

#### Acceptance Criteria
1. Deep link scheme configured (myapp://)
2. Link to specific tabs
3. Link to product detail
4. Link to chat screen
5. Handle invalid deep links
6. Handle deep link when logged out
7. Universal links (iOS) and App Links (Android)

#### Technical Notes
- Use @react-navigation/native linking
- Configure iOS Associated Domains
- Configure Android App Links
- Handle authentication for protected links
- Architecture: View layer
- Define deep link config object

---

### TASK-5.7: Tab Badge Support

**GitHub Issue:** [#288](https://github.com/vovkins/agents-react-native-experiment-2/issues/288)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-5.2  

#### Description
Implement badge support for tab bar (unread count, notifications).

#### Acceptance Criteria
1. Badge on Chat tab for unread messages
2. Badge styling (red dot or number)
3. Badge count updates in real-time
4. Clear badge on tab visit
5. Handle badge overflow (99+)
6. Badge positioning
7. Platform-specific badge styles

#### Technical Notes
- Connect to chat unread count
- Use badge prop from navigation
- Update on message read
- Architecture: View layer
- Integrate with chat state

---

### TASK-5.8: Transition Animations

**GitHub Issue:** [#289](https://github.com/vovkins/agents-react-native-experiment-2/issues/289)  
**Size:** S (1-2 days)  
**Priority:** P0  
**Dependencies:** TASK-5.1  

#### Description
Implement smooth transition animations for navigation.

#### Acceptance Criteria
1. Screen push animation (slide)
2. Screen pop animation (slide back)
3. Tab switch animation (fade or none)
4. Auth to main app transition
5. Consistent animation duration
6. Platform-appropriate animations
7. Reduced motion support (accessibility)

#### Technical Notes
- Use react-native-reanimated
- Configure navigation animations
- iOS and Android specific defaults
- Architecture: View layer
- Support prefers-reduced-motion

---

## Epic 6: Data Synchronization & Offline Support

### TASK-6.1: Local Storage Setup

**GitHub Issue:** [#290](https://github.com/vovkins/agents-react-native-experiment-2/issues/290)  
**Size:** M (2-3 days)  
**Priority:** P2  
**Dependencies:** TASK-2.1, TASK-3.1, TASK-4.1  

#### Description
Set up local database/storage solution for caching app data.

#### Acceptance Criteria
1. Storage solution selected and configured (Realm/SQLite/MMKV)
2. Storage service created
3. Clear storage on logout
4. Handle storage errors
5. Storage size monitoring
6. Migrations handling
7. TypeScript types for storage

#### Technical Notes
- Architecture: Data layer
- Consider Realm for complex data
- Or MMKV for key-value
- Or SQLite for SQL-based
- Define StorageService interface
- Implement storage migration strategy

---

### TASK-6.2: Cache Service Implementation

**GitHub Issue:** [#291](https://github.com/vovkins/agents-react-native-experiment-2/issues/291)  
**Size:** M (2-3 days)  
**Priority:** P2  
**Dependencies:** TASK-6.1  

#### Description
Implement caching service for products, portfolio, and messages.

#### Acceptance Criteria
1. Cache products list
2. Cache portfolio data
3. Cache messages
4. Cache invalidation timestamps
5. Max age for cached data
6. Force refresh capability
7. Cache clear capability
8. Partial cache update

#### Technical Notes
- Implement per-entity caching
- Use timestamps or versions for invalidation
- Consider stale-while-revalidate pattern
- Architecture: Domain + Data layer
- Define CacheService interface

---

### TASK-6.3: Sync Engine Logic

**GitHub Issue:** [#292](https://github.com/vovkins/agents-react-native-experiment-2/issues/292)  
**Size:** L (3-5 days)  
**Priority:** P2  
**Dependencies:** TASK-6.2, TASK-2.2, TASK-3.2, TASK-4.2  

#### Description
Implement synchronization engine for keeping local and remote data in sync.

#### Acceptance Criteria
1. Sync products on app launch
2. Sync portfolio on app launch
3. Sync messages on app launch
4. Periodic sync (configurable interval)
5. Manual sync trigger
6. Sync queue management
7. Sync status tracking
8. Handle concurrent syncs

#### Technical Notes
- Architecture: Domain + Adapter layer
- Use background tasks or timers
- Consider delta sync (only changes)
- Define SyncEngine service
- Implement sync status enum

---

### TASK-6.4: Conflict Resolution Strategy

**GitHub Issue:** [#293](https://github.com/vovkins/agents-react-native-experiment-2/issues/293)  
**Size:** M (2-3 days)  
**Priority:** P2  
**Dependencies:** TASK-6.3  

#### Description
Implement conflict resolution for data sync conflicts.

#### Acceptance Criteria
1. Detect conflicts (local vs server)
2. Resolve based on timestamp (last write wins)
3. Or resolve based on version
4. Log conflicts for debugging
5. Handle unresolvable conflicts (use server)
6. Notify user of major conflicts (optional)
7. Conflict resolution UI (future consideration)

#### Technical Notes
- Consider operational transforms
- Use version vectors if needed
- Server usually wins for financial data
- Architecture: Domain layer
- Define ConflictResolver service

---

### TASK-6.5: Network Status Monitoring

**GitHub Issue:** [#294](https://github.com/vovkins/agents-react-native-experiment-2/issues/294)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** None  

#### Description
Implement network connectivity monitoring service.

#### Acceptance Criteria
1. Detect online/offline status
2. Detect connection type (wifi, cellular)
3. Status change events
4. Provide network status to app
5. Exponential backoff on reconnect attempts
6. Handle airplane mode
7. Test with network simulation

#### Technical Notes
- Use @react-native-community/netinfo
- Or react-native-offline
- Consider reachability for specific endpoints
- Architecture: Adapter layer
- Define NetworkStatusService

---

### TASK-6.6: Connection Indicator UI

**GitHub Issue:** [#295](https://github.com/vovkins/agents-react-native-experiment-2/issues/295)  
**Size:** XS (<1 day)  
**Priority:** P2  
**Dependencies:** TASK-6.5  

#### Description
Implement UI indicator for connection status.

#### Acceptance Criteria
1. Offline banner at top of screen
2. Syncing indicator (optional)
3. Color-coded status (green/yellow/red)
4. Dismissible (remembers dismissal)
5. Appears when offline
6. Auto-hide when online
7. Accessible announcement

#### Technical Notes
- Use global overlay or header
- Connect to network status service
- Consider toast notification
- Architecture: View layer
- Define ConnectionBanner component

---

### TASK-6.7: Background Sync Triggers

**GitHub Issue:** [#296](https://github.com/vovkins/agents-react-native-experiment-2/issues/296)  
**Size:** M (2-3 days)  
**Priority:** P2  
**Dependencies:** TASK-6.3, TASK-6.5  

#### Description
Implement background sync triggers based on app state and network events.

#### Acceptance Criteria
1. Sync when app comes to foreground
2. Sync when network reconnects
3. Sync when app becomes active
4. Throttle sync frequency
5. Cancel sync on app backgrounding
6. Handle app termination
7. Background fetch (if supported)

#### Technical Notes
- Use AppState API
- Consider react-native-background-fetch
- Balance battery vs freshness
- Architecture: Domain layer
- Define SyncTriggerService

---

### TASK-6.8: Sync Status Display

**GitHub Issue:** [#297](https://github.com/vovkins/agents-react-native-experiment-2/issues/297)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** TASK-6.3  

#### Description
Implement UI for displaying sync status to users.

#### Acceptance Criteria
1. Last synced timestamp
2. Syncing indicator (spinner)
3. Sync failed indicator
4. Retry button on failure
5. Pull-to-refresh triggers sync
6. Status in relevant screens
7. Optional: sync details modal

#### Technical Notes
- Display in header or pull-to-refresh
- Use sync state from sync engine
- Consider per-entity sync status
- Architecture: View layer
- Define SyncStatusIndicator component

---

## Epic 7: Push Notifications

### TASK-7.1: Push Notification Permission Handling

**GitHub Issue:** [#298](https://github.com/vovkins/agents-react-native-experiment-2/issues/298)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** None  

#### Description
Implement push notification permission request and handling.

#### Acceptance Criteria
1. Request permission on appropriate trigger
2. Handle permission granted
3. Handle permission denied
4. Handle "ask later" option
5. Check current permission status
6. Open settings if denied
7. Show rationale for permission

#### Technical Notes
- Use react-native-push-notification or expo-notifications
- iOS: request at appropriate time
- Android: request on first use or manifest
- Architecture: Adapter layer
- Define NotificationPermissionService

---

### TASK-7.2: APNs/FCM Token Registration

**GitHub Issue:** [#299](https://github.com/vovkins/agents-react-native-experiment-2/issues/299)  
**Size:** M (2-3 days)  
**Priority:** P2  
**Dependencies:** TASK-7.1, TASK-1.4  

#### Description
Implement device token registration with Apple Push Notification service and Firebase Cloud Messaging.

#### Acceptance Criteria
1. Register for APNs (iOS)
2. Register for FCM (Android)
3. Store device token locally
4. Send token to backend server
5. Handle token refresh
6. Handle registration failure
7. Platform-specific implementations

#### Technical Notes
- iOS: APNs device token
- Android: FCM registration token
- Store token with user account
- Token may change, handle updates
- Architecture: Adapter layer
- Define TokenRegistrationService

---

### TASK-7.3: Notification Service Integration

**GitHub Issue:** [#300](https://github.com/vovkins/agents-react-native-experiment-2/issues/300)  
**Size:** M (2-3 days)  
**Priority:** P2  
**Dependencies:** TASK-7.2  

#### Description
Integrate with backend notification service for sending and receiving notifications.

#### Acceptance Criteria
1. Notification service adapter created
2. Subscribe to notification topics
3. Handle notification received
4. Handle notification opened
5. Display notification in foreground
6. Queue notification for background
7. Parse notification payload

#### Technical Notes
- Architecture: Adapter layer
- Handle both data and notification payloads
- Consider notification channels (Android)
- Define NotificationService interface
- Use @react-native-firebase/messaging

---

### TASK-7.4: Chat Notification Handler

**GitHub Issue:** [#301](https://github.com/vovkins/agents-react-native-experiment-2/issues/301)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** TASK-7.3, TASK-4.5  

#### Description
Implement notification handling specifically for new chat messages.

#### Acceptance Criteria
1. Receive chat notification payload
2. Display notification with sender name and message preview
3. Navigate to chat on tap
4. Update unread count badge
5. Handle notification while in chat (suppress)
6. Handle notification when app killed
7. Mark as read when notification opened

#### Technical Notes
- Deep link to chat screen
- Suppress if already in chat
- Update badge count
- Architecture: Domain + Adapter layer
- Define ChatNotificationHandler

---

### TASK-7.5: Portfolio Notification Handler

**GitHub Issue:** [#302](https://github.com/vovkins/agents-react-native-experiment-2/issues/302)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** TASK-7.3, TASK-3.3  

#### Description
Implement notification handling for portfolio change alerts.

#### Acceptance Criteria
1. Receive portfolio notification payload
2. Display notification with summary
3. Navigate to portfolio on tap
4. Refresh portfolio data on open
5. Handle significant change threshold
6. User preference for portfolio notifications

#### Technical Notes
- Deep link to portfolio screen
- Trigger data refresh on open
- May include change amount in payload
- Architecture: Domain + Adapter layer
- Define PortfolioNotificationHandler

---

### TASK-7.6: Deep Link Routing

**GitHub Issue:** [#303](https://github.com/vovkins/agents-react-native-experiment-2/issues/303)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** TASK-5.6, TASK-7.3  

#### Description
Implement routing from notification deep links to specific screens.

#### Acceptance Criteria
1. Parse deep link from notification payload
2. Route to correct screen
3. Handle auth requirement
4. Handle invalid deep links
5. Handle deep link parameters
6. Maintain navigation history
7. Support all notification types

#### Technical Notes
- Use existing deep link config
- Handle both cold start and warm start
- Queue navigation if auth required
- Architecture: View + Domain layer
- Define NotificationDeepLinkHandler

---

### TASK-7.7: Foreground Notification Handling

**GitHub Issue:** [#304](https://github.com/vovkins/agents-react-native-experiment-2/issues/304)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** TASK-7.3  

#### Description
Implement in-app notification display when app is in foreground.

#### Acceptance Criteria
1. Show in-app notification banner
2. Banner auto-dismisses after timeout
3. User can tap to action
4. User can swipe to dismiss
5. Banner doesn't block interactions
6. Queue multiple notifications
7. Style matches app theme

#### Technical Notes
- Use custom banner component or library
- Position below header or at top
- Consider toast/snackbar pattern
- Architecture: View layer
- Define InAppNotificationBanner component

---

### TASK-7.8: Notification Settings UI

**GitHub Issue:** [#305](https://github.com/vovkins/agents-react-native-experiment-2/issues/305)  
**Size:** S (1-2 days)  
**Priority:** P2  
**Dependencies:** TASK-7.1, Epic 8  

#### Description
Implement notification settings/preferences UI in profile section.

#### Acceptance Criteria
1. Toggle for chat notifications
2. Toggle for portfolio notifications
3. Toggle for product updates (future)
4. Open system settings link
5. Show current permission status
6. Save preferences to backend
7. Real-time toggle effect

#### Technical Notes
- Part of Epic 8 (Profile)
- Save preferences server-side
- Handle permission not granted state
- Architecture: View layer
- Define NotificationSettings component

---

## Epic 8: User Profile & Settings

### TASK-8.1: Profile Screen UI

**GitHub Issue:** [#306](https://github.com/vovkins/agents-react-native-experiment-2/issues/306)  
**Size:** M (2-3 days)  
**Priority:** P3  
**Dependencies:** TASK-1.4  

#### Description
Implement user profile screen showing personal information.

#### Acceptance Criteria
1. Profile screen renders correctly
2. Display user name
3. Display user email
4. Display user phone (if available)
5. Display account type/status
6. Profile avatar/placeholder
7. Edit profile (if supported, or read-only)
8. Settings list below profile
9. Loading and error states

#### Technical Notes
- Access from settings or dedicated tab
- Consider separate API for profile data
- May need profile adapter
- Architecture: View layer
- Define ProfileScreen component

---

### TASK-8.2: Profile Data Fetching

**GitHub Issue:** [#307](https://github.com/vovkins/agents-react-native-experiment-2/issues/307)  
**Size:** S (1-2 days)  
**Priority:** P3  
**Dependencies:** TASK-8.1  

#### Description
Implement API integration for fetching user profile data.

#### Acceptance Criteria
1. ProfileAdapter created
2. Fetch profile endpoint
3. Response mapping to user entity
4. Error handling
5. Caching profile data
6. Refresh on pull-to-refresh
7. Use cached data when offline

#### Technical Notes
- Architecture: Adapter layer
- May be part of auth user data
- Handle partial data
- Define ProfileApiService interface
- Use dependency injection

---

### TASK-8.3: Security Settings Section

**GitHub Issue:** [#308](https://github.com/vovkins/agents-react-native-experiment-2/issues/308)  
**Size:** M (2-3 days)  
**Priority:** P3  
**Dependencies:** TASK-1.6, TASK-1.7  

#### Description
Implement security settings section with biometric and PIN controls.

#### Acceptance Criteria
1. Biometric auth toggle
2. PIN code toggle
3. Change PIN button
4. Security status indicators
5. Require re-auth to change settings
6. Handle biometric not available
7. Handle PIN not set

#### Technical Notes
- Use settings from Epic 1
- Secure auth before allowing changes
- Update preferences in storage
- Architecture: View layer
- Define SecuritySettings component

---

### TASK-8.4: Logout with Data Cleanup

**GitHub Issue:** [#309](https://github.com/vovkins/agents-react-native-experiment-2/issues/309)  
**Size:** S (1-2 days)  
**Priority:** P3  
**Dependencies:** TASK-1.9, TASK-6.1  

#### Description
Implement complete logout with all data cleanup.

#### Acceptance Criteria
1. Logout button accessible
2. Confirmation dialog
3. Clear all cached data
4. Clear local storage
5. Clear sync queue
6. Clear message storage
7. Reset all state
8. Navigate to login
9. Handle logout API call

#### Technical Notes
- Comprehensive cleanup required
- Logout from auth service
- Clear navigation stack
- May need async cleanup
- Architecture: Domain layer
- Define LogoutService

---

### TASK-8.5: About/Version Info Screen

**GitHub Issue:** [#310](https://github.com/vovkins/agents-react-native-experiment-2/issues/310)  
**Size:** XS (<1 day)  
**Priority:** P3  
**Dependencies:** TASK-8.1  

#### Description
Implement about screen with app version and legal information.

#### Acceptance Criteria
1. App version display
2. Build number display
3. Terms of service link
4. Privacy policy link
5. Contact/support link
6. Logo and branding
7. Consistent styling

#### Technical Notes
- Read version from app config
- External links to web pages
- Consider in-app webview for legal
- Architecture: View layer
- Define AboutScreen component
- Use react-native-device-info for version

---

## Task Summary

| Task ID | Task Name | Size | Priority | GitHub Issue |
|---------|-----------|------|----------|--------------|
| TASK-1.1 | Login Screen UI | M | P0 | #247 |
| TASK-1.2 | Backend Auth API Integration | M | P0 | #248 |
| TASK-1.3 | Secure Token Storage | S | P0 | #249 |
| TASK-1.4 | Session Management & Auth State | M | P0 | #250 |
| TASK-1.5 | Token Refresh Mechanism | M | P0 | #251 |
| TASK-1.6 | Biometric Authentication Module | M | P0 | #252 |
| TASK-1.7 | PIN Code Setup and Validation | M | P0 | #253 |
| TASK-1.8 | Error Handling and Auth Flows | S | P0 | #254 |
| TASK-1.9 | Logout Functionality | XS | P0 | #255 |
| TASK-2.1 | Product Domain Entities | S | P0 | #256 |
| TASK-2.2 | Product API Adapter | S | P0 | #257 |
| TASK-2.3 | Product List Screen UI | M | P0 | #258 |
| TASK-2.4 | Strategy Card Component | S | P0 | #259 |
| TASK-2.5 | Product Detail Screen UI | M | P0 | #260 |
| TASK-2.6 | Product Categorization Logic | S | P0 | #261 |
| TASK-2.7 | Product Loading States and Skeletons | XS | P0 | #262 |
| TASK-3.1 | Portfolio Domain Entities | S | P0 | #263 |
| TASK-3.2 | Portfolio API Adapter | S | P0 | #264 |
| TASK-3.3 | Portfolio Overview Screen UI | M | P0 | #265 |
| TASK-3.4 | Portfolio Value Display Component | S | P0 | #266 |
| TASK-3.5 | Position List Component | S | P0 | #267 |
| TASK-3.6 | Position Detail Screen UI | M | P0 | #268 |
| TASK-3.7 | Portfolio Metrics Calculation | M | P0 | #269 |
| TASK-3.8 | Portfolio Empty State | XS | P0 | #270 |
| TASK-4.1 | Chat Domain Entities | S | P0 | #271 |
| TASK-4.2 | Chat API Adapter | S | P0 | #272 |
| TASK-4.3 | WebSocket Connection Management | M | P0 | #273 |
| TASK-4.4 | Real-time Message Handling | M | P0 | #274 |
| TASK-4.5 | Chat Screen UI | M | P0 | #275 |
| TASK-4.6 | Message List Component | M | P0 | #276 |
| TASK-4.7 | Message Input Component | S | P0 | #277 |
| TASK-4.8 | Manager Status Indicator | XS | P0 | #278 |
| TASK-4.9 | Message Persistence Layer | M | P0 | #279 |
| TASK-4.10 | Offline Message Queue | S | P0 | #280 |
| TASK-4.11 | Chat History Pagination | S | P0 | #281 |
| TASK-5.1 | Navigation Structure Setup | M | P0 | #282 |
| TASK-5.2 | Tab Bar Component | S | P0 | #283 |
| TASK-5.3 | Tab Icons and Styling | XS | P0 | #284 |
| TASK-5.4 | Screen Wrappers and Layouts | S | P0 | #285 |
| TASK-5.5 | Navigation State Preservation | M | P0 | #286 |
| TASK-5.6 | Deep Linking Configuration | M | P0 | #287 |
| TASK-5.7 | Tab Badge Support | S | P0 | #288 |
| TASK-5.8 | Transition Animations | S | P0 | #289 |
| TASK-6.1 | Local Storage Setup | M | P2 | #290 |
| TASK-6.2 | Cache Service Implementation | M | P2 | #291 |
| TASK-6.3 | Sync Engine Logic | L | P2 | #292 |
| TASK-6.4 | Conflict Resolution Strategy | M | P2 | #293 |
| TASK-6.5 | Network Status Monitoring | S | P2 | #294 |
| TASK-6.6 | Connection Indicator UI | XS | P2 | #295 |
| TASK-6.7 | Background Sync Triggers | M | P2 | #296 |
| TASK-6.8 | Sync Status Display | S | P2 | #297 |
| TASK-7.1 | Push Notification Permission | S | P2 | #298 |
| TASK-7.2 | APNs/FCM Token Registration | M | P2 | #299 |
| TASK-7.3 | Notification Service Integration | M | P2 | #300 |
| TASK-7.4 | Chat Notification Handler | S | P2 | #301 |
| TASK-7.5 | Portfolio Notification Handler | S | P2 | #302 |
| TASK-7.6 | Deep Link Routing | S | P2 | #303 |
| TASK-7.7 | Foreground Notification Handling | S | P2 | #304 |
| TASK-7.8 | Notification Settings UI | S | P2 | #305 |
| TASK-8.1 | Profile Screen UI | M | P3 | #306 |
| TASK-8.2 | Profile Data Fetching | S | P3 | #307 |
| TASK-8.3 | Security Settings Section | M | P3 | #308 |
| TASK-8.4 | Logout with Data Cleanup | S | P3 | #309 |
| TASK-8.5 | About/Version Info Screen | XS | P3 | #310 |

---

## Size Distribution

| Size | Count | Est. Days |
|------|-------|-----------|
| XS | 8 | 4-8 days |
| S | 22 | 22-44 days |
| M | 27 | 54-81 days |
| L | 1 | 3-5 days |
| **Total** | **58** | **83-138 days** |

---

## Priority Distribution

| Priority | Milestone | Task Count |
|----------|-----------|------------|
| P0 | MVP v1.0 | 43 tasks |
| P2 | v1.1 | 12 tasks |
| P3 | v1.2 | 5 tasks |

---

## Epic Distribution

| Epic | Task Count |
|------|------------|
| Epic 1: Authentication & Onboarding | 9 tasks |
| Epic 2: Product Showcase | 7 tasks |
| Epic 3: Portfolio Dashboard | 8 tasks |
| Epic 4: Chat with Manager | 11 tasks |
| Epic 5: Navigation & App Structure | 8 tasks |
| Epic 6: Data Synchronization & Offline | 8 tasks |
| Epic 7: Push Notifications | 8 tasks |
| Epic 8: User Profile & Settings | 5 tasks |

---

*Generated by Business Analyst Agent*