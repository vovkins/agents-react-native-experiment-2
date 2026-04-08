# Product Backlog

**Проект**: Asset Management Client App  
**Дата создания**: 2026-04-08  
**Версия**: 1.0

---

## GitHub Issues Summary

Все эпики и user stories созданы как GitHub Issues:

### Epic Issues (P0 - Must Have):
- **Epic 1**: Project Setup & Infrastructure - [#65](https://github.com/vovkins/agents-react-native-experiment-2/issues/65)
- **Epic 2**: Domain Layer Architecture - [#70](https://github.com/vovkins/agents-react-native-experiment-2/issues/70)
- **Epic 3**: Adapters Layer - API Integration - [#71](https://github.com/vovkins/agents-react-native-experiment-2/issues/71)
- **Epic 4**: Authentication & Authorization - [#72](https://github.com/vovkins/agents-react-native-experiment-2/issues/72)
- **Epic 5**: Products Showcase - [#73](https://github.com/vovkins/agents-react-native-experiment-2/issues/73)
- **Epic 6**: Client Portfolio - [#74](https://github.com/vovkins/agents-react-native-experiment-2/issues/74)
- **Epic 7**: Chat with Manager - [#75](https://github.com/vovkins/agents-react-native-experiment-2/issues/75)
- **Epic 14**: Testing & Quality Assurance - [#81](https://github.com/vovkins/agents-react-native-experiment-2/issues/81)
- **Epic 15**: App Store Deployment - [#82](https://github.com/vovkins/agents-react-native-experiment-2/issues/82)

### Epic Issues (P1 - Should Have):
- **Epic 8**: User Profile & Settings - [#76](https://github.com/vovkins/agents-react-native-experiment-2/issues/76)
- **Epic 9**: Product Application - [#77](https://github.com/vovkins/agents-react-native-experiment-2/issues/77)
- **Epic 10**: Push Notifications System - [#84](https://github.com/vovkins/agents-react-native-experiment-2/issues/84)
- **Epic 16**: Analytics & Monitoring - [#83](https://github.com/vovkins/agents-react-native-experiment-2/issues/83)

### Epic Issues (P2 - Could Have):
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

## Приоритеты

| Приоритет | Обозначение | Описание |
|-----------|-------------|----------|
| **P0** | Must Have | Критически важно для MVP |
| **P1** | Should Have | Важно для первой версии |
| **P2** | Could Have | Желательно в будущих версиях |
| **P3** | Won't Have | Не планируется в текущей версии |

---

## EPIC 1: Project Setup & Infrastructure (P0)

### US-001: Инициализация React Native проекта
**Приоритет**: P0  
**Story Points**: 3  
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

**GitHub Issue**: [#70](https://github.com/vovkins/agents-react-native-experiment-2/issues/70)

### US-005: Создание Domain Entities (5 SP)
**Задачи**: Создать entities (User, Product, Portfolio, Asset, Message, Manager)

### US-006: Создание Repository Interfaces (3 SP)
**Задачи**: Создать interfaces для Auth, Products, Portfolio, Chat, User

### US-007: Создание Use Cases (5 SP)
**Задачи**: Реализовать бизнес-логику для всех доменных областей

---

## EPIC 3: Adapters Layer - API Integration (P0)

**GitHub Issue**: [#71](https://github.com/vovkins/agents-react-native-experiment-2/issues/71)

### US-008: Настройка API Client (3 SP)
**Задачи**: Создать HTTP клиент с JWT auth и certificate pinning

### US-009: Реализация Repository Implementations (5 SP)
**Задачи**: Реализовать репозитории для работы с бэкендом

### US-010: Local Storage и Offline Support (5 SP)
**Задачи**: Реализовать кэширование и offline поддержку

---

## EPIC 4: Authentication & Authorization (P0)

**GitHub Issue**: [#72](https://github.com/vovkins/agents-react-native-experiment-2/issues/72)

### US-011: Экран входа (Login Screen) (5 SP)
**Задачи**: Создать экран аутентификации (phone + SMS, email + password)

### US-012: Биометрическая аутентификация (3 SP)
**Задачи**: Реализовать Face ID / Touch ID

### US-013: Session Management (3 SP)
**Задачи**: Auto-logout, refresh token, logout from all devices

### US-014: Безопасность аутентификации (5 SP)
**Задачи**: Certificate pinning, encryption, secure storage

---

## EPIC 5: Products Showcase (P0)

**GitHub Issue**: [#73](https://github.com/vovkins/agents-react-native-experiment-2/issues/73)

### US-015: Экран списка продуктов (5 SP)
**Задачи**: Создать список продуктов с карточками

### US-016: Фильтрация продуктов (3 SP)
**Задачи**: Реализовать фильтры по категориям и риску

### US-017: Детальный экран продукта (5 SP)
**Задачи**: Создать детальный экран с информацией о продукте

### US-018: Графики доходности (5 SP)
**Задачи**: Реализовать интерактивные графики

---

## EPIC 6: Client Portfolio (P0)

**GitHub Issue**: [#74](https://github.com/vovkins/agents-react-native-experiment-2/issues/74)

### US-019: Экран портфеля (5 SP)
**Задачи**: Создать экран с портфелем клиента

### US-020: Детализация активов портфеля (5 SP)
**Задачи**: Список активов с детализацией

### US-021: История портфеля и аналитика (5 SP)
**Задачи**: График истории и метрики

### US-022: Структура портфеля (3 SP)
**Задачи**: Круговая диаграмма структуры

---

## EPIC 7: Chat with Manager (P0)

**GitHub Issue**: [#75](https://github.com/vovkins/agents-react-native-experiment-2/issues/75)

### US-023: Экран списка чатов (3 SP)
**Задачи**: Создать список чатов

### US-024: Экран чата (8 SP)
**Задачи**: Создать полнофункциональный чат

### US-025: Real-time Messaging (5 SP)
**Задачи**: WebSocket для real-time сообщений

### US-026: Отправка вложений в чат (5 SP)
**Задачи**: Отправка файлов и изображений

### US-027: Push-уведомления для чата (3 SP)
**Задачи**: Уведомления о новых сообщениях

---

## EPIC 8: User Profile & Settings (P1)

**GitHub Issue**: [#76](https://github.com/vovkins/agents-react-native-experiment-2/issues/76)

### US-028: Экран профиля пользователя (3 SP)
### US-029: Настройки уведомлений (3 SP)
### US-030: Настройки безопасности (5 SP)
### US-031: Logout functionality (2 SP)

---

## EPIC 9: Product Application (P1)

**GitHub Issue**: [#77](https://github.com/vovkins/agents-react-native-experiment-2/issues/77)

### US-032: Форма заявки на продукт (5 SP)
### US-033: Подтверждение заявки (3 SP)

---

## EPIC 10: Push Notifications System (P1)

**GitHub Issue**: [#84](https://github.com/vovkins/agents-react-native-experiment-2/issues/84)

### US-034: Система push-уведомлений (5 SP)
### US-035: Уведомления о событиях портфеля (3 SP)

---

## EPIC 11: Analytics & Reports (P2)

**GitHub Issue**: [#78](https://github.com/vovkins/agents-react-native-experiment-2/issues/78)

### US-036: Сравнение с бенчмарками (5 SP)
### US-037: Экспорт отчетов в PDF (5 SP)
### US-038: Детальная аналитика по рискам (5 SP)

---

## EPIC 12: News & Market Analytics (P2)

**GitHub Issue**: [#79](https://github.com/vovkins/agents-react-native-experiment-2/issues/79)

### US-039: Лента новостей (5 SP)
### US-040: Аналитические обзоры рынка (5 SP)

---

## EPIC 13: Localization (P2)

**GitHub Issue**: [#80](https://github.com/vovkins/agents-react-native-experiment-2/issues/80)

### US-041: Мультиязычность (5 SP)

---

## EPIC 14: Testing & Quality Assurance (P0)

**GitHub Issue**: [#81](https://github.com/vovkins/agents-react-native-experiment-2/issues/81)

### US-042: Unit Testing (8 SP)
### US-043: Integration Testing (5 SP)
### US-044: Security Testing (3 SP)

---

## EPIC 15: App Store Deployment (P0)

**GitHub Issue**: [#82](https://github.com/vovkins/agents-react-native-experiment-2/issues/82)

### US-045: Подготовка к публикации в App Store (5 SP)
### US-046: Подготовка к публикации в Google Play (5 SP)

---

## EPIC 16: Analytics & Monitoring (P1)

**GitHub Issue**: [#83](https://github.com/vovkins/agents-react-native-experiment-2/issues/83)

### US-047: Analytics Integration (3 SP)
### US-048: Crash Reporting (2 SP)
### US-049: Performance Monitoring (3 SP)

---

## Приоритизированный список задач (Summary)

### Sprint 1-2: Foundation (Weeks 1-4)
1. US-001: Инициализация проекта - **P0** - Issue [#65]
2. US-002: Настройка навигации - **P0** - Issue [#66]
3. US-003: Настройка UI Kit и стилей - **P0** - Issue [#67]
4. US-004: Настройка State Management - **P0** - Issue [#68]
5. US-005: Создание Domain Entities - **P0** - Issue [#70]
6. US-006: Создание Repository Interfaces - **P0** - Issue [#70]
7. US-050: Настройка CI/CD - **P0** - Issue [#69]

### Sprint 3-4: Core Features (Weeks 5-8)
8. US-008: Настройка API Client - **P0** - Issue [#71]
9. US-007: Создание Use Cases - **P0** - Issue [#70]
10. US-009: Реализация Repository Implementations - **P0** - Issue [#71]
11. US-010: Local Storage и Offline Support - **P0** - Issue [#71]
12. US-011: Экран входа - **P0** - Issue [#72]
13. US-012: Биометрическая аутентификация - **P0** - Issue [#72]
14. US-013: Session Management - **P0** - Issue [#72]
15. US-014: Безопасность аутентификации - **P0** - Issue [#72]

### Sprint 5-6: Products & Portfolio (Weeks 9-12)
16. US-015: Экран списка продуктов - **P0** - Issue [#73]
17. US-016: Фильтрация продуктов - **P0** - Issue [#73]
18. US-017: Детальный экран продукта - **P0** - Issue [#73]
19. US-018: Графики доходности - **P0** - Issue [#73]
20. US-019: Экран портфеля - **P0** - Issue [#74]
21. US-020: Детализация активов портфеля - **P0** - Issue [#74]
22. US-021: История портфеля и аналитика - **P0** - Issue [#74]
23. US-022: Структура портфеля - **P0** - Issue [#74]

### Sprint 7-8: Chat & Testing (Weeks 13-16)
24. US-023: Экран списка чатов - **P0** - Issue [#75]
25. US-024: Экран чата - **P0** - Issue [#75]
26. US-025: Real-time Messaging - **P0** - Issue [#75]
27. US-026: Отправка вложений в чат - **P0** - Issue [#75]
28. US-027: Push-уведомления для чата - **P0** - Issue [#75]
29. US-042: Unit Testing - **P0** - Issue [#81]
30. US-043: Integration Testing - **P0** - Issue [#81]
31. US-044: Security Testing - **P0** - Issue [#81]

### Sprint 9-10: Polish & Deploy (Weeks 17-20)
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

---

*Документ создан PM Agent*
*Последнее обновление: 2026-04-08*