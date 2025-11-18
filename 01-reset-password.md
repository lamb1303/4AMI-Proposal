# Story 1: Reset Password

## Context

**Figma URL:**
https://www.figma.com/design/JDoPGdZ6anmqLy7YFI9sXp/4ami-Dashboard?node-id=2151-5786

**Story goal (from PRD + Figma)**
Give any authenticated user who forgets their password a reliable, self-serve path to request a reset code, verify it, set a new password that meets security rules, and confirm success so they can log back in without contacting support.

## UX / Product

**Main user flows (from Figma)**
- [x] Step 1 – `Forgot Password` screen: email input, helper text, CTA to send verification code, link back to login.
- [x] Step 2 – `Verification Code` (6-digit OTP) screen: segmented inputs, timer + resend link, inline feedback for invalid/expired codes.
- [x] Step 3 – `Reset Password` form: new password + confirm fields with eye toggle, strength meter, requirement helper text.
- [x] Step 4 – `Password Updated Successfully` confirmation screen with success icon and CTA to return to login/dashboard.

**States to support**
- [x] Loading states – disable buttons + show inline spinner while sending code, verifying OTP, and saving new password.
- [x] Error states – invalid email, throttled requests, incorrect/expired OTP, password policy failures, backend/network errors.
- [x] Empty / edge states – blank form validation, user revisiting link after success, OTP resend lockout, expired link guidance.
- [x] Success confirmation – success banner + redirect guidance after password update and after requesting new code (toast/inline).

## Frontend

**Screens / components**
- [ ] `ForgotPasswordRequestView` (email form + illustration) – Status: Not Started
- [ ] `VerifyResetCodeView` (OTP inputs + timer) – Status: Not Started
- [ ] `ResetPasswordForm` (new + confirm password with strength meter) – Status: Not Started
- [ ] `PasswordResetSuccess` (confirmation banner + CTA) – Status: Not Started

**Frontend tasks**
- [ ] Scaffold `/forgot-password` route + shell layout matching Figma navigation panel – Status: Not Started – Est: 2h
- [ ] Build email input form with validation, helper text, disabled/responsive CTA – Status: Not Started – Est: 2h
- [ ] Wire `Send code` mutation + inline loading/error feedback + toast confirmation – Status: Not Started – Est: 2.5h
- [ ] Implement reusable 6-field OTP input component with auto-focus, paste support, and timer/resend UI – Status: Not Started – Est: 3h
- [ ] Hook OTP verification state machine (success path -> reset form, errors show inline messaging) – Status: Not Started – Est: 2.5h
- [ ] Build reset password form with password + confirm inputs, strength meter, policy checklist, show/hide toggles – Status: Not Started – Est: 3h
- [ ] Implement submission handling, disabling state, API integration, and success transition to confirmation view – Status: Not Started – Est: 2.5h
- [ ] Create success screen (icon, copy, CTA back to login) and route guard to prevent direct access – Status: Not Started – Est: 1.5h
- [ ] Add analytics & accessibility polish (focus management, aria-live for errors, keyboard flows) – Status: Not Started – Est: 2h

## Backend

**APIs / endpoints**
- [ ] POST `/auth/password-reset-request` – send OTP + throttle – Status: partial – Est: 3h
  **Current:** POST `/auth/forgot-password` sends token link, not OTP. Needs refactor for 6-digit OTP generation, rate limiting, and different response format.
- [ ] POST `/auth/password-reset-verify` – validate OTP/token and issue short-lived reset token – Status: missing – Est: 3h
  **Gap:** No verification endpoint exists. Current flow is single-step (token in URL). Need new endpoint to verify OTP and return short-lived JWT/token.
- [ ] POST `/auth/password-reset-confirm` – update password with new credential – Status: partial – Est: 2.5h
  **Current:** POST `/auth/reset-password` updates password but uses long-lived token from email, not short-lived token from OTP verification. Needs session invalidation logic.

**Backend tasks**
- [ ] Model reset requests table (user_id, hashed OTP, expiry, attempt counters) + migration – Status: missing – Est: 2.5h
  **Gap:** Currently uses `passwordResetToken` and `passwordResetExpires` columns on User table. No dedicated table for tracking attempts, no attempt counters. Need separate `password_reset_requests` table with fields: id, user_id, hashed_otp, otp_expires_at, attempts, created_at, verified_at.
- [ ] Implement POST `/auth/password-reset-request` (lookup user, rate limit, generate OTP + signed token, persist) – Status: partial – Est: 4h
  **Current:** `requestPasswordReset` method exists (auth.service.ts:284) but generates UUID token, not 6-digit OTP. Missing: rate limiting (@nestjs/throttler), OTP generation (crypto.randomInt), attempt tracking, proper error responses. Email template exists but needs OTP format update.
- [ ] Integrate transactional email template + provider client for reset OTP delivery – Status: done
  **Current:** Email service fully implemented with Bull queue, Resend/SMTP providers, and password reset template (email.processor.ts:111-154). Only needs template update for OTP format.
- [ ] Implement OTP verification endpoint (validate code, check expiry/attempts, issue short-lived JWT or signed token) – Status: missing – Est: 3.5h
  **Gap:** No `/auth/password-reset-verify` endpoint. Need new controller method and service logic to: validate OTP, check expiry (5-10 min), track attempts (max 3-5), issue short-lived token (5-15 min), return appropriate error codes for invalid/expired/max-attempts.
- [ ] Implement password update endpoint (validate token, enforce password policy, salt+hash new password, invalidate sessions) – Status: partial – Est: 3h
  **Current:** `resetPassword` method exists (auth.service.ts:312) with basic token validation and password update. Missing: password policy validation (length, complexity, common passwords), session invalidation logic, proper error handling. Password hashing is handled by User entity BeforeInsert/Update hooks.
- [ ] Add audit/event logging for reset requests, successes, failures for monitoring/security – Status: missing – Est: 2.5h
  **Gap:** Only console.log statements exist. Need structured logging with: event type, user_id, IP address, user agent, timestamp, success/failure reason. Consider Winston/Pino logger with log levels and log aggregation service integration.
- [ ] Unit/integration tests covering happy path, invalid email, brute-force lockout, expired token – Status: missing – Est: 3h
  **Current:** auth.spec.ts has only trivial placeholder tests. Need comprehensive test suite for: request OTP, verify OTP (valid/invalid/expired/max attempts), reset password (valid/invalid token, weak password), rate limiting, concurrent requests.

**Additional production-ready tasks identified:**
- [ ] Implement rate limiting middleware for password reset endpoints – Status: missing – Est: 2h
  **Gap:** No @nestjs/throttler found in codebase. Need to install and configure with sensible limits (e.g., 3 requests per 15min per IP, 5 requests per hour per email). Add to app.module.ts and apply @Throttle decorator to reset endpoints.
- [ ] Add password policy validation service – Status: missing – Est: 2h
  **Gap:** No password strength validation. Need service to enforce: min 8 chars, uppercase, lowercase, number, special char, check against common passwords list (e.g., zxcvbn library), reject passwords containing email/name.
- [ ] Implement cleanup job for expired reset tokens/OTPs – Status: missing – Est: 1.5h
  **Gap:** No cleanup mechanism. Add Bull cron job or TypeORM @Index with TTL to clean up expired records (>24h old) from reset_requests table daily.
- [ ] Add monitoring/alerting for suspicious activity – Status: missing – Est: 2h
  **Gap:** No monitoring beyond console logs. Need metrics for: reset request rate spikes, failed verification attempts, successful resets. Consider integration with monitoring service (DataDog, New Relic, CloudWatch).

## DevOps / Infra

**Config / services**
- [ ] Email provider
- [ ] Secrets / env vars
- [ ] Monitoring / logging

**DevOps tasks**
- [ ] Configure transactional email provider (API keys per env, sandbox sender) – Status: done
  **Current:** Resend and SMTP providers configured with environment variables (RESEND_API_KEY, MAIL_HOST, MAIL_USER, MAIL_PASS, MAIL_FROM). Factory pattern supports multiple providers.
- [ ] Manage secrets (`EMAIL_API_KEY`, OTP signing secret, password policy config) in secret manager – Status: partial – Est: 1.5h
  **Current:** .env files used. Production should use AWS Secrets Manager, HashiCorp Vault, or similar. Need OTP_SECRET for HMAC signing, PASSWORD_RESET_TOKEN_SECRET separate from JWT_SECRET.
- [ ] Add CI/CD env vars + rotation playbook for reset secrets – Status: missing – Est: 1.5h
  **Gap:** No documented secret rotation process. Need playbook for rotating OTP_SECRET, JWT_SECRET without breaking active reset flows. Consider dual-key validation during rotation window.
- [ ] Set up alerting/metrics for reset failures, rate-limit breaches, and email provider errors – Status: missing – Est: 2h
  **Gap:** No alerting configured. Need alerts for: >10 failed verifications in 5min (brute force), email send failures >5%, rate limit triggers >20/hour, password reset success rate <80%.
- [ ] Schedule job or TTL index cleanup for expired reset tokens/OTPs – Status: missing – Est: 1.5h
  **Gap:** No cleanup job. Need Bull cron job (@nestjs/bull) or PostgreSQL TTL extension to delete expired records. Run daily at off-peak hours with batch size limit to avoid DB load.

## Definition of Done

**Functional**
- [ ] Users can request a reset code with valid email and receive instructions via email.
- [ ] Users can submit the received OTP, pass validation, and set a new password that immediately works for login.
- [ ] Requests are rate-limited, tokens expire as designed, and audit logs capture attempts.

**UX**
- [ ] Matches Figma for key screens and states
- [ ] Error states visible and understandable
- [ ] Responsive behavior verified for desktop + tablet breakpoints shown in Figma.
- [ ] Accessibility: focus order, keyboard-only navigation, readable status messaging.

**QA**
- [ ] Happy path tested
- [ ] Invalid token tested
- [ ] Expired token tested
- [ ] Weak password + mismatch handling tested
- [ ] Multiple rapid requests trigger throttling and expose proper messaging.

## Estimate

- Frontend: ~20h (M)
- Backend: ~32h (L) - Updated from 18h due to OTP implementation gap, rate limiting, password policy, tests, and additional production requirements
- DevOps: ~8h (S)

## Summary of Backend Gap Analysis

  Current State

  The backend has a basic password reset implementation using a token-based approach:
  - ✅ Email infrastructure (Bull queue, Resend/SMTP providers)
  - ✅ Basic endpoints (/auth/forgot-password, /auth/reset-password)
  - ✅ Database fields for reset tokens in User table
  - ✅ Password hashing via bcrypt

### Critical Gaps

  **1. Architecture Mismatch (HIGH IMPACT)**
  - Spec requires: 3-step OTP flow (request → verify OTP → reset password)
  - Current implementation: 2-step token link flow (request → reset with URL token)
  - Impact: Entire flow needs refactoring to match Figma design with 6-digit OTP

  **2. Missing Security Features (HIGH PRIORITY)**
  - ❌ No rate limiting (no @nestjs/throttler found)
  - ❌ No password policy validation (strength, complexity)
  - ❌ No attempt tracking or brute-force protection
  - ❌ No session invalidation after password reset
  - ❌ No dedicated reset_requests table with attempt counters

  **3. Missing Verification Endpoint (BLOCKER)**
  - ❌ No /auth/password-reset-verify endpoint for OTP validation
  - Current flow goes directly from email to password reset (single-step)

  **4. Production Readiness Gaps**
  - ❌ No audit logging (only console.log statements)
  - ❌ No monitoring/alerting for suspicious activity
  - ❌ No automated cleanup of expired tokens
  - ❌ Minimal test coverage (auth.spec.ts has placeholder tests only)

### Revised Effort Estimate

  Original estimate: 18h
  Updated estimate: 32h (+14h)

  **Breakdown:**
  - Refactor to OTP flow: ~10.5h
  - Security features (rate limiting, password policy): ~4h
  - Audit logging & monitoring: ~4.5h
  - Comprehensive testing: ~3h
  - Additional production tasks: ~5.5h
  - DevOps (partial tasks): ~4.5h

  **Recommendation**

  The backend needs significant refactoring to match the spec. The current token-link approach is simpler but doesn't align with the Figma design
  requiring OTP verification. Consider whether to:
  1. Refactor to match spec (32h) for better UX and security
  2. Simplify spec to match current implementation (save ~14h but compromise on design)

  The production-ready features (rate limiting, password policy, audit logging, tests) are essential and should not be skipped.
