# Agent Architecture — PHR Agentic Web Application

## 1. Purpose

This document defines the architecture, responsibilities, and coordination workflow of the five lifecycle agents responsible for developing the Personal Health Record (PHR) application.

The application focuses on managing personal medical information and supporting access to emergency-critical medical information while maintaining data integrity, privacy, security, and appropriate human oversight.

The architecture consists of five distinct lifecycle agents and a logical orchestration responsibility.

The five agents must remain separate. Security and privacy are cross-cutting concerns that apply to every lifecycle phase.

This document describes the intended architecture. It does not claim that autonomous coordination, approval enforcement, or automated execution has already been implemented.

## 2. Architectural Overview

### 2.1 Lifecycle Agents

The project contains five specialized agents:

1. Requirements Engineer
2. System Designer
3. Implementation Engineer
4. QA Engineer
5. Deployment Engineer

Each agent has a defined scope, expected inputs, deliverables, acceptance criteria, and handoff responsibilities.

### 2.2 Orchestration Responsibility

A coordinator manages the lifecycle by assigning tasks, supplying relevant context, tracking project status, checking handoff conditions, and routing rejected work back to the responsible phase.

Initially, the main Claude Code session may perform this coordination role.

A separate autonomous orchestrator is not required by default. If greater automation is needed, its behavior must be designed, implemented, and tested explicitly.

### 2.3 Cross-Cutting Governance

All agents must consider:

- Security and privacy.
- Medical-data integrity and provenance.
- Risk identification and documentation.
- Human review and approval.
- Least-privilege access.
- Requirements traceability.
- Controlled changes and version history.

## 3. Requirements Engineer

### Purpose

Translate stakeholder needs into clear, testable, prioritized, and documented requirements.

### Responsibilities

- Identify stakeholders, user roles, and use cases.
- Define functional and non-functional requirements.
- Establish acceptance criteria.
- Identify assumptions, dependencies, constraints, and unresolved questions.
- Document privacy, security, accessibility, and operational requirements.
- Identify risks requiring design or human review.
- Maintain traceability between requirements and validation criteria.

### Inputs

- Project overview.
- Stakeholder needs.
- Existing project instructions and decisions.
- Relevant research and constraints.

### Outputs

- Requirements specification.
- Prioritized requirements.
- Acceptance criteria.
- Assumptions and open questions.
- Initial risk register.
- Stable requirement identifiers.

### Acceptance Criteria

- Requirements are clear and testable where applicable.
- Ambiguities and conflicts are explicitly recorded.
- Security and privacy requirements are included.
- Significant requirements have unique identifiers.
- Unresolved decisions are visible.
- The requirements baseline is reviewed and approved by the authorized decision-maker before system design is finalized.

### Boundaries

The agent must not independently finalize system architecture, begin implementation, or invent stakeholder decisions.

### Handoff

Deliver the requirements baseline to the System Designer.

If a requirement is ambiguous, contradictory, or incomplete, return it for clarification before relying on it in design.

## 4. System Designer

### Purpose

Transform approved requirements into a coherent, maintainable, secure system architecture.

### Responsibilities

- Define system components and their boundaries.
- Specify component responsibilities and interfaces.
- Design data models and data flows.
- Define authentication and authorization requirements.
- Specify medical-data provenance and verification handling.
- Design emergency-access behavior and audit requirements.
- Evaluate security and privacy threats.
- Document architecture decisions and trade-offs.
- Map requirements to design components.
- Identify technical uncertainties before implementation.

### Inputs

- Approved requirements baseline.
- Acceptance criteria.
- Project constraints.
- Existing architecture and risk documentation.

### Outputs

- System architecture.
- Component and interface specifications.
- Data model and data-flow documentation.
- Security and privacy design.
- Threat-model updates.
- Architecture decision records.
- Requirements-to-design traceability.
- Implementation constraints.

### Acceptance Criteria

- Significant requirements are addressed or explicitly marked unresolved.
- Component responsibilities and interfaces are sufficiently clear.
- Security, privacy, and data-integrity risks are addressed or documented.
- Assumptions and trade-offs are recorded.
- The design is reviewed and approved before implementation begins.

### Boundaries

The agent must not silently change approved requirements or present proposed controls as already implemented.

### Handoff

Deliver the approved design package to the Implementation Engineer.

If implementation reveals a design flaw, return the affected decision to the System Designer. If the root cause is an unclear requirement, involve the Requirements Engineer.

## 5. Implementation Engineer

### Purpose

Implement approved requirements and design decisions in maintainable, testable code.

### Responsibilities

- Inspect the existing repository and coding conventions.
- Break approved work into bounded implementation tasks.
- Implement features according to the approved design.
- Follow secure coding practices.
- Add or update relevant tests.
- Implement input validation, error handling, and access-control behavior as specified.
- Document implementation decisions and deviations.
- Report blockers, defects, and design conflicts.
- Update relevant technical documentation.

### Inputs

- Approved requirements.
- Approved system design.
- Implementation task and acceptance criteria.
- Coding standards and security requirements.

### Outputs

- Source-code changes.
- Relevant automated tests.
- Implementation notes.
- Updated technical documentation.
- Requirement-to-code references where practical.
- Test execution evidence and known limitations.

### Acceptance Criteria

- The assigned requirements are implemented according to the approved design.
- Relevant tests are added or updated.
- Repository conventions are followed.
- Deviations are disclosed rather than hidden.
- Security-sensitive changes are documented.
- The changes are ready for QA review.

### Boundaries

The agent must not silently redefine requirements, bypass required reviews, invent test results, or deploy to production without the required authorization.

Synthetic data must be used by default. Real medical information must not be used in development or testing unless a separately approved process explicitly permits it.

### Handoff

Submit implementation changes, test evidence, and known limitations to the QA Engineer.

Implementation defects return to the Implementation Engineer. Design and requirements defects return to their respective responsible agents.

## 6. QA Engineer

### Purpose

Independently evaluate whether the implementation satisfies requirements, acceptance criteria, and documented quality expectations.

### Responsibilities

- Derive tests from requirements and acceptance criteria.
- Review requirements coverage.
- Execute or inspect appropriate automated and manual tests.
- Evaluate validation, authorization, error handling, and data integrity.
- Test relevant boundary and failure conditions.
- Review security- and privacy-sensitive behavior within the assigned scope.
- Document defects, missing evidence, and untested areas.
- Verify fixes through retesting.
- Produce a release-readiness assessment.

### Inputs

- Approved requirements and design.
- Implementation changes.
- Test plans and acceptance criteria.
- Available test environment and synthetic data.
- Previous defect reports and test results.

### Outputs

- Test plan and test cases.
- Test execution results.
- Requirements coverage report.
- Defect and risk reports.
- Retest evidence.
- QA assessment with a documented rationale.

### Acceptance Criteria

- Required tests are executed or their absence is explicitly reported.
- Results include sufficient supporting evidence.
- Failures and uncovered requirements are documented.
- High-risk defects are not silently waived.
- Remaining risks are visible to the authorized decision-maker.

### Boundaries

The agent must not change acceptance criteria merely to make a failing implementation pass, conceal failures, invent test results, or independently authorize production deployment.

Passing tests do not prove complete security, regulatory compliance, or clinical safety.

### Handoff

Failed implementation returns to the Implementation Engineer with actionable evidence.

Design defects return to the System Designer. Ambiguous requirements return to the Requirements Engineer.

Once applicable QA criteria are satisfied, provide the test evidence and release-readiness assessment to the Deployment Engineer.

## 7. Deployment Engineer

### Purpose

Prepare and execute controlled releases and establish the operational procedures needed to maintain the application.

### Responsibilities

- Define deployment prerequisites and environment requirements.
- Review configuration and secret-handling requirements.
- Prepare migration, backup, and rollback plans where applicable.
- Verify required QA and approval evidence.
- Plan monitoring and failure handling.
- Document release versions and configuration changes.
- Coordinate post-deployment verification.
- Record deployment results and operational limitations.

### Inputs

- QA results and release-readiness assessment.
- Approved requirements and design.
- Release artifacts and implementation notes.
- Environment configuration and deployment constraints.
- Relevant security findings and required approvals.

### Outputs

- Deployment plan.
- Environment and configuration checklist.
- Migration and backup plan where applicable.
- Rollback procedure.
- Release record.
- Post-deployment verification results.
- Operational documentation.

### Acceptance Criteria

- Required QA evidence is available.
- Security and operational checks are addressed.
- The deployment target and release artifact are identified.
- Recovery and rollback considerations are documented.
- Required human approval has been obtained before consequential deployment actions.
- Results are recorded accurately.

### Boundaries

The agent must not bypass failed QA gates, expose secrets or medical information in logs, or deploy to production without required authorization.

### Handoff

Present the release package and remaining risks to the authorized approver.

After approval, execute the approved deployment procedure if the necessary tools and permissions are available. Document the result and follow the rollback or incident process if deployment fails.

## 8. Orchestration and Workflow Management

### Purpose

Coordinate the five agents and maintain lifecycle integrity.

### Responsibilities

- Track the current lifecycle phase.
- Assign work to the appropriate agent.
- Supply the relevant project context and artifacts.
- Check deliverables and handoff conditions.
- Track approval status, risks, and blockers.
- Route rejected work to the responsible agent.
- Maintain requirements traceability.
- Update project status.
- Prevent workflow progression when required evidence or authorization is missing.

### Initial Coordination Model

Initially, the main Claude Code session may coordinate the agents by following this architecture and explicitly assigning tasks.

Agent definitions and Skills can support specialized behavior, but their existence does not automatically implement a fully autonomous workflow.

If automated orchestration is introduced, its state model, routing rules, artifact transfer, retry behavior, logging, permission boundaries, and approval enforcement must be specified and tested.

## 9. Lifecycle Workflow

### Phase 1 — Requirements

**Responsible:** Requirements Engineer

Produce the requirements baseline, acceptance criteria, assumptions, and open questions.

**Gate R1:** Authorized review and approval of the requirements baseline.

Do not proceed with unresolved ambiguities that materially affect design.

### Phase 2 — System Design

**Responsible:** System Designer

Produce the architecture, interfaces, data model, security and privacy design, and traceability records.

**Gate D1:** Design review and approval.

Do not begin implementation until the design is sufficiently complete for the assigned work.

### Phase 3 — Implementation

**Responsible:** Implementation Engineer

Implement the approved design and requirements, add relevant tests, and document known limitations.

**Exit condition:** The change is ready for independent QA review.

Implementation completion is not proof that requirements have been satisfied.

### Phase 4 — QA and Revision

**Responsible:** QA Engineer

Verify implementation against requirements and acceptance criteria.

**Gate Q1:** Required acceptance criteria must be satisfied, or any permitted exception must be documented and approved by the authorized role.

If QA fails:
1. Document the defect and supporting evidence.
2. Identify the responsible lifecycle phase.
3. Return implementation defects to the Implementation Engineer.
4. Return design defects to the System Designer.
5. Return requirements defects to the Requirements Engineer.
6. Retest the corrected work.

High-risk defects must not be silently bypassed.

### Phase 5 — Deployment Readiness

**Responsible:** Deployment Engineer

Prepare the release checklist, deployment plan, recovery procedures, and operational documentation.

**Gate DEP1:** Required release evidence and explicit deployment authorization.

Do not deploy when required QA evidence is missing or deployment authorization has not been obtained.

### Phase 6 — Post-Deployment Verification

**Responsible:** Deployment Engineer

Verify the release, record the actual outcome, and document operational issues.

If deployment fails, follow the documented incident or rollback procedure and route necessary corrections to the responsible agent.

## 10. Handoff Contract

Every handoff should include:

1. Task and lifecycle phase.
2. Relevant approved requirements.
3. Relevant design decisions.
4. Deliverables produced.
5. Acceptance criteria and their status.
6. Supporting evidence and test results.
7. Known defects, limitations, and risks.
8. Unresolved questions and assumptions.
9. Required approvals and their status.
10. Recommended next action.

The receiving agent must not assume that missing information has been completed or approved.

If essential information is missing, request clarification or return the task with a documented reason.

## 11. Cross-Cutting Security and Privacy

### Requirements Phase
Define data sensitivity, intended use, user roles, access boundaries, emergency-access expectations, and security requirements.

### Design Phase
Evaluate trust boundaries, data flows, authentication, authorization, medical-data provenance, audit behavior, and QR-code risks.

### Implementation Phase
Implement approved controls, validate inputs, protect secrets, minimize data exposure, and document security-sensitive changes.

### QA Phase
Test access-control rules, failure cases, emergency-access restrictions, data-integrity behavior, and logging exposure.

### Deployment Phase
Protect configuration, restrict deployment permissions, prepare recovery procedures, and verify release settings.

A separate security-review agent may be considered later if justified. It must supplement rather than replace any of the five lifecycle agents.

## 12. PHR-Specific Safety Considerations

### Medical Data Provenance
Medical records should preserve their source, relevant timestamps, and verification status. Unverified information must not be represented as verified.

### Emergency Access
Define who may access emergency information, under what conditions, which fields are exposed, how access is restricted, and how access is audited.

### QR-Code Risks
Do not assume a QR code is secure merely because it is difficult to guess or physically attached to a person.

Evaluate copying, unauthorized scanning, URL sharing, token exposure, unintended disclosure, expiration, and revocation. Proposed safeguards must be specified and tested rather than assumed to exist.

### Audit Logs
Audit records should support accountability while minimizing exposure of medical information. Access to audit records must also be controlled.

### Test Data
Use synthetic data by default. Do not place real medical information, credentials, or private tokens in source control, ordinary prompts, test fixtures, or logs.

### Human Oversight
Automated tests do not establish clinical safety or legal compliance. Appropriate evidence and qualified human review may be required.

## 13. Permissions and Approval Gates

Permissions must be appropriate to each task.

Where supported by the available tooling:
- Use read-only access for review-only tasks.
- Restrict modifications to the relevant project scope.
- Require authorization for destructive operations.
- Protect secrets and sensitive information.
- Restrict production deployment and consequential external actions.

Each approval gate must identify the required evidence and authorized approver.

A Markdown instruction does not itself enforce a technical restriction. Enforcement depends on the configured tools, permissions, environment, and application logic.

## 14. Documentation and Traceability

Use the following locations where applicable:

- `CLAUDE.md` — project-wide instructions.
- `docs/project-overview.md` — purpose and scope.
- `docs/architecture.md` — this architecture.
- `projects/phr/docs/project-status.md` — current phase, progress, blockers, and next action.
- `docs/requirements/` — requirements and acceptance criteria.
- `docs/design/` — architecture and design decisions.
- `docs/implementation/` — implementation notes.
- `docs/testing/` — test plans, results, and defects.
- `docs/deployment/` — release and operational documentation.
- `docs/security/` — threat models, risks, and security decisions.

Create missing files or directories when needed. Do not assume that a referenced path already exists.

Requirements should be traceable to design decisions, implementation changes, tests, and release decisions wherever practical.

Record significant changes, risks, and decisions in the appropriate documentation and version control.

## 15. Open Decisions

The following matters must be resolved through requirements, research, design, or appropriate human review:

- Which user roles and organizations may access medical records?
- What is the emergency-access authorization model?
- What information is exposed in the emergency view?
- How are QR-linked access mechanisms issued, protected, and revoked?
- Which medical information sources and verification procedures are supported?
- Which audit events are recorded, and who may inspect them?
- What data-retention and account-deletion rules apply?
- Which legal and regulatory requirements apply to the intended deployment jurisdiction?
- What backup, recovery, and incident-response requirements are necessary?
- Which actions require explicit human approval?
- Which orchestration activities will initially be manual and which may later be automated?

Do not silently resolve these decisions through implementation assumptions.

## 16. Architecture Acceptance Criteria

The architecture is ready for implementation planning when:

- All five lifecycle agents have distinct responsibilities.
- Each agent has defined inputs, outputs, boundaries, and acceptance criteria.
- Coordination responsibilities and limitations are explicit.
- Lifecycle transitions and revision loops are documented.
- Approval gates identify required evidence and authorized approvers.
- Security, privacy, medical-data integrity, and emergency access span all phases.
- Traceability and project-status tracking are defined.
- Claude configuration capabilities are distinguished from custom orchestration and technical enforcement.
- Open decisions are recorded.
- The architecture has been reviewed and approved by the appropriate project decision-maker.

**End state:** A documented five-agent lifecycle architecture with explicit coordination, traceable deliverables, controlled approval gates, and cross-cutting security and privacy.