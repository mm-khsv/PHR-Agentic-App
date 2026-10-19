# PHR Agentic Web Application — Project Overview

## 1. Project Purpose

The project aims to build a Personal Health Record (PHR) web application that enables users to manage their personal medical information and supports controlled access to a limited set of emergency-critical information when needed.

The first release is intended to be an MVP usable by real users. Because the application handles sensitive medical information, privacy, security, data integrity, and appropriate human oversight are essential requirements.

## 2. Initial Product Scope

The first release is planned as a web application, with the possibility of extending it to mobile platforms in the future.

The initial scope should be limited to the capabilities necessary for a useful, secure, and testable first release.

Potential capabilities include:

- User registration, authentication, and account management.
- Personal medical profile management.
- Recording blood type, allergies and sensitivities, medical conditions, medications, relevant medical history, implants or medical devices, and emergency contacts.
- Recording the source of medical information, its verification status, and relevant timestamps.
- Allowing users to review and update their own information under appropriate access controls.
- Providing a limited emergency-information view.
- Applying controlled access to information that should not be publicly visible.
- Recording relevant access and security events in audit logs.

These capabilities are candidates for the initial scope. Their priorities, detailed behavior, and acceptance criteria must be established during requirements analysis.

## 3. Emergency Access Model

The intended approach combines a limited emergency view with controlled access to more sensitive information.

The exact authorization model, information exposed in the emergency view, and any QR-code or other access mechanism remain open decisions.

Possession of a QR code or link must not automatically be treated as proof of authorization to access a complete medical record.

Emergency access behavior must be designed and tested before the application is used for real-world emergency scenarios.

## 4. Medical Data Integrity

The application must preserve the source and verification status of medical information.

Patient-reported information must not be presented as physician-verified or document-verified information without appropriate supporting evidence.

The application must not independently diagnose medical conditions, invent medical information, or silently change user-provided medical facts.

The detailed verification process and supported evidence types remain to be defined.

## 5. Security and Privacy

Security and privacy must be considered throughout requirements analysis, system design, implementation, testing, and deployment.

The project should address:

- Authentication and least-privilege authorization.
- Protection of sensitive medical information.
- Secure handling of secrets and application configuration.
- Input validation and appropriate error handling.
- Controlled emergency access and revocation where applicable.
- Audit logging with minimized exposure of medical information.
- Data retention, account deletion, backup, and recovery.
- Use of synthetic medical data during development and testing by default.
- Security testing and appropriate human review before operational use.

The specific controls and applicable legal or regulatory requirements must be established before release.

## 6. Agent Lifecycle

The project uses five distinct lifecycle agents:

1. Requirements Engineer
2. System Designer
3. Implementation Engineer
4. QA Engineer
5. Deployment Engineer

A coordinator manages task assignment, deliverable review, handoffs, project status, and approval gates. Initially, coordination may be manual.

Agent definitions do not by themselves guarantee autonomous execution or technical enforcement of approval gates.

## 7. Initial Release Constraints

- The first release should remain focused on an MVP rather than attempting to implement every possible feature.
- Requirements must be documented and reviewed before system design is finalized.
- Design decisions must be reviewed before implementation of the corresponding scope.
- Testing evidence and appropriate approvals are required before consequential release actions.
- Real medical information must not be used in development or testing unless a separately approved process explicitly permits it.
- Production readiness, clinical safety, and legal compliance must not be assumed merely because the application runs or its automated tests pass.

## 8. Open Questions

The following decisions require further analysis:

- Which user roles will exist, and what may each role access?
- What exact information will be available in the limited emergency view?
- Will the emergency view use QR codes, authenticated access, or another mechanism?
- How will emergency access be authorized, restricted, audited, and revoked?
- Which medical information requires verification, and who may verify it?
- What are the data retention and account deletion rules?
- Which jurisdiction's legal and regulatory requirements apply?
- What minimum security, backup, recovery, and incident-response measures are required?
- What evidence and human approvals are necessary before real users can rely on the application in an emergency?

## 9. Next Step

The Requirements Engineer should analyze the project context, identify stakeholders and use cases, prioritize candidate MVP capabilities, define testable requirements and acceptance criteria, document risks and assumptions, and maintain a list of unresolved decisions.

The requirements baseline must be reviewed and approved by the authorized project decision-maker before system design is finalized.
