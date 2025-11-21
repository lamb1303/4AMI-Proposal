# File: stories/10-customer-transportation-request.md

# Story 10: Customer – Transportation Request

## Context

**Figma URL:**  
https://www.figma.com/design/yiCfEo9ZDgLyIkSiK7NVP2/4ami-Dashboard--copia-?node-id=2652-21140&t=dwNhFJQ5EbJ3AdrU-0

**Story goal (from PRD + Figma)**
Enable customers to submit transportation requests for waste/residual pickup and delivery through a streamlined form-based workflow. The flow must support entering pickup and delivery locations with address validation, selecting waste/material types and quantities, specifying preferred date/time windows, adding special handling instructions and attachments, reviewing request details before submission, and receiving confirmation with tracking information. The system must validate all inputs, enforce business rules (delivery dates, quantity limits, service area restrictions), provide real-time feedback on availability, and route approved requests to the operations team for scheduling and fulfillment.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – Initiate request: Customer navigates to transportation requests section, clicks "New Transportation Request" or "Request Pickup" button, sees introduction/welcome screen explaining the process (optional), proceeds to request form.
- [x] Step 2 – Pickup location details: Customer enters or selects pickup address (autocomplete from saved locations or manual entry with address validation), specifies contact person name and phone for pickup, adds access instructions or gate codes, marks location on map for verification (optional).
- [x] Step 3 – Delivery location details: Customer enters or selects delivery address (autocomplete or manual entry), specifies delivery contact person and phone, adds delivery instructions, confirms location on map, option to mark as "same as pickup" for roundtrip requests.
- [x] Step 4 – Material/waste information: Customer selects waste/material type from categorized dropdown (Hazardous, Non-Hazardous, Recyclable, etc.), enters quantity with unit selection (tons, cubic yards, gallons, containers), specifies container type if applicable (roll-off, drum, tank), adds material description or special handling notes.
- [x] Step 5 – Schedule selection: Customer chooses preferred pickup date from calendar (respecting business rules like minimum lead time), selects time window (morning, afternoon, specific time range), optionally selects preferred delivery date/time, sees availability indicators or blackout dates.
- [x] Step 6 – Additional details: Customer adds special instructions for driver or operations team, uploads supporting documents (manifests, safety data sheets, photos) with file type and size validation, specifies any equipment requirements (forklift, crane access).
- [x] Step 7 – Review and submit: Customer reviews complete request summary with all entered information organized in sections, can edit any section by clicking back/edit buttons, sees estimated cost or pricing information (if available), checks required acknowledgments or terms, clicks "Submit Request" button.
- [x] Step 8 – Confirmation: After successful submission, customer sees confirmation screen with request ID, confirmation number, and tracking link, receives confirmation email with request details and next steps, can view request status in "My Requests" dashboard, sees estimated response time from operations team.

**States to support**
- [x] Loading states – initial form load with skeleton placeholders, address autocomplete loading with spinner, calendar loading for availability check, file upload progress indicators with percentage, submit button loading during submission with spinner and disabled state.
- [x] Error states – inline field validation errors (required fields, invalid formats, quantity limits exceeded), address validation errors (invalid address, address outside service area), date selection errors (past dates, dates outside allowed window, blackout dates), file upload errors (file too large, invalid file type, upload failed), server-side validation errors (duplicate request, service unavailable for selected material, capacity exceeded), network errors with retry option.
- [x] Empty/edge states – empty saved locations list prompts manual address entry, no available dates in calendar shows message and alternative contact option, missing optional fields show placeholder text, zero quantity or invalid material selection prevents proceeding, form auto-save for incomplete requests (draft state), abandoned request warning before navigation.
- [x] Success confirmation – success screen with checkmark icon, request ID prominently displayed, confirmation message with next steps, email confirmation sent notification, link to view request status, option to create another request or return to dashboard.

## Frontend

**Screens / components**
- [ ] `TransportationRequestWizard` (multi-step form container managing step navigation and state) – Status: Not Started
- [ ] `PickupLocationStep` (pickup address, contact, instructions form) – Status: Not Started
- [ ] `DeliveryLocationStep` (delivery address, contact, instructions form) – Status: Not Started
- [ ] `MaterialInfoStep` (material type, quantity, container selection) – Status: Not Started
- [ ] `ScheduleSelectionStep` (date/time picker with availability) – Status: Not Started
- [ ] `AdditionalDetailsStep` (special instructions, file uploads, equipment) – Status: Not Started
- [ ] `ReviewStep` (read-only summary of all entered data with edit options) – Status: Not Started
- [ ] `ConfirmationScreen` (success screen with request ID and next steps) – Status: Not Started
- [ ] `AddressAutocomplete` (reusable address input with Google Maps/geocoding integration) – Status: Not Started
- [ ] `LocationPicker` (map component for visual location selection/verification) – Status: Not Started
- [ ] `MaterialTypeSelector` (categorized dropdown for waste/material types) – Status: Not Started
- [ ] `QuantityInput` (quantity field with unit selector and validation) – Status: Not Started
- [ ] `DateTimePicker` (calendar with availability indicators and time slot selection) – Status: Not Started
- [ ] `FileUploadWidget` (multi-file upload with drag-drop, progress, preview) – Status: Not Started
- [ ] `StepProgressIndicator` (visual stepper showing current step and completion) – Status: Not Started
- [ ] `SavedLocationSelector` (dropdown/list of customer's saved addresses) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/transportation-requests/new` route with multi-step wizard layout (sidebar, stepper, content area) matching Figma structure – Status: Not Started – Est: 2h
- [ ] Build `TransportationRequestWizard` container component managing step navigation (Next, Back, Submit), form state persistence across steps, step validation before advancing – Status: Not Started – Est: 3h
- [ ] Create `StepProgressIndicator` component showing numbered steps with labels (Pickup, Delivery, Material, Schedule, Details, Review), active/completed/upcoming states, clickable steps for going back – Status: Not Started – Est: 2h
- [ ] Implement `PickupLocationStep` with address input (autocomplete), saved locations dropdown, contact name and phone fields, access instructions textarea, map preview (optional) – Status: Not Started – Est: 3h
- [ ] Build `AddressAutocomplete` component integrating with Google Maps Places API or similar, showing suggestions dropdown, validating selected address, extracting structured address components (street, city, state, zip) – Status: Not Started – Est: 2.5h
- [ ] Create `SavedLocationSelector` component loading customer's saved locations from API, displaying as dropdown with address formatting, option to add new location, "Use this address" button – Status: Not Started – Est: 2h
- [ ] Implement `DeliveryLocationStep` with same address input functionality as pickup, checkbox for "Same as pickup location" that auto-fills fields, delivery contact and instructions fields – Status: Not Started – Est: 2.5h
- [ ] Build `LocationPicker` map component using Google Maps or Mapbox, showing selected address marker, allowing drag-to-adjust location, zoom and pan controls, confirming final location – Status: Not Started – Est: 3h
- [ ] Create `MaterialInfoStep` with material type selector, quantity input with units, container type dropdown (optional), material description textarea, hazardous material checkbox with warnings – Status: Not Started – Est: 2.5h
- [ ] Implement `MaterialTypeSelector` component with categorized material types (dropdown or multi-level select), filter/search functionality, material icons or color coding, tooltips for material descriptions – Status: Not Started – Est: 2.5h
- [ ] Build `QuantityInput` component with number input, unit dropdown (tons, cubic yards, gallons, containers, pounds), validation for min/max quantities, formatting for decimal places – Status: Not Started – Est: 2h
- [ ] Create `ScheduleSelectionStep` with date picker calendar, time window selection (radio buttons or dropdown), availability indicators (green/red days, disabled dates), minimum lead time enforcement – Status: Not Started – Est: 3h
- [ ] Implement `DateTimePicker` with calendar component showing available/unavailable dates, time slot selection for chosen date, business rules display (e.g., "Minimum 2 business days notice"), holiday/blackout date highlighting – Status: Not Started – Est: 2.5h
- [ ] Build `AdditionalDetailsStep` with special instructions textarea (with character limit), equipment requirements checkboxes (forklift, crane, etc.), file upload section, summary of selected options – Status: Not Started – Est: 2.5h
- [ ] Create `FileUploadWidget` component supporting multiple file uploads, drag-and-drop interface, file type validation (PDF, JPG, PNG, max 10MB per file), upload progress bars, file preview thumbnails, remove file button – Status: Not Started – Est: 3h
- [ ] Implement `ReviewStep` displaying all entered information in organized sections (Pickup, Delivery, Material, Schedule, Attachments), each section with "Edit" button to jump back to that step, estimated cost display (if available), terms and conditions checkbox – Status: Not Started – Est: 2.5h
- [ ] Build `ConfirmationScreen` component with success icon/animation, request ID and confirmation number prominently displayed, summary of request details, email confirmation message, "View Request Status" button, "Create Another Request" button – Status: Not Started – Est: 2h
- [ ] Add client-side validation for all steps: required field validation, phone number format validation, quantity min/max validation, date range validation (not in past, within allowed window), file size and type validation – Status: Not Started – Est: 2.5h
- [ ] Implement step navigation logic: disable Next button until current step is valid, allow Back navigation without validation, remember scroll position on step changes, prevent direct URL navigation to later steps – Status: Not Started – Est: 2h
- [ ] Add form state persistence: save draft to localStorage on field changes, restore draft on page reload, show "Resume draft" option on form entry, clear draft after successful submission – Status: Not Started – Est: 2.5h
- [ ] Implement API integration for POST /transportation-requests: build request payload from form state, handle submission with loading state, map server validation errors to form fields, handle success and error responses – Status: Not Started – Est: 2.5h
- [ ] Add API integration for address validation: call address validation endpoint, display validation errors inline, suggest corrections for ambiguous addresses, handle service area validation (address outside service area) – Status: Not Started – Est: 2h
- [ ] Implement GET /material-types API integration for loading material categories and types, cache results, handle loading and error states, provide fallback for offline/error scenarios – Status: Not Started – Est: 1.5h
- [ ] Add GET /availability API integration for checking date availability, show loading state on calendar, display available/unavailable dates, fetch time slots for selected date – Status: Not Started – Est: 2h
- [ ] Build GET /saved-locations API integration for customer addresses, load on step mount, handle empty state, allow adding new location inline or via modal – Status: Not Started – Est: 1.5h
- [ ] Implement file upload API integration: POST /uploads endpoint for document upload, multipart/form-data support, upload progress tracking, retry failed uploads, associate uploaded files with request – Status: Not Started – Est: 2.5h
- [ ] Add error handling across all steps: display inline validation errors below fields, show toast notifications for network errors, provide retry buttons for failed operations, gracefully handle partial data loss – Status: Not Started – Est: 2h
- [ ] Implement responsive design: ensure all steps work on desktop, tablet, and mobile, stack form fields appropriately on small screens, mobile-friendly date picker and file upload, touch-optimized map interactions – Status: Not Started – Est: 2.5h
- [ ] Add accessibility features: keyboard navigation through steps and form fields, focus management (focus first error on validation failure), ARIA labels for all inputs, screen reader announcements for step changes and errors, keyboard shortcuts for Next/Back – Status: Not Started – Est: 2.5h
- [ ] Polish UX details: add loading skeletons for step content, smooth transitions between steps, confirmation dialog before abandoning incomplete request, helpful placeholder text and tooltips, field auto-focus on step entry – Status: Not Started – Est: 2h

## Backend

**APIs / endpoints**
- [ ] POST `/transportation-requests` – create new transportation request – **Status: missing** | Est: 4h | *No transportation request infrastructure exists. Need entire module: entities, controllers, services, DTOs*
- [ ] GET `/transportation-requests/:id` – retrieve specific transportation request details – **Status: missing** | Est: 2h
- [ ] GET `/transportation-requests` – list customer's transportation requests with filtering/pagination – **Status: missing** | Est: 3h
- [ ] PATCH `/transportation-requests/:id` – update request (draft state only) – **Status: missing** | Est: 2.5h
- [ ] DELETE `/transportation-requests/:id` – cancel transportation request – **Status: missing** | Est: 2h
- [ ] POST `/transportation-requests/:id/attachments` – upload supporting documents – **Status: missing** | Est: 2.5h | *Can reuse file upload infrastructure from file-upload.config.ts*
- [ ] DELETE `/transportation-requests/:id/attachments/:attachmentId` – remove uploaded document – **Status: missing** | Est: 1.5h
- [ ] GET `/material-types` – list available material/waste types with categories – **Status: missing** | Est: 2h
- [ ] POST `/addresses/validate` – validate and geocode address – **Status: missing** | Est: 2.5h | *No geocoding integration exists; need Google Maps/Here/Bing API*
- [ ] GET `/addresses/saved` – retrieve customer's saved locations – **Status: missing** | Est: 1.5h
- [ ] POST `/addresses/saved` – save new location for future use – **Status: missing** | Est: 1.5h
- [ ] GET `/availability` – check date availability for transportation – **Status: missing** | Est: 3h
- [ ] POST `/transportation-requests/:id/submit` – submit draft request for processing – **Status: missing** | Est: 2h

**Backend tasks**
- [ ] Design TransportationRequest entity schema with fields: id, requestNumber (auto-generated), customerId, companyId, status (draft, submitted, approved, scheduled, in_progress, completed, cancelled), pickupAddress (JSON or FK), pickupContact, pickupPhone, pickupInstructions, deliveryAddress, deliveryContact, deliveryPhone, deliveryInstructions, materialType (FK to MaterialType), quantity, quantityUnit, containerType, materialDescription, isHazardous, preferredPickupDate, preferredPickupTimeWindow, preferredDeliveryDate, specialInstructions, equipmentRequirements, estimatedCost, createdAt, updatedAt, submittedAt, scheduledAt, completedAt – **Status: missing** | Est: 3h
- [ ] Create MaterialType entity with fields: id, category (enum: Hazardous, Non-Hazardous, Recyclable, Special), code, name, description, requiresPermit, handlingInstructions, isActive – **Status: missing** | Est: 2h
- [ ] Create TransportationRequestAttachment entity with fields: id, transportationRequestId (FK), fileName, originalFileName, fileSize, mimeType, storageUrl, uploadedBy, uploadedAt – **Status: missing** | Est: 1.5h
- [ ] Create SavedLocation entity with fields: id, companyId, label, addressLine1, addressLine2, city, state, zipCode, country, contactName, contactPhone, latitude, longitude, isActive – **Status: missing** | Est: 1.5h
- [ ] Create database migrations for all new entities with proper indexes: index on requestNumber for lookups, index on (companyId, status) for list queries, index on preferredPickupDate for availability queries, foreign key constraints – **Status: missing** | Est: 2.5h
- [ ] Implement POST `/transportation-requests` endpoint: accept CreateTransportationRequestDto, validate all required fields (pickup, delivery, material, quantity, date), auto-generate requestNumber, set initial status to 'draft', associate with authenticated user's company, return created request with ID – **Status: missing** | Est: 4h
- [ ] Add CreateTransportationRequestDto with validation: required pickup address fields, required delivery address (or sameAsPickup flag), material type ID validation, quantity min/max by material type, date validation (minimum lead time, not in past), phone number format, file attachment references (optional), special instruction character limits – **Status: missing** | Est: 3h
- [ ] Implement business rule validation: minimum lead time enforcement (e.g., 2 business days for standard, 5 days for hazardous), quantity limits by material type (prevent unrealistic quantities), service area validation (pickup/delivery within coverage area), capacity check for requested date (optional), blackout date validation (holidays, maintenance periods) – **Status: missing** | Est: 3.5h
- [ ] Implement address validation service: integrate with geocoding API (Google Maps, Here, Bing), validate address format and existence, extract standardized address components, check coordinates within service area polygon, return validation result with suggestions – **Status: missing** | Est: 3h | *No geocoding integration exists*
- [ ] Build availability checking service: query existing scheduled requests for date, calculate available capacity by material type, check blackout dates calendar, enforce minimum lead time from current date, return available dates with time slot options – **Status: missing** | Est: 3.5h
- [ ] Implement file upload handling for attachments: multer middleware for multipart upload, file type validation (PDF, JPG, PNG, DOC, XLS, max 10MB), generate unique filename with UUID, upload to S3 or local storage, create TransportationRequestAttachment record, return file URL and ID – **Status: missing** | Est: 3h | *Can reuse existing multer config (file-upload.config.ts) but needs adaptation for 10MB limit*
- [ ] Add authorization middleware: verify user is CUSTOMER_ADMIN for their company, prevent access to other companies' requests, allow ADMIN to view all requests, implement row-level security checks – **Status: missing** | Est: 2h | *RolesGuard exists but need company-level filtering*
- [ ] Implement request status management: define status enum (draft, submitted, approved, rejected, scheduled, in_progress, completed, cancelled), status transition rules (draft → submitted → approved/rejected → scheduled, etc.), prevent invalid status transitions, track status history (optional) – **Status: missing** | Est: 2.5h
- [ ] Build request submission logic (POST `/transportation-requests/:id/submit`): validate request is in draft status, verify all required fields present, transition to submitted status, generate unique tracking number, enqueue for operations team review, send confirmation email to customer, send notification to operations team – **Status: missing** | Est: 3h | *Email infrastructure exists (nodemailer, resend) but need templates*
- [ ] Implement email notifications: confirmation email on submission with request details and tracking number, status update emails (approved, scheduled, completed), cancellation confirmation, use existing email infrastructure from auth story – **Status: missing** | Est: 2.5h | *EmailService exists, need new templates*
- [ ] Add request number generation service: generate unique alphanumeric request numbers (e.g., TR-2024-001234), ensure uniqueness with database constraint, sequential or hash-based generation, include year/month for readability – **Status: missing** | Est: 1.5h
- [ ] Implement GET `/transportation-requests` list endpoint: filter by status (query param), filter by date range (createdAt, preferredPickupDate), pagination with page/limit params, sorting by date or status, return request summaries with key fields – **Status: missing** | Est: 3h
- [ ] Build service area validation: define service area as polygon coordinates or zip code list, check if pickup/delivery addresses fall within service area, return specific error messages for out-of-area addresses, configurable per company or global – **Status: missing** | Est: 2.5h
- [ ] Add request update logic (PATCH endpoint): allow updates only for draft/pending status, re-validate changed fields, update modifiedAt timestamp, track change history (optional audit log), prevent updates for submitted/scheduled requests – **Status: missing** | Est: 2.5h
- [ ] Implement cancellation logic (DELETE endpoint): verify request status allows cancellation (not completed/in-progress), soft delete with cancelled status and cancellation reason, send cancellation notification, update capacity availability if scheduled, enforce cancellation deadline (e.g., 24 hours before pickup) – **Status: missing** | Est: 2.5h
- [ ] Add rate limiting to request creation: prevent spam or abuse (e.g., max 50 requests per day per company), apply @Throttle decorator, return 429 with retry-after header, different limits for different company tiers (optional) – **Status: missing** | Est: 1.5h
- [ ] Write unit tests for DTOs, validation logic, business rules: test required field validation, test quantity limits, test date validation (past dates, minimum lead time), test status transitions, test authorization rules – **Status: missing** | Est: 3h
- [ ] Add integration tests for all endpoints: POST happy path (create request), POST with invalid data (missing fields, invalid material type, past date), GET list with filters, GET by ID with authorization check, PATCH draft request, DELETE/cancel request, file upload endpoint – **Status: missing** | Est: 4h
- [ ] Implement audit logging for transportation requests: log all request creations, status changes, updates, cancellations with user, timestamp, IP address, use activity log infrastructure from dashboard story – **Status: missing** | Est: 2h

**Additional production-ready tasks identified:**
- [ ] Create RequestStatusHistory table for tracking status changes – **Status: missing** | Est: 2h
- [ ] Implement duplicate request detection – **Status: missing** | Est: 2.5h
- [ ] Add material type compatibility rules – **Status: missing** | Est: 2h
- [ ] Implement cost estimation logic (optional) – **Status: missing** | Est: 4h
- [ ] Add geofencing for service areas – **Status: missing** | Est: 3h
- [ ] Create webhook system for request status updates – **Status: missing** | Est: 3h

## DevOps / Infra

**Config / services**
- [ ] Database migrations for transportation request entities
- [ ] File storage for attachments (S3 or local)
- [ ] Geocoding API configuration (Google Maps, Here, Bing)
- [ ] Email notification templates for request lifecycle
- [ ] Message queue for async operations (optional)
- [ ] Monitoring for request submission and processing

**DevOps tasks**
- [ ] Create database migrations for TransportationRequest, MaterialType, TransportationRequestAttachment, SavedLocation, RequestStatusHistory tables with proper indexes and foreign keys – Status: missing – Est: 3h
  **Gap:** Need comprehensive migrations for entire transportation request domain. Include indexes on (companyId, status), (requestNumber), (preferredPickupDate), (customerId) for query performance.
- [ ] Seed MaterialType database with initial material categories and types: Hazardous (chemical waste, batteries, solvents), Non-Hazardous (paper, cardboard, plastic), Recyclable (metals, glass, e-waste), Special (medical waste, radioactive) – Status: missing – Est: 2h
  **Gap:** Need initial data for material type dropdown. Include material codes, names, descriptions, handling requirements, permit requirements.
- [ ] Configure file storage service for attachments: reuse S3 configuration from company logo story or set up new bucket, configure bucket CORS for direct uploads (optional), set lifecycle rules for attachment retention, configure local filesystem storage for development – Status: missing – Est: 2h
  **Gap:** Attachments storage infrastructure. May share S3 bucket with company logos in different folder, or use dedicated bucket.
- [ ] Set up geocoding API credentials: obtain Google Maps API key (or Here, Bing alternatives), configure API quotas and billing alerts, store credentials in secrets manager, configure allowed origins/IP restrictions – Status: missing – Est: 1.5h
  **Gap:** Third-party API integration for address validation and geocoding. Need API key and configuration per environment.
- [ ] Configure environment variables for transportation requests: GEOCODING_API_KEY, GEOCODING_PROVIDER (google, here, bing), SERVICE_AREA_COORDINATES (polygon or zip codes), MINIMUM_LEAD_TIME_DAYS, MAX_ATTACHMENTS_PER_REQUEST, ATTACHMENT_MAX_SIZE_MB, REQUEST_RATE_LIMIT – Status: missing – Est: 1h
  **Gap:** Configuration for business rules, API integration, and operational parameters.
- [ ] Create email templates for transportation requests: request submitted confirmation (with request ID, summary, next steps), request approved (with scheduling details), request scheduled (with driver info, ETA), request completed (with invoice link), request cancelled (with reason, refund info) – Status: missing – Est: 2.5h
  **Gap:** Email templates using existing email infrastructure from auth story. Need branded templates with request details.
- [ ] Set up message queue for async operations (optional): configure Bull queue for background jobs (availability calculation, email sending, geocoding batch operations), Redis configuration for queue storage, worker process for job processing – Status: missing – Est: 2.5h
  **Gap:** Async processing for long-running operations to improve API response times. Optional but recommended for production.
- [ ] Configure monitoring dashboards for transportation requests: track request submission rate, monitor status distribution (draft, submitted, approved, scheduled, completed), measure time-to-approval SLA, track geocoding API usage and errors, monitor file upload success rates – Status: missing – Est: 2.5h
  **Gap:** Business metrics and operational monitoring for transportation request workflows.
- [ ] Set up alerting for transportation request operations: alert on high request failure rate (>5% over 10min), alert on geocoding API failures or quota exceeded, alert on file upload storage errors, alert on long processing times (submission to approval >24h) – Status: missing – Est: 2h
  **Gap:** Proactive monitoring to catch issues before customer impact.
- [ ] Configure log aggregation for request operations: log all request creations with full payload, log status transitions with user and reason, log validation failures with field details, log geocoding API calls and results, integrate with centralized logging service – Status: missing – Est: 2h
  **Gap:** Structured logging for debugging, compliance, and analytics.
- [ ] Set up database indexes for query performance: composite index on (companyId, status, preferredPickupDate) for list queries, index on requestNumber for tracking lookups, index on (materialType, preferredPickupDate) for availability queries, index on createdAt for time-based queries – Status: missing – Est: 1.5h
  **Gap:** Optimize query performance for common access patterns (customer viewing their requests, filtering by status, searching by date).
- [ ] Configure geocoding API caching: implement Redis cache for geocoded addresses (TTL 30 days), cache key based on normalized address string, reduce API costs and improve response time, cache eviction strategy – Status: missing – Est: 2h
  **Gap:** Reduce costs and latency for repeated address lookups.
- [ ] Set up capacity planning for request volume: monitor request creation trends, forecast storage requirements for attachments (assume avg 5MB per request), plan database scaling for high request volume, configure auto-scaling for API servers – Status: missing – Est: 2h
  **Gap:** Ensure infrastructure can handle growth in request volume without performance degradation.
- [ ] Create backup and retention policies: daily backups of transportation request data, retain request data for compliance period (e.g., 7 years), archive old completed requests to cold storage, backup attachment files periodically – Status: missing – Est: 1.5h
  **Gap:** Data protection and compliance with retention requirements.
- [ ] Document deployment and configuration: document geocoding API setup steps, document service area configuration (how to update polygon coordinates), document material type seeding process, create runbook for common issues (geocoding failures, storage quota, rate limits) – Status: missing – Est: 2h
  **Gap:** Operations documentation for deployment and troubleshooting.
- [ ] Set up service area configuration management: define service areas as polygon coordinates or geofence, store in database or configuration file, provide admin UI or API to update service areas (future enhancement), validate service area data integrity – Status: missing – Est: 2h
  **Gap:** Manage geographic coverage areas for service delivery.
- [ ] Configure blackout dates calendar: create database table or config file for holiday/maintenance blackout dates, seed with national holidays and company holidays, provide mechanism to update blackout dates annually, integrate with availability checking logic – Status: missing – Est: 1.5h
  **Gap:** Prevent scheduling on non-operational days.
- [ ] Set up webhook delivery infrastructure (optional): create webhook queue for reliable delivery, implement retry logic with exponential backoff, log webhook delivery attempts and failures, provide webhook management UI for customers to configure URLs – Status: missing – Est: 3h
  **Gap:** Enable integration with customer systems for real-time status updates.

## Definition of Done

**Functional**
- [ ] Customer can initiate new transportation request and navigate through multi-step wizard with proper step progression.
- [ ] Customer can enter pickup location by selecting from saved addresses or entering new address with autocomplete and validation.
- [ ] Customer can enter delivery location with same functionality as pickup, or mark "same as pickup" for roundtrip requests.
- [ ] Customer can select material/waste type from categorized dropdown, enter quantity with unit selection, and specify container type.
- [ ] Customer can choose preferred pickup date from calendar showing available/unavailable dates, and select time window.
- [ ] Customer can add special instructions (character limit enforced), upload supporting documents (multiple files, drag-drop, type/size validation), and specify equipment requirements.
- [ ] Customer can review complete request summary with all details organized in sections, edit any section by navigating back.
- [ ] Form validates all required fields (pickup address, delivery address, material type, quantity, pickup date) before allowing submission.
- [ ] Address validation integrates with geocoding API, validates address format, checks service area coverage, shows errors for invalid or out-of-area addresses.
- [ ] Calendar enforces minimum lead time (e.g., 2 business days), disables past dates, shows blackout dates, prevents selection of unavailable dates.
- [ ] File upload handles multiple files, validates type (PDF, JPG, PNG, DOC, XLS) and size (max 10MB per file), shows progress, allows removal.
- [ ] On successful submission, request is saved with 'draft' or 'submitted' status, request ID and confirmation number are generated, confirmation email is sent.
- [ ] Customer sees confirmation screen with request ID, summary, email confirmation message, link to view status, option to create another request.
- [ ] Form state persists to localStorage, abandoned forms can be resumed, draft is cleared after successful submission.
- [ ] Authorization ensures customers can only submit requests for their own company, cannot view or modify other companies' requests.
- [ ] All request creations, status changes, and key actions are logged to audit log with user, timestamp, and details.

**UX**
- [ ] Multi-step wizard layout matches Figma design with step progress indicator, content area, navigation buttons.
- [ ] Step progress indicator shows current step highlighted, completed steps marked with checkmark, upcoming steps in muted state, steps are clickable for backward navigation.
- [ ] All form fields have proper labels, placeholders, and helper text matching Figma specifications.
- [ ] Address autocomplete shows dropdown with suggestions as user types, displays formatted addresses, handles selection smoothly.
- [ ] Map component (if included) shows selected location marker, allows zoom/pan, provides visual confirmation of address.
- [ ] Material type selector displays categorized options, shows material icons or color coding, provides tooltips with descriptions.
- [ ] Date picker calendar highlights available dates in green, unavailable/blackout dates in red or disabled, shows current selection clearly.
- [ ] File upload widget shows drag-drop zone, displays upload progress with percentage, shows file thumbnails/icons, provides remove button for each file.
- [ ] Loading states show skeleton placeholders on initial load, spinners during address validation, progress bars during file upload, disabled form during submission.
- [ ] Inline validation errors appear below fields with error icons, clear messages, and red styling immediately after field blur or form submission attempt.
- [ ] Review step displays all entered information in well-organized sections with clear labels, edit buttons visible for each section.
- [ ] Confirmation screen shows success icon/animation, request ID prominently displayed, summary of submitted request, clear next steps.
- [ ] Success toast or message confirms email sent, provides reassurance about next steps and timeline.
- [ ] Next/Back buttons are clearly visible, Next button disabled until current step is valid, Submit button shows loading state during submission.
- [ ] Responsive design works for desktop, tablet, and mobile: form fields stack properly, map interactions work on touch devices, file upload works on mobile.
- [ ] Smooth transitions between steps, no janky animations, proper focus management, helpful tooltips and placeholders throughout.

**QA**
- [ ] Happy path: Navigate through all steps → Fill all required fields with valid data → Upload 2-3 files → Review summary → Submit → See confirmation screen with request ID → Receive confirmation email.
- [ ] Saved location selection: Select saved address from dropdown → Auto-fills address fields → Continue to next step successfully.
- [ ] Manual address entry: Type partial address → See autocomplete suggestions → Select suggestion → Address fields populate → Validation passes → Continue.
- [ ] "Same as pickup" delivery: Enter pickup address → Check "Same as pickup" on delivery step → Delivery fields auto-fill → Can override if needed.
- [ ] Material type selection: Open material type dropdown → See categorized list → Select "Hazardous - Chemical Waste" → Hazardous flag set → Can enter quantity.
- [ ] Date selection with lead time: Open calendar → Past dates disabled → Dates within minimum lead time (2 days) disabled → Select valid future date → Select time window → Continue.
- [ ] File upload happy path: Drag PDF onto upload zone → See progress bar → File appears in list with thumbnail → Upload 2 more files → All 3 files listed → Can remove one → 2 files remain.
- [ ] Required field validation: Leave pickup address empty → Click Next → Inline error "Pickup address is required" → Fill address → Error clears → Next enabled.
- [ ] Material type validation: Enter quantity 0 → Next → Error "Quantity must be greater than 0" → Enter 100 tons → Error clears.
- [ ] Date validation - past date: Try to select yesterday (via manual date entry) → Error "Date cannot be in the past" → Select tomorrow → Still error "Minimum 2 business days required" → Select 3 days out → Validation passes.
- [ ] Address outside service area: Enter address in different state/region → Address validation fails → Error "Address outside service area" → Shows alternative contact option.
- [ ] File size validation: Upload 15MB PDF → Error "File size exceeds 10MB limit" → Upload 5MB PDF → Success.
- [ ] File type validation: Upload .exe file → Error "Invalid file type, use PDF, JPG, PNG, DOC, XLS" → Upload .pdf → Success.
- [ ] Maximum file limit: Upload 5 files successfully → Try to upload 6th file → Error "Maximum 5 attachments allowed" (or configured limit).
- [ ] Edit from review step: On review step → Click "Edit" for pickup location → Returns to step 2 → Change address → Navigate forward again → Review shows updated address.
- [ ] Form persistence: Fill 3 steps → Refresh page → See "Resume draft" option → Resume → All entered data intact → Continue from where left off.
- [ ] Abandon draft warning: Enter data in 2 steps → Try to navigate away → See "You have unsaved changes" confirmation → Cancel → Stay on page → Navigate back works without warning (Back button).
- [ ] Network error on submit: Disconnect network → Submit form → Error "Network error, please try again" with retry button → Reconnect → Retry → Success.
- [ ] Server validation error: Submit request with material type that's been disabled → Error "Selected material type is no longer available" → Select different type → Resubmit → Success.
- [ ] Authorization: User A (Company A) submits request → Request associated with Company A → User B (Company B) cannot see User A's request in their list.
- [ ] Multiple requests: Submit first request → See confirmation → Click "Create Another Request" → Form resets → Can submit second request independently.
- [ ] Accessibility: Tab through all fields in logical order → Focus visible → Use arrow keys in dropdown → Select with Enter → Navigate steps with keyboard → Screen reader announces step changes and errors.
- [ ] Mobile: Complete entire flow on mobile device → All steps accessible → Address autocomplete works → File upload works with camera option → Calendar picker mobile-friendly → Submit successful.

## Estimate

- Frontend: ~72h (XXL)
- Backend: ~79h (XXL) - Includes comprehensive transportation request infrastructure, entity design, geocoding integration, availability checking, file upload, email notifications, status management, and full test coverage. Excludes optional cost estimation logic (add +4h if needed).
- DevOps: ~34h (XL) - Includes database migrations, material type seeding, file storage configuration, geocoding API setup, email templates, monitoring, alerting, caching, and documentation. Excludes optional message queue setup (+2.5h) and webhook infrastructure (+3h).

**Total: ~185h (XXXL)**

---

## Backend Implementation Gap Summary

### Current State
The backend has **NO implementation** of transportation request functionality:
- ❌ **No Transportation Request Module** - No controllers, services, entities, or DTOs
- ❌ **No Material Type System** - No material catalog or categorization
- ❌ **No Address Validation** - No geocoding API integration
- ❌ **No Saved Locations** - No customer address management
- ❌ **No Availability System** - No capacity checking or scheduling logic
- ❌ **No Request Status Management** - No workflow or state machine

**Reusable Infrastructure:**
- ✅ **File Upload**: Multer config and FilesInterceptor exist (file-upload.config.ts) - can be adapted for attachments
- ✅ **Email Service**: EmailService exists with nodemailer/resend integration - need new templates
- ✅ **Authorization**: RolesGuard exists - needs company-level filtering
- ✅ **Queue System**: Bull queue with Redis configured - can be used for async operations

### Critical Gaps (100% Missing - Greenfield Feature)

#### 1. **Core Domain Entities (100% Missing)**
   - ❌ TransportationRequest entity with 25+ fields
   - ❌ MaterialType entity and catalog
   - ❌ TransportationRequestAttachment entity
   - ❌ SavedLocation entity
   - ❌ RequestStatusHistory entity (optional)
   - ❌ Database migrations for all tables
   - ❌ Entity relationships and foreign keys

#### 2. **All API Endpoints (100% Missing - 13 Endpoints)**
   - ❌ POST /transportation-requests (create)
   - ❌ GET /transportation-requests (list with filters)
   - ❌ GET /transportation-requests/:id (detail)
   - ❌ PATCH /transportation-requests/:id (update draft)
   - ❌ DELETE /transportation-requests/:id (cancel)
   - ❌ POST /transportation-requests/:id/submit (submit for approval)
   - ❌ POST /transportation-requests/:id/attachments (upload)
   - ❌ DELETE /transportation-requests/:id/attachments/:id (remove)
   - ❌ GET /material-types (catalog)
   - ❌ POST /addresses/validate (geocoding)
   - ❌ GET /addresses/saved (list)
   - ❌ POST /addresses/saved (create)
   - ❌ GET /availability (date checking)

#### 3. **Geocoding Integration (100% Missing)**
   - ❌ Google Maps / Here / Bing API integration
   - ❌ Address validation service
   - ❌ Address standardization and parsing
   - ❌ Coordinate extraction
   - ❌ Service area validation
   - ❌ Geocoding result caching (Redis)
   - ❌ API key configuration and management

#### 4. **Business Logic & Validation (100% Missing)**
   - ❌ Minimum lead time enforcement (2-5 business days)
   - ❌ Quantity limits by material type
   - ❌ Service area polygon validation
   - ❌ Blackout dates calendar
   - ❌ Capacity checking for dates
   - ❌ Status transition rules (state machine)
   - ❌ Duplicate request detection
   - ❌ Cancellation deadline enforcement

#### 5. **File Upload for Attachments (80% Missing)**
   - ✅ Multer config exists (file-upload.config.ts)
   - ❌ Attachment-specific endpoints
   - ❌ 10MB limit configuration (current is 10MB, so OK)
   - ❌ TransportationRequestAttachment entity
   - ❌ Association with requests
   - ❌ Multiple file handling per request

#### 6. **Email Notifications (90% Missing)**
   - ✅ EmailService exists
   - ❌ Request submission confirmation template
   - ❌ Status update notification templates
   - ❌ Cancellation confirmation template
   - ❌ Operations team notification
   - ❌ Email sending in submission workflow

#### 7. **Status Management (100% Missing)**
   - ❌ Request status enum definition
   - ❌ Status transition validation
   - ❌ Status history tracking
   - ❌ Workflow orchestration
   - ❌ Draft → Submitted → Approved → Scheduled → Completed flow

#### 8. **Authorization & Security (50% Missing)**
   - ✅ RolesGuard exists
   - ❌ Company-level filtering (user can only see own company's requests)
   - ❌ Row-level security on all endpoints
   - ❌ Rate limiting for request creation
   - ❌ Request ownership validation

#### 9. **Material Type System (100% Missing)**
   - ❌ MaterialType entity
   - ❌ Material categories (Hazardous, Non-Hazardous, Recyclable, Special)
   - ❌ Material catalog seeding
   - ❌ GET /material-types endpoint
   - ❌ Permit requirement flags
   - ❌ Handling instructions

#### 10. **Availability System (100% Missing)**
   - ❌ Capacity calculation logic
   - ❌ Scheduled requests query
   - ❌ Blackout dates management
   - ❌ Lead time calculation
   - ❌ Time slot generation
   - ❌ GET /availability endpoint

#### 11. **Saved Locations (100% Missing)**
   - ❌ SavedLocation entity
   - ❌ CRUD endpoints for saved addresses
   - ❌ Company-specific location lists
   - ❌ Location labels and metadata

#### 12. **Request Number Generation (100% Missing)**
   - ❌ Unique ID generation service
   - ❌ Format: TR-2024-001234
   - ❌ Uniqueness constraint
   - ❌ Sequential or hash-based logic

#### 13. **Testing (100% Missing)**
   - ❌ Unit tests for DTOs and validation
   - ❌ Unit tests for business rules
   - ❌ Integration tests for all 13 endpoints
   - ❌ Authorization test coverage
   - ❌ File upload test coverage

#### 14. **DevOps & Infrastructure (100% Missing)**
   - ❌ Database migrations (4 entities)
   - ❌ Material type seed data
   - ❌ Geocoding API setup and credentials
   - ❌ Service area configuration
   - ❌ Blackout dates calendar setup
   - ❌ Monitoring dashboards
   - ❌ Alerting for failures
   - ❌ Log aggregation

### Path Forward

This is a **complete greenfield feature** requiring full-stack implementation from scratch. The backend alone is ~79 hours of work.

**Phase 1: Foundation (Critical - ~25h)**
1. Design and create 4 core entities (TransportationRequest, MaterialType, SavedLocation, TransportationRequestAttachment) (~8.5h)
2. Database migrations with indexes (~2.5h)
3. Seed MaterialType catalog (~2h)
4. Integrate geocoding API (Google Maps/Here/Bing) (~3h)
5. Build address validation service (~3h)
6. Implement POST /transportation-requests endpoint (~4h)
7. Add CreateTransportationRequestDto with validation (~3h)

**Phase 2: Core Functionality (Critical - ~28h)**
1. Implement business rule validation (~3.5h)
2. Build availability checking service (~3.5h)
3. Implement request status management (~2.5h)
4. Add request submission logic and workflow (~3h)
5. Implement GET /transportation-requests list endpoint (~3h)
6. Add GET /transportation-requests/:id detail endpoint (~2h)
7. Build service area validation (~2.5h)
8. Implement file upload for attachments (~3h)
9. Add authorization middleware with company filtering (~2h)
10. Implement email notifications with templates (~2.5h)
11. Add request number generation (~1.5h)

**Phase 3: Additional Endpoints (High Priority - ~15h)**
1. PATCH /transportation-requests/:id for updates (~2.5h)
2. DELETE /transportation-requests/:id for cancellation (~2.5h)
3. GET /material-types endpoint (~2h)
4. POST/GET /addresses/saved endpoints (~3h)
5. GET /availability endpoint (~3h)
6. Attachment upload/delete endpoints (~2h)

**Phase 4: Quality & Production-Ready (Medium Priority - ~11h)**
1. Add rate limiting (~1.5h)
2. Implement audit logging (~2h)
3. Write unit tests (~3h)
4. Add integration tests (~4h)
5. Add duplicate request detection (~2.5h, not counted here - optional)

**Phase 5: DevOps & Monitoring (Critical - ~20h estimated from DevOps section)**
1. Database migrations and seeding
2. Geocoding API configuration
3. Service area and blackout dates setup
4. Email templates
5. Monitoring and alerting
6. Caching for geocoding
7. Documentation

### Summary

**Backend Completion:** **0%** (completely greenfield)

**Total Backend Effort:** ~79 hours (all missing)

**Key Challenges:**
1. **Geocoding API Integration** - New third-party service with costs per API call
2. **Complex Business Rules** - Lead times, capacity, service areas, blackout dates
3. **Status Workflow** - State machine with 7 states and transition rules
4. **Availability Calculation** - Complex logic considering capacity, materials, dates
5. **Service Area Validation** - Geographic polygon checks or geofencing

**Dependencies:**
- Geocoding API account and API key (Google Maps recommended)
- Service area definition (polygon coordinates or zip codes)
- Material type catalog from business team
- Business rules definition (lead times, quantity limits, cancellation policies)
- Blackout dates calendar

**Risk Mitigation:**
- Start with simplified service area (zip code list) before complex polygons
- Implement basic capacity checking before advanced material-specific logic
- Use existing file upload infrastructure (reduces 2-3h)
- Reuse email service (reduces 1-2h)
- Consider message queue for async operations (optional +2.5h but improves UX)

This is the largest backend story by effort (~79h), requiring complete domain modeling, third-party API integration, complex business logic, and extensive testing. No existing code can be reused except infrastructure (file upload, email, queues, auth guards).

## Summary of Key Features

### Core Functionality
- **Multi-Step Wizard**: Guided request creation through 6 steps (Pickup, Delivery, Material, Schedule, Details, Review) with progress tracking
- **Address Management**: Autocomplete with geocoding, saved locations, service area validation, map visualization
- **Material Selection**: Categorized material types with quantity/unit selection, hazardous material flagging
- **Smart Scheduling**: Calendar with availability checking, minimum lead time enforcement, blackout dates, time slot selection
- **Document Attachments**: Multi-file upload with drag-drop, progress tracking, type/size validation
- **Request Lifecycle**: Draft saving, submission workflow, status tracking, email notifications

### Technical Highlights
- **Geocoding Integration**: Google Maps/Here/Bing API for address validation and standardization
- **Service Area Validation**: Geofencing to ensure pickup/delivery within coverage areas
- **Availability Engine**: Real-time capacity checking based on scheduled requests, blackout dates, business rules
- **File Storage**: Multi-file attachment support with S3 or local filesystem
- **Form State Management**: Draft persistence with localStorage, resume incomplete requests, abandon warnings
- **Status State Machine**: Controlled status transitions (draft → submitted → approved → scheduled → in-progress → completed)
- **Email Notifications**: Request confirmation, status updates, cancellation notices
- **Request Number Generation**: Unique tracking numbers for customer reference

### Production-Ready Aspects
- Comprehensive entity design (TransportationRequest, MaterialType, SavedLocation, RequestStatusHistory, Attachments)
- Business rule validation (lead times, quantity limits, service areas, blackout dates)
- Geocoding API integration with caching to reduce costs
- Database migrations with performance-optimized indexes
- Material type catalog seeded with common waste categories
- Rate limiting to prevent request spam
- Audit logging for all request lifecycle events
- Monitoring for submission rates, API usage, success/failure metrics
- Alerting for geocoding failures, storage errors, processing delays
- Comprehensive test coverage (unit and integration tests)
- Responsive design for desktop, tablet, mobile
- Full accessibility support (keyboard navigation, screen readers)
- Data retention and backup policies for compliance

### Design Decisions Needed
1. **Geocoding Provider**: Google Maps (most accurate) vs Here (competitive pricing) vs Bing (Azure integration)
2. **Service Area Definition**: Polygon coordinates vs zip code list vs radius-based
3. **Cost Estimation**: Include estimated pricing in review step (complex pricing engine required, +4h backend)
4. **Message Queue**: Use async processing for emails, geocoding, availability checks (+2.5h DevOps, improves performance)
5. **Webhook Integration**: Enable customer systems to receive status updates (+3h backend, +3h DevOps)
6. **Map Provider**: Google Maps vs Mapbox vs Leaflet for location visualization
7. **Draft Auto-Save**: How frequently to save drafts (on field change vs every 30 seconds)
8. **Request Approval**: Auto-approve all requests or require operations team review before scheduling

### Risks & Dependencies
- **Geocoding API Costs**: Address validation on every request, need budget for API calls, caching reduces costs significantly
- **Service Area Data**: Need to define service area boundaries (polygon coordinates or zip codes) before development
- **Material Type Catalog**: Need business team to provide definitive list of material types, categories, handling requirements
- **Availability Logic**: Complex if considering capacity by material type, vehicle availability, route optimization
- **File Storage**: Requires S3 setup or local filesystem with adequate storage capacity
- **Email Infrastructure**: Depends on email service from auth story (Resend, SMTP, etc.)
- **Third-Party APIs**: Geocoding service account, API keys, billing alerts setup
- **Business Rules**: Minimum lead time, quantity limits, cancellation deadlines need to be defined by operations team

### Optional Enhancements (Not Included in Estimate)
- Cost estimation and pricing display in review step (+4h backend, +1h frontend)
- Message queue for async operations (+2.5h DevOps, better performance)
- Webhook system for external integrations (+3h backend, +3h DevOps)
- Request templates for frequently used configurations (+3h frontend, +2h backend)
- Bulk request creation via CSV upload (+5h frontend, +4h backend)
- Driver assignment and route optimization (+12h backend, separate feature)
- Real-time request tracking with GPS (+15h full stack, separate feature)
- SMS notifications in addition to email (+2h backend)
- Customer portal for tracking multiple requests with timeline view (+8h frontend)
- Advanced filtering and search for request history (+3h frontend, +2h backend)