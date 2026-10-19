# PHR Project-Specific Agent Rules

These rules apply only to the PHR application. They supplement the reusable agent definitions and must not be applied by default to unrelated projects.
## Agent: requirements-engineer

## 4. PHR-Specific Responsibilities

Consider requirements for:

- Personal identity and emergency contacts.
- Blood type.
- Allergies and medication sensitivities.
- Medical conditions and relevant medical history.
- Current medications.
- Implants, medical devices, and surgeries.
- Source and timestamp of medical information.
- Verification status and verification history.
- Emergency access permissions and access auditing.
- Privacy, data retention, correction, and deletion.
- Availability and safe behavior during service failures.

Requirements must distinguish patient-reported information from information verified by an appropriate professional or supporting document.

Unknown, not recorded, absent, expired, conflicting, incomplete, and rejected information must not be treated as interchangeable states when that distinction matters.

The application must not invent medical facts, diagnose users, or present unverified information as professionally verified.

A QR code or public identifier must not, by itself, be considered proof of identity or authorization.

Use synthetic data for development and testing by default. Never request real patient records merely to clarify a requirement.

Clinical, legal, regulatory, and professional-verification policies must be identified as decisions requiring appropriate human expertise.

## Agent: system-designer

## 4. PHR-Specific Design Requirements

### 4.1 Medical Information and Provenance

The design must support approved requirements for:

- Personal identity and medical profile information.
- Allergies and sensitivities.
- Medical conditions and relevant history.
- Medications.
- Blood type, when supplied and appropriately verified.
- Implants and medical devices.
- Surgeries and procedures.
- Emergency contacts.
- Source and provenance of medical information.
- Verification status, verification timestamp, and verifier where applicable.
- Expired, rejected, or otherwise outdated information when required by the approved requirements.

Keep patient-reported information distinguishable from physician-verified or document-verified information. Never design a flow that silently treats unverified information as verified.

Do not invent medical facts or make the application diagnose, prescribe, or independently determine clinical truth.

### 4.2 Emergency Access

Design emergency access according to explicitly approved requirements and a documented threat model.

Consider:

- Who may access emergency information and under which conditions.
- How access is authenticated or otherwise controlled.
- What minimum information is exposed.
- How access is logged and reviewed.
- Abuse, impersonation, and unauthorized disclosure risks.
- Failure and recovery behavior.

A QR code or public link must not automatically be treated as proof of identity or authorization. Document the risks and require explicit approval for the chosen access model.

### 4.3 Privacy and Security

Apply least privilege and data minimization.

Identify:

- Sensitive fields and their access rules.
- Trust boundaries and entry points.
- Authentication and authorization checks.
- Encryption requirements.
- Secure session and secret handling.
- Input validation and error handling.
- Audit-log content and sensitive-data exclusions.
- Retention and deletion requirements.
- Backup and recovery considerations.
- Threats arising from external services or integrations.

Do not claim a design is legally or clinically compliant without appropriate evidence and review.

### 4.4 Safe Development and Testing

Assume synthetic data is the default for development, testing, and demonstrations.

Do not require real patient data to validate ordinary application workflows. Identify any exceptional need for real data and escalate it for explicit privacy and security review before use.

## Agent: implementation-engineer

## 4. PHR-Specific Implementation Rules

### 4.1 Medical Data Integrity

- Do not invent, infer, or silently fill in missing medical information.
- Preserve the distinction between patient-reported and verified information.
- Preserve required source, verification status, timestamps, and verifier metadata.
- Validate medical data according to approved requirements; do not treat validation as proof of clinical truth.
- Do not implement diagnosis, treatment recommendations, or medication decisions unless explicitly approved and appropriately reviewed as a separate scope.
- Do not silently overwrite or discard existing medical history where the approved design requires history or auditability.

### 4.2 Authentication and Authorization

- Enforce authorization on the server side for protected data and operations.
- Do not rely solely on hidden buttons, client-side checks, QR codes, or possession of a URL to protect sensitive information.
- Follow least privilege and the approved access model.
- Prevent users from accessing another person's medical records without explicit authorization.
- Apply the approved emergency-access rules and logging requirements.
- If the required authorization behavior is unclear, request clarification rather than choosing a weaker control.

### 4.3 Privacy and Security

- Use synthetic data for development and testing by default.
- Do not copy real patient data into test fixtures, logs, screenshots, or demonstrations.
- Never hardcode API keys, passwords, tokens, private keys, or production credentials.
- Use the project's approved secret-management and configuration approach.
- Avoid logging medical details, credentials, session tokens, or other unnecessary sensitive values.
- Apply appropriate input validation, output encoding, safe error handling, and protections against the threats identified in the design.
- Do not disable security checks merely to make a test pass.
- Treat external API responses and user-supplied content as untrusted input.

### 4.4 Database and Data Changes

- Follow the approved data model and migration strategy.
- Make schema changes explicit and reviewable.
- Consider data integrity, access permissions, rollback, and migration safety.
- Never run destructive commands against production data without explicit authorization and a verified recovery plan.
- Do not use real personal medical information to seed a development database.

## Agent: qa-engineer

## 4. PHR-Specific QA Requirements

### 4.1 Medical Information Integrity

Where supported by approved requirements, verify that:

- Medical fields accept and display the expected data.
- Required source and provenance information is preserved.
- Patient-reported information remains distinguishable from verified information.
- Verification status and timestamps are handled correctly.
- Missing or invalid information is not silently fabricated.
- Updates do not unintentionally erase information that should be retained.
- Outdated or rejected information is handled according to the approved rules.

QA must not judge the clinical correctness of a diagnosis or treatment. Clinical validation, where required, must be handled by an appropriately qualified reviewer.

### 4.2 Authentication and Authorization

Test access rules for relevant user roles and scenarios.

Where applicable, verify that:

- Unauthenticated users cannot access protected medical information.
- Users cannot access another person's records without authorization.
- Server-side authorization is enforced for protected operations.
- Changing a URL, identifier, request payload, or client-side state does not bypass access controls.
- Emergency access follows the approved rules.
- Unauthorized and emergency-access events are audited as required.
- Failure responses do not expose sensitive information.

Do not assume that a QR code, hidden interface element, or hard-to-guess URL is an adequate security control.

### 4.3 Privacy and Security

Within the approved test scope, examine:

- Sensitive information in application responses and error messages.
- Accidental disclosure through logs.
- Authentication and session handling.
- Input validation and unsafe data handling.
- Permission checks at relevant trust boundaries.
- Secret exposure in code, configuration, and test output.
- Dependency or configuration risks that are observable with available checks.
- Audit-log completeness without unnecessary medical details.
- Data retention and deletion behavior where implemented.

Do not claim a complete security assessment from a limited test suite. Clearly state the scope and limitations.

### 4.4 Safe Test Data and Environment

- Use synthetic test records by default.
- Do not copy real patient records into test cases, screenshots, logs, or reports.
- Confirm the target environment before executing potentially destructive tests.
- Do not run destructive tests against production.
- Do not modify production data, accounts, permissions, or infrastructure.
- Stop and request approval if safe testing requires an action outside the authorized scope.

## Agent: deployment-engineer

## 4. PHR-Specific Deployment Requirements

### 4.1 Protection of Medical Data

Before a release is considered ready, verify that the release plan addresses:

- Secure transport for sensitive data.
- Appropriate protection of stored data.
- Authentication and authorization configuration.
- Secret and credential management.
- Access logging and avoidance of unnecessary medical details in logs.
- Backup protection and recovery procedures.
- Data retention and deletion requirements where applicable.
- Separation between development, testing, and production environments.
- Secure handling of exports, temporary files, and diagnostic output where applicable.

These checks must be supported by evidence. Do not claim that an application is secure simply because a checklist exists.

### 4.2 Environment and Configuration

- Keep development, test, staging, and production configuration separate.
- Do not commit production credentials, private keys, API keys, passwords, or tokens.
- Use synthetic data outside production by default.
- Never copy production medical records into development or test environments without a separately approved and justified process.
- Document required environment variables without recording their secret values.
- Validate required configuration before release.
- Ensure debug features and verbose error output are disabled in production where appropriate.
- Document external services and their security and availability dependencies.

### 4.3 Database Migrations and Recovery

- Identify database schema changes and their compatibility requirements.
- Document pre-release backup requirements where applicable.
- Describe migration order and validation steps.
- Identify whether each migration is reversible and explain limitations.
- Avoid destructive data operations without explicit authorization and a verified recovery plan.
- Do not assume restoring a database backup alone is sufficient to recover the entire application.
- Consider the consistency of application code, database state, uploaded files, and external services during rollback.

### 4.4 Emergency Access and Auditability

Where these features are in scope, verify that deployment documentation covers:

- Correct configuration of emergency-access rules.
- Protection of authentication and authorization controls.
- Availability and integrity of required audit records.
- Monitoring and escalation for access-control failures.
- Safe behavior when an external dependency is unavailable.
- Recovery and incident procedures for suspected unauthorized access.

A QR code or public endpoint must not be treated as a substitute for the approved authorization model.

