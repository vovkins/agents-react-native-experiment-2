# Task Dependency Map

## Document Information
- **Product:** Мобильное приложение для клиентов управляющей компании
- **Technology:** React Native (iOS/Android)
- **Created:** 2026-04-13
- **Analyst:** Business Analyst Agent

---

## Quick Reference

| Task ID | Issue # | Depends On | Blocks | Can Parallel With |
|---------|---------|------------|--------|-------------------|
| TASK-APP-02 | #210 | None | All UI tasks | #209, #211 |
| TASK-APP-01 | #209 | None | All UI tasks | #210, #211 |
| TASK-APP-03 | #211 | None | None | #210, #209 |
| TASK-001-01 | #212 | #209, #210 | #214, #213, #215, #216, #218, #224, #221, #229, #230, #232 | None |
| TASK-001-02 | #214 | #212 | #227 | #213, #215, #216 |
| TASK-001-03 | #213 | #212 | None | #214, #215, #216 |
| TASK-001-04 | #215 | #212 | None | #214, #213, #216 |
| TASK-001-05 | #216 | #212 | None | #214, #213, #215 |
| TASK-002-01 | #218 | #212 | #217, #219 | #224, #221, #229, #230, #232 |
| TASK-002-02 | #217 | #218 | None | #223, #220, #222 |
| TASK-002-03 | #219 | #218 | None | #223, #220, #222, #217 |
| TASK-003-01 | #224 | #212 | #223, #220, #236 | #218, #221, #229, #230, #232 |
| TASK-003-02 | #223 | #224 | None | #220, #219, #217 |
| TASK-003-03 | #220 | #224 | None | #223, #219, #217 |
| TASK-004-01 | #221 | #212 | #222 | #218, #224, #229, #230, #232 |
| TASK-004-02 | #222 | #221 | #226, #225 | #217, #223, #220 |
| TASK-004-03 | #226 | #222 | None | #225, #228 |
| TASK-004-04 | #225 | #222 | None | #226, #228 |
| TASK-005-01 | #229 | #212 | #228 | #218, #224, #221, #230, #232 |
| TASK-005-02 | #228 | #229 | None | #226, #225, #231, #233 |
| TASK-006-01 | #227 | #214, #230 | None | #231 |
| TASK-007-01 | #230 | #212 | #231, #227 | #218, #224, #221, #229, #232 |
| TASK-007-02 | #231 | #230 | None | #226, #225, #228, #227 |
| TASK-008-01 | #232 | #212 | #233 | #218, #224, #221, #229, #230 |
| TASK-008-02 | #233 | #232 | None | #237, #235 |
| TASK-009-01 | #236 | #224 | #237 | #220, #223 |
| TASK-009-02 | #237 | #236 | None | #233, #235 |
| TASK-010-01 | #234 | None (optional: #212) | #235 | Any task |
| TASK-010-02 | #235 | #234 | None | #233, #237 |

---

## Dependency Levels (Wave Analysis)

Tasks are organized by their dependency depth - Wave 0 has no dependencies, Wave 1 depends only on Wave 0, etc.

### Wave 0: Foundation (No Dependencies)
```
┌─────────────────────────────────────────────────────────────────────┐
│  #210 Design System ──┐                                            │
│                       ├──► (All UI tasks)                          │
│  #209 Navigation ─────┘                                             │
│                                                                     │
│  #211 Error Handling ──► (Independent utility)                     │
│                                                                     │
│  #234 Articles/FAQ ─────► (Can start anytime, public content)       │
└─────────────────────────────────────────────────────────────────────┘
```

**Duration:** L + M + M + M = ~13 days
**Parallel Capacity:** All 4 tasks can run simultaneously

### Wave 1: Core Infrastructure
```
┌─────────────────────────────────────────────────────────────────────┐
│                        #212 Auth Infrastructure                      │
│                        (M - 2-3 days)                               │
│                              │                                       │
│        ┌─────────────────────┼─────────────────────┐               │
│        │                     │                     │                │
│        ▼                     ▼                     ▼                │
│  ┌──────────┐         ┌──────────┐         ┌──────────┐           │
│  │#218      │         │#224      │         │#221      │           │
│  │Products  │         │Portfolio │         │Chat UI   │           │
│  │List      │         │Overview  │         │          │           │
│  └──────────┘         └──────────┘         └──────────┘           │
│        │                     │                     │                │
│        │                     │                     │                │
│        ▼                     ▼                     ▼                │
│  ┌──────────┐         ┌──────────┐         ┌──────────┐           │
│  │#229      │         │#230      │         │#232      │           │
│  │Push      │         │Profile   │         │Docs List │           │
│  │Setup     │         │View      │         │          │           │
│  └──────────┘         └──────────┘         └──────────┘           │
│                                                                     │
│  Also in Wave 1:                                                   │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐         │
│  │#214      │  │#213      │  │#215      │  │#216      │         │
│  │Login     │  │Reg       │  │Recovery  │  │Timeout   │         │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘         │
└─────────────────────────────────────────────────────────────────────┘
```

**Duration:** M + max(M, M, M, S, M, M, M) = ~5-6 days
**Parallel Capacity:** Up to 8 tasks can run simultaneously after #212

### Wave 2: Feature Details
```
┌─────────────────────────────────────────────────────────────────────┐
│  From #218:                From #224:            From #221:         │
│  ┌──────────┐             ┌──────────┐         ┌──────────┐       │
│  │#217      │             │#223      │         │#222      │       │
│  │Product   │             │Structure │         │Chat API  │       │
│  │Detail    │             │Chart     │         │          │       │
│  └──────────┘             └──────────┘         └──────────┘       │
│        │                        │                     │            │
│        ▼                        ▼                     ▼            │
│  ┌──────────┐             ┌──────────┐         ┌──────────┐       │
│  │#219      │             │#220      │         │#236      │       │
│  │Products  │             │History   │         │Charts    │       │
│  │Offline   │             │          │         │          │       │
│  └──────────┘             └──────────┘         └──────────┘       │
│                                                                     │
│  From #229:                From #230:            From #232:        │
│  ┌──────────┐             ┌──────────┐         ┌──────────┐       │
│  │#228      │             │#231      │         │#233      │       │
│  │Push Nav  │             │Profile   │         │PDF View  │       │
│  │          │             │Edit      │         │          │       │
│  └──────────┘             └──────────┘         └──────────┘       │
│                                                                     │
│  From #234:                                                         │
│  ┌──────────┐                                                      │
│  │#235      │                                                      │
│  │Glossary  │                                                      │
│  └──────────┘                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

**Duration:** M + max(M, M, M, S, M, M, M) = ~5-6 days
**Parallel Capacity:** Up to 10 tasks can run simultaneously

### Wave 3: Advanced Features
```
┌─────────────────────────────────────────────────────────────────────┐
│  From #222:                From #214+#230:        From #236:        │
│  ┌──────────┐             ┌──────────┐         ┌──────────┐       │
│  │#226      │             │#227      │         │#237      │       │
│  │WebSocket │             │Biometry  │         │Benchmark │       │
│  └──────────┘             └──────────┘         └──────────┘       │
│        │                                                         │
│        ▼                                                         │
│  ┌──────────┐                                                    │
│  │#225      │                                                    │
│  │Offline   │                                                    │
│  │Queue     │                                                    │
│  └──────────┘                                                    │
└─────────────────────────────────────────────────────────────────────┘
```

**Duration:** M + M = ~5-6 days
**Parallel Capacity:** Up to 4 tasks can run simultaneously

---

## Critical Path

The critical path is the longest sequence of dependent tasks. Any delay on the critical path delays the entire project.

```
Critical Path #1 (Auth Flow):
#210 (L) → #209 (M) → #212 (M) → #214 (M) → #227 (S)
Duration: 5 + 3 + 3 + 3 + 2 = 16 days

Critical Path #2 (Chat Flow):
#210 (L) → #209 (M) → #212 (M) → #221 (M) → #222 (M) → #226 (M)
Duration: 5 + 3 + 3 + 3 + 3 + 3 = 20 days ⚠️ LONGEST

Critical Path #3 (Portfolio Analytics):
#210 (L) → #209 (M) → #212 (M) → #224 (M) → #236 (M) → #237 (M)
Duration: 5 + 3 + 3 + 3 + 3 + 3 = 20 days ⚠️ LONGEST

Critical Path #4 (Documents):
#210 (L) → #209 (M) → #212 (M) → #232 (M) → #233 (M)
Duration: 5 + 3 + 3 + 3 + 3 = 17 days
```

**⚠️ Critical Path Length: 20 days (4 weeks)**

---

## Blocking Tasks Analysis

### Tier 1 Blockers (Highest Impact)
These tasks block the most other tasks:

| Task | Issue # | Blocks Count | Blocked Tasks |
|------|---------|--------------|---------------|
| Design System | #210 | 26 | All UI tasks |
| Navigation | #209 | 26 | All UI tasks |
| Auth Infrastructure | #212 | 19 | All authenticated features |

### Tier 2 Blockers (Medium Impact)

| Task | Issue # | Blocks Count | Blocked Tasks |
|------|---------|--------------|---------------|
| Products List | #218 | 2 | #217, #219 |
| Portfolio Overview | #224 | 3 | #223, #220, #236 |
| Chat UI | #221 | 1 | #222 |
| Chat API | #222 | 2 | #226, #225 |
| Push Setup | #229 | 1 | #228 |
| Profile View | #230 | 2 | #231, #227 |
| Docs List | #232 | 1 | #233 |
| Charts | #236 | 1 | #237 |
| Articles | #234 | 1 | #235 |

### Non-Blocking Tasks
These tasks don't block any other tasks and can be scheduled flexibly:
- #211 Error Handling
- #213 Registration
- #215 Password Recovery
- #216 Session Timeout
- #217 Product Detail
- #219 Products Offline
- #223 Portfolio Structure
- #220 Portfolio History
- #226 Real-time Messaging
- #225 Chat Offline Queue
- #228 Push Navigation
- #227 Biometry
- #231 Profile Edit
- #233 PDF Viewer
- #237 Benchmark
- #235 Glossary

---

## Parallel Work Streams

### Stream A: Authentication Team (2 developers)
```
Week 1-2:
  #210 Design System (L)
  #209 Navigation (M)
  
Week 2-3:
  #212 Auth Infrastructure (M)
  
Week 3-4:
  #214 Login (M)        ─┐
  #213 Registration (M) ─┼─ Parallel
  #215 Recovery (M)     ─┤
  #216 Timeout (S)      ─┘
  
Week 4-5:
  #230 Profile View (S)
  #227 Biometry (S)
```

### Stream B: Products & Portfolio Team (2 developers)
```
Week 2-3:
  Wait for #212
  
Week 3-4:
  #218 Products List (M)  ─┐
  #224 Portfolio (M)      ─┼─ Parallel
  #232 Documents (M)      ─┘
  
Week 4-5:
  #217 Product Detail (M) ─┐
  #219 Products Offline(S) ─┼─ Parallel
  #223 Structure (M)       ─┤
  #220 History (M)         ─┤
  #233 PDF Viewer (M)      ─┘
  
Week 5-6:
  #236 Charts (M)
  #237 Benchmark (M)
```

### Stream C: Chat & Notifications Team (2 developers)
```
Week 2-3:
  Wait for #212
  
Week 3-4:
  #221 Chat UI (M)     ─┐
  #229 Push Setup (M)  ─┼─ Parallel
  #231 Profile Edit (M)─┘
  
Week 4-5:
  #222 Chat API (M)    ─┐
  #228 Push Nav (M)    ─┼─ Parallel
  #231 Profile Edit (M)─┘
  
Week 5-6:
  #226 WebSocket (M)   ─┐
  #225 Offline Queue(S)─┘
```

### Stream D: Content Team (1 developer)
```
Week 1-2:
  #234 Articles/FAQ (M)
  
Week 2-3:
  #235 Glossary (S)
  
Note: Can run independently of other streams
```

---

## Recommended Execution Order

### Sprint 1: Foundation (Week 1-2) 
**Team Size: 3 developers**

| Week | Day | Task | Size | Assignee |
|------|-----|------|------|----------|
| 1 | 1-5 | #210 Design System | L | Dev A |
| 1-2 | 1-3 | #209 Navigation | M | Dev B |
| 1-2 | 1-3 | #211 Error Handling | M | Dev C |
| 2 | 1-5 | #210 Design System (cont.) | - | Dev A |
| 2 | 4-6 | #234 Articles/FAQ | M | Dev B |
| 2 | 4-5 | (Prepare for Auth) | - | Dev C |

**Deliverables:** Design system, Navigation, Error handling, Articles

### Sprint 2: Core Auth (Week 2-3)
**Team Size: 3 developers**

| Week | Day | Task | Size | Assignee |
|------|-----|------|------|----------|
| 2-3 | 1-3 | #212 Auth Infrastructure | M | Dev A |
| 3 | 1-3 | #214 Login | M | Dev B |
| 3 | 1-3 | #213 Registration | M | Dev C |
| 3 | 4-5 | #215 Password Recovery | M | Dev A |
| 3 | 4-5 | #216 Session Timeout | S | Dev B |
| 3 | 4-6 | #235 Glossary | S | Dev C |

**Deliverables:** Complete authentication system

### Sprint 3: Core Features Start (Week 3-4)
**Team Size: 3 developers**

| Week | Day | Task | Size | Assignee |
|------|-----|------|------|----------|
| 3-4 | 1-3 | #218 Products List | M | Dev A |
| 3-4 | 1-3 | #224 Portfolio Overview | M | Dev B |
| 3-4 | 1-3 | #221 Chat UI | M | Dev C |
| 4 | 1-3 | #229 Push Setup | M | Dev A |
| 4 | 1-3 | #230 Profile View | S | Dev B |
| 4 | 1-3 | #232 Documents List | M | Dev C |

**Deliverables:** Main feature foundations

### Sprint 4: Feature Details (Week 4-5)
**Team Size: 3 developers**

| Week | Day | Task | Size | Assignee |
|------|-----|------|------|----------|
| 4-5 | 1-3 | #217 Product Detail | M | Dev A |
| 4-5 | 1-3 | #222 Chat API | M | Dev C |
| 4-5 | 1-3 | #223 Structure Chart | M | Dev B |
| 5 | 1-2 | #219 Products Offline | S | Dev A |
| 5 | 1-3 | #220 Portfolio History | M | Dev B |
| 5 | 1-3 | #236 Charts | M | Dev C |

**Deliverables:** Detailed feature implementations

### Sprint 5: MVP Completion (Week 5-6)
**Team Size: 3 developers**

| Week | Day | Task | Size | Assignee |
|------|-----|------|------|----------|
| 5-6 | 1-3 | #226 WebSocket | M | Dev C |
| 5-6 | 1-3 | #228 Push Navigation | M | Dev A |
| 5-6 | 1-3 | #237 Benchmark | M | Dev B |
| 6 | 1-2 | #225 Offline Queue | S | Dev C |
| 6 | 1-2 | #231 Profile Edit | M | Dev A |
| 6 | 1-2 | #233 PDF Viewer | M | Dev B |

**Deliverables:** MVP complete, all MUST HAVE features

### Sprint 6: Enhancement Features (Week 6-7)
**Team Size: 3 developers**

| Week | Day | Task | Size | Assignee |
|------|-----|------|------|----------|
| 6-7 | 1-2 | #227 Biometry | S | Dev A |
| 7 | 1-3 | Polish & Bug Fixes | - | All |
| 7 | 1-3 | Integration Testing | - | QA |

**Deliverables:** SHOULD HAVE features, polished MVP

---

## Dependency Matrix

```
                    ┌────────────────────────────────────────────────────────────┐
                    │                    D E P E N D E N C I E S                  │
                    │                                                            │
Task ID      Issue #│0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2│
                    │1 2 2 2 2 2 2 2 2 2 3 3 3 3 3 3 3 3 3 3 0 0 0 0 0 0 0 0 0 0│
                    │0 0 1 1 1 1 1 2 2 2 0 0 0 0 0 0 0 0 0 9 0 0 0 0 0 0 0 0 0 0│
                    │2 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7│
                    ├────────────────────────────────────────────────────────────┤
TASK-APP-02  #210   │● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-APP-01  #209   │○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-APP-03  #211   │○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-001-01  #212   │● ● ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-001-02  #214   │○ ○ ○ ● ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-001-03  #213   │○ ○ ○ ● ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-001-04  #215   │○ ○ ○ ● ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-001-05  #216   │○ ○ ○ ● ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-002-01  #218   │○ ○ ○ ● ○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-002-02  #217   │○ ○ ○ ○ ○ ○ ○ ○ ● ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-002-03  #219   │○ ○ ○ ○ ○ ○ ○ ○ ● ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-003-01  #224   │○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-003-02  #223   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-003-03  #220   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-004-01  #221   │○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-004-02  #222   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-004-03  #226   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-004-04  #225   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-005-01  #229   │○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-005-02  #228   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ● ○ ○ ○ ○ ○ ○ ○ ○ ○│
TASK-006-01  #227   │○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○│
TASK-007-01  #230   │○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○│
TASK-007-02  #231   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ● ○ ○ ○ ○ ○│
TASK-008-01  #232   │○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○ ○ ○│
TASK-008-02  #233   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ● ○ ○ ○ ○│
TASK-009-01  #236   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ○ ○ ○│
TASK-009-02  #237   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ● ● ○│
TASK-010-01  #234   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ●│
TASK-010-02  #235   │○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ●│
                    └────────────────────────────────────────────────────────────┘

Legend:
● = Dependency exists
○ = No dependency
```

---

## Risk Analysis

### High-Risk Dependencies

| Risk | Affected Tasks | Mitigation |
|------|----------------|------------|
| Design System delays | All 26 UI tasks | Start early, use temporary stubs |
| Auth Infrastructure delays | 19 dependent tasks | Prioritize, allocate senior dev |
| Backend API not ready | #212, #218, #224, #221, #229, #232 | Use mock APIs, contract testing |
| WebSocket complexity | #226 (on critical path) | Plan polling fallback |

### Circular Dependencies
**None identified** - The dependency graph is a DAG (Directed Acyclic Graph).

### Bottleneck Analysis

| Bottleneck | Reason | Solution |
|------------|--------|----------|
| Single Auth Infrastructure | Only one task provides this | Cannot parallelize, must prioritize |
| #210 + #209 blocking | Foundation must be complete | Start immediately, no waiting |
| Chat real-time complexity | Multiple dependencies | Can start UI early with mocks |

---

## External Dependencies

These are dependencies outside the codebase:

| Dependency | Required For | Owner | Status |
|------------|--------------|-------|--------|
| Backend Auth API | #212, #214, #213, #215 | Backend Team | ⚠️ Needs confirmation |
| Products API | #218, #217 | Backend Team | ⚠️ Needs confirmation |
| Portfolio API | #224, #220 | Backend Team | ⚠️ Needs confirmation |
| Chat API | #222, #226 | Backend Team | ⚠️ Needs confirmation |
| WebSocket Server | #226 | Backend Team | ⚠️ Needs confirmation |
| Push Certificates (iOS) | #229 | DevOps | ⚠️ Needs setup |
| Firebase Project (Android) | #229 | DevOps | ⚠️ Needs setup |
| Design Mockups | All UI tasks | Designer | ⚠️ Needs confirmation |

---

## Parallel Execution Opportunities

### Maximum Parallelism by Phase

| Phase | Max Parallel Tasks | Tasks |
|-------|-------------------|-------|
| Wave 0 | 4 | #210, #209, #211, #234 |
| Wave 1 | 8 | #214, #213, #215, #216, #218, #224, #221, #229, #230, #232 |
| Wave 2 | 10 | #217, #219, #223, #220, #222, #236, #228, #231, #233, #235 |
| Wave 3 | 4 | #226, #225, #227, #237 |

### Recommended Team Structure

For optimal velocity with maximum parallelism:

| Role | Count | Focus Area |
|------|-------|------------|
| Senior Developer | 1 | Infrastructure (#210, #209, #212) |
| Mid Developer | 2 | Core features (rotate between streams) |
| Junior Developer | 1 | Content, tests, documentation |

**Minimum Team:** 3 developers
**Optimal Team:** 4 developers
**Maximum Useful Team:** 5 developers (diminishing returns after)

---

## Timeline Summary

| Milestone | Week | Key Deliverables |
|-----------|------|------------------|
| Foundation Complete | 2 | Design system, Navigation, Error handling |
| Auth Complete | 3 | Full authentication system |
| MVP Core Started | 4 | Products, Portfolio, Chat foundations |
| MVP Complete | 6 | All MUST HAVE features working |
| Enhancement Complete | 7 | SHOULD HAVE features, polish |
| Full Release Ready | 8 | COULD HAVE features, final QA |

---

## Summary Statistics

| Metric | Value |
|--------|-------|
| Total Tasks | 29 |
| Independent Tasks (Wave 0) | 4 |
| Maximum Dependency Depth | 3 levels |
| Critical Path Length | 20 days |
| Parallel Tasks Maximum | 10 (Wave 2) |
| Blocking Tasks | 3 (high impact) |
| External Dependencies | 8 |

---

*Document created by Business Analyst Agent*
*Artifact type: dep-map*
