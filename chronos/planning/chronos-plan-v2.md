# Chronos - AI Task Management Platform

*Planning Document v2.0 - Enhanced Architecture & Execution Plan*  
*Updated: 2026-03-10*  
*Status: Strategy + Technical Plan Ready for Review*

---

## Executive Summary

**Chronos** is an AI-native planning and execution platform designed to beat Motion on intelligence and beat Akiflow on usability. The product thesis is simple:

- **Tasks should become plans automatically**
- **Calendars should adapt intelligently, not just display events**
- **Native apps should feel Apple-grade, not web wrappers**
- **AI should act like an operations copilot, not a chat gimmick**

Chronos should launch as a premium productivity system for ambitious individual professionals first, then expand into teams. The wedge is **AI scheduling + beautiful native experience + deep calendar/task interoperability**.

### Strategic Positioning

**Motion competitor:** stronger UX, clearer controls, lighter cognitive load  
**Akiflow competitor:** more intelligence, better automation, deeper planning engine  
**Native advantage:** true iPhone + Mac apps with fast capture, widgets, menu bar, offline support, and Apple ecosystem integrations

### Core Product Promise

> "Tell Chronos what matters. It turns that into an adaptive, realistic plan for your day and keeps it updated automatically."

---

## 1. Product Vision

Chronos is not just a task list, calendar, or assistant. It is a **decision-support and scheduling system** built around six capabilities:

1. **Capture** — turn messy user input, imported tasks, and incoming plan requests into structured work
2. **Prioritize** — score what matters based on urgency, strategic importance, effort, and context
3. **Schedule** — allocate realistic time blocks across available calendars, social constraints, and working hours
4. **Adapt** — replan when meetings change, tasks slip, collaborators respond, or the user’s priorities shift
5. **Coordinate** — help users find time with other people through availability-aware planning flows
6. **Learn** — personalize duration estimates, focus windows, and suggestion quality over time

The long-term moat is the **planning engine + behavioral personalization layer**, not generic LLM access.

---

## 2. Market Opportunity and Product Thesis

### Current Market Gaps

#### Motion
**What Motion gets right:**
- Automated scheduling
- Calendar + tasks in one place
- AI framing
- Strong appeal to busy professionals

**Where Motion leaves room:**
- UX can feel too algorithmic and heavy
- Limited sense of native delight
- Less transparent control over why plans were made
- Premium pricing creates room for a better value proposition

#### Akiflow
**What Akiflow gets right:**
- Fast capture
- Excellent command-bar workflow
- Good time-blocking ergonomics
- Focused product surface

**Where Akiflow leaves room:**
- Weak AI core
- Mostly manual intelligence
- Limited strategic planning features
- Native desktop experience still not a major differentiator

### Chronos Opportunity
Chronos should win by combining:
- **Akiflow-level speed for capture and inbox processing**
- **Motion-level auto-planning**
- **Better transparency and control than both**
- **Best-in-class native Apple ecosystem experience**
- **Practical AI workflows users trust**
- **A lightweight social planning layer competitors do not handle elegantly**

---

## 3. Product Scope by Capability

### 3.1 Core Task Management
- Natural language task capture
- Structured task fields and constraints
- Hierarchical projects / subprojects
- Priority and energy metadata
- Recurrence rules
- Time estimates and confidence ranges
- Manual and AI-assisted planning
- Task history and audit trail
- Tags, contexts, areas, and labels

### 3.2 Calendar Intelligence
- Unified multi-calendar support
- Two-way sync with Google and Microsoft first
- Read/write Apple Calendar support via EventKit on native devices and CalDAV/iCloud later if needed
- Conflict detection
- Buffer time and travel time support
- Hard vs soft commitments
- Schedule protection for deep work
- Busy/free availability sharing for social planning without exposing event details
- Distinction between fixed scheduled events and movable flexible events

### 3.3 AI Planning Engine
- Auto-prioritization
- Auto-scheduling
- Replanning after disruptions
- Suggested task breakdowns
- Deadline risk detection
- Meeting follow-up extraction
- Daily planning assistant
- End-of-day rescheduling / shutdown ritual

### 3.4 Native Experience
- iPhone capture, review, and planning
- Mac menu bar quick entry and command bar
- Widgets, live activities, notifications
- Offline-first caches
- Siri/App Intents shortcuts
- Handoff and continuity across Apple devices

### 3.5 Smart Inbox and Intake System
- Unified inbox for raw tasks, imported items, plan requests, and AI suggestions
- Auto-received tasks from email, meetings, docs, integrations, and API sources
- Akiflow-style inbox-zero workflow with review, approve, snooze, convert, or archive actions
- AI-assisted parsing, categorization, and auto-scheduling recommendations
- One-click approve or adjust for AI-proposed schedule placements
- Distinct inbox states for "needs review," "scheduled draft," "waiting on others," and "done"

### 3.6 Flexible Event and Task Types
Chronos should explicitly model **how movable an item is**, because scheduling quality depends on knowing what the AI is allowed to change.

Core event/task types:
- **Scheduled Event** — fixed commitment; cannot move automatically
- **Flexible Event** — exists at a planned time, but can move if needed; user would prefer it stay where it is
- **Flexible Task** — AI can reschedule freely inside constraints

This classification becomes a first-class planning signal used by the scheduler, UI, and explanations. It helps the AI distinguish between:
- truly immovable meetings
- soft personal commitments
- work blocks or tasks that can be rearranged safely

### 3.7 Social Planning Features
Chronos should support lightweight person-to-person planning before expanding into full team collaboration.

Initial social planning capabilities:
- Friend request / connection system so users can **invite friends to plan something**
- Availability sharing that exposes only **busy/free windows**, not sensitive calendar details
- Inbox items for incoming plan requests
- Flows to accept, adjust, or suggest an alternative time
- Shared planning proposals for events like dinner, workouts, coffee, study sessions, or travel coordination

This gives Chronos a differentiated use case beyond solo productivity: helping people find time together without the friction of manual back-and-forth.

### 3.8 User Control and Scheduling Preferences
Chronos should feel intelligent **without feeling authoritarian**. Users need clear policy controls that shape what the AI is allowed to do.

Required control settings include:
- Work hours and scheduling windows
- Hard deadlines vs soft deadlines
- Energy level preferences by time of day or task type
- Focus time protection
- Maximum tasks per day
- Buffer time between events
- Rules for when the AI can auto-schedule vs when it must ask first

### 3.9 Collaboration (Phase 2+)
- Shared workspaces
- Shared calendars and visibility rules
- Assignee workflows
- Team planning suggestions
- Meeting action item coordination

---

## 4. Recommended Technical Architecture

## 4.1 Architecture Principles

1. **API-first backend** so web and native apps share a consistent domain model
2. **Event-driven internal design** for sync, scheduling, notifications, and AI jobs
3. **Relational core** because tasks, calendars, recurrence, dependencies, and audit logs are highly structured
4. **LLM-assisted, rules-constrained planning** rather than pure LLM autonomy
5. **User policy controls as first-class constraints** so scheduling behavior remains predictable
6. **Offline-capable clients** with optimistic updates and sync reconciliation
7. **Modular AI services** so models can be swapped based on cost and quality

## 4.2 Recommended Stack

### Frontend Web
- **Framework:** Next.js 15 + TypeScript
- **UI:** React + Tailwind CSS + shadcn/ui primitives + custom design system
- **State:** TanStack Query + Zustand
- **Calendar UI:** FullCalendar for web MVP, gradually replaced with custom timeline/calendar views where differentiation matters
- **Command Bar:** cmdk
- **Forms:** React Hook Form + Zod
- **Auth Client:** Clerk or Auth.js depending on final auth strategy

**Why this stack:** Next.js accelerates app shell, auth, API integration, and deployability. It is mature, recruiter-friendly, and easy to scale with strong developer velocity.

### Native Apple Apps
- **Language:** Swift
- **UI:** SwiftUI first
- **Mac-specific extensions:** AppKit bridging only where needed for menu bar, keyboard behavior, multi-window management, and advanced drag/drop
- **Data layer:** SwiftData or Core Data wrapper for local cache; recommendation: **SQLite via GRDB** for explicit control and sync conflict handling
- **Calendar access:** EventKit
- **Notifications:** UserNotifications framework
- **Shortcuts/Siri:** App Intents
- **Widgets:** WidgetKit
- **Sync transport:** REST + WebSocket/SSE fallback

**Recommendation:** Use **shared business logic patterns**, not cross-platform UI frameworks. For Chronos, native feel is part of the product moat.

### Backend / API
- **Primary runtime:** TypeScript on Node.js
- **Framework:** NestJS
- **API style:** REST for core resources, background webhooks, limited GraphQL optional later if needed for complex clients
- **Validation:** Zod / class-validator
- **Auth:** Clerk or Auth0 for fastest secure launch; if cost-sensitive and wanting full control, Supabase Auth is viable
- **Background jobs:** Temporal or BullMQ
  - **Recommendation:** start with **BullMQ + Redis**, upgrade to **Temporal** if workflow complexity explodes
- **Realtime:** WebSockets via NestJS gateway or Postgres logical event fanout; start with **Pusher/Ably** or native WebSocket infrastructure

### Database
- **Primary DB:** PostgreSQL 16
- **ORM:** Prisma
- **Cache / queue:** Redis
- **Search:** Postgres full-text initially, optional Meilisearch/OpenSearch later
- **Blob/document storage:** S3-compatible object storage (AWS S3, Cloudflare R2)
- **Analytics warehouse:** PostHog + ClickHouse or BigQuery later

**Why PostgreSQL:** recurring schedules, task relations, user preferences, audit trails, and sync metadata belong in a relational system. Postgres also supports JSONB where flexibility is needed.

### Infrastructure / DevOps
- **Cloud:** AWS recommended for long-term flexibility; Vercel acceptable for web frontend only
- **Containerization:** Docker
- **Orchestration:** ECS Fargate initially, Kubernetes only after proven scale
- **CDN / edge:** Cloudflare
- **Monitoring:** Sentry + Datadog or Grafana stack
- **Product analytics:** PostHog
- **CI/CD:** GitHub Actions
- **Secrets:** AWS Secrets Manager / Doppler / 1Password Secrets Automation

### AI / ML Stack
- **LLM orchestration:** custom service layer, not LangChain-heavy by default
- **Primary reasoning model:** GPT-5.4 or Claude Sonnet class depending on cost/quality tradeoff
- **Fast extraction model:** smaller model for parsing and classification tasks
- **Embeddings:** OpenAI text-embedding model or Voyage AI
- **Vector store:** pgvector in PostgreSQL initially
- **Transcription:** Whisper or Deepgram
- **Meeting intelligence:** LLM + diarization/transcription pipeline

---

## 5. System Architecture Overview

## 5.1 Core Services

### 1. Identity & Account Service
Handles:
- user accounts
- org/workspace memberships
- auth sessions
- connected integrations
- subscription entitlements

### 2. Task Domain Service
Handles:
- tasks
- projects
- subtasks
- recurrence
- dependencies
- event/task flexibility types
- tags/contexts
- task events/history

### 3. Calendar Sync Service
Handles:
- calendar account connections
- calendar sync cursors/tokens
- event import/export
- conflict detection
- availability snapshots
- shareable busy/free availability views for social planning

### 4. Scheduling Engine
Handles:
- ranking unscheduled tasks
- slot generation
- constraints evaluation
- block allocation
- re-planning events
- movable vs fixed item handling
- optimization scoring

### 5. AI Orchestration Service
Handles:
- NL parsing
- prioritization rationale
- task decomposition
- daily planning summaries
- meeting note extraction
- risk alerts
- inbox auto-scheduling suggestions
- prompt templates and guardrails

### 6. Social Planning Service
Handles:
- friend connections and plan invitations
- inbound/outbound planning requests
- shared availability negotiation
- accept / adjust / suggest-alternative flows
- privacy-safe busy/free sharing

### 7. Notification Service
Handles:
- push notifications
- reminder emails
- daily planning prompts
- schedule change alerts
- plan request alerts
- digest generation

### 8. Analytics & Learning Service
Handles:
- behavioral telemetry
- completion times
- schedule adherence
- suggestion acceptance rates
- personalization features

---

## 5.2 High-Level Data Flow

### Example: Natural Language Task Capture
1. User enters: "Finish deck by Friday, needs 3 hours, review with Sarah Thursday afternoon"
2. Client sends raw capture text or imported item to `/v1/inbox/parse`
3. AI parsing service extracts:
   - title
   - deadline
   - estimated duration
   - stakeholder
   - prep/review step suggestions
4. Backend stores task draft + parse confidence
5. User confirms or edits
6. Task is promoted to active task
7. Scheduling engine evaluates open availability and proposes blocks

### Example: Auto Replanning
1. Calendar sync receives new meeting or delayed meeting event
2. Affected planned task blocks are marked disrupted
3. Scheduling engine recalculates feasible slots
4. AI layer produces explanation: "Moved deep work block to 3:00 PM because your 1:00 PM meeting ran over and the task needs a 90-minute uninterrupted window"
5. User gets a push notification or sees updated timeline

### Example: Social Planning Request
1. User taps "Invite friends to plan something" and selects a few connections
2. Chronos creates a plan request with rough intent, duration, and optional date range
3. Recipients receive an inbox item and can accept, adjust, or suggest an alternative
4. Calendar service shares only busy/free windows based on privacy rules
5. Scheduler proposes candidate times that respect both users' constraints
6. Once confirmed, the plan becomes a calendar event or flexible shared placeholder


---

## 6. Detailed Data Model

## 6.1 Core Entities

Below is the recommended relational model. IDs should be UUIDv7 where possible for sortability.

### users
- id (pk)
- email
- name
- timezone
- locale
- avatar_url
- onboarding_state
- created_at
- updated_at
- deleted_at

### workspaces
- id (pk)
- name
- slug
- plan_tier
- owner_user_id
- created_at
- updated_at

### workspace_members
- id (pk)
- workspace_id (fk)
- user_id (fk)
- role (`owner`, `admin`, `member`, `viewer`)
- created_at

### user_preferences
- id (pk)
- user_id (fk)
- working_hours_json
- energy_profile_json
- focus_protection_json
- max_tasks_per_day
- default_buffer_minutes
- default_task_duration_minutes
- scheduling_preferences_json
- notification_preferences_json
- theme
- created_at
- updated_at

### calendar_accounts
- id (pk)
- user_id (fk)
- provider (`google`, `microsoft`, `apple`, `caldav`)
- provider_account_id
- email
- access_token_encrypted
- refresh_token_encrypted
- token_expires_at
- scopes_json
- sync_status
- last_synced_at
- created_at
- updated_at

### calendars
- id (pk)
- calendar_account_id (fk)
- provider_calendar_id
- name
- color
- is_primary
- is_read_only
- timezone
- sync_token
- created_at
- updated_at

### calendar_events
- id (pk)
- calendar_id (fk)
- provider_event_id
- title
- description
- location
- starts_at
- ends_at
- is_all_day
- status
- event_flexibility_type (`scheduled_event`, `flexible_event`)
- attendees_json
- recurrence_rule
- last_provider_updated_at
- created_at
- updated_at

### projects
- id (pk)
- workspace_id (fk)
- parent_project_id (nullable fk)
- owner_user_id (fk)
- name
- description
- color
- status
- due_at
- created_at
- updated_at

### tasks
- id (pk)
- workspace_id (fk)
- project_id (nullable fk)
- parent_task_id (nullable fk)
- creator_user_id (fk)
- assignee_user_id (nullable fk)
- source (`manual`, `email`, `meeting`, `doc`, `api`, `ai_parse`)
- title
- description
- status (`inbox`, `todo`, `scheduled`, `in_progress`, `blocked`, `done`, `archived`)
- priority_manual (1-5 nullable)
- priority_ai_score (decimal)
- urgency_score (decimal)
- importance_score (decimal)
- effort_score (decimal)
- confidence_score (decimal)
- estimated_duration_minutes
- actual_duration_minutes
- earliest_start_at
- due_at
- do_date
- hard_deadline boolean
- energy_required (`low`, `medium`, `high`)
- scheduling_flexibility (`scheduled_event`, `flexible_event`, `flexible_task`, `must_schedule_today`, `someday`)
- scheduling_autonomy_level (`manual_only`, `suggest_only`, `auto_schedule`)
- recurrence_rule
- is_focus_block_required boolean
- preferred_time_windows_json
- tags_json or normalized task_tags table
- external_ref_json
- created_at
- updated_at
- completed_at
- deleted_at

### task_dependencies
- id (pk)
- task_id (fk)
- depends_on_task_id (fk)
- dependency_type (`blocks`, `relates_to`, `duplicates`)
- created_at

### task_blocks
Represents planned calendar allocations for tasks.
- id (pk)
- task_id (fk)
- user_id (fk)
- calendar_event_id (nullable fk)
- block_type (`planned`, `focus`, `break`, `travel`, `buffer`)
- starts_at
- ends_at
- duration_minutes
- schedule_confidence
- locked_by_user boolean
- generated_by (`user`, `scheduler`, `ai_replan`)
- disruption_status (`none`, `conflicted`, `moved`, `cancelled`)
- created_at
- updated_at

### task_events
Audit log of task changes.
- id (pk)
- task_id (fk)
- actor_type (`user`, `system`, `ai`, `integration`)
- actor_id
- event_type
- old_value_json
- new_value_json
- metadata_json
- created_at

### inbox_items
For unprocessed input.
- id (pk)
- user_id (fk)
- source (`quick_add`, `email`, `meeting`, `voice`, `import`, `integration`, `social_request`, `ai_suggestion`)
- inbox_type (`capture`, `imported_task`, `plan_request`, `schedule_suggestion`, `approval_request`)
- raw_content
- parsed_content_json
- parse_status
- confidence_score
- approval_state (`pending`, `approved`, `adjusted`, `rejected`, `archived`)
- task_id (nullable fk)
- created_at
- updated_at

### meetings
- id (pk)
- workspace_id (fk)
- calendar_event_id (nullable fk)
- title
- provider_meeting_id
- transcript_status
- summary_text
- action_items_json
- recording_url
- created_at
- updated_at

### friend_connections
- id (pk)
- requester_user_id (fk)
- addressee_user_id (fk)
- status (`pending`, `accepted`, `declined`, `blocked`)
- created_at
- updated_at

### social_plan_requests
- id (pk)
- creator_user_id (fk)
- recipient_user_id (fk)
- title
- description
- duration_minutes
- date_range_start
- date_range_end
- status (`pending`, `accepted`, `adjusting`, `suggested_alternative`, `confirmed`, `declined`, `expired`)
- visibility_mode (`busy_free_only`, `limited_details`)
- selected_slot_json
- created_at
- updated_at

### availability_shares
- id (pk)
- owner_user_id (fk)
- viewer_user_id (fk)
- share_type (`busy_free`, `custom_window`)
- rules_json
- expires_at
- created_at
- updated_at

### documents
- id (pk)
- workspace_id (fk)
- owner_user_id (fk)
- title
- content_json
- source
- created_at
- updated_at

### ai_runs
Auditability for AI actions.
- id (pk)
- user_id (fk)
- workspace_id (nullable fk)
- run_type (`parse`, `prioritize`, `schedule`, `summarize`, `extract_actions`)
- model_name
- prompt_version
- input_hash
- output_json
- token_usage_json
- latency_ms
- success boolean
- created_at

### subscriptions
- id (pk)
- workspace_id (fk)
- billing_provider
- plan_code
- status
- trial_ends_at
- renewal_at
- seats
- mrr_amount
- created_at
- updated_at

---

## 6.2 Notes on Schema Design

### Normalize Where It Matters
Use normalized tables for:
- tasks
- projects
- task blocks
- dependencies
- memberships
- social plan requests
- friend connections
- subscriptions

Use JSONB for:
- AI outputs
- user scheduling preferences
- provider metadata
- parse confidence detail
- analytics snapshots

### Why This Matters
Chronos will need:
- analytics on scheduling performance
- auditability for AI actions
- conflict resolution
- sync reconciliation with external calendars
- data portability for enterprise later

A loose NoSQL-first model would become painful quickly.

---

## 7. Scheduling Engine Design

This is the actual moat.

## 7.1 Planning Inputs
The scheduler should consider:
- task duration
- priority score
- urgency and due date proximity
- user-defined priority overrides
- dependencies
- calendar availability
- meeting density
- preferred work hours
- preferred focus windows
- energy profile by time of day
- task type/context
- required uninterrupted time
- historical actual duration vs estimate
- protected personal time
- maximum tasks per day
- buffer time requirements
- hard vs soft deadline policy
- movable vs fixed classification for every scheduled item
- calendar-specific constraints

## 7.2 Scheduling Strategy
Use a **hybrid deterministic + AI-assisted approach**:

### Deterministic layer
Responsible for:
- time slot search
- conflict detection
- recurrence expansion
- dependency enforcement
- hard deadline feasibility checks
- fixed vs flexible item enforcement
- user preference and policy enforcement
- optimization scoring

### AI layer
Responsible for:
- interpreting ambiguous task inputs
- generating rationale/explanations
- recommending task decomposition
- adjusting scoring when context is ambiguous
- proposing fallback strategies when schedule is overloaded
- selecting optimal timing for inbox items before user approval

### Recommendation
Do **not** let the LLM directly own final calendar placement decisions. The LLM can suggest, but the scheduling engine should enforce constraints deterministically.

## 7.3 Scheduling Algorithm (MVP)
1. Gather unscheduled and disrupted tasks
2. Filter by planning window (today, 3 days, week)
3. Compute weighted score per task:
   - urgency
   - importance
   - flexibility
   - expected effort
   - risk of missing due date
   - user override
   - energy fit
4. Generate feasible slots from availability map
5. Exclude immovable scheduled events and penalize movement of flexible events
6. Match tasks to slots using heuristic optimization
7. Reserve best-fit blocks
8. Surface rationale, approval options, and alternatives

## 7.4 Optimization Technique
For MVP:
- Weighted heuristic + greedy fit + limited backtracking

For later versions:
- Constraint solver / integer programming for advanced team scheduling
- Behavioral prediction model for duration accuracy
- Reinforcement loop on suggestion acceptance

---

## 8. AI/ML Implementation Approach

## 8.1 AI Jobs That Actually Matter
Chronos should focus AI on high-value tasks:

1. **Natural language parsing**
2. **Task prioritization explanation**
3. **Task decomposition into subtasks**
4. **Schedule rationale generation**
5. **Meeting action-item extraction**
6. **Deadline risk warnings**
7. **Daily planning summary and review**
8. **Inbox auto-scheduling suggestions**
9. **Social planning slot proposals**
10. **Personalization insights**

## 8.2 AI Architecture Pattern
Use a **task-oriented AI service** with strict contracts.

### Example internal modules
- `TaskParserAgent`
- `PriorityScorerAgent`
- `ScheduleRationaleAgent`
- `MeetingNotesAgent`
- `TaskBreakdownAgent`
- `DailyReviewAgent`
- `InboxTriageAgent`
- `SocialPlanProposalAgent`

Each module should:
- accept structured inputs
- use versioned prompts
- return validated JSON schemas
- log model, prompt version, and confidence
- fail safely into deterministic fallback behavior

## 8.3 Prompt Engineering Approach

### Design Principles
1. **JSON-only structured outputs** for operational tasks
2. **System prompts define role + constraints clearly**
3. **Few-shot examples for ambiguous date/time and duration extraction**
4. **Prompt versioning** stored in code/config
5. **Guardrails against overcommitting or hallucinating schedule facts**

### Example: Task Parsing Prompt Strategy
**Goal:** convert free text into a structured task draft.

**System instructions should force:**
- no invented dates
- confidence scoring
- extraction of ambiguity flags
- proposal of missing fields, not fabricated values
- normalized durations and deadlines

**Expected output schema:**
- title
- description
- estimated_duration_minutes
- due_at
- earliest_start_at
- tags
- project_guess
- stakeholders
- recurrence_rule
- ambiguity_flags[]
- confidence_score

### Example: Prioritization Prompt Strategy
Input includes:
- task metadata
- upcoming calendar load
- overdue tasks
- project context
- user preference profile

Output includes:
- importance score explanation
- urgency score explanation
- recommended action (`schedule_now`, `defer`, `break_down`, `clarify`)
- narrative rationale for UI

### Example: Daily Planning Assistant Prompt
The AI should produce:
- top 3 priorities
- hidden risks
- overloaded time windows
- suggested schedule changes
- short human-readable daily briefing

Tone should be concise and practical, not motivational fluff.

## 8.4 Personalization / ML Roadmap

### MVP Personalization
Rules + simple statistics:
- actual vs estimated duration by task type
- preferred completion windows
- snooze frequency
- schedule acceptance rate
- preferred block size

### V2 Personalization
Supervised models for:
- duration prediction
- schedule acceptance likelihood
- overdue risk prediction
- ideal time-of-day recommendations

### V3 Personalization
Context-aware recommendations using:
- embeddings of task descriptions
- work pattern clustering
- project/category-specific estimates

**Recommendation:** start with analytics-driven heuristics. Do not overbuild custom ML before enough behavioral data exists.

---

## 9. API Design

Chronos should use clean REST APIs with strong versioning.

Base path: `/v1`

## 9.1 Auth & Account
- `POST /v1/auth/session`
- `POST /v1/auth/logout`
- `GET /v1/me`
- `PATCH /v1/me/preferences`
- `GET /v1/me/entitlements`

## 9.2 Inbox & Parsing
- `POST /v1/inbox/items`
  - create inbox item from raw text, email, voice, import, or integration
- `GET /v1/inbox/items`
- `POST /v1/inbox/parse`
  - parse raw text into structured draft
- `POST /v1/inbox/items/:id/confirm`
  - convert parsed item into task/project
- `POST /v1/inbox/items/:id/approve-schedule`
- `POST /v1/inbox/items/:id/adjust-schedule`
- `POST /v1/inbox/items/:id/archive`

## 9.3 Tasks
- `GET /v1/tasks`
  - filters: status, due_before, due_after, project_id, assignee, tag, scheduled
- `POST /v1/tasks`
- `GET /v1/tasks/:id`
- `PATCH /v1/tasks/:id`
- `DELETE /v1/tasks/:id`
- `POST /v1/tasks/:id/complete`
- `POST /v1/tasks/:id/reopen`
- `POST /v1/tasks/:id/breakdown`
  - AI-generated subtasks
- `POST /v1/tasks/:id/prioritize`
  - returns updated priority reasoning
- `GET /v1/tasks/:id/history`
- `POST /v1/tasks/bulk-update`

## 9.4 Projects
- `GET /v1/projects`
- `POST /v1/projects`
- `GET /v1/projects/:id`
- `PATCH /v1/projects/:id`
- `DELETE /v1/projects/:id`
- `GET /v1/projects/:id/tasks`

## 9.5 Scheduling
- `POST /v1/schedule/plan`
  - generate schedule for a date range
- `POST /v1/schedule/replan`
  - replan after disruption
- `GET /v1/schedule/blocks`
- `PATCH /v1/schedule/blocks/:id`
  - move, resize, lock, unlock
- `POST /v1/schedule/blocks/:id/commit`
  - write planned block into calendar provider if applicable
- `POST /v1/schedule/simulate`
  - what-if planning output without committing
- `PATCH /v1/schedule/preferences`
  - update work hours, buffers, max task load, and automation rules

## 9.6 Calendar Integrations
- `POST /v1/integrations/google/connect`
- `POST /v1/integrations/microsoft/connect`
- `POST /v1/integrations/apple/connect`
- `GET /v1/calendars`
- `GET /v1/calendars/events`
- `POST /v1/calendars/events`
- `PATCH /v1/calendars/events/:id`
- `POST /v1/calendars/sync`
- `GET /v1/calendars/sync/status`
- `POST /v1/availability/share`
- `GET /v1/availability/share/:id`

## 9.7 Social Planning
- `POST /v1/friends/requests`
- `POST /v1/friends/requests/:id/accept`
- `POST /v1/friends/requests/:id/decline`
- `GET /v1/friends`
- `POST /v1/social-plans`
- `GET /v1/social-plans`
- `POST /v1/social-plans/:id/accept`
- `POST /v1/social-plans/:id/adjust`
- `POST /v1/social-plans/:id/suggest-alternative`
- `POST /v1/social-plans/:id/confirm`

## 9.8 Meetings
- `POST /v1/meetings/import`
- `GET /v1/meetings`
- `GET /v1/meetings/:id`
- `POST /v1/meetings/:id/transcribe`
- `POST /v1/meetings/:id/extract-actions`
- `POST /v1/meetings/:id/create-tasks`

## 9.9 Documents
- `GET /v1/documents`
- `POST /v1/documents`
- `GET /v1/documents/:id`
- `PATCH /v1/documents/:id`
- `POST /v1/documents/:id/extract-tasks`

## 9.10 Notifications
- `GET /v1/notifications`
- `PATCH /v1/notifications/:id/read`
- `PATCH /v1/me/notification-preferences`

## 9.11 Billing
- `GET /v1/billing/subscription`
- `POST /v1/billing/checkout`
- `POST /v1/billing/portal`
- `POST /v1/webhooks/stripe`

## 9.12 Admin / Observability
- `GET /v1/admin/ai-runs`
- `GET /v1/admin/sync-health`
- `GET /v1/admin/scheduler-health`

## 9.13 Realtime Events
WebSocket channels or SSE topics:
- `task.updated`
- `schedule.updated`
- `calendar.sync.completed`
- `notification.created`
- `meeting.processed`
- `social_plan.updated`
- `inbox.item.requires_review`

---

## 10. Native App Architecture - iPhone + Mac

This is a major differentiator and should be treated as product core, not accessory.

## 10.1 Shared Native Principles
- SwiftUI-first UI architecture
- Local persistence for offline use
- Fast launch and instant capture
- Sync engine with background refresh
- Design language aligned to Apple HIG but more futuristic/premium

## 10.2 iPhone App Architecture

### Recommended modules
- **Capture Module**
  - quick add
  - voice capture
  - natural language parsing
- **Today Module**
  - top priorities
  - scheduled blocks
  - focus mode
- **Calendar Module**
  - day/week views
  - drag-to-reschedule
- **Inbox Module**
  - review and confirm parsed items
  - approve or adjust AI-scheduled inbox tasks
  - manage incoming social plan requests
- **Notifications Module**
  - reminders
  - disruptions
  - AI daily plan prompts
- **Settings / Integrations Module**

### iOS Tech Design
- SwiftUI navigation stack
- BackgroundTasks for sync windows
- WidgetKit for Today widget + next block widget
- Live Activities for active focus block/timer
- App Intents for Siri shortcuts such as:
  - “Add task in Chronos”
  - “Plan my day in Chronos”
  - “What’s next in Chronos?”
- EventKit bridge for Apple calendar read/write when permission granted

### iPhone UX Differentiators
- One-tap quick capture from lock screen/widget
- Swipe gestures for defer, schedule, complete, approve, or adjust
- Smart daily briefing card each morning
- Elegant timeline with AI suggestions embedded inline
- Lightweight social planning request handling from mobile inbox

## 10.3 Mac App Architecture

### Recommended modules
- **Main Window**
  - full calendar + task planning board
- **Command Center**
  - universal quick-add and navigation palette
  - friend invite and social planning launcher
- **Menu Bar App**
  - instant capture
  - next task
  - focus timer
- **Mini Planner Window**
  - compact daily overview
- **Deep Work Mode**
  - distraction-reduced planning workspace

### Mac Tech Design
- SwiftUI app lifecycle
- MenuBarExtra for quick access
- NSWindow customizations through AppKit where needed
- Spotlight/App Intents integration
- Drag/drop between task list and planning timeline
- Local keyboard shortcut manager

### Mac UX Differentiators
- Blazing-fast command palette
- Keyboard-first scheduling
- Desktop notifications with actionable replanning
- Native split-pane planning experience better than web competitors
- Fast inbox-zero workflow for imported tasks and AI recommendations

## 10.4 Shared Sync Model
Use a client repository pattern:
- local write first
- queued outbound sync actions
- server reconciliation on reconnect
- conflict policy:
  - user explicit edits win over AI suggestions
  - latest confirmed provider sync wins over stale local mirror
  - conflicting edits create review state, not silent overwrite

---


## 10.5 Key Product Differentiators Added in This Revision

### Smart Inbox as the Operational Front Door
Chronos should treat the inbox as more than a dumping ground. It should be the central operating queue where raw inputs become approved plans. Imported tasks, AI suggestions, and social requests all land in a single review system, allowing users to work toward inbox zero instead of juggling disconnected capture surfaces.

### Flexibility Types as a Core Scheduling Primitive
Most task apps treat all blocks as roughly equal. Chronos should not. The distinction between **Scheduled Event**, **Flexible Event**, and **Flexible Task** should sit at the heart of the planner so the AI understands what is immovable, what is movable with friction, and what can be freely optimized. This improves both trust and schedule quality.

### User-Controlled Automation
The product should market AI automation as **user-shaped**, not fully autonomous. Work hours, focus protection, energy preferences, hard vs soft deadlines, and daily task limits should all be visible settings that directly govern scheduling behavior. This becomes both a UX trust feature and a technical design principle.

### Social Planning as a Differentiated Expansion Path
Rather than jumping straight from solo productivity to enterprise collaboration, Chronos can open a middle lane: helping individuals coordinate with friends, partners, and peers. That creates a more consumer-friendly growth loop while still supporting a later move into team features.

## 11. Security, Privacy, and Compliance

Chronos will handle calendar data, meeting content, user routines, social availability, and potentially sensitive work tasks. Security posture needs to be credible from day one.

## 11.1 Security Principles
1. Least privilege for integrations
2. Encryption in transit and at rest
3. Tenant isolation for all workspace data
4. Strong auditability of AI actions
5. No silent AI actions on external calendars without user-configured rules
6. Clear consent flows for recording/transcription features

## 11.2 Authentication & Authorization
- OAuth 2.0 / OIDC for sign-in and integrations
- Support Apple, Google, Microsoft sign-in
- MFA for admin accounts and optionally all users
- RBAC for workspace roles
- Session revocation and device/session management

## 11.3 Data Protection
- TLS 1.2+
- AES-256 encrypted storage for tokens and sensitive integration metadata
- Envelope encryption for provider tokens
- Separate KMS-managed secrets
- Signed webhook verification for Stripe, Google, Microsoft, etc.

## 11.4 Privacy Controls
- User-visible integration permissions
- Ability to disconnect and purge integrations
- Data export and deletion workflows
- Configurable AI data retention
- Option to disable model training retention with vendors
- Clear handling of meeting recordings and transcripts
- Fine-grained controls for busy/free availability sharing and social planning visibility

## 11.5 AI-Specific Safety
- Log all AI actions that affect scheduling or task structure
- Require confirmation for high-impact destructive changes
- Confidence thresholds for auto-actions
- Fallback behavior when model confidence is low
- Model output schema validation before persistence

## 11.6 Compliance Roadmap
**MVP:**
- SOC 2-ready architecture
- GDPR/CCPA-aware policies
- DPA support
- audit logging
- secure SDLC

**Post-traction:**
- SOC 2 Type II
- pen testing
- enterprise SSO/SAML
- data residency options if enterprise needed

---

## 12. Revenue Model and Financial Projection

## 12.1 Recommended Pricing Strategy

### Tier 1: Free
**Price:** $0  
**Target:** capture, lightweight planning, personal trial

Includes:
- 1 connected calendar
- up to 100 active tasks
- manual scheduling
- limited AI parses per month
- basic iPhone app

### Tier 2: Pro
**Price:** $15/month or $144/year  
**Target:** professionals replacing Akiflow / upgrading from basic tools

Includes:
- unlimited tasks
- multiple calendars
- AI scheduling
- AI reprioritization
- meeting action extraction (limited)
- Mac app + iPhone app
- widgets and advanced notifications
- smart inbox review and approval workflows

### Tier 3: Pro Plus
**Price:** $24/month or $228/year  
**Target:** power users / founders / executives

Includes:
- advanced AI planning
- meeting intelligence
- docs to tasks
- premium analytics
- social planning features
- priority support
- higher AI quotas

### Tier 4: Teams
**Price:** $20-$30/user/month depending on feature scope  
**Target:** small teams, agencies, executive offices

Includes:
- shared workspaces
- assignees
- shared planning views
- team analytics
- admin controls

### Tier 5: Enterprise
**Price:** custom  
Includes:
- SSO/SAML
- audit exports
- security review
- custom retention
- onboarding/support

## 12.2 Unit Economics Assumptions

For rough planning:
- blended AI cost per active Pro user: **$1.50-$4.00/month** depending on model usage discipline
- infrastructure per active user early stage: **$0.50-$2.00/month**
- payment + support overhead: **$0.75-$1.50/month**

This means a $15-$24 pricing band is healthy if AI usage is rate-limited intelligently and the product avoids wasteful always-on model calls.

## 12.3 Revenue Projection Scenarios

### Conservative Scenario
- Year 1 end: 500 paying users
- ARPU: $16/month
- MRR: $8,000
- ARR: $96,000

### Base Case Scenario
- Year 1 end: 1,500 paying users
- ARPU: $17/month
- MRR: $25,500
- ARR: $306,000

### Aggressive Scenario
- Year 1 end: 5,000 paying users
- ARPU: $18/month
- MRR: $90,000
- ARR: $1.08M

## 12.4 24-Month Vision Scenario
If Chronos reaches:
- 8,000 Pro users at $16 ARPU = $128,000 MRR
- 1,000 Pro Plus users at $24 ARPU = $24,000 MRR
- 50 small teams averaging $400/month = $20,000 MRR

**Total MRR:** ~$172,000  
**Annualized:** ~$2.06M ARR

This is realistic only if retention is strong and the native experience genuinely creates loyalty.

---

## 13. Build vs Buy Recommendations

## Buy / use managed first
- Auth: Clerk/Auth0/Supabase Auth
- Billing: Stripe
- Analytics: PostHog
- Error monitoring: Sentry
- Transcription: Deepgram or Whisper API
- Email: Resend/Postmark
- Push: OneSignal or native APNs/FCM path

## Build in-house
- Scheduling engine
- AI orchestration layer
- task prioritization logic
- native UX layer
- sync reconciliation logic
- behavioral personalization layer

**Opinion:** do not waste time reinventing auth or billing. Build the planning moat.

---

## 14. MVP Definition

A strong MVP should not try to be a full operating system for work.

## 14.1 MVP Must-Haves
- account creation and onboarding
- Google Calendar integration
- task inbox + task management
- smart inbox for imports and AI scheduling suggestions
- natural language task parsing
- basic AI prioritization
- auto-scheduling for personal use
- user controls for work hours, buffers, focus protection, and task-load limits
- flexible item types (scheduled event, flexible event, flexible task)
- replanning after calendar disruptions
- basic daily planning timeline with approve/adjust controls

## 14.2 MVP Should Explicitly Include

To preserve product clarity, the MVP should already include the foundations of the new planning model even if the most advanced collaboration layers ship later. That means:
- the three flexibility types in the domain model and scheduler
- smart inbox ingestion from manual capture plus at least one external integration source
- one-click approve/adjust flows for AI-proposed schedule placements
- user policy controls that define when and how auto-scheduling can happen

## 14.3 Phase 2 Expansion

Once the solo planning loop is strong, Chronos should expand into:
- friend connections and social planning invites
- privacy-safe availability sharing
- inbox-driven incoming plan requests
- collaborative accept / adjust / suggest-alternative workflows
- richer integrations that feed the smart inbox automatically
