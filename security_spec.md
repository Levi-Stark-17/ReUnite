# API & MySQL Security Specification

## Core security rules
- Public users do not need permanent accounts.
- Lost reports require successful OTP verification before database creation.
- Found reports do not require OTP.
- Admin portal and every sensitive admin API require authenticated JWT access.
- Authorization is enforced server-side; hiding a frontend button is never a security control.
- Public APIs return sanitized item/report data and never expose protected reporter contact information or claim evidence.

## Database security
- Use SQLAlchemy/parameterized queries to prevent SQL injection.
- Enforce foreign keys and controlled status transitions in backend business logic.
- Store passwords using bcrypt/Argon2-compatible password hashing; never plaintext.
- Store OTPs as secure hashes and expire them quickly.
- Never return OTP values to the browser in production.
- Rate-limit login, OTP verification and resend operations in production.
- Validate and size-limit uploaded files.
- Audit important administrative decisions.

## Required workflows
- Pending Approval → Approved before public visibility.
- Lost-only OTP verification.
- Match records created/reviewed by trusted backend/admin operations.
- Claims require ownership evidence and admin decision.
- Handover is available only when eligible.
- Unclaimed Found → Open for Collection → Collection Request → Collected → Closed.
- Collection continues the original Found case; it does not create a new Lost/Found tracking code.
