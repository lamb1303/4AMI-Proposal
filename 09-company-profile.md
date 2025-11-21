# File: stories/09-company-profile.md

# Story 9: Company Profile

## Context

**Figma URL:**  
https://www.figma.com/design/yiCfEo9ZDgLyIkSiK7NVP2/4ami-Dashboard--copia-?node-id=2890-26012&t=dwNhFJQ5EbJ3AdrU-0

**Story goal (from PRD + Figma)**
Enable company administrators to view and manage their company's profile information, including business details, contact information, address, and settings. The flow must support read-only profile viewing for reference, inline editing with validation, save confirmation with optimistic UI updates, cancel/discard flow with unsaved changes warning, and proper error handling for validation failures and network issues. All changes must be tracked for audit purposes and restricted to authorized users only.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – Profile view: User navigates to company profile page, sees read-only view of all company information organized in sections (Company Details, Contact Information, Business Address, Tax & Legal), with "Edit Profile" button prominently displayed.
- [x] Step 2 – Enter edit mode: User clicks "Edit Profile" button, form fields become editable inline or form switches to edit mode, all current values pre-populated, "Save Changes" and "Cancel" buttons appear, edit button is hidden.
- [x] Step 3 – Modify company information: User updates any combination of fields: company name, email, phone (with country code selector), address (street, city, state, ZIP, country), website URL, industry (dropdown), company type (dropdown), tax ID, logo upload (optional).
- [x] Step 4 – Save changes: User clicks "Save Changes" button, form validates all fields client-side, shows loading state on save button and disables form, sends update request to backend, handles success with confirmation toast and transitions back to view mode, or shows inline error messages for validation failures.
- [x] Step 5 – Cancel/discard flow: User clicks "Cancel" button while in edit mode, if no changes were made, immediately returns to view mode, if changes were made, shows confirmation modal asking "Discard unsaved changes?", user can choose "Keep Editing" (stay in edit mode) or "Discard" (abandon changes and return to view mode).
- [x] Step 6 – View mode refresh: After successful save, profile view updates with new values using optimistic UI update, success toast notification displays briefly ("Company profile updated successfully"), user can navigate away or start editing again.

**States to support**
- [x] Loading states – initial profile load with skeleton placeholders for each section, save button shows spinner during submission, form fields disabled during save operation, no navigation allowed until save completes.
- [x] Error states – inline field validation errors (invalid email format, invalid phone, invalid URL, required fields empty), server-side error messages (duplicate company name/email, database errors), network error handling with retry option, permission errors for unauthorized users.
- [x] Empty/edge states – missing optional fields show placeholder text or N/A, required fields enforce validation, partial profile data handled gracefully, logo placeholder if no logo uploaded.
- [x] Success confirmation – success toast notification with auto-dismiss after 3-5 seconds, smooth transition back to view mode with updated values, optional success animation/checkmark.

## Frontend

**Screens / components**
- [ ] `CompanyProfileView` (read-only profile display with sections, edit button, breadcrumbs) – Status: Not Started
- [ ] `CompanyProfileEdit` (editable form with all company fields, validation, save/cancel actions) – Status: Not Started
- [ ] `ProfileSection` (reusable section container with title, content, and optional edit mode) – Status: Not Started
- [ ] `DiscardChangesModal` (confirmation dialog for canceling edits with unsaved changes) – Status: Not Started
- [ ] `CompanyLogoUpload` (image upload component with preview, validation, delete option) – Status: Not Started
- [ ] `CountryCodeSelector` (phone country code dropdown, reusable from registration) – Status: Not Started
- [ ] `ProfileLoadingSkeleton` (skeleton placeholders for loading state) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/company/profile` route with layout shell (sidebar, topbar, breadcrumbs) matching Figma structure – Status: Not Started – Est: 2h
- [ ] Build `CompanyProfileView` component with read-only sections: Company Details (name, email, phone, website), Business Address (street, city, state, ZIP, country), Tax & Legal (tax ID, industry, company type), logo display – Status: Not Started – Est: 2.5h
- [ ] Implement "Edit Profile" button that toggles between view and edit modes, updates button visibility, manages component state – Status: Not Started – Est: 1.5h
- [ ] Create `ProfileLoadingSkeleton` component with skeleton placeholders matching profile sections layout for initial load state – Status: Not Started – Est: 1.5h
- [ ] Build `CompanyProfileEdit` component with editable form fields: Company Name, Email, Phone (with country code), Address, City, State, ZIP, Country, Website, Industry dropdown, Company Type dropdown, Tax ID – Status: Not Started – Est: 3h
- [ ] Integrate `CountryCodeSelector` component for phone field with flag icons, country search, proper formatting – Status: Not Started – Est: 1.5h
- [ ] Implement `CompanyLogoUpload` component: file input, image preview, drag-and-drop support, file type validation (jpg, png, max 2MB), crop/resize UI (optional), delete button – Status: Not Started – Est: 2.5h
- [ ] Add client-side validation for all fields: required field checks (name, email, phone, address, tax ID), email format validation, phone number validation, URL format for website, field-specific character limits – Status: Not Started – Est: 2.5h
- [ ] Implement inline error messages for each field with proper styling, error icons, and clear error text positioned below inputs – Status: Not Started – Est: 2h
- [ ] Create industry dropdown with async loading from GET /industries endpoint, search/filter functionality, proper loading and error states – Status: Not Started – Est: 2h
- [ ] Create company type dropdown with options loaded from enum or GET /company-types endpoint, proper selection handling – Status: Not Started – Est: 1.5h
- [ ] Implement form dirty state tracking to detect unsaved changes, manage Cancel button behavior based on dirty state – Status: Not Started – Est: 2h
- [ ] Build `DiscardChangesModal` component with title "Discard unsaved changes?", description, "Keep Editing" and "Discard" buttons, backdrop, ESC key handling – Status: Not Started – Est: 2h
- [ ] Wire cancel flow: detect form changes (dirty state), show modal if changes exist, handle Keep Editing (close modal) and Discard (reset form, return to view mode) actions – Status: Not Started – Est: 2h
- [ ] Implement save flow: disable form during submission, show loading spinner on Save button, prevent double submission, send PATCH request with changed fields only – Status: Not Started – Est: 2.5h
- [ ] Add optimistic UI update: immediately update view mode with new values on successful save, rollback to previous values on error – Status: Not Started – Est: 2h
- [ ] Implement success toast notification with "Company profile updated successfully" message, auto-dismiss after 3-5 seconds, proper positioning – Status: Not Started – Est: 1.5h
- [ ] Add error handling: display server-side validation errors (duplicate email, invalid data), network error handling with retry button, permission denied errors, timeout handling – Status: Not Started – Est: 2.5h
- [ ] Implement GET /companies/:id API integration for initial profile load with loading state, error handling, data transformation – Status: Not Started – Est: 2h
- [ ] Implement PATCH /companies/:id API integration for profile updates with request payload formatting, response handling, error mapping – Status: Not Started – Est: 2h
- [ ] Add logo upload API integration: POST /companies/:id/logo endpoint for upload, DELETE /companies/:id/logo for removal, progress indicator during upload – Status: Not Started – Est: 2.5h
- [ ] Polish responsive behavior: ensure form fields and sections adapt to tablet/mobile breakpoints, proper field stacking on smaller screens – Status: Not Started – Est: 2h
- [ ] Add accessibility features: keyboard navigation (Tab through fields), focus management (focus first error field on validation failure), ARIA labels for all inputs, screen reader announcements for save success/error – Status: Not Started – Est: 2.5h
- [ ] Implement permission checks: hide/disable Edit button for users without COMPANY_ADMIN or ADMIN roles, show read-only message for unauthorized users – Status: Not Started – Est: 1.5h

## Backend

**APIs / endpoints**
- [ ] GET `/companies/:id` – retrieve company profile by ID – **Status: partial** | Est: 1.5h | *Endpoint exists (companies.controller.ts:60-70) but missing authorization check - any authenticated user can view any company; needs to verify user.companyId === id OR user.role === ADMIN*
- [ ] PATCH `/companies/:id` – update company profile fields – **Status: partial** | Est: 3h | *Endpoint exists (companies.controller.ts:72-90) with basic update and authorization (user.companyId check). Missing: (1) validation for new fields (website, phone_extension, company_type), (2) duplicate checking for name/email changes, (3) audit logging, (4) URL/phone format validation*
- [ ] POST `/companies/:id/logo` – upload company logo image – **Status: missing** | Est: 3h | *No logo upload endpoint. File upload infrastructure exists (multer config, FilesInterceptor) but needs: logo-specific endpoint, image validation (JPG/PNG/WEBP, 2MB max), storage integration, URL generation*
- [ ] DELETE `/companies/:id/logo` – remove company logo – **Status: missing** | Est: 1.5h
- [ ] GET `/industries` – list available industries for dropdown – **Status: done** | *Endpoint exists at industries.controller.ts:39-48 with optional search param*
- [ ] GET `/company-types` – list available company types for dropdown – **Status: missing** | Est: 1.5h

**Backend tasks**
- [ ] Update Company entity with missing fields: website (string, @IsUrl), phone_extension (string, optional), company_type (enum), logoUrl (string, nullable), industryId (for dropdown) – **Status: partial** | Est: 2h | *Company entity (company.entity.ts:14-70) has: companyName, companyEmail, einTaxId, regionBranch, phone, mobile, address1, address2, city, state, zip, country. Missing: website, phone_extension, company_type, logoUrl, industryId fields*
- [ ] Create CompanyType enum with common values: LLC, Corporation, Partnership, Sole Proprietorship, Non-Profit, etc. – **Status: missing** | Est: 1h
- [ ] Implement PATCH `/companies/:id` endpoint validation: UpdateCompanyDto with optional fields, email format validation, URL validation for website, phone validation, required field preservation – **Status: partial** | Est: 2.5h | *UpdateCompanyDto (update-company.dto.ts) exists with basic validation (@IsEmail, @IsString). Missing: @IsUrl for website, phone format validation, company_type validation, phone_extension field*
- [ ] Add duplicate checking for company name and email updates: check if new name/email conflicts with other companies, skip check if value unchanged, return ConflictException for duplicates – **Status: missing** | Est: 2h | *CompaniesService.update (companies.service.ts:113-150) has NO duplicate checking; Object.assign(company, updateCompanyDto) directly without validation*
- [ ] Implement authorization logic: verify user belongs to company being updated OR user is ADMIN role, return 403 Forbidden for unauthorized access – **Status: partial** | Est: 1h | *PATCH has authorization (companies.service.ts:142-144 checks user.companyId === id). BUT GET /companies/:id (companies.service.ts:76-87) has NO authorization - any user can view any company. Need to add check in findOne()*
- [ ] Add audit logging for profile updates: log user who made change, timestamp, fields changed (before/after values), IP address – **Status: missing** | Est: 2.5h
- [ ] Implement logo upload endpoint POST `/companies/:id/logo`: accept multipart/form-data, validate file type (jpg, png, webp), validate file size (<2MB), integrate with storage service (S3 or local), generate public URL, update Company.logoUrl field – **Status: missing** | Est: 3h | *File upload infrastructure EXISTS (file-upload.config.ts with multer, FilesInterceptor used in projects). Need to: (1) create logo endpoint, (2) add image-only validation (vs current PDF/Excel/etc), (3) implement storage service abstraction, (4) add 2MB limit (vs current 10MB)*
- [ ] Add image processing for logo upload: resize to standard dimensions (e.g., 200x200), create thumbnail version (optional), optimize file size, maintain aspect ratio – **Status: missing** | Est: 2.5h
- [ ] Implement DELETE `/companies/:id/logo` endpoint: verify company ownership, delete file from storage, update Company.logoUrl to null, handle file not found gracefully – **Status: missing** | Est: 2h
- [ ] Create GET `/company-types` endpoint: return list of company type enum values with display labels, simple endpoint with static data or database-backed – **Status: missing** | Est: 1.5h
- [ ] Add rate limiting to profile update endpoint: prevent rapid repeated updates (e.g., max 10 updates per minute), apply @Throttle decorator, return 429 for exceeded limits – **Status: missing** | Est: 1.5h
- [ ] Implement field-level validation: ensure tax ID format matches country requirements, validate phone number with libphonenumber, ensure ZIP code format, validate state/province codes – **Status: partial** | Est: 2h | *EIN validation exists (register-company.dto.ts:14-18 with @Matches for XX-XXXXXXX format). Missing: phone format validation, ZIP validation, state codes, URL format. Current validation is basic @IsString/@IsEmail only*
- [ ] Add transaction support for logo upload + database update: wrap file upload and database update in transaction-like flow, rollback file upload if database update fails – **Status: missing** | Est: 2h
- [ ] Write unit tests for UpdateCompanyDto validation, duplicate checking logic, authorization checks, field transformations – **Status: missing** | Est: 2.5h | *No company tests found in test directory*
- [ ] Add integration tests for PATCH `/companies/:id`: happy path update, duplicate name/email rejection, unauthorized access (wrong company, wrong role), invalid field formats, logo upload with invalid files – **Status: missing** | Est: 3h
- [ ] Implement GET `/companies/:id` authorization: verify user belongs to company OR is ADMIN, prevent users from viewing other companies' profiles – **Status: missing** | Est: 1h | *CompaniesService.findOne (companies.service.ts:76-87) has NO authorization - directly returns company by ID. Need to add user check*
- [ ] Add response sanitization: exclude sensitive fields from API responses (internal IDs, audit fields), format phone numbers consistently, ensure null vs empty string consistency – **Status: partial** | Est: 1h | *CompanyResponseDto exists (company-response.dto.ts) but not used in controller responses (companies.controller.ts returns raw Company entity). Need to apply DTO transformation*

**Additional production-ready tasks identified:**
- [ ] Implement logo file storage service abstraction – **Status: missing** | Est: 3h | *Need storage service interface for S3/local filesystem. Projects module has file handling but no abstracted storage service*
- [ ] Add logo file cleanup job for orphaned files – **Status: missing** | Est: 2h
- [ ] Implement company profile versioning (optional) – **Status: missing** | Est: 4h
- [ ] Add validation for business rules: prevent changing company name more than X times per year, require admin approval for critical field changes (name, tax ID), flag suspicious changes – **Status: missing** | Est: 3h
- [ ] Implement cache invalidation for company profile – **Status: missing** | Est: 1.5h
- [ ] Add monitoring for logo upload failures – **Status: missing** | Est: 1h
- [ ] Create CompanyProfileResponseDto for standardized responses – **Status: partial** | Est: 0.5h | *CompanyResponseDto exists but not used in controller returns; need to apply transformation*

## DevOps / Infra

**Config / services**
- [ ] Database migrations for new Company fields (website, phone_extension, company_type, logoUrl)
- [ ] File storage service configuration (S3 or local filesystem)
- [ ] Audit logging infrastructure for profile changes
- [ ] CDN configuration for logo delivery (optional)
- [ ] Monitoring for profile update operations

**DevOps tasks**
- [ ] Create database migration for new Company fields: add website (varchar), phone_extension (varchar), company_type (enum), logoUrl (varchar) columns with proper indexes – Status: missing – Est: 2h
  **Gap:** New fields identified in spec not yet in database schema. Need migration to add columns, ensure nullable/not-null constraints correct, add indexes where needed.
- [ ] Create or update CompanyType enum in database: define enum type with values (LLC, Corporation, Partnership, Sole Proprietorship, Non-Profit), apply to company_type column – Status: missing – Est: 1.5h
  **Gap:** No company_type enum exists. For PostgreSQL, need CREATE TYPE statement. For MySQL, use ENUM column type. Ensure migration handles enum creation before column addition.
- [ ] Add database indexes for company profile queries: index on companyName for search/uniqueness, index on companyEmail for uniqueness, index on logoUrl for cleanup queries – Status: missing – Est: 1h
  **Gap:** Current schema may lack optimized indexes. Need indexes to support duplicate checking queries (SELECT WHERE name = ? AND id != ?) efficiently.
- [ ] Configure file storage service for logo uploads: set up S3 bucket with public-read ACL for logos (production), configure IAM credentials with upload/delete permissions, set up local filesystem storage for development – Status: missing – Est: 2.5h
  **Gap:** No file storage infrastructure exists. Production needs S3: create bucket, configure CORS, set lifecycle rules for orphaned files, manage credentials. Development needs local directory with proper permissions.
- [ ] Set up CDN for logo delivery (optional): configure CloudFront distribution pointing to S3 bucket, enable gzip compression, set cache headers, configure SSL certificate – Status: missing – Est: 2h
  **Gap:** Direct S3 URLs may be slow for global users. CDN improves performance and reduces S3 costs. Optional but recommended for production.
- [ ] Configure environment variables for storage: STORAGE_PROVIDER (s3 or local), S3_BUCKET_NAME, S3_REGION, AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, LOCAL_STORAGE_PATH, LOGO_BASE_URL – Status: missing – Est: 1h
  **Gap:** Need environment configuration for storage service. Different values per environment (dev uses local, prod uses S3).
- [ ] Set up audit logging infrastructure: create AuditLog or ActivityLog table (if not exists from other stories), configure log retention policy, set up log rotation, integrate with application logger – Status: missing – Est: 2h
  **Gap:** Audit logging needed for compliance. If ActivityLog from dashboard story exists, extend it. Otherwise create new audit table with fields: user_id, action, entity_type, entity_id, changes_json, ip_address, timestamp.
- [ ] Configure monitoring dashboards for company profile operations: track profile update success/failure rates, monitor logo upload success/failure, track validation error types, measure API response times – Status: missing – Est: 2h
  **Gap:** No monitoring exists. Need metrics for: PATCH /companies/:id success rate, logo upload success rate, storage errors, validation error distribution, response time p50/p95/p99.
- [ ] Set up alerting for profile update failures: alert on high error rates (>5% over 10min), alert on storage failures, alert on duplicate detection spikes, alert on slow response times (>2s p95) – Status: missing – Est: 2h
  **Gap:** No alerting configured. Need alerts for: API errors, storage service failures (S3 errors), quota warnings, performance degradation.
- [ ] Configure file upload limits: set max file size (2MB) in nginx/load balancer, configure multer max file size, set request body size limit, add rate limiting for upload endpoint – Status: missing – Est: 1.5h
  **Gap:** No upload limits configured. Need limits at multiple layers: load balancer (prevent huge uploads from reaching app), application (multer maxSize), rate limiting (prevent abuse).
- [ ] Set up log aggregation for profile updates: log all profile change attempts with user, timestamp, fields changed, configure structured logging (JSON format), integrate with log aggregation service (CloudWatch, DataDog, ELK) – Status: missing – Est: 2h
  **Gap:** Only console.log exists. Need structured logging with consistent format, include request ID for tracing, log to aggregation service for analysis.
- [ ] Create backup strategy for logo files: configure S3 versioning for logo bucket (optional), set up periodic backups of logos, document restore procedure – Status: missing – Est: 1.5h
  **Gap:** If logo files are critical, need backup strategy. S3 versioning allows rollback. Alternative: periodic backup job copying files to backup bucket.
- [ ] Set up storage quota monitoring: monitor S3 bucket size, set alerts for quota thresholds (80%, 90% full), track storage costs, configure lifecycle rules to delete orphaned files after 30 days – Status: missing – Est: 1.5h
  **Gap:** Storage can grow indefinitely. Need monitoring and cleanup. Lifecycle rules auto-delete unreferenced files to control costs.
- [ ] Configure CORS for logo uploads: set CORS headers on S3 bucket to allow uploads from frontend domain, configure allowed origins, methods (PUT, POST, DELETE), headers (Content-Type, Authorization) – Status: missing – Est: 1h
  **Gap:** Frontend needs CORS to upload directly to S3 (if using presigned URLs) or to backend upload endpoint. Configure CORS on both S3 and API server.
- [ ] Document deployment process for storage changes: document S3 bucket setup steps, document migration rollback procedure, create runbook for storage service failures – Status: missing – Est: 1.5h
  **Gap:** No documentation for DevOps team. Need runbook covering: initial S3 setup, credential rotation, disaster recovery, common troubleshooting steps.
- [ ] Set up image optimization pipeline: configure image processing service (AWS Lambda + sharp, or in-app processing), set up automatic resize/optimization on upload, configure cache headers for optimized images – Status: missing – Est: 2.5h
  **Gap:** Raw uploaded images may be large. Optimization reduces bandwidth and improves load times. Lambda function can process uploads async, or use in-app sharp processing.

## Definition of Done

**Functional**
- [ ] Authorized users (COMPANY_ADMIN, ADMIN) can view their company profile with all fields displayed correctly in read-only sections.
- [ ] Users can click "Edit Profile" button to enter edit mode, all fields become editable with current values pre-populated.
- [ ] All company information fields can be updated: company name, email, phone, phone extension, address (street, city, state, ZIP, country), website, industry, company type, tax ID.
- [ ] Logo can be uploaded, previewed, and deleted; supported formats: JPG, PNG, WEBP; max size 2MB; logo displays correctly in profile view.
- [ ] Form validates all required fields (name, email, phone, address, tax ID) and shows inline errors for invalid formats.
- [ ] Duplicate company name or email detection works and prevents saving with appropriate error messages.
- [ ] Cancel button with unsaved changes shows confirmation modal; "Discard" abandons changes, "Keep Editing" stays in edit mode.
- [ ] Cancel button without changes immediately returns to view mode without confirmation.
- [ ] Save button triggers validation, shows loading state, disables form during submission, handles success and error responses.
- [ ] Successful save updates profile view with new values (optimistic UI update), shows success toast, and returns to view mode.
- [ ] Unauthorized users (different company, non-admin roles) cannot edit or view other companies' profiles (403 Forbidden).
- [ ] All profile changes are logged to audit log with user, timestamp, and fields changed.

**UX**
- [ ] Profile layout matches Figma design: sections organized logically (Company Details, Contact Info, Business Address, Tax & Legal).
- [ ] All form fields have proper labels, placeholders, and helper text matching Figma specifications.
- [ ] Inline validation errors appear immediately below fields with clear, actionable messages and error icons.
- [ ] Loading states work correctly: skeleton placeholders on initial load, spinner on save button, disabled fields during submission.
- [ ] Edit mode transition is smooth with proper visual feedback (button text changes, fields become editable).
- [ ] "Discard unsaved changes?" modal matches Figma design with proper messaging, buttons, and backdrop.
- [ ] Success toast notification displays "Company profile updated successfully" with auto-dismiss after 3-5 seconds.
- [ ] Logo upload shows preview immediately after selection, displays upload progress, shows errors for invalid files.
- [ ] Empty optional fields show placeholder text or "N/A"; required fields show clear required indicators.
- [ ] Responsive behavior works for desktop, tablet, and mobile breakpoints; proper field stacking on smaller screens.
- [ ] All interactions feel responsive with no janky animations or layout shifts.

**QA**
- [ ] Happy path: View profile → Edit → Change multiple fields → Save → Success toast → View mode with updated values.
- [ ] Logo upload happy path: Edit → Select valid image → Preview shown → Save → Logo appears in view mode with correct URL.
- [ ] Logo deletion: Edit → Delete logo → Save → Logo removed from view mode, placeholder shown.
- [ ] Required field validation: Leave name empty → Save → Inline error "Company name is required" → Fill name → Save succeeds.
- [ ] Email format validation: Enter invalid email "test@" → Save → Error "Invalid email format" → Fix → Save succeeds.
- [ ] Phone validation: Enter invalid phone → Save → Error message → Fix → Save succeeds.
- [ ] URL validation for website: Enter "not-a-url" → Save → Error "Invalid URL format" → Enter "https://example.com" → Save succeeds.
- [ ] Duplicate name: Change name to existing company → Save → Error "Company name already exists" → Change to unique name → Save succeeds.
- [ ] Duplicate email: Change email to existing company → Save → Error "Company email already exists" → Change to unique email → Save succeeds.
- [ ] Cancel with no changes: Edit → Cancel → Immediately returns to view mode, no modal shown.
- [ ] Cancel with changes: Edit → Change name → Cancel → Modal shown "Discard unsaved changes?" → Keep Editing → Stays in edit mode → Cancel → Discard → Returns to view mode with original values.
- [ ] Logo upload validation: Select 5MB file → Error "File size exceeds 2MB limit" → Select PDF → Error "Invalid file type, use JPG/PNG/WEBP" → Select valid PNG → Upload succeeds.
- [ ] Authorization: User A tries to view User B's company profile → 403 Forbidden error.
- [ ] Authorization: CUSTOMER_ADMIN cannot edit company → Edit button hidden or disabled → Manual API call returns 403.
- [ ] Network error: Disconnect network → Save → Error "Network error, please try again" with retry button → Reconnect → Retry → Success.
- [ ] Server error: Simulate 500 error → Save → Error message "An error occurred, please try again" → User can retry.
- [ ] Concurrent update: User A saves changes → User B saves changes → Detect conflict or last-write-wins with proper feedback.
- [ ] Form persistence: Start editing → Refresh page → Changes preserved (if implemented) or warning shown before navigation.
- [ ] Accessibility: Tab through all fields in order → Focus visible → ARIA labels present → Screen reader announces errors → Success announced.
- [ ] Mobile responsiveness: All fields accessible on mobile → No horizontal scroll → Touch targets adequate size → Keyboard appears for text inputs.

## Estimate

- Frontend: ~50h (XL)
- Backend: ~51h (XL) → **Revised: ~42h (L)** (reduced from original due to existing company CRUD, file upload infrastructure, and industries endpoint)
- DevOps: ~26h (L) - Includes database migrations, S3 storage configuration, monitoring, alerting, log aggregation, and documentation. Excludes optional CDN setup (add +2h if needed).

**Total: ~127h (XXL) → Revised: ~118h (XXL)**

---

## Backend Implementation Gap Summary

### Current State
The backend has a functional companies module (`/companies`) with:
- ✅ **Company Entity**: Core schema with business details (companyName, companyEmail, einTaxId, phone, mobile, address1/2, city, state, zip, country, regionBranch)
- ✅ **GET /companies/:id**: Endpoint exists (companies.controller.ts:60-70) returning company with relations
- ✅ **PATCH /companies/:id**: Update endpoint exists (companies.controller.ts:72-90) with basic authorization (user.companyId check)
- ✅ **DTOs**: RegisterCompanyDto and UpdateCompanyDto with validation (@IsEmail, @IsString, @Matches for EIN format)
- ✅ **Authorization**: Update endpoint checks user.companyId === id before allowing changes
- ✅ **GET /industries**: Industries endpoint exists (industries.controller.ts:39-48) with search support
- ✅ **File Upload Infrastructure**: Multer config (file-upload.config.ts), FilesInterceptor, file validation exist for projects module

### Critical Gaps

#### 1. **Entity Schema (40% Missing)**
   - ✅ Has: companyName, companyEmail, einTaxId, phone, mobile, address fields
   - ❌ Missing: website, phone_extension, company_type (enum), logoUrl, industryId fields
   - ❌ Missing: CompanyType enum definition
   - ❌ Missing: industry relation (ManyToOne)

#### 2. **Authorization (50% Missing)**
   - ✅ PATCH checks user.companyId === id
   - ❌ GET /companies/:id has NO authorization check - any authenticated user can view any company
   - ❌ No ADMIN role bypass check (admins should access all companies)

#### 3. **Logo Management (100% Missing)**
   - ❌ POST /companies/:id/logo endpoint
   - ❌ DELETE /companies/:id/logo endpoint
   - ❌ Image-specific validation (2MB, JPG/PNG/WEBP only)
   - ❌ Storage service abstraction (S3/local filesystem)
   - ❌ Image processing (resize, thumbnail, optimization)
   - ⚠️ File upload infrastructure exists but not adapted for logos

#### 4. **Validation & Business Logic (70% Missing)**
   - ✅ Basic validation: @IsEmail, @IsString, @Matches for EIN format
   - ❌ No duplicate checking for company name/email on updates
   - ❌ No URL format validation for website field
   - ❌ No phone format validation (country-aware)
   - ❌ No ZIP/state code validation
   - ❌ UpdateCompanyDto missing new fields (website, phone_extension, company_type)

#### 5. **Audit & Compliance (100% Missing)**
   - ❌ No audit logging for profile changes
   - ❌ No before/after value tracking
   - ❌ No IP address logging
   - ❌ No user action tracking

#### 6. **Company Types (100% Missing)**
   - ❌ No CompanyType enum definition
   - ❌ No GET /company-types endpoint
   - ❌ No company_type field in entity/DTOs

#### 7. **Production Readiness (90% Missing)**
   - ❌ No rate limiting on update endpoint
   - ❌ No transaction support for logo operations
   - ❌ No response sanitization (CompanyResponseDto exists but not used)
   - ❌ No storage service abstraction
   - ❌ No logo file cleanup for orphaned files
   - ❌ No monitoring for failures
   - ❌ No cache invalidation

#### 8. **Testing (100% Missing)**
   - ❌ No unit tests for company services
   - ❌ No integration tests for profile updates
   - ❌ No file upload test coverage

### Path Forward

**High Priority (Blocking MVP):**
1. Add missing entity fields (website, phone_extension, company_type, logoUrl) + migration (~2h)
2. Create CompanyType enum and GET /company-types endpoint (~1.5h)
3. Add authorization to GET /companies/:id (~1h)
4. Add duplicate checking to PATCH endpoint (~2h)
5. Implement POST /companies/:id/logo endpoint with validation (~3h)
6. Implement DELETE /companies/:id/logo endpoint (~2h)
7. Add URL and phone validation to UpdateCompanyDto (~1.5h)

**Medium Priority (Production Quality):**
1. Implement storage service abstraction (S3/local) (~3h)
2. Add image processing (resize, optimize) (~2.5h)
3. Add audit logging for profile changes (~2.5h)
4. Add rate limiting to update endpoint (~1.5h)
5. Implement transaction support for logo operations (~2h)
6. Apply CompanyResponseDto to responses (~0.5h)
7. Add field-level validation (ZIP, state codes) (~1.5h)

**Low Priority (Quality & Maintenance):**
1. Write unit tests (~2.5h)
2. Write integration tests (~3h)
3. Add logo cleanup job (~2h)
4. Add monitoring (~1h)
5. Implement cache invalidation (~1.5h)
6. Add business rule validation (~3h, optional)
7. Implement profile versioning (~4h, optional)

### Summary
The company profile backend is **~35% complete**. Core CRUD operations and entity exist from registration story, providing a solid foundation. The main gaps are:
1. **Logo upload system** (endpoints, storage, processing) - ~10.5h
2. **Missing entity fields and validation** - ~5h
3. **Authorization fixes and duplicate checking** - ~3h
4. **Audit logging and compliance** - ~2.5h
5. **Testing** - ~5.5h

The file upload infrastructure already exists (multer, validation), which reduces implementation time compared to starting from scratch. The core challenge is adapting it for image-specific requirements and implementing the storage service abstraction.

**Total Remaining Effort:** ~42 hours (reduced from 51h due to existing infrastructure)

## Summary of Key Features

### Core Functionality
- **Profile Management**: View and edit company information with organized sections (Company Details, Contact Info, Business Address, Tax & Legal)
- **Logo Upload**: Full file upload workflow with validation, preview, storage, and deletion capabilities
- **Field Validation**: Comprehensive client and server-side validation for all fields with specific format requirements
- **Authorization**: Role-based access control ensuring users can only manage their own company profile
- **Audit Trail**: Complete logging of all profile changes for compliance and tracking

### Technical Highlights
- **File Storage**: Abstracted storage service supporting both S3 (production) and local filesystem (development)
- **Image Processing**: Automatic resize and optimization of uploaded logos for performance
- **Optimistic UI**: Immediate UI updates on save with rollback on error for better UX
- **Duplicate Detection**: Prevents duplicate company names/emails across the system
- **Form State Management**: Dirty state tracking with unsaved changes warning
- **Comprehensive Testing**: Unit and integration tests for all validation, authorization, and business logic

### Production-Ready Aspects
- Database migrations for schema changes
- S3 storage with lifecycle rules for orphaned file cleanup
- Monitoring dashboards for update success rates and logo upload metrics
- Alerting for failures and performance degradation
- Structured audit logging with log aggregation
- Rate limiting to prevent abuse
- Responsive design for all device sizes
- Full accessibility support (keyboard navigation, screen readers, ARIA labels)

### Design Decisions Needed
1. **Storage Provider**: Confirm S3 for production vs alternative (Google Cloud Storage, Azure Blob)
2. **Company Profile Versioning**: Decide if version history tracking is required for compliance (adds ~4h backend)
3. **CDN Setup**: Decide if CloudFront/CDN is needed for logo delivery (adds ~2h DevOps)
4. **Image Optimization**: In-app processing with sharp vs AWS Lambda for async processing
5. **Form Persistence**: Implement localStorage for unsaved changes across page refreshes (recommended for better UX, adds ~2h frontend)

### Risks & Dependencies
- **File Storage Setup**: Requires AWS account, S3 bucket creation, IAM credentials before development can proceed
- **Company Type Enum**: Need business team to provide definitive list of company type values
- **Industry Linking**: Depends on Industry entity existing and GET /industries endpoint (mentioned in registration story)
- **Audit Logging**: If not implemented in other stories, need to create AuditLog infrastructure
- **Logo Upload Library**: Need to select and integrate file upload library (multer recommended)
- **Image Processing**: Need sharp library for resize/optimization (~100MB dependency size)

### Optional Enhancements (Not Included in Estimate)
- Company profile versioning with history table (+4h backend, +1h frontend)
- CDN setup for logo delivery (+2h DevOps)
- Form auto-save with localStorage persistence (+2h frontend)
- Presigned S3 URLs for direct browser upload (+3h backend, reduces server load)
- Admin approval workflow for critical field changes (+8h full stack)
- Logo templates/guidelines UI for brand consistency (+4h frontend)