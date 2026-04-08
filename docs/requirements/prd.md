# Product Backlog

**Проект**: Asset Management Client App  
**Дата создания**: 2026-04-08  
**Версия**: 1.0

---

## Приоритеты

| Приоритет | Обозначение | Описание | Milestone |
|-----------|-------------|----------|-----------|
| **P0** | Must Have | Критически важно для MVP | MVP Release |
| **P1** | Should Have | Важно для первой версии | v1.0 Release |
| **P2** | Could Have | Желательно в будущих версиях | v1.1 Release |
| **P3** | Won't Have | Не планируется в текущей версии | Backlog |

---

## GitHub Issues Summary

Все эпики и user stories созданы как GitHub Issues:

### Epic Issues (P0 - Must Have) - MVP Release:
- **Epic 1**: Project Setup & Infrastructure - [#65](https://github.com/vovkins/agents-react-native-experiment-2/issues/65)
- **Epic 2**: Domain Layer Architecture - [#70](https://github.com/vovkins/agents-react-native-experiment-2/issues/70)
- **Epic 3**: Adapters Layer - API Integration - [#71](https://github.com/vovkins/agents-react-native-experiment-2/issues/71)
- **Epic 4**: Authentication & Authorization - [#72](https://github.com/vovkins/agents-react-native-experiment-2/issues/72)
- **Epic 5**: Products Showcase - [#73](https://github.com/vovkins/agents-react-native-experiment-2/issues/73)
- **Epic 6**: Client Portfolio - [#74](https://github.com/vovkins/agents-react-native-experiment-2/issues/74)
- **Epic 7**: Chat with Manager - [#75](https://github.com/vovkins/agents-react-native-experiment-2/issues/75)
- **Epic 14**: Testing & Quality Assurance - [#81](https://github.com/vovkins/agents-react-native-experiment-2/issues/81)
- **Epic 15**: App Store Deployment - [#82](https://github.com/vovkins/agents-react-native-experiment-2/issues/82)

### Epic Issues (P1 - Should Have) - v1.0 Release:
- **Epic 8**: User Profile & Settings - [#76](https://github.com/vovkins/agents-react-native-experiment-2/issues/76)
- **Epic 9**: Product Application - [#77](https://github.com/vovkins/agents-react-native-experiment-2/issues/77)
- **Epic 10**: Push Notifications System - [#84](https://github.com/vovkins/agents-react-native-experiment-2/issues/84)
- **Epic 16**: Analytics & Monitoring - [#83](https://github.com/vovkins/agents-react-native-experiment-2/issues/83)

### Epic Issues (P2 - Could Have) - v1.1 Release:
- **Epic 11**: Analytics & Reports - [#78](https://github.com/vovkins/agents-react-native-experiment-2/issues/78)
- **Epic 12**: News & Market Analytics - [#79](https://github.com/vovkins/agents-react-native-experiment-2/issues/79)
- **Epic 13**: Localization - [#80](https://github.com/vovkins/agents-react-native-experiment-2/issues/80)

---

## Структура Backlog

Backlog организован по приоритетам (P0-P3) и содержит:
- **Epics**: Крупные функциональные блоки
- **User Stories**: Конкретные требования с точки зрения пользователя
- **Tasks**: Технические задачи для реализации stories

---

## EPIC 1: Project Setup & Infrastructure (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#65](https://github.com/vovkins/agents-react-native-experiment-2/issues/65)  
**Total Story Points**: 14 SP

### US-001: Инициализация React Native проекта
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 1  
**GitHub Issue**: [#65](https://github.com/vovkins/agents-react-native-experiment-2/issues/65)

**Описание**: Создать базовую структуру React Native проекта с TypeScript

**Задачи**:
- [ ] Инициализировать React Native проект с TypeScript шаблоном
- [ ] Настроить ESLint и Prettier
- [ ] Настроить Jest для unit тестирования
- [ ] Добавить базовую структуру папок (src/view, src/domain, src/adapters)
- [ ] Настроить Git hooks (husky, lint-staged)

**Критерии приемки**:
- ✅ Проект запускается на iOS и Android
- ✅ Линтер работает без ошибок
- ✅ Тесты запускаются успешно
- ✅ Структура папок соответствует трехслойной архитектуре

---

### US-002: Настройка навигации
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 1  
**GitHub Issue**: [#66](https://github.com/vovkins/agents-react-native-experiment-2/issues/66)

**Описание**: Настроить React Navigation с базовой структурой экранов

**Задачи**:
- [ ] Установить React Navigation и зависимости
- [ ] Создать Bottom Tab Navigator для основных экранов
- [ ] Создать Stack Navigator для детальных экранов
- [ ] Настроить типизацию навигации с TypeScript
- [ ] Создать заглушки для основных экранов (Products, Portfolio, Chat, Profile)

**Критерии приемки**:
- ✅ Навигация работает между экранами
- ✅ Bottom Tab отображается корректно
- ✅ Навигация типизирована в TypeScript

---

### US-003: Настройка UI Kit и стилей
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 1-2  
**GitHub Issue**: [#67](https://github.com/vovkins/agents-react-native-experiment-2/issues/67)

**Описание**: Интегрировать shadcn/ui и настроить Tailwind CSS (NativeWind)

**Задачи**:
- [ ] Установить и настроить NativeWind (Tailwind CSS для React Native)
- [ ] Установить и настроить shadcn/ui компоненты
- [ ] Создать тему приложения (цвета, типографика, spacing)
- [ ] Создать базовые переиспользуемые компоненты (Button, Input, Card, etc.)
- [ ] Настроить темную/светлую тему

**Критерии приемки**:
- ✅ Tailwind классы работают в компонентах
- ✅ shadcn/ui компоненты интегрированы
- ✅ Тема применяется ко всему приложению
- ✅ Базовые компоненты созданы и работают

---

### US-004: Настройка State Management
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 1-2  
**GitHub Issue**: [#68](https://github.com/vovkins/agents-react-native-experiment-2/issues/68)

**Описание**: Настроить глобальное состояние приложения

**Задачи**:
- [ ] Выбрать и установить state manager (Zustand или Redux Toolkit)
- [ ] Создать структуру stores (auth, products, portfolio, chat)
- [ ] Настроить persist для offline данных
- [ ] Создать middleware для логирования (dev mode)

**Критерии приемки**:
- ✅ State manager интегрирован
- ✅ Stores созданы для каждой доменной области
- ✅ Persist работает корректно
- ✅ Dev tools работают

---

### US-050: Настройка CI/CD
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 1-2  
**GitHub Issue**: [#69](https://github.com/vovkins/agents-react-native-experiment-2/issues/69)

**Описание**: Настроить автоматическую сборку и деплой

**Задачи**:
- [ ] Настроить GitHub Actions или Bitrise
- [ ] Создать workflow для pull request checks (lint, test)
- [ ] Создать workflow для сборки iOS (TestFlight)
- [ ] Создать workflow для сборки Android (Internal Test)
- [ ] Настроить automatic version bumping

**Критерии приемки**:
- ✅ CI/CD работает автоматически
- ✅ Pull request checks работают
- ✅ Build загружается в TestFlight/Internal Test

---

## EPIC 2: Domain Layer Architecture (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#70](https://github.com/vovkins/agents-react-native-experiment-2/issues/70)  
**Total Story Points**: 13 SP

### US-005: Создание Domain Entities
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 2

**Описание**: Определить базовые сущности domain слоя

**Задачи**:
- [ ] Создать entity: User (профиль клиента)
- [ ] Создать entity: Product (инвестиционный продукт)
- [ ] Создать entity: Portfolio (портфель клиента)
- [ ] Создать entity: Asset (актив в портфеле)
- [ ] Создать entity: Message (сообщение в чате)
- [ ] Создать entity: Manager (персональный менеджер)
- [ ] Добавить валидацию для каждой entity

**Критерии приемки**:
- ✅ Все entities определены с TypeScript типами
- ✅ Валидация работает корректно
- ✅ Entities не зависят от внешних библиотек

---

### US-006: Создание Repository Interfaces
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 2

**Описание**: Определить контракты для работы с данными

**Задачи**:
- [ ] Создать IAuthRepository (login, logout, refresh)
- [ ] Создать IProductsRepository (getProducts, getProductById)
- [ ] Создать IPortfolioRepository (getPortfolio, getPortfolioHistory)
- [ ] Создать IChatRepository (getMessages, sendMessage, subscribe)
- [ ] Создать IUserRepository (getProfile, updateProfile)

**Критерии приемки**:
- ✅ Все interfaces определены
- ✅ Interfaces не содержат реализации
- ✅ Методы возвращают Promise с правильными типами

---

### US-007: Создание Use Cases
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 3-4

**Описание**: Реализовать бизнес-логику приложения

**Задачи**:
- [ ] Создать AuthUseCases (login, logout, refreshToken, checkSession)
- [ ] Создать ProductsUseCases (loadProducts, loadProductDetails, filterProducts)
- [ ] Создать PortfolioUseCases (loadPortfolio, loadHistory, calculateMetrics)
- [ ] Создать ChatUseCases (loadMessages, sendMessage, subscribeToMessages)
- [ ] Добавить unit тесты для Use Cases

**Критерии приемки**:
- ✅ Use Cases инкапсулируют бизнес-логику
- ✅ Use Cases не зависят от UI
- ✅ Unit тесты покрывают критические сценарии

---

## EPIC 3: Adapters Layer - API Integration (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#71](https://github.com/vovkins/agents-react-native-experiment-2/issues/71)  
**Total Story Points**: 13 SP

### US-008: Настройка API Client
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 3

**Описание**: Создать базовый HTTP клиент для работы с бэкендом

**Задачи**:
- [ ] Установить Axios или настроить fetch wrapper
- [ ] Создать ApiClient с interceptors (auth, logging, error handling)
- [ ] Настроить JWT token management (storage, refresh)
- [ ] Добавить certificate pinning для безопасности
- [ ] Создать error handling middleware

**Критерии приемки**:
- ✅ API client работает с базовыми HTTP методами
- ✅ Interceptors добавляют auth token автоматически
- ✅ Token refresh работает прозрачно
- ✅ Ошибки обрабатываются единообразно

---

### US-009: Реализация Repository Implementations
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 3-4

**Описание**: Реализовать репозитории для работы с бэкендом

**Задачи**:
- [ ] Реализовать AuthRepository (login, logout, refresh)
- [ ] Реализовать ProductsRepository (fetch products, fetch details)
- [ ] Реализовать PortfolioRepository (fetch portfolio, fetch history)
- [ ] Реализовать ChatRepository (fetch messages, send, websocket connection)
- [ ] Добавить маппинг DTO → Domain Entities

**Критерии приемки**:
- ✅ Репозитории реализуют interfaces из domain слоя
- ✅ Маппинг данных работает корректно
- ✅ Обработка ошибок работает

---

### US-010: Local Storage и Offline Support
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 4

**Описание**: Реализовать локальное хранение данных для offline режима

**Задачи**:
- [ ] Настроить AsyncStorage или SQLite для локального хранения
- [ ] Реализовать кэширование продуктов
- [ ] Реализовать кэширование портфеля
- [ ] Реализовать кэширование истории чата
- [ ] Добавить синхронизацию при восстановлении connection
- [ ] Создать queue для отправки сообщений offline

**Критерии приемки**:
- ✅ Данные кэшируются локально
- ✅ Приложение работает offline с кэшированными данными
- ✅ Синхронизация работает при восстановлении connection

---

## EPIC 4: Authentication & Authorization (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#72](https://github.com/vovkins/agents-react-native-experiment-2/issues/72)  
**Total Story Points**: 16 SP

### US-011: Экран входа (Login Screen)
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 3-4

**Описание**: Создать экран аутентификации с двумя способами входа

**Задачи**:
- [ ] Создать UI экрана входа (phone/email tabs)
- [ ] Реализовать форму входа по номеру телефона + SMS код
- [ ] Реализовать форму входа по email + пароль
- [ ] Добавить валидацию форм
- [ ] Реализовать отправку SMS кода
- [ ] Добавить обработку ошибок аутентификации
- [ ] Создать экран для ввода SMS кода (OTP)

**Критерии приемки**:
- ✅ Пользователь может выбрать способ входа (phone/email)
- ✅ Валидация работает для обоих способов
- ✅ SMS код отправляется и проверяется
- ✅ Ошибки отображаются пользователю

---

### US-012: Биометрическая аутентификация
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 4

**Описание**: Реализовать вход через Face ID / Touch ID

**Задачи**:
- [ ] Установить react-native-biometrics или аналог
- [ ] Реализовать проверку доступности биометрии на устройстве
- [ ] Реализовать сохранение credentials для биометрии
- [ ] Добавить prompt для биометрического входа
- [ ] Добавить fallback на пароль при ошибке биометрии

**Критерии приемки**:
- ✅ Face ID / Touch ID работает на поддерживаемых устройствах
- ✅ Fallback работает при недоступности биометрии
- ✅ Credentials безопасно хранятся в Keychain / Keystore

---

### US-013: Session Management
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 4

**Описание**: Управление сессией пользователя

**Задачи**:
- [ ] Реализовать автоматический logout после 30 мин неактивности
- [ ] Реализовать refresh token logic
- [ ] Добавить logout из всех устройств
- [ ] Реализовать защиту при Root/Jailbreak устройствах
- [ ] Добавить activity tracking для auto-logout

**Критерии приемки**:
- ✅ Автоматический logout работает после 30 мин
- ✅ Token refresh работает прозрачно
- ✅ Logout из всех устройств работает
- ✅ Приложение блокируется на Root/Jailbreak устройствах

---

### US-014: Безопасность аутентификации
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 4

**Описание**: Реализовать критические меры безопасности

**Задачи**:
- [ ] Добавить certificate pinning для API запросов
- [ ] Реализовать шифрование локальных данных (sensitive)
- [ ] Добавить detection of debuggers/inspectors
- [ ] Реализовать secure storage для токенов (Keychain/Keystore)
- [ ] Добавить rate limiting для попыток входа
- [ ] Реализовать логирование security events

**Критерии приемки**:
- ✅ Certificate pinning работает
- ✅ Чувствительные данные зашифрованы
- ✅ Токены хранятся в secure storage
- ✅ Rate limiting предотвращает brute force

---

## EPIC 5: Products Showcase (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#73](https://github.com/vovkins/agents-react-native-experiment-2/issues/73)  
**Total Story Points**: 18 SP

### US-015: Экран списка продуктов
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 5

**Описание**: Создать главный экран с витриной инвестиционных продуктов

**Задачи**:
- [ ] Создать UI для списка продуктов (FlatList)
- [ ] Создать карточку продукта (название, описание, доходность)
- [ ] Реализовать загрузку продуктов из API
- [ ] Добавить pull-to-refresh
- [ ] Добавить skeleton loading
- [ ] Реализовать обработку ошибок загрузки
- [ ] Добавить пустое состояние (empty state)

**Критерии приемки**:
- ✅ Список продуктов отображается корректно
- ✅ Карточки содержат ключевую информацию
- ✅ Pull-to-refresh работает
- ✅ Loading и error states отображаются

---

### US-016: Фильтрация продуктов
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 5

**Описание**: Реализовать фильтры для продуктов

**Задачи**:
- [ ] Создать UI для фильтров (категория, уровень риска)
- [ ] Реализовать filter logic в domain слое
- [ ] Добавить chips для активных фильтров
- [ ] Реализовать сброс фильтров
- [ ] Сохранять выбранные фильтры в local state

**Критерии приемки**:
- ✅ Фильтры работают корректно
- ✅ Можно выбрать несколько фильтров
- ✅ Сброс фильтров работает

---

### US-017: Детальный экран продукта
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 5-6

**Описание**: Создать экран с детальной информацией о продукте

**Задачи**:
- [ ] Создать UI для детального экрана продукта
- [ ] Отобразить полное описание стратегии
- [ ] Добавить график исторической доходности
- [ ] Показать ключевые метрики (доходность, риск, дюрация)
- [ ] Добавить информацию о минимальной сумме инвестирования
- [ ] Реализовать share functionality
- [ ] Добавить кнопку "Подать заявку" (для P1)

**Критерии приемки**:
- ✅ Детальная информация отображается корректно
- ✅ График доходности работает
- ✅ Все метрики видны пользователю
- ✅ Навигация на детальный экран работает

---

### US-018: Графики доходности
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 5-6

**Описание**: Реализовать интерактивные графики доходности

**Задачи**:
- [ ] Выбрать и установить библиотеку графиков (victory-native или react-native-chart-kit)
- [ ] Создать компонент LineChart для доходности
- [ ] Добавить интерактивность (tooltip при тапе)
- [ ] Реализовать переключение периодов (1м, 3м, 6м, 1г, все время)
- [ ] Добавить сравнение с бенчмарком
- [ ] Оптимизировать производительность графиков

**Критерии приемки**:
- ✅ Графики отображаются корректно
- ✅ Tooltip работает при тапе
- ✅ Переключение периодов работает
- ✅ Сравнение с бенчмарком работает

---

## EPIC 6: Client Portfolio (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#74](https://github.com/vovkins/agents-react-native-experiment-2/issues/74)  
**Total Story Points**: 18 SP

### US-019: Экран портфеля
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 5-6

**Описание**: Создать главный экран с портфелем клиента

**Задачи**:
- [ ] Создать UI для экрана портфеля
- [ ] Отобразить общую стоимость портфеля
- [ ] Показать общую доходность (абсолютная, %)
- [ ] Добавить круговую диаграмму структуры портфеля
- [ ] Реализовать загрузку данных портфеля
- [ ] Добавить pull-to-refresh
- [ ] Добавить skeleton loading

**Критерии приемки**:
- ✅ Общая стоимость портфеля отображается
- ✅ Доходность рассчитана корректно
- ✅ Круговая диаграмма показывает структуру
- ✅ Loading и refresh работают

---

### US-020: Детализация активов портфеля
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 6

**Описание**: Создать список активов с возможностью детализации

**Задачи**:
- [ ] Создать список активов портфеля (FlatList)
- [ ] Создать карточку актива (название, стоимость, доля, доходность)
- [ ] Реализовать детальный экран актива
- [ ] Показать график доходности актива
- [ ] Добавить историю операций по активу
- [ ] Реализовать сортировку активов (по стоимости, доходности)

**Критерии приемки**:
- ✅ Список активов отображается
- ✅ Детальный экран актива работает
- ✅ График доходности актива работает
- ✅ История операций отображается

---

### US-021: История портфеля и аналитика
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 6

**Описание**: Реализовать историю изменений портфеля

**Задачи**:
- [ ] Создать экран истории портфеля
- [ ] Реализовать график стоимости портфеля во времени
- [ ] Добавить выбор периода анализа (1м, 3м, 6м, 1г, все время)
- [ ] Показать ключевые метрики (max drawdown, sharpe ratio)
- [ ] Добавить сравнение с бенчмарками
- [ ] Показать дивиденды и купоны

**Критерии приемки**:
- ✅ График истории портфеля работает
- ✅ Метрики рассчитаны корректно
- ✅ Периключение периодов работает
- ✅ Сравнение с бенчмарками работает

---

### US-022: Структура портфеля
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 6

**Описание**: Визуализация структуры портфеля

**Задачи**:
- [ ] Создать интерактивную круговую диаграмму
- [ ] Реализовать breakdown по классам активов (акции, облигации, фонды)
- [ ] Добавить breakdown по валютам
- [ ] Реализовать breakdown по стратегиям
- [ ] Добавить легенду с процентами

**Критерии приемки**:
- ✅ Круговая диаграмма интерактивная
- ✅ Breakdown работает по всем измерениям
- ✅ Легенда отображается корректно

---

## EPIC 7: Chat with Manager (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#75](https://github.com/vovkins/agents-react-native-experiment-2/issues/75)  
**Total Story Points**: 24 SP

### US-023: Экран списка чатов
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 7

**Описание**: Создать экран со списком чатов (для будущего расширения)

**Задачи**:
- [ ] Создать UI для списка чатов
- [ ] Показать карточку чата с менеджером
- [ ] Отобразить последнее сообщение и время
- [ ] Показать счетчик непрочитанных сообщений
- [ ] Реализовать переход в чат

**Критерии приемки**:
- ✅ Список чатов отображается
- ✅ Последнее сообщение видно
- ✅ Badge непрочитанных сообщений работает
- ✅ Переход в чат работает

---

### US-024: Экран чата
**Приоритет**: P0  
**Story Points**: 8  
**Milestone**: Sprint 7-8

**Описание**: Создать полнофункциональный чат с менеджером

**Задачи**:
- [ ] Создать UI для экрана чата
- [ ] Отобразить информацию о менеджере (имя, фото, статус)
- [ ] Реализовать список сообщений (FlatList, inverted)
- [ ] Создать bubble сообщений (sent/received)
- [ ] Реализовать статус доставки (отправлено, доставлено, прочитано)
- [ ] Создать input для набора сообщения
- [ ] Реализовать отправку текстовых сообщений
- [ ] Добавить auto-scroll к последнему сообщению
- [ ] Реализовать загрузку истории при скролле вверх

**Критерии приемки**:
- ✅ Сообщения отображаются корректно
- ✅ Отправка сообщений работает
- ✅ Статусы доставки отображаются
- ✅ Auto-scroll работает
- ✅ Загрузка истории работает

---

### US-025: Real-time Messaging
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 7-8

**Описание**: Реализовать real-time обновление сообщений

**Задачи**:
- [ ] Настроить WebSocket соединение для чата
- [ ] Реализовать подписку на новые сообщения
- [ ] Добавить reconnection logic при потере connection
- [ ] Реализовать optimistic updates при отправке
- [ ] Добавить индикатор typing (менеджер печатает)
- [ ] Реализовать offline queue для сообщений

**Критерии приемки**:
- ✅ WebSocket соединение работает
- ✅ Новые сообщения приходят в real-time
- ✅ Reconnection работает при потере связи
- ✅ Optimistic updates работают
- ✅ Typing indicator отображается

---

### US-026: Отправка вложений в чат
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 8

**Описание**: Реализовать отправку файлов и изображений в чат

**Задачи**:
- [ ] Добавить кнопку attachment в input
- [ ] Реализовать picker для изображений (camera + gallery)
- [ ] Реализовать picker для документов
- [ ] Добавить preview перед отправкой
- [ ] Реализовать upload файлов на сервер
- [ ] Добавить progress indicator для загрузки
- [ ] Реализовать отображение вложений в чате
- [ ] Добавить download functionality для полученных файлов

**Критерии приемки**:
- ✅ Можно выбрать изображение или документ
- ✅ Preview работает перед отправкой
- ✅ Upload с progress indicator работает
- ✅ Вложения отображаются в чате
- ✅ Download файлов работает

---

### US-027: Push-уведомления для чата
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 8

**Описание**: Уведомления о новых сообщениях

**Задачи**:
- [ ] Настроить Firebase Cloud Messaging
- [ ] Настроить Apple Push Notifications (APNs)
- [ ] Реализовать регистрацию device token
- [ ] Добавить обработку push-уведомлений
- [ ] Реализовать deep link в чат при tap на уведомление
- [ ] Добавить управление подписками на уведомления

**Критерии приемки**:
- ✅ Push-уведомления приходят на iOS
- ✅ Push-уведомления приходят на Android
- ✅ Deep link в чат работает
- ✅ Управление подписками работает

---

## EPIC 8: User Profile & Settings (P1)

**Приоритет**: P1 - Should Have  
**Milestone**: v1.0 Release  
**GitHub Issue**: [#76](https://github.com/vovkins/agents-react-native-experiment-2/issues/76)  
**Total Story Points**: 13 SP

### US-028: Экран профиля пользователя
**Приоритет**: P1  
**Story Points**: 3  
**Milestone**: Sprint 9

**Описание**: Создать экран с информацией о клиенте

**Задачи**:
- [ ] Создать UI для экрана профиля
- [ ] Отобразить имя, email, телефон клиента
- [ ] Показать дату регистрации
- [ ] Добавить раздел настроек
- [ ] Добавить раздел безопасности
- [ ] Добавить ссылки на документы (privacy policy, terms)

**Критерии приемки**:
- ✅ Профиль пользователя отображается
- ✅ Все разделы доступны
- ✅ Ссылки на документы работают

---

### US-029: Настройки уведомлений
**Приоритет**: P1  
**Story Points**: 3  
**Milestone**: Sprint 9

**Описание**: Экран настройки push-уведомлений

**Задачи**:
- [ ] Создать UI для настроек уведомлений
- [ ] Добавить toggle для уведомлений чата
- [ ] Добавить toggle для уведомлений портфеля
- [ ] Добавить toggle для уведомлений о продуктах
- [ ] Реализовать сохранение настроек
- [ ] Синхронизировать с backend

**Критерии приемки**:
- ✅ Настройки отображаются
- ✅ Toggles работают
- ✅ Настройки сохраняются

---

### US-030: Настройки безопасности
**Приоритет**: P1  
**Story Points**: 5  
**Milestone**: Sprint 9

**Описание**: Экран управления безопасностью аккаунта

**Задачи**:
- [ ] Создать UI для настроек безопасности
- [ ] Реализовать смену пароля
- [ ] Добавить toggle для биометрического входа
- [ ] Показать активные сессии
- [ ] Реализовать logout из других устройств
- [ ] Добавить двухфакторную аутентификацию (опционально)

**Критерии приемки**:
- ✅ Смена пароля работает
- ✅ Биометрия настраивается
- ✅ Список сессий отображается
- ✅ Logout из других устройств работает

---

### US-031: Logout functionality
**Приоритет**: P1  
**Story Points**: 2  
**Milestone**: Sprint 9

**Описание**: Реализовать выход из аккаунта

**Задачи**:
- [ ] Добавить кнопку logout в профиль
- [ ] Реализовать подтверждение logout
- [ ] Очистить local storage при logout
- [ ] Отозвать tokens на backend
- [ ] Перенаправить на экран входа

**Критерии приемки**:
- ✅ Logout работает корректно
- ✅ Данные очищаются
- ✅ Перенаправление на login работает

---

## EPIC 9: Product Application (P1)

**Приоритет**: P1 - Should Have  
**Milestone**: v1.0 Release  
**GitHub Issue**: [#77](https://github.com/vovkins/agents-react-native-experiment-2/issues/77)  
**Total Story Points**: 8 SP

### US-032: Форма заявки на продукт
**Приоритет**: P1  
**Story Points**: 5  
**Milestone**: Sprint 9-10

**Описание**: Создать форму для подачи заявки на инвестирование

**Задачи**:
- [ ] Создать UI для формы заявки
- [ ] Добавить поле для суммы инвестирования
- [ ] Показать минимальную сумму для продукта
- [ ] Добавить валидацию суммы
- [ ] Реализовать выбор источника средств (существующий счет / новый)
- [ ] Добавить комментарии к заявке (textarea)
- [ ] Реализовать отправку заявки на backend

**Критерии приемки**:
- ✅ Форма отображается корректно
- ✅ Валидация работает
- ✅ Заявка отправляется успешно
- ✅ Пользователь видит подтверждение

---

### US-033: Подтверждение заявки
**Приоритет**: P1  
**Story Points**: 3  
**Milestone**: Sprint 10

**Описание**: Экран успешной отправки заявки

**Задачи**:
- [ ] Создать UI для экрана подтверждения
- [ ] Показать summary заявки
- [ ] Указать, что менеджер свяжется в ближайшее время
- [ ] Добавить кнопку возврата к продуктам
- [ ] Сохранить заявку в истории (для будущего функционала)

**Критерии приемки**:
- ✅ Подтверждение отображается
- ✅ Summary заявки корректен
- ✅ Возврат к продуктам работает

---

## EPIC 10: Push Notifications System (P1)

**Приоритет**: P1 - Should Have  
**Milestone**: v1.0 Release  
**GitHub Issue**: [#84](https://github.com/vovkins/agents-react-native-experiment-2/issues/84)  
**Total Story Points**: 8 SP

### US-034: Система push-уведомлений
**Приоритет**: P1  
**Story Points**: 5  
**Milestone**: Sprint 9-10

**Описание**: Полноценная система уведомлений

**Задачи**:
- [ ] Настроить Firebase Cloud Messaging (базовая интеграция)
- [ ] Настроить APNs для iOS
- [ ] Реализовать обработку foreground notifications
- [ ] Реализовать обработку background notifications
- [ ] Добавить notification center в приложении
- [ ] Реализовать deep links для всех типов уведомлений
- [ ] Добавить badges для непрочитанных уведомлений

**Критерии приемки**:
- ✅ Push-уведомления работают на обеих платформах
- ✅ Foreground и background обработка работает
- ✅ Deep links работают
- ✅ Notification center отображает историю

---

### US-035: Уведомления о событиях портфеля
**Приоритет**: P1  
**Story Points**: 3  
**Milestone**: Sprint 10

**Описание**: Уведомления об изменениях в портфеле

**Задачи**:
- [ ] Определить типы событий портфеля
- [ ] Реализовать уведомления о изменении стоимости
- [ ] Добавить уведомления о выплатах (дивиденды, купоны)
- [ ] Реализовать уведомления о ребалансировке
- [ ] Добавить настройку порога уведомлений (% изменения)

**Критерии приемки**:
- ✅ Уведомления приходят при событиях
- ✅ Настройка порога работает
- ✅ Deep link ведет в портфель

---

## EPIC 11: Analytics & Reports (P2)

**Приоритет**: P2 - Could Have  
**Milestone**: v1.1 Release  
**GitHub Issue**: [#78](https://github.com/vovkins/agents-react-native-experiment-2/issues/78)  
**Total Story Points**: 15 SP

### US-036: Сравнение с бенчмарками (5 SP)
### US-037: Экспорт отчетов в PDF (5 SP)
### US-038: Детальная аналитика по рискам (5 SP)

---

## EPIC 12: News & Market Analytics (P2)

**Приоритет**: P2 - Could Have  
**Milestone**: v1.1 Release  
**GitHub Issue**: [#79](https://github.com/vovkins/agents-react-native-experiment-2/issues/79)  
**Total Story Points**: 10 SP

### US-039: Лента новостей (5 SP)
### US-040: Аналитические обзоры рынка (5 SP)

---

## EPIC 13: Localization (P2)

**Приоритет**: P2 - Could Have  
**Milestone**: v1.1 Release  
**GitHub Issue**: [#80](https://github.com/vovkins/agents-react-native-experiment-2/issues/80)  
**Total Story Points**: 5 SP

### US-041: Мультиязычность (5 SP)

---

## EPIC 14: Testing & Quality Assurance (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#81](https://github.com/vovkins/agents-react-native-experiment-2/issues/81)  
**Total Story Points**: 16 SP

### US-042: Unit Testing
**Приоритет**: P0  
**Story Points**: 8  
**Milestone**: Sprint 7-8

**Описание**: Написать unit тесты для критических компонентов

**Задачи**:
- [ ] Настроить Jest и React Native Testing Library
- [ ] Написать тесты для Domain entities
- [ ] Написать тесты для Use Cases
- [ ] Написать тесты для View Models
- [ ] Написать тесты для utility функций
- [ ] Достичь coverage > 60%

**Критерии приемки**:
- ✅ Все тесты проходят
- ✅ Code coverage > 60%
- ✅ Критические сценарии покрыты

---

### US-043: Integration Testing
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 8

**Описание**: Интеграционные тесты для ключевых flow

**Задачи**:
- [ ] Настроить Detox для E2E тестирования
- [ ] Написать тесты для authentication flow
- [ ] Написать тесты для products flow
- [ ] Написать тесты для portfolio flow
- [ ] Написать тесты для chat flow
- [ ] Настроить CI для запуска E2E тестов

**Критерии приемки**:
- ✅ E2E тесты проходят
- ✅ Все ключевые сценарии покрыты
- ✅ Тесты запускаются в CI

---

### US-044: Security Testing
**Приоритет**: P0  
**Story Points**: 3  
**Milestone**: Sprint 8

**Описание**: Проверка безопасности приложения

**Задачи**:
- [ ] Провести security code review
- [ ] Проверить certificate pinning
- [ ] Проверить secure storage
- [ ] Протестировать на Root/Jailbreak устройствах
- [ ] Проверить защиту от MITM атак
- [ ] Провести penetration testing

**Критерии приемки**:
- ✅ Нет критических security vulnerabilities
- ✅ Certificate pinning работает
- ✅ Secure storage работает корректно

---

## EPIC 15: App Store Deployment (P0)

**Приоритет**: P0 - Must Have  
**Milestone**: MVP Release  
**GitHub Issue**: [#82](https://github.com/vovkins/agents-react-native-experiment-2/issues/82)  
**Total Story Points**: 10 SP

### US-045: Подготовка к публикации в App Store
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 10

**Описание**: Подготовка и публикация в Apple App Store

**Задачи**:
- [ ] Подготовить иконки приложения (все размеры)
- [ ] Подготовить screenshots для разных устройств
- [ ] Написать описание приложения
- [ ] Подготовить privacy policy
- [ ] Настроить App Store Connect
- [ ] Подготовить banking и compliance документы
- [ ] Отправить на review
- [ ] Исправить замечания review team (если есть)

**Критерии приемки**:
- ✅ Приложение опубликовано в App Store
- ✅ Все metadata заполнены
- ✅ Privacy policy доступна

---

### US-046: Подготовка к публикации в Google Play
**Приоритет**: P0  
**Story Points**: 5  
**Milestone**: Sprint 10

**Описание**: Подготовка и публикация в Google Play Store

**Задачи**:
- [ ] Подготовить иконки и graphics assets
- [ ] Подготовить screenshots для разных устройств
- [ ] Написать описание и release notes
- [ ] Настроить Google Play Console
- [ ] Подготовить privacy policy
- [ ] Заполнить content rating questionnaire
- [ ] Отправить на review
- [ ] Исправить замечания (если есть)

**Критерии приемки**:
- ✅ Приложение опубликовано в Google Play
- ✅ Все metadata заполнены
- ✅ Privacy policy доступна

---

## EPIC 16: Analytics & Monitoring (P1)

**Приоритет**: P1 - Should Have  
**Milestone**: v1.0 Release  
**GitHub Issue**: [#83](https://github.com/vovkins/agents-react-native-experiment-2/issues/83)  
**Total Story Points**: 8 SP

### US-047: Analytics Integration (3 SP)
### US-048: Crash Reporting (2 SP)
### US-049: Performance Monitoring (3 SP)

---

## Приоритизированный список задач (Summary)

### Sprint 1-2: Foundation (Weeks 1-4) - P0
1. US-001: Инициализация проекта - **P0** - Issue [#65]
2. US-002: Настройка навигации - **P0** - Issue [#66]
3. US-003: Настройка UI Kit и стилей - **P0** - Issue [#67]
4. US-004: Настройка State Management - **P0** - Issue [#68]
5. US-005: Создание Domain Entities - **P0** - Issue [#70]
6. US-006: Создание Repository Interfaces - **P0** - Issue [#70]
7. US-050: Настройка CI/CD - **P0** - Issue [#69]

### Sprint 3-4: Core Features (Weeks 5-8) - P0
8. US-008: Настройка API Client - **P0** - Issue [#71]
9. US-007: Создание Use Cases - **P0** - Issue [#70]
10. US-009: Реализация Repository Implementations - **P0** - Issue [#71]
11. US-010: Local Storage и Offline Support - **P0** - Issue [#71]
12. US-011: Экран входа - **P0** - Issue [#72]
13. US-012: Биометрическая аутентификация - **P0** - Issue [#72]
14. US-013: Session Management - **P0** - Issue [#72]
15. US-014: Безопасность аутентификации - **P0** - Issue [#72]

### Sprint 5-6: Products & Portfolio (Weeks 9-12) - P0
16. US-015: Экран списка продуктов - **P0** - Issue [#73]
17. US-016: Фильтрация продуктов - **P0** - Issue [#73]
18. US-017: Детальный экран продукта - **P0** - Issue [#73]
19. US-018: Графики доходности - **P0** - Issue [#73]
20. US-019: Экран портфеля - **P0** - Issue [#74]
21. US-020: Детализация активов портфеля - **P0** - Issue [#74]
22. US-021: История портфеля и аналитика - **P0** - Issue [#74]
23. US-022: Структура портфеля - **P0** - Issue [#74]

### Sprint 7-8: Chat & Testing (Weeks 13-16) - P0
24. US-023: Экран списка чатов - **P0** - Issue [#75]
25. US-024: Экран чата - **P0** - Issue [#75]
26. US-025: Real-time Messaging - **P0** - Issue [#75]
27. US-026: Отправка вложений в чат - **P0** - Issue [#75]
28. US-027: Push-уведомления для чата - **P0** - Issue [#75]
29. US-042: Unit Testing - **P0** - Issue [#81]
30. US-043: Integration Testing - **P0** - Issue [#81]
31. US-044: Security Testing - **P0** - Issue [#81]

### Sprint 9-10: Polish & Deploy (Weeks 17-20) - P0 + P1
32. US-028: Экран профиля пользователя - **P1** - Issue [#76]
33. US-029: Настройки уведомлений - **P1** - Issue [#76]
34. US-030: Настройки безопасности - **P1** - Issue [#76]
35. US-031: Logout functionality - **P1** - Issue [#76]
36. US-032: Форма заявки на продукт - **P1** - Issue [#77]
37. US-033: Подтверждение заявки - **P1** - Issue [#77]
38. US-034: Система push-уведомлений - **P1** - Issue [#84]
39. US-035: Уведомления о событиях портфеля - **P1** - Issue [#84]
40. US-047: Analytics Integration - **P1** - Issue [#83]
41. US-048: Crash Reporting - **P1** - Issue [#83]
42. US-049: Performance Monitoring - **P1** - Issue [#83]
43. US-045: Подготовка к публикации в App Store - **P0** - Issue [#82]
44. US-046: Подготовка к публикации в Google Play - **P0** - Issue [#82]

---

## Velocity Estimation

**Общее количество Story Points**: ~230 SP

**При условии velocity 25-30 SP per sprint (2 недели)**:
- **Sprint 1-2**: 30 SP - Foundation
- **Sprint 3-4**: 35 SP - Core Features
- **Sprint 5-6**: 40 SP - Products & Portfolio
- **Sprint 7-8**: 35 SP - Chat & Testing
- **Sprint 9-10**: 30 SP - Polish & Deploy
- **Буфер**: 60 SP

**Общая длительность MVP**: ~20 недель (5 месяцев)

---

## Definition of Done

Для каждой User Story:
- [ ] Код написан и соответствует coding standards
- [ ] Unit тесты написаны и проходят (coverage > 60%)
- [ ] Integration/E2E тесты написаны (для критических сценариев)
- [ ] Code review пройден
- [ ] QA тестирование пройдено
- [ ] Документация обновлена (если требуется)
- [ ] Product Owner acceptance получен
- [ ] Нет критических багов
- [ ] Performance не деградировал
- [ ] Security requirements соблюдены

---

## Definition of Ready

Для начала работы над User Story:
- [ ] Story четко сформулирована
- [ ] Acceptance criteria определены
- [ ] Зависимости выявлены
- [ ] Задачи декомпозированы
- [ ] Оценка story points выполнена
- [ ] Нет блокирующих вопросов

---

## Риски Backlog

| Риск | Влияние | Митигация |
|------|---------|-----------|
| Нет API документации | Высокое | Создать mock API, использовать contract-first development |
| Изменение требований | Среднее | Agile процесс, регулярные sprint reviews |
| Технический долг | Среднее | Code review, refactoring time в каждом sprint |
| Недооценка сложности | Среднее | Буфер в оценке, регулярный re-estimation |

---

## История изменений

| Версия | Дата | Автор | Описание изменений |
|--------|------|-------|-------------------|
| 1.0 | 2026-04-08 | PM Agent | Начальная версия backlog |
| 1.1 | 2026-04-08 | PM Agent | Добавлены приоритеты P0-P3 и milestones |

---

*Документ создан PM Agent*
*Последнее обновление: 2026-04-08*