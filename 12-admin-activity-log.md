# File: stories/12-admin-activity-log.md

# Story 12: Admin – Activity Log

## Context

**Figma URL:**  
https://www.figma.com/design/yiCfEo9ZDgLyIkSiK7NVP2/4ami-Dashboard--copia-?node-id=2730-5846&t=dwNhFJQ5EbJ3AdrU-0

**Story goal (from PRD + Figma)**
Enable administrators to monitor and audit all significant system activities through a comprehensive activity log viewer that tracks user actions, system events, data changes, and security-related activities for compliance, security monitoring, debugging, and operational oversight. The system must capture all key actions (user logins, data modifications, permission changes, document uploads, request submissions), display them in a searchable and filterable table, provide detailed drill-down views for investigation, support exporting for external analysis, and maintain logs for compliance retention periods. This enables admins to investigate security incidents, troubleshoot user issues, verify compliance with policies, and maintain a complete audit trail of all system operations.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – Access activity log: Admin navigates to "Activity Log" from main navigation or admin menu, sees introduction/description of what's tracked (optional), views main activity log table with recent activities loaded.
- [x] Step 2 – Browse activities: Admin scrolls through paginated list of activities (default sorted by timestamp descending, newest first), sees key information in table columns (timestamp, user, action type, entity, status, IP address), can adjust page size (25, 50, 100 entries per page), navigates between pages.
- [x] Step 3 – Filter activities: Admin applies filters to narrow down results by action type (Login, Create, Update, Delete, Export, Permission Change), by user (dropdown or autocomplete with user list), by entity type (User, Company, Transportation Request, Call Request, etc.), by status (Success, Failed), by date range (predefined ranges: Today, Last 7 Days, Last 30 Days, Custom), sees filtered results update in table, can clear individual filters or all filters.
- [x] Step 4 – Search activities: Admin uses text search to find specific activities, searches across user names, action descriptions, entity IDs, IP addresses, sees search results highlighted in table, can combine search with filters.
- [x] Step 5 – View activity details: Admin clicks on activity row to open detail panel or modal, sees comprehensive information (full timestamp, user details with avatar, action description, entity type and ID, IP address and location, user agent/browser, request ID for correlation, changes made with before/after values for data modifications, error details if action failed), can copy values for investigation, can navigate to related entity if applicable.
- [x] Step 6 – Export activities: Admin selects export option (CSV, JSON, Excel), optionally applies filters before export to limit data, chooses date range for export, initiates export (may be async for large datasets), downloads exported file or receives email with download link, export includes all visible columns and detail information.
- [x] Step 7 – Real-time monitoring: Admin can enable auto-refresh to see new activities as they occur (optional), sees new activity indicators or notifications, can pause auto-refresh for detailed investigation.

**States to support**
- [x] Loading states – initial table load with skeleton rows, filter/search loading with spinner, pagination loading when changing pages, detail panel loading, export progress indicator.
- [x] Error states – failed to load activities (show error message with retry button), filter/search errors (show inline error), export errors (show toast with error details), permission denied for viewing certain activities, network errors with offline indicator.
- [x] Empty/edge states – no activities found (fresh system or all activities deleted), no results for current filters (show "No activities match your filters" with option to clear filters), no activities in selected date range, user has no permission to view any logs, detail panel when activity has been purged/archived.
- [x] Success confirmation – export initiated successfully (show toast "Export started, you'll receive an email when complete"), filters applied (show filter count badge), search results found (show "X results found"), activity detail loaded.

## Frontend

**Screens / components**
- [ ] `ActivityLogView` (main page container with table, filters, search) – Status: Not Started
- [ ] `ActivityLogTable` (data table with sortable columns, pagination, row selection) – Status: Not Started
- [ ] `ActivityLogFilters` (filter controls for type, user, entity, status, date range) – Status: Not Started
- [ ] `ActivityLogSearch` (search input with autocomplete suggestions) – Status: Not Started
- [ ] `ActivityDetailPanel` (side panel or modal showing full activity details) – Status: Not Started
- [ ] `ActivityExportDialog` (export options modal with format and date range selection) – Status: Not Started
- [ ] `DateRangePicker` (reusable date range selector with presets) – Status: Not Started
- [ ] `UserFilter` (autocomplete user selector for filtering) – Status: Not Started
- [ ] `ActivityTypeIcon` (icon component for different action types) – Status: Not Started
- [ ] `ChangesDiffViewer` (before/after comparison for data changes) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/admin/activity-log` route with layout (page header, filters sidebar or top bar, main content area) matching Figma structure – Status: Not Started – Est: 2h
- [ ] Build `ActivityLogView` container component managing table state, filters state, search state, pagination state, handles API integration – Status: Not Started – Est: 2.5h
- [ ] Implement `ActivityLogTable` component with sortable columns (Timestamp, User, Action Type, Entity, Status, IP Address), pagination controls (page size selector, previous/next, page numbers), loading skeleton rows, empty state, row click handlers – Status: Not Started – Est: 3h
- [ ] Create table column definitions: timestamp with relative time (e.g., "2 hours ago") and full datetime on hover, user column with avatar and name, action type with icon and color coding (green for Create, blue for Update, red for Delete), entity column with type and ID/name, status column with badge (success = green, failed = red), IP address column with location flag (optional) – Status: Not Started – Est: 2.5h
- [ ] Build `ActivityLogFilters` component with action type multi-select dropdown (Login, Create, Update, Delete, Export, Permission Change, etc.), entity type dropdown (All, User, Company, Transportation Request, Call Request), status dropdown (All, Success, Failed), date range picker, user filter autocomplete, clear filters button, filter count badge – Status: Not Started – Est: 3h
- [ ] Implement `DateRangePicker` component with preset ranges (Today, Yesterday, Last 7 Days, Last 30 Days, This Month, Last Month, Custom), custom range selection with start/end date pickers, validation (end date cannot be before start date), display selected range in button/input – Status: Not Started – Est: 2.5h
- [ ] Create `ActivityLogSearch` component with search input field (placeholder: "Search by user, action, entity, IP..."), debounced search (wait 300ms after typing stops), autocomplete suggestions dropdown (recent searches, suggested filters), search icon and clear button – Status: Not Started – Est: 2h
- [ ] Build `UserFilter` component with autocomplete user search, loads users from API as user types, displays user avatar and name in results, multi-select capability (filter by multiple users), shows selected users as chips with remove button – Status: Not Started – Est: 2.5h
- [ ] Implement `ActivityDetailPanel` as sliding panel or modal that opens when clicking activity row, displays all activity fields (timestamp, user info with avatar, action description, entity type and ID with link, IP address with geolocation, user agent/browser, request ID, duration if applicable), shows changes diff for Update actions (before/after comparison), includes copy buttons for IDs and values, has close button or click-outside to close – Status: Not Started – Est: 3h
- [ ] Create `ChangesDiffViewer` component for displaying data changes, shows side-by-side or inline diff of before/after values, highlights changed fields in yellow, shows field name, old value (strikethrough), new value (underline or green), handles nested objects and arrays, supports JSON formatting for complex values – Status: Not Started – Est: 2.5h
- [ ] Build `ActivityTypeIcon` component that returns appropriate icon for each action type (Login = lock icon, Create = plus icon, Update = pencil icon, Delete = trash icon, Export = download icon, Permission Change = shield icon), with color coding matching action severity/type – Status: Not Started – Est: 1.5h
- [ ] Add filter state management: store active filters in URL query params for bookmarking and sharing, restore filters from URL on page load, update URL when filters change without page reload, clear URL params when clearing filters – Status: Not Started – Est: 2h
- [ ] Implement pagination controls: page size selector (25, 50, 100 entries per page), previous/next buttons, page number buttons (show 1, 2, 3, ..., last), current page indicator, total count display ("Showing 1-25 of 1,234 activities"), jump to page input (optional) – Status: Not Started – Est: 2h
- [ ] Add sorting functionality: sortable columns with sort indicator (up/down arrow), click column header to sort ascending, click again for descending, click third time to remove sort, default sort by timestamp descending, only one column sorted at a time – Status: Not Started – Est: 2h
- [ ] Implement API integration for GET /activity-log: build query params from filters, search, sort, pagination state, handle response with activities array and metadata (total count, page, pageSize), map response data to table rows, handle error responses – Status: Not Started – Est: 2h
- [ ] Add real-time updates with polling or WebSocket (optional): poll GET /activity-log every 30 seconds when auto-refresh enabled, show "New activities available" indicator at top of table, click indicator to refresh and show new activities, pause polling when user is interacting with filters or detail panel – Status: Not Started – Est: 2.5h
- [ ] Build `ActivityExportDialog` component: modal with export format selection (CSV, JSON, Excel), date range selection for export scope, option to export filtered results only or all activities, estimated file size calculation, export button that triggers download or sends email, progress indicator for large exports – Status: Not Started – Est: 2.5h
- [ ] Implement export functionality: POST /activity-log/export endpoint with format and filters, for small exports (<1000 rows): trigger immediate download, for large exports: show "Export in progress, we'll email you" message, handle export errors with retry option – Status: Not Started – Est: 2h
- [ ] Add loading states: skeleton rows while table loads (show 10 skeleton rows with pulsing animation), spinner in filter dropdown while options load, loading spinner on search while searching, disabled state for filters/search during load, pagination disabled while loading next page – Status: Not Started – Est: 2h
- [ ] Implement error handling: show error message banner if activities fail to load with "Retry" button, show inline error for failed searches or filters, handle 403 permission denied (show "You don't have permission to view activity logs"), handle 500 server errors gracefully, show toast for export errors – Status: Not Started – Est: 2h
- [ ] Add empty states: "No activities found" when system has no logged activities, "No activities match your filters" when filters return no results with "Clear filters" button, "Search returned no results" with suggestions, empty detail panel when clicking on deleted activity – Status: Not Started – Est: 1.5h
- [ ] Implement responsive design: table scrolls horizontally on mobile, filters collapse to mobile-friendly accordion or sheet, detail panel becomes full-screen modal on mobile, pagination controls stack vertically on small screens, search bar full-width on mobile – Status: Not Started – Est: 2h
- [ ] Add accessibility features: keyboard navigation through table rows (up/down arrows), keyboard shortcuts for filters (Alt+F to focus filters), focus visible for all interactive elements, ARIA labels for icons and buttons, screen reader friendly table headers, announce filter changes and search results – Status: Not Started – Est: 2h
- [ ] Polish UX details: highlight recently added activities (fade in animation), smooth transitions for filter application, tooltip on hover for truncated values, copy to clipboard buttons with confirmation toast, link to related entity (e.g., click company name to go to company profile), relative time updates (e.g., "2 minutes ago" updates to "3 minutes ago") – Status: Not Started – Est: 2h

## Backend

**APIs / endpoints**
- [ ] GET `/activity-log` – retrieve activity logs with filtering, search, pagination – **Status: missing** | Est: 3.5h | *No activity log infrastructure exists*
- [ ] GET `/activity-log/:id` – retrieve specific activity log entry details – **Status: missing** | Est: 1.5h
- [ ] POST `/activity-log/export` – export activity logs to CSV/JSON/Excel – **Status: missing** | Est: 3h
- [ ] DELETE `/activity-log/purge` – manually purge old activity logs (admin only) – **Status: missing** | Est: 1.5h

**Backend tasks**
- [ ] Design ActivityLog entity schema with fields: id, timestamp, userId (FK to User, nullable for system events), userName (denormalized for fast query), userEmail, action (enum: Login, Logout, Create, Update, Delete, Export, View, PermissionChange, etc.), entityType (User, Company, TransportationRequest, CallRequest, etc.), entityId (ID of affected entity), entityName (denormalized), description (human-readable action description), status (Success, Failed), ipAddress, userAgent, requestId (for correlation across logs), duration (milliseconds, optional), changes (JSON field with before/after values for Updates), metadata (JSON field for additional context), errorMessage (if status = Failed), createdAt – **Status: missing** | Est: 3h
- [ ] Create database migration for ActivityLog table with indexes: index on (userId, timestamp DESC), index on (action, timestamp DESC), index on (entityType, entityId, timestamp DESC), index on timestamp for retention queries, composite index on (timestamp, status, action) for common filter combinations – **Status: missing** | Est: 2h
- [ ] Implement activity logging middleware/interceptor: create NestJS interceptor that captures requests and responses, logs successful actions automatically, extracts user from JWT, captures IP address from request headers (X-Forwarded-For or req.ip), captures user agent from headers, generates request ID for correlation, wraps in try-catch to not break requests if logging fails – **Status: missing** | Est: 3h | *No interceptor infrastructure exists*
- [ ] Define loggable actions enum and mapping: enumerate all action types (Login, Logout, CreateUser, UpdateUser, DeleteUser, CreateCompany, UpdateCompany, CreateTransportationRequest, etc.), map controller methods to action types, define which actions to log (log all state-changing operations, skip GET requests except sensitive data views), configure log levels (always log, conditional log, never log) – **Status: missing** | Est: 2h
- [ ] Implement manual logging helper service: create ActivityLogService with log() method for manual logging, accepts action, entityType, entityId, description, changes, metadata, handles user extraction from context, handles system events (no userId for scheduled jobs), provides type-safe logging for each entity type, includes helper methods (logLogin, logCreate, logUpdate, logDelete, logExport) – **Status: missing** | Est: 2.5h
- [ ] Add change tracking for Update actions: implement decorator or util to capture before/after state of entities, compare old and new entity, extract changed fields only (don't log unchanged), sanitize sensitive fields (passwords, tokens), format changes as { field: { before: oldValue, after: newValue } }, store in changes JSON field – **Status: missing** | Est: 3h
- [ ] Implement GET `/activity-log` endpoint with filters: accept query params (userId, action, entityType, status, startDate, endDate, search, page, pageSize, sortBy, sortOrder), build dynamic query with filters, support search across userName, description, entityName, IP address, implement pagination with total count, sort by timestamp DESC by default, return ActivityLogDto array and metadata – **Status: missing** | Est: 3.5h
- [ ] Add search functionality with full-text search: implement search across multiple fields (userName, userEmail, description, entityName, ipAddress), use LIKE queries or full-text search indexes (PostgreSQL tsvector), highlight search terms in results (optional), rank results by relevance – **Status: missing** | Est: 2.5h
- [ ] Implement GET `/activity-log/:id` endpoint: fetch single activity log by ID, include all fields and metadata, format changes diff for easy reading, check authorization (ADMIN only), return 404 if not found or purged – **Status: missing** | Est: 1.5h
- [ ] Build export functionality POST `/activity-log/export`: accept filters and format (CSV, JSON, Excel), for small datasets (<1000): generate file immediately and return download URL, for large datasets: enqueue background job, send email with download link when complete, use streaming for large exports to avoid memory issues, apply same filters as GET endpoint – **Status: missing** | Est: 3h | *Can reuse Bull queue for async exports*
- [ ] Implement CSV export generator: create headers row with column names, iterate through filtered activities, format each activity as CSV row, escape special characters (commas, quotes, newlines), include changes as formatted text, generate downloadable file – **Status: missing** | Est: 2h
- [ ] Implement JSON export generator: serialize activities to JSON array, include all fields including metadata and changes, pretty-print JSON for readability, compress if large (gzip), generate downloadable file – **Status: missing** | Est: 1.5h
- [ ] Add authorization middleware: verify user has ADMIN role for all activity log endpoints, prevent non-admins from viewing logs, prevent users from viewing activity logs for other companies (if multi-tenant), log access to activity logs (meta-logging) – **Status: missing** | Est: 1.5h | *RolesGuard exists but need ADMIN check*
- [ ] Implement data sanitization for logs: never log passwords or tokens in plain text, hash or mask sensitive data (credit cards, SSNs), exclude sensitive fields from changes tracking (password fields), redact PII in error messages, configurable sensitive field list – **Status: missing** | Est: 2h
- [ ] Add retention and archival logic: implement DELETE `/activity-log/purge` endpoint for manual purge, create background job to auto-purge logs older than retention period (e.g., 90 days, 1 year), move to archive storage before purge (optional), log purge actions themselves, configurable retention period per action type (keep security events longer) – **Status: missing** | Est: 2.5h | *Bull queue exists for background jobs*
- [ ] Implement query performance optimizations: use database indexes for common filters, implement query result caching for repeated queries (5-minute TTL), limit max page size to prevent performance issues (max 100 per page), use cursor-based pagination for large result sets (optional), monitor slow queries and add indexes as needed – **Status: missing** | Est: 2h
- [ ] Add rate limiting to log queries: prevent abuse of activity log endpoint (max 60 requests per minute per admin), prevent export spam (max 5 exports per hour), return 429 with clear message – **Status: missing** | Est: 1h
- [ ] Write unit tests for ActivityLog entity, logging service, change tracking: test log entry creation, test change diff generation, test sanitization of sensitive data, test query building with various filters – **Status: missing** | Est: 2.5h
- [ ] Add integration tests for endpoints: GET with various filter combinations, GET with pagination and sorting, GET single activity details, POST export with different formats, search functionality, authorization checks (non-admin cannot access) – **Status: missing** | Est: 3h

**Additional production-ready tasks identified:**
- [ ] Implement log integrity verification (optional) – **Status: missing** | Est: 3h | *HMAC/digital signatures for tamper-proof logs*
- [ ] Add alerting for suspicious activities – **Status: missing** | Est: 2.5h | *Pattern detection: failed logins, mass deletions, permission escalations*
- [ ] Create activity log analytics and metrics – **Status: missing** | Est: 2h
- [ ] Implement log forwarding to SIEM – **Status: missing** | Est: 2.5h | *Integration with Splunk/ELK/CloudWatch*
- [ ] Add geolocation for IP addresses – **Status: missing** | Est: 2h | *MaxMind GeoIP integration*

## DevOps / Infra

**Config / services**
- [ ] Database storage for activity logs with proper indexes
- [ ] Log retention and archival policies
- [ ] Monitoring for log storage growth
- [ ] Optional external logging service integration (SIEM)

**DevOps tasks**
- [ ] Create database migration for ActivityLog table with optimized indexes on (userId, timestamp), (action, timestamp), (entityType, entityId, timestamp), (timestamp, status, action) – Status: missing – Est: 2h
  **Gap:** Need migration with indexes optimized for common query patterns to handle large log tables efficiently.
- [ ] Configure log retention policy: define retention periods (default 90 days, security events 1 year), configure auto-purge background job (runs daily), set up archive storage for long-term retention (S3 Glacier or similar), document retention requirements for compliance – Status: missing – Est: 2h
  **Gap:** Manage database growth and comply with data retention regulations.
- [ ] Set up database partitioning for activity log table (optional): partition by timestamp (monthly or quarterly), automatic partition creation for future periods, automatic old partition drop after retention period, improves query performance on recent data – Status: missing – Est: 3h
  **Gap:** For high-volume systems, partitioning prevents table from becoming too large and slow.
- [ ] Configure monitoring for activity log storage: track database table size and growth rate, monitor query performance (slow query log), alert when table size exceeds thresholds, monitor purge job execution and failures, track logs created per day/hour – Status: missing – Est: 2h
  **Gap:** Proactive monitoring to prevent storage issues and performance degradation.
- [ ] Set up alerting for activity log issues: alert on purge job failures, alert on excessive storage growth (>20% per week), alert on slow queries (>5 seconds), alert on logging errors (if logging infrastructure fails) – Status: missing – Est: 1.5h
  **Gap:** Early detection of issues before they impact system.
- [ ] Configure logging framework settings: set log level for activity logging (INFO), configure structured logging format (JSON), ensure log context includes request ID for correlation, configure async logging to not block requests, set up error handling (log logging failures to separate error log) – Status: missing – Est: 1.5h
  **Gap:** Proper logging configuration for performance and debuggability.
- [ ] Set up log export storage: configure S3 bucket or file storage for exported log files, set lifecycle rules to delete exports after 7 days, configure access permissions for download links, set up CDN for fast downloads (optional) – Status: missing – Est: 2h
  **Gap:** Storage infrastructure for log exports.
- [ ] Configure query result caching: set up Redis cache for frequently run queries, configure cache TTL (5 minutes), implement cache invalidation on new logs (optional), monitor cache hit rate – Status: missing – Est: 2h
  **Gap:** Improve performance for repeated queries with caching.
- [ ] Set up data privacy compliance: configure automatic PII redaction in logs, implement data subject access request (DSAR) support (export specific user's activities), implement right to erasure (delete user's activity logs on account deletion), document data retention and privacy practices – Status: missing – Est: 2.5h
  **Gap:** GDPR, CCPA, and other privacy regulation compliance.
- [ ] Create backup strategy for activity logs: include activity log table in regular database backups, test restore procedure, document retention of backups (longer than live data), configure point-in-time recovery – Status: missing – Est: 1.5h
  **Gap:** Protect audit trail data from loss.
- [ ] Set up external logging integration (optional): configure log forwarding to SIEM (Splunk, DataDog, CloudWatch Logs), format logs as JSON with standard fields, configure sampling for high-volume logs, set up log shipping pipeline – Status: missing – Est: 3h
  **Gap:** Integration with enterprise security monitoring tools.
- [ ] Document activity log system: document what actions are logged and why, document retention policies, document how to investigate incidents using logs, create runbook for common scenarios (user lockout investigation, data change audit, security incident), document export and archival procedures – Status: missing – Est: 2h
  **Gap:** Operations documentation for using activity log system.
- [ ] Configure sensitive data filtering: create list of sensitive fields to exclude from logging (password, token, SSN, credit card), implement regex patterns for automatic detection and redaction, configure field-level encryption for necessary sensitive data (optional), audit log entries for accidental sensitive data exposure – Status: missing – Est: 2h
  **Gap:** Prevent sensitive data leakage through activity logs.

## Definition of Done

**Functional**
- [ ] Activity logging automatically captures all significant system actions (logins, creates, updates, deletes, exports, permission changes).
- [ ] Admin can access activity log viewer and sees paginated list of activities sorted by timestamp (newest first).
- [ ] Activity table displays key columns: timestamp (relative time with tooltip), user (with avatar), action type (with icon), entity type/ID, status (success/failed badge), IP address.
- [ ] Admin can filter activities by action type (multi-select: Login, Create, Update, Delete, Export, etc.), by user (autocomplete with user list), by entity type (dropdown), by status (Success/Failed), by date range (presets or custom).
- [ ] Admin can search activities with text search across user names, action descriptions, entity names, IP addresses.
- [ ] Filters and search can be combined, results update dynamically, filter count badge shows number of active filters.
- [ ] Admin can click on activity row to open detail panel showing full information: complete timestamp, user details, action description, entity details, IP address with location (optional), user agent, request ID, changes diff (for updates), error message (if failed).
- [ ] For Update actions, detail panel shows before/after comparison of changed fields with highlighting.
- [ ] Admin can export filtered activities to CSV, JSON, or Excel format with date range selection.
- [ ] For small exports (<1000 rows), file downloads immediately; for large exports, admin receives email with download link.
- [ ] Pagination works with page size options (25, 50, 100), page navigation (prev/next, page numbers), total count display.
- [ ] Table columns are sortable (click header to sort ascending, again for descending, third time to remove sort).
- [ ] All logged activities appear in real-time (or within 1-2 seconds) after action occurs.
- [ ] Sensitive data (passwords, tokens) never appears in logs; PII is handled according to privacy requirements.
- [ ] Only users with ADMIN role can access activity log; non-admins receive 403 Forbidden.
- [ ] Activity log tracks its own access (meta-logging): viewing logs, exporting logs logged as activities.

**UX**
- [ ] Activity log page matches Figma design with table, filters sidebar/top bar, search bar, export button.
- [ ] Table displays with clean, readable layout; color coding for action types (green Create, blue Update, red Delete).
- [ ] Loading states show skeleton rows (10 pulsing rows) during initial load, spinners for filter/search operations.
- [ ] Empty state shows "No activities found" with helpful message when no logs exist or filters return no results.
- [ ] Error states display clear messages with retry buttons for failed loads, inline errors for failed filters.
- [ ] Detail panel/modal opens smoothly with slide or fade animation, displays information in organized sections.
- [ ] Changes diff viewer highlights changes clearly with color coding (yellow highlight, strikethrough for old, underline for new).
- [ ] Filter dropdowns, search autocomplete, date picker are responsive and user-friendly.
- [ ] Active filters shown as chips/badges with remove (X) button, "Clear all filters" button available.
- [ ] Success toast shows "Export started" or "Export downloaded" with appropriate messaging.
- [ ] Responsive design works on desktop, tablet; table scrolls horizontally on mobile, filters collapse appropriately.
- [ ] Accessibility: keyboard navigation, focus visible, ARIA labels, screen reader friendly.

**QA**
- [ ] Happy path: Admin logs in → Creates new user → Views activity log → Sees "Create User" entry with correct timestamp, admin name, user ID, status Success.
- [ ] Login tracking: User logs in → Activity log shows "Login" entry with username, timestamp, IP address, user agent, status Success.
- [ ] Failed action tracking: User enters wrong password → Activity log shows "Login Failed" entry with username, IP, error message.
- [ ] Update tracking with changes: Admin updates company name from "Acme Inc" to "Acme Corp" → Activity log shows "Update Company" entry → Click to view details → Changes diff shows before: "Acme Inc", after: "Acme Corp".
- [ ] Filter by action type: Select "Login" filter → Table shows only login activities → Select additional "Create" → Shows both Logins and Creates.
- [ ] Filter by user: Start typing user name in user filter → Autocomplete shows matching users → Select user → Table shows only that user's activities.
- [ ] Filter by date range: Select "Last 7 Days" → Table shows activities from past week → Select custom range (Jan 1 - Jan 31) → Shows activities in that range.
- [ ] Filter by entity type: Select "Transportation Request" → Shows only activities related to transportation requests.
- [ ] Search functionality: Type "john@example.com" in search → Sees all activities by John → Type "192.168." → Sees activities from that IP range.
- [ ] Combined filters: Apply user filter + date range + action type → Results match ALL filters (AND logic) → Clear filters → Back to all activities.
- [ ] Pagination: Load log with 100+ entries → Shows 25 per page → Click page 2 → Loads next 25 → Change page size to 50 → Shows 50 entries.
- [ ] Sorting: Click "Timestamp" column → Sorts oldest first → Click again → Back to newest first → Click "User" column → Sorts alphabetically.
- [ ] Detail panel: Click on Update activity → Panel opens → Shows all details including changes diff → Click outside or close button → Panel closes.
- [ ] Copy to clipboard: In detail panel, click copy button next to request ID → ID copied to clipboard → Toast shows "Copied to clipboard".
- [ ] Export - small dataset: Apply filter showing 500 activities → Click Export CSV → Select "Filtered results" → File downloads immediately.
- [ ] Export - large dataset: Select all activities (10,000+) → Click Export Excel → Toast shows "Export started, you'll receive an email" → Receives email with download link.
- [ ] Authorization: Login as non-admin user → Navigate to /admin/activity-log → Redirected or shown 403 Forbidden.
- [ ] Real-time updates (if implemented): Admin viewing log → Another admin creates user → New activity appears at top of table within 30 seconds (if auto-refresh enabled).
- [ ] Sensitive data protection: Admin updates user password → Activity log shows "Update User" → Detail panel shows password field changed but NOT the actual password value.
- [ ] Performance with large dataset: Log has 100,000+ entries → Load log page → Loads quickly (<2 seconds) → Apply filters → Results return quickly (<1 second).
- [ ] Empty state: Fresh system with no activities → Activity log shows "No activities found" with helpful message.
- [ ] Network error: Disconnect network → Try to load log → Shows error "Failed to load activities" with "Retry" button → Reconnect → Retry → Loads successfully.
- [ ] Retention: After retention period (90 days), old activities automatically purged → Verify old activities no longer appear in log.

## Estimate

- Frontend: ~56h (XL)
- Backend: ~60h (XXL) - Includes ActivityLog entity design, automatic logging middleware, change tracking, comprehensive query endpoint with filters/search/pagination, export functionality (CSV/JSON/Excel), data sanitization, retention/archival logic, and full test coverage. Includes optional features: log integrity verification (+3h), alerting for suspicious activities (+2.5h), analytics/metrics (+2h), SIEM forwarding (+2.5h), IP geolocation (+2h).
- DevOps: ~28h (L) - Includes database migrations with optimized indexes, log retention policies, auto-purge jobs, monitoring and alerting for storage growth and performance, query caching, data privacy compliance, backup strategy, and comprehensive documentation. Includes optional database partitioning (+3h) and external SIEM integration (+3h).

**Total: ~144h (XXL)**

---

## Backend Implementation Gap Summary

### Current State
The backend has **NO implementation** of activity log functionality:
- ❌ **No ActivityLog Module** - No controllers, services, entities, or DTOs
- ❌ **No Logging Infrastructure** - No middleware, interceptors, or logging service
- ❌ **No Change Tracking** - No before/after capture for updates
- ❌ **No Log Querying** - No endpoints for viewing or filtering logs
- ❌ **No Export Functionality** - No CSV/JSON/Excel export
- ❌ **No Retention Management** - No auto-purge or archival

**Reusable Infrastructure:**
- ✅ **Authorization**: RolesGuard exists - need ADMIN-only check
- ✅ **Queue System**: Bull queue with Redis configured - can be used for async exports and auto-purge jobs
- ✅ **Email Service**: EmailService exists - can be used for export delivery

### Critical Gaps (100% Missing - Greenfield Feature)

#### 1. **Core Domain Entity (100% Missing)**
   - ❌ ActivityLog entity with 18+ fields (timestamp, user, action, entity, status, IP, changes, metadata)
   - ❌ Database migration for ActivityLog table
   - ❌ Performance-optimized indexes (userId+timestamp, action+timestamp, entityType+entityId+timestamp)
   - ❌ Composite indexes for common filter combinations

#### 2. **All API Endpoints (100% Missing - 4 Endpoints)**
   - ❌ GET /activity-log (list with filters, search, pagination)
   - ❌ GET /activity-log/:id (detail view)
   - ❌ POST /activity-log/export (CSV/JSON/Excel export)
   - ❌ DELETE /activity-log/purge (manual purge)

#### 3. **Automatic Logging Infrastructure (100% Missing)**
   - ❌ NestJS interceptor for capturing requests/responses
   - ❌ User extraction from JWT
   - ❌ IP address capture from headers
   - ❌ User agent capture
   - ❌ Request ID generation for correlation
   - ❌ Error handling (logging failures shouldn't break requests)

#### 4. **Manual Logging Service (100% Missing)**
   - ❌ ActivityLogService with log() method
   - ❌ Helper methods (logLogin, logCreate, logUpdate, logDelete, logExport)
   - ❌ User context extraction
   - ❌ System event support (no userId for scheduled jobs)
   - ❌ Type-safe logging per entity type

#### 5. **Change Tracking System (100% Missing)**
   - ❌ Before/after state capture for entities
   - ❌ Field-level diff generation
   - ❌ Changed fields extraction (exclude unchanged)
   - ❌ Sensitive field sanitization (passwords, tokens)
   - ❌ JSON storage format: { field: { before: X, after: Y } }

#### 6. **Query & Search Functionality (100% Missing)**
   - ❌ GET /activity-log with 10+ filter params
   - ❌ Dynamic query builder for filters
   - ❌ Full-text search across multiple fields
   - ❌ Pagination with total count
   - ❌ Sorting (default: timestamp DESC)
   - ❌ Search highlighting (optional)

#### 7. **Export System (100% Missing)**
   - ❌ CSV export generator with proper escaping
   - ❌ JSON export with pretty-printing
   - ❌ Excel export (optional)
   - ❌ Async export for large datasets (>1000 rows)
   - ❌ Email delivery for large exports
   - ❌ Streaming for memory efficiency
   - ❌ Export storage and download URLs

#### 8. **Data Sanitization (100% Missing)**
   - ❌ Password/token exclusion from logs
   - ❌ Sensitive data masking (credit cards, SSNs)
   - ❌ PII redaction in error messages
   - ❌ Configurable sensitive field list
   - ❌ Field-level encryption (optional)

#### 9. **Retention & Archival (100% Missing)**
   - ❌ DELETE /activity-log/purge endpoint
   - ❌ Background job for auto-purge
   - ❌ Configurable retention periods
   - ❌ Retention per action type (security events longer)
   - ❌ Archive to cold storage before purge (optional)
   - ❌ Meta-logging of purge actions

#### 10. **Performance Optimizations (100% Missing)**
   - ❌ Database indexes for common filters
   - ❌ Query result caching (5-minute TTL)
   - ❌ Max page size limits (100 per page)
   - ❌ Cursor-based pagination (optional)
   - ❌ Slow query monitoring

#### 11. **Authorization & Security (50% Missing)**
   - ✅ RolesGuard exists
   - ❌ ADMIN-only enforcement
   - ❌ Company-level filtering (multi-tenant)
   - ❌ Meta-logging (log access to logs)
   - ❌ Rate limiting on queries and exports

#### 12. **Action Definitions (100% Missing)**
   - ❌ Action enum (Login, Logout, Create, Update, Delete, Export, View, PermissionChange)
   - ❌ Controller method to action mapping
   - ❌ Log level configuration (always/conditional/never)
   - ❌ Entity-specific action definitions

#### 13. **Testing (100% Missing)**
   - ❌ Unit tests for entity and logging service
   - ❌ Unit tests for change tracking
   - ❌ Integration tests for all 4 endpoints
   - ❌ Filter combination tests
   - ❌ Authorization tests
   - ❌ Sanitization tests

#### 14. **DevOps & Infrastructure (100% Missing)**
   - ❌ Database migrations with indexes
   - ❌ Retention policy configuration
   - ❌ Auto-purge background job setup
   - ❌ Export storage (S3 or filesystem)
   - ❌ Query result caching (Redis)
   - ❌ Monitoring for storage growth
   - ❌ Alerting for purge failures
   - ❌ Data privacy compliance setup
   - ❌ Backup strategy

#### 15. **Optional Production Features (100% Missing)**
   - ❌ Log integrity verification (cryptographic signatures)
   - ❌ Suspicious activity alerting
   - ❌ Analytics and metrics
   - ❌ SIEM forwarding (Splunk/ELK/CloudWatch)
   - ❌ IP geolocation (MaxMind GeoIP)
   - ❌ Database partitioning for high-volume

### Path Forward

This is a **complete greenfield feature** requiring full-stack implementation from scratch. The backend alone is ~60 hours of work.

**Phase 1: Foundation (Critical - ~13h)**
1. Design and create ActivityLog entity (~3h)
2. Database migration with indexes (~2h)
3. Define action enum and mapping (~2h)
4. Implement automatic logging middleware/interceptor (~3h)
5. Implement manual logging service (ActivityLogService) (~2.5h)

**Phase 2: Change Tracking & Sanitization (Critical - ~5h)**
1. Add change tracking for Update actions (~3h)
2. Implement data sanitization (~2h)

**Phase 3: Query & Search (Critical - ~8h)**
1. Implement GET /activity-log endpoint with filters (~3.5h)
2. Add full-text search functionality (~2.5h)
3. Implement GET /activity-log/:id detail endpoint (~1.5h)
4. Add authorization middleware (ADMIN only) (~1.5h, partial - RolesGuard exists)

**Phase 4: Export Functionality (High Priority - ~6.5h)**
1. Build export POST /activity-log/export endpoint (~3h)
2. Implement CSV export generator (~2h)
3. Implement JSON export generator (~1.5h)

**Phase 5: Retention & Performance (Medium Priority - ~5.5h)**
1. Add retention and archival logic with purge endpoint (~2.5h)
2. Implement query performance optimizations (~2h)
3. Add rate limiting (~1h)

**Phase 6: Quality & Testing (Medium Priority - ~5.5h)**
1. Write unit tests (~2.5h)
2. Add integration tests (~3h)

**Phase 7: Optional Enhancements (~12h if included)**
1. Log integrity verification (~3h)
2. Alerting for suspicious activities (~2.5h)
3. Analytics and metrics (~2h)
4. SIEM forwarding (~2.5h)
5. IP geolocation (~2h)

**Phase 8: DevOps & Monitoring (Critical - ~16h estimated from DevOps section)**
1. Database migrations and indexes
2. Retention policy configuration
3. Auto-purge background job
4. Export storage setup
5. Query caching (Redis)
6. Monitoring and alerting
7. Data privacy compliance
8. Documentation

### Summary

**Backend Completion:** **0%** (completely greenfield)

**Total Backend Effort:** ~60 hours (base) + optional features (~12h)

**Key Challenges:**
1. **Automatic Logging** - Interceptor must not break requests even if logging fails
2. **Change Tracking** - Capture before/after state without impacting performance
3. **Storage Growth** - Activity logs grow rapidly; need retention and purge strategy
4. **Query Performance** - Must remain fast with millions of log entries
5. **Sensitive Data** - Must never log passwords, tokens, or expose PII
6. **Export Performance** - Large exports (100k+ rows) need async processing

**Dependencies:**
- Database capacity planning for log storage
- Retention policy definition (90 days default? 1 year for security events?)
- Sensitive field list (what to exclude from logging)
- Action definitions (what operations to log)
- Export storage (S3 or filesystem)

**Risk Mitigation:**
- Start with manual logging before automatic interceptor (reduces risk)
- Implement comprehensive sanitization from day 1 (prevent sensitive data leaks)
- Use Bull queue for exports (reduces 1h, existing infrastructure)
- Monitor storage growth from launch (prevent database bloat)
- Consider database partitioning early if expecting high volume (>1M logs/month)

**Compliance Considerations:**
This implementation must support:
- **GDPR**: Right to access, right to erasure, data minimization
- **HIPAA**: 6-year retention, tamper-proof logs
- **SOX**: 7-year retention, change tracking for financial data
- **PCI-DSS**: 1-year retention, cardholder data access logging

This is a large backend story (~60h base effort) requiring comprehensive audit trail infrastructure including automatic logging, change tracking, querying with complex filters, export functionality, and retention management. The complexity comes from performance requirements (fast queries on large tables), security requirements (sensitive data sanitization), and compliance requirements (retention, integrity, privacy). No existing code can be reused except infrastructure (auth guards, queues, email).

## Summary of Key Features

### Core Functionality
- **Comprehensive Activity Tracking**: Automatic logging of all significant actions (logins, creates, updates, deletes, exports, permission changes)
- **Admin Dashboard**: Paginated table with sortable columns, filters, search, and detail drill-down
- **Advanced Filtering**: Multi-dimensional filtering by action type, user, entity, status, date range
- **Full-Text Search**: Search across user names, descriptions, entities, IP addresses
- **Change Tracking**: Before/after comparison for data modifications with field-level diff viewer
- **Export Capability**: CSV, JSON, Excel export with filtered results and async processing for large datasets
- **Audit Trail**: Complete record of who did what, when, where, and why with request correlation

### Technical Highlights
- **Automatic Logging Middleware**: NestJS interceptor captures all requests automatically without manual logging code
- **Change Diff Tracking**: Automatic before/after comparison for Update actions with sanitization of sensitive fields
- **Optimized Queries**: Database indexes for common filter combinations, query result caching, pagination
- **Data Sanitization**: Never log passwords or tokens; automatic redaction of PII; configurable sensitive field list
- **Retention Management**: Automatic purge of old logs based on configurable retention policy; archive before delete
- **Performance Optimization**: Query caching, database indexing, optional partitioning for high-volume systems
- **Security**: Admin-only access, meta-logging (log access to logs), optional cryptographic signatures
- **Export Processing**: Async export for large datasets with email delivery; streaming for memory efficiency

### Production-Ready Aspects
- Comprehensive ActivityLog entity with all audit fields (user, action, entity, IP, user agent, changes, metadata)
- Automatic logging via middleware/interceptor for all state-changing operations
- Manual logging service for business logic that needs custom logging
- Database migrations with performance-optimized indexes for large tables
- Log retention policies with automatic purge and archival
- Data privacy compliance (GDPR/CCPA): PII redaction, right to erasure, data subject access
- Monitoring: storage growth, query performance, purge job execution
- Alerting: purge failures, excessive growth, slow queries
- Query result caching for repeated queries (5-minute TTL)
- Export functionality with async processing and email delivery for large datasets
- Rate limiting to prevent abuse of log queries and exports
- Comprehensive test coverage (unit and integration tests)
- Responsive design for desktop, tablet, mobile
- Full accessibility support
- Complete documentation and runbooks

### Design Decisions Needed
1. **Retention Period**: Default 90 days vs 1 year; different retention for security events vs routine operations
2. **Database Partitioning**: Implement table partitioning for high-volume systems (>1M logs/month)
3. **External SIEM**: Integrate with external security monitoring (Splunk, DataDog, ELK) or keep logs internal only
4. **Log Integrity**: Implement cryptographic signatures for tamper-proof logs (required for legal compliance in some industries)
5. **Real-Time Updates**: WebSocket vs polling for auto-refresh of activity log table
6. **IP Geolocation**: Include geographic location resolution for IP addresses (requires MaxMind or similar service)
7. **Change Granularity**: Log all field changes vs only significant changes to reduce log volume
8. **Archival Strategy**: Archive to S3 Glacier vs delete permanently after retention period

### Risks & Dependencies
- **Storage Growth**: Activity logs can grow rapidly; need monitoring and retention policies to prevent database bloat
- **Query Performance**: Large log tables (millions of rows) can slow down queries; need proper indexing and optional partitioning
- **Sensitive Data Exposure**: Risk of accidentally logging passwords, tokens, PII; need comprehensive sanitization rules
- **Compliance Requirements**: Different industries have different audit log requirements (HIPAA, SOX, PCI-DSS)
- **Logging Failures**: Logging infrastructure failure could lose audit trail; need error handling and fallbacks
- **Performance Impact**: Logging on every request can impact performance; need async logging and optimization
- **Database Capacity**: Need to plan for log storage growth based on expected user activity volume
- **Export Performance**: Large exports (100k+ rows) can timeout or consume excessive memory; need streaming and async processing

### Optional Enhancements (Not Included in Base Estimate)
- Log integrity verification with cryptographic signatures (+3h backend, compliance requirement)
- Alerting for suspicious activity patterns (+2.5h backend, security feature)
- Activity analytics dashboard with charts (+2h backend, +6h frontend)
- SIEM forwarding integration (+2.5h backend, +3h DevOps, enterprise feature)
- IP geolocation with country/city display (+2h backend, +1h frontend)
- Database partitioning for high-volume systems (+3h DevOps, performance optimization)
- Custom retention policies per action type (+2h backend, advanced feature)
- Activity replay/rollback functionality (+8h backend, +4h frontend, advanced feature)
- Advanced search with boolean operators and regex (+3h backend, +2h frontend)
- Scheduled log exports and reports (+4h backend, +2h frontend)

### Compliance Considerations
- **GDPR**: Right to access (export user's activities), right to erasure (delete on account deletion), data minimization (don't log unnecessary PII)
- **HIPAA**: Audit trail requirements, log retention (6 years), tamper-proof logs
- **SOX**: Financial data change tracking, segregation of duties logging, retention (7 years)
- **PCI-DSS**: Access to cardholder data logging, log review requirements, retention (1 year)
- **CCPA**: Consumer data access rights, deletion requirements

This Activity Log implementation provides a comprehensive audit trail system suitable for regulatory compliance, security monitoring, and operational troubleshooting.