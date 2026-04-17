# Product Backlog (Epic Level)

**Проект:** Мобильное приложение для клиентов управляющей компании  
**Статус:** Prioritized  
**Дата:** 2026-04-17  

---

## Epic 1: Authentication & Onboarding

**Приоритет:** P0 (Must Have)  
**MoSCoW:** Must Have  
**Milestone:** MVP v1.0  

**Описание:**  
Система аутентификации и онбординга клиентов. Позволяет пользователям безопасно входить в приложение и получить доступ к своим персональным данным. Критически важна для финансового приложения с чувствительными данными.

**Acceptance Criteria:**
- Пользователь может войти в приложение с использованием безопасной аутентификации
- Поддержка биометрической авторизации (Face ID / Touch ID)
- PIN-код для быстрого доступа при повторном входе
- Безопасное хранение токенов авторизации

**Зависимости:** Нет (фундаментальный эпик)

**GitHub Issue:** [#239](https://github.com/vovkins/agents-react-native-experiment-2/issues/239)

---

## Epic 2: Product Showcase (Витрина продуктов)

**Приоритет:** P0 (Must Have)  
**MoSCoW:** Must Have  
**Milestone:** MVP v1.0  

**Описание:**  
Экран витрины инвестиционных продуктов управляющей компании. Клиенты могут просматривать стратегии доверительного управления и продукты индивидуального доверительного управления с детальной информацией о каждом.

**Acceptance Criteria:**
- Отображение списка доступных инвестиционных стратегий
- Детальная информация о каждом продукте (описание, параметры, условия)
- Возможность просмотра деталей стратегии при нажатии
- Каталог продуктов с категоризацией

**Зависимости:** Epic 1 (Authentication & Onboarding)

**GitHub Issue:** [#240](https://github.com/vovkins/agents-react-native-experiment-2/issues/240)

---

## Epic 3: Portfolio Dashboard (Портфель активов)

**Приоритет:** P0 (Must Have)  
**MoSCoW:** Must Have  
**Milestone:** MVP v1.0  

**Описание:**  
Экран просмотра текущего портфеля активов клиента под управлением. Отображает персональные финансовые данные клиента, состав портфеля и ключевые показатели.

**Acceptance Criteria:**
- Отображение текущей стоимости портфеля
- Состав активов с детализацией по позициям
- Ключевые метрики (доходность, изменение стоимости)
- Обновление данных при синхронизации с бэкендом

**Зависимости:** Epic 1 (Authentication & Onboarding)

**GitHub Issue:** [#241](https://github.com/vovkins/agents-react-native-experiment-2/issues/241)

---

## Epic 4: Chat with Manager (Чат с менеджером)

**Приоритет:** P0 (Must Have)  
**MoSCoW:** Must Have  
**Milestone:** MVP v1.0  

**Описание:**  
In-app чат для коммуникации клиента с персональным менеджером. Позволяет клиентам общаться со своим управляющим напрямую через приложение без использования сторонних мессенджеров.

**Acceptance Criteria:**
- Отправка и получение сообщений в реальном времени
- История переписки сохраняется и доступна
- Уведомления о новых сообщениях
- Отображение статуса менеджера (онлайн/офлайн)

**Зависимости:** Epic 1 (Authentication & Onboarding)

**GitHub Issue:** [#242](https://github.com/vovkins/agents-react-native-experiment-2/issues/242)

---

## Epic 5: Navigation & App Structure

**Приоритет:** P0 (Must Have)  
**MoSCoW:** Must Have  
**Milestone:** MVP v1.0  

**Описание:**  
Навигационная структура приложения с тремя основными разделами: Витрина, Портфель, Чат. Tab-based навигация для удобного переключения между экранами.

**Acceptance Criteria:**
- Bottom tab навигация с тремя основными разделами
- Корректный переход между экранами
- Сохранение состояния при переключении
- Соответствие UI гайдлайнам iOS и Android

**Зависимости:** Epic 1 (Authentication & Onboarding)

**GitHub Issue:** [#243](https://github.com/vovkins/agents-react-native-experiment-2/issues/243)

---

## Epic 6: Data Synchronization & Offline Support

**Приоритет:** P2 (Should Have)  
**MoSCoW:** Should Have  
**Milestone:** v1.1  

**Описание:**  
Синхронизация данных с бэкендом и поддержка офлайн-режима. Кэширование данных для работы без постоянного интернет-соединения.

**Acceptance Criteria:**
- Автоматическая синхронизация при восстановлении соединения
- Кэширование данных портфеля и продуктов
- Индикация статуса соединения
- Обработка ошибок сети

**Зависимости:** Epic 2, Epic 3, Epic 4

**GitHub Issue:** [#244](https://github.com/vovkins/agents-react-native-experiment-2/issues/244)

---

## Epic 7: Push Notifications

**Приоритет:** P2 (Should Have)  
**MoSCoW:** Should Have  
**Milestone:** v1.1  

**Описание:**  
Система push-уведомлений для информирования клиентов о важных событиях: новые сообщения от менеджера, изменения в портфеле, обновления продуктов.

**Acceptance Criteria:**
- Уведомления о новых сообщениях в чате
- Уведомления об изменениях в портфеле
- Настройки уведомлений в профиле пользователя
- Глубокие ссылки (deep links) на соответствующие экраны

**Зависимости:** Epic 4 (Chat with Manager)

**GitHub Issue:** [#245](https://github.com/vovkins/agents-react-native-experiment-2/issues/245)

---

## Epic 8: User Profile & Settings

**Приоритет:** P3 (Could Have)  
**MoSCoW:** Could Have  
**Milestone:** v1.2  

**Описание:**  
Экран профиля пользователя и настроек приложения. Позволяет клиентам управлять своими настройками, уведомлениями и безопасностью.

**Acceptance Criteria:**
- Просмотр персональной информации
- Настройки уведомлений
- Настройки безопасности (смена PIN, биометрия)
- Выход из аккаунта

**Зависимости:** Epic 1 (Authentication & Onboarding)

**GitHub Issue:** [#246](https://github.com/vovkins/agents-react-native-experiment-2/issues/246)

---

## Приоритизация (MoSCoW)

| Приоритет | Milestone | Эпики | Описание |
|-----------|-----------|-------|----------|
| **P0 - Must Have** | MVP v1.0 | Epic 1, 2, 3, 4, 5 | Критически важные функции MVP |
| **P1 - Should Have** | - | - | Резерв для новых требований |
| **P2 - Should Have** | v1.1 | Epic 6, 7 | Улучшения UX и надежности |
| **P3 - Could Have** | v1.2 | Epic 8 | Желательные функции |
| **Won't Have** | - | - | За рамками текущей итерации |

---

## Roadmap по Milestone'ам

### MVP v1.0 (P0 - Must Have)
- Epic 1: Authentication & Onboarding
- Epic 2: Product Showcase
- Epic 3: Portfolio Dashboard
- Epic 4: Chat with Manager
- Epic 5: Navigation & App Structure

### v1.1 (P2 - Should Have)
- Epic 6: Data Synchronization & Offline Support
- Epic 7: Push Notifications

### v1.2 (P3 - Could Have)
- Epic 8: User Profile & Settings

---

## Out of Scope (не включено в MVP)

- Самостоятельная регистрация клиентов (вход только по приглашению)
- Подача заявок на подключение стратегий
- История транзакций с детализацией
- Отправка файлов в чате
- Интеграция с внешними банковскими системами

---

*Обновлено PM Agent*