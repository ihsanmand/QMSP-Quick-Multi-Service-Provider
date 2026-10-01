# Public Architecture Overview

This document provides a deliberately high-level view of QMSP - Quick Multi Service Provider. It is intended to demonstrate engineering judgment without disclosing implementation details that would weaken security, privacy, or commercial confidentiality.

## Client Surfaces

### Next.js Web

The web application provides role-specific customer, provider, and administrative experiences. Sensitive browser operations pass through same-origin server boundaries where appropriate, and private workflow data is treated as non-cacheable.

### Flutter Android

The Android application provides customer and provider flows using typed API models, secure authentication storage, backend-authoritative permissions, and explicit online-only handling for sensitive mutations.

## Application Boundary

The Django platform owns:

- Authentication and account-state enforcement
- Marketplace request and offer rules
- Customer-controlled offer acceptance
- Booking creation and lifecycle transitions
- OTP-controlled service authorization
- Direct-request privacy
- Validation and transaction integrity
- Audit and notification boundaries
- Authorized journey-tracking decisions

Clients improve usability, but they do not replace server authorization.

## Data and Coordination

PostgreSQL provides transactional persistence. Redis supports coordination and real-time capabilities where required. Precise location, private verification evidence, credentials, and security-sensitive metadata are restricted to their authorized contexts.

## Key Domain Invariant

```text
Request -> Provider offer -> Customer acceptance -> Booking
```

Neither provider selection nor provider action creates a booking without customer acceptance.

## Privacy Boundary

The public case study excludes:

- Internal route and serializer contracts
- Database tables, fields, constraints, and migrations
- Exact authorization and anti-abuse rules
- Tracking thresholds or retention implementation
- Audit schemas and operational logs
- Environment variables, infrastructure addresses, and credentials
- Production data and private media

## Why the Source Is Private

QMSP combines marketplace workflow design with security, identity, tracking, and deployment concerns. Publishing the complete implementation would reveal commercially sensitive behavior and security-relevant details. Public documentation therefore focuses on architecture, trade-offs, validation principles, and non-sensitive evidence.
