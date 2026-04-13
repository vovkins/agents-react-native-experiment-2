# Task Specifications - Decomposed from PRD Features

## Document Information
- **Source:** docs/requirements/feature-extracted-features.md
- **Product:** Мобильное приложение для клиентов управляющей компании
- **Technology:** React Native (iOS/Android)
- **Analysis Date:** 2026-04-13
- **Analyst:** Business Analyst Agent

---

## Task Sizing Legend

| Size | Duration | Description |
|------|----------|-------------|
| XS | < 1 day | Trivial task, minimal effort |
| S | 1-2 days | Simple task, straightforward implementation |
| M | 2-3 days | Moderate complexity, clear requirements |
| L | 3-5 days | Complex task, multiple components |
| XL | > 5 days | Should be split into smaller tasks |

---

## INVEST Criteria Checklist

- **I**ndependent: Task can be completed alone
- **N**egotiable: Details can be discussed
- **V**aluable: Adds value to the product
- **E**stimable: Can be estimated
- **S**mall: Can be completed in reasonable time
- **T**estable: Can be verified

---

## PHASE 1: FOUNDATION (MUST HAVE)

---

### FR-001: Аутентификация и авторизация

---

#### TASK-001-01: Auth Infrastructure Setup

**Parent Feature:** FR-001 - Аутентификация и авторизация

**Description:**
Создание базовой инфраструктуры для аутентификации: API клиент, управление токенами, безопасное хранение учетных данных.

**Acceptance Criteria:**
- [ ] API client configured with base URL and interceptors
- [ ] Token storage implemented using Keychain (iOS) and Keystore (Android)
- [ ] Token refresh mechanism implemented
- [ ] Auth state management (Context/Redux) created
- [ ] Auth interceptor for adding Bearer token to requests
- [ ] Unit tests for token management (min 80% coverage)

**Technical Notes:**
- Use react-native-keychain for secure storage
- Implement Axios interceptors for token handling
- Consider using react-query or Apollo for API state management
- Store both access and refresh tokens

**Size:** M (2-3 days)

**Dependencies:** None (foundational task)

**Blocked By:** None

**Blocks:** TASK-001-02, TASK-001-03, TASK-001-04, TASK-001-05

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-001-02: Login Screen and Flow

**Parent Feature:** FR-001 - Аутентификация и авторизация

**Description:**
Реализация экрана входа в систему с формой логина/пароля и интеграцией с API аутентификации.

**Acceptance Criteria:**
- [ ] Login screen UI implemented according to design
- [ ] Email/phone and password input fields with validation
- [ ] "Forgot password" link navigates to recovery flow
- [ ] Login API integration working
- [ ] Error messages displayed for invalid credentials
- [ ] Loading state during authentication
- [ ] Navigation to main app on successful login
- [ ] Network error handling with retry option
- [ ] E2E tests for login flow

**Technical Notes:**
- Use react-hook-form for form validation
- Implement proper keyboard handling
- Add accessibility labels for screen readers
- Handle biometric prompt setup (preparation for FR-006)

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-001-03: Registration Screen and Flow

**Parent Feature:** FR-001 - Аутентификация и авторизация

**Description:**
Реализация экрана регистрации нового пользователя после заключения договора.

**Acceptance Criteria:**
- [ ] Registration screen UI implemented according to design
- [ ] Form fields: name, email, phone, password, confirm password
- [ ] Password strength indicator
- [ ] Terms of service acceptance checkbox
- [ ] Registration API integration working
- [ ] Email/phone validation
- [ ] Duplicate email/phone error handling
- [ ] Success screen and navigation to main app
- [ ] E2E tests for registration flow

**Technical Notes:**
- Password requirements: min 8 chars, uppercase, lowercase, number
- Consider phone number formatting library (libphonenumber)
- Add privacy policy link

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-001-04: Password Recovery Flow

**Parent Feature:** FR-001 - Аутентификация и авторизация

**Description:**
Реализация функции восстановления пароля через email или SMS.

**Acceptance Criteria:**
- [ ] "Forgot password" screen with email/phone input
- [ ] Verification code input screen
- [ ] New password setup screen
- [ ] API integration for password reset request
- [ ] API integration for code verification
- [ ] API integration for password update
- [ ] Error handling for expired/invalid codes
- [ ] Resend code functionality with cooldown timer
- [ ] Success confirmation and redirect to login
- [ ] E2E tests for recovery flow

**Technical Notes:**
- Implement rate limiting for code resends
- Consider using OTP input component for better UX
- Clear navigation stack after successful recovery

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-001-05: Session Timeout Management

**Parent Feature:** FR-001 - Аутентификация и авторизация

**Description:**
Реализация автоматического выхода пользователя после периода неактивности.

**Acceptance Criteria:**
- [ ] Configurable session timeout (default 30 min)
- [ ] Timer reset on user activity (tap, scroll)
- [ ] Timer reset on API calls
- [ ] Modal warning before logout (1 min before)
- [ ] Automatic logout and redirect to login screen
- [ ] Option to extend session from warning modal
- [ ] Clear stored tokens on logout
- [ ] Unit tests for timeout logic

**Technical Notes:**
- Use AppState for background/foreground detection
- Consider using react-native-interactive
- Pause timer when app goes to background

**Size:** S (1-2 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

### FR-002: Витрина продуктов

---

#### TASK-002-01: Products List Screen

**Parent Feature:** FR-002 - Витрина продуктов

**Description:**
Реализация экрана со списком инвестиционных продуктов и стратегий.

**Acceptance Criteria:**
- [ ] Products list screen UI implemented according to design
- [ ] Product cards showing: name, risk level, return, min investment
- [ ] Pull-to-refresh functionality
- [ ] Loading skeleton during data fetch
- [ ] Empty state when no products available
- [ ] Error state with retry button
- [ ] Navigation to product detail on card tap
- [ ] Products API integration
- [ ] Basic filtering by product type
- [ ] E2E tests for products list

**Technical Notes:**
- Use FlatList with optimized renderItem
- Implement pagination if list is large
- Cache products data for offline access
- Consider using react-query for caching

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** TASK-002-02

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-002-02: Product Detail Screen

**Parent Feature:** FR-002 - Витрина продуктов

**Description:**
Реализация детального экрана продукта с полной информацией о стратегии.

**Acceptance Criteria:**
- [ ] Product detail screen UI implemented according to design
- [ ] Product header with name, risk badge, key metrics
- [ ] Strategy description section
- [ ] Historical performance section
- [ ] Risk metrics and indicators
- [ ] Investment requirements section
- [ ] "Contact manager" CTA button
- [ ] Share product functionality
- [ ] Loading and error states
- [ ] Deep link support for product URLs
- [ ] E2E tests for product detail

**Technical Notes:**
- Implement scrollable content with sticky header
- Add animations for smooth transitions
- Consider adding related products section

**Size:** M (2-3 days)

**Dependencies:** TASK-002-01 (Products List Screen)

**Blocked By:** TASK-002-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-002-03: Products Offline Support

**Parent Feature:** FR-002 - Витрина продуктов

**Description:**
Реализация кэширования данных о продуктах для офлайн доступа.

**Acceptance Criteria:**
- [ ] Products data cached locally on successful fetch
- [ ] Cached data shown when offline
- [ ] Offline indicator displayed when using cached data
- [ ] Automatic cache refresh when back online
- [ ] Cache invalidation policy (max age 24h)
- [ ] Manual refresh forces new data fetch
- [ ] Cache cleared on logout
- [ ] Unit tests for caching logic

**Technical Notes:**
- Use AsyncStorage or MMKV for cache storage
- Implement with react-query offline support
- Consider using NetInfo for connectivity detection

**Size:** S (1-2 days)

**Dependencies:** TASK-002-01 (Products List Screen)

**Blocked By:** TASK-002-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

### FR-003: Портфель активов

---

#### TASK-003-01: Portfolio Overview Screen

**Parent Feature:** FR-003 - Портфель активов

**Description:**
Реализация главного экрана портфеля с общей информацией и списком активов.

**Acceptance Criteria:**
- [ ] Portfolio overview screen UI implemented according to design
- [ ] Total portfolio value prominently displayed
- [ ] Period change indicator (absolute and percentage)
- [ ] List of portfolio assets with weights and values
- [ ] Pull-to-refresh functionality
- [ ] Loading skeleton during data fetch
- [ ] Empty state when no portfolio
- [ ] Error state with retry button
- [ ] Last update timestamp displayed
- [ ] Portfolio API integration
- [ ] E2E tests for portfolio overview

**Technical Notes:**
- Use FlatList for assets list
- Implement efficient re-renders with memo
- Consider using react-query for state management
- Format currency values according to locale

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** TASK-003-02, TASK-003-03

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-003-02: Portfolio Structure Visualization

**Parent Feature:** FR-003 - Портфель активов

**Description:**
Реализация визуализации структуры портфеля с помощью диаграмм.

**Acceptance Criteria:**
- [ ] Pie/donut chart showing asset allocation
- [ ] Chart segments colored by asset class
- [ ] Interactive legend with tap to highlight
- [ ] Tap on segment shows details tooltip
- [ ] Breakdown by asset class, currency, or sector
- [ ] Toggle between different views
- [ ] Percentage and value labels
- [ ] Handles single-asset portfolio
- [ ] Unit tests for chart calculations

**Technical Notes:**
- Use react-native-svg-charts or victory-native
- Implement smooth animations for chart transitions
- Consider accessibility (describe chart content for screen readers)

**Size:** M (2-3 days)

**Dependencies:** TASK-003-01 (Portfolio Overview Screen)

**Blocked By:** TASK-003-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-003-03: Portfolio History Screen

**Parent Feature:** FR-003 - Портфель активов

**Description:**
Реализация экрана истории операций и изменений портфеля.

**Acceptance Criteria:**
- [ ] Transaction history list implemented
- [ ] Filter by date range
- [ ] Filter by transaction type (buy, sell, dividend, etc.)
- [ ] Transaction details: type, asset, amount, date, status
- [ ] Grouping by date (today, this week, this month, older)
- [ ] Empty state when no history
- [ ] Pagination for long history
- [ ] Search/filter functionality
- [ ] Portfolio history API integration
- [ ] E2E tests for history screen

**Technical Notes:**
- Use FlatList with pagination
- Implement date picker for range filter
- Consider using SectionList for grouped view

**Size:** M (2-3 days)

**Dependencies:** TASK-003-01 (Portfolio Overview Screen)

**Blocked By:** TASK-003-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

### FR-004: Чат с персональным менеджером

---

#### TASK-004-01: Chat UI Implementation

**Parent Feature:** FR-004 - Чат с персональным менеджером

**Description:**
Реализация пользовательского интерфейса чата без интеграции с бэкендом.

**Acceptance Criteria:**
- [ ] Chat screen UI implemented according to design
- [ ] Message list with user and manager message bubbles
- [ ] Message input field with send button
- [ ] Timestamp on each message
- [ ] Message status indicators (sent, delivered, read)
- [ ] Auto-scroll to latest message
- [ ] Keyboard handling for input field
- [ ] Avatar placeholder for manager
- [ ] Manager info header with name and status
- [ ] Empty state for new conversation
- [ ] Unit tests for UI components

**Technical Notes:**
- Use react-native-gifted-chat or build custom
- Implement keyboard avoiding view
- Use FlatList with inverted for message list
- Consider message bubble animations

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** TASK-004-02

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-004-02: Chat API Integration

**Parent Feature:** FR-004 - Чат с персональным менеджером

**Description:**
Интеграция чата с REST API для отправки и получения сообщений.

**Acceptance Criteria:**
- [ ] Chat history API integration
- [ ] Send message API integration
- [ ] Message pagination (load older messages)
- [ ] Optimistic UI updates on send
- [ ] Error handling for failed sends
- [ ] Retry mechanism for failed messages
- [ ] Message delivery confirmation
- [ ] Unread count badge
- [ ] Last message preview in chat list
- [ ] Integration tests for chat API

**Technical Notes:**
- Use optimistic updates pattern
- Implement message queue for failed messages
- Store messages locally for persistence
- Consider using react-query mutations

**Size:** M (2-3 days)

**Dependencies:** TASK-004-01 (Chat UI Implementation)

**Blocked By:** TASK-004-01

**Blocks:** TASK-004-03, TASK-004-04

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-004-03: Real-time Messaging (WebSocket/Polling)

**Parent Feature:** FR-004 - Чат с персональным менеджером

**Description:**
Реализация real-time получения сообщений через WebSocket или long polling.

**Acceptance Criteria:**
- [ ] WebSocket connection established on chat open
- [ ] Connection status indicator
- [ ] Automatic reconnection on disconnect
- [ ] New message received in real-time
- [ ] Connection closed on chat screen unmount
- [ ] Fallback to polling if WebSocket unavailable
- [ ] Heartbeat/ping-pong to keep connection alive
- [ ] Handle app background/foreground states
- [ ] Connection error handling
- [ ] Unit tests for connection logic

**Technical Notes:**
- Use socket.io-client or native WebSocket
- Implement exponential backoff for reconnection
- Use AppState for background handling
- Consider battery optimization

**Size:** M (2-3 days)

**Dependencies:** TASK-004-02 (Chat API Integration)

**Blocked By:** TASK-004-02

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-004-04: Chat Offline Queue

**Parent Feature:** FR-004 - Чат с персональным менеджером

**Description:**
Реализация офлайн-очереди сообщений для отправки при восстановлении соединения.

**Acceptance Criteria:**
- [ ] Messages queued when offline
- [ ] Queued messages persisted locally
- [ ] Visual indicator for pending messages
- [ ] Automatic send when connection restored
- [ ] Duplicate message prevention
- [ ] Message order preserved
- [ ] Queue cleared after successful send
- [ ] Manual retry option for failed messages
- [ ] Queue limit (max 100 messages)
- [ ] Unit tests for queue logic

**Technical Notes:**
- Use AsyncStorage or SQLite for queue persistence
- Implement queue processor with retry logic
- Add NetInfo listener for connectivity changes
- Consider background task for sending

**Size:** S (1-2 days)

**Dependencies:** TASK-004-02 (Chat API Integration)

**Blocked By:** TASK-004-02

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

## PHASE 2: ENHANCEMENT (SHOULD HAVE)

---

### FR-005: Push-уведомления

---

#### TASK-005-01: Push Notifications Setup

**Parent Feature:** FR-005 - Push-уведомления

**Description:**
Настройка инфраструктуры push-уведомлений для iOS и Android.

**Acceptance Criteria:**
- [ ] Firebase Cloud Messaging configured for Android
- [ ] APNs configured for iOS
- [ ] Device token registration on app launch
- [ ] Token sent to backend API
- [ ] Permission request for notifications
- [ ] Handle permission denied gracefully
- [ ] Handle token refresh
- [ ] Token unregistration on logout
- [ ] Integration tests for push setup

**Technical Notes:**
- Use @react-native-firebase/messaging
- Configure push notification certificates for iOS
- Set up Firebase project for Android
- Handle both foreground and background messages

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** TASK-005-02

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-005-02: Push Notification Handling and Navigation

**Parent Feature:** FR-005 - Push-уведомления

**Description:**
Реализация обработки push-уведомлений и навигации к соответствующим экранам.

**Acceptance Criteria:**
- [ ] Notification received in foreground (in-app banner)
- [ ] Notification received in background (system notification)
- [ ] Notification received when app killed
- [ ] Tap on notification navigates to correct screen
- [ ] Deep link parsing from notification data
- [ ] Badge count management
- [ ] Notification type routing (chat, portfolio, products)
- [ ] Local notification support
- [ ] Notification logging for analytics
- [ ] E2E tests for notification flow

**Technical Notes:**
- Use react-navigation deep linking
- Implement notification handler service
- Consider using Notifee for local notifications
- Test on both iOS and Android

**Size:** M (2-3 days)

**Dependencies:** TASK-005-01 (Push Notifications Setup)

**Blocked By:** TASK-005-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

### FR-006: Биометрическая аутентификация

---

#### TASK-006-01: Biometric Authentication Implementation

**Parent Feature:** FR-006 - Биометрическая аутентификация

**Description:**
Реализация входа в приложение с использованием биометрии (Touch ID, Face ID, Fingerprint).

**Acceptance Criteria:**
- [ ] Biometric availability check on device
- [ ] Biometric prompt after first login (opt-in)
- [ ] Biometric authentication flow
- [ ] Fallback to password on biometric error
- [ ] Settings toggle for enabling/disabling biometrics
- [ ] Handle biometric changes on device
- [ ] Cross-platform support (iOS + Android)
- [ ] Secure storage of biometric preference
- [ ] Error handling for locked biometrics
- [ ] E2E tests for biometric flow

**Technical Notes:**
- Use react-native-biometrics or expo-local-authentication
- Store biometric enabled flag in secure storage
- Handle different biometric types per platform
- Never store actual biometric data

**Size:** S (1-2 days)

**Dependencies:** TASK-001-02 (Login Screen), TASK-007-01 (Profile Screen)

**Blocked By:** TASK-001-02, TASK-007-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

### FR-007: Профиль пользователя

---

#### TASK-007-01: Profile View Screen

**Parent Feature:** FR-007 - Профиль пользователя

**Description:**
Реализация экрана просмотра профиля пользователя.

**Acceptance Criteria:**
- [ ] Profile screen UI implemented according to design
- [ ] Display: name, email, phone, profile photo
- [ ] Display assigned manager info
- [ ] Edit profile button
- [ ] Settings section (notifications, biometrics, security)
- [ ] Logout button
- [ ] Profile API integration
- [ ] Loading and error states
- [ ] E2E tests for profile screen

**Technical Notes:**
- Use placeholder for missing profile photo
- Consider using cached image component
- Add accessibility labels

**Size:** S (1-2 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** TASK-007-02

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-007-02: Profile Edit Functionality

**Parent Feature:** FR-007 - Профиль пользователя

**Description:**
Реализация редактирования профиля и контактных данных.

**Acceptance Criteria:**
- [ ] Edit profile screen with form fields
- [ ] Editable fields: name, email, phone
- [ ] Email change with verification flow
- [ ] Phone change with verification flow
- [ ] Form validation for all fields
- [ ] Save changes API integration
- [ ] Success/error feedback
- [ ] Optimistic UI updates
- [ ] Profile update API integration
- [ ] E2E tests for edit flow

**Technical Notes:**
- Use react-hook-form for validation
- Implement OTP verification for email/phone
- Consider debounce for validation

**Size:** M (2-3 days)

**Dependencies:** TASK-007-01 (Profile View Screen)

**Blocked By:** TASK-007-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

## PHASE 3: VALUE-ADD (COULD HAVE)

---

### FR-008: Документы и отчеты

---

#### TASK-008-01: Documents List Screen

**Parent Feature:** FR-008 - Документы и отчеты

**Description:**
Реализация экрана списка документов с фильтрацией.

**Acceptance Criteria:**
- [ ] Documents list screen UI implemented
- [ ] Document cards with: name, type, date, size
- [ ] Filter by document type
- [ ] Filter by date range
- [ ] Sort by date (newest first)
- [ ] New document indicator/badge
- [ ] Empty state when no documents
- [ ] Pull-to-refresh
- [ ] Pagination for long lists
- [ ] Documents API integration
- [ ] E2E tests for documents list

**Technical Notes:**
- Use FlatList with pagination
- Implement document type icons
- Consider document preview thumbnail

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure)

**Blocked By:** TASK-001-01

**Blocks:** TASK-008-02

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-008-02: PDF Viewer and Download

**Parent Feature:** FR-008 - Документы и отчеты

**Description:**
Реализация просмотра и скачивания PDF документов.

**Acceptance Criteria:**
- [ ] PDF viewer integration
- [ ] Document download to device
- [ ] Download progress indicator
- [ ] Share document functionality
- [ ] Open in external app option
- [ ] Handle large files (>10MB)
- [ ] Offline access to downloaded documents
- [ ] Storage management (clear cache)
- [ ] Error handling for corrupted files
- [ ] E2E tests for document viewing

**Technical Notes:**
- Use react-native-pdf for viewing
- Use RNFS for file system access
- Implement caching for downloaded files
- Handle iOS/Android file paths differences

**Size:** M (2-3 days)

**Dependencies:** TASK-008-01 (Documents List Screen)

**Blocked By:** TASK-008-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

### FR-009: Графики и аналитика

---

#### TASK-009-01: Portfolio Charts Implementation

**Parent Feature:** FR-009 - Графики и аналитика

**Description:**
Реализация графиков динамики портфеля и доходности.

**Acceptance Criteria:**
- [ ] Line chart for portfolio value over time
- [ ] Period selector (1W, 1M, 3M, 1Y, All)
- [ ] Interactive tooltip on tap/hover
- [ ] Zoom and pan functionality
- [ ] Return percentage calculation
- [ ] Handle missing data points gracefully
- [ ] Animate chart on period change
- [ ] Dark/light theme support
- [ ] Accessibility description
- [ ] Unit tests for chart calculations

**Technical Notes:**
- Use react-native-svg-charts or victory-native
- Consider react-native-chart-kit for simpler charts
- Implement gesture handlers for interactivity
- Optimize for large datasets

**Size:** M (2-3 days)

**Dependencies:** TASK-003-01 (Portfolio Overview Screen)

**Blocked By:** TASK-003-01

**Blocks:** TASK-009-02

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-009-02: Benchmark Comparison

**Parent Feature:** FR-009 - Графики и аналитика

**Description:**
Реализация сравнения портфеля с бенчмарками и индексами.

**Acceptance Criteria:**
- [ ] Benchmark selection UI
- [ ] Multiple benchmark comparison
- [ ] Overlay chart with portfolio and benchmarks
- [ ] Legend with toggle visibility
- [ ] Performance comparison table
- [ ] Relative performance calculations
- [ ] Benchmark API integration
- [ ] Cache benchmark data
- [ ] E2E tests for comparison view

**Technical Notes:**
- Normalize data for comparison (starting point = 100%)
- Consider using D3.js for complex visualizations
- Implement efficient re-renders

**Size:** M (2-3 days)

**Dependencies:** TASK-009-01 (Portfolio Charts Implementation)

**Blocked By:** TASK-009-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

### FR-010: Образовательный контент

---

#### TASK-010-01: Articles and FAQ

**Parent Feature:** FR-010: Образовательный контент

**Description:**
Реализация раздела со статьями и FAQ.

**Acceptance Criteria:**
- [ ] Articles list with categories
- [ ] Article detail page with formatting
- [ ] Search functionality
- [ ] FAQ with expandable answers
- [ ] Category filtering
- [ ] Bookmarks/favorites
- [ ] Share article
- [ ] Loading and error states
- [ ] Articles API integration
- [ ] E2E tests for articles flow

**Technical Notes:**
- Use WebView or markdown renderer for article content
- Implement full-text search
- Consider offline caching

**Size:** M (2-3 days)

**Dependencies:** TASK-001-01 (Auth Infrastructure) - optional

**Blocked By:** None (can be public content)

**Blocks:** TASK-010-02

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-010-02: Glossary Implementation

**Parent Feature:** FR-010: Образовательный контент

**Description:**
Реализация глоссария инвестиционных терминов.

**Acceptance Criteria:**
- [ ] Glossary list with alphabetical navigation
- [ ] Search by term name
- [ ] Term detail with definition
- [ ] Related terms links
- [ ] Alphabet quick jump
- [ ] Recent searches
- [ ] Offline access to glossary
- [ ] Glossary API integration
- [ ] Unit tests for glossary logic

**Technical Notes:**
- Use SectionList for alphabetical grouping
- Implement local caching for offline
- Consider highlighting terms in articles

**Size:** S (1-2 days)

**Dependencies:** TASK-010-01 (Articles and FAQ)

**Blocked By:** TASK-010-01

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

## CROSS-CUTTING TASKS

---

#### TASK-APP-01: Navigation Structure Setup

**Parent Feature:** Infrastructure

**Description:**
Настройка навигационной структуры приложения с React Navigation.

**Acceptance Criteria:**
- [ ] React Navigation configured
- [ ] Stack navigator for auth flows
- [ ] Tab navigator for main app
- [ ] Drawer navigator (if needed)
- [ ] Deep linking setup
- [ ] Navigation state persistence
- [ ] Transition animations
- [ ] Navigation types (TypeScript)
- [ ] Unit tests for navigation

**Technical Notes:**
- Use @react-navigation/native
- Implement typed navigation
- Configure screen options for headers

**Size:** M (2-3 days)

**Dependencies:** None

**Blocked By:** None

**Blocks:** All UI tasks

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-APP-02: Design System Components

**Parent Feature:** Infrastructure

**Description:**
Создание базовых UI компонентов дизайн-системы.

**Acceptance Criteria:**
- [ ] Button component (primary, secondary, outline, ghost)
- [ ] Input component with validation states
- [ ] Card component
- [ ] Typography components
- [ ] Loading indicator
- [ ] Error message component
- [ ] Badge component
- [ ] Avatar component
- [ ] Divider component
- [ ] Storybook setup for components

**Technical Notes:**
- Use shadcn/ui patterns
- Implement with Tailwind (twrnc or nativewind)
- Ensure accessibility compliance
- Document all props

**Size:** L (3-5 days)

**Dependencies:** None

**Blocked By:** None

**Blocks:** All UI tasks

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

#### TASK-APP-03: Error Handling and Logging

**Parent Feature:** Infrastructure

**Description:**
Реализация глобальной обработки ошибок и логирования.

**Acceptance Criteria:**
- [ ] Global error boundary
- [ ] Network error handler
- [ ] Crash logging integration (Sentry/Crashlytics)
- [ ] Error reporting to backend
- [ ] User-friendly error messages
- [ ] Retry mechanisms
- [ ] Offline mode detection
- [ ] Analytics events logging
- [ ] Unit tests for error handling

**Technical Notes:**
- Use Sentry or Firebase Crashlytics
- Implement error reporting service
- Consider using react-native-exception-handler

**Size:** M (2-3 days)

**Dependencies:** None

**Blocked By:** None

**Blocks:** None

**INVEST Score:** ✅ Independent, ✅ Negotiable, ✅ Valuable, ✅ Estimable, ✅ Small, ✅ Testable

---

## Task Summary by Feature

| Feature | Tasks | Total Size | Est. Days |
|---------|-------|------------|-----------|
| FR-001: Аутентификация | 5 | M+M+M+M+S = 11-15 days | ~13 |
| FR-002: Витрина продуктов | 3 | M+M+S = 5-8 days | ~6 |
| FR-003: Портфель активов | 3 | M+M+M = 6-9 days | ~7 |
| FR-004: Чат с менеджером | 4 | M+M+M+S = 8-12 days | ~10 |
| FR-005: Push-уведомления | 2 | M+M = 4-6 days | ~5 |
| FR-006: Биометрия | 1 | S = 1-2 days | ~1.5 |
| FR-007: Профиль | 2 | S+M = 3-5 days | ~4 |
| FR-008: Документы | 2 | M+M = 4-6 days | ~5 |
| FR-009: Графики | 2 | M+M = 4-6 days | ~5 |
| FR-010: Контент | 2 | M+S = 3-5 days | ~4 |
| Infrastructure | 3 | M+L+M = 7-11 days | ~9 |
| **TOTAL** | **29 tasks** | | **~70 days** |

---

## Critical Path Analysis

```
TASK-APP-02 (Design System)
       │
       ▼
TASK-APP-01 (Navigation) ──► TASK-001-01 (Auth Infrastructure)
                                      │
                    ┌─────────────────┼─────────────────┐
                    ▼                 ▼                 ▼
            TASK-001-02         TASK-002-01       TASK-003-01
            (Login)             (Products)        (Portfolio)
                    │                 │                 │
                    ▼                 ▼                 ▼
            TASK-001-03         TASK-002-02       TASK-003-02
            (Registration)      (Product Detail)  (Structure)
                    │                 │                 │
                    ▼                 ▼                 ▼
            TASK-001-04         TASK-002-03       TASK-003-03
            (Recovery)          (Offline)         (History)
                    │                                   │
                    ▼                                   ▼
            TASK-001-05                         TASK-009-01
            (Timeout)                           (Charts)
```

---

## Task Execution Order Recommendations

### Sprint 1: Foundation Infrastructure (Week 1-2)
1. TASK-APP-02: Design System Components
2. TASK-APP-01: Navigation Structure Setup
3. TASK-APP-03: Error Handling and Logging
4. TASK-001-01: Auth Infrastructure Setup

### Sprint 2: Core Authentication (Week 2-3)
5. TASK-001-02: Login Screen and Flow
6. TASK-001-03: Registration Screen and Flow
7. TASK-001-04: Password Recovery Flow

### Sprint 3: Products and Portfolio (Week 3-4)
8. TASK-002-01: Products List Screen
9. TASK-002-02: Product Detail Screen
10. TASK-003-01: Portfolio Overview Screen

### Sprint 4: Chat System (Week 4-5)
11. TASK-004-01: Chat UI Implementation
12. TASK-004-02: Chat API Integration
13. TASK-004-03: Real-time Messaging

### Sprint 5: MVP Completion (Week 5-6)
14. TASK-001-05: Session Timeout Management
15. TASK-002-03: Products Offline Support
16. TASK-003-02: Portfolio Structure Visualization
17. TASK-004-04: Chat Offline Queue

### Sprint 6: Enhancement Features (Week 6-7)
18. TASK-005-01: Push Notifications Setup
19. TASK-005-02: Push Notification Handling
20. TASK-007-01: Profile View Screen
21. TASK-007-02: Profile Edit Functionality

### Sprint 7: Value-Add Features (Week 7-8)
22. TASK-006-01: Biometric Authentication
23. TASK-008-01: Documents List Screen
24. TASK-008-02: PDF Viewer and Download

### Sprint 8: Analytics and Content (Week 8-9)
25. TASK-003-03: Portfolio History Screen
26. TASK-009-01: Portfolio Charts Implementation
27. TASK-009-02: Benchmark Comparison

### Sprint 9: Final Features (Week 9-10)
28. TASK-010-01: Articles and FAQ
29. TASK-010-02: Glossary Implementation

---

## Risk Mitigation Notes

### High-Risk Tasks
1. **TASK-004-03 (Real-time Messaging)** - WebSocket reliability, battery drain
   - Mitigation: Implement fallback to polling, thorough testing

2. **TASK-001-01 (Auth Infrastructure)** - Security critical
   - Mitigation: Security audit, penetration testing

3. **TASK-005-01 (Push Notifications Setup)** - Platform-specific complexity
   - Mitigation: Early setup, test on multiple devices

### Tasks Requiring External Dependencies
- TASK-001-xx: Backend Auth API
- TASK-002-xx: Products API
- TASK-003-xx: Portfolio API
- TASK-004-xx: Chat API and WebSocket server
- TASK-005-xx: FCM/APNs configuration

---

## Definition of Done for Tasks

- [ ] Code written and follows coding standards
- [ ] Unit tests written (min 80% coverage)
- [ ] Integration tests for critical paths
- [ ] Code review completed
- [ ] UI matches design specifications
- [ ] Accessibility requirements met
- [ ] Performance requirements met (< 500ms response)
- [ ] Error handling implemented
- [ ] Documentation updated
- [ ] QA testing completed

---

*Document created by Business Analyst Agent*
*Source: docs/requirements/feature-extracted-features.md*
