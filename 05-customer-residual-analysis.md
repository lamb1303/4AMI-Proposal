# File: stories/05-customer-residual-analysis.md

# Story 5: Customer User Residual Analysis

## Context

**Figma URL:**
https://www.figma.com/design/JDoPGdZ6anmqLy7YFI9sXp/4ami-Dashboard?node-id=3498-35229

**Story goal (from PRD + Figma)**
Enable customers to view, analyze, and understand residual value analysis for their equipment/assets. The feature provides a comprehensive view of residual analysis data through interactive charts, detailed data tables, and expandable insights sections. Customers can filter, sort, and navigate through multiple residual analysis reports, view detailed breakdowns by category (Summary, Inflation, Depreciation, Utilization, Market Data, Overview), and access actionable recommendations.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – View all residual analysis: Customer navigates to residual analysis page, sees table listing all residual analyses with columns (ID, Date, Status, Residual Value, Residual %), can filter by multiple criteria (dropdown filters, "Add Filter", "Clear Filter"), can adjust rows per page, can paginate through results.
- [x] Step 2 – View detailed analysis: Customer clicks on a residual analysis row or opens detailed view, sees tabs (Summary, Inflation, Depreciation, Utilization, Market Data, Overview), Summary tab shows "Residual Value Analysis" chart with 4 lines (Residual % High, Residual % Low, Residual Value High, Residual Value Low) over time periods (12-120 months).
- [x] Step 3 – Review data table: Customer scrolls to "Analysis Data Points" table showing month-by-month breakdown with columns (Month, Residual % High, Residual % Low, Residual Value High, Residual Value Low), can sort columns, can view all data points.
- [x] Step 4 – Explore insights: Customer expands/collapses sections (Overview, Key Findings, Market Conditions, Utilization Analysis, Recommendations, Next Steps) to read detailed insights and recommendations.
- [x] Step 5 – Navigate tabs: Customer clicks different tabs (Inflation, Depreciation, Utilization, Market Data, Overview) to see category-specific analysis and data.
- [x] Step 6 – Delete analysis: Customer selects one or more analyses via checkboxes, clicks delete button, confirms deletion, sees updated table.
- [x] Step 7 – View report: Customer clicks "View Report" button to generate/export detailed report (if applicable).

**States to support**
- [x] Loading states – skeleton loaders for table rows, chart placeholder while data loads, disabled interactions during fetch.
- [x] Error states – failed data fetch shows error message with retry option, invalid analysis ID shows not found message, network errors handled gracefully.
- [x] Empty/edge states – no residual analyses show empty state with "Create Analysis" CTA, insufficient data for chart shows placeholder message, empty filters show "No results" message.
- [x] Success states – analysis submitted successfully shows confirmation screen, data loads and displays correctly, filters apply and update results.

## Frontend

**Screens / components**
- [ ] `ResidualAnalysisListView` (table view with filters, pagination, row actions) – Status: Not Started
- [ ] `ResidualAnalysisDetailView` (detailed view with tabs, chart, data table, insights) – Status: Not Started
- [ ] `ResidualValueChart` (multi-line chart component showing residual % and value over time) – Status: Not Started
- [ ] `AnalysisDataTable` (table component for month-by-month data points with sorting) – Status: Not Started
- [ ] `ResidualAnalysisSuccess` (success confirmation screen after analysis submission) – Status: Not Started
- [ ] `FilterBar` (filter controls with multiple dropdowns, add/clear filter buttons) – Status: Not Started
- [ ] `ExpandableInsightsSection` (collapsible sections for Overview, Key Findings, Recommendations, etc.) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/customer/residual-analysis` route with layout shell (sidebar, topbar, breadcrumbs) matching Figma structure – Status: Not Started – Est: 2h
- [ ] Build `ResidualAnalysisListView` component with header, breadcrumbs, filter bar, table container matching Figma layout – Status: Not Started – Est: 2.5h
- [ ] Create `FilterBar` component with multiple filter dropdowns (Status, Date, etc.), "Add Filter" button, "Clear Filter" button, rows per page selector – Status: Not Started – Est: 2.5h
- [ ] Implement residual analysis table with columns: checkbox, ID, Date, Status, Residual Value, Residual %, Actions (delete), row click navigation, checkbox selection – Status: Not Started – Est: 3h
- [ ] Add table pagination component with page numbers, prev/next buttons, items per page selector, pagination info text – Status: Not Started – Est: 2h
- [ ] Implement filter functionality: apply filters on change, update table data, show active filter indicators, handle "Clear Filter" action – Status: Not Started – Est: 2.5h
- [ ] Build `ResidualAnalysisDetailView` component with header, breadcrumbs, tab navigation (Summary, Inflation, Depreciation, Utilization, Market Data, Overview) matching Figma – Status: Not Started – Est: 2.5h
- [ ] Create tab navigation component with active indicator, tab switching, content area for each tab – Status: Not Started – Est: 2h
- [ ] Build `ResidualValueChart` component using charting library (Chart.js/Recharts) with 4 lines (Residual % High/Low, Residual Value High/Low), time period x-axis (12-120 months), y-axes (Residual % and $), legend, tooltips – Status: Not Started – Est: 3h
- [ ] Implement chart data formatting: format currency values, format percentages, handle time period labels, ensure proper scaling – Status: Not Started – Est: 2h
- [ ] Create `AnalysisDataTable` component with columns (Month, Residual % High, Residual % Low, Residual Value High, Residual Value Low), sortable columns, row styling matching Figma – Status: Not Started – Est: 2.5h
- [ ] Build `ExpandableInsightsSection` component with collapsible sections (Overview, Key Findings, Market Conditions, Utilization Analysis, Recommendations, Next Steps), expand/collapse icons, content rendering – Status: Not Started – Est: 2.5h
- [ ] Implement tab content for each category: Summary (chart + data table + insights), Inflation/Depreciation/Utilization/Market Data/Overview (category-specific content) – Status: Not Started – Est: 2.5h
- [ ] Wire data fetching: call list API for table view, call detail API for detailed view, handle loading states with skeletons – Status: Not Started – Est: 2.5h
- [ ] Add delete functionality: handle checkbox selection, show delete confirmation modal, call delete API, update table after deletion – Status: Not Started – Est: 2h
- [ ] Implement "View Report" button: navigate to report view or trigger report generation/export (if applicable) – Status: Not Started – Est: 1.5h
- [ ] Build `ResidualAnalysisSuccess` component with success icon, title, subtitle, Continue button matching Figma design – Status: Not Started – Est: 2h
- [ ] Add empty states: no analyses message with CTA, insufficient data for chart placeholder, no results after filtering – Status: Not Started – Est: 2h
- [ ] Implement error handling: display error messages for failed API calls, network errors with retry option, invalid analysis ID handling – Status: Not Started – Est: 2h
- [ ] Add responsive behavior for table and chart views, ensure proper layout on tablet/desktop breakpoints shown in Figma – Status: Not Started – Est: 2h
- [ ] Polish accessibility: keyboard navigation, focus management, ARIA labels for tables and charts, screen reader support for data – Status: Not Started – Est: 2h

## Backend

**APIs / endpoints**
- [ ] GET `/customer/residual-analysis` – returns paginated list of customer's residual analyses with filters – Status: missing – Est: 3.5h
  **Gap:** No customer-specific residual analysis listing endpoint exists. Current endpoints: (1) POST `/ai/residual-analysis` for processing (ai.controller.ts:18), (2) GET `/reports` for generic reports (reports.controller.ts:40). Need new endpoint to: query ResidualForm by customer (via user.companyId or projects), support pagination, filtering (status, date range, residual value), sorting, return list format with ID, Date, Status, Residual Value, Residual %.
- [ ] GET `/customer/residual-analysis/:id` – returns detailed residual analysis data including chart data, data points, insights – Status: missing – Est: 4h
  **Gap:** No customer-specific detail endpoint. Need to: (1) Find ResidualForm by ID and verify customer ownership, (2) Extract/structure chart data from aiAnalysis JSONB (4 lines over 12-120 months), (3) Format data points for table (month-by-month breakdown), (4) Structure insights by sections (Overview, Key Findings, etc.), (5) Return comprehensive response with tabs data.
- [ ] DELETE `/customer/residual-analysis/:id` – deletes a residual analysis (single or bulk) – Status: missing – Est: 2.5h
  **Gap:** No delete endpoint for residual analyses. Generic DELETE `/reports/:id` exists (reports.controller.ts:129) but not for ResidualForm. Need to: (1) Verify customer ownership, (2) Delete ResidualForm record, (3) Handle cascade deletion or related data cleanup, (4) Support bulk delete if spec requires multiple selections.
- [ ] GET `/customer/residual-analysis/:id/report` – generates/returns detailed report (optional, if report export needed) – Status: partial – Est: 2.5h
  **Current:** Generic POST `/reports/generate/:projectId` exists (reports.controller.ts:102) and GET `/reports/:id/download` (reports.controller.ts:86). **Gap:** Not specific to residual analysis. Need to: (1) Generate residual-specific report from ResidualForm data, (2) Format with charts, data tables, insights, (3) Return PDF or structured export, (4) Handle report generation errors.

**Backend tasks**
- [ ] Design residual analysis data model/schema with fields: id, customer_id, analysis_date, status, residual_value, residual_percentage, created_at, updated_at, metadata – Status: partial – Est: 2.5h
  **Current:** ResidualForm entity exists (residual-form.entity.ts) with id, formData (JSONB), aiAnalysis (JSONB), isProcessed, assetId, submittedById, createdAt, updatedAt. **Gap:** Missing structured fields for listing view: (1) No analysis_date (separate from createdAt), (2) No status enum (just isProcessed boolean), (3) No residual_value extracted field, (4) No residual_percentage field, (5) No customer_id (uses submittedById, but need company association). Decision: either add fields to ResidualForm or create new ResidualAnalysis entity that references ResidualForm.
- [ ] Create database migration for residual_analyses table with indexes on customer_id, analysis_date, status for efficient queries – Status: missing – Est: 2.5h
  **Gap:** Using synchronize:true (app.module.ts:53). ResidualForm table created automatically. Need migration to: (1) Add missing columns if extending ResidualForm, OR create new residual_analyses table, (2) Add indexes on customer/company queries, (3) Add index on analysis_date for sorting, (4) Add index on status for filtering.
- [ ] Design residual analysis data points model: month, residual_percent_high, residual_percent_low, residual_value_high, residual_value_low, analysis_id (foreign key) – Status: missing – Est: 2.5h
  **Gap:** Currently aiAnalysis stores everything in JSONB. No structured table for data points. Need to: (1) Create ResidualAnalysisDataPoint entity with columns for each value, (2) Foreign key to ResidualForm or new ResidualAnalysis entity, (3) Support 12-120 month data points per analysis. Alternative: keep JSONB but add helper methods to extract/format data.
- [ ] Create database migration for residual_analysis_data_points table with foreign key to residual_analyses, index on analysis_id and month – Status: missing – Est: 2h
  **Gap:** No separate table for data points. If creating, need migration with: (1) Foreign key constraint to residual_analyses/residual_forms, (2) Index on (analysis_id, month) for fast lookups, (3) Unique constraint on (analysis_id, month) to prevent duplicates.
- [ ] Design insights/recommendations model: analysis_id, section_type (overview, key_findings, etc.), content, order_index – Status: missing – Est: 2h
  **Gap:** aiAnalysis JSONB likely contains insights but not structured. Need to: (1) Create ResidualAnalysisInsight entity with section_type enum, (2) Content field (text or JSONB), (3) order_index for section ordering, (4) Foreign key to analysis. Alternative: keep insights in JSONB with consistent structure for extraction.
- [ ] Create database migration for residual_analysis_insights table (if storing insights in DB, or use JSON field) – Status: missing – Est: 1.5h
  **Gap:** If creating separate table, need migration. If keeping JSONB, need to document expected structure and add validation.
- [ ] Implement GET `/customer/residual-analysis` endpoint with pagination (page, limit), filtering (status, date range, residual value range), sorting (date desc default), customer-scoped queries – Status: missing – Est: 4h
  **Gap:** No endpoint exists. Need to: (1) Create controller method in new CustomerResidualAnalysisController or add to existing, (2) Query ResidualForm (or new entity) filtered by customer (via user.companyId, projects, or submittedById), (3) Parse pagination params, (4) Parse filter params (status, dateFrom, dateTo, minResidualValue, maxResidualValue), (5) Build query with filters and pagination, (6) Return paginated response with total count, (7) Add @Roles guard for CUSTOMER_ADMIN/CUSTOMER_USER.
- [ ] Add filter parsing logic: parse query parameters for filters, validate filter values, build database query with filters, return filtered results – Status: missing – Est: 2.5h
  **Gap:** No filter parsing for residual analyses. Need to: (1) Create DTOs for query params (FilterResidualAnalysisDto), (2) Validate date formats, (3) Validate numeric ranges, (4) Build TypeORM query with where conditions, (5) Handle multiple filters (AND logic), (6) Return clear error messages for invalid filters.
- [ ] Implement GET `/customer/residual-analysis/:id` endpoint with authentication check, verify customer ownership, fetch analysis with all related data (data points, insights) – Status: missing – Est: 4h
  **Gap:** No endpoint. Need to: (1) Find ResidualForm by ID, (2) Verify ownership (check submittedById === user.id OR asset.projectId belongs to user's company), (3) Load related data (asset, project if needed), (4) Extract chart data from aiAnalysis JSONB, (5) Format data points, (6) Structure insights by sections, (7) Return comprehensive object with tabs structure, (8) Handle not found and unauthorized errors.
- [ ] Format chart data response: structure data points for chart library consumption, include metadata (time periods, value ranges), format currency and percentages – Status: missing – Est: 3h
  **Gap:** aiAnalysis JSONB likely has raw data. Need service methods to: (1) Extract time series data for 4 lines (Residual % High/Low, Value High/Low), (2) Format for frontend charting library (array of {month, residual_percent_high, residual_percent_low, residual_value_high, residual_value_low}), (3) Calculate min/max values for axis scaling, (4) Format currency values (USD), (5) Format percentages (0-100 with decimals), (6) Include metadata (analysis type, asset info).
- [ ] Structure insights response: organize insights by section type, include content and ordering, handle missing sections gracefully – Status: missing – Est: 2.5h
  **Gap:** Need to extract insights from aiAnalysis JSONB and structure by sections. Need to: (1) Define section types enum (Overview, KeyFindings, MarketConditions, UtilizationAnalysis, Recommendations, NextSteps), (2) Parse JSONB to extract each section, (3) Return array of {sectionType, content, order} objects, (4) Handle missing sections with empty content or default messaging, (5) Support rich text formatting if needed.
- [ ] Implement DELETE `/customer/residual-analysis/:id` endpoint with authentication, verify ownership, delete analysis and related data points/insights (cascade or explicit), return success response – Status: missing – Est: 2.5h
  **Gap:** No delete endpoint. Need to: (1) Verify customer ownership, (2) Use transaction to delete ResidualForm and related data, (3) If separate tables exist for data points/insights, cascade delete or explicit deletion, (4) Return success message, (5) Log deletion for audit trail, (6) Handle errors (not found, unauthorized, FK constraints).
- [ ] Add bulk delete support (optional): accept array of IDs, validate all belong to customer, delete in transaction, handle partial failures – Status: missing – Est: 2.5h
  **Gap:** If spec requires checkbox selection for multiple deletes, need to: (1) Accept array of IDs in request body or query params, (2) Validate all IDs exist and belong to customer, (3) Delete all in single transaction, (4) Handle partial failures (rollback or continue), (5) Return list of successful/failed deletions.
- [ ] Implement GET `/customer/residual-analysis/:id/report` endpoint (optional): generate formatted report, return PDF or structured data, handle report generation errors – Status: partial – Est: 3h
  **Current:** Report generation exists (reports.service.ts) but generic. **Gap:** Need residual-specific report: (1) Create report template for residual analysis, (2) Include chart images or data, (3) Include data tables formatted, (4) Include insights sections, (5) Generate PDF using library (puppeteer, pdfkit, or similar), (6) Store report file and return download URL, (7) Handle generation failures and timeouts.
- [ ] Add authentication middleware: verify customer JWT token, extract customer_id, ensure customer can only access their own analyses – Status: done
  **Current:** JWT auth exists (jwt.strategy.ts), @CurrentUser decorator extracts user. Just need to add ownership checks in service methods.
- [ ] Add rate limiting for analysis endpoints to prevent abuse, especially for detailed view and report generation – Status: missing – Est: 1.5h
  **Gap:** No @nestjs/throttler (same gap as other stories). Need to: (1) Apply throttler to endpoints, (2) Limit list endpoint to reasonable rate (e.g., 30/min), (3) Limit detail endpoint to 60/min, (4) Limit report generation to 5/hour (expensive operation), (5) Return 429 with retry-after header.
- [ ] Write unit tests for filter parsing, data formatting, chart data structure, insights organization – Status: missing – Est: 3h
  **Gap:** No tests for residual analysis. Need unit tests for: (1) Filter DTO validation, (2) Filter query building, (3) Chart data extraction from JSONB, (4) Data formatting (currency, percentages), (5) Insights structuring, (6) Ownership verification logic.
- [ ] Add integration tests for endpoints: list with filters/pagination, detail view, delete, ownership verification, error cases – Status: missing – Est: 3h
  **Gap:** No e2e tests. Need integration tests for: (1) GET list with pagination, (2) GET list with various filters, (3) GET detail for valid analysis, (4) GET detail unauthorized (different customer), (5) DELETE analysis, (6) DELETE unauthorized, (7) Bulk delete, (8) Report generation, (9) Empty states, (10) Invalid IDs.

**Additional production-ready tasks identified:**
- [ ] Create customer residual analysis controller – Status: missing – Est: 1.5h
  **Gap:** No dedicated controller. Need to create CustomerResidualAnalysisController or add methods to existing customer controller with @Controller('customer/residual-analysis').
- [ ] Decide on data model architecture – Status: missing – Est: 2h
  **Gap:** Decision needed: (1) Extend ResidualForm with new fields (simpler, less refactoring), OR (2) Create new ResidualAnalysis entity that references ResidualForm (cleaner separation). Consider: querying needs, data duplication, migration complexity. Recommend: extend ResidualForm for MVP, refactor later if needed.
- [ ] Add status enum for residual analyses – Status: missing – Est: 1h
  **Gap:** ResidualForm has isProcessed boolean. Need ResidualAnalysisStatus enum (e.g., PROCESSING, COMPLETED, FAILED, ARCHIVED) similar to ReportStatus enum (report-status.enum.ts).
- [ ] Extract residual values from aiAnalysis – Status: missing – Est: 2h
  **Gap:** ResidualForm stores everything in aiAnalysis JSONB. For listing view, need to: (1) Extract residualValue and residualPercentage from JSONB, (2) Store in separate columns for efficient filtering/sorting, (3) Update on AI processing completion, (4) Add migration to backfill existing records.
- [ ] Implement customer scoping strategy – Status: missing – Est: 1.5h
  **Gap:** ResidualForm has submittedById but no direct company relation. Need to: (1) Join through user.companyId, OR (2) Add companyId column to ResidualForm, OR (3) Join through asset.project.companyId. Recommend: add companyId for efficiency.
- [ ] Add caching for analysis list and details – Status: missing – Est: 2h
  **Gap:** No caching layer. Residual analyses are relatively static after processing. Need to: (1) Cache list results with key including filters/pagination, (2) Cache detail view by ID, (3) Set TTL (e.g., 5-10 minutes), (4) Invalidate on delete or update, (5) Use Redis for distributed caching.
- [ ] Implement AI analysis result parsing – Status: missing – Est: 2.5h
  **Gap:** aiAnalysis JSONB structure needs to be standardized and documented. Need to: (1) Define expected JSONB schema for AI results, (2) Create parser/transformer service, (3) Extract chart data (4 time series), (4) Extract data points (month-by-month), (5) Extract insights (6 sections), (6) Handle versioning if AI output format changes.
- [ ] Add analysis type filtering – Status: missing – Est: 1h
  **Gap:** ResidualForm has analysisType field (process-residual-analysis.dto.ts:24) but optional. Need to: (1) Make analysisType required or default to 'residual_value_analysis', (2) Add filter by analysisType in list endpoint, (3) Support different analysis types if multiple exist.

## DevOps / Infra

**Config / services**
- [ ] Database migrations for residual_analyses, residual_analysis_data_points, residual_analysis_insights tables
- [ ] Database indexes for efficient queries (customer_id, analysis_date, status, analysis_id)
- [ ] Monitoring/alerting for residual analysis endpoint performance
- [ ] Logging aggregation for analysis access patterns
- [ ] Caching strategy for analysis data (if applicable)

**DevOps tasks**
- [ ] Create and apply database migration for residual_analyses table with proper indexes on customer_id, analysis_date, status – Status: missing – Est: 2h
  **Gap:** Using synchronize:true. If extending ResidualForm, need migration to: (1) Add status column (enum), (2) Add analysisDate column, (3) Add residualValue column (extracted), (4) Add residualPercentage column, (5) Add companyId column for scoping, (6) Add indexes on (companyId, analysisDate), (companyId, status), (analysisDate DESC) for sorting. If creating new table, need full table creation migration.
- [ ] Create and apply database migration for residual_analysis_data_points table with foreign key constraints and indexes – Status: missing – Est: 2h
  **Gap:** If creating separate table for data points (instead of JSONB), need migration with: (1) Create table with all columns (month, residual_percent_high, residual_percent_low, residual_value_high, residual_value_low), (2) Foreign key to residual_forms ON DELETE CASCADE, (3) Index on (residual_form_id, month), (4) Unique constraint on (residual_form_id, month).
- [ ] Create and apply database migration for residual_analysis_insights table (if using separate table) with proper relationships – Status: missing – Est: 1.5h
  **Gap:** If creating separate insights table, need migration with: (1) section_type enum column, (2) content text/jsonb, (3) order_index integer, (4) Foreign key to residual_forms, (5) Index on residual_form_id, (6) Consider order_index for ordering within analysis.
- [ ] Add database indexes on frequently queried fields: customer_id for list queries, analysis_id for data points lookups, month for sorting – Status: missing – Est: 1.5h
  **Gap:** Need composite indexes: (1) (companyId, createdAt DESC) for customer list sorted by date, (2) (companyId, status) for filtered lists, (3) (submittedById) if querying by user, (4) (assetId) for asset-specific analyses. Monitor query performance and add as needed.
- [ ] Configure monitoring dashboards for residual analysis endpoints: response times, error rates, pagination usage, filter usage patterns – Status: missing – Est: 2h
  **Gap:** No monitoring configured. Need APM integration: (1) Track response times for list, detail, delete endpoints, (2) Monitor error rates, (3) Track pagination patterns (average page size, max page accessed), (4) Track filter usage (which filters most used), (5) Monitor report generation success rate and duration.
- [ ] Set up alerting for analysis endpoint failures, slow queries (>500ms), high error rates, unusual access patterns – Status: missing – Est: 2h
  **Gap:** No alerting. Need alerts for: (1) Endpoint error rate >5%, (2) Response time >1s p95, (3) Database query time >500ms, (4) Report generation failures >10%, (5) Unusual access patterns (spike in deletes, mass data extraction), (6) AI processing failures.
- [ ] Configure log aggregation for analysis access: log list views, detail views, filter usage, delete operations for audit trail – Status: missing – Est: 1.5h
  **Gap:** Only console.log. Need structured logging: (1) Log list queries with filters/pagination, (2) Log detail access with user and analysis ID, (3) Log deletions with user and IDs, (4) Log filter usage for analytics, (5) Log report generations, (6) Integrate with log aggregation service, (7) Retain logs for compliance.
- [ ] Document residual analysis data model, relationships, and query patterns for future reference – Status: missing – Est: 1.5h
  **Gap:** No documentation. Need runbook covering: (1) Data model diagram (entities and relationships), (2) JSONB structure for aiAnalysis, (3) Query patterns for common operations, (4) Customer scoping strategy, (5) Cache invalidation triggers, (6) Report generation process, (7) Troubleshooting guide (missing data, slow queries, AI processing failures).

## Definition of Done

**Functional**
- [ ] Customer can view list of all residual analyses in table format with correct columns (ID, Date, Status, Residual Value, Residual %).
- [ ] Filtering works: multiple filters can be applied, "Add Filter" adds new filter options, "Clear Filter" removes filters, results update correctly.
- [ ] Pagination works: page navigation, rows per page selection, pagination info displays correctly, no duplicate or missing items.
- [ ] Customer can view detailed residual analysis: click row opens detail view, tabs switch correctly, Summary tab shows chart and data table.
- [ ] Chart displays correctly: 4 lines visible (Residual % High/Low, Residual Value High/Low), axes labeled, legend shows, tooltips work on hover.
- [ ] Data table displays correctly: all columns show data, sorting works for sortable columns, month-by-month data accurate.
- [ ] Insights sections expand/collapse correctly: Overview, Key Findings, Market Conditions, Utilization Analysis, Recommendations, Next Steps all functional.
- [ ] Delete functionality works: select analyses via checkboxes, delete button removes selected items, confirmation prevents accidental deletion, table updates.

**UX**
- [ ] List view layout, spacing, typography, and table styling match Figma design exactly.
- [ ] Filter bar matches Figma: dropdown styling, button placement, rows per page selector.
- [ ] Detail view matches Figma: tab navigation, chart layout, data table styling, insights sections.
- [ ] Chart matches Figma: line colors, axis labels, legend positioning, grid lines, value formatting.
- [ ] Loading states: skeleton loaders for table, chart placeholder during load, disabled interactions.
- [ ] Error states: clear error messages with retry options, graceful handling of network failures.
- [ ] Empty states: helpful messaging when no analyses exist, insufficient data placeholders, "No results" after filtering.
- [ ] Responsive behavior works for desktop and tablet breakpoints shown in Figma.

**QA**
- [ ] Happy path: View list, apply filters, paginate, open detail view, view chart and data table, expand insights sections.
- [ ] Filter testing: Apply single filter, apply multiple filters, clear filters, test all filter types, verify results accuracy.
- [ ] Pagination testing: Navigate pages, change rows per page, verify no duplicates, verify correct total count.
- [ ] Chart testing: Verify all 4 lines render, check data accuracy, test tooltips, verify axis scaling, test with different data ranges.
- [ ] Data table testing: Verify all columns display, test sorting on sortable columns, verify month-by-month data accuracy.
- [ ] Tab navigation: Switch between all tabs, verify content loads correctly, verify active tab indicator.
- [ ] Delete testing: Select single analysis, select multiple analyses, confirm deletion, verify table updates, test error handling.
- [ ] Empty state testing: No analyses, insufficient data for chart, no results after filtering all show appropriate messages.
- [ ] Error handling: Network failures, invalid analysis ID, unauthorized access all handled gracefully with appropriate messages.

## Estimate

- Frontend: ~40h (L)
- Backend: ~52h (XL) - Updated from 30h due to missing customer-scoped endpoints, data model restructuring, chart/insights formatting, comprehensive filtering, caching, AI result parsing, and production infrastructure
- DevOps: ~14h (M) - Updated from 12h due to complex migrations and monitoring requirements

## Summary of Backend Gap Analysis

### Current State

The backend has **AI processing infrastructure** but lacks **customer viewing/analysis** capabilities:
- ✅ ResidualForm entity for storing form submissions and AI results (residual-form.entity.ts)
- ✅ POST `/ai/residual-analysis` for processing analyses (ai.controller.ts:18)
- ✅ Asset entity with residualValue field (asset.entity.ts:34)
- ✅ Generic Reports module with CRUD endpoints (reports.controller.ts)
- ✅ Report entity with status, data, download capability (report.entity.ts)
- ✅ AI processing queue with Bull (ai.processor.ts)
- ✅ JWT authentication and @CurrentUser decorator

### Critical Gaps

**1. No Customer-Scoped Endpoints (BLOCKER)**
- ❌ No GET `/customer/residual-analysis` for listing customer's analyses
- ❌ No GET `/customer/residual-analysis/:id` for detailed view
- ❌ No DELETE `/customer/residual-analysis/:id` for deletion
- ❌ Current endpoints are admin/generic (POST /ai/residual-analysis, GET /reports)
- **Impact:** Cannot view or manage residual analyses from customer perspective

**2. Data Model Not Optimized for Viewing (HIGH PRIORITY)**
- ❌ ResidualForm stores everything in aiAnalysis JSONB - not queryable/filterable
- ❌ No structured fields for listing: analysis_date, status enum, residual_value, residual_percentage
- ❌ No separate tables for data points (month-by-month) or insights (sections)
- ❌ No customer/company scoping (uses submittedById, no companyId)
- **Impact:** Cannot efficiently filter, sort, or display data without complex JSONB parsing

**3. Missing Chart Data Formatting (HIGH PRIORITY)**
- ❌ No service to extract 4 time series from aiAnalysis JSONB
- ❌ No formatting for chart library (Residual % High/Low, Value High/Low over 12-120 months)
- ❌ No data point extraction for month-by-month table
- **Impact:** Frontend cannot render chart without extensive data transformation

**4. Missing Insights Structuring (MEDIUM PRIORITY)**
- ❌ No extraction of insights from aiAnalysis by sections
- ❌ No organization by section types (Overview, Key Findings, Market Conditions, Utilization, Recommendations, Next Steps)
- **Impact:** Cannot display expandable insights sections as per Figma

**5. No Filtering/Pagination for Residual Analyses (HIGH PRIORITY)**
- ❌ No filter support (status, date range, residual value range)
- ❌ No sorting support (by date, residual value)
- ❌ No pagination for customer's analyses list
- **Impact:** Cannot implement filter bar and table controls from Figma

**6. Missing Production Features**
- ❌ No rate limiting
- ❌ No caching (analyses are relatively static after processing)
- ❌ No structured logging/audit trail
- ❌ No monitoring for endpoint performance
- ❌ No tests for residual analysis endpoints
- ❌ No migrations (using synchronize:true)
- ❌ No documentation of aiAnalysis JSONB structure

**7. Architecture Mismatch**
- Current: Processing-focused (create analysis via AI)
- Spec: Viewing/analysis-focused (list, filter, chart, insights)
- **Impact:** Fundamental use case mismatch

### Data Model Decision Needed

**Option 1: Extend ResidualForm (Recommended for MVP)**
- Add columns: status (enum), analysisDate, residualValue, residualPercentage, companyId
- Keep data points and insights in aiAnalysis JSONB
- Add helper methods to extract/format data
- Pros: Less refactoring, faster to implement
- Cons: JSONB querying limitations, data duplication

**Option 2: Create New Entities (Better Long-term)**
- Create ResidualAnalysis entity referencing ResidualForm
- Create ResidualAnalysisDataPoint entity (month-by-month)
- Create ResidualAnalysisInsight entity (sections)
- Pros: Structured, queryable, scalable
- Cons: More complex migrations, data transformation needed

### Revised Effort Estimate

**Original estimate:** 30h
**Updated estimate:** 52h (+22h)

**Breakdown:**
- Data model restructuring (add fields to ResidualForm): ~4h
- Customer listing endpoint with filters/pagination: ~4h
- Customer detail endpoint with data extraction: ~4h
- Chart data formatting service: ~3h
- Insights structuring service: ~2.5h
- Delete endpoint with ownership verification: ~2.5h
- Bulk delete support: ~2.5h
- Report generation (residual-specific): ~3h
- Filter parsing and validation: ~2.5h
- Customer scoping strategy: ~1.5h
- AI result parsing/standardization: ~2.5h
- Status enum and extraction logic: ~2h
- Caching implementation: ~2h
- Rate limiting: ~1.5h
- Comprehensive testing: ~6h
- Migrations + indexes: ~5.5h
- Documentation: ~1.5h
- DevOps (monitoring, logging): ~14h

### Recommendation

The backend has **strong AI processing** but needs **significant customer-facing development**:

**Priority 1 (Blockers - Enable Basic Viewing):**
1. Extend ResidualForm with extracted fields (status, analysisDate, residualValue, residualPercentage, companyId)
2. Create GET `/customer/residual-analysis` with basic list/pagination
3. Create GET `/customer/residual-analysis/:id` with chart data extraction
4. Implement chart data formatting from aiAnalysis JSONB

**Priority 2 (Core Features):**
5. Add filtering support (status, date range, residual value)
6. Implement insights structuring by sections
7. Create DELETE endpoint with ownership verification
8. Standardize and document aiAnalysis JSONB structure

**Priority 3 (Production-ready):**
9. Add caching for list and detail views
10. Implement rate limiting
11. Add structured logging and audit trail
12. Create migrations and disable synchronize:true
13. Comprehensive testing and monitoring

**Architecture Note:**
Current ResidualForm is processing-centric. For MVP, extend it with fields needed for customer viewing. For future scalability, consider refactoring to separate ResidualAnalysis entity with dedicated data points and insights tables.

**Estimate: 52h to build customer-facing residual analysis feature** with filtering, charting, insights, and production readiness. The main effort is in data extraction/formatting from JSONB and building customer-scoped query infrastructure.
