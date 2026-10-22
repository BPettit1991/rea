# NDIS Wizard SaaS: Product Requirements (PRD)

Product: NDIS Wizard (Ozzieai.com.au)
Status: Draft v0.1, depends on decisions D1 to D7 in 01-scope.md
Date: 2026-10-22

## 1. Problem statement

Small registered NDIS providers cannot easily tell whether they meet the NDIS Practice Standards, whether they reported incidents on time, or whether their workers and prices are compliant. They track this in spreadsheets and folders. Gaps appear late.

## 2. Goals and non-goals

### Goals (v1)
- G1: Get a new provider to a complete, personalised gap assessment in under 60 minutes.
- G2: Make reportable incidents impossible to miss: every incident shows the correct deadline, the correct portal, and a reminder.
- G3: Keep the worker and policy registers current with reminders before expiry.
- G4: Make every AI-generated document reviewable, editable and approved by a named person.
- G5: Give the owner one dashboard that answers "what is overdue or about to be?".

### Non-goals (v1)
- Claim lodgement, invoicing, rostering, payroll, clinical notes (see scope section 4.2).
- Legal advice, certification, or any statement that the provider is "compliant".

## 3. Personas

- **Owner (Dana, example):** Runs a 12-person disability support provider. Not a compliance specialist. Wants to know she is safe and what to do this week.
- **Coordinator (Sam, example):** Manages incidents, worker records and audits. Uses the register daily. Wants speed and fewer clicks.
- **Support worker (Priya, example):** Needs to complete training and read policies. Should see only their own tasks.

Personas are hypotheses. Replace them with interview findings from Phase 0.

## 4. Functional requirements

Priority: P0 = MVP must have, P1 = MVP should have, P2 = later.

### FR-1 Onboarding wizard (P0)

Steps:
1. Organisation: legal name, ABN, trading name, contact, state or territory.
2. Registration: registration groups held, and the date each was granted.
3. Services: the support categories and support types delivered.
4. Team: estimated headcount, roles, and whether there are shared-living or community services.
5. Review and generate the gap assessment.

Acceptance criteria:
- AC-1.1: Each step saves progress. The user can leave and resume at the same step.
- AC-1.2: Registration groups and support categories come from a versioned reference list, not free text.
- AC-1.3: A user can complete the wizard in one session without contacting support, in a usability test with 5 owners (target: median under 45 minutes).
- AC-1.4: Skipping a required field shows a plain-language reason and does not produce a gap assessment.

### FR-2 Practice Standards gap assessment (P0)

- The product maps the organisation's profile to the applicable Practice Standards indicators (versioned, currently the November 2021 version, to confirm).
- For each applicable indicator the user marks: evidence held, partly held, not held, or not applicable (with a reason).
- The output is a gap list with a priority, an owner and a due date.

Acceptance criteria:
- AC-2.1: Every indicator in the rule pack appears once. None are dropped or duplicated (checked against the rule pack file).
- AC-2.2: A "not applicable" answer requires a written reason.
- AC-2.3: The report states that it is a readiness checklist, not a certification (fixed wording, reviewed by counsel).
- AC-2.4: Changing the rule pack version does not change historic assessments. Each assessment stores the version it used.

### FR-3 Policy and procedure library with AI drafts (P0)

- Library of templates: incident management, complaints, restrictive practices, privacy and information management, worker screening, and others from the rule pack.
- An AI draft is generated from the template and the organisation profile. The draft is labelled "AI draft, not approved".
- The user edits the draft. Only a user with the Owner role can approve. Approval records name, date and version.
- Each approved policy has a review date (default 12 months), with reminders.

Acceptance criteria:
- AC-3.1: No policy can be marked "approved" by a user without the Owner role.
- AC-3.2: Every edit creates a version. The user can view and restore any prior version.
- AC-3.3: The draft is never exported or shared outside the organisation without approval.
- AC-3.4: The AI drafting prompt and model version are logged for each draft.
- AC-3.5: Before launch, every template has been reviewed by a qualified reviewer (tracked as a launch gate, not a code check).

### FR-4 Incident register and reporting clock (P0)

- Create an incident with: date and time of awareness, person(s) involved (by participant reference, not name in the free-text fields), description, immediate actions, and category.
- Category selection drives the reporting rule:
  - Death, serious injury, abuse or neglect, unlawful sexual or physical contact, or sexual misconduct: 24-hour notification.
  - Unauthorised restrictive practice: 5-business-day report. If harm occurred, 24-hour notification.
- The reporting clock starts from the time the provider became aware (the field in AC-4.1), not from when the incident was entered.
- The product shows the deadline, the reporting portal (per the date rule in section 5 of the scope), and a status (not yet notified, notified, 5-day report due, closed).
- Reminders at 50% and 90% of the time window, and on the due time, to the owner and coordinator.
- The product does not submit reports to the Commission in v1. It stores the content the user needs to enter there.

Acceptance criteria:
- AC-4.1: The "time of awareness" field is required. Entering an incident without it is blocked.
- AC-4.2: For each category in the rule table, a test case confirms the correct deadline (24 hours or 5 business days, and the harm override). Test cases run in CI.
- AC-4.3: Business-day calculation excludes weekends and the public holidays for the state or territory. Holiday data is versioned. Test cases cover a holiday on a Monday and a long weekend.
- AC-4.4: For incidents with an awareness date on or after 12 October 2026, the portal shown is the new NDIS Commission Portal. Earlier incidents show the existing portal. Test cases cover both sides of the boundary.
- AC-4.5: Each incident keeps a full audit trail. Edits after notification are shown as amendments, not overwrites.
- AC-4.6: Reminder emails contain no participant names.

### FR-5 Worker compliance register (P0)

- Per worker: role, start date, worker screening check (type, reference, issue and expiry dates), qualifications, and mandatory training.
- Expiry reminders at 90, 30 and 7 days, and on expiry.
- Workers who are overdue on a required item are flagged on the dashboard.

Acceptance criteria:
- AC-5.1: A worker with an expired screening check is shown as non-compliant with a reason.
- AC-5.2: Reminders are sent once per threshold per item. A test confirms no duplicates on re-runs of the reminder job.
- AC-5.3: Workers with the "worker" role see only their own records and assigned training.
- AC-5.4: Screening check references are stored as entered. The product does not verify them against any external system in v1.

### FR-6 Evidence vault (P0)

- Attach files (PDF, Word, Excel, images; maximum 25 MB per file) to a requirement, policy, incident or worker record.
- Each file has a hash, uploader, timestamp and a link to the record it supports.

Acceptance criteria:
- AC-6.1: Uploaded files are virus-scanned before becoming downloadable.
- AC-6.2: Deleting a file creates an audit entry and removes it from view, but keeps it for the retention period (decision D8, default 7 years).
- AC-6.3: Files are only downloadable by users in the same organisation with access to the linked record. A cross-tenant access test is in the automated suite.

### FR-7 Price reference (P1)

- Import the NDIS Pricing Schedule and Support Catalogue for each financial year (manual upload in v1, with a checksum and the effective date recorded).
- A user enters a support item number, unit, and location (national, remote or very remote). The product shows the maximum price for that combination and flags a rate above it.
- No claim is created or lodged.

Acceptance criteria:
- AC-7.1: Prices are stored by financial year. Looking up a 2026-27 item returns the 2026-27 price, not the earlier price.
- AC-7.2: A rate above the maximum is flagged. A rate at or below the maximum is not.
- AC-7.3: The product shows the source file and effective date with every price result.
- AC-7.4: Before launch, legal review confirms the product can display the price data (decision in scope section 9).

### FR-8 Dashboard and task list (P0)

- Shows: open gaps by priority, reporting clocks due in the next 48 hours, worker items expiring in 30 days, policies due for review, and actions assigned to the user.
- Each item links to the record.

Acceptance criteria:
- AC-8.1: Every dashboard count links to a filtered list that returns the same count.
- AC-8.2: The page loads in under 2 seconds at the 95th percentile with 500 workers and 2,000 incidents (test dataset).

### FR-9 Accounts, roles and audit log (P0)

- Roles: Owner, Coordinator, Worker. Owner can invite, change roles, approve policies, and see the audit log.
- Every create, edit, approve, delete and login event is logged with user and time.

Acceptance criteria:
- AC-9.1: Role permissions are enforced on the server, not only in the interface. Automated tests cover each role against each endpoint.
- AC-9.2: Sessions expire after 30 minutes of inactivity. Multi-factor authentication is available from day one and required for the Owner role (decision D9).
- AC-9.3: The audit log cannot be edited by any user.

## 5. Non-functional requirements

| Area | Requirement |
|---|---|
| Hosting | Australian region for all participant data (decision D4) |
| Privacy | Data minimisation: no participant names in free text, notes or reminder emails. Privacy policy and data handling reviewed before launch |
| Security | Encryption at rest and in transit. Secrets in a managed vault. Dependency and secret scanning in CI. Annual external penetration test before paid launch |
| Availability | 99.5% monthly for the app. Reminder jobs retried until success or alert |
| Accessibility | WCAG 2.2 AA for all screens (the accessibility skill and review apply) |
| Performance | See AC-8.2. Wizard steps respond within 300 ms at the 95th percentile, excluding network |
| Backups | Daily backups, 30-day retention, restore tested monthly |
| Records | Retention default 7 years for incident and worker records (confirm against state requirements) |
| Browsers | Current two versions of Chrome, Edge, Safari, and Firefox |
| Support | Email support, 1 business day first response, in-app help for each step |

## 6. Data model (outline)

Core entities (names are proposals):

- `Organisation` (id, legal name, ABN, state, registration groups, rule pack version)
- `User` (id, organisation, role, MFA status, status)
- `Assessment` (id, organisation, rule pack version, created, status) and `AssessmentItem` (indicator id, status, reason, evidence links)
- `Policy` (id, organisation, template id, current version, status, review date) and `PolicyVersion` (content, author, approver, AI draft flag, prompt and model version)
- `Incident` (id, organisation, awareness time, category, reportable flag, deadline, portal, status, participant reference) and `IncidentEvent` (append-only)
- `Worker` (id, organisation, user link optional, role) and `WorkerRequirement` (type, reference, issued, expires, status)
- `EvidenceFile` (id, hash, scan status, linked record, uploader, timestamp)
- `PriceItem` (financial year, item number, unit, location, max price, source file, effective date)
- `AuditEvent` (append-only: actor, action, target, time, before and after hashes)

Design rules:
- Append-only tables for `IncidentEvent` and `AuditEvent`.
- Rule packs (Practice Standards indicators, incident rules, holidays, price years) are versioned data files, not code constants.

## 7. Analytics and success metrics

| Metric | Target at 90 days from pilot start |
|---|---|
| Time to gap assessment (median) | Under 45 minutes |
| Pilot providers still active weekly (week 4) | At least 60% |
| Incidents with a reporting deadline shown within 1 minute of entry | 100% |
| Reminders delivered on schedule (test metric) | 100% in test, 99% in production |
| Paid conversion from pilot | Measured, target set after Phase 0 |

Track events for funnel steps only. No participant data in analytics.

## 8. Open questions

- Q1: Does the owner or the coordinator buy? (Interview question in Phase 0.)
- Q2: Which state or territory first? Requirements for state-specific holidays and rules depend on the answer.
- Q3: Should the product support plan-managed or self-managed participants' records, or only provider-side compliance? (Current answer: provider-side only.)
- Q4: Retention period for records (default 7 years, confirm).
- Q5: Whether the AI draft model may be hosted by a third party outside Australia. (Affects D4.)

## 9. Release gates (not optional)

1. Legal review of every policy template and AI drafting prompt.
2. Verification of the incident rule table and portal date rule against the Commission's current published guidance.
3. Verification of price data licensing for display in the product.
4. Penetration test passed with no open high or critical findings.
5. Pilot exit criteria met (section 7).
