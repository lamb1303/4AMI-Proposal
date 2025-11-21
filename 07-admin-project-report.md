# File: stories/07-admin-project-report.md

# Story 7: Admin – Project Report

## Context

**Figma URL:**  
https://www.figma.com/design/uKXM3ydEdoSU1TwMaBPKhc/4ami-Dashboard--copia-?node-id=2629-8606&t=4WL8Z3qHAQ0FStna-0

**Story goal (from PRD + Figma)**  
Give 4AMI admins a dedicated workspace to review all submitted projects, monitor data readiness, and export finished deliverables. MVP scope includes browsing a paginated table of projects, filtering by metadata, inspecting per-project summary cards (data availability + processing timeline), previewing raw JSON responses, and downloading PDF/Excel reports.

## UX / Product

**Main user flows (from Figma)**  
- [ ] **Landing on Project Management Module**: Admin opens page with breadcrumbs, header text, filters, and table listing multiple projects with checkbox selection.
- [ ] **Apply filters/search**: Admin toggles quick filters (status, industry, owner), adds advanced filters via “Add Filter”, clears filters, and adjusts rows-per-page control.
- [ ] **Sort/paginate table**: Admin uses column sort icons and pagination controls to move between result pages.
- [ ] **Inspect project summary**: Selecting a row reveals cards listing each report artifact (Valuation Workbook, Market Comps, Executive Summary) with Available/Unavailable badges.
- [ ] **Review processing details**: Admin reads timeline entries (Project Start, Submitted, Reviewed) and stats (total data sources, analysis status).
- [ ] **Read JSON response**: Admin opens card CTA to inspect structured JSON returned by the pipeline for debugging.
- [ ] **Download PDF/Excel**: Admin checks desired formats (PDF report, Excel data) and triggers download/export.
- [ ] **Handle unavailable sections**: Admin sees badges that highlight missing documents and can follow up with analysts.

**States to support**
- [ ] **Loading**: Skeleton rows for table, shimmer cards for detail panel, disabled actions while data fetches.
- [ ] **Error**: Inline banner/toast on failed API calls, per-card error placeholder, download failure dialog.
- [ ] **Empty/edge**: “No projects found” message after filters, default empty dataset state with CTA to reset filters, cards showing “Not available yet”.
- [ ] **Success**: Populated table, badges showing Available/Completed, snackbar on successful download/export.
- [ ] **Processing**: Status chips for “Processing”, “Queued”, “Failed” plus disabled downloads until completed.

## Frontend

**Screens / components**  
- [ ] `ProjectReportListView`: layout shell with header, breadcrumbs, main content.
- [ ] `ProjectReportFilters`: quick filters, “Add filter”, “Clear filter”, rows-per-page selector.
- [ ] `ProjectReportTable`: selectable rows, sortable columns, action buttons.
- [ ] `ProjectSummaryCards`: Data Availability + Processing Details cards.
- [ ] `ReportDownloadCard`: JSON preview CTA, PDF/Excel checkboxes, download trigger.
- [ ] `ReportStatusBadge`: badge component with Available/Unavailable/Processing/Failed states.
- [ ] `ReportEmptyState` + skeleton loaders.

**Frontend tasks**
- [ ] Build `ProjectReportListView` shell (header, breadcrumb trail, container spacing) (~1.5h)
- [ ] Implement quick filters dropdown (status/industry) with selected value chips (~2h)
- [ ] Add “Add Filter” composable control (field/operator/value) with multi-row support (~2.5h)
- [ ] Implement “Clear Filter” action to reset state and refetch data (~1h)
- [ ] Create rows-per-page selector component wired to query params/local storage (~1.5h)
- [ ] Build `ProjectReportTable` with sticky header and alternating row styles (~2.5h)
- [ ] Add column sorting icons and update API query params accordingly (~2h)
- [ ] Implement checkbox selection logic (select all, indeterminate state, per-row) (~2h)
- [ ] Wire action buttons column (View Details, Generate) with disabled states per status (~1.5h)
- [ ] Integrate React Query/RTK Query for list fetch with caching + error handling (~2.5h)
- [ ] Build `ProjectSummaryCards` (Data Availability, Processing Details) with grid layout (~2h)
- [ ] Render per-document badging (Available/Unavailable/Processing) with color tokens (~1.5h)
- [ ] Implement timeline component for Project Start/Submited/Reviewed/Analysis Status (~1.5h)
- [ ] Create JSON preview modal/drawer with syntax highlighting + copy button (~2h)
- [ ] Build `ReportDownloadCard` with PDF/Excel checkboxes and validation before submit (~2h)
- [ ] Add download state management (spinners, success toast, error alert) (~1.5h)
- [ ] Implement skeleton loaders for table + cards and show while fetching (~1.5h)
- [ ] Implement empty states (illustration + reset filters CTA) (~1.5h)
- [ ] Add accessibility (keyboard trap in modal, table semantics, ARIA labels) (~2h)
- [ ] Write component/unit tests covering filters, table selection, detail cards, downloads (~2.5h)

## Backend

**APIs / endpoints**
- [ ] `GET /admin/project-reports`: paginated list with filters (status, industry, owner, submitted range, analysis status) + sorting. **Status: missing** | Est: 3h
- [ ] `GET /admin/project-reports/{id}`: returns detail payload (section availability, processing timeline, totals). **Status: missing** | Est: 2.5h
- [ ] `GET /admin/project-reports/{id}/json`: streams latest JSON analysis payload for selected project. **Status: missing** | Est: 2h
- [ ] `POST /admin/project-reports/{id}/exports`: accepts `{ formats: ['pdf','excel'] }`, queues export, returns job id + status. **Status: missing** | Est: 3h
- [ ] `GET /admin/project-reports/{id}/exports/{jobId}`: poll export completion + signed URLs. **Status: missing** | Est: 2h

**Note:** Current implementation has `/reports` endpoints (not `/admin/project-reports`) with basic CRUD and report generation, but missing admin-specific filters, export job system, JSON streaming, and section availability features.

**Backend tasks**
- [ ] Extend report schema/DTOs to include per-section availability flags + processing timestamps (~2h) **Status: missing** | Est: 2h
- [ ] Add repository query builder for list endpoint (filters, sorting, pagination) (~2.5h) **Status: partial** | Est: 2h | *Basic pagination exists in ReportsService.findAll, but missing filters for industry, owner, submitted range, analysis status, and sorting capabilities*
- [ ] Implement `GET /admin/project-reports` controller/service with admin auth + response mapper (~2h) **Status: missing** | Est: 2h | *Current implementation uses `/reports` path, needs admin-specific route and advanced filtering*
- [ ] Implement `GET /admin/project-reports/{id}` combining project meta + report stats (~2h) **Status: missing** | Est: 2h | *Current `/reports/:id` doesn't include section availability or processing timeline*
- [ ] Create serializer for timeline entries (start/submitted/reviewed/completed) (~1.5h) **Status: missing** | Est: 1.5h
- [ ] Implement JSON payload streaming with storage adapter + permission checks (~2h) **Status: missing** | Est: 2h
- [ ] Build export request handler validating formats + deduplicating in-flight jobs (~2.5h) **Status: missing** | Est: 2.5h
- [ ] Implement background worker to generate PDF/Excel, upload to storage, persist job result (~3h) **Status: partial** | Est: 2h | *ReportProcessor exists with Bull queue but only generates placeholder JSON, not actual PDF/Excel files; missing storage upload*
- [ ] Add polling endpoint returning job status + signed URLs (~2h) **Status: missing** | Est: 2h
- [ ] Cache dropdown metadata (distinct industries/statuses) in Redis for filters (~1.5h) **Status: missing** | Est: 1.5h | *Redis config exists but no caching implementation*
- [ ] Add audit logging + metrics events for downloads/JSON views (~1.5h) **Status: missing** | Est: 1.5h
- [ ] Rate limit export + JSON endpoints to prevent abuse (~1h) **Status: missing** | Est: 1h
- [ ] Unit tests for services (filters, serializers, job creation) (~2.5h) **Status: missing** | Est: 2.5h | *No report-specific tests found*
- [ ] Integration tests hitting list/detail/json/export endpoints (~3h) **Status: missing** | Est: 3h
- [ ] Seed scripts/factories for QA data with varied statuses (~2h) **Status: missing** | Est: 2h | *No report/project seeders found*
- [ ] Add admin role guard to protect admin-specific endpoints (~1h) **Status: missing** | Est: 1h | *Roles guard exists but not applied to admin project report routes*
- [ ] Implement storage service integration (S3/GCS) for report files (~2h) **Status: missing** | Est: 2h | *Currently using local filesystem*
- [ ] Add signed URL generation for secure downloads (~1.5h) **Status: missing** | Est: 1.5h
- [ ] Add comprehensive error handling middleware (~1h) **Status: missing** | Est: 1h
- [ ] Add request validation DTOs for all endpoints (~1.5h) **Status: partial** | Est: 1h | *Basic DTOs exist but missing export format validation and filter DTOs*

## DevOps / Infra

**Config / services**
- [ ] Background queue/worker for exports.
- [ ] Object storage (S3/GCS) for PDF/Excel + JSON payloads.
- [ ] Observability for report API + job metrics.
- [ ] Secret management for storage + queue credentials.

**DevOps tasks**
- [ ] Provision queue (Redis/Bull/SQS) + worker deployment with retry/backoff (~2h)
- [ ] Configure worker autoscaling + concurrency tuned for PDF generation (~1.5h)
- [ ] Create storage bucket + IAM policy + lifecycle rules (auto-delete after N days) (~2h)
- [ ] Add dashboards/alerts for failed jobs, slow queries, high error rate (~2h)
- [ ] Configure API gateway timeouts, gzip, caching headers for list/detail endpoints (~1.5h)
- [ ] Add structured logging + trace ids for report APIs/exports (~1h)
- [ ] Update CI/CD pipelines to run new tests + migrations before deploy (~1h)
- [ ] Document env vars (REPORTS_BUCKET, EXPORT_QUEUE_URL, EXPORT_TTL) in ops runbook (~1h)

## Definition of Done

**Functional**
- [ ] Admin sees paginated, filterable, sortable list of projects.
- [ ] Selecting a project renders summary + processing cards.
- [ ] PDF and/or Excel exports can be requested and downloaded.
- [ ] Raw JSON responses are viewable/downloadable per project.
- [ ] Filters, search, and pagination behave as designed.
- [ ] Error, empty, loading, and processing states behave per UX specs.

**UX**
- [ ] Layout, spacing, colors, and typography match Figma across desktop/tablet.
- [ ] Filter dropdown placements, table density, and badge colors match design tokens.
- [ ] Detail cards consume exact structure shown in Figma (labels vs values, availability badges).
- [ ] Download/JSON interactions follow Figma (checkboxes + CTA hierarchy).
- [ ] Loading/empty/error visuals align with Figma references.
- [ ] Experience is accessible (keyboard + screen reader support).

**QA**
- [ ] Automated tests cover filtering, sorting, selection, exports, and detail endpoints.
- [ ] Manual QA verifies exports contents for multiple sample projects.
- [ ] Performance validated with ≥1k projects and concurrent export jobs.
- [ ] Permission tests confirm only admins reach these endpoints.
- [ ] Regression tests ensure download links expire per retention policy.

## Estimate

- Frontend: ~44h (L)
- Backend: ~38h (L) → **Revised: ~46h (L)** (original estimate + 5 additional production-ready tasks @ ~8h)
- DevOps: ~14h (M)

---

## Backend Implementation Gap Summary

### Current State
The backend has a basic reports module (`/reports`) with:
- ✅ **Report Entity**: Basic schema with status, data, metadata, file paths
- ✅ **CRUD Operations**: Create, read, update, delete reports
- ✅ **Background Worker**: Bull queue processor for async report generation (ReportProcessor)
- ✅ **Basic Pagination**: Simple page/limit support in findAll
- ✅ **Basic Download**: Single file download via `/reports/:id/download`
- ✅ **Infrastructure**: Redis config exists, roles guard available

### Critical Gaps

#### 1. **Admin-Specific Routes (100% Missing)**
   - Current routes use `/reports` instead of `/admin/project-reports`
   - Missing admin role enforcement on routes
   - No admin-specific filtering or response shaping

#### 2. **Advanced Filtering & Querying (90% Missing)**
   - ❌ Filter by status, industry, owner, submitted date range, analysis status
   - ❌ Column sorting capabilities
   - ❌ Redis-cached dropdown metadata for filters
   - ✅ Basic pagination exists but limited

#### 3. **Export Job System (100% Missing)**
   - ❌ Multi-format export endpoint (PDF + Excel)
   - ❌ Export job deduplication
   - ❌ Job polling endpoint with status tracking
   - ❌ Signed URL generation for secure downloads
   - ⚠️ Worker exists but only creates JSON placeholders, not real PDFs/Excel

#### 4. **JSON Streaming (100% Missing)**
   - ❌ Dedicated JSON payload viewing endpoint
   - ❌ Storage adapter integration (S3/GCS)
   - ❌ Permission checks for data access

#### 5. **Section Availability & Timeline (100% Missing)**
   - ❌ Per-section availability flags (Valuation, Market Comps, Executive Summary)
   - ❌ Processing timeline serializer (Start → Submitted → Reviewed → Completed)
   - ❌ Data readiness indicators

#### 6. **Production Readiness (100% Missing)**
   - ❌ Rate limiting on export/JSON endpoints
   - ❌ Audit logging for downloads and views
   - ❌ Comprehensive error handling
   - ❌ Metrics/observability events
   - ❌ Storage service integration (currently local filesystem only)

#### 7. **Testing & QA (100% Missing)**
   - ❌ Unit tests for report services
   - ❌ Integration tests for admin endpoints
   - ❌ Seed data for QA with varied project/report statuses

### Path Forward

**High Priority (Blocking MVP):**
1. Create `/admin/project-reports` controller with admin guards (~2h)
2. Implement advanced filtering in service layer (~2h)
3. Add section availability to report schema/DTOs (~2h)
4. Build export job system with format validation (~2.5h)
5. Add export polling endpoint (~2h)
6. Implement JSON streaming endpoint (~2h)
7. Create timeline serializer (~1.5h)

**Medium Priority (Production Quality):**
1. Integrate cloud storage (S3/GCS) (~2h)
2. Add signed URL generation (~1.5h)
3. Implement Redis caching for filters (~1.5h)
4. Add rate limiting (~1h)
5. Add audit logging (~1.5h)
6. Enhance background worker for PDF/Excel (~2h)

**Low Priority (Quality & Maintenance):**
1. Write unit tests (~2.5h)
2. Write integration tests (~3h)
3. Create seed scripts (~2h)
4. Add comprehensive error handling (~1h)

**Total Remaining Effort:** ~46 hours (revised from 38h original estimate)