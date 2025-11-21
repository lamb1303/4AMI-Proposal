# File: stories/08-admin-user-management.md

# Story 8: Admin – User Management

## Context

**Figma URL:**  
https://www.figma.com/design/uKXM3ydEdoSU1TwMaBPKhc/4ami-Dashboard--copia-?node-id=881-266&t=4WL8Z3qHAQ0FStna-0

**Story goal (from PRD + Figma)**  
Provide 4AMI admins with a centralized workspace to list every platform user, search/filter accounts, invite new admins/customers, edit profile/role details, import users in bulk, and activate/deactivate access with proper confirmation, validations, audit trails, and success/error feedback.

## UX / Product

**Main user flows (from Figma)**  
- [ ] **Landing on Manage Users**: Admin opens “Manage User” table view with breadcrumb, action buttons (Add user, Import, Download template), filters, pagination, and per-row actions (edit/delete).  
- [ ] **Filter/search users**: Admin selects quick filters (role, status), adds advanced filters (“Add Filter”), clears filters, and changes rows-per-page while results update.  
- [ ] **Bulk selection**: Admin uses table checkboxes (select-all header + per-row) to prep bulk actions (future) and receives visual feedback for selected rows.  
- [ ] **Create user manually**: Admin clicks Add User → navigates to form with personal info, company/title fields, contact data, role selector, invitation code section, consent checkbox, and Create/Cancel/Discard buttons.  
- [ ] **Import users**: Admin clicks Import button to upload CSV/Excel, optionally download template, and see success/error toast states (per design actions).  
- [ ] **Edit user**: Admin clicks edit icon on a row, pre-populated form opens, changes saved via Update action.  
- [ ] **Deactivate/delete user**: Admin clicks trash icon, sees confirmation, and status updates (active/inactive) reflected in list.  
- [ ] **Success confirmation**: Toast/banner appears after create/update/delete/import actions confirming result.  

**States to support**
- [ ] **Loading**: Skeleton table rows, disabled filters while fetching, spinners on buttons (Create, Import).  
- [ ] **Error**: Inline form errors, toast/banner for API failures, file-upload error states (invalid template, network).  
- [ ] **Empty/edge**: No users yet, no results after filters, empty table placeholders with guidance to add/import.  
- [ ] **Success**: Toast after create/update/delete/import, status chips reflecting latest state.  
- [ ] **Confirmation**: Modal/dialog for destructive actions (Deactivate/Delete) requiring explicit confirmation.

## Frontend

**Screens / components**  
- [ ] `UserManagementListView` (header, breadcrumb, action toolbar, filters, pagination).  
- [ ] `UserFilterBar` (role dropdown, Add/Clear filter controls, rows-per-page).  
- [ ] `UserTable` with checkbox column, sortable headers, action buttons.  
- [ ] `UserFormPage` for create/edit with grouped input sections and role selector.  
- [ ] `UserImportDialog` / upload panel with template download CTA.  
- [ ] `RoleSelector` component (dropdown with search + multi-select if needed).  
- [ ] `StatusBadge` for Active/Pending/Inactive states.  
- [ ] `ConfirmationModal` for deactivate/delete.  
- [ ] `Toast/Alert` component for success/error.  

**Frontend tasks**
- [ ] Build `UserManagementListView` shell (header, breadcrumb, layout spacing) (~1.5h)  
- [ ] Implement action toolbar (Add User, Import Users, Download Template buttons) with icons/tooltips (~1.5h)  
- [ ] Create `UserFilterBar` with role dropdown, Add Filter menu, Clear Filter action (~2h)  
- [ ] Implement rows-per-page dropdown synced with pagination/query params (~1h)  
- [ ] Build `UserTable` with sticky header, alternating rows, responsive columns (~2.5h)  
- [ ] Add checkbox selection logic (select-all, indeterminate state) (~2h)  
- [ ] Implement column sorting UI + param handling for Name/Role/Status columns (~2h)  
- [ ] Add action column buttons (edit, delete) with hover/focus states (~1h)  
- [ ] Integrate React Query (or equivalent) for GET /admin/users with filters, pagination, caching (~2.5h)  
- [ ] Implement empty-state component with CTA to add/import (~1.5h)  
- [ ] Add skeleton loaders for table rows + filter bar while loading (~1h)  
- [ ] Build `UserFormPage` with sections (Personal Info, Company, Contact, Role, Invitation, Terms checkbox) (~3h)  
- [ ] Implement validation messages (required, email format, phone mask, password requirements if any) (~2h)  
- [ ] Wire Create/Update submission with optimistic disabled states + success toast (~1.5h)  
- [ ] Add Cancel/Discard logic (confirmation when unsaved changes) (~1.5h)  
- [ ] Build `UserImportDialog` with drag-and-drop area, file picker, progress indicator (~2.5h)  
- [ ] Implement template download handler + tooltip/instructions (~1h)  
- [ ] Add error handling for import (invalid format, partial failures) with inline list (~1.5h)  
- [ ] Implement `ConfirmationModal` for delete/deactivate including reason textarea if needed (~1.5h)  
- [ ] Add `StatusBadge` component with theme tokens for each state (~1h)  
- [ ] Integrate toast/alert service for success/error notifications (~1h)  
- [ ] Write unit/component tests for filters, table selection, form validation, import dialog (~2.5h)  

## Backend

**APIs / endpoints**
- [ ] `GET /admin/users` – paginated + filtered list (status, role, company, search). **Status: partial** | Est: 2h | *Exists at `/users` with basic pagination, but missing status/role/company filters and search functionality*
- [ ] `POST /admin/users` – create/invite user (assign role, send invitation email). **Status: done** | *Exists at `/users` (POST) and `/users/invite` (POST) with email integration*
- [ ] `GET /admin/users/{id}` – fetch detail for edit form. **Status: done** | *Exists at `/users/:id` with role-based access control*
- [ ] `PATCH /admin/users/{id}` – update profile, role, contact info. **Status: done** | *Exists at `/users/:id` with validation*
- [ ] `PATCH /admin/users/{id}/status` – activate/deactivate or soft-delete. **Status: partial** | Est: 1h | *Exists as separate `/users/:id/activate` and `/users/:id/deactivate` endpoints; missing unified status endpoint and deactivation reason tracking*
- [ ] `POST /admin/users/import` – upload CSV/Excel to create multiple users. **Status: missing** | Est: 3h
- [ ] `POST /admin/users/{id}/resend-invite` (optional CTA from form). **Status: missing** | Est: 1.5h

**Note:** Current implementation uses `/users` path instead of `/admin/users`. Most core CRUD operations exist but missing advanced filtering, bulk import, and resend invite features.  

**Backend tasks**
- [ ] Review/extend User entity with fields surfaced in Figma (first/last name, company, title, phone, invitation code, role, status) (~2h) **Status: done** | *User entity already has all required fields: firstName, lastName, title, phone, companyName, source, role, isActive, emailVerificationToken*
- [ ] Create DB migration for new columns + indexes on email/status/role (~2h) **Status: partial** | Est: 1h | *Schema exists, but missing explicit indexes on email, status (isActive), and role for query optimization*
- [ ] Implement query builder for `GET /admin/users` with pagination, filtering, sorting, search (~2.5h) **Status: partial** | Est: 2h | *Basic pagination exists in UsersService.findAll; missing filters for status, role, company, search by name/email, and sorting*
- [ ] Enforce admin-only guard + RBAC checks on all endpoints (~1h) **Status: done** | *RolesGuard implemented and applied to user endpoints with @Roles(ADMIN, CUSTOMER_ADMIN) decorator*
- [ ] Build `POST /admin/users` service with validation (unique email, password rules, required role) (~2h) **Status: done** | *UsersService.create and inviteUser implemented with email uniqueness check and role validation*
- [ ] Trigger invitation email (token generation, expiry) after creation (~2h) **Status: done** | *EmailService.sendUserCredentials integrated in create/invite methods with token generation*
- [ ] Implement `GET /admin/users/{id}` serializer returning form-ready payload (~1h) **Status: done** | *UsersService.findOne returns user with company relation mapped*
- [ ] Implement `PATCH /admin/users/{id}` with optimistic concurrency + audit logging (~2h) **Status: partial** | Est: 1.5h | *Update method exists but missing optimistic concurrency control and audit logging*
- [ ] Build status toggle endpoint (activate/deactivate) with reason + timestamp (~1.5h) **Status: partial** | Est: 1h | *Activate/deactivate endpoints exist but missing deactivation reason field and timestamp tracking*
- [ ] Implement import parsing (CSV/Excel), row-level validation, bulk insert with transaction (~3h) **Status: missing** | Est: 3h
- [ ] Queue email sends for imported users to avoid request timeouts (~1.5h) **Status: missing** | Est: 1.5h
- [ ] Add ability to resend invites with rate limiting (~1.5h) **Status: missing** | Est: 1.5h
- [ ] Record admin audit events (action, target user, timestamp, metadata) (~1.5h) **Status: missing** | Est: 1.5h
- [ ] Implement error handling + standardized responses for validation vs server errors (~1h) **Status: partial** | Est: 0.5h | *Basic error handling exists (ConflictException, NotFoundException, BadRequestException) but could be more standardized*
- [ ] Unit tests for services (create, update, deactivate, import) (~2.5h) **Status: missing** | Est: 2.5h
- [ ] Integration tests for endpoints incl. permission failures and happy paths (~3h) **Status: missing** | Est: 3h
- [ ] Add search functionality (full-text search on name, email) (~1h) **Status: missing** | Est: 1h
- [ ] Add sorting capabilities (by name, role, status, created date) (~1h) **Status: missing** | Est: 1h
- [ ] Implement rate limiting on sensitive endpoints (invite, resend) (~1h) **Status: missing** | Est: 1h
- [ ] Add password strength requirements validation (~0.5h) **Status: missing** | Est: 0.5h
- [ ] Implement soft delete vs hard delete distinction (~1h) **Status: missing** | Est: 1h | *Current delete uses hard delete (repository.remove)*  

## DevOps / Infra

**Config / services**
- [ ] Database migrations for user fields/indexes.  
- [ ] Email/notification service credentials for invitations.  
- [ ] Background queue for bulk import + email jobs.  
- [ ] Audit logging/monitoring for admin user actions.  
- [ ] Feature flags/env vars for invitation templates + import size.  

**DevOps tasks**
- [ ] Apply new migrations across environments with rollback plan (~1h)  
- [ ] Configure secrets for email provider + invitation templates (ENV vars, secret manager) (~1h)  
- [ ] Provision/update background worker (BullMQ/SQS/etc.) for import + email jobs (~2h)  
- [ ] Add log ingestion & dashboards for admin user actions (create/edit/delete) (~1.5h)  
- [ ] Configure alerting for failed import jobs or high error rate on user endpoints (~1.5h)  
- [ ] Update CI/CD to run new backend tests + lint before deploy (~1h)  
- [ ] Document operational runbook (env vars, queue names, template IDs, rate limits) (~1h)  
- [ ] Ensure GDPR/PII compliance: retention policy + secure audit trail storage (~2h)  

## Definition of Done

**Functional**
- [ ] Admin can view paginated user list with filters, sorting, and selection.  
- [ ] Admin can create/invite users manually via form with validations.  
- [ ] Admin can import users via CSV/Excel and receive success/error feedback.  
- [ ] Admin can edit existing user details, roles, and contact info.  
- [ ] Admin can deactivate/delete users with confirmation and see updated status.  
- [ ] System sends invitation/resend emails with secure tokens.  
- [ ] Audit log records every admin action on users.  

**UX**
- [ ] Table layout, filter chips, badges, and buttons match Figma spacing/colors.  
- [ ] Form fields, sections, and button hierarchy mirror Figma screens.  
- [ ] Import dialog, template CTAs, and toasts behave as designed.  
- [ ] Loading, empty, error, and confirmation states visually align with Figma.  
- [ ] Experience is accessible (keyboard navigation, labeled inputs, focus states).  

**QA**
- [ ] Automated tests cover list filters, create, edit, deactivate, import, invites.  
- [ ] Manual QA verifies toasts, confirmation dialogs, and edge cases (duplicate email, invalid file).  
- [ ] Performance validated with ≥5k users and large import files.  
- [ ] Security/RBAC tests confirm only authorized admins can manage users.  

## Estimate

- Frontend: ~46h (L)
- Backend: ~36h (L) → **Revised: ~23h (M)** (reduced from original due to existing implementation)
- DevOps: ~12h (M)

---

## Backend Implementation Gap Summary

### Current State
The backend has a robust users module (`/users`) with:
- ✅ **User Entity**: Complete schema with all required fields (firstName, lastName, email, phone, title, companyName, source, role, isActive, emailVerificationToken, etc.)
- ✅ **Core CRUD Operations**: Create, read, update, delete users with role-based access control
- ✅ **Invitation System**: POST /users/invite with email integration and token generation
- ✅ **Activate/Deactivate**: Separate endpoints for status management
- ✅ **Role Guards**: RolesGuard implemented and applied to all endpoints
- ✅ **Email Integration**: EmailService sends credentials/invitations with tokens
- ✅ **Basic Pagination**: Page/limit support in findAll
- ✅ **Company Filtering**: CUSTOMER_ADMIN users see only their company's users
- ✅ **Test Seeders**: Test users seeder exists for QA data
- ✅ **Validation**: DTOs with email, role, and field validation

### Critical Gaps

#### 1. **Advanced Filtering & Search (80% Missing)**
   - ✅ Basic pagination exists
   - ❌ No status filter (active/inactive/pending)
   - ❌ No role filter
   - ❌ No company filter for admins
   - ❌ No search by name or email
   - ❌ No sorting capabilities

#### 2. **Bulk Import System (100% Missing)**
   - ❌ CSV/Excel upload endpoint
   - ❌ File parsing and validation
   - ❌ Row-level error handling
   - ❌ Bulk insert with transactions
   - ❌ Queued email sends to avoid timeouts

#### 3. **Resend Invitation (100% Missing)**
   - ❌ Resend invite endpoint
   - ❌ Rate limiting for invite operations
   - ❌ Token regeneration logic

#### 4. **Audit & Compliance (100% Missing)**
   - ❌ Audit logging for admin actions
   - ❌ Deactivation reason tracking
   - ❌ Timestamp tracking for status changes
   - ❌ GDPR/PII compliance measures
   - ❌ Soft delete vs hard delete distinction

#### 5. **Enhanced Status Management (50% Missing)**
   - ✅ Activate/deactivate endpoints exist
   - ❌ Unified status endpoint
   - ❌ Deactivation reason field
   - ❌ Status change timestamps

#### 6. **Performance & Optimization (60% Missing)**
   - ✅ Basic query optimization with relations
   - ❌ Database indexes on email/status/role
   - ❌ Optimistic concurrency control
   - ❌ Rate limiting on sensitive endpoints

#### 7. **Testing & Quality (100% Missing)**
   - ❌ Unit tests for user services
   - ❌ Integration tests for endpoints
   - ❌ Permission/RBAC test coverage
   - ❌ Import validation test cases

#### 8. **Admin Path Convention (Minor)**
   - ⚠️ Routes use `/users` instead of `/admin/users` (cosmetic, not blocking)

### Path Forward

**High Priority (Blocking MVP):**
1. Add advanced filters to GET /users (status, role, company, search) (~2h)
2. Add sorting to GET /users (name, role, status, created) (~1h)
3. Implement bulk import endpoint with CSV/Excel parsing (~3h)
4. Add queued email sends for imported users (~1.5h)
5. Implement resend invite endpoint (~1.5h)

**Medium Priority (Production Quality):**
1. Add audit logging for user management actions (~1.5h)
2. Add deactivation reason tracking (~1h)
3. Create database indexes for optimization (~1h)
4. Add rate limiting on invite/resend (~1h)
5. Implement optimistic concurrency control (~1.5h)
6. Add soft delete functionality (~1h)

**Low Priority (Quality & Maintenance):**
1. Write unit tests for services (~2.5h)
2. Write integration tests (~3h)
3. Standardize error responses (~0.5h)
4. Add password strength validation (~0.5h)
5. Refactor to use `/admin/users` path (optional, ~0.5h)

### Summary
The user management backend is **~65% complete**. Core CRUD operations, authentication, role-based access control, and email invitations are fully functional. The main gaps are in advanced filtering/search, bulk import, audit logging, and comprehensive testing. Most gaps are non-blocking enhancements rather than missing core functionality.

**Total Remaining Effort:** ~23 hours (reduced from 36h original estimate due to substantial existing implementation)