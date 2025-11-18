# File: stories/04-customer-signup-login.md

# Story 4: Customer Signup / Login

## Context

**Figma URL:**
https://www.figma.com/design/JDoPGdZ6anmqLy7YFI9sXp/4ami-Dashboard?node-id=3009-78475

**Story goal (from PRD + Figma)**
Enable customers to create accounts and authenticate into the 4AMI platform. The signup flow includes multi-step form completion with password strength validation, email confirmation, and secure login with session management. Customers should be able to sign up, verify their email, log in with credentials, and access their dashboard upon successful authentication.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – Signup form (Step 1): Customer navigates to signup page, sees progress bar (Step 1 of 2), fills out Email, Password, and Confirm Password fields, clicks "Sign Up" to proceed to next step.
- [x] Step 2 – Signup form (Step 2): Customer sees progress bar (Step 2 of 2), password field shows tooltip with requirements (8 characters, 1 uppercase, 1 lowercase, 1 number) with visual indicators, can click "Back" to return to step 1, clicks "Sign Up" to submit.
- [x] Step 3 – Email confirmation: After signup submission, customer sees confirmation screen with title, subtitle, instructions to check email, "Resend Email" button (if applicable), and support contact information.
- [x] Step 4 – Login: Customer navigates to login page, enters Email and Password, can toggle "Remember me" checkbox, can click "Forgot Password" link (links to reset password flow from Story 1), clicks "Sign In" button to authenticate.
- [x] Step 5 – Dashboard redirect: After successful login, customer is redirected to their dashboard with sidebar, topbar, and dashboard content visible.

**States to support**
- [x] Loading states – signup/login buttons show loading spinner during submission, form fields disabled during authentication, no navigation allowed until completion.
- [x] Error states – invalid email format, weak password (doesn't meet requirements), password mismatch, account already exists, invalid credentials on login, account not verified, network errors with retry option.
- [x] Empty/edge states – empty form with placeholders, partial form completion, password tooltip appears on focus/input, password strength indicators update in real-time.
- [x] Success states – email confirmation screen after signup, successful login redirect to dashboard, session persistence with "Remember me" option.

## Frontend

**Screens / components**
- [ ] `SignupStep1View` (email, password, confirm password fields with progress bar) – Status: Not Started
- [ ] `SignupStep2View` (password field with tooltip showing requirements, back button) – Status: Not Started
- [ ] `EmailConfirmationView` (confirmation message, instructions, support info) – Status: Not Started
- [ ] `LoginView` (email, password, remember me checkbox, forgot password link) – Status: Not Started
- [ ] `PasswordStrengthTooltip` (tooltip component showing password requirements with checkmarks) – Status: Not Started
- [ ] `ProgressBar` (multi-step progress indicator component) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/signup` route with layout shell (logo sidebar, main content area) matching Figma structure – Status: Not Started – Est: 2h
- [ ] Build `SignupStep1View` component with header, progress bar (Step 1 of 2), Email, Password, Confirm Password fields, Sign Up button matching Figma layout – Status: Not Started – Est: 2.5h
- [ ] Implement `ProgressBar` component with step indicator, progress fill, step labels, reusable for multi-step flows – Status: Not Started – Est: 2h
- [ ] Build `SignupStep2View` component with progress bar (Step 2 of 2), password field with tooltip trigger, Back button, Sign Up button – Status: Not Started – Est: 2h
- [ ] Create `PasswordStrengthTooltip` component with requirements list (8 characters, uppercase, lowercase, number), real-time validation indicators (checkmarks/X), positioning logic near password field – Status: Not Started – Est: 2.5h
- [ ] Implement password strength validation: check requirements in real-time as user types, update tooltip indicators, prevent submission if requirements not met – Status: Not Started – Est: 2h
- [ ] Add form validation for signup: email format, password match validation, required field checks, inline error messages – Status: Not Started – Est: 2h
- [ ] Wire signup form submission: collect form data from both steps, call signup API, handle loading state, navigate to email confirmation on success – Status: Not Started – Est: 2h
- [ ] Build `EmailConfirmationView` component with title, subtitle, instructions text, button (Resend Email if applicable), support contact info matching Figma – Status: Not Started – Est: 2h
- [ ] Scaffold `/login` route with layout shell (logo sidebar, main content, signup link at top) matching Figma – Status: Not Started – Est: 2h
- [ ] Build `LoginView` component with header, Email and Password fields, "Remember me" checkbox, "Forgot Password" link, "Sign In" button matching Figma layout – Status: Not Started – Est: 2.5h
- [ ] Implement password visibility toggle (eye icon) for password fields in both signup and login forms – Status: Not Started – Est: 1.5h
- [ ] Add form validation for login: email format, required field checks, inline error messages – Status: Not Started – Est: 1.5h
- [ ] Wire login form submission: call login API with credentials and remember_me flag, handle loading state, store auth token/session, redirect to dashboard on success – Status: Not Started – Est: 2.5h
- [ ] Implement auth token/session storage: store JWT token in localStorage or httpOnly cookie, handle "Remember me" option (extended expiry), create auth context/provider – Status: Not Started – Est: 2.5h
- [ ] Add protected route logic: redirect unauthenticated users to login, redirect authenticated users away from login/signup pages, handle token expiry – Status: Not Started – Est: 2h
- [ ] Implement error handling: display server-side error messages (account exists, invalid credentials, account not verified), network error handling with retry, error toast notifications – Status: Not Started – Est: 2h
- [ ] Add responsive behavior for signup/login forms, ensure proper layout on tablet/desktop breakpoints shown in Figma – Status: Not Started – Est: 2h
- [ ] Polish accessibility: keyboard navigation, focus management, ARIA labels, screen reader announcements for errors and success – Status: Not Started – Est: 2h

## Backend

**APIs / endpoints**
- [ ] POST `/auth/signup` – create customer account with email, password, send verification email – Status: partial – Est: 2h
  **Current:** Endpoint exists (auth.controller.ts:38) with SignUpDto. **Gap:** (1) Password validation too weak (MinLength 6, spec requires 8 chars + uppercase + lowercase + number), (2) No confirmPassword field in DTO, (3) Email verification sent but not enforced on login. Need to update SignUpDto validation to match spec requirements.
- [ ] POST `/auth/login` – authenticate customer with email/password, return JWT token – Status: partial – Est: 2h
  **Current:** POST `/auth/signin` endpoint exists (auth.controller.ts:71) with SignInDto. **Gap:** (1) No rememberMe field in DTO, (2) Fixed JWT expiry (24h), doesn't support extended expiry for "remember me", (3) May not enforce email verification check. Need to add rememberMe support and conditional token expiry.
- [ ] POST `/auth/logout` – invalidate session/token (optional, for explicit logout) – Status: missing – Est: 1.5h
  **Gap:** No logout endpoint exists. Current JWT implementation is stateless (can't invalidate server-side). Need to either: (1) Add token blacklist with Redis, (2) Return success without server-side invalidation (client removes token), (3) Implement refresh token rotation. Option 2 is simplest for MVP.
- [ ] POST `/auth/verify-email` – verify email token and activate account (if email verification required) – Status: done
  **Current:** Endpoint exists (auth.controller.ts:120) with verifyEmail service method (auth.service.ts:233-255). Validates token and email, updates isEmailVerified flag.
- [ ] POST `/auth/resend-verification` – resend verification email to customer (optional) – Status: missing – Est: 2h
  **Gap:** No resend endpoint exists. Need to: (1) Create endpoint accepting email, (2) Find user by email, (3) Check if already verified, (4) Generate new verification token, (5) Send email, (6) Add rate limiting (max 3 resends per hour).

**Backend tasks**
- [ ] Design customer user data model/schema with fields: email (unique), password_hash, email_verified, created_at, updated_at, last_login, account_status – Status: done
  **Current:** User entity exists (user.entity.ts) with all required fields: email (unique, line 25-26), password (hashed, line 28-30), isEmailVerified (line 60-61), createdAt (line 84-85), updatedAt (line 87-88), lastLoginAt (line 75-76), isActive for account status (line 57-58).
- [ ] Create database migration for customers/users table with unique index on email, appropriate indexes for lookups – Status: missing – Est: 2h
  **Gap:** Using synchronize:true (app.module.ts:53) instead of migrations. User entity has @Column({ unique: true }) on email but no explicit indexes. Need: (1) Create migration for users table, (2) Add unique index on email, (3) Add index on emailVerificationToken for verify-email lookups, (4) Add index on isActive and isEmailVerified for filtering.
- [ ] Implement POST `/auth/signup` endpoint with request body validation (email format, password strength requirements: 8 chars, uppercase, lowercase, number) – Status: partial – Est: 2h
  **Current:** Endpoint exists but password validation is weak. SignUpDto has @MinLength(6) (signup.dto.ts:18). **Gap:** Need to update to match spec: @MinLength(8) + @Matches regex for uppercase, lowercase, number. Can reuse pattern from CustomerSignupDto (customer-signup.dto.ts:63).
- [ ] Add duplicate email checking: verify email doesn't already exist, return appropriate error message if account exists – Status: done
  **Current:** signUp method checks for existing user (auth.service.ts:33-40) and throws ConflictException. Works correctly.
- [ ] Implement password hashing: use bcrypt or similar with appropriate salt rounds, store hashed password in database – Status: done
  **Current:** User entity has @BeforeInsert and @BeforeUpdate hooks with bcrypt hashing using 12 salt rounds (user.entity.ts:117-123). Industry standard implementation.
- [ ] Create customer account record in database with email_verified=false initially, handle database errors gracefully – Status: done
  **Current:** signUp creates user with emailVerificationToken (auth.service.ts:46-52). Email verification defaults to false. Database errors handled by NestJS exception filters.
- [ ] Integrate email service for verification: generate verification token, send verification email with link, store token with expiry – Status: partial – Est: 1h
  **Current:** Email verification sent (auth.service.ts:55-63) with UUID token. **Gap:** No token expiry tracking. emailVerificationToken has no associated timestamp/expiry field. Need to add emailVerificationTokenExpires field to User entity or use JWT with expiry for verification tokens.
- [ ] Implement POST `/auth/login` endpoint with request body validation (email format, password required) – Status: done
  **Current:** POST `/auth/signin` endpoint exists with SignInDto validation (@IsEmail, @IsString). LocalStrategy validates credentials (auth.service.ts:154-219).
- [ ] Add credential verification: lookup user by email, compare password hash, verify account is active and email verified (if required) – Status: partial – Est: 1h
  **Current:** validateUser method looks up user and compares password (auth.service.ts:154-219). signIn checks isActive (auth.service.ts:141-144). **Gap:** May not enforce isEmailVerified check. Need to add check and throw appropriate error if email not verified.
- [ ] Generate JWT token on successful login: include user ID, email, role, set appropriate expiry (short for normal, extended for "remember me") – Status: partial – Est: 2h
  **Current:** generateToken creates JWT with user ID, email, role (auth.service.ts:334-342). Fixed expiry from JWT_EXPIRES_IN config (default 24h). **Gap:** No conditional expiry based on rememberMe. Need to: (1) Accept rememberMe parameter, (2) Set 7d expiry if rememberMe=true, 24h otherwise, (3) Update SignInDto and signIn method signature.
- [ ] Update last_login timestamp on successful authentication, track login attempts for security monitoring – Status: partial – Est: 2h
  **Current:** lastLoginAt updated on successful login (auth.service.ts:147). **Gap:** No failed login attempt tracking. Need: (1) Add failedLoginAttempts and lockedUntil fields to User entity, (2) Increment counter on failed login, (3) Lock account after 5 failed attempts for 15min, (4) Reset counter on successful login, (5) Log failed attempts for security monitoring.
- [ ] Implement POST `/auth/verify-email` endpoint: validate verification token, check expiry, update email_verified flag, activate account – Status: partial – Est: 1h
  **Current:** Endpoint exists and validates token (auth.service.ts:233-255). **Gap:** No expiry check (no expiry field exists). If adding token expiry, need to validate it here.
- [ ] Add POST `/auth/resend-verification` endpoint (optional): generate new verification token, resend email, handle rate limiting – Status: missing – Est: 2.5h
  **Gap:** No endpoint exists. Need to: (1) Create controller method, (2) Accept email in body, (3) Find user and check if already verified, (4) Generate new UUID token, (5) Update user.emailVerificationToken, (6) Send email, (7) Add rate limiting (@Throttle decorator), (8) Return success message.
- [ ] Implement rate limiting for auth endpoints: limit signup attempts per IP/email, limit login attempts to prevent brute force, return appropriate error messages – Status: missing – Est: 2.5h
  **Gap:** No @nestjs/throttler configured (same as other stories). Need to: (1) Install @nestjs/throttler, (2) Configure ThrottlerModule in app.module.ts, (3) Apply @Throttle decorators to auth endpoints (signup: 5/hour, login: 10/15min, resend: 3/hour), (4) Implement custom rate limit strategy per email for login, (5) Return 429 with clear messages.
- [ ] Add authentication middleware: verify JWT token, extract user info, handle token expiry, refresh token logic (if applicable) – Status: done
  **Current:** JWT strategy exists (jwt.strategy.ts) with token validation and user extraction. JwtAuthGuard applied via @UseGuards or globally. Token expiry handled by passport-jwt (returns 401 on expired token).
- [ ] Implement POST `/auth/logout` endpoint (optional): invalidate token, clear session, return success response – Status: missing – Est: 1.5h
  **Gap:** No logout endpoint. With stateless JWT, need token blacklist or client-side removal. Simplest approach: (1) Create endpoint that returns success without server-side action, (2) Client removes token from storage, (3) Optional: add Redis token blacklist for enterprise security.
- [ ] Add audit logging for auth events: log signup attempts, successful logins, failed login attempts, email verifications for security monitoring – Status: missing – Est: 2.5h
  **Gap:** Only console.log statements (auth.service.ts:139, 155, etc.). Need structured logging: (1) Create AuditLog entity or reuse ActivityLog from dashboard story, (2) Log signup success/failure with user_id, email, IP, timestamp, (3) Log login attempts (success/failure) with reason, (4) Log email verifications, (5) Log rate limit violations, (6) Integrate with log aggregation service.
- [ ] Write unit tests for password hashing, email validation, password strength validation, token generation – Status: missing – Est: 3h
  **Gap:** auth.spec.ts has trivial placeholder tests (test/auth.spec.ts). Need unit tests for: (1) User entity password hashing (bcrypt integration), (2) validatePassword method, (3) SignUpDto validation (email format, password strength), (4) CustomerSignupDto validation (all requirements), (5) generateToken method (JWT payload structure), (6) Duplicate email detection, (7) Password confirmation matching.
- [ ] Add integration tests for auth endpoints: signup happy path, duplicate email, weak password, login happy path, invalid credentials, account not verified, rate limiting – Status: missing – Est: 3.5h
  **Gap:** No e2e tests for auth endpoints. Need integration tests for: (1) POST /auth/signup success with email verification sent, (2) Duplicate email rejection, (3) Weak password rejection, (4) POST /auth/signin success with JWT returned, (5) Invalid credentials (wrong email, wrong password), (6) Account not verified error, (7) Account locked after failed attempts, (8) Email verification flow, (9) Resend verification, (10) Rate limiting triggers, (11) Remember me token expiry.

**Additional production-ready tasks identified:**
- [ ] Add password confirmation validation to SignUpDto – Status: missing – Est: 0.5h
  **Gap:** SignUpDto doesn't have confirmPassword field (signup.dto.ts). CustomerSignupDto has it (customer-signup.dto.ts:72-74). Need to add field and validation in service to check password === confirmPassword.
- [ ] Add email verification enforcement on login – Status: missing – Est: 0.5h
  **Gap:** signIn checks isActive but may not check isEmailVerified. Need to add check in auth.service.ts signIn method around line 141 and throw UnauthorizedException if email not verified with message "Please verify your email before logging in."
- [ ] Add verification token expiry – Status: missing – Est: 1.5h
  **Gap:** emailVerificationToken has no expiry. Tokens never expire. Need to: (1) Add emailVerificationTokenExpires field to User entity, (2) Set expiry (24h or 7d) when generating token, (3) Check expiry in verifyEmail method, (4) Clean up expired tokens periodically.
- [ ] Implement account lockout after failed login attempts – Status: missing – Est: 2.5h
  **Gap:** No failed login tracking. Need: (1) Add failedLoginAttempts: number and lockedUntil: Date to User entity, (2) Increment counter in validateUser on password mismatch, (3) Lock account (set lockedUntil = now + 15min) after 5 failed attempts, (4) Check lockedUntil in signIn, throw error if locked, (5) Reset counter on successful login, (6) Add unlock endpoint or auto-unlock on expiry.
- [ ] Add remember me functionality – Status: missing – Est: 2h
  **Gap:** SignInDto has no rememberMe field. Token expiry is fixed. Need to: (1) Add @IsOptional() @IsBoolean() rememberMe to SignInDto, (2) Update signIn signature to accept rememberMe, (3) Modify generateToken to accept expiry parameter, (4) Set 7d expiry if rememberMe=true, 24h otherwise, (5) Document token refresh strategy.
- [ ] Create comprehensive password strength validation – Status: missing – Est: 1h
  **Gap:** SignUpDto has weak validation. Need to update to match spec: (1) Change @MinLength(6) to @MinLength(8), (2) Add @Matches regex like CustomerSignupDto for uppercase, lowercase, number, (3) Optional: add special character requirement, (4) Consider using zxcvbn library for advanced strength checking.
- [ ] Add HTTPS enforcement for auth endpoints – Status: missing – Est: 1h
  **Gap:** No HTTPS enforcement in code (should be handled by infrastructure). For defense in depth: (1) Add middleware to check x-forwarded-proto header, (2) Redirect HTTP to HTTPS, (3) Set secure flag on cookies if using httpOnly cookies for tokens, (4) Document HTTPS requirement.
- [ ] Implement JWT refresh token mechanism (optional) – Status: missing – Est: 3h
  **Gap:** Current implementation uses single long-lived access token. For better security: (1) Create RefreshToken entity, (2) Generate refresh token on login (store in DB with expiry), (3) Return both access token (15min expiry) and refresh token (7d expiry), (4) Add POST /auth/refresh endpoint, (5) Rotate refresh tokens on use, (6) Add logout that deletes refresh tokens.

## DevOps / Infra

**Config / services**
- [ ] JWT secret keys for token signing
- [ ] Email service configuration for verification emails
- [ ] HTTPS enforcement for auth endpoints
- [ ] Monitoring/alerting for auth failures and security events
- [ ] Rate limiting configuration
- [ ] Database indexes for user lookups

**DevOps tasks**
- [ ] Configure JWT secret keys in secret manager (different for dev/staging/prod), set appropriate token expiry times – Status: partial – Est: 1h
  **Current:** JWT_SECRET and JWT_EXPIRES_IN configured in env (auth.module.ts:22, 24). **Gap:** Should use secret manager (AWS Secrets Manager, HashiCorp Vault) instead of .env in production. Need different secrets per environment. Document rotation process.
- [ ] Set up email service integration (SMTP or transactional email provider) for verification emails with templates – Status: done
  **Current:** Email service integrated with Resend/SMTP (email.service.ts) with sendEmailVerification method. Templates exist.
- [ ] Configure HTTPS enforcement: ensure all auth endpoints require HTTPS, redirect HTTP to HTTPS, set secure cookie flags – Status: missing – Est: 1.5h
  **Gap:** No HTTPS enforcement in code (relies on infrastructure). Need to: (1) Add middleware to check protocol, (2) Reject or redirect HTTP requests, (3) Set secure flag on cookies (if using), (4) Add HSTS header, (5) Document HTTPS requirement in deployment guide.
- [ ] Add database indexes on email column for fast user lookups during login, index on verification tokens if stored separately – Status: missing – Est: 1h
  **Gap:** Entity has unique constraint on email but no explicit index definition. With synchronize:true, basic indexes created but not optimized. Need migration to add: (1) B-tree index on email (case-insensitive if PostgreSQL), (2) Index on emailVerificationToken for verify-email lookups, (3) Composite index on (email, isActive) for login queries, (4) Index on lastLoginAt for analytics.
- [ ] Configure rate limiting: set up rate limit rules for signup (e.g., 5 per hour per IP), login (e.g., 5 failed attempts per 15 minutes), verification resend – Status: missing – Est: 2h
  **Gap:** No throttler configured. Need to: (1) Install @nestjs/throttler, (2) Configure global settings, (3) Apply specific limits per endpoint (signup: 5/hour, signin: 10/15min per IP + custom per email, resend: 3/hour), (4) Use Redis for distributed rate limiting in production, (5) Return clear 429 error messages.
- [ ] Set up monitoring dashboards for auth endpoints: signup success rate, login success rate, failed login attempts, email verification rate – Status: missing – Est: 2h
  **Gap:** No monitoring configured. Need APM integration: (1) Track signup success/failure rates, (2) Monitor login success rate and failed attempts, (3) Track email verification completion rate, (4) Alert on anomalies (spike in failed logins, low verification rate), (5) Dashboard for auth metrics (daily signups, active users, avg time to verify).
- [ ] Configure alerting for security events: alert on high failed login attempts (potential brute force), alert on unusual signup patterns, alert on auth endpoint errors – Status: missing – Est: 2h
  **Gap:** No alerting. Need alerts for: (1) >20 failed logins in 5min (brute force attack), (2) >10 signups from single IP in 1hour (bot/fraud), (3) Auth endpoint error rate >5%, (4) JWT validation failures >10/min (token tampering), (5) Account lockouts >5/hour, (6) Email send failures >10%.
- [ ] Configure log aggregation for auth events: log all signup attempts, login attempts (success/failure), email verifications, security events for audit trail – Status: missing – Est: 1.5h
  **Gap:** Only console.log statements. Need structured logging: (1) Configure Winston or Pino, (2) Log to stdout in JSON format, (3) Ship logs to aggregation service (CloudWatch, DataDog, ELK), (4) Create log parsing rules, (5) Set up search queries for security investigations, (6) Retain auth logs for compliance (90 days minimum).
- [ ] Document auth flow, token management, email verification process, and security measures for future reference – Status: missing – Est: 1.5h
  **Gap:** No documentation. Need runbook covering: (1) Signup flow diagram (multi-step form → email verification), (2) Login flow with remember me option, (3) JWT token structure and expiry, (4) Email verification process and token expiry, (5) Rate limiting policies, (6) Account lockout logic, (7) Security best practices, (8) Troubleshooting guide (locked accounts, email not received, token expired).

## Definition of Done

**Functional**
- [ ] Customer can complete signup flow: Step 1 (email, password, confirm password), Step 2 (password validation with tooltip), submit successfully, receive email confirmation screen.
- [ ] Password strength validation works: tooltip shows requirements, real-time indicators update, submission blocked if requirements not met.
- [ ] Email verification flow works: verification email sent after signup, customer can verify email (if required), account activated after verification.
- [ ] Customer can log in successfully: enter email/password, toggle "Remember me", click "Sign In", receive JWT token, redirect to dashboard.
- [ ] Invalid credentials handled safely: incorrect email/password shows error, account not verified shows appropriate message, rate limiting prevents brute force.
- [ ] Session/token management works: JWT token stored securely, "Remember me" extends token expiry, token refresh works (if implemented), logout invalidates token.

**UX**
- [ ] Signup screens (Step 1 and Step 2) match Figma: layout, spacing, typography, progress bar, form fields, buttons.
- [ ] Password strength tooltip matches Figma: appears on focus/input, shows requirements with checkmarks, updates in real-time.
- [ ] Email confirmation screen matches Figma: title, subtitle, instructions, support info, button styling.
- [ ] Login screen matches Figma: layout, form fields, "Remember me" checkbox, "Forgot Password" link, "Sign In" button.
- [ ] Loading states: buttons show spinners, forms disabled during submission, no navigation during auth.
- [ ] Error messages: clear, non-leaky (don't reveal if email exists), actionable, displayed inline or as toasts.
- [ ] Responsive behavior works for desktop and tablet breakpoints shown in Figma.

**QA**
- [ ] Happy path signup: Complete Step 1, proceed to Step 2, meet password requirements, submit successfully, see email confirmation.
- [ ] Happy path login: Enter valid credentials, click "Sign In", receive token, redirect to dashboard.
- [ ] Password validation: Test weak passwords, missing requirements, password mismatch, tooltip updates correctly.
- [ ] Invalid credentials: Test incorrect email, incorrect password, non-existent account, unverified account.
- [ ] Duplicate signup: Attempt to sign up with existing email, see appropriate error message.
- [ ] Rate limiting: Test multiple failed login attempts, verify rate limiting triggers, verify lockout behavior.
- [ ] Session management: Test "Remember me" option, verify extended token expiry, test token refresh, test logout.
- [ ] Email verification: Test verification flow (if required), test resend verification, test expired tokens.
- [ ] Error handling: Network failures, server errors, timeout scenarios all handled gracefully with retry options.

## Estimate

- Frontend: ~35h (L)
- Backend: ~44h (XL) - Updated from 35h due to missing remember me functionality, rate limiting, account lockout, audit logging, token expiry, comprehensive testing, and production security features
- DevOps: ~14h (M)

## Summary of Backend Gap Analysis

### Current State

The backend has **good auth infrastructure** with core signup/login functionality implemented:
- ✅ POST `/auth/signup` endpoint with email verification (auth.controller.ts:38)
- ✅ POST `/auth/signin` endpoint with JWT tokens (auth.controller.ts:71)
- ✅ POST `/auth/verify-email` endpoint (auth.controller.ts:120)
- ✅ User entity with all required fields (user.entity.ts)
- ✅ Password hashing via bcrypt with 12 salt rounds (user.entity.ts:117-123)
- ✅ Email verification system (auth.service.ts:55-63)
- ✅ JWT auth middleware/strategy (jwt.strategy.ts)
- ✅ Duplicate email checking (auth.service.ts:33-40)
- ✅ Last login tracking (auth.service.ts:147)

### Critical Gaps

**1. Weak Password Validation on Signup (HIGH PRIORITY)**
- ❌ SignUpDto requires only MinLength(6) - too weak
- ❌ Spec requires: 8 chars + uppercase + lowercase + number
- ❌ No confirmPassword field in SignUpDto
- **Impact:** Weak passwords allowed, violates security requirements

**2. Missing "Remember Me" Functionality (MEDIUM PRIORITY)**
- ❌ SignInDto has no rememberMe field
- ❌ JWT expiry is fixed (24h), no extended expiry option
- **Impact:** Cannot provide different session lengths per spec

**3. No Rate Limiting (HIGH PRIORITY - Security)**
- ❌ No @nestjs/throttler configured (same gap as all stories)
- ❌ No brute force protection on login
- ❌ No signup spam protection
- **Impact:** Vulnerable to brute force attacks and abuse

**4. No Account Lockout After Failed Logins (HIGH PRIORITY - Security)**
- ❌ No failed login attempt tracking
- ❌ No account lockout mechanism
- ❌ Spec requires tracking for security monitoring
- **Impact:** Brute force attacks not prevented

**5. Missing Endpoints**
- ❌ No POST `/auth/logout` endpoint (optional but requested)
- ❌ No POST `/auth/resend-verification` endpoint
- **Impact:** Incomplete user experience (can't resend verification email)

**6. Email Verification Not Enforced on Login (MEDIUM PRIORITY)**
- ❌ signIn checks isActive but may not enforce isEmailVerified
- ❌ Spec mentions "account not verified" error state
- **Impact:** Users can login without verifying email

**7. No Verification Token Expiry (MEDIUM PRIORITY)**
- ❌ emailVerificationToken has no expiry field
- ❌ Tokens never expire
- **Impact:** Old tokens remain valid indefinitely (security risk)

**8. Missing Production Requirements**
- ❌ No comprehensive audit logging (only console.log)
- ❌ No structured security event logging
- ❌ No monitoring/alerting for auth failures
- ❌ Minimal test coverage (trivial placeholders only)
- ❌ No migrations (using synchronize:true)
- ❌ No database indexes optimization
- ❌ JWT secret in .env (should use secret manager)
- ❌ No HTTPS enforcement in code

**9. Password Strength Inconsistency**
- SignUpDto: MinLength(6) - weak
- CustomerSignupDto: MinLength(8) + complexity regex - strong
- **Impact:** Inconsistent security standards across endpoints

### Security Concerns

1. **Brute Force Vulnerability:** No rate limiting or account lockout
2. **Weak Password Policy:** SignUpDto allows "pass12" (6 chars)
3. **Token Security:** No expiry on verification tokens
4. **Missing Audit Trail:** Only console.log, no structured logging for security investigations
5. **No Login Monitoring:** Cannot detect or alert on suspicious login patterns

### Revised Effort Estimate

**Original estimate:** 35h
**Updated estimate:** 44h (+9h)

**Breakdown:**
- Password validation fixes: ~2.5h
- Remember me functionality: ~2h
- Rate limiting implementation: ~2.5h
- Account lockout mechanism: ~2.5h
- Email verification enforcement: ~0.5h
- Token expiry system: ~1.5h
- Resend verification endpoint: ~2h
- Logout endpoint: ~1.5h
- Audit logging: ~2.5h
- Comprehensive testing: ~6.5h
- Migrations + indexes: ~2h
- Documentation: ~1.5h
- DevOps (monitoring, alerting, configs): ~7.5h (partial - done: 2h, missing: 12h)

### Recommendation

The backend has **good foundation** but needs **security hardening** and **spec alignment**:

**Priority 1 (Security Blockers):**
1. Implement rate limiting (prevent brute force)
2. Add account lockout after failed attempts
3. Strengthen password validation on signup
4. Add audit logging for security events

**Priority 2 (Spec Requirements):**
5. Add remember me functionality
6. Enforce email verification on login
7. Add password confirmation to signup
8. Create resend verification endpoint

**Priority 3 (Production-ready):**
9. Add verification token expiry
10. Implement logout endpoint
11. Comprehensive testing
12. Monitoring and alerting
13. Migrations instead of synchronize:true

**Quick Wins (Low Effort, High Impact):**
- Update SignUpDto password validation: 0.5h
- Add confirmPassword field: 0.5h
- Enforce email verification: 0.5h
- Add logout endpoint (client-side only): 1h

The core authentication flow is solid (signup → email verification → login → JWT). The main gaps are around **security hardening** (rate limiting, lockout), **spec alignment** (password strength, remember me), and **production readiness** (logging, monitoring, testing). **Estimate 44h to achieve production-ready auth** with all security features and comprehensive testing.
