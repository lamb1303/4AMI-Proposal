# File: stories/03-company-registration.md

# Story 3: Company Registration

## Context

**Figma URL:**
https://www.figma.com/design/JDoPGdZ6anmqLy7YFI9sXp/4ami-Dashboard?node-id=2681-12128

**Story goal (from PRD + Figma)**
Enable 4AMI administrators to register new companies in the system with complete company information, including contact details, address, business classification, and initial system administrators. The flow must support multi-step form completion, validation, cancellation with confirmation, and success confirmation before redirecting to the dashboard.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – Registration form entry: Admin navigates to company registration form and fills out company name, email, phone (with country code selector), full address (Address, City, State, ZIP, Country), phone extension, mobile, industry (dropdown), company type (dropdown), website, and tax ID.
- [x] Step 2 – System administrators section: Admin adds one or more system administrator emails in a list format, can add additional administrators via "Add Administrator" button, and remove administrators via delete button.
- [x] Step 3 – Form submission: Admin clicks "Create" button to submit the form; form validates all required fields, shows loading state during submission, and handles success/error responses.
- [x] Step 4 – Cancel flow: Admin clicks "Discard Changes" button, sees confirmation popup asking to confirm cancellation, can choose to "Cancel" (stay on form) or "Discard" (navigate away), and if discarded, returns to dashboard with a warning toast notification.
- [x] Step 5 – Success confirmation: After successful registration, admin sees success screen with checkmark icon, success message, subtitle, and "Continue" button that navigates to dashboard or company profile.

**States to support**
- [x] Loading states – form submission button shows loading spinner, form fields disabled during submission, no navigation allowed until completion.
- [x] Error states – inline field validation errors (required fields, invalid email format, invalid phone, invalid URL), server-side error messages (duplicate company name/email, validation failures), network error handling with retry option.
- [x] Empty/edge states – empty form with placeholders, partial form completion (handle browser back/refresh), minimum one administrator required validation, empty administrator list with "Add Administrator" prompt.
- [x] Success confirmation – success screen with clear messaging, auto-redirect option after delay, manual "Continue" button for immediate navigation.

## Frontend

**Screens / components**
- [ ] `CompanyRegistrationForm` (main form container with all fields, validation, submission) – Status: Not Started
- [ ] `SystemAdministratorsList` (dynamic list of administrator emails with add/remove functionality) – Status: Not Started
- [ ] `CancelConfirmationModal` (confirmation popup for discarding changes) – Status: Not Started
- [ ] `CompanyRegistrationSuccess` (success confirmation screen with icon, message, CTA) – Status: Not Started
- [ ] `CountryCodeSelector` (phone country code dropdown component) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/admin/companies/register` route with layout shell (sidebar, topbar, breadcrumbs) matching Figma structure – Status: Not Started – Est: 2h
- [ ] Build company registration form layout with header, breadcrumbs, and form container matching Figma spacing – Status: Not Started – Est: 2h
- [ ] Implement basic form fields: Company Name, Email, Phone (with country code selector), Address, City, State, ZIP, Country with proper labels and input styling – Status: Not Started – Est: 2.5h
- [ ] Add remaining form fields: Phone Extension, Mobile, Industry (dropdown), Company Type (dropdown), Website, Tax ID with validation placeholders – Status: Not Started – Est: 2.5h
- [ ] Build `CountryCodeSelector` component with flag icons, country list, search functionality, and integration with phone input – Status: Not Started – Est: 2.5h
- [ ] Create `SystemAdministratorsList` component with table layout (Email column, Actions column), "Add Administrator" button, email input for new entries, delete button per row – Status: Not Started – Est: 2.5h
- [ ] Implement client-side validation: required field checks, email format validation, phone number validation, URL validation for website, minimum one administrator requirement – Status: Not Started – Est: 2.5h
- [ ] Add inline error messages for each field with proper styling, error state indicators, and clear error text – Status: Not Started – Est: 2h
- [ ] Implement form submission handling: disable form during submission, show loading spinner on Create button, prevent double submission – Status: Not Started – Est: 2h
- [ ] Create `CancelConfirmationModal` component with title, description, Cancel and Discard buttons, backdrop, and proper positioning – Status: Not Started – Est: 2h
- [ ] Wire cancel flow: detect form changes (dirty state), show confirmation modal on "Discard Changes" click, handle Cancel/Discard actions, navigate to dashboard on discard – Status: Not Started – Est: 2h
- [ ] Build `CompanyRegistrationSuccess` component with success icon, title, subtitle, Continue button matching Figma design – Status: Not Started – Est: 2h
- [ ] Implement success flow: redirect to success screen after successful submission, handle Continue button navigation to dashboard, optional auto-redirect after delay – Status: Not Started – Est: 1.5h
- [ ] Add error handling: display server-side error messages (duplicate company, validation errors), network error handling with retry option, error toast notifications – Status: Not Started – Est: 2h
- [ ] Implement form state persistence: save form data to localStorage on field changes, restore form state on page reload/back navigation, clear persisted data on successful submission – Status: Not Started – Est: 2h
- [ ] Add responsive behavior for form layout, ensure proper field wrapping on smaller screens, test mobile/tablet views – Status: Not Started – Est: 2h
- [ ] Polish accessibility: keyboard navigation, focus management, ARIA labels, screen reader announcements for errors and success – Status: Not Started – Est: 2h

## Backend

**APIs / endpoints**
- [ ] POST `/admin/companies` – create new company with all details and administrators – Status: partial – Est: 4h
  **Current:** POST `/companies/register` exists (companies.controller.ts:33) but is for CUSTOMER_ADMIN self-registration, not admin-initiated registration. **Gap:** (1) Need new endpoint at `/admin/companies` for ADMIN role, (2) Current endpoint only associates creator with company, doesn't accept system administrator emails list, (3) Missing fields: industry, company_type, website, phone_extension.
- [ ] GET `/admin/companies/check?name=...&email=...` – check if company name or email already exists (optional, for real-time validation) – Status: missing – Est: 2h
  **Gap:** No duplicate checking endpoint. Need endpoint to query companyName and companyEmail for uniqueness before form submission. Simple query with boolean response.

**Backend tasks**
- [ ] Design company data model/schema with fields: name, email, phone, phone_extension, mobile, address, city, state, zip, country, industry, company_type, website, tax_id, created_at, updated_at – Status: partial – Est: 2h
  **Current:** Company entity exists (company.entity.ts) with fields: companyName, companyEmail, einTaxId, regionBranch, phone, mobile, address1, address2, city, state, zip, country. **Gap:** Missing fields: (1) phone_extension, (2) industry (foreign key or enum), (3) company_type (enum or string), (4) website. Need to add these fields to entity with proper types and validation.
- [ ] Create database migration for companies table with appropriate indexes (name, email for uniqueness checks) – Status: missing – Est: 2h
  **Gap:** Using synchronize:true (app.module.ts:53) instead of migrations. No unique constraints defined on companyName or companyEmail. Need to: (1) Create migration for companies table, (2) Add unique constraints on companyName and companyEmail, (3) Add indexes for lookups, (4) Handle migration in production without synchronize.
- [ ] Design system administrators relationship: junction table or embedded array for company-administrator associations with email addresses – Status: missing – Est: 2h
  **Gap:** No system administrators handling at all. Current implementation only associates creator (CUSTOMER_ADMIN) with company via user.companyId. Need design decision: (1) Junction table (company_administrators) with company_id + user_id/email, (2) JSONB array field on companies table, (3) Separate administrators field on users table with company association. Recommend junction table for flexibility.
- [ ] Implement POST `/admin/companies` endpoint with request body validation (required fields, email format, phone format, URL format for website) – Status: partial – Est: 3h
  **Current:** POST `/companies/register` exists with RegisterCompanyDto validation (register-company.dto.ts). **Gap:** (1) Wrong role restriction (@Roles(CUSTOMER_ADMIN) instead of ADMIN), (2) Missing administrators array in DTO, (3) Missing validation for new fields (industry, company_type, website, phone_extension), (4) Need to create new AdminRegisterCompanyDto or extend existing DTO.
- [ ] Add duplicate checking logic: verify company name uniqueness, verify company email uniqueness, return appropriate error messages for conflicts – Status: missing – Est: 2h
  **Gap:** No duplicate checking in companies.service.ts register method. Currently saves company without checking if name or email exists. Need to: (1) Query database for existing companyName (case-insensitive), (2) Query for existing companyEmail, (3) Throw ConflictException with clear error message, (4) Add test cases for duplicate scenarios.
- [ ] Implement administrator email validation: validate all provided administrator emails, ensure at least one administrator is provided, check for duplicate emails in the list – Status: missing – Est: 2.5h
  **Gap:** No administrator handling exists. Need to: (1) Accept administrators: string[] in DTO, (2) Validate each email format using class-validator, (3) Check minimum 1 administrator, (4) Check for duplicate emails in array, (5) Validate emails are unique in system or create placeholder users if needed.
- [ ] Create company record in database with transaction support, handle database errors gracefully, return created company with ID – Status: done
  **Current:** companies.service.ts:52-57 creates and saves company record. Returns saved company with ID. Database errors handled by NestJS exception filters.
- [ ] Associate system administrators with company (create records in junction table or update embedded array), handle administrator creation failures – Status: missing – Est: 3h
  **Gap:** No administrator association logic. Need to: (1) After company creation, iterate through administrator emails, (2) Find or create User records for each email, (3) Set user.companyId or create junction table records, (4) Handle partial failures (e.g., invalid email after company created), (5) Consider transaction rollback strategy, (6) Send invitation emails to administrators.
- [ ] Add authentication middleware to verify admin role, ensure only authorized admins can create companies – Status: partial – Est: 0.5h
  **Current:** @Roles(CUSTOMER_ADMIN) decorator exists on register endpoint (companies.controller.ts:34). @ApiBearerAuth() requires JWT. **Gap:** Need to change to @Roles(UserRole.ADMIN) for new admin endpoint. Current endpoint is for customer self-registration, not admin-initiated.
- [ ] Implement GET `/admin/companies/check` endpoint (optional) for real-time validation: check name availability, check email availability, return boolean or availability status – Status: missing – Est: 2h
  **Gap:** No check endpoint. Need controller method: (1) Accept query params name and/or email, (2) Query database for existence, (3) Return {available: boolean} or {nameAvailable: boolean, emailAvailable: boolean}, (4) Add @Roles(ADMIN) guard, (5) Cache results briefly to reduce DB load.
- [ ] Add audit logging for company creation: log admin user, timestamp, company details for compliance and tracking – Status: missing – Est: 2h
  **Gap:** Only console.log for email failure (companies.service.ts:69). No structured audit logging. Need: (1) Create AuditLog entity or use activity logging from dashboard story, (2) Log company creation with user_id, action, company_id, timestamp, metadata, (3) Log administrator associations, (4) Log failures with reason.
- [ ] Write unit tests for company model validation, duplicate checking logic, administrator validation – Status: missing – Est: 3h
  **Gap:** No test files found for companies module. Need unit tests for: (1) RegisterCompanyDto validation (all fields, required/optional), (2) Duplicate name/email detection logic, (3) Administrator email validation, (4) Entity field constraints, (5) Service methods (register, findOne, findAll, update).
- [ ] Add integration tests for POST endpoint: happy path, duplicate name/email scenarios, missing required fields, invalid data formats, administrator validation failures – Status: missing – Est: 3h
  **Gap:** No e2e tests for companies endpoints. Need integration tests for: (1) Successful company creation with valid data, (2) Duplicate name rejection, (3) Duplicate email rejection, (4) Missing required fields (name, email, tax_id, phone, address), (5) Invalid email format, (6) Invalid URL format for website, (7) Administrator validation (empty array, invalid emails, duplicates), (8) Authorization (non-admin cannot create).

**Additional production-ready tasks identified:**
- [ ] Add unique constraints to Company entity – Status: missing – Est: 1h
  **Gap:** No @Unique decorators on companyName or companyEmail (company.entity.ts). Need to add unique constraints at database level using TypeORM decorators or migration to prevent race condition duplicates.
- [ ] Create CompanyType enum or reference table – Status: missing – Est: 2h
  **Gap:** No company_type field or enum exists. Spec mentions "company type (dropdown)" in form. Need to: (1) Decide if enum or reference table, (2) Create CompanyType enum (e.g., LLC, Corporation, Partnership, Sole Proprietorship), (3) Add to Company entity as enum type, (4) Seed initial company types, (5) Create GET /company-types endpoint.
- [ ] Link Industry entity to Company – Status: missing – Est: 1.5h
  **Gap:** Industry entity exists (industry.entity.ts) but not linked to Company. Need to: (1) Add industryId foreign key to Company entity, (2) Add @ManyToOne relation to Industry, (3) Update RegisterCompanyDto to accept industryId, (4) Add validation for valid industry ID, (5) Frontend can use GET /industries for dropdown options.
- [ ] Implement rate limiting for company creation – Status: missing – Est: 1.5h
  **Gap:** No rate limiting on company endpoints (same gap as other stories). Need to: (1) Install @nestjs/throttler, (2) Configure with sensible limits (e.g., 10 company creations per hour per admin), (3) Apply to company creation endpoint, (4) Return 429 with clear message.
- [ ] Add phone number validation library – Status: missing – Est: 2h
  **Gap:** RegisterCompanyDto has @IsString for phone/mobile (register-company.dto.ts:26-31) but no format validation. Need to: (1) Install libphonenumber-js or google-libphonenumber, (2) Create custom validator decorator, (3) Validate phone and mobile with country code, (4) Return clear error messages for invalid formats.
- [ ] Add URL validation for website field – Status: missing – Est: 0.5h
  **Gap:** Need to add website field to DTO with @IsUrl() validation from class-validator. Simple addition to RegisterCompanyDto.
- [ ] Implement transaction for company + administrators creation – Status: missing – Est: 2h
  **Gap:** Current register method doesn't use transactions. If administrator creation fails after company is created, company remains orphaned. Need to: (1) Wrap company creation + administrator associations in transaction, (2) Rollback on any failure, (3) Return appropriate error message.

## DevOps / Infra

**Config / services**
- [ ] Database migrations for companies and company_administrators tables
- [ ] Monitoring/alerting for company registration failures
- [ ] Logging aggregation for company creation events
- [ ] Database indexes for performance (name, email lookups)

**DevOps tasks**
- [ ] Create and apply database migration for companies table with proper indexes on name and email – Status: missing – Est: 2h
  **Gap:** Using synchronize:true instead of migrations. Need to: (1) Disable synchronize in production config, (2) Create initial migration for companies table with all fields, (3) Add unique constraints on companyName and companyEmail, (4) Add B-tree indexes for fast lookups, (5) Test migration rollback, (6) Document migration process.
- [ ] Create and apply database migration for company_administrators junction table (if using separate table) with foreign key constraints – Status: missing – Est: 2h
  **Gap:** No junction table exists. If design uses separate table, need migration for: (1) company_administrators table with id, company_id, user_id, email, role, created_at, (2) Foreign key to companies(id) with ON DELETE CASCADE, (3) Unique constraint on (company_id, email), (4) Index on company_id for lookups.
- [ ] Add database indexes on company name and email columns for fast uniqueness checks and lookups – Status: missing – Est: 1h
  **Gap:** No explicit indexes defined. With synchronize:true, TypeORM creates basic indexes but not optimized for uniqueness checks. Need to: (1) Add index on companyName (case-insensitive if PostgreSQL), (2) Add unique index on companyEmail, (3) Consider composite index on (name, email) for check endpoint, (4) Monitor query performance with EXPLAIN.
- [ ] Configure monitoring dashboards for company registration endpoint: success rate, error rate, response times, duplicate detection frequency – Status: missing – Est: 2h
  **Gap:** No monitoring configured (same gap as other stories). Need APM integration: (1) Track company creation success/failure rates, (2) Monitor response times, (3) Track duplicate detection frequency (important metric), (4) Alert on high failure rates, (5) Dashboard for business metrics (companies created per day).
- [ ] Set up alerting for company registration failures: alert on high error rates, alert on duplicate detection spikes, alert on slow response times (>1s) – Status: missing – Est: 2h
  **Gap:** No alerting. Need alerts for: (1) Error rate >10% over 10min, (2) Duplicate detection spike (>50% of requests), (3) Response time >1s p95, (4) Database unique constraint violations, (5) Administrator email send failures.
- [ ] Configure log aggregation for company creation events: log successful registrations, log failed attempts with reasons, track registration patterns – Status: missing – Est: 1.5h
  **Gap:** Only console.log for email failures. Need structured logging: (1) Log all company creation attempts with admin user, (2) Log success with company_id and details, (3) Log failures with reason (duplicate, validation, etc.), (4) Track registration patterns (time of day, admin user), (5) Integrate with log aggregation service.
- [ ] Document company registration flow, data model, and administrator association strategy for future reference – Status: missing – Est: 1.5h
  **Gap:** No documentation found. Need runbook covering: (1) Company registration API flow, (2) Data model and relationships, (3) Administrator association strategy (junction table or embedded), (4) Duplicate checking logic, (5) Transaction handling, (6) Troubleshooting common issues.

## Definition of Done

**Functional**
- [ ] Admin can successfully register a new company with all required fields (name, email, phone, address, industry, company type, website, tax ID).
- [ ] System administrators section allows adding multiple administrator emails, removing administrators, and enforces minimum one administrator requirement.
- [ ] Form validation prevents submission with invalid data (invalid email, phone, URL formats, missing required fields).
- [ ] Duplicate company name or email detection works and displays appropriate error messages.
- [ ] Cancel flow shows confirmation modal and properly handles discard/cancel actions.
- [ ] Success screen displays after successful registration and Continue button navigates correctly.

**UX**
- [ ] Form layout, field styling, spacing, and typography match Figma design exactly.
- [ ] All form fields have proper labels, placeholders, and helper text where shown in Figma.
- [ ] Inline validation errors appear immediately with clear, actionable messages.
- [ ] Loading states disable form appropriately during submission with visual feedback.
- [ ] Cancel confirmation modal matches Figma design with proper messaging.
- [ ] Success screen matches Figma with checkmark icon, title, subtitle, and Continue button.
- [ ] Responsive behavior works for desktop and tablet breakpoints.

**QA**
- [ ] Happy path: Complete form submission with valid data, all fields populated, multiple administrators, successful creation and redirect.
- [ ] Validation testing: Required field validation, email format validation, phone format validation, URL validation, minimum administrator requirement.
- [ ] Duplicate testing: Attempt to register company with existing name, existing email, both scenarios show appropriate errors.
- [ ] Cancel flow testing: Click discard with no changes, click discard with changes, confirm discard, cancel discard action.
- [ ] Error handling: Network failures, server errors, timeout scenarios all handled gracefully with retry options.
- [ ] Form persistence: Partial form completion persists on page refresh, clears on successful submission.
- [ ] Administrator list: Add multiple administrators, remove administrators, validate email format in administrator list.

## Estimate

- Frontend: ~33h (L)
- Backend: ~38h (XL) - Updated from 26h due to missing system administrators handling, duplicate checking, missing entity fields, audit logging, transaction support, and comprehensive testing
- DevOps: ~13h (M)

## Summary of Backend Gap Analysis

### Current State

The backend has **basic company registration infrastructure** but lacks admin-initiated registration and system administrators handling:
- ✅ Company entity with core fields (company.entity.ts)
- ✅ POST `/companies/register` endpoint for customer self-registration (companies.controller.ts:33)
- ✅ GET `/companies` (admin list), GET `/companies/:id`, PATCH `/companies/:id`
- ✅ RegisterCompanyDto with validation for most fields (register-company.dto.ts)
- ✅ Email notification on registration (companies.service.ts:63)
- ✅ @Roles auth infrastructure
- ✅ Industry entity exists (industry.entity.ts) but not linked to Company

### Critical Gaps

**1. Wrong Registration Flow (HIGH PRIORITY)**
- ❌ Current: POST `/companies/register` is for CUSTOMER_ADMIN self-registration
- ❌ Spec requires: POST `/admin/companies` for ADMIN to register companies on behalf of customers
- ❌ No way for admin to create multiple companies
- **Impact:** Fundamental flow mismatch - spec is admin-initiated, current is customer-initiated

**2. Missing System Administrators Feature (BLOCKER)**
- ❌ No way to add multiple administrator emails during registration
- ❌ No junction table or relationship for company-administrator associations
- ❌ Current only associates creator with company (1:1 instead of 1:N)
- ❌ No administrator invitation/notification system
- **Impact:** Core feature completely missing - cannot assign multiple admins to company

**3. Missing Entity Fields (MEDIUM PRIORITY)**
- ❌ No phone_extension field
- ❌ No industry relationship (Industry entity exists but not linked)
- ❌ No company_type field or enum
- ❌ No website field
- **Impact:** Cannot capture all required data from form

**4. No Duplicate Detection (HIGH PRIORITY)**
- ❌ No unique constraints on companyName or companyEmail
- ❌ No validation logic to check for duplicates before saving
- ❌ Using synchronize:true so no migrations with constraints
- ❌ Race condition possible with concurrent registrations
- **Impact:** Can create duplicate companies, violates business rules

**5. No Real-time Validation Endpoint (NICE TO HAVE)**
- ❌ No GET `/admin/companies/check` endpoint
- **Impact:** Cannot provide instant feedback on duplicate names/emails in form

**6. Missing Production Requirements**
- ❌ No audit logging (only console.log for email failure)
- ❌ No transaction support (company can be created without administrators)
- ❌ No rate limiting
- ❌ No phone number format validation (just @IsString)
- ❌ No URL validation for website
- ❌ No monitoring/alerting
- ❌ No tests
- ❌ No migrations
- ❌ No documentation

**7. Data Model Incomplete**
- ❌ No CompanyType enum or reference table
- ❌ Industry not linked to Company (missing foreign key)
- ❌ No company_administrators junction table design

### Architecture Mismatch

**Spec requires:** Admin-initiated company registration with multiple system administrators
**Current implementation:** Customer self-registration (CUSTOMER_ADMIN creates their own company)

The use case is fundamentally different:
- **Spec (Admin flow):** System admin registers company → assigns multiple customer admins → customer admins receive invitations
- **Current (Customer flow):** Customer admin creates account → registers their company → becomes sole admin

### Data Integrity Risks

1. **No unique constraints:** Duplicate company names/emails possible
2. **No transactions:** Company can be created without administrators (orphaned records)
3. **No validation:** Invalid phone numbers, URLs, email formats can be saved
4. **Using synchronize:true:** Production risk, no migration history, schema changes not tracked

### Revised Effort Estimate

**Original estimate:** 26h
**Updated estimate:** 38h (+12h)

**Breakdown:**
- Endpoint restructuring (admin vs customer flows): ~3h
- System administrators handling (junction table, associations, invitations): ~6h
- Missing entity fields (phone_extension, industry, company_type, website): ~3h
- Duplicate checking + unique constraints: ~3h
- Validation improvements (phone, URL): ~2.5h
- Transaction support: ~2h
- Audit logging: ~2h
- Real-time check endpoint: ~2h
- Testing (unit + integration): ~6h
- Migrations + indexes: ~4h
- DevOps (monitoring, logging, docs): ~4.5h

### Recommendation

The backend requires **significant refactoring** to align with spec requirements:

**Priority 1 (Blockers):**
1. Create POST `/admin/companies` endpoint for ADMIN role
2. Design and implement system administrators handling (junction table or embedded)
3. Add missing fields to Company entity (phone_extension, industry FK, company_type, website)
4. Implement duplicate checking with unique constraints

**Priority 2 (Important):**
5. Add phone number and URL validation
6. Implement transaction support for atomic company+administrators creation
7. Add migrations and disable synchronize:true

**Priority 3 (Production-ready):**
8. Audit logging for compliance
9. Rate limiting
10. Comprehensive testing
11. Monitoring and alerting

**Design Decision Needed:**
- **System Administrators Storage:** Choose between:
  1. Junction table `company_administrators` (recommended for flexibility)
  2. JSONB array on `companies` table (simpler but less queryable)
  3. Many-to-many through `users` table (current approach, extend to N:M)

The current implementation serves customer self-registration use case. The spec requires admin-initiated registration with multi-admin support. **Estimate 38h to bridge this gap** including design, implementation, and testing.
