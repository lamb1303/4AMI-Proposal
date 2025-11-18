# File: stories/06-admin-asset-management.md

# Story 6: Admin – Asset Management

## Context

**Figma URL:**
https://www.figma.com/design/JDoPGdZ6anmqLy7YFI9sXp/4ami-Dashboard?node-id=977-1476

**Story goal (from PRD + Figma)**
Enable 4AMI admins to manage assets through a comprehensive CRUD interface, including manual creation, bulk import via CSV/Excel files, filtering/searching, and table-based management. Admins must be able to create, view, edit, and delete assets with proper validation, error handling, and feedback throughout all operations.

## UX / Product

**Main user flows (from Figma)**
- [ ] **View asset list**: Admin lands on "Manage Assets" page with table showing all assets (Industry, Asset Type, Make, Model columns), filters, pagination, and action buttons
- [ ] **Create asset manually**: Admin clicks "Create New Asset" button, fills form with Industry (dropdown), Subject Asset Type, Make, Model, Length/Width/Height (meter units), Weight (pound unit), Special Transportation Consideration (optional), Year of Manufacture, then clicks Create
- [ ] **Import assets via file**: Admin clicks "Import Asset Data" button, views instructions and downloads template, drags/drops or selects CSV/Excel file, sees upload progress, handles success/error states
- [ ] **Filter assets**: Admin uses filter dropdowns (Industries All, Asset All, Make All, Model All), adds custom filters, clears filters, adjusts rows per page
- [ ] **Edit asset**: Admin clicks edit icon on asset row, form pre-populated, makes changes, saves or discards
- [ ] **Delete asset**: Admin clicks delete icon on asset row, confirms deletion, sees success feedback
- [ ] **Sort table columns**: Admin clicks sort icons on Industry, Asset Type, Make, Model column headers
- [ ] **Select multiple assets**: Admin uses checkboxes to select assets for bulk operations (if supported)

**States to support**
- [ ] **Loading**: Skeleton loaders for table rows, loading spinner for form submission, progress bar for file upload
- [ ] **Error**: Upload errors (file format, validation failures), form validation errors (field-level and summary), API errors (network, server), delete confirmation errors
- [ ] **Empty/edge**: Empty asset list (no assets message), no search/filter results, file upload area (drag and drop state), form with empty fields
- [ ] **Success**: Asset created successfully, asset updated successfully, asset deleted successfully, file imported successfully, upload progress completion

## Frontend

**Screens / components**
- [ ] `AssetManagementListView`: Main page with header ("Manage Assets"), breadcrumbs, action buttons, filters, table, pagination
- [ ] `AssetForm`: Create/edit form with all fields (Industry dropdown, Subject Asset Type, Make, Model, Length/Width/Height/Weight inputs, Special Transportation Consideration, Year of Manufacture), Create/Discard Changes/Cancel buttons
- [ ] `AssetTable`: Sortable table with Select (checkbox), Industry, Asset Type, Make, Model, Action (Edit/Delete icons) columns, row selection, alternating row colors
- [ ] `AssetFilters`: Filter bar with Industries dropdown, Asset dropdown, Make dropdown, Model dropdown, Add Filter button, Clear Filter button
- [ ] `ImportAssetModal`: Modal/page with instructions, template download button, drag-and-drop file upload area, Upload button
- [ ] `UploadProgress`: Progress indicator showing file name, size, percentage, Cancel button
- [ ] `AssetFormValidation`: Field-level and form-level validation messages, error states

**Frontend tasks**
- [ ] Create `AssetManagementListView` component with header, breadcrumbs, and layout structure (~2h)
- [ ] Implement action buttons section ("Import New Asset", "Import Asset Data") with proper styling and routing (~1.5h)
- [ ] Build `AssetFilters` component with Industries, Asset, Make, Model dropdowns, Add Filter, Clear Filter buttons (~3h)
- [ ] Implement rows per page selector dropdown with state management (~1h)
- [ ] Create `AssetTable` component with Select, Industry, Asset Type, Make, Model, Action columns (~2.5h)
- [ ] Add table row selection (checkbox) functionality with select all/deselect all (~2h)
- [ ] Implement column sorting (Industry, Asset Type, Make, Model) with sort indicators (~2h)
- [ ] Add table pagination component with page navigation and page size controls (~2h)
- [ ] Create `AssetForm` component with all form fields (Industry dropdown, Subject Asset Type, Make, Model, Length/Width/Height/Weight, Special Transportation Consideration, Year of Manufacture) (~3h)
- [ ] Implement form validation (required fields, numeric validation for dimensions/weight/year, format validation) (~2.5h)
- [ ] Add form state management (controlled inputs, form submission, reset, discard changes) (~2h)
- [ ] Create Create/Discard Changes/Cancel button handlers with proper navigation (~1h)
- [ ] Build `ImportAssetModal` component with instructions section and template download button (~2h)
- [ ] Implement drag-and-drop file upload area with visual feedback (hover states, file preview) (~2.5h)
- [ ] Create file upload handler with file validation (CSV/Excel formats, size limits) (~2h)
- [ ] Build `UploadProgress` component showing file name, size, progress bar, percentage, Cancel button (~2h)
- [ ] Implement upload progress tracking with real-time updates (~2h)
- [ ] Add error handling for file upload (format errors, size errors, validation errors) with error messages (~2h)
- [ ] Create success state for file import completion (~1h)
- [ ] Implement edit asset flow (pre-populate form, handle updates) (~2h)
- [ ] Add delete asset confirmation modal/dialog (~1.5h)
- [ ] Implement delete asset handler with success feedback (~1h)
- [ ] Add loading states (skeleton loaders for table, loading spinners for forms) (~2h)
- [ ] Implement empty states (no assets message, no filter results) (~1.5h)
- [ ] Add error states (API errors, network errors, validation errors) with user-friendly messages (~2h)
- [ ] Integrate with asset APIs (GET list, POST create, PATCH update, DELETE) using React Query or similar (~2.5h)
- [ ] Implement client-side filtering and search functionality (~2h)
- [ ] Add responsive design for mobile/tablet views (~2h)
- [ ] Implement accessibility features (keyboard navigation, ARIA labels, screen reader support) (~2h)
- [ ] Add form persistence (save draft to localStorage, restore on page reload) (~1.5h)

## Backend

**APIs / endpoints**
- [ ] `GET /admin/assets`: List all assets with filtering (industry, asset type, make, model), sorting, pagination, search – Status: partial – Est: 3h
  **Current:** GET `/assets` exists (assets.controller.ts:44) with pagination and projectId filter. **Gap:** (1) No /admin prefix, (2) No @Roles(ADMIN) guard, (3) No filtering by industry/asset_type/make/model (only projectId), (4) No sorting parameters, (5) No search functionality. CreateAssetDto has generic fields (name, type) not matching spec (industry, make, model, dimensions).
- [ ] `POST /admin/assets`: Create new asset with validation – Status: partial – Est: 3h
  **Current:** POST `/assets` exists (assets.controller.ts:37). **Gap:** (1) No /admin prefix, (2) No @Roles(ADMIN) guard, (3) CreateAssetDto doesn't match spec - has name/type/value instead of industry/subject_asset_type/make/model/length/width/height/weight/year_of_manufacture, (4) No validation for dimensions/weight/year.
- [ ] `GET /admin/assets/{id}`: Get single asset details – Status: partial – Est: 1h
  **Current:** GET `/assets/:id` exists (assets.controller.ts:80). **Gap:** (1) No /admin prefix, (2) No @Roles(ADMIN) guard. Otherwise functional with permission checks.
- [ ] `PATCH /admin/assets/{id}`: Update asset with validation – Status: partial – Est: 2h
  **Current:** PATCH `/assets/:id` exists (assets.controller.ts:88). **Gap:** (1) No /admin prefix, (2) No @Roles(ADMIN) guard, (3) UpdateAssetDto doesn't match spec fields.
- [ ] `DELETE /admin/assets/{id}`: Delete asset (soft delete recommended) – Status: partial – Est: 2h
  **Current:** DELETE `/assets/:id` exists (assets.controller.ts:114) with hard delete (assetRepository.remove). **Gap:** (1) No /admin prefix, (2) No @Roles(ADMIN) guard, (3) Hard delete instead of soft delete (no deletedAt field in Asset entity), (4) No cascade checks for dependencies.
- [ ] `POST /admin/assets/import`: Bulk import assets from CSV/Excel file – Status: partial – Est: 4h
  **Current:** POST `/assets/bulk-import` exists (assets.controller.ts:122) but imports Equipment hierarchy (Industry, Asset Class, Make, Model) not individual assets. **Gap:** (1) No /admin prefix, (2) No @Roles(ADMIN) guard, (3) Different use case - creates Equipment entities with hierarchical structure, not Assets with dimensions/weight/year, (4) Returns jobId for async processing, need sync response with import summary.
- [ ] `GET /admin/assets/import/template`: Download import template file – Status: missing – Est: 1.5h
  **Gap:** No template download endpoint. Need to generate CSV/Excel template with headers (Industry, Subject Asset Type, Make, Model, Length, Width, Height, Weight, Special Transportation Consideration, Year of Manufacture) and example row.
- [ ] `GET /admin/assets/filters/options`: Get filter options (industries, asset types, makes, models) for dropdowns – Status: missing – Est: 2.5h
  **Gap:** No filters options endpoint. Need to return distinct values for: (1) industries (from Industry entity or Equipment), (2) asset types (from AssetClass entity or Equipment), (3) makes (from Make entity or Equipment), (4) models (from Model entity or Equipment). Equipment entity has these (equipment.entity.ts:20-49) with denormalized names.

**Backend tasks**
- [ ] Define Asset data model with fields: id, industry, subject_asset_type, make, model, length (decimal), width (decimal), height (decimal), weight (decimal), special_transportation_consideration (text, nullable), year_of_manufacture (integer), created_at, updated_at, deleted_at (for soft delete) – Status: partial – Est: 3h
  **Current:** Asset entity exists (asset.entity.ts) with basic fields: name, description, type, value, residualValue, status, properties (JSONB), metadata (JSONB), projectId, createdById. **Gap:** Missing spec fields: industry, subject_asset_type (vs generic "type"), make, model, length, width, height, weight, special_transportation_consideration, year_of_manufacture, deleted_at. Decision needed: extend Asset entity or use Equipment entity (which has industry/assetClass/make/model structure).
- [ ] Create database migration for assets table with proper indexes – Status: missing – Est: 2h
  **Gap:** Using synchronize:true (app.module.ts:53). Asset table created automatically. If extending Asset entity, need migration to: (1) Add missing columns (industry, make, model, length, width, height, weight, year, etc.), (2) Add deletedAt for soft delete, (3) Add indexes on industry, make, model, year for filtering/sorting.
- [ ] Implement `GET /admin/assets` endpoint with query parameters for filtering (industry, asset_type, make, model), sorting (by column, asc/desc), pagination (page, limit), search (full-text search across relevant fields) – Status: partial – Est: 3.5h
  **Current:** GET `/assets` (assets.service.ts:57-96) has pagination and projectId filter. **Gap:** (1) Add /admin route, (2) Add @Roles(ADMIN) guard, (3) Add query params for industry/asset_type/make/model filters, (4) Add sorting params (sortBy, sortOrder), (5) Add search param, (6) Update query builder to handle all filters, (7) Add full-text search across name/industry/make/model.
- [ ] Add admin authentication and authorization middleware to all asset endpoints – Status: partial – Est: 1.5h
  **Current:** JWT auth exists (@ApiBearerAuth), role-based filtering in service (userRole !== 'admin'). **Gap:** No @Roles(ADMIN) decorators on controller methods. Need to add @Roles(UserRole.ADMIN) to all admin endpoints to enforce admin-only access.
- [ ] Implement `POST /admin/assets` endpoint with request validation (required fields, data types, format validation), create asset, return created asset – Status: partial – Est: 3h
  **Current:** POST `/assets` exists (assets.service.ts:33-55). **Gap:** (1) Create AdminCreateAssetDto with spec fields, (2) Add validation: @IsString for industry/make/model, @IsNumber for length/width/height/weight, @IsInt for year, @Min/@Max for year range (e.g., 1900-current year), (3) Optional special_transportation_consideration, (4) Update service to handle new fields.
- [ ] Implement `GET /admin/assets/{id}` endpoint with asset existence check, return asset details – Status: done
  **Current:** GET `/assets/:id` (assets.service.ts:98-122) checks existence, handles permissions, returns asset with relations. Just need to add /admin route and @Roles(ADMIN).
- [ ] Implement `PATCH /admin/assets/{id}` endpoint with request validation, asset existence check, update asset, return updated asset – Status: partial – Est: 2.5h
  **Current:** PATCH `/assets/:id` (assets.service.ts:124-139) exists. **Gap:** (1) Update AdminUpdateAssetDto with spec fields, (2) Add validation for new fields, (3) Add /admin route and @Roles(ADMIN).
- [ ] Implement `DELETE /admin/assets/{id}` endpoint with soft delete (set deleted_at), or hard delete with cascade checks – Status: partial – Est: 2.5h
  **Current:** DELETE `/assets/:id` (assets.service.ts:141-150) hard deletes with assetRepository.remove. **Gap:** (1) Add deletedAt column to Asset entity, (2) Implement soft delete (set deletedAt = new Date()), (3) Update findAll to exclude deleted (WHERE deletedAt IS NULL), (4) Add cascade checks for ResidualForm relations, (5) Add /admin route and @Roles(ADMIN).
- [ ] Create file upload handler for CSV/Excel import with file validation (format, size) – Status: done
  **Current:** Bulk import endpoint uses FileInterceptor (assets.controller.ts:148) with file upload handling. File validation likely in processor.
- [ ] Implement CSV/Excel parser to extract asset data from uploaded file – Status: partial – Est: 2.5h
  **Current:** Bulk import processes CSV (assets-processor likely) for Equipment hierarchy. **Gap:** Need parser for asset-specific CSV with columns: Industry, Subject Asset Type, Make, Model, Length, Width, Height, Weight, Special Transportation Consideration, Year of Manufacture. Parse each row, validate data types, handle missing values.
- [ ] Build bulk import logic: validate each row, create assets in batch, handle errors per row, return import results (success count, error details) – Status: partial – Est: 3.5h
  **Current:** Bulk import enqueues job for async processing (assets.service.ts likely calls assetImportQueue.add). **Gap:** (1) Need sync import or return import summary, (2) Validate each row (required fields, numeric formats, year range), (3) Batch insert assets, (4) Track errors per row (row number, field, error message), (5) Return {successCount, errorCount, errors: [{row, field, message}]}.
- [ ] Implement `POST /admin/assets/import` endpoint with file upload, parsing, validation, bulk creation, return import summary – Status: partial – Est: 3h
  **Current:** POST `/assets/bulk-import` exists but for Equipment import. **Gap:** (1) Create new /admin/assets/import endpoint, (2) Use asset-specific CSV parser, (3) Return import summary instead of jobId, (4) Add @Roles(ADMIN).
- [ ] Create import template generator (CSV/Excel with headers and example row) – Status: missing – Est: 2h
  **Gap:** No template generation. Need service to: (1) Create CSV/Excel file with headers (Industry, Subject Asset Type, Make, Model, Length (meters), Width (meters), Height (meters), Weight (pounds), Special Transportation Consideration, Year of Manufacture), (2) Add example row with sample data, (3) Return file buffer or path.
- [ ] Implement `GET /admin/assets/import/template` endpoint to serve template file download – Status: missing – Est: 1h
  **Gap:** No endpoint. Create controller method: (1) Generate template using service, (2) Set headers (Content-Type: text/csv or application/vnd.openxmlformats, Content-Disposition: attachment), (3) Return file stream.
- [ ] Implement `GET /admin/assets/filters/options` endpoint to return distinct values for industries, asset types, makes, models for filter dropdowns – Status: missing – Est: 2.5h
  **Gap:** No endpoint. Need to query: (1) Distinct industries from Equipment.industryName or Industry entity, (2) Distinct asset classes from Equipment.assetClassName or AssetClass entity, (3) Distinct makes from Equipment.makeName or Make entity, (4) Distinct models from Equipment.modelName or Model entity. Return {industries: string[], assetTypes: string[], makes: string[], models: string[]}.
- [ ] Add database indexes on industry, asset_type, make, model, year_of_manufacture for performance – Status: missing – Est: 1.5h
  **Gap:** No indexes on new fields. Need migration to add: (1) Index on industry for filtering, (2) Index on make for filtering, (3) Index on model for filtering, (4) Index on year_of_manufacture for filtering/sorting, (5) Composite index on (industry, make, model) for combined filters.
- [ ] Implement audit logging for asset CRUD operations (who created/updated/deleted, when) – Status: partial – Est: 2h
  **Current:** Asset has createdById field. **Gap:** (1) Add updatedById and deletedById fields, (2) Track who performed each action, (3) Add structured logging (Winston/Pino) for: create (user, asset_id, timestamp), update (user, asset_id, changes, timestamp), delete (user, asset_id, timestamp), bulk_import (user, file_name, success_count, error_count).
- [ ] Add input sanitization and SQL injection prevention – Status: done
  **Current:** Using TypeORM parameterized queries, class-validator for DTO validation. SQL injection already prevented.
- [ ] Write unit tests for asset model, validation logic, CRUD operations – Status: missing – Est: 3.5h
  **Gap:** No test files found. Need unit tests for: (1) AdminCreateAssetDto validation (required fields, numeric ranges, year validation), (2) Asset entity field constraints, (3) Service methods (create, findAll with filters, findOne, update, remove), (4) Soft delete logic, (5) Filter parsing, (6) CSV parser, (7) Bulk import row validation.
- [ ] Write integration tests for all asset endpoints – Status: missing – Est: 4h
  **Gap:** No e2e tests. Need integration tests for: (1) GET /admin/assets with various filters/sorting/pagination, (2) POST /admin/assets with valid/invalid data, (3) GET /admin/assets/:id, (4) PATCH /admin/assets/:id, (5) DELETE /admin/assets/:id (soft delete), (6) POST /admin/assets/import with valid/invalid CSV, (7) GET /admin/assets/import/template, (8) GET /admin/assets/filters/options, (9) Authorization (non-admin access denied).
- [ ] Add error handling and proper HTTP status codes for all endpoints – Status: partial – Est: 1h
  **Current:** Basic error handling with NotFoundException, BadRequestException, ForbiddenException. **Gap:** Ensure all errors return proper status codes: 200 (success), 201 (created), 400 (validation error), 401 (unauthorized), 403 (forbidden), 404 (not found), 409 (conflict), 422 (unprocessable entity for import errors), 500 (server error).
- [ ] Implement rate limiting for asset creation/import endpoints to prevent abuse – Status: missing – Est: 1.5h
  **Gap:** No @nestjs/throttler (same gap as other stories). Need to: (1) Apply @Throttle to POST /admin/assets (e.g., 20/min), (2) Apply stricter limit to import (e.g., 5/hour), (3) Return 429 with clear message.

**Additional production-ready tasks identified:**
- [ ] Clarify Asset vs Equipment architecture – Status: missing – Est: 2h
  **Gap:** Current codebase has both Asset and Equipment entities with different purposes. Asset is generic (name, type, value), Equipment has hierarchical structure (Industry→AssetClass→Make→Model). Spec describes Equipment-like structure for assets. Decision needed: (1) Use Equipment entity for this feature and rename routes to /admin/equipment, OR (2) Extend Asset entity with Equipment-like fields, OR (3) Create relationship between Asset and Equipment (asset.equipmentId). Recommend: use Equipment entity as it matches spec structure.
- [ ] Add admin controller with /admin prefix – Status: missing – Est: 1h
  **Gap:** Current assets.controller.ts has no /admin prefix. Need to either: (1) Create admin-assets.controller.ts with @Controller('admin/assets'), OR (2) Add @Controller('admin') to existing and change to @Controller('admin/assets'). Recommend: create separate AdminAssetsController for clarity.
- [ ] Add @Roles(ADMIN) guards to all admin endpoints – Status: missing – Est: 0.5h
  **Gap:** No role decorators on asset endpoints. Add @Roles(UserRole.ADMIN) to all methods in admin controller.
- [ ] Implement soft delete globally – Status: missing – Est: 2h
  **Gap:** No soft delete infrastructure. Need to: (1) Add deletedAt to Asset entity, (2) Add @DeleteDateColumn() decorator, (3) Update findAll queries to exclude deleted (WHERE deletedAt IS NULL), (4) Option to include deleted for admins (includeDeleted param).
- [ ] Add validation for metric units – Status: missing – Est: 1h
  **Gap:** Spec mentions "meter units" for length/width/height, "pound unit" for weight. Add validation messages indicating units: "Length (meters)", validate positive numbers, reasonable ranges (e.g., 0.01-100 meters, 1-100000 pounds).
- [ ] Add cascade delete checks – Status: missing – Est: 1.5h
  **Gap:** Before deleting asset, check if it has: (1) Associated ResidualForms, (2) Associated with Project. Warn user or prevent deletion, or cascade soft delete.
- [ ] Implement search functionality – Status: missing – Est: 2h
  **Gap:** No full-text search. Need to: (1) Add search param to GET /admin/assets, (2) Search across: name, industry, make, model, type, (3) Use ILIKE for case-insensitive search (PostgreSQL), (4) Support partial matches.
- [ ] Add CSV/Excel export functionality – Status: missing – Est: 2h
  **Gap:** Import exists but no export. Add GET /admin/assets/export endpoint to: (1) Export current filtered/sorted results, (2) Generate CSV/Excel with all asset data, (3) Return file download.

## DevOps / Infra

**Config / services**
- [ ] Database migration files for assets table
- [ ] Database indexes on filterable/searchable columns
- [ ] File storage configuration for asset import files (temporary storage)
- [ ] Environment variables for file upload limits, allowed file types

**DevOps tasks**
- [ ] Create and apply database migration for assets table with all fields and constraints – Status: missing – Est: 2h
  **Gap:** Using synchronize:true. If extending Asset entity with new fields, need migration to: (1) Add columns: industry (varchar), subject_asset_type (varchar), make (varchar), model (varchar), length (decimal), width (decimal), height (decimal), weight (decimal), special_transportation_consideration (text nullable), year_of_manufacture (integer), deletedAt (timestamp nullable), (2) Add NOT NULL constraints on required fields, (3) Add CHECK constraints (year >= 1900 AND year <= current year, length/width/height/weight > 0).
- [ ] Add database indexes on industry, asset_type, make, model, year_of_manufacture columns for query performance – Status: missing – Est: 1.5h
  **Gap:** Need indexes for filtering/sorting: (1) B-tree index on industry, (2) B-tree index on make, (3) B-tree index on model, (4) B-tree index on year_of_manufacture, (5) Composite index on (industry, make, model) for combined filters, (6) Index on deletedAt for soft delete queries.
- [ ] Configure file upload storage (local filesystem or cloud storage like S3) for import files – Status: partial – Est: 1.5h
  **Current:** File upload configured with multer (file-upload.config.ts likely). **Gap:** Configure temporary storage for import files, cleanup policy, size limits. Ensure temp files deleted after processing.
- [ ] Set up environment variables for file upload configuration (max file size, allowed MIME types, storage path) – Status: partial – Est: 1h
  **Current:** Multer config exists. **Gap:** Add env vars: MAX_IMPORT_FILE_SIZE (e.g., 10MB), ALLOWED_IMPORT_MIME_TYPES (text/csv, application/vnd.ms-excel, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet), IMPORT_STORAGE_PATH.
- [ ] Configure file cleanup job/cron to remove old import files after processing – Status: missing – Est: 2h
  **Gap:** No cleanup job. Need Bull cron job or system cron to: (1) Delete files older than 24h from temp storage, (2) Run daily at off-peak hours, (3) Log cleanup results.
- [ ] Add monitoring and alerting for asset import failures, API errors, slow queries – Status: missing – Est: 2h
  **Gap:** No monitoring. Need APM integration: (1) Track asset CRUD operation success/failure rates, (2) Monitor import success rate, (3) Alert on import failures >10%, (4) Alert on slow queries >500ms, (5) Track asset growth (assets created per day).
- [ ] Set up logging aggregation for asset operations (creation, updates, deletions, imports) – Status: missing – Est: 1.5h
  **Gap:** Only console.log. Need structured logging: (1) Log asset creation with admin user, (2) Log updates with changes, (3) Log deletions with reason, (4) Log imports with file name, row count, success/error counts, (5) Ship logs to aggregation service.
- [ ] Configure rate limiting rules for asset creation and import endpoints – Status: missing – Est: 1h
  **Gap:** No rate limiting configured. Apply throttler with: (1) POST /admin/assets: 20/min per admin, (2) POST /admin/assets/import: 5/hour per admin (expensive operation), (3) Other endpoints: 60/min.
- [ ] Add database backup strategy for assets table – Status: missing – Est: 1h
  **Gap:** No asset-specific backup. Ensure database backup includes assets table, test restore procedure, document recovery process.
- [ ] Performance testing for asset list endpoint with large datasets (1000+ assets) – Status: missing – Est: 2h
  **Gap:** No load testing. Test GET /admin/assets with: (1) 1000+ assets, (2) Various filter combinations, (3) Sorting by different columns, (4) Large page sizes, (5) Identify query bottlenecks, (6) Optimize indexes based on results.

## Definition of Done

**Functional**
- [ ] Admin can view list of all assets in sortable, filterable table with pagination
- [ ] Admin can create new asset manually through form with all required fields validated
- [ ] Admin can edit existing asset with form pre-populated and validation
- [ ] Admin can delete asset with confirmation dialog
- [ ] Admin can import multiple assets via CSV/Excel file upload with progress tracking
- [ ] Admin can download import template file
- [ ] Admin can filter assets by Industry, Asset Type, Make, Model with dropdown filters
- [ ] Admin can clear filters and reset to default view
- [ ] Admin can sort table by Industry, Asset Type, Make, Model columns
- [ ] Admin can adjust rows per page (pagination size)
- [ ] All form validations work correctly (required fields, numeric formats, year validation)
- [ ] File upload validates file format (CSV/Excel) and size limits
- [ ] Bulk import handles errors gracefully (shows which rows failed and why)
- [ ] All API endpoints require admin authentication and authorization

**UX**
- [ ] Asset list page matches Figma design (header, breadcrumbs, filters, table, pagination)
- [ ] Asset form matches Figma design (all fields, labels, button styling)
- [ ] Import asset modal/page matches Figma design (instructions, template download, drag-and-drop area)
- [ ] Upload progress indicator shows file name, size, percentage, and Cancel button
- [ ] Loading states show skeleton loaders for table and spinners for form submissions
- [ ] Error states display user-friendly messages with actionable guidance
- [ ] Empty states show helpful messages when no assets or no filter results
- [ ] Success feedback appears after create, update, delete, and import operations
- [ ] Form validation shows inline error messages for each field
- [ ] Delete confirmation dialog prevents accidental deletions
- [ ] Responsive design works on mobile and tablet devices
- [ ] Keyboard navigation and screen reader support for accessibility

**QA**
- [ ] All CRUD operations tested (create, read, update, delete assets)
- [ ] File import tested with valid CSV/Excel files
- [ ] File import tested with invalid files (wrong format, missing columns, invalid data)
- [ ] Form validation tested (required fields, numeric formats, year ranges)
- [ ] Filtering and sorting tested with various combinations
- [ ] Pagination tested with different page sizes and large datasets
- [ ] Error handling tested (network errors, server errors, validation errors)
- [ ] Edge cases tested: empty asset list, single asset, very long asset names/values
- [ ] Permission testing: non-admin users cannot access asset management endpoints
- [ ] File upload tested with files exceeding size limits
- [ ] Bulk import tested with files containing duplicate assets
- [ ] Delete operation tested with assets that may have dependencies
- [ ] Browser compatibility tested (Chrome, Firefox, Safari, Edge)
- [ ] Mobile responsiveness tested on various screen sizes

## Estimate

- Frontend: ~48h (L)
- Backend: ~54h (XL) - Updated from 35h due to data model mismatch (Asset vs Equipment), missing admin routes, missing filtering/sorting/search, soft delete implementation, template generation, filter options endpoint, comprehensive validation, and production infrastructure
- DevOps: ~16h (M) - Updated from 14h due to complex migration and additional monitoring requirements

## Summary of Backend Gap Analysis

### Current State

The backend has **basic asset CRUD** but with **architecture mismatch** and **missing admin features**:
- ✅ Basic CRUD endpoints (POST, GET, PATCH, DELETE) at /assets
- ✅ Pagination support in GET /assets
- ✅ JWT authentication and role-based filtering in services
- ✅ Bulk import endpoint (POST /assets/bulk-import) for Equipment hierarchy
- ✅ Asset entity with basic fields (name, description, type, value)
- ✅ Equipment entity with hierarchical structure (Industry, AssetClass, Make, Model)
- ✅ File upload handling with FileInterceptor
- ✅ Bull queue for async processing

### Critical Gaps

**1. Asset vs Equipment Architecture Confusion (BLOCKER)**
- ❌ Spec describes Equipment-like assets (Industry, Make, Model, dimensions, weight)
- ❌ Current Asset entity is generic (name, type, value, properties JSONB)
- ❌ Current Equipment entity matches spec structure but separate use case
- ❌ Bulk import creates Equipment hierarchy, not Assets with dimensions
- **Impact:** Fundamental data model mismatch - unclear which entity to use

**2. No Admin-Specific Routes (HIGH PRIORITY)**
- ❌ Current routes: /assets (generic, not /admin/assets)
- ❌ No @Roles(ADMIN) decorators on any endpoints
- ❌ Service has role filtering but controllers don't enforce admin access
- **Impact:** Non-admin users can access endpoints meant for admins

**3. Missing Critical Fields in Asset Entity (HIGH PRIORITY)**
- ❌ Current: name, description, type, value, residualValue, status, properties, metadata
- ❌ Spec requires: industry, subject_asset_type, make, model, length, width, height, weight, special_transportation_consideration, year_of_manufacture
- **Impact:** Cannot store required data for asset management per spec

**4. No Filtering/Sorting/Search (HIGH PRIORITY)**
- ❌ GET /assets only filters by projectId
- ❌ No filtering by industry, asset_type, make, model
- ❌ No sorting parameters (sortBy, sortOrder)
- ❌ No search functionality (full-text across fields)
- **Impact:** Cannot implement filter bar and sorting from Figma

**5. Missing Endpoints (MEDIUM PRIORITY)**
- ❌ No GET /admin/assets/import/template for template download
- ❌ No GET /admin/assets/filters/options for dropdown values
- **Impact:** Cannot download template or populate filter dropdowns

**6. No Soft Delete (MEDIUM PRIORITY)**
- ❌ DELETE hard deletes (assetRepository.remove)
- ❌ No deletedAt field in Asset entity
- ❌ No cascade checks for dependencies (ResidualForm relations)
- **Impact:** Cannot recover accidentally deleted assets

**7. Validation Doesn't Match Spec (MEDIUM PRIORITY)**
- ❌ CreateAssetDto validates name/type/value, not industry/make/model/dimensions/weight/year
- ❌ No numeric validation for length/width/height/weight
- ❌ No year range validation (1900-current year)
- ❌ No unit indicators (meters, pounds)
- **Impact:** Cannot enforce spec requirements

**8. Bulk Import Mismatch (MEDIUM PRIORITY)**
- ❌ Current import creates Equipment hierarchy (Industry→AssetClass→Make→Model)
- ❌ Spec requires importing individual assets with dimensions/weight
- ❌ Returns jobId for async processing, spec wants import summary
- **Impact:** Cannot import assets as specified in Figma

**9. Missing Production Features**
- ❌ No rate limiting
- ❌ No comprehensive audit logging (only createdById)
- ❌ No structured logging for operations
- ❌ No tests (unit or e2e)
- ❌ No migrations (using synchronize:true)
- ❌ No monitoring/alerting
- ❌ No search functionality

### Architecture Decision Needed

**Option 1: Use Equipment Entity (Recommended)**
- Equipment entity already has industry/make/model structure
- Add missing fields: length, width, height, weight, special_transportation_consideration, year_of_manufacture
- Create /admin/equipment routes (or keep as /admin/assets using Equipment)
- Pros: Matches spec structure, hierarchical relationships exist
- Cons: Rename routes, update DTOs, separate from generic Asset concept

**Option 2: Extend Asset Entity**
- Add all spec fields to Asset entity
- Create relationship to Equipment (asset.equipmentId)
- Keep /admin/assets routes
- Pros: Clearer naming, Asset remains generic
- Cons: Duplicate some Equipment data, more complex queries

**Option 3: Merge Asset and Equipment**
- Consolidate into single entity with all fields
- Pros: Single source of truth
- Cons: Breaking change, complex migration

### Revised Effort Estimate

**Original estimate:** 35h
**Updated estimate:** 54h (+19h)

**Breakdown:**
- Architecture decision and entity restructuring: ~4h
- Add missing fields to Asset/Equipment entity: ~2h
- Create /admin/assets controller with @Roles guards: ~2h
- Implement filtering (industry, make, model, type): ~3h
- Implement sorting (multiple columns): ~2h
- Implement search (full-text): ~2h
- Create AdminCreateAssetDto with validation: ~2h
- Implement soft delete: ~2.5h
- Update bulk import for asset-specific CSV: ~3.5h
- Create template generation service: ~2h
- Implement template download endpoint: ~1h
- Implement filter options endpoint: ~2.5h
- Add comprehensive validation (dimensions, weight, year): ~2h
- Implement cascade delete checks: ~1.5h
- Add audit logging: ~2h
- Rate limiting: ~1.5h
- Comprehensive testing (unit + e2e): ~7.5h
- Migrations + indexes: ~3.5h
- Documentation: ~1.5h
- DevOps (monitoring, logging, file cleanup): ~7h

### Recommendation

The backend has **basic CRUD infrastructure** but needs **significant refactoring** to match spec:

**Priority 1 (Architecture - Blockers):**
1. **Decision:** Choose Asset vs Equipment entity approach (recommend: use Equipment with added fields)
2. Create /admin/assets controller with @Roles(ADMIN) guards
3. Add missing fields to chosen entity (length, width, height, weight, year, etc.)
4. Create AdminCreateAssetDto and AdminUpdateAssetDto with spec validation

**Priority 2 (Core Features):**
5. Implement filtering by industry/make/model/type
6. Implement sorting by any column
7. Implement full-text search
8. Implement soft delete with deletedAt
9. Create filter options endpoint for dropdowns
10. Create template download endpoint

**Priority 3 (Import/Export):**
11. Update bulk import to match spec (asset CSV with dimensions/weight)
12. Return import summary instead of jobId
13. Add CSV/Excel template generation
14. Optional: Add export functionality

**Priority 4 (Production-ready):**
15. Add rate limiting
16. Add comprehensive audit logging
17. Add structured logging for operations
18. Comprehensive testing (unit + e2e)
19. Create migrations and disable synchronize:true
20. Add monitoring and alerting

**Critical Decision Point:**
Before proceeding, clarify whether:
- Asset management = managing Equipment entities (with industry/make/model hierarchy)
- Asset management = separate Assets entity linked to Equipment
- Asset management = generic Assets with Equipment-like fields

**Estimate: 54h to build admin asset management** with filtering, sorting, search, soft delete, import/export, validation, and production readiness. The main effort is in resolving the Asset vs Equipment architecture and adding missing filtering/sorting/search infrastructure.
