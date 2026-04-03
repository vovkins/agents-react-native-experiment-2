# Feature Extraction Analysis

**Project:** Мобильное приложение для управляющей компании  
**Analysis Date:** 2026-04-03  
**Source Document:** docs/requirements/prd.md (Product Backlog)

---

## Executive Summary

This document provides a comprehensive extraction of all features and functional requirements from the Product Requirements Document. The application is a mobile app for an asset management company (управляющая компания) that enables clients to manage their investment portfolios, view products, and communicate with personal managers.

---

## Complete Feature List

### 1. Feature: Настройка проекта и инфраструктура (Project Setup & Infrastructure)

**Priority:** MUST HAVE  
**Story Points:** 5 SP  
**Estimate:** 24 hours  
**Epic:** Infrastructure & Setup

**Description:**
Initial setup of React Native project, build configuration, and CI/CD pipeline.

**Functional Requirements:**
- React Native project initialization
- iOS and Android build configuration
- CI/CD pipeline setup for automated builds and deployments
- Development environment configuration
- Code quality tools (ESLint, Prettier, TypeScript)
- Testing framework setup (Jest, Detox)

**Technical Constraints:**
- Must support iOS 12+ and Android 6.0+
- Must use React Native 0.70+
- Must support both development and production environments

**Dependencies:**
- None (foundational feature)
- Blocks all other features

**Edge Cases & Error Scenarios:**
- Build failures on different environments
- CI/CD pipeline timeouts
- Certificate/signing issues for iOS builds
- Environment variable misconfiguration

**Integration Points:**
- Version control system (GitHub)
- CI/CD service (GitHub Actions or similar)
- App Store Connect / Google Play Console

---

### 2. Feature: UI Kit и дизайн-система (UI Kit & Design System)

**Priority:** MUST HAVE  
**Story Points:** 8 SP  
**Estimate:** 40 hours  
**Epic:** Infrastructure & Setup

**Description:**
Create base UI components and setup design system for consistent look and feel.

**Functional Requirements:**
- Typography system (headings, body text, labels)
- Color palette (primary, secondary, semantic colors)
- Button components (primary, secondary, ghost, disabled states)
- Input components (text fields, selectors, checkboxes)
- Card components
- Navigation components (headers, tabs, drawers)
- Loading states and skeletons
- Error states
- Empty states
- Modal and dialog components
- Icon system

**Technical Constraints:**
- Must follow accessibility guidelines (WCAG 2.1 AA)
- Must support dark mode (optional for MVP)
- Must support responsive layouts for different screen sizes
- Must use theme system for easy customization

**Dependencies:**
- Depends on: #44 (Project Setup)

**Edge Cases & Error Scenarios:**
- Long text overflow in components
- Missing images or icons
- Accessibility issues with screen readers
- RTL (right-to-left) language support (future consideration)

**Integration Points:**
- Design tokens from Figma/design tools
- Storybook for component documentation

---

### 3. Feature: Аутентификация и безопасность (Authentication & Security)

**Priority:** MUST HAVE  
**Story Points:** 8 SP  
**Estimate:** 40 hours  
**Epic:** Authentication

**Description:**
Implement authentication system including login/password, biometrics, and secure token storage.

**Functional Requirements:**
- Login screen with email/phone and password
- Password validation and error handling
- Biometric authentication (Face ID, Touch ID, Fingerprint)
- Secure token storage using Keychain (iOS) and Keystore (Android)
- Session management (auto-logout after inactivity)
- Token refresh mechanism
- Logout functionality
- PIN code as fallback authentication
- Remember me functionality

**Technical Constraints:**
- Must use OAuth 2.0 or JWT authentication
- Tokens must be stored securely (no AsyncStorage/localStorage)
- Session timeout: 30 minutes of inactivity
- Password must meet security requirements (min 8 chars, complexity)

**Dependencies:**
- Depends on: #44 (Project Setup), #45 (UI Kit)

**Edge Cases & Error Scenarios:**
- Invalid credentials
- Account locked after multiple failed attempts
- Network timeout during login
- Biometric not available or not enrolled
- Token expired during session
- Refresh token expired (re-login required)
- App backgrounded during authentication
- Device date/time changed (affects token validity)
- Certificate pinning failures

**Integration Points:**
- Backend authentication API (REST or GraphQL)
- Biometric APIs (Face ID, Touch ID, Fingerprint)
- Push notification service (for auth notifications)

---

### 4. Feature: Витрина продуктов (Product Showcase)

**Priority:** MUST HAVE  
**Story Points:** 8 SP  
**Estimate:** 40 hours  
**Epic:** Products

**Description:**
View list of trust management strategies and Individual Trust Management (ИДУ) product.

**Functional Requirements:**
- Product catalog screen with list of strategies
- Product detail screen with full information
- Strategy comparison functionality
- Filter and search products
- Product performance metrics (ROI, risk level, duration)
- Historical performance charts
- Investment minimums
- Product documents and prospectus
- "Request callback" or "Contact manager" button

**Technical Constraints:**
- Must cache product data for offline viewing
- Product data refresh at least daily
- Charts must be interactive and responsive
- Images must be optimized for mobile

**Dependencies:**
- Depends on: #46 (Authentication)

**Edge Cases & Error Scenarios:**
- Empty product catalog
- Product data unavailable (API error)
- Slow network for images
- Outdated cached data
- Invalid product ID (deep link)
- Product removed or archived
- Currency conversion issues
- Chart rendering failures

**Integration Points:**
- Backend product catalog API
- Chart library (Victory Native, React Native Charts)
- Analytics tracking (product views, interactions)

---

### 5. Feature: Портфель активов (Portfolio of Assets)

**Priority:** MUST HAVE  
**Story Points:** 8 SP  
**Estimate:** 40 hours  
**Epic:** Portfolio

**Description:**
View current asset portfolio, portfolio structure, and profitability.

**Functional Requirements:**
- Portfolio overview screen with total value
- Asset allocation chart (pie chart)
- Individual asset details
- Portfolio performance over time (line chart)
- Profit/Loss indicators (absolute and percentage)
- Portfolio structure breakdown (by asset type, sector, currency)
- Transaction history
- Portfolio valuation history
- Currency breakdown (RUB, USD, EUR)
- Risk metrics display

**Technical Constraints:**
- Real-time or near real-time data updates (max 15 min delay)
- Must support offline viewing with last known data
- Calculations must be accurate to 2 decimal places
- Currency rates must be current

**Dependencies:**
- Depends on: #46 (Authentication)

**Edge Cases & Error Scenarios:**
- Zero portfolio value (new user)
- Negative portfolio value (losses exceed assets)
- Missing historical data
- Currency conversion API failures
- Large portfolios (performance issues)
- Data synchronization conflicts
- Stale data warning
- Market closed (no updates)

**Integration Points:**
- Backend portfolio API
- Market data provider API
- Currency exchange rate API
- Analytics tracking

---

### 6. Feature: Чат с менеджером (Chat with Manager)

**Priority:** MUST HAVE  
**Story Points:** 13 SP  
**Estimate:** 60 hours  
**Epic:** Chat

**Description:**
In-app chat for real-time communication with personal manager.

**Functional Requirements:**
- Chat interface with message history
- Real-time message delivery (WebSocket or similar)
- Message status indicators (sent, delivered, read)
- Timestamp display
- Typing indicator
- Push notifications for new messages
- Message search functionality
- Chat history pagination
- Offline message queueing
- Auto-reconnection on network restore
- Manager profile display (name, photo, role)
- Quick replies / templates

**Technical Constraints:**
- Message delivery latency < 3 seconds
- Must support offline mode (queue messages)
- Message history: minimum 1 year
- Images in chat optional for MVP
- Must use WebSocket or similar real-time protocol

**Dependencies:**
- Depends on: #46 (Authentication)

**Edge Cases & Error Scenarios:**
- Manager offline or unavailable
- Network disconnection during send
- Message delivery failure
- Large message history (performance)
- Image upload failures
- Invalid message format
- Message order inconsistency
- Duplicate messages
- Chat room deleted/archived
- Manager changed (reassignment)
- Profanity/spam filtering (optional)

**Integration Points:**
- Backend chat service (WebSocket server)
- Push notification service (FCM/APNs)
- File storage service (for attachments in Phase 2)
- Analytics tracking

---

### 7. Feature: Push-уведомления (Push Notifications)

**Priority:** SHOULD HAVE  
**Story Points:** 5 SP  
**Estimate:** 24 hours  
**Epic:** Notifications

**Description:**
Push notifications for important portfolio events and notification settings.

**Functional Requirements:**
- Push notification registration (permissions)
- Notification types:
  - Portfolio value changes (significant changes)
  - New messages from manager
  - Document uploads
  - Market alerts
  - System announcements
- Notification settings screen
- Deep linking to relevant app section
- Notification history (in-app)
- Do not disturb mode

**Technical Constraints:**
- Must use Firebase Cloud Messaging (FCM) for Android
- Must use Apple Push Notification service (APNs) for iOS
- Notifications must be received within 1 minute of trigger
- Must handle notifications in foreground, background, and killed states

**Dependencies:**
- Depends on: #46 (Authentication)

**Edge Cases & Error Scenarios:**
- User denied notification permission
- Token registration failure
- Notification delivery failure
- App in foreground (how to display)
- Notification tapped when app is killed
- Duplicate notifications
- Rich notification display issues
- Notification sound/vibration settings

**Integration Points:**
- Firebase Cloud Messaging
- Apple Push Notification service
- Backend notification service
- Deep linking system

---

### 8. Feature: Профиль пользователя (User Profile)

**Priority:** SHOULD HAVE  
**Story Points:** 3 SP  
**Estimate:** 16 hours  
**Epic:** Profile

**Description:**
View personal data, manager contact information, and app settings.

**Functional Requirements:**
- Profile screen with user information
- Manager contact card (name, phone, email, photo)
- Edit profile (limited fields: phone, email)
- App settings (notifications, language, theme)
- Logout button
- App version and legal information
- Contact support option

**Technical Constraints:**
- Profile data must be current
- Changes must sync with backend immediately
- Must support profile image (if available)

**Dependencies:**
- Depends on: #46 (Authentication)

**Edge Cases & Error Scenarios:**
- Missing manager information
- Profile update failure
- Invalid phone/email format
- Profile image loading failure
- Manager reassigned (data change)

**Integration Points:**
- Backend user profile API
- Backend manager assignment API
- Support ticket system (optional)

---

### 9. Feature: Документы и отчеты (Documents & Reports)

**Priority:** SHOULD HAVE  
**Story Points:** 5 SP  
**Estimate:** 24 hours  
**Epic:** Documents

**Description:**
View portfolio reports and contracts in PDF format.

**Functional Requirements:**
- Document list screen (categorized by type)
- Document detail view (PDF viewer)
- Download document to device
- Share document functionality
- Filter documents by type, date
- Document search
- Document categories:
  - Portfolio statements
  - Tax reports
  - Contracts and agreements
  - Confirmations
- Document preview thumbnail

**Technical Constraints:**
- Must support PDF viewing within app
- Document downloads must be encrypted
- Maximum file size: 50 MB
- Must support offline access to downloaded documents

**Dependencies:**
- Depends on: #46 (Authentication)

**Edge Cases & Error Scenarios:**
- No documents available
- Document loading failure
- PDF rendering error
- Download interrupted
- Storage full on device
- Corrupted PDF file
- Document expired/archived
- Share functionality failure

**Integration Points:**
- Backend document management API
- File storage service (S3, Azure Blob, etc.)
- PDF rendering library (react-native-pdf)
- Device file system

---

### 10. Feature: Расширенная аналитика портфеля (Advanced Portfolio Analytics)

**Priority:** COULD HAVE  
**Story Points:** 8 SP  
**Estimate:** 40 hours  
**Epic:** Analytics

**Description:**
Profitability charts, benchmark comparisons, forecasts, and recommendations.

**Functional Requirements:**
- Advanced performance charts (multiple timeframes)
- Benchmark comparison (index comparison)
- Risk analysis visualization
- Sector/asset allocation drill-down
- Profitability forecast (model-based)
- Personalized recommendations
- Export reports to PDF/Excel
- Interactive chart annotations
- Historical performance analysis

**Technical Constraints:**
- Planned for Phase 2 or Phase 3
- Charts must render smoothly on low-end devices
- Calculations must be performed server-side
- Forecast disclaimer must be displayed

**Dependencies:**
- Depends on: #48 (Portfolio)

**Edge Cases & Error Scenarios:**
- Insufficient historical data
- Forecast model unavailable
- Benchmark data missing
- Chart rendering performance issues
- Complex calculations timeout
- Currency mismatch in comparisons

**Integration Points:**
- Backend analytics API
- Chart library with advanced features
- Export service (PDF/Excel generation)

---

### 11. Feature: Расширенные функции чата (Extended Chat Functions)

**Priority:** COULD HAVE  
**Story Points:** 8 SP  
**Estimate:** 40 hours  
**Epic:** Chat Extensions

**Description:**
Send images, documents, and voice messages.

**Functional Requirements:**
- Image attachment support (gallery, camera)
- Document attachment support (PDF, DOC, XLS)
- Voice message recording and playback
- Image preview before sending
- Document preview
- Attachment size indicators
- Progress indicators for uploads
- Attachment download and save

**Technical Constraints:**
- Planned for Phase 2 or Phase 3
- Image compression: max 5 MB per image
- Voice message: max 5 minutes
- Document: max 50 MB
- Must support common file formats

**Dependencies:**
- Depends on: #49 (Chat with Manager)

**Edge Cases & Error Scenarios:**
- Camera permission denied
- Gallery permission denied
- Microphone permission denied
- File too large
- Unsupported file format
- Upload interrupted
- Download interrupted
- Storage full on device
- Corrupted file
- Voice recording failure

**Integration Points:**
- Device camera and gallery APIs
- Device microphone API
- File storage service
- Media processing service (compression, conversion)

---

## Technical Constraints Summary

### Platform Requirements
- **iOS:** Version 12.0+
- **Android:** Version 6.0+ (API 23+)
- **React Native:** Version 0.70+

### Performance Requirements
- App launch time: < 3 seconds
- Screen transition: < 300ms
- API response timeout: 30 seconds
- Real-time chat latency: < 3 seconds
- Push notification delivery: < 1 minute

### Security Requirements
- OAuth 2.0 or JWT authentication
- Secure token storage (Keychain/Keystore)
- HTTPS for all API calls
- Certificate pinning recommended
- Session timeout: 30 minutes

### Data Requirements
- Offline mode support for critical features
- Data caching for portfolio and products
- Test coverage: ≥ 70%

---

## Integration Points Summary

### External APIs
1. **Authentication API** - User login, token management
2. **Product Catalog API** - Investment products and strategies
3. **Portfolio API** - User portfolio data and transactions
4. **Chat Service API** - Real-time messaging (WebSocket)
5. **Document Management API** - PDF reports and contracts
6. **Push Notification Service** - FCM/APNs
7. **Market Data API** - Real-time market prices
8. **Currency Exchange API** - Currency conversion rates
9. **Analytics API** - Advanced portfolio analytics (Phase 2/3)

### Third-Party Services
- Firebase Cloud Messaging (Android push)
- Apple Push Notification service (iOS push)
- File Storage (S3/Azure Blob)
- Analytics platform (Firebase Analytics, Amplitude, etc.)

---

## Dependency Graph

```
#44 (Project Setup & Infrastructure) [MUST HAVE]
  └─> #45 (UI Kit & Design System) [MUST HAVE]
        └─> #46 (Authentication & Security) [MUST HAVE]
              ├─> #47 (Product Showcase) [MUST HAVE]
              ├─> #48 (Portfolio of Assets) [MUST HAVE]
              │     └─> #53 (Advanced Analytics) [COULD HAVE]
              ├─> #49 (Chat with Manager) [MUST HAVE]
              │     └─> #54 (Extended Chat Functions) [COULD HAVE]
              ├─> #50 (Push Notifications) [SHOULD HAVE]
              ├─> #51 (User Profile) [SHOULD HAVE]
              └─> #52 (Documents & Reports) [SHOULD HAVE]
```

---

## Feature Summary by Priority

### MUST HAVE (6 features, 50 SP, 244 hours)
1. Project Setup & Infrastructure
2. UI Kit & Design System
3. Authentication & Security
4. Product Showcase
5. Portfolio of Assets
6. Chat with Manager

### SHOULD HAVE (3 features, 13 SP, 64 hours)
7. Push Notifications
8. User Profile
9. Documents & Reports

### COULD HAVE (2 features, 16 SP, 80 hours)
10. Advanced Portfolio Analytics
11. Extended Chat Functions

---

## Critical Edge Cases & Error Scenarios Summary

### Network/Connectivity
- Offline mode handling
- Network timeout
- Slow network conditions
- Network disconnection during operations
- Reconnection handling

### Authentication
- Invalid credentials
- Account lockout
- Token expiration
- Biometric failures
- Session management

### Data Loading
- Empty states (no data)
- API failures
- Data synchronization issues
- Stale data
- Large data sets (performance)

### File Operations
- File upload failures
- File download failures
- File size limits
- Unsupported formats
- Storage full

### Permissions
- Camera access denied
- Gallery access denied
- Microphone access denied
- Push notification permission denied
- Biometric not available

---

## Recommendations for Task Decomposition

### High-Priority Decomposition (MUST HAVE)
1. **Project Setup** - Can be split into iOS setup, Android setup, CI/CD setup
2. **UI Kit** - Can be split by component types (forms, navigation, data display)
3. **Authentication** - Can be split into login flow, biometrics, session management
4. **Product Showcase** - Can be split into catalog list, product details, filtering
5. **Portfolio** - Can be split into overview, charts, transaction history
6. **Chat** - Can be split into UI, WebSocket integration, message handling

### Medium-Priority Decomposition (SHOULD HAVE)
7. **Push Notifications** - Can be split into registration, notification handling, settings
8. **User Profile** - Can be split into profile view, manager info, settings
9. **Documents** - Can be split into document list, viewer, download/share

### Low-Priority Decomposition (COULD HAVE)
10. **Advanced Analytics** - Can be split into charts, benchmarks, forecasts
11. **Extended Chat** - Can be split into images, documents, voice messages

---

## Open Questions

1. **Authentication Method:** OAuth 2.0 or JWT? Specific provider?
2. **Backend APIs:** Are all backend APIs available? What's the API contract?
3. **Chat Protocol:** WebSocket, Socket.io, or custom implementation?
4. **Market Data Provider:** Which provider for real-time market data?
5. **File Storage:** Which cloud storage service (S3, Azure, GCP)?
6. **Analytics Platform:** Which analytics platform for user tracking?
7. **Designer Collaboration:** Who provides design assets and design tokens?
8. **Test Environment:** Is there a staging/test environment available?
9. **Biometric Fallback:** PIN code requirements and implementation?
10. **Offline Strategy:** Which features must work offline?

---

**Document Created:** 2026-04-03  
**Created By:** Business Analyst Agent  
**Status:** Complete