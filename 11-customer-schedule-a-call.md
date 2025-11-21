# File: stories/11-customer-schedule-a-call.md

# Story 11: Customer – Schedule a Call

## Context

**Figma URL:**  
https://www.figma.com/design/yiCfEo9ZDgLyIkSiK7NVP2/4ami-Dashboard--copia-?node-id=2656-10428&t=dwNhFJQ5EbJ3AdrU-0

**Story goal (from PRD + Figma)**
Enable customers to request a call with 4AMI's service team to discuss additional services, support needs, or account questions through a streamlined scheduling workflow. The flow must support selecting the reason/topic for the call, choosing from available time slots or providing preferred contact times, entering contact details and phone preferences, adding optional notes or questions, and receiving confirmation with calendar integration. The system must integrate with the team's calendar to show real-time availability, send calendar invites to both customer and team, provide email confirmation with call details, and route requests to the appropriate team member based on topic selection.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – Initiate call request: Customer navigates to "Schedule a Call" from dashboard navigation or help menu, sees introduction explaining the call scheduling service (optional), clicks "Schedule Now" or "Request a Call" button to proceed.
- [x] Step 2 – Select call topic/reason: Customer chooses call topic from categorized options (New Services, Account Support, Technical Issues, Billing Questions, General Inquiry), sees description for each topic, can add custom topic in "Other" field if needed.
- [x] Step 3 – Choose scheduling method: Customer selects between "Choose from available times" (calendar view) or "Let team contact me" (flexible scheduling), both paths supported with different subsequent steps.
- [x] Step 4a – Calendar path: If calendar selected, customer sees weekly or monthly calendar view with available time slots highlighted, can navigate between dates, selects preferred date then time slot (15 or 30-minute intervals), sees timezone confirmation, confirms selection.
- [x] Step 4b – Flexible path: If "contact me" selected, customer enters preferred days/times as text (e.g., "weekday mornings" or "Tuesday afternoon"), can specify urgency level (Urgent, This Week, Within 2 Weeks, Flexible), provides time zone preference.
- [x] Step 5 – Contact information: Customer enters or confirms phone number (with country code selector), selects phone type (Mobile, Office, Other), optionally adds extension, enters backup phone number (optional), chooses preferred contact method (phone, video call, in-person if applicable).
- [x] Step 6 – Additional details: Customer adds notes or specific questions for the call (textarea with character limit), specifies language preference if multilingual support available, indicates if anyone else should join the call.
- [x] Step 7 – Review and confirm: Customer reviews complete request summary (topic, scheduled time or preferences, contact info, notes), can edit any section by navigating back, sees confirmation checkbox for terms (e.g., "I understand the team will call at the scheduled time"), clicks "Confirm Call Request" button.
- [x] Step 8 – Confirmation and calendar: After successful submission, customer sees confirmation screen with call request ID and details, receives option to add to personal calendar (Google Calendar, Outlook, iCal download), sees confirmation email notification sent message, gets estimated response time if using flexible scheduling, can view request in "My Calls" dashboard section.

**States to support**
- [x] Loading states – calendar loading with skeleton placeholders for time slots, availability check spinner when navigating dates, submit button loading during request creation, calendar integration loading when adding to personal calendar.
- [x] Error states – no available time slots found (suggest alternative dates or flexible scheduling), selected time slot no longer available (race condition, offer alternatives), phone number format validation errors, required fields missing (topic, contact method, phone), calendar integration failure (proceed without calendar add), submission failure with retry option.
- [x] Empty/edge states – all time slots booked (suggest flexible scheduling or future dates), customer profile missing phone number (prompt to add), timezone mismatch warning (detected timezone differs from profile), no team members available for selected topic (reroute to general inquiry or offer callback).
- [x] Success confirmation – confirmation screen with checkmark icon, call request ID displayed prominently, calendar event details shown, calendar integration options visible (Add to Google Calendar, Outlook, Download .ics), email confirmation message, link to view/manage all scheduled calls.

## Frontend

**Screens / components**
- [ ] `ScheduleCallWizard` (main container managing multi-step flow and state) – Status: Not Started
- [ ] `CallTopicSelector` (topic/reason selection with descriptions) – Status: Not Started
- [ ] `SchedulingMethodChoice` (choose calendar vs flexible scheduling) – Status: Not Started
- [ ] `CalendarTimeSlotPicker` (weekly/monthly calendar with available slots) – Status: Not Started
- [ ] `FlexibleSchedulingForm` (preferred times input and urgency selection) – Status: Not Started
- [ ] `ContactInformationForm` (phone number, contact method, preferences) – Status: Not Started
- [ ] `CallDetailsForm` (notes, questions, additional requirements) – Status: Not Started
- [ ] `CallReviewStep` (summary of all entered information) – Status: Not Started
- [ ] `CallConfirmationScreen` (success screen with calendar integration) – Status: Not Started
- [ ] `TimeSlotCard` (individual time slot display with selection) – Status: Not Started
- [ ] `CalendarIntegrationButtons` (Google Calendar, Outlook, iCal download) – Status: Not Started
- [ ] `PhoneNumberInput` (reusable phone input with country code selector) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/schedule-call` route with wizard layout (progress indicator, content area, navigation) matching Figma structure – Status: Not Started – Est: 2h
- [ ] Build `ScheduleCallWizard` container managing step navigation (Next, Back, Confirm), form state across steps, validation before advancing – Status: Not Started – Est: 2.5h
- [ ] Implement `CallTopicSelector` component with topic categories (New Services, Account Support, Technical Issues, Billing, General), radio buttons or cards with descriptions, "Other" option with custom text input – Status: Not Started – Est: 2h
- [ ] Create `SchedulingMethodChoice` component with two options: "Choose from available times" (shows calendar icon) and "Let team contact me" (shows flexible icon), clear descriptions for each option, radio button selection – Status: Not Started – Est: 1.5h
- [ ] Build `CalendarTimeSlotPicker` component with weekly or monthly calendar view, navigation between weeks/months, available time slots highlighted in green, unavailable slots grayed out, selected slot emphasized, timezone display – Status: Not Started – Est: 3h
- [ ] Implement calendar time slot loading: fetch available slots for selected date range, show loading skeleton during fetch, handle no availability scenario (show message, suggest alternatives), allow date navigation to find availability – Status: Not Started – Est: 2.5h
- [ ] Create `TimeSlotCard` component displaying time (e.g., "2:00 PM - 2:30 PM"), duration, team member name (optional), selection state (hover, selected), click to select – Status: Not Started – Est: 1.5h
- [ ] Build `FlexibleSchedulingForm` with preferred times textarea (with helpful placeholder: "e.g., Weekday mornings, Tuesday afternoon"), urgency dropdown (Urgent, This Week, Within 2 Weeks, Flexible), timezone selector, character limit on textarea – Status: Not Started – Est: 2h
- [ ] Implement `ContactInformationForm` with phone number input (country code selector, number field), phone type dropdown (Mobile, Office, Other), extension field (optional), backup phone number (optional), preferred contact method radio buttons (Phone Call, Video Call) – Status: Not Started – Est: 2.5h
- [ ] Create `PhoneNumberInput` reusable component integrating country code selector with flag icons, phone number validation as user types, formatting based on country (e.g., US: (XXX) XXX-XXXX), clear error messages – Status: Not Started – Est: 2h
- [ ] Build `CallDetailsForm` with notes/questions textarea (character limit 500), language preference dropdown (if multilingual support), checkbox for "Someone else will join", additional attendees field (conditional) – Status: Not Started – Est: 2h
- [ ] Implement `CallReviewStep` displaying complete request summary in organized sections (Topic, Schedule, Contact Information, Additional Details), each section with "Edit" button to jump back, confirmation checkbox for terms, all information read-only – Status: Not Started – Est: 2h
- [ ] Create `CallConfirmationScreen` with success icon/animation, call request ID prominently displayed, summary of scheduled call details (date/time or "Team will contact you"), email confirmation message, calendar integration section – Status: Not Started – Est: 2h
- [ ] Build `CalendarIntegrationButtons` component with three options: "Add to Google Calendar" (opens Google Calendar add), "Add to Outlook" (opens Outlook), "Download .ics file" (triggers .ics download), generate proper calendar event data with title, description, time, location (phone/video link) – Status: Not Started – Est: 2.5h
- [ ] Implement .ics file generation for calendar download: create iCalendar format file with event details, include call topic in title, add notes in description, set reminder 15 minutes before, trigger browser download – Status: Not Started – Est: 2h
- [ ] Add client-side validation for all steps: required topic selection, either calendar slot or flexible preferences required, phone number format validation, notes character limit enforcement, terms checkbox must be checked – Status: Not Started – Est: 2h
- [ ] Implement step navigation logic: disable Next until current step valid, Back navigation without validation, remember scroll position, prevent skipping steps via URL – Status: Not Started – Est: 1.5h
- [ ] Add API integration for POST /call-requests: build request payload from form state, handle submission with loading state, map server errors to form fields, handle success and navigate to confirmation – Status: Not Started – Est: 2h
- [ ] Implement GET /call-availability API integration: fetch available time slots for date range, pass timezone parameter, cache results, handle loading and error states, refresh on date navigation – Status: Not Started – Est: 2h
- [ ] Add timezone detection and selection: auto-detect user timezone on component mount, allow manual timezone selection, display timezone throughout flow, warn if detected timezone differs from profile, convert all times to user's timezone – Status: Not Started – Est: 2h
- [ ] Implement conditional rendering for calendar vs flexible path: show `CalendarTimeSlotPicker` if calendar method selected, show `FlexibleSchedulingForm` if flexible method selected, both paths lead to same contact information step – Status: Not Started – Est: 1.5h
- [ ] Add time slot selection handling: optimistic locking (check availability before final submission), handle race condition (slot taken by another user), show error if selected slot no longer available, offer alternative slots – Status: Not Started – Est: 2h
- [ ] Implement error handling across all steps: display inline validation errors, show toast notifications for API errors, provide retry buttons for failed operations, graceful handling of calendar integration failures – Status: Not Started – Est: 2h
- [ ] Add responsive design: ensure all steps work on desktop, tablet, mobile, stack form fields on small screens, mobile-friendly calendar picker, touch-optimized time slot selection – Status: Not Started – Est: 2h
- [ ] Implement accessibility features: keyboard navigation through steps, focus management (first field on step entry), ARIA labels for all inputs, screen reader announcements for step changes, calendar keyboard navigation – Status: Not Started – Est: 2h
- [ ] Polish UX details: smooth step transitions, helpful placeholder text and tooltips, field auto-focus on step entry, loading skeletons for async data, confirmation dialog before abandoning incomplete request – Status: Not Started – Est: 1.5h

## Backend

**APIs / endpoints**
- [ ] POST `/call-requests` – create new call scheduling request – **Status: missing** | Est: 3h | *No call request infrastructure exists*
- [ ] GET `/call-requests/:id` – retrieve specific call request details – **Status: missing** | Est: 1.5h
- [ ] GET `/call-requests` – list customer's call requests with filtering – **Status: missing** | Est: 2h
- [ ] PATCH `/call-requests/:id` – update or cancel call request – **Status: missing** | Est: 2h
- [ ] DELETE `/call-requests/:id/cancel` – cancel call request – **Status: missing** | Est: 1.5h
- [ ] GET `/call-availability` – fetch available time slots for calendar scheduling – **Status: missing** | Est: 3h | *No calendar API integration exists*
- [ ] POST `/call-requests/:id/reschedule` – reschedule existing call – **Status: missing** | Est: 2h

**Backend tasks**
- [ ] Design CallRequest entity schema with fields: id, requestNumber (auto-generated), customerId, companyId, topic (enum: New Services, Account Support, Technical Issues, Billing, General Inquiry, Other), customTopicDescription (for Other), schedulingType (calendar, flexible), scheduledDateTime (for calendar), preferredTimes (text for flexible), urgencyLevel (for flexible: Urgent, This Week, Within 2 Weeks, Flexible), contactPhone, phoneType (Mobile, Office, Other), phoneExtension, backupPhone, preferredContactMethod (Phone, Video, InPerson), notes, languagePreference, additionalAttendees, assignedTeamMemberId (FK to User), status (pending, confirmed, in_progress, completed, cancelled, no_show), timezone, createdAt, updatedAt, scheduledAt, completedAt, cancelledAt – **Status: missing** | Est: 2.5h
- [ ] Create database migration for CallRequest table with indexes: index on requestNumber, index on (customerId, status), index on (assignedTeamMemberId, scheduledDateTime), index on scheduledDateTime for availability queries – **Status: missing** | Est: 1.5h
- [ ] Implement POST `/call-requests` endpoint: accept CreateCallRequestDto, validate required fields (topic, contact phone, either scheduledDateTime or preferredTimes), auto-generate requestNumber, assign to appropriate team member based on topic, set initial status to 'pending' or 'confirmed', return created request with ID – **Status: missing** | Est: 3h
- [ ] Add CreateCallRequestDto with validation: required topic selection, conditional validation (if scheduling type calendar, scheduledDateTime required; if flexible, preferredTimes required), phone number format validation, notes character limit (500), timezone required, custom topic description required if topic is Other – **Status: missing** | Est: 2h
- [ ] Implement team member assignment logic: define topic-to-team mapping (e.g., Billing → accounting team, Technical → support team), check team member availability for scheduled time (if calendar), round-robin or load-balanced assignment within team, fallback to general pool if no specialist available – **Status: missing** | Est: 2.5h
- [ ] Build calendar availability service: integrate with team calendar system (Google Calendar, Outlook, or internal calendar), query availability for multiple team members, aggregate available slots (union of all availabilities), filter slots by business hours (9 AM - 5 PM or configured), exclude holidays and blackout dates, support timezone conversion – **Status: missing** | Est: 3.5h | *No calendar API integration exists (Google/Microsoft)*
- [ ] Implement calendar event creation: create calendar event for scheduled call in team member's calendar, include call details (topic, customer info, notes) in event description, set event reminder 15 minutes before, optionally send calendar invite to customer email – **Status: missing** | Est: 3h | *Need Google Calendar API or Microsoft Graph integration*
- [ ] Add time slot validation and race condition handling: verify selected time slot still available before confirming (query database for conflicts), implement optimistic locking or transaction-level locking, return error if slot taken with alternative suggestions, update availability cache on booking – **Status: missing** | Est: 2.5h
- [ ] Implement request number generation: generate unique alphanumeric call request numbers (e.g., CALL-2024-001234), ensure uniqueness with database constraint, include year/month for readability, sequential or hash-based generation – **Status: missing** | Est: 1h
- [ ] Build email notification system: send confirmation email to customer with call details (scheduled time or "team will contact you"), send assignment notification to team member with customer info and request details, send reminder emails 24 hours and 1 hour before call (for scheduled calls), use existing email infrastructure from auth story – **Status: missing** | Est: 2.5h | *EmailService exists, need new templates and reminder scheduling*
- [ ] Implement GET `/call-availability` endpoint: accept date range (startDate, endDate) and topic parameters, query team members qualified for topic, fetch their calendar availability, aggregate and deduplicate time slots, apply business hours filter, return slots grouped by date with timezone – **Status: missing** | Est: 3h
- [ ] Add authorization middleware: verify customer can only create/view their company's call requests, prevent access to other companies' requests, allow team members to view assigned requests, allow ADMINs to view all requests – **Status: missing** | Est: 1.5h | *RolesGuard exists but need company-level filtering*
- [ ] Implement status management: define status enum and transitions (pending → confirmed → in_progress → completed/no_show/cancelled), validate status transitions (can't complete if not started), track status history with timestamps, auto-transition to in_progress at scheduled time (optional background job) – **Status: missing** | Est: 2h
- [ ] Build reschedule logic (PATCH endpoint): verify request not in final status (completed, cancelled), check new time slot availability, update scheduledDateTime and status, update calendar event, send reschedule notification to customer and team, track reschedule history – **Status: missing** | Est: 2.5h
- [ ] Implement cancellation logic (DELETE endpoint): verify cancellation deadline (e.g., minimum 2 hours before scheduled time), soft delete with cancelled status and reason, send cancellation notification, delete or update calendar event, mark time slot as available again – **Status: missing** | Est: 2h
- [ ] Add rate limiting to call request creation: prevent spam (e.g., max 10 call requests per day per customer), apply @Throttle decorator, return 429 with clear message, different limits for urgent vs normal requests – **Status: missing** | Est: 1h
- [ ] Write unit tests for DTOs, validation logic, team assignment: test required field validation, test conditional validation (calendar vs flexible), test phone number format, test team assignment by topic, test timezone handling – **Status: missing** | Est: 2h
- [ ] Add integration tests for all endpoints: POST happy path (create request), POST with invalid data, GET availability with various date ranges, PATCH reschedule, DELETE cancel, authorization checks – **Status: missing** | Est: 2.5h
- [ ] Implement audit logging for call requests: log all request creations, status changes, reschedules, cancellations with user, timestamp, IP address, use activity log infrastructure – **Status: missing** | Est: 1.5h

**Additional production-ready tasks identified:**
- [ ] Implement no-show tracking and reporting – **Status: missing** | Est: 2h
- [ ] Add calendar sync for customer calendar integration (.ics files) – **Status: missing** | Est: 3h
- [ ] Implement call outcome recording – **Status: missing** | Est: 2h
- [ ] Create reminder system for upcoming calls (background jobs) – **Status: missing** | Est: 2.5h | *Bull queue exists, need reminder scheduling logic*
- [ ] Add timezone mismatch warning – **Status: missing** | Est: 1.5h

## DevOps / Infra

**Config / services**
- [ ] Calendar API credentials (Google Calendar or Microsoft Graph)
- [ ] Email notification templates for call lifecycle
- [ ] Background job scheduler for reminders
- [ ] Monitoring for call request operations

**DevOps tasks**
- [ ] Create database migration for CallRequest table with proper indexes on requestNumber, (customerId, status), (assignedTeamMemberId, scheduledDateTime), scheduledDateTime – Status: missing – Est: 1.5h
  **Gap:** Need migration for call request entity with performance-optimized indexes for common queries.
- [ ] Set up calendar API credentials: obtain Google Calendar API key or Microsoft Graph credentials for team calendar integration, configure OAuth 2.0 flow for accessing team calendars, store credentials securely in secrets manager, set up API quotas and billing alerts – Status: missing – Est: 2h
  **Gap:** Third-party calendar API integration required for availability checking and event creation.
- [ ] Configure environment variables for call scheduling: CALENDAR_API_PROVIDER (google, microsoft, internal), CALENDAR_API_KEY or CALENDAR_CLIENT_ID/SECRET, BUSINESS_HOURS_START, BUSINESS_HOURS_END, DEFAULT_CALL_DURATION_MINUTES, CANCELLATION_DEADLINE_HOURS, MAX_CALL_REQUESTS_PER_DAY – Status: missing – Est: 1h
  **Gap:** Configuration for calendar integration, business rules, and operational parameters.
- [ ] Create email templates for call requests: request confirmation (with scheduled time or callback notice), team assignment notification, reminder emails (24h and 1h before), reschedule confirmation, cancellation notification, no-show follow-up – Status: missing – Est: 2h
  **Gap:** Email templates using existing email infrastructure. Need branded templates with call details and calendar links.
- [ ] Set up background job scheduler for reminders: configure Bull queue or similar for scheduled reminder jobs, create worker to process reminder emails at scheduled times (24h, 1h before call), handle timezone differences for reminder timing, retry logic for failed email sends – Status: missing – Est: 2.5h
  **Gap:** Automated reminder system requires background job processing.
- [ ] Configure monitoring dashboards for call requests: track call request submission rate, monitor status distribution (pending, confirmed, completed, cancelled, no-show), measure response time for flexible scheduling, track calendar API usage and errors, monitor team utilization (calls per team member) – Status: missing – Est: 2h
  **Gap:** Business metrics and operational monitoring for call scheduling workflows.
- [ ] Set up alerting for call scheduling operations: alert on high request failure rate (>5% over 10min), alert on calendar API failures or quota exceeded, alert on assignment failures (no available team member), alert on high no-show rate (>20%), alert on reminder send failures – Status: missing – Est: 1.5h
  **Gap:** Proactive monitoring to catch issues before customer impact.
- [ ] Configure log aggregation for call operations: log all request creations with full payload, log team assignments with routing logic used, log status transitions with reasons, log calendar API calls and responses, integrate with centralized logging service – Status: missing – Est: 1.5h
  **Gap:** Structured logging for debugging, analytics, and audit trail.
- [ ] Set up calendar API rate limit handling: implement exponential backoff for API rate limits, cache calendar availability results (TTL 5-10 minutes), batch calendar queries where possible, monitor API quota usage with alerts at 80% – Status: missing – Est: 2h
  **Gap:** Prevent calendar API failures due to rate limits and reduce costs.
- [ ] Configure team member availability management: create interface for team members to set availability (working hours, time off), store availability preferences in database or sync with calendar, use availability data to filter time slots, handle conflicts and double-booking prevention – Status: missing – Est: 2.5h
  **Gap:** Team availability management system for accurate scheduling.
- [ ] Set up timezone handling infrastructure: configure timezone database for accurate conversions, validate timezone identifiers (IANA timezone names), handle daylight saving time transitions, display times in user's timezone throughout system – Status: missing – Est: 1.5h
  **Gap:** Robust timezone handling to prevent scheduling confusion.
- [ ] Create backup and archival policies: archive completed call requests after 1 year, retain cancelled/no-show requests for 6 months, backup call request data daily, purge very old records according to retention policy – Status: missing – Est: 1h
  **Gap:** Data retention and compliance with archival requirements.
- [ ] Document deployment and configuration: document calendar API setup steps (OAuth flow, credentials), document team assignment configuration (topic-to-team mapping), document business hours and blackout dates configuration, create runbook for common issues (calendar sync failures, double-booking, reminder failures) – Status: missing – Est: 1.5h
  **Gap:** Operations documentation for deployment and troubleshooting.
- [ ] Configure blackout dates and holidays: create database table or config for non-working days, seed with national holidays, allow manual addition of company blackout dates, integrate with availability checking logic to exclude these dates – Status: missing – Est: 1.5h
  **Gap:** Prevent scheduling on non-operational days.
- [ ] Set up .ics file generation infrastructure: implement iCalendar format generation library, configure event details (title, description, location, reminders), generate unique event UIDs, serve .ics files for download or email attachment – Status: missing – Est: 1.5h
  **Gap:** Calendar file generation for customer calendar integration.
- [ ] Configure notification delivery reliability: implement retry logic for failed email sends, track email delivery status, log failed notifications with reasons, provide manual retry mechanism for critical notifications – Status: missing – Est: 1.5h
  **Gap:** Ensure reliable delivery of time-sensitive notifications.

## Definition of Done

**Functional**
- [ ] Customer can initiate call scheduling request and navigate through multi-step wizard with proper step progression.
- [ ] Customer can select call topic from predefined categories (New Services, Account Support, Technical Issues, Billing, General) or enter custom topic.
- [ ] Customer can choose between two scheduling methods: calendar (select from available time slots) or flexible (provide preferred times and urgency).
- [ ] If calendar method selected, customer sees weekly/monthly view with available time slots, can navigate dates, select slot, and see timezone confirmation.
- [ ] If flexible method selected, customer enters preferred times as text, selects urgency level, provides timezone.
- [ ] Customer enters contact information: phone number with country code, phone type, extension (optional), backup phone (optional), preferred contact method (phone/video).
- [ ] Customer can add notes/questions (500 char limit), specify language preference, indicate additional attendees.
- [ ] Customer reviews complete request summary with all details, can edit any section by navigating back, must check confirmation terms.
- [ ] Form validates all required fields (topic, scheduling info, phone number) before allowing submission.
- [ ] Phone number validation ensures proper format with country code.
- [ ] Calendar availability integrates with team calendars to show real-time available slots filtered by topic expertise.
- [ ] On successful submission, call request is saved with pending/confirmed status, unique request number generated, assigned to appropriate team member based on topic.
- [ ] Customer sees confirmation screen with request ID, call details, calendar integration options (Google Calendar, Outlook, .ics download).
- [ ] Confirmation email sent to customer with call details, calendar invite (if scheduled time), next steps.
- [ ] Team member receives assignment notification with customer info and request details.
- [ ] For scheduled calls, calendar event created in team member's calendar with call details and 15-minute reminder.
- [ ] For scheduled calls, reminder emails sent to customer at 24 hours and 1 hour before call time.
- [ ] Authorization ensures customers only create/view their company's call requests, team members view assigned requests.
- [ ] All call request creations, status changes, and actions logged to audit log with user, timestamp, details.

**UX**
- [ ] Multi-step wizard layout matches Figma design with progress indicator, content area, Next/Back buttons.
- [ ] All form fields have proper labels, placeholders, and helper text matching Figma specifications.
- [ ] Topic selector displays categories clearly with descriptions, "Other" option with text input.
- [ ] Scheduling method choice shows clear options with icons and descriptions for calendar vs flexible paths.
- [ ] Calendar view displays available slots in green, unavailable in gray/disabled, selected slot emphasized, timezone shown.
- [ ] Time slot cards show time range, duration, team member (optional), clear selection state.
- [ ] Phone number input shows country code flags, validates as user types, formats appropriately.
- [ ] Review step displays all information in organized sections with clear labels, edit buttons visible.
- [ ] Confirmation screen shows success icon, request ID prominently, call details summary, calendar integration buttons.
- [ ] Calendar integration buttons clearly labeled (Add to Google Calendar, Outlook, Download .ics).
- [ ] Loading states show skeleton placeholders for calendar, spinners during submission, disabled form during processing.
- [ ] Inline validation errors appear below fields with error icons, clear messages immediately after validation trigger.
- [ ] Toast notifications for success, network errors provide clear feedback.
- [ ] Next button disabled until current step valid, Back navigation works without validation.
- [ ] Responsive design works on desktop, tablet, mobile with proper field stacking and touch-friendly interactions.
- [ ] Smooth step transitions, helpful tooltips, auto-focus on step entry.

**QA**
- [ ] Happy path - calendar method: Select topic → Choose calendar method → See available slots → Select date and time → Enter phone number → Add notes → Review → Submit → See confirmation with request ID → Receive confirmation email → Calendar event created.
- [ ] Happy path - flexible method: Select topic → Choose flexible method → Enter preferred times and urgency → Enter phone number → Add notes → Review → Submit → See confirmation → Receive email that team will contact.
- [ ] Topic selection: Select each predefined topic → Proceeds correctly → Select "Other" → Must enter custom description → Validation works.
- [ ] Calendar availability: Navigate between weeks → Slots load → See available/unavailable slots → Past dates disabled → Business hours only shown → Holidays excluded.
- [ ] Time slot race condition: User A selects slot → User B selects same slot → One succeeds → Other gets error "Slot no longer available" with alternative suggestions.
- [ ] Phone validation: Enter invalid phone → Error "Invalid phone number format" → Enter valid phone with country code → Validation passes.
- [ ] Required field validation: Skip topic → Next disabled → Select topic → Next enabled → Skip phone → Submit blocked → Error shown → Fill phone → Submits.
- [ ] Notes character limit: Enter 600 characters → Warning at 450 → Error at 501 → Cannot exceed limit.
- [ ] Timezone handling: Auto-detect timezone → Displayed throughout → Change timezone → Times update → Warning if mismatch with profile.
- [ ] Calendar integration - Google: Click "Add to Google Calendar" → Opens Google Calendar → Event details pre-filled → Can save to calendar.
- [ ] Calendar integration - .ics download: Click "Download .ics" → File downloads → Open in calendar app → Event details correct → Reminder set for 15 min before.
- [ ] Edit from review: On review step → Click "Edit" for contact info → Returns to contact step → Change phone → Navigate forward → Review shows updated phone.
- [ ] Team assignment: Submit with "Technical Issues" topic → Assigned to support team member → Submit with "Billing" → Assigned to accounting team.
- [ ] Email notifications: Submit request → Customer receives confirmation email → Team member receives assignment email → Request ID in both.
- [ ] Reminder emails: Schedule call for tomorrow → 24h reminder sent → 1h before call → Reminder sent → Emails contain correct time in customer's timezone.
- [ ] Reschedule request: View scheduled call → Click "Reschedule" → Select new time → Confirm → Calendar event updated → Notifications sent.
- [ ] Cancel request: View scheduled call → Click "Cancel" → Confirm cancellation → Status changes to cancelled → Notifications sent → Calendar event removed.
- [ ] Network error on submit: Disconnect network → Submit → Error "Network error, please try again" with retry → Reconnect → Retry → Success.
- [ ] Calendar API failure: Simulate calendar API down → Availability fetch fails → Graceful error "Unable to load availability, try flexible scheduling or contact support".
- [ ] Authorization: User A (Company A) creates request → Associated with Company A → User B (Company B) cannot view A's request.
- [ ] No available slots: All slots booked for 2 weeks → Calendar shows "No availability" → Suggests flexible scheduling or later dates.
- [ ] Accessibility: Tab through all fields → Focus visible → Use arrow keys in dropdowns → Select with Enter → Screen reader announces steps and errors.
- [ ] Mobile: Complete flow on mobile → All steps accessible → Calendar picker mobile-friendly → Phone input works → .ics download triggers → Successful submission.

## Estimate

- Frontend: ~56h (XL)
- Backend: ~53h (XL) - Includes call request infrastructure, calendar API integration (Google Calendar or Microsoft Graph), team assignment logic, availability checking, email notifications with reminders, .ics file generation, and comprehensive testing.
- DevOps: ~27h (L) - Includes database migrations, calendar API credentials setup, email templates, background job scheduler for reminders, monitoring, alerting, timezone handling, and blackout dates configuration.

**Total: ~136h (XXL)**

---

## Backend Implementation Gap Summary

### Current State
The backend has **NO implementation** of call scheduling functionality:
- ❌ **No Call Request Module** - No controllers, services, entities, or DTOs
- ❌ **No Calendar API Integration** - No Google Calendar or Microsoft Graph integration
- ❌ **No Team Assignment System** - No topic-to-team routing
- ❌ **No Availability Checking** - No calendar availability aggregation
- ❌ **No Request Status Management** - No workflow or state machine
- ❌ **No Reminder System** - No background jobs for scheduled reminders

**Reusable Infrastructure:**
- ✅ **Email Service**: EmailService exists with nodemailer/resend integration - need new templates
- ✅ **Authorization**: RolesGuard exists - needs company-level filtering
- ✅ **Queue System**: Bull queue with Redis configured - can be used for reminder scheduling

### Critical Gaps (100% Missing - Greenfield Feature)

#### 1. **Core Domain Entity (100% Missing)**
   - ❌ CallRequest entity with 25+ fields (topic, scheduling type, contact info, team assignment, status, timestamps)
   - ❌ Database migration for CallRequest table
   - ❌ Entity relationships and foreign keys (customerId, assignedTeamMemberId)
   - ❌ Indexes for query optimization

#### 2. **All API Endpoints (100% Missing - 7 Endpoints)**
   - ❌ POST /call-requests (create)
   - ❌ GET /call-requests (list with filters)
   - ❌ GET /call-requests/:id (detail)
   - ❌ PATCH /call-requests/:id (update)
   - ❌ DELETE /call-requests/:id/cancel (cancel)
   - ❌ GET /call-availability (fetch available time slots)
   - ❌ POST /call-requests/:id/reschedule (reschedule)

#### 3. **Calendar API Integration (100% Missing)**
   - ❌ Google Calendar API or Microsoft Graph integration
   - ❌ OAuth 2.0 configuration for calendar access
   - ❌ Team calendar availability querying
   - ❌ Calendar event creation (programmatic)
   - ❌ Calendar event updates (reschedule/cancel)
   - ❌ Calendar invite generation for customers
   - ❌ API rate limiting and error handling
   - ❌ Availability result caching

#### 4. **Availability System (100% Missing)**
   - ❌ Multi-calendar availability aggregation
   - ❌ Business hours filtering
   - ❌ Blackout dates and holiday exclusion
   - ❌ Timezone conversion for slots
   - ❌ Topic-based team member filtering
   - ❌ Time slot deduplication
   - ❌ GET /call-availability endpoint

#### 5. **Team Assignment Logic (100% Missing)**
   - ❌ Topic-to-team mapping configuration
   - ❌ Team member availability checking
   - ❌ Load balancing / round-robin assignment
   - ❌ Fallback to general pool
   - ❌ Assignment notification system

#### 6. **Status Management (100% Missing)**
   - ❌ Status enum definition (pending, confirmed, in_progress, completed, cancelled, no_show)
   - ❌ Status transition rules and validation
   - ❌ Status history tracking with timestamps
   - ❌ Auto-transition to in_progress (optional)
   - ❌ State machine implementation

#### 7. **Email Notifications (90% Missing)**
   - ✅ EmailService exists
   - ❌ Confirmation email template (scheduled time or callback notice)
   - ❌ Team assignment notification template
   - ❌ Reminder email templates (24h and 1h before)
   - ❌ Reschedule confirmation template
   - ❌ Cancellation notification template
   - ❌ No-show follow-up template

#### 8. **Reminder System (100% Missing)**
   - ❌ Background job scheduler for reminders
   - ❌ Reminder scheduling logic (24h, 1h before)
   - ❌ Timezone-aware reminder timing
   - ❌ Retry logic for failed emails
   - ❌ Reminder status tracking

#### 9. **Race Condition Prevention (100% Missing)**
   - ❌ Time slot conflict detection
   - ❌ Optimistic locking or transaction-level locking
   - ❌ Alternative slot suggestions
   - ❌ Availability cache invalidation on booking

#### 10. **Reschedule & Cancellation (100% Missing)**
   - ❌ Reschedule endpoint with validation
   - ❌ Cancellation deadline enforcement
   - ❌ Calendar event updates
   - ❌ Reschedule/cancellation notifications
   - ❌ Time slot release logic

#### 11. **Request Number Generation (100% Missing)**
   - ❌ Unique ID generation service
   - ❌ Format: CALL-2024-001234
   - ❌ Uniqueness constraint
   - ❌ Sequential or hash-based logic

#### 12. **.ics Calendar File Generation (100% Missing)**
   - ❌ iCalendar format implementation
   - ❌ Event details (title, description, location, reminders)
   - ❌ Unique event UID generation
   - ❌ File serving for download
   - ❌ Email attachment support

#### 13. **Authorization & Security (50% Missing)**
   - ✅ RolesGuard exists
   - ❌ Company-level filtering (customer sees only own requests)
   - ❌ Team member access (view assigned requests)
   - ❌ Row-level security on all endpoints
   - ❌ Rate limiting for request creation

#### 14. **Testing (100% Missing)**
   - ❌ Unit tests for DTOs and validation
   - ❌ Unit tests for team assignment logic
   - ❌ Integration tests for all 7 endpoints
   - ❌ Calendar API integration tests
   - ❌ Authorization test coverage
   - ❌ Timezone handling tests

#### 15. **DevOps & Infrastructure (100% Missing)**
   - ❌ Database migrations
   - ❌ Calendar API credentials (Google/Microsoft)
   - ❌ OAuth 2.0 configuration
   - ❌ Email templates (6 templates)
   - ❌ Background job scheduler setup
   - ❌ Business hours configuration
   - ❌ Blackout dates calendar
   - ❌ Timezone handling infrastructure
   - ❌ Monitoring dashboards
   - ❌ Alerting for failures

### Path Forward

This is a **complete greenfield feature** requiring full-stack implementation from scratch. The backend alone is ~53 hours of work.

**Phase 1: Foundation (Critical - ~14h)**
1. Design and create CallRequest entity (~2.5h)
2. Database migration with indexes (~1.5h)
3. Integrate calendar API (Google Calendar or Microsoft Graph) (~3.5h)
4. Implement POST /call-requests endpoint (~3h)
5. Add CreateCallRequestDto with validation (~2h)
6. Implement request number generation (~1h)

**Phase 2: Core Functionality (Critical - ~20h)**
1. Build calendar availability service (~3.5h)
2. Implement GET /call-availability endpoint (~3h)
3. Implement calendar event creation (~3h)
4. Add team member assignment logic (~2.5h)
5. Add time slot validation and race condition handling (~2.5h)
6. Implement status management (~2h)
7. Build email notification system with templates (~2.5h)
8. Add authorization middleware with company filtering (~1.5h)

**Phase 3: Additional Endpoints (High Priority - ~8h)**
1. GET /call-requests list endpoint (~2h)
2. GET /call-requests/:id detail endpoint (~1.5h)
3. Build reschedule logic (~2.5h)
4. Implement cancellation logic (~2h)

**Phase 4: Reminders & Calendar Sync (Medium Priority - ~6h)**
1. Create reminder system with background jobs (~2.5h)
2. Add .ics calendar file generation (~3h)
3. Implement timezone mismatch warning (~1.5h, optional)

**Phase 5: Quality & Production-Ready (Medium Priority - ~5h)**
1. Add rate limiting (~1h)
2. Implement audit logging (~1.5h)
3. Write unit tests (~2h)
4. Add integration tests (~2.5h, counted separately)

**Phase 6: DevOps & Monitoring (Critical - ~15h estimated from DevOps section)**
1. Calendar API credentials setup
2. Email templates (6 templates)
3. Background job scheduler for reminders
4. Business hours and blackout dates configuration
5. Monitoring and alerting
6. Timezone handling infrastructure
7. Documentation

### Summary

**Backend Completion:** **0%** (completely greenfield)

**Total Backend Effort:** ~53 hours (all missing)

**Key Challenges:**
1. **Calendar API Integration** - New third-party service (Google/Microsoft) with OAuth 2.0 setup
2. **Availability Aggregation** - Query multiple calendars, merge slots, handle conflicts
3. **Race Conditions** - Prevent double-booking when multiple users select same slot
4. **Timezone Handling** - Convert times across timezones, handle DST transitions
5. **Team Assignment** - Smart routing based on topic and availability
6. **Reminder System** - Background jobs for scheduled reminders at specific times

**Dependencies:**
- Calendar API account (Google Workspace or Microsoft 365)
- OAuth 2.0 credentials for calendar access
- Topic-to-team mapping definition from operations
- Business hours configuration
- Blackout dates calendar
- Team member availability management

**Risk Mitigation:**
- Start with single calendar provider (Google Calendar) before adding Microsoft Graph
- Implement basic team assignment before load balancing
- Use Bull queue infrastructure for reminders (reduces 1-2h)
- Reuse email service (reduces 1-2h)
- Consider starting with flexible scheduling only, add calendar scheduling later (reduces ~10h for MVP)

This is a medium-sized backend story (~53h) requiring calendar API integration (most complex part), team assignment logic, reminder scheduling, and comprehensive email notifications. The calendar API integration alone accounts for ~10 hours of the work. No existing code can be reused except infrastructure (email, queues, auth guards).

## Summary of Key Features

### Core Functionality
- **Multi-Step Wizard**: Guided call request creation through 5-6 steps (Topic, Scheduling Method, Calendar/Flexible, Contact Info, Details, Review)
- **Flexible Scheduling**: Two paths - calendar-based (select from available slots) or flexible (provide preferred times)
- **Calendar Integration**: Real-time availability from team calendars, automatic event creation, customer calendar sync
- **Smart Routing**: Automatic team member assignment based on topic expertise and availability
- **Email Notifications**: Confirmation, reminders (24h and 1h before), team assignment, reschedule/cancellation notices
- **Request Management**: View, reschedule, cancel call requests with proper validation

### Technical Highlights
- **Calendar API Integration**: Google Calendar or Microsoft Graph for team availability and event management
- **Availability Aggregation**: Query multiple team calendars, aggregate available slots, filter by business hours and blackout dates
- **Timezone Handling**: Auto-detection, conversion, display in user's timezone throughout flow
- **Race Condition Prevention**: Optimistic locking to prevent double-booking of time slots
- **iCalendar Generation**: Create .ics files for customer calendar integration with reminders
- **Team Assignment Logic**: Topic-to-team mapping, availability checking, load balancing
- **Background Jobs**: Scheduled reminder emails at 24h and 1h before calls
- **Request Number Generation**: Unique tracking numbers for customer reference

### Production-Ready Aspects
- Comprehensive entity design (CallRequest with calendar/flexible scheduling support)
- Calendar API integration with rate limiting, caching, and error handling
- Team member availability management and assignment logic
- Database migrations with performance-optimized indexes
- Email notification system with branded templates for all lifecycle events
- Background job scheduler for automated reminders
- Rate limiting to prevent request spam
- Audit logging for all call request operations
- Monitoring for submission rates, calendar API usage, team utilization, no-show rates
- Alerting for calendar API failures, assignment failures, high no-show rates
- Timezone handling with DST support
- Blackout dates and holiday calendar
- Comprehensive test coverage (unit and integration tests)
- Responsive design for desktop, tablet, mobile
- Full accessibility support

### Design Decisions Needed
1. **Calendar Provider**: Google Calendar (most common) vs Microsoft Graph (Outlook/Office 365) vs internal calendar system
2. **Team Assignment Strategy**: Manual assignment by admin vs automatic based on topic vs round-robin
3. **Call Duration**: Fixed duration (15 min, 30 min) vs variable based on topic
4. **Availability Window**: How far in advance to show availability (2 weeks, 1 month)
5. **Reminder Timing**: 24h and 1h default vs configurable per request
6. **No-Show Policy**: How to handle repeated no-shows (warnings, scheduling restrictions)
7. **Video Call Support**: Include video call links (Zoom, Teams, Google Meet) or phone only
8. **Multi-Language Support**: Include language preference selection for multilingual support

### Risks & Dependencies
- **Calendar API Access**: Requires Google Workspace or Microsoft 365 account with API access, proper OAuth setup
- **Calendar API Costs**: API usage fees based on volume, need budget and quota monitoring
- **Team Calendar Accuracy**: Depends on team members keeping calendars up-to-date
- **Timezone Complexity**: Handling DST transitions, international customers, timezone mismatches
- **Race Conditions**: Multiple customers selecting same slot simultaneously, need proper locking
- **Email Infrastructure**: Depends on email service from auth story for notifications
- **Background Jobs**: Requires Redis or similar for Bull queue, worker process for reminders
- **Topic-Team Mapping**: Need clear definition from operations team on which topics route to which teams

### Optional Enhancements (Not Included in Estimate)
- Video call link generation (Zoom, Teams, Google Meet integration) (+4h backend, +2h frontend)
- SMS reminders in addition to email (+2h backend, +1h frontend)
- Customer self-service reschedule without team approval (+2h frontend, +2h backend)
- Team availability calendar UI for admins to view/manage (+6h frontend, +3h backend)
- Call recording integration (for quality/training) (+8h backend, compliance requirements)
- Customer satisfaction survey after call completion (+4h frontend, +3h backend)
- Analytics dashboard for call volume, topic trends, no-show rates (+8h frontend, +4h backend)
- Recurring call scheduling (weekly status calls, etc.) (+5h frontend, +4h backend)
- Wait list for high-demand time slots (+3h frontend, +3h backend)
- Multi-language customer support with language-specific team routing (+3h backend)