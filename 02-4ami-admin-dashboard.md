# File: stories/02-4ami-admin-dashboard.md

# Story 2: 4AMI Admin – Dashboard

## Context

**Figma URL:**
https://www.figma.com/design/JDoPGdZ6anmqLy7YFI9sXp/4ami-Dashboard?node-id=917-3536

**Story goal (from PRD + Figma)**
Provide 4AMI administrators with a centralized dashboard that displays key business metrics (Total Residual, Users, Projects, Customers), recent project activity, quick actions, and notifications. The dashboard serves as the primary landing page after login, enabling admins to quickly assess system health, navigate to key sections, and take common actions without deep navigation.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – Dashboard landing view: Admin logs in and sees dashboard with 4 metric cards (Total Residual with dropdown filter, Users with trend indicator, Projects with description, Customers with trend indicator), Projects short table, Recent Activity table, and Quick Actions sidebar.
- [x] Step 2 – Filter interaction: Admin clicks Total Residual dropdown to filter by time period or other criteria; filter state persists and updates metric cards accordingly.
- [x] Step 3 – Projects table interaction: Admin views recent projects in short table format, can click to navigate to project details, and sees key project information at a glance.
- [x] Step 4 – Recent Activity review: Admin scrolls through recent activity feed showing system events, user actions, and project updates with timestamps.
- [x] Step 5 – Quick Actions: Admin clicks quick action items (Add User, Add Asset, Add Project) to navigate to creation flows.
- [x] Step 6 – Notification access: Admin clicks notification bell in topbar to view grouped notifications (Today, Earlier), dismiss individual items, or navigate to full notification page.
- [x] Step 7 – Profile dropdown: Admin clicks profile avatar to access profile menu (Profile, Settings, Logout).
- [x] Step 8 – Sidebar toggle: Admin can collapse/expand sidebar to maximize content area while maintaining navigation access.

**States to support**
- [x] Loading states – skeleton loaders or spinners for metric cards, tables, and activity feed while data fetches.
- [x] Error states – inline error messages for failed metric calculations, table load failures, network errors with retry options.
- [x] Empty data states – placeholder messaging when no projects exist, no recent activity, or metrics are zero with guidance on next steps.
- [x] Permission/role-based visibility – hide or disable features based on admin role/permissions (e.g., certain quick actions, metric filters).

## Frontend

**Screens / components**
- [ ] `AdminDashboardView` (main dashboard container with header, breadcrumbs, content grid) – Status: Not Started
- [ ] `MetricCard` (reusable stat card with icon, value, label, optional dropdown/trend indicator) – Status: Not Started
- [ ] `ProjectsShortTable` (compact table showing recent projects with columns, pagination, row actions) – Status: Not Started
- [ ] `RecentActivityTable` (activity feed with avatars, messages, timestamps, scrollable list) – Status: Not Started
- [ ] `QuickActionsSidebar` (vertical list of quick action items with icons and descriptions) – Status: Not Started
- [ ] `NotificationDropdown` (dropdown menu with grouped notifications, dismiss actions, "See all" link) – Status: Not Started
- [ ] `ProfileDropdown` (user menu with avatar, email, Profile/Settings/Logout options) – Status: Not Started
- [ ] `FilterDropdown` (time period/criteria selector for Total Residual metric) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/admin/dashboard` route with layout shell (sidebar, topbar, content area) matching Figma structure – Status: Not Started – Est: 2.5h
- [ ] Build reusable `MetricCard` component with icon slot, value display, label, optional trend indicator, and dropdown trigger – Status: Not Started – Est: 2.5h
- [ ] Implement 4 metric cards (Total Residual, Users, Projects, Customers) with correct icons, data binding, and conditional UI (dropdown on Total Residual, trends on Users/Customers) – Status: Not Started – Est: 2.5h
- [ ] Build `FilterDropdown` component for Total Residual with time period options, state management, and callback to update metrics – Status: Not Started – Est: 2h
- [ ] Create `ProjectsShortTable` component with columns (project name, status, date, actions), row click navigation, and empty state – Status: Not Started – Est: 3h
- [ ] Implement `RecentActivityTable` component with activity items (avatar, message, timestamp), infinite scroll or pagination, and empty state – Status: Not Started – Est: 2.5h
- [ ] Build `QuickActionsSidebar` with 3 action items (Add User, Add Asset, Add Project), icon + text layout, click handlers for navigation – Status: Not Started – Est: 2h
- [ ] Create `NotificationDropdown` component with grouped sections (Today, Earlier), dismiss buttons, avatar + message layout, "See all" link – Status: Not Started – Est: 2.5h
- [ ] Implement `ProfileDropdown` with user info header, menu items (Profile, Settings, Logout), click handlers, and positioning logic – Status: Not Started – Est: 2h
- [ ] Wire dashboard data fetching (metrics, projects, activity) with React Query or similar, loading states, error boundaries – Status: Not Started – Est: 2.5h
- [ ] Add skeleton loaders for metric cards, tables, and activity feed during initial load – Status: Not Started – Est: 2h
- [ ] Implement error states with retry buttons for failed API calls, inline error messages per widget – Status: Not Started – Est: 2h
- [ ] Add empty states for projects table, activity feed, and zero-value metrics with helpful messaging – Status: Not Started – Est: 1.5h
- [ ] Implement sidebar collapse/expand toggle with state persistence and responsive layout adjustments – Status: Not Started – Est: 2h
- [ ] Add responsive breakpoints for tablet/desktop views per Figma, ensure metric cards wrap appropriately – Status: Not Started – Est: 2h
- [ ] Polish accessibility: keyboard navigation, focus management, ARIA labels for interactive elements, screen reader announcements – Status: Not Started – Est: 2h

## Backend

**APIs / endpoints**
- [ ] GET `/admin/dashboard/metrics` – returns Total Residual, Users count, Projects count, Customers count with optional time filter – Status: missing – Est: 4h
  **Gap:** No dedicated admin dashboard module or combined metrics endpoint. Individual stats exist across modules (users.controller.ts:85, projects.controller.ts:96, reports.controller.ts:64) but not aggregated. Need new admin module with controller to aggregate: (1) Total Residual from assets.residualValue SUM, (2) Users count from users table, (3) Projects count from projects table, (4) Customers count from companies table. Must support time filtering for Total Residual.
- [ ] GET `/admin/dashboard/projects` – returns paginated list of recent projects (short format) – Status: partial – Est: 2h
  **Current:** GET `/projects` exists with pagination but returns full project objects. **Gap:** Need dashboard-specific endpoint returning lightweight format (id, name, status, date, projectNumber) optimized for dashboard table. Add to new admin controller or projects controller with `?view=dashboard` query param.
- [ ] GET `/admin/dashboard/activity` – returns recent activity feed with pagination – Status: missing – Est: 5h
  **Gap:** No activity logging system exists. No ActivityLog or AuditLog entity found. Need to: (1) Create activity_logs entity (id, user_id, action, entity_type, entity_id, message, metadata, timestamp), (2) Add activity logging middleware or decorator, (3) Implement endpoint to fetch recent activities with pagination, (4) Add activity tracking for key events (user creation, project submission, password reset, etc.).
- [ ] GET `/admin/notifications` – returns grouped notifications (Today, Earlier) with pagination – Status: missing – Est: 4h
  **Gap:** No notifications system exists. No Notification entity found. Need to: (1) Create notifications entity (id, user_id, type, title, message, is_read, is_dismissed, metadata, created_at), (2) Implement notification service to create/read/dismiss notifications, (3) Add notification triggers for events (new user, project submitted, report ready), (4) Implement endpoint with Today/Earlier grouping logic.
- [ ] PATCH `/admin/notifications/:id/dismiss` – marks notification as dismissed – Status: missing – Est: 1h
  **Gap:** Depends on notifications entity creation. Need endpoint to update notification.is_dismissed = true with user ownership validation.

**Backend tasks**
- [ ] Design dashboard metrics data model and aggregation strategy (cache vs real-time, time windows) – Status: missing – Est: 2h
  **Gap:** No caching strategy defined. Need to decide: (1) Real-time vs cached metrics, (2) Cache TTL (suggest 5min for dashboard), (3) Cache invalidation triggers, (4) Time window calculations for filters. Redis already configured (app.module.ts:83) but not used for dashboard metrics.
- [ ] Implement GET `/admin/dashboard/metrics` endpoint with aggregation queries for Total Residual (sum calculation), Users (count with optional trend), Projects (count with description), Customers (count with trend) – Status: partial – Est: 4h
  **Current:** Individual stats endpoints exist: users.service.ts:406 (getDashboardStats), projects.service.ts:496 (getDashboardStats). **Gap:** Need new admin controller/service to aggregate all metrics in single endpoint. Total Residual calculation missing (need SUM(assets.residualValue) from assets table). Trend calculations not implemented. Must add role guard @Roles(UserRole.ADMIN).
- [ ] Add time period filtering support for Total Residual metric (today, week, month, year, custom range) with efficient date range queries – Status: missing – Est: 3h
  **Gap:** No time-based filtering exists for any metrics. Need to: (1) Add query params (startDate, endDate, period enum), (2) Implement date range SQL queries on assets table with createdAt/updatedAt filters, (3) Optimize with database indexes on date columns, (4) Add validation for date ranges.
- [ ] Implement GET `/admin/dashboard/projects` endpoint with pagination, sorting (by date desc), and field selection for short table format – Status: partial – Est: 2h
  **Current:** GET `/projects` (projects.controller.ts:83) returns full project objects with relations. **Gap:** Need dashboard-optimized endpoint returning only: id, projectNumber, name, status, submitDate, createdAt. Can add to projects controller with query param `?format=dashboard` or create in admin controller.
- [ ] Build GET `/admin/dashboard/activity` endpoint aggregating events from multiple sources (user actions, project updates, system events) with pagination and timestamp ordering – Status: missing – Est: 5h
  **Gap:** Complete activity tracking system missing. Need to: (1) Create ActivityLog entity with migration, (2) Build ActivityService with create/findRecent methods, (3) Add logging decorator or middleware, (4) Implement activity tracking in key services (auth, users, projects, companies), (5) Create endpoint to query activities with pagination, filtering, and formatting (avatar, message template).
- [ ] Implement GET `/admin/notifications` endpoint with grouping logic (Today vs Earlier), pagination, and user-specific filtering – Status: missing – Est: 4h
  **Gap:** Notifications system doesn't exist. Need to: (1) Create Notification entity with migration, (2) Build NotificationService with CRUD methods, (3) Implement grouping logic (Today = created_at >= start of today, Earlier = before today), (4) Add pagination and filtering, (5) Create endpoint with proper response format.
- [ ] Create PATCH `/admin/notifications/:id/dismiss` endpoint to mark notifications as dismissed, validate ownership, update database – Status: missing – Est: 1h
  **Gap:** Depends on Notification entity. Simple update operation with validation: check notification exists, verify user_id matches current user (or is admin), set is_dismissed = true, return success.
- [ ] Add authentication middleware to all dashboard endpoints, verify admin role/permissions – Status: partial – Est: 1.5h
  **Current:** JWT auth exists (jwt-auth.guard.ts), @Roles decorator exists (roles.decorator.ts, roles.guard.ts). **Gap:** Need to apply @Roles(UserRole.ADMIN) to all new admin endpoints and ensure guards are active globally or per-controller. Verify guard order (JWT -> Roles).
- [ ] Implement rate limiting for dashboard endpoints to prevent abuse, especially for metrics aggregation – Status: missing – Est: 2h
  **Gap:** No @nestjs/throttler found (same as password reset story). Need to: (1) Install @nestjs/throttler, (2) Configure ThrottlerModule in app.module.ts with sensible limits (e.g., 20 requests per minute for admin endpoints), (3) Apply @Throttle decorator to dashboard controllers, (4) Add custom rate limit strategy for expensive aggregation queries.
- [ ] Add caching layer for metrics (Redis or in-memory) with TTL to reduce database load on frequent dashboard refreshes – Status: missing – Est: 3h
  **Gap:** Redis configured but not used for caching. Need to: (1) Install @nestjs/cache-manager, (2) Configure CacheModule with Redis store, (3) Use @CacheKey and @CacheTTL decorators on metrics endpoints (suggest 300s TTL), (4) Implement cache invalidation on data changes (user created, project submitted, asset updated), (5) Add cache hit/miss logging.
- [ ] Write unit tests for metric calculation logic, aggregation queries, time period filtering – Status: missing – Est: 3h
  **Gap:** auth.spec.ts shows minimal test coverage. Need comprehensive tests for: (1) Total Residual calculation with various asset states, (2) Time period filtering edge cases, (3) Aggregation query correctness, (4) Cache behavior, (5) Permission checks.
- [ ] Add integration tests for dashboard endpoints covering happy path, pagination, filtering, permission checks – Status: missing – Est: 3h
  **Gap:** Need e2e tests for: (1) Full dashboard metrics endpoint with various filters, (2) Projects list with pagination, (3) Activity feed with date ranges, (4) Notifications CRUD with grouping, (5) Non-admin access denial, (6) Rate limiting behavior.

**Additional production-ready tasks identified:**
- [ ] Create admin dashboard module and controller – Status: missing – Est: 2h
  **Gap:** No dedicated admin module. Create src/modules/admin/admin.module.ts, admin.controller.ts, admin.service.ts to centralize dashboard logic. Import required repositories and services (users, projects, companies, assets).
- [ ] Implement Total Residual calculation service – Status: missing – Est: 2.5h
  **Gap:** Assets have residualValue field (asset.entity.ts:34) but no aggregation logic. Need service method to: (1) Query SUM(residualValue) from assets table, (2) Support filtering by date range, asset status, project, (3) Handle null values, (4) Format currency output.
- [ ] Add database indexes for dashboard query optimization – Status: missing – Est: 1.5h
  **Gap:** No indexes identified for dashboard queries. Need indexes on: (1) assets(createdAt, residualValue), (2) projects(status, submitDate, createdAt), (3) users(role, isActive, createdAt), (4) companies(createdAt), (5) activity_logs(timestamp, user_id), (6) notifications(user_id, created_at, is_dismissed).
- [ ] Implement trend calculation logic for metrics – Status: missing – Est: 2.5h
  **Gap:** Spec mentions "trend indicator" for Users and Customers metrics but no implementation. Need service to: (1) Calculate current period count, (2) Calculate previous period count, (3) Compute percentage change, (4) Return trend direction (up/down) and value. Consider caching historical counts.
- [ ] Add structured logging for dashboard access and performance – Status: missing – Est: 2h
  **Gap:** Only console.log statements exist. Need structured logger (Winston/Pino) with: (1) Dashboard access logs (user_id, endpoint, timestamp, duration), (2) Slow query alerts (>500ms), (3) Cache hit/miss rates, (4) Error tracking with stack traces, (5) Correlation IDs for request tracing.
- [ ] Implement dashboard metrics cache warming strategy – Status: missing – Est: 2h
  **Gap:** No cache warming. Need Bull cron job to: (1) Pre-calculate and cache dashboard metrics every 5 minutes, (2) Run at off-peak times for expensive calculations, (3) Ensure cache is warm before business hours, (4) Add job monitoring and failure alerting.

## DevOps / Infra

**Config / services**
- [ ] Redis cache for dashboard metrics
- [ ] Monitoring/alerting for dashboard endpoint performance
- [ ] Logging aggregation for dashboard access patterns
- [ ] Database query optimization/indexes for aggregation queries

**DevOps tasks**
- [ ] Configure Redis instance/connection for dashboard metrics caching with appropriate TTL settings – Status: done
  **Current:** Redis already configured in app.module.ts:83-93 with connection settings from environment. Ready for use with @nestjs/cache-manager.
- [ ] Set up monitoring dashboards for dashboard endpoint response times, error rates, cache hit rates – Status: missing – Est: 2h
  **Gap:** No monitoring configured. Need to: (1) Add APM integration (DataDog, New Relic, or CloudWatch), (2) Track custom metrics (dashboard_load_time, cache_hit_rate, query_duration), (3) Create monitoring dashboard with key metrics, (4) Set baseline performance targets.
- [ ] Add database indexes on frequently queried fields (project dates, activity timestamps, user roles) to optimize aggregation queries – Status: missing – Est: 2h
  **Gap:** No custom indexes identified. Need migration to add indexes listed in backend tasks above. Use EXPLAIN ANALYZE to validate query performance improvements. Monitor index usage and size.
- [ ] Configure log aggregation for dashboard access patterns, user behavior analytics, and error tracking – Status: missing – Est: 1.5h
  **Gap:** No centralized logging. Need to: (1) Configure log shipping to aggregation service (ELK, CloudWatch Logs, Datadog), (2) Add structured JSON logging, (3) Create log parsing rules, (4) Set up dashboard access pattern analysis, (5) Add error rate tracking.
- [ ] Set up alerting for dashboard endpoint failures, slow queries (>500ms), and cache misses exceeding threshold – Status: missing – Est: 2h
  **Gap:** No alerting configured. Need alerts for: (1) Dashboard endpoint error rate >5%, (2) Response time >1s (p95), (3) Cache miss rate >20%, (4) Aggregation query duration >500ms, (5) Redis connection failures. Use PagerDuty, Slack, or email for notifications.
- [ ] Document caching strategy, cache invalidation triggers (when new projects/users added), and cache warming approach – Status: missing – Est: 1.5h
  **Gap:** No documentation exists. Need runbook covering: (1) Cache key structure and TTLs, (2) Invalidation triggers and implementation, (3) Cache warming schedule and job configuration, (4) Debugging cache issues, (5) Cache monitoring and health checks.
- [ ] Performance testing: load test dashboard endpoints with expected concurrent admin users, identify bottlenecks – Status: missing – Est: 2h
  **Gap:** No performance testing. Need to: (1) Define expected load (e.g., 10 concurrent admins, 100 requests/min), (2) Use k6, JMeter, or Artillery for load testing, (3) Test with cold and warm cache, (4) Identify query bottlenecks, (5) Establish performance baselines and SLOs.

## Definition of Done

**Functional**
- [ ] Admin can view all 4 metric cards with accurate, real-time or cached data on dashboard load.
- [ ] Total Residual dropdown filter works and updates metric value based on selected time period.
- [ ] Projects short table displays recent projects with pagination, row clicks navigate to project details.
- [ ] Recent Activity table shows chronological activity feed with proper pagination/infinite scroll.
- [ ] Quick Actions sidebar items navigate to correct creation flows (Add User, Add Asset, Add Project).
- [ ] Notification dropdown displays grouped notifications, dismiss functionality works, "See all" links to full page.
- [ ] Profile dropdown shows user info and menu items, logout functionality works.
- [ ] Sidebar collapse/expand toggle works and persists state across page refreshes.

**UX**
- [ ] Layout, spacing, typography, and component styling match Figma designs for all dashboard views (opened sidebar, closed sidebar, with filters).
- [ ] Loading states (skeletons/spinners) appear during data fetch, no blank screens.
- [ ] Error states display clear messages with retry options, no unhandled errors.
- [ ] Empty states show helpful messaging when no projects/activity exist, guide users to next actions.
- [ ] Responsive behavior works for desktop and tablet breakpoints shown in Figma.
- [ ] All interactive elements have proper hover/focus states, keyboard navigation works.

**QA**
- [ ] Happy path: Dashboard loads with all widgets populated, metrics are accurate, tables show data.
- [ ] Filter testing: Total Residual filter updates metric correctly for each time period option.
- [ ] Pagination testing: Projects and Activity tables paginate correctly, no duplicate or missing items.
- [ ] Permission testing: Non-admin users cannot access dashboard, admin users see all features.
- [ ] Error handling: Network failures show error states, retry works, partial failures don't break entire dashboard.
- [ ] Performance: Dashboard loads within 2 seconds on average, metrics cache reduces subsequent load times.
- [ ] Empty state testing: Zero projects, zero activity, zero metrics all show appropriate empty states.
- [ ] Notification testing: Dismiss works, grouping is correct, navigation to full notification page works.

## Estimate

- Frontend: ~32h (L)
- Backend: ~45h (XL) - Updated from 26h due to missing notifications system, activity logging, Total Residual calculation, caching implementation, and admin module creation
- DevOps: ~13h (M)

## Summary of Backend Gap Analysis

### Current State

The backend has **scattered dashboard statistics** but no centralized admin dashboard:
- ✅ Individual stats endpoints exist (users.controller.ts:85, projects.controller.ts:96, reports.controller.ts:64)
- ✅ User counts with role breakdown (users.service.ts:406)
- ✅ Project counts by status (projects.service.ts:496)
- ✅ Projects listing with pagination (projects.controller.ts:83)
- ✅ Assets have residualValue field (asset.entity.ts:34)
- ✅ JWT auth + role guards infrastructure exists
- ✅ Redis configured for caching (app.module.ts:83)
- ✅ Bull queue system for background jobs

### Critical Gaps

**1. No Admin Dashboard Module (HIGH PRIORITY)**
- ❌ No dedicated admin module or controller
- ❌ Stats endpoints scattered across different modules
- ❌ No combined metrics aggregation endpoint
- **Impact:** Need new admin module to centralize dashboard logic

**2. Missing Core Features (BLOCKERS)**
- ❌ **Total Residual Calculation:** Assets have residualValue but no SUM aggregation endpoint
- ❌ **Notifications System:** No Notification entity, service, or endpoints at all
- ❌ **Activity Feed:** No ActivityLog entity or tracking system
- ❌ **Time-based Filtering:** No date range filtering for any metrics
- **Impact:** 3 of 5 main dashboard features are completely missing

**3. No Dashboard Optimization (HIGH IMPACT)**
- ❌ Redis configured but not used for metrics caching
- ❌ No rate limiting (same gap as password reset story)
- ❌ No database indexes for aggregation queries
- ❌ No trend calculations for metrics
- ❌ No cache warming strategy
- **Impact:** Dashboard will be slow and expensive without caching layer

**4. Missing Infrastructure (PRODUCTION REQUIREMENTS)**
- ❌ No structured logging (only console.log)
- ❌ No monitoring/alerting for dashboard performance
- ❌ No performance testing baseline
- ❌ Minimal test coverage (auth.spec.ts has placeholders only)
- **Impact:** Cannot ensure production readiness or troubleshoot issues

**5. Data Model Gaps**
- ❌ No Notification entity/table
- ❌ No ActivityLog entity/table
- ❌ No indexes on date columns for filtering
- **Impact:** Need 2 new entities + migrations before building endpoints

### Architecture Mismatch

**Spec requires:** Unified admin dashboard with real-time metrics, activity feed, and notifications
**Current implementation:** Scattered stats endpoints with no aggregation, no activity tracking, no notifications

The gap is substantial - approximately **60% of backend functionality is missing**:
- Endpoints: 3 of 5 missing (60%)
- Core features: 3 of 4 missing (Total Residual calc, Activity, Notifications)
- Infrastructure: Caching, rate limiting, monitoring all missing
- Entities: 2 new entities needed (Notification, ActivityLog)

### Revised Effort Estimate

**Original estimate:** 26h
**Updated estimate:** 45h (+19h)

**Breakdown:**
- Admin module + combined metrics endpoint: ~6h
- Total Residual calculation + time filtering: ~5.5h
- Notifications system (entity, service, endpoints): ~8h
- Activity logging system (entity, tracking, endpoint): ~10h
- Caching layer + cache warming: ~5h
- Rate limiting + database indexes: ~3.5h
- Testing (unit + integration): ~6h
- DevOps (monitoring, logging, docs): ~7h (partial - done: 2h, missing: 11h)

### Recommendation

The backend requires **significant new development** across multiple layers:
1. **Data Layer:** Create 2 new entities (Notification, ActivityLog) with migrations
2. **Service Layer:** Build notification service, activity logging service, metrics aggregation service
3. **API Layer:** Create admin controller with 5 new endpoints
4. **Infrastructure:** Implement caching, rate limiting, monitoring, indexes
5. **Testing:** Comprehensive test suite for all new functionality

**Priority Order:**
1. Create admin module + Total Residual endpoint (enables basic dashboard)
2. Implement caching layer (ensures performance)
3. Build activity logging (enables activity feed)
4. Build notifications system (enables notifications feature)
5. Add monitoring + testing (ensures production readiness)

The scattered architecture and missing core features make this a **large effort** requiring careful planning and execution to avoid technical debt.
