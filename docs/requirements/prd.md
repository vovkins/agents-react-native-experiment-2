# Product Backlog Prioritization

## Приоритизация Issues

### P0: Critical (Must Have for MVP) - Sprint 1-3

| Issue # | Feature | Story Points | Milestone | Rationale |
|---------|---------|--------------|-----------|-----------|
| #5 | Authentication & Security (MVP) | 8 | MVP - Sprint 1-2 | Критически важная функция. Без аутентификации пользователи не смогут получить доступ к приложению. Включает базовую безопасность для финансовых данных. |
| #7 | Product Showcase (Vitrina) | 13 | MVP - Sprint 2 | Основная фича приложения. Клиенты должны видеть доступные продукты для принятия инвестиционных решений. |
| #10 | Portfolio Overview & Details | 13 | MVP - Sprint 2 | Ключевая фича для мониторинга активов. Клиенты ожидают видеть свой портфель в реальном времени. |
| #21 | Chat with Personal Manager | 13 | MVP - Sprint 3 | Уникальное ценностное предложение. Персональный контакт с менеджером - главное преимущество управляющей компании. |
| #8 | User Profile | 5 | MVP - Sprint 3 | Базовый функционал для отображения данных клиента и документов. Необходим для доверия и прозрачности. |

**Total P0:** 52 Story Points | **Timeline:** Sprints 1-3 (6-9 weeks)

---

### P1: High Priority (Should Have) - Sprint 4-5

| Issue # | Feature | Story Points | Milestone | Rationale |
|---------|---------|--------------|-----------|-----------|
| #9 | Push Notifications | 8 | Phase 2 - Sprint 3-4 | Критично для вовлечённости пользователей. Уведомления о сообщениях важны для коммуникации с менеджером. |
| #6 | Two-Factor Authentication (2FA) | 5 | Phase 2 - Sprint 4 | Повышает безопасность для финансовых приложений. Важно для соответствия требованиям регулятора. |
| #4 | PIN Code for Quick Access | 3 | Phase 2 - Sprint 4 | Улучшает UX. Альтернатива биометрии для устройств без поддержки. |
| #11 | Transaction History | 8 | Phase 2 - Sprint 4 | Важно для прозрачности. Клиенты хотят видеть историю операций. |
| #12 | Portfolio Analytics | 8 | Phase 2 - Sprint 5 | Добавляет ценность для продвинутых пользователей. Показатели риска и сравнение с бенчмарком. |
| #13 | File Sharing in Chat | 5 | Phase 2 - Sprint 5 | Улучшает коммуникацию. Позволяет отправлять документы менеджеру. |
| #14 | Profile Editing | 5 | Phase 2 - Sprint 5 | Базовая функциональность для обновления контактных данных. |
| #15 | Notification Settings | 3 | Phase 2 - Sprint 4 | Даёт контроль пользователю над уведомлениями. |

**Total P1:** 45 Story Points | **Timeline:** Sprints 4-5 (4-6 weeks)

---

### P2: Medium Priority (Could Have) - Sprint 6-8

| Issue # | Feature | Story Points | Milestone | Rationale |
|---------|---------|--------------|-----------|-----------|
| #16 | Product Comparison | 8 | Phase 3 - Sprint 6 | Улучшает процесс принятия решений. Позволяет сравнивать стратегии. |
| #17 | Voice Messages in Chat | 5 | Phase 3 - Sprint 6 | Удобная функция, но не критична. Улучшает UX для мобильных пользователей. |
| #18 | Share to Chat | 3 | Phase 3 - Sprint 6 | Удобная функция для шаринга продуктов и активов в чат. |
| #19 | Chat Search | 5 | Phase 3 - Sprint 7 | Полезно для поиска в истории переписки. Становится важным при накоплении большого объёма сообщений. |
| #20 | English Localization | 13 | Phase 3 - Sprint 7-8 | Важно для международных клиентов, но требует значительных усилий на перевод и тестирование. |

**Total P2:** 34 Story Points | **Timeline:** Sprints 6-8 (6-9 weeks)

---

### P3: Low Priority (Nice to Have) - Future Releases

В настоящее время нет issues с приоритетом P3. Потенциальные кандидаты для P3 (не созданы как issues):

- Продвинутая аналитика с ИИ-рекомендациями
- Виджеты для домашнего экрана
- Интеграция с Apple Watch / Wear OS
- Офлайн-режим для полного функционала чата
- Многоязычная поддержка (кроме английского)

---

## Milestone Assignments

### Milestone 1: MVP Release (Sprint 1-3)
**Target Date:** Weeks 1-9  
**Goal:** Запуск минимально жизнеспособного продукта с основными функциями

**Issues:**
- #5: Authentication & Security (Sprint 1-2)
- #7: Product Showcase (Sprint 2)
- #10: Portfolio Overview & Details (Sprint 2)
- #21: Chat with Personal Manager (Sprint 3)
- #8: User Profile (Sprint 3)

**Deliverables:**
- Приложение опубликовано в App Store и Google Play
- Основные функции работают стабильно
- Базовая безопасность реализована
- Unit тесты покрывают 70% кода

**Success Criteria:**
- Crash-free rate ≥ 99%
- Время загрузки < 3 секунд
- Все Must Have функции протестированы

---

### Milestone 2: Enhanced Features (Sprint 4-5)
**Target Date:** Weeks 10-15  
**Goal:** Добавление важных улучшений безопасности и UX

**Issues:**
- #9: Push Notifications (Sprint 3-4)
- #6: Two-Factor Authentication (Sprint 4)
- #4: PIN Code for Quick Access (Sprint 4)
- #11: Transaction History (Sprint 4)
- #12: Portfolio Analytics (Sprint 5)
- #13: File Sharing in Chat (Sprint 5)
- #14: Profile Editing (Sprint 5)
- #15: Notification Settings (Sprint 4)

**Deliverables:**
- Улучшенная безопасность с 2FA
- Расширенный функционал портфеля
- Улучшенная коммуникация в чате
- Полный контроль над уведомлениями

---

### Milestone 3: Advanced Features (Sprint 6-8)
**Target Date:** Weeks 16-24  
**Goal:** Добавление продвинутых функций для улучшения UX

**Issues:**
- #16: Product Comparison (Sprint 6)
- #17: Voice Messages in Chat (Sprint 6)
- #18: Share to Chat (Sprint 6)
- #19: Chat Search (Sprint 7)
- #20: English Localization (Sprint 7-8)

**Deliverables:**
- Продвинутые функции сравнения продуктов
- Голосовые сообщения
- Английская локализация
- Поиск по истории чата

---

## Velocity Estimates

### Team Capacity
- **Sprint Duration:** 2 weeks
- **Team Size:** 2 frontend developers, 1 backend developer (part-time), 1 QA (part-time)
- **Average Velocity:** ~15-20 Story Points per sprint

### Timeline

| Phase | Sprints | Story Points | Duration | Target Completion |
|-------|---------|--------------|----------|-------------------|
| **MVP (P0)** | 3 sprints | 52 SP | 6 weeks | Week 6 |
| **Enhanced (P1)** | 2 sprints | 45 SP | 4 weeks | Week 10 |
| **Advanced (P2)** | 3 sprints | 34 SP | 6 weeks | Week 16 |
| **Total** | 8 sprints | 131 SP | 16 weeks | Week 16 |

**Note:** Оценки включают буфер на интеграцию с бэкендом и тестирование.

---

## Risk Mitigation for Priorities

### P0 Risks
1. **Бэкенд неготов**
   - Mitigation: Использовать мок-данные для разработки UI
   - Plan B: Отложить интеграцию на Sprint 3, использовать заглушки

2. **Сложности с биометрией на старых устройствах**
   - Mitigation: Тестирование на минимально поддерживаемых версиях OS
   - Plan B: Биометрия как опция, основной вход по паролю

### P1 Risks
1. **Push-уведомления на Android**
   - Mitigation: Раннее тестирование FCM, использование проверенных библиотек
   - Plan B: Сократить функционал до базовых уведомлений

2. **Производительность аналитики портфеля**
   - Mitigation: Оптимизация запросов, кэширование на клиенте
   - Plan B: Упрощённые графики, вычисления на сервере

### P2 Risks
1. **Качество локализации**
   - Mitigation: Профессиональный переводчик, тестирование носителями языка
   - Plan B: Отложить локализацию до накопления обратной связи от пользователей

---

## Priority Labels to Apply

### Label Structure
- `P0-critical` - Must have for MVP
- `P1-high` - Should have
- `P2-medium` - Could have
- `P3-low` - Nice to have

### Issues Mapping

**P0-critical (5 issues):**
- #5 - Authentication & Security (MVP)
- #7 - Product Showcase (Vitrina)
- #10 - Portfolio Overview & Details
- #21 - Chat with Personal Manager
- #8 - User Profile

**P1-high (8 issues):**
- #9 - Push Notifications
- #6 - Two-Factor Authentication (2FA)
- #4 - PIN Code for Quick Access
- #11 - Transaction History
- #12 - Portfolio Analytics
- #13 - File Sharing in Chat
- #14 - Profile Editing
- #15 - Notification Settings

**P2-medium (5 issues):**
- #16 - Product Comparison
- #17 - Voice Messages in Chat
- #18 - Share to Chat
- #19 - Chat Search
- #20 - English Localization

**P3-low (0 issues):**
- Нет issues с P3 приоритетом в текущем бэклоге

---

## Recommendations

### Critical Path for MVP
1. **Sprint 1:** Start with #5 (Authentication) - blocking issue for all other features
2. **Sprint 2:** Parallel development of #7 (Products) and #10 (Portfolio) - independent features
3. **Sprint 3:** Complete MVP with #21 (Chat) and #8 (Profile) - finalize core functionality

### Dependencies
- **#5 (Auth)** blocks all other issues - must be completed first
- **#21 (Chat)** depends on #9 (Push Notifications) for full functionality
- **#12 (Analytics)** depends on #10 (Portfolio) for data
- **#13 (File Sharing)** depends on #21 (Chat) infrastructure

### Quick Wins (Low Effort, High Impact)
- #8 (User Profile) - 5 SP, essential for MVP
- #15 (Notification Settings) - 3 SP, improves UX significantly
- #18 (Share to Chat) - 3 SP, enhances communication

---

**Document Version:** 1.0  
**Last Updated:** 2026-04-02  
**Author:** PM Agent