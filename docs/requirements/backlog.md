# Product Backlog

## Обзор
Продукт бэклог для мобильного приложения управляющей компании. Приоритизация выполнена по методу MoSCoW и уровням P0-P3.

**Приоритеты:**
- **P0 (Critical)** - Must Have, MVP обязателен
- **P1 (High)** - Should Have, желательно для MVP
- **P2 (Medium)** - Could Have, возможно после MVP
- **P3 (Low)** - Won't Have, не входит в текущую версию

**Milestones:**
- **MVP Phase 1** - Базовая инфраструктура и аутентификация
- **MVP Phase 2** - Основные функции (Products, Portfolio, Chat)
- **MVP Phase 3** - Тестирование и QA
- **Post-MVP** - Дополнительные функции (P1-P2)

---

## Epic 1: Infrastructure & Setup (P0)

### TASK-001: Project Initialization
**Приоритет:** P0  
**Оценка:** 2 SP  
**Milestone:** MVP Phase 1  
**GitHub Issue:** [#178](https://github.com/vovkins/agents-react-native-experiment-2/issues/178)  
**Business Value:** Критический - основа для всего проекта  
**Описание:** Инициализация React Native проекта для iOS и Android платформ

**Критерии приемки:**
- [ ] React Native проект создан и запускается на iOS симуляторе
- [ ] React Native проект создан и запускается на Android эмуляторе
- [ ] Базовая структура папок создана (src/view, src/domain, src/adapters)
- [ ] ESLint и Prettier настроены
- [ ] TypeScript сконфигурирован
- [ ] Git репозиторий инициализирован с .gitignore

---

### TASK-002: Architecture Setup - Three-Layer Structure
**Приоритет:** P0  
**Оценка:** 3 SP  
**Milestone:** MVP Phase 1  
**GitHub Issue:** [#179](https://github.com/vovkins/agents-react-native-experiment-2/issues/179)  
**Business Value:** Критический - обеспечивает масштабируемость и поддерживаемость  
**Описание:** Настройка трехуровневой архитектуры (View, Domain, Adapters)

**Критерии приемки:**
- [ ] Структура папок для View слоя создана (screens, components, navigation)
- [ ] Структура папок для Domain слоя создана (entities, usecases, repositories/interfaces)
- [ ] Структура папок для Adapters слоя создана (api, storage, mappers)
- [ ] Примеры базовых сущностей созданы (User, Product, Portfolio, Message)
- [ ] Пример репозитория interface создан
- [ ] Документация по архитектуре добавлена в README.md

---

### TASK-003: Styling Setup - Tailwind CSS
**Приоритет:** P0  
**Оценка:** 2 SP  
**Milestone:** MVP Phase 1  
**GitHub Issue:** [#180](https://github.com/vovkins/agents-react-native-experiment-2/issues/180)  
**Business Value:** Высокий - ускоряет разработку UI  
**Описание:** Интеграция Tailwind CSS для стилизации приложения

**Критерии приемки:**
- [ ] Tailwind CSS установлен и сконфигурирован для React Native
- [ ] Базовая тема определена (цвета, шрифты, отступы)
- [ ] Примеры использования Tailwind классов в компонентах
- [ ] Документация по стилизации добавлена

---

### TASK-004: UI Kit Integration - shadcn/ui
**Приоритет:** P0  
**Оценка:** 3 SP  
**Milestone:** MVP Phase 1  
**GitHub Issue:** [#181](https://github.com/vovkins/agents-react-native-experiment-2/issues/181)  
**Business Value:** Высокий - обеспечивает консистентность UI  
**Описание:** Интеграция и адаптация shadcn/ui компонентов для React Native

**Критерии приемки:**
- [ ] shadcn/ui интегрирован в проект
- [ ] Базовые компоненты адаптированы (Button, Input, Card, Text)
- [ ] Компоненты соответствуют дизайн-системе
- [ ] Storybook настроен для компонентов (опционально)

---

### TASK-005: Navigation Setup
**Приоритет:** P0  
**Оценка:** 3 SP  
**Milestone:** MVP Phase 1  
**GitHub Issue:** [#182](https://github.com/vovkins/agents-react-native-experiment-2/issues/182)  
**Business Value:** Критический - необходим для навигации между экранами  
**Описание:** Настройка навигации между экранами приложения

**Критерии приемки:**
- [ ] React Navigation установлен и сконфигурирован
- [ ] Bottom Tab Navigator создан для главных экранов
- [ ] Stack Navigator создан для детальных экранов
- [ ] Примеры навигации между экранами работают
- [ ] Типизация навигации настроена

---

## Epic 2: Authentication & Authorization (P0 - MUST HAVE)

### FEAT-001: User Authentication Flow
**Приоритет:** P0  
**Оценка:** 8 SP  
**Milestone:** MVP Phase 1  
**GitHub Issue:** [#183](https://github.com/vovkins/agents-react-native-experiment-2/issues/183)  
**Business Value:** Критический - безопасность и доступ к приложению  
**Эпик:** Authentication  
**Зависимости:** TASK-001, TASK-002, TASK-005

**Описание:** Полный цикл аутентификации пользователя (вход, выход, восстановление пароля)

**Критерии приемки:**
- [ ] Экран входа с полями логин/пароль
- [ ] Валидация формы входа
- [ ] Интеграция с API аутентификации
- [ ] Хранение токена авторизации в безопасном хранилище (Keychain/Keystore)
- [ ] Экран восстановления пароля
- [ ] Отправка email для восстановления пароля
- [ ] Экран регистрации (если применимо)
- [ ] Автоматический вход при наличии валидного токена
- [ ] Кнопка выхода из приложения
- [ ] Автоматический выход после периода неактивности

---

### FEAT-002: Secure Token Storage
**Приоритет:** P0  
**Оценка:** 3 SP  
**Milestone:** MVP Phase 1  
**GitHub Issue:** [#184](https://github.com/vovkins/agents-react-native-experiment-2/issues/184)  
**Business Value:** Критический - безопасность данных клиента  
**Эпик:** Authentication  
**Зависимости:** TASK-002

**Описание:** Безопасное хранение токенов авторизации на устройстве

**Критерии приемки:**
- [ ] iOS: токены хранятся в Keychain
- [ ] Android: токены хранятся в EncryptedSharedPreferences
- [ ] Токены автоматически удаляются при выходе
- [ ] Токены валидируются при запуске приложения

---

## Epic 3: Product Showcase (P0 - MUST HAVE)

### FEAT-003: Products List Screen
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#185](https://github.com/vovkins/agents-react-native-experiment-2/issues/185)  
**Business Value:** Критический - основная функция для клиентов  
**Эпик:** Product Showcase  
**Зависимости:** TASK-002, TASK-003, TASK-005

**Описание:** Экран со списком доступных инвестиционных продуктов и стратегий

**Критерии приемки:**
- [ ] Отображение списка продуктов в виде карточек
- [ ] Каждая карточка содержит: название, краткое описание, доходность, уровень риска
- [ ] Pull-to-refresh для обновления списка
- [ ] Skeleton loading при загрузке данных
- [ ] Обработка состояния ошибки загрузки
- [ ] Обработка пустого состояния (нет продуктов)
- [ ] Навигация на детальный экран продукта по нажатию

---

### FEAT-004: Product Detail Screen
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#186](https://github.com/vovkins/agents-react-native-experiment-2/issues/186)  
**Business Value:** Высокий - детальная информация для принятия решений  
**Эпик:** Product Showcase  
**Зависимости:** FEAT-003

**Описание:** Детальный экран с информацией о конкретном инвестиционном продукте

**Критерии приемки:**
- [ ] Отображение детальной информации о продукте
- [ ] Полное описание стратегии управления
- [ ] Историческая доходность
- [ ] Минимальная сумма инвестиций
- [ ] Уровень риска
- [ ] Условия управления
- [ ] Кнопка "Связаться с менеджером" (открывает чат)
- [ ] Возможность поделиться информацией о продукте

---

### FEAT-005: Individual Trust Management Product
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#187](https://github.com/vovkins/agents-react-native-experiment-2/issues/187)  
**Business Value:** Высокий - премиум продукт для VIP клиентов  
**Эпик:** Product Showcase  
**Зависимости:** FEAT-003

**Описание:** Специальный экран для продукта индивидуального доверительного управления

**Критерии приемки:**
- [ ] Отдельный экран или секция для ИДУ
- [ ] Описание преимуществ индивидуального подхода
- [ ] Информация о минимальной сумме
- [ ] Форма заявки на консультацию (опционально)
- [ ] Кнопка связи с менеджером

---

## Epic 4: Portfolio Management (P0 - MUST HAVE)

### FEAT-006: Portfolio Overview Screen
**Приоритет:** P0  
**Оценка:** 8 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#188](https://github.com/vovkins/agents-react-native-experiment-2/issues/188)  
**Business Value:** Критический - основная функция для клиентов  
**Эпик:** Portfolio  
**Зависимости:** TASK-002, TASK-003, TASK-005

**Описание:** Главный экран с текущим портфелем активов пользователя

**Критерии приемки:**
- [ ] Отображение общей стоимости портфеля
- [ ] Отображение изменения стоимости (абсолютное и в %)
- [ ] Визуализация структуры портфеля (круговая диаграмма)
- [ ] Список активов с их долей и стоимостью
- [ ] Pull-to-refresh для обновления данных
- [ ] Обработка состояния "нет портфеля" (новый клиент)
- [ ] Обработка ошибок загрузки

---

### FEAT-007: Asset Detail View
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#189](https://github.com/vovkins/agents-react-native-experiment-2/issues/189)  
**Business Value:** Высокий - прозрачность для клиента  
**Эпик:** Portfolio  
**Зависимости:** FEAT-006

**Описание:** Детальная информация о конкретном активе в портфеле

**Критерии приемки:**
- [ ] Название и тип актива
- [ ] Текущая стоимость
- [ ] Количество/доля в портфеле
- [ ] Изменение стоимости за период
- [ ] График динамики стоимости (опционально для MVP)

---

### FEAT-008: Portfolio History
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#190](https://github.com/vovkins/agents-react-native-experiment-2/issues/190)  
**Business Value:** Высокий - история операций для клиента  
**Эпик:** Portfolio  
**Зависимости:** FEAT-006

**Описание:** История изменений портфеля

**Критерии приемки:**
- [ ] Список операций с портфелем
- [ ] Фильтрация по типу операции (пополнение, вывод, ребалансировка)
- [ ] Фильтрация по дате
- [ ] Детали каждой операции

---

## Epic 5: Chat with Manager (P0 - MUST HAVE)

### FEAT-009: Chat Screen UI
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#191](https://github.com/vovkins/agents-react-native-experiment-2/issues/191)  
**Business Value:** Критический - коммуникация с менеджером  
**Эпик:** Chat  
**Зависимости:** TASK-002, TASK-003, TASK-005

**Описание:** UI для экрана чата с персональным менеджером

**Критерии приемки:**
- [ ] Отображение списка сообщений
- [ ] Поле ввода сообщения
- [ ] Кнопка отправки сообщения
- [ ] Автоскролл к последнему сообщению
- [ ] Отображение времени сообщения
- [ ] Индикатор отправки сообщения
- [ ] Различие между своими сообщениями и сообщениями менеджера

---

### FEAT-010: Real-time Messaging
**Приоритет:** P0  
**Оценка:** 8 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#192](https://github.com/vovkins/agents-react-native-experiment-2/issues/192)  
**Business Value:** Критический - real-time коммуникация  
**Эпик:** Chat  
**Зависимости:** FEAT-009

**Описание:** Real-time отправка и получение сообщений

**Критерии приемки:**
- [ ] Интеграция с WebSocket или polling для real-time обновлений
- [ ] Отправка сообщений через API
- [ ] Получение сообщений в реальном времени
- [ ] Очередь сообщений при отсутствии сети (офлайн режим)
- [ ] Автоматическая отправка при восстановлении связи
- [ ] Повторная отправка при ошибке

---

### FEAT-011: Chat History
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#193](https://github.com/vovkins/agents-react-native-experiment-2/issues/193)  
**Business Value:** Высокий - сохранение истории переписки  
**Эпик:** Chat  
**Зависимости:** FEAT-009

**Описание:** Загрузка и отображение истории переписки

**Критерии приемки:**
- [ ] Загрузка истории сообщений при открытии чата
- [ ] Пагинация при скролле вверх (подгрузка старых сообщений)
- [ ] Кэширование истории локально
- [ ] Отображение индикатора загрузки

---

### FEAT-012: Chat Notifications
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 2  
**GitHub Issue:** [#194](https://github.com/vovkins/agents-react-native-experiment-2/issues/194)  
**Business Value:** Высокий - уведомления о новых сообщениях  
**Эпик:** Chat  
**Зависимости:** FEAT-010

**Описание:** Уведомления о новых сообщениях в чате

**Критерии приемки:**
- [ ] Push-уведомление о новом сообщении
- [ ] Badge на иконке приложения
- [ ] Badge на табе чата в приложении
- [ ] Предпросмотр сообщения в уведомлении
- [ ] Переход в чат по нажатию на уведомление

---

## Epic 6: Push Notifications (P1 - SHOULD HAVE)

### FEAT-013: Push Notifications Integration
**Приоритет:** P1  
**Оценка:** 8 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#198](https://github.com/vovkins/agents-react-native-experiment-2/issues/198)  
**Business Value:** Высокий - улучшение вовлеченности пользователей  
**Эпик:** Notifications  
**Зависимости:** TASK-001

**Описание:** Интеграция системы push-уведомлений

**Критерии приемки:**
- [ ] Firebase Cloud Messaging интегрирован для Android
- [ ] Apple Push Notifications интегрирован для iOS
- [ ] Запрос разрешения на уведомления
- [ ] Регистрация устройства для уведомлений
- [ ] Обработка foreground уведомлений
- [ ] Обработка background уведомлений
- [ ] Навигация по нажатию на уведомление

---

### FEAT-014: Notification Types
**Приоритет:** P1  
**Оценка:** 3 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#199](https://github.com/vovkins/agents-react-native-experiment-2/issues/199)  
**Business Value:** Средний - персонализация уведомлений  
**Эпик:** Notifications  
**Зависимости:** FEAT-013

**Описание:** Различные типы уведомлений

**Критерии приемки:**
- [ ] Уведомления о новых сообщениях
- [ ] Уведомления об изменениях в портфеле
- [ ] Уведомления о новых продуктах
- [ ] Настройки уведомлений (включение/выключение по типам)

---

## Epic 7: Biometric Authentication (P1 - SHOULD HAVE)

### FEAT-015: Biometric Login
**Приоритет:** P1  
**Оценка:** 5 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#200](https://github.com/vovkins/agents-react-native-experiment-2/issues/200)  
**Business Value:** Высокий - улучшение UX и безопасности  
**Эпик:** Authentication  
**Зависимости:** FEAT-001, FEAT-002

**Описание:** Вход в приложение с помощью биометрии

**Критерии приемки:**
- [ ] Touch ID / Face ID интегрирован для iOS
- [ ] Fingerprint / Face Unlock интегрирован для Android
- [ ] Запрос разрешения на использование биометрии
- [ ] Fallback на пароль при отказе от биометрии
- [ ] Настройка включения/выключения биометрического входа

---

## Epic 8: User Profile (P1 - SHOULD HAVE)

### FEAT-016: Profile Screen
**Приоритет:** P1  
**Оценка:** 5 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#201](https://github.com/vovkins/agents-react-native-experiment-2/issues/201)  
**Business Value:** Средний - управление профилем  
**Эпик:** Profile  
**Зависимости:** TASK-002, TASK-005

**Описание:** Экран профиля пользователя

**Критерии приемки:**
- [ ] Отображение имени пользователя
- [ ] Отображение email
- [ ] Отображение контактного телефона
- [ ] Кнопка редактирования профиля
- [ ] Настройки уведомлений
- [ ] Кнопка выхода из аккаунта

---

### FEAT-017: Edit Profile
**Приоритет:** P1  
**Оценка:** 3 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#202](https://github.com/vovkins/agents-react-native-experiment-2/issues/202)  
**Business Value:** Средний - редактирование данных  
**Эпик:** Profile  
**Зависимости:** FEAT-016

**Описание:** Редактирование профиля пользователя

**Критерии приемки:**
- [ ] Редактирование контактного телефона
- [ ] Валидация введенных данных
- [ ] Сохранение изменений через API
- [ ] Отображение успеха сохранения

---

## Epic 9: Documents & Reports (P2 - COULD HAVE)

### FEAT-018: Documents Screen
**Приоритет:** P2  
**Оценка:** 5 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#205](https://github.com/vovkins/agents-react-native-experiment-2/issues/205)  
**Business Value:** Средний - доступ к документам  
**Эпик:** Documents  
**Зависимости:** TASK-002, TASK-005

**Описание:** Экран с документами по портфелю

**Критерии приемки:**
- [ ] Список документов с датой и типом
- [ ] Фильтрация по типу документа
- [ ] Предпросмотр документа
- [ ] Скачивание документа в PDF
- [ ] Шаринг документа

---

## Epic 10: Charts & Analytics (P2 - COULD HAVE)

### FEAT-019: Portfolio Charts
**Приоритет:** P2  
**Оценка:** 8 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#206](https://github.com/vovkins/agents-react-native-experiment-2/issues/206)  
**Business Value:** Средний - визуализация для клиента  
**Эпик:** Analytics  
**Зависимости:** FEAT-006

**Описание:** Графики и визуализация портфеля

**Критерии приемки:**
- [ ] График динамики стоимости портфеля
- [ ] Выбор периода (неделя, месяц, год, все время)
- [ ] Круговая диаграмма структуры портфеля
- [ ] Сравнение с бенчмарками (опционально)

---

## Epic 11: Educational Content (P2 - COULD HAVE)

### FEAT-020: FAQ Screen
**Приоритет:** P2  
**Оценка:** 3 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#207](https://github.com/vovkins/agents-react-native-experiment-2/issues/207)  
**Business Value:** Низкий - информационная поддержка  
**Эпик:** Education  
**Зависимости:** TASK-002, TASK-005

**Описание:** Экран с часто задаваемыми вопросами

**Критерии приемки:**
- [ ] Список вопросов с ответами
- [ ] Поиск по вопросам
- [ ] Категоризация вопросов

---

### FEAT-021: Investment Glossary
**Приоритет:** P2  
**Оценка:** 3 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#208](https://github.com/vovkins/agents-react-native-experiment-2/issues/208)  
**Business Value:** Низкий - образовательный контент  
**Эпик:** Education  
**Зависимости:** TASK-002, TASK-005

**Описание:** Глоссарий инвестиционных терминов

**Критерии приемки:**
- [ ] Список терминов с определениями
- [ ] Поиск по терминам
- [ ] Алфавитный указатель

---

## Epic 12: Testing & QA (P0)

### TASK-006: Unit Tests Setup
**Приоритет:** P0  
**Оценка:** 3 SP  
**Milestone:** MVP Phase 3  
**GitHub Issue:** [#195](https://github.com/vovkins/agents-react-native-experiment-2/issues/195)  
**Business Value:** Высокий - качество кода  
**Описание:** Настройка инфраструктуры для unit-тестирования

**Критерии приемки:**
- [ ] Jest сконфигурирован для React Native
- [ ] React Native Testing Library установлен
- [ ] Примеры тестов для компонентов
- [ ] Примеры тестов для domain-логики
- [ ] Coverage отчет настроен

---

### TASK-007: E2E Tests Setup
**Приоритет:** P0  
**Оценка:** 5 SP  
**Milestone:** MVP Phase 3  
**GitHub Issue:** [#196](https://github.com/vovkins/agents-react-native-experiment-2/issues/196)  
**Business Value:** Высокий - тестирование критических сценариев  
**Описание:** Настройка инфраструктуры для E2E тестирования

**Критерии приемки:**
- [ ] Detox или Maestro установлен и сконфигурирован
- [ ] Тесты для критических сценариев (вход, просмотр портфеля)
- [ ] Запуск тестов в CI настроен

---

### TASK-008: Test Coverage - 70% Minimum
**Приоритет:** P0  
**Оценка:** 13 SP  
**Milestone:** MVP Phase 3  
**GitHub Issue:** [#197](https://github.com/vovkins/agents-react-native-experiment-2/issues/197)  
**Business Value:** Критический - качество продукта  
**Описание:** Написание тестов для достижения 70% coverage

**Критерии приемки:**
- [ ] Unit-тесты для domain-слоя (сущности, use cases)
- [ ] Unit-тесты для адаптеров (API клиенты, мапперы)
- [ ] Component-тесты для UI компонентов
- [ ] Integration-тесты для критических флоу
- [ ] Coverage >= 70%

---

## Epic 13: DevOps & CI/CD (P1)

### TASK-009: CI/CD Pipeline Setup
**Приоритет:** P1  
**Оценка:** 5 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#203](https://github.com/vovkins/agents-react-native-experiment-2/issues/203)  
**Business Value:** Высокий - автоматизация развертывания  
**Описание:** Настройка CI/CD пайплайна

**Критерии приемки:**
- [ ] GitHub Actions или аналогичный CI настроен
- [ ] Автоматический запуск тестов при PR
- [ ] Автоматическая сборка dev версии
- [ ] Автоматическая сборка staging версии
- [ ] Автоматическая сборка production версии

---

### TASK-010: Code Quality Tools
**Приоритет:** P1  
**Оценка:** 2 SP  
**Milestone:** Post-MVP  
**GitHub Issue:** [#204](https://github.com/vovkins/agents-react-native-experiment-2/issues/204)  
**Business Value:** Средний - качество кода  
**Описание:** Настройка инструментов контроля качества кода

**Критерии приемки:**
- [ ] ESLint правила настроены
- [ ] Prettier настроен
- [ ] Husky pre-commit hooks настроены
- [ ] TypeScript strict mode включен
- [ ] Lint-staged настроен

---

## Приоритизация бэклога по Milestone

### MVP Phase 1 - Infrastructure & Authentication (13 SP)
**Цель:** Базовая инфраструктура и аутентификация

| Задача | Приоритет | Оценка | GitHub Issue |
|--------|-----------|--------|--------------|
| TASK-001: Project Initialization | P0 | 2 SP | #178 |
| TASK-002: Architecture Setup | P0 | 3 SP | #179 |
| TASK-003: Styling Setup | P0 | 2 SP | #180 |
| TASK-004: UI Kit Integration | P0 | 3 SP | #181 |
| TASK-005: Navigation Setup | P0 | 3 SP | #182 |
| FEAT-001: User Authentication Flow | P0 | 8 SP | #183 |
| FEAT-002: Secure Token Storage | P0 | 3 SP | #184 |

**Итого Phase 1:** 24 SP

---

### MVP Phase 2 - Core Features (51 SP)
**Цель:** Основные функции (Products, Portfolio, Chat)

| Задача | Приоритет | Оценка | GitHub Issue |
|--------|-----------|--------|--------------|
| FEAT-003: Products List Screen | P0 | 5 SP | #185 |
| FEAT-004: Product Detail Screen | P0 | 5 SP | #186 |
| FEAT-005: Individual Trust Management Product | P0 | 5 SP | #187 |
| FEAT-006: Portfolio Overview Screen | P0 | 8 SP | #188 |
| FEAT-007: Asset Detail View | P0 | 5 SP | #189 |
| FEAT-008: Portfolio History | P0 | 5 SP | #190 |
| FEAT-009: Chat Screen UI | P0 | 5 SP | #191 |
| FEAT-010: Real-time Messaging | P0 | 8 SP | #192 |
| FEAT-011: Chat History | P0 | 5 SP | #193 |
| FEAT-012: Chat Notifications | P0 | 5 SP | #194 |

**Итого Phase 2:** 51 SP

---

### MVP Phase 3 - Testing & QA (21 SP)
**Цель:** Качество и тестирование

| Задача | Приоритет | Оценка | GitHub Issue |
|--------|-----------|--------|--------------|
| TASK-006: Unit Tests Setup | P0 | 3 SP | #195 |
| TASK-007: E2E Tests Setup | P0 | 5 SP | #196 |
| TASK-008: Test Coverage - 70% Minimum | P0 | 13 SP | #197 |

**Итого Phase 3:** 21 SP

---

### Post-MVP - Additional Features (31 SP P1 + 19 SP P2 = 50 SP)
**Цель:** Дополнительные функции и улучшения

| Задача | Приоритет | Оценка | GitHub Issue |
|--------|-----------|--------|--------------|
| FEAT-013: Push Notifications Integration | P1 | 8 SP | #198 |
| FEAT-014: Notification Types | P1 | 3 SP | #199 |
| FEAT-015: Biometric Login | P1 | 5 SP | #200 |
| FEAT-016: Profile Screen | P1 | 5 SP | #201 |
| FEAT-017: Edit Profile | P1 | 3 SP | #202 |
| TASK-009: CI/CD Pipeline Setup | P1 | 5 SP | #203 |
| TASK-010: Code Quality Tools | P1 | 2 SP | #204 |
| FEAT-018: Documents Screen | P2 | 5 SP | #205 |
| FEAT-019: Portfolio Charts | P2 | 8 SP | #206 |
| FEAT-020: FAQ Screen | P2 | 3 SP | #207 |
| FEAT-021: Investment Glossary | P2 | 3 SP | #208 |

**Итого Post-MVP:** 50 SP

---

## Общая сводка по приоритетам

### P0 - Critical (MVP обязательные)
**Всего:** 20 задач, 96 SP

1. TASK-001: Project Initialization (2 SP) - #178
2. TASK-002: Architecture Setup (3 SP) - #179
3. TASK-003: Styling Setup (2 SP) - #180
4. TASK-004: UI Kit Integration (3 SP) - #181
5. TASK-005: Navigation Setup (3 SP) - #182
6. FEAT-001: User Authentication Flow (8 SP) - #183
7. FEAT-002: Secure Token Storage (3 SP) - #184
8. FEAT-003: Products List Screen (5 SP) - #185
9. FEAT-004: Product Detail Screen (5 SP) - #186
10. FEAT-005: Individual Trust Management Product (5 SP) - #187
11. FEAT-006: Portfolio Overview Screen (8 SP) - #188
12. FEAT-007: Asset Detail View (5 SP) - #189
13. FEAT-008: Portfolio History (5 SP) - #190
14. FEAT-009: Chat Screen UI (5 SP) - #191
15. FEAT-010: Real-time Messaging (8 SP) - #192
16. FEAT-011: Chat History (5 SP) - #193
17. FEAT-012: Chat Notifications (5 SP) - #194
18. TASK-006: Unit Tests Setup (3 SP) - #195
19. TASK-007: E2E Tests Setup (5 SP) - #196
20. TASK-008: Test Coverage - 70% Minimum (13 SP) - #197

### P1 - High (Желательно для MVP)
**Всего:** 7 задач, 31 SP

1. FEAT-013: Push Notifications Integration (8 SP) - #198
2. FEAT-014: Notification Types (3 SP) - #199
3. FEAT-015: Biometric Login (5 SP) - #200
4. FEAT-016: Profile Screen (5 SP) - #201
5. FEAT-017: Edit Profile (3 SP) - #202
6. TASK-009: CI/CD Pipeline Setup (5 SP) - #203
7. TASK-010: Code Quality Tools (2 SP) - #204

### P2 - Medium (После MVP)
**Всего:** 4 задачи, 19 SP

1. FEAT-018: Documents Screen (5 SP) - #205
2. FEAT-019: Portfolio Charts (8 SP) - #206
3. FEAT-020: FAQ Screen (3 SP) - #207
4. FEAT-021: Investment Glossary (3 SP) - #208

---

## Оценка общего объема работ

| Milestone | Количество задач | Объем (SP) | Примерное время (2 недели/спринт) |
|-----------|------------------|------------|-----------------------------------|
| MVP Phase 1 | 7 | 24 SP | ~3 спринта |
| MVP Phase 2 | 10 | 51 SP | ~6 спринтов |
| MVP Phase 3 | 3 | 21 SP | ~2.5 спринта |
| **MVP Итого** | **20** | **96 SP** | **~11.5 спринтов** |
| Post-MVP | 11 | 50 SP | ~6 спринтов |
| **ВСЕГО** | **31** | **146 SP** | **~17.5 спринтов** |

---

## Рекомендации по Sprint Planning

### Sprint Velocity
При velocity 10 SP за спринт:
- **MVP Phase 1:** 2.4 спринта (~5 недель)
- **MVP Phase 2:** 5.1 спринта (~10 недель)
- **MVP Phase 3:** 2.1 спринта (~4 недели)
- **MVP Total:** ~19 недель

### Команда
Рекомендуемый состав для MVP:
- 1 Tech Lead / Senior React Native Developer
- 1-2 Middle React Native Developer
- 1 QA Engineer
- 1 UI/UX Designer (part-time)

---

## Зависимости

```
TASK-001 (Project Init)
    ├─> TASK-002 (Architecture)
    │       ├─> FEAT-001 (Auth)
    │       ├─> FEAT-003 (Products)
    │       ├─> FEAT-006 (Portfolio)
    │       └─> FEAT-009 (Chat)
    ├─> TASK-003 (Styling)
    ├─> TASK-004 (UI Kit)
    ├─> TASK-005 (Navigation)
    └─> FEAT-013 (Push Notifications)

FEAT-001 (Auth) -> FEAT-002 (Token Storage) -> FEAT-015 (Biometric)

FEAT-003 (Products List) -> FEAT-004 (Product Detail)
FEAT-003 (Products List) -> FEAT-005 (IDU Product)

FEAT-006 (Portfolio) -> FEAT-007 (Asset Detail)
FEAT-006 (Portfolio) -> FEAT-008 (History)
FEAT-006 (Portfolio) -> FEAT-019 (Charts - P2)

FEAT-009 (Chat UI) -> FEAT-010 (Real-time)
FEAT-009 (Chat UI) -> FEAT-011 (History)
FEAT-010 (Real-time) -> FEAT-012 (Notifications)

FEAT-013 (Push) -> FEAT-014 (Notification Types)
```

---

## Критические пути

### Критический путь MVP:
TASK-001 → TASK-002 → FEAT-001 → FEAT-006 → FEAT-010 → TASK-008

**Длина критического пути:** ~39 SP (~4 месяца при velocity 10 SP/спринт)

---

## Риски и митигация

| Риск | Вероятность | Влияние | Митигация |
|------|-------------|---------|-----------|
| Задержка готовности бэкенд API | Средняя | Высокое | Раннее согласование контрактов API, использование моков на начальном этапе |
| Изменения требований | Средняя | Среднее | Гибкая методология, приоритизация изменений |
| Проблемы с интеграцией | Средняя | Высокое | Ранний этап интеграции, технический спайк |
| Нехватка ресурсов | Низкая | Высокое | Резервное время в плане, приоритизация P0 |

---

## История изменений

| Дата | Версия | Описание |
|------|--------|----------|
| 2026-04-13 | 1.0 | Начальная версия бэклога |
| 2026-04-13 | 2.0 | Добавлена приоритизация по P0-P3, milestones, GitHub Issues |

---

*Документ создан и обновлен PM Agent*
