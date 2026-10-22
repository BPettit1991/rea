# NDIS Wizard SaaS: Scope

Product: NDIS Wizard, a SaaS product from Ozzieai.com.au
Status: Draft v0.1 (for review)
Date: 2026-10-22

## 1. Working assumption (confirm this first)

The brief says "NDIS wizard". This document assumes it means:

> A guided, AI-assisted workspace that takes a registered NDIS provider (a small or medium support provider) from setup to day-to-day compliance. It produces the policies, registers, evidence and claim-ready records the NDIS Quality and Safeguards Commission (the Commission) expects, and tells the user what to do next.

If the intent is different (for example, a tool for participants reading their plans, or a plan manager tool), sections 3 and 4 change materially. Decision D1 in section 8 covers this.

## 2. Problem

- Small NDIS providers must meet the NDIS Practice Standards, report incidents on tight deadlines, keep worker screening current, and price every claim within the NDIS price limits.
- Most small providers do this with spreadsheets, template folders and memory. Gaps surface at audit or at an incident, not earlier.
- Compliance advice is expensive. Generic templates do not fit the provider's actual services, so they are often not used.

Hypothesis to test in Phase 0: a provider with 1 to 30 staff will pay to get to "audit-ready" faster and with fewer gaps than a spreadsheet and template set gives them.

## 3. Target users

| User | Role in the product | Priority |
|---|---|---|
| Owner or director of a small provider | Buys, sets up, approves policies, receives alerts | Primary |
| Compliance or quality coordinator | Runs the registers, evidence and audits day to day | Primary |
| Support coordinator or team leader | Logs incidents, completes shift and service records | Secondary |
| Support worker | Completes assigned training and acknowledgements only | Secondary (limited access) |
| External auditor | Read-only access to evidence for an audit | Tertiary (later phase) |

## 4. Scope

### 4.1 In scope for v1 (MVP)

1. Onboarding wizard
   - Business profile: legal entity, ABN, registration groups, services delivered, states and territories.
   - Generates a Practice Standards gap assessment from the profile.
2. Practice Standards gap assessment and action plan
   - Maps each applicable indicator to evidence the user holds, and marks gaps.
3. Policy and procedure library
   - Template policies tailored to the profile (for example incident management, complaints, restrictive practices, privacy, worker screening).
   - AI draft, then mandatory human review and approval with version history.
4. Incident register
   - Captures incidents, classifies them as reportable or not, and runs the reporting clock (see section 5).
   - Stores the 24-hour notice and 5-day report content.
5. Worker compliance register
   - Tracks worker screening checks, qualifications, mandatory training, and expiry dates, with reminders.
6. Evidence vault
   - Attaches files to requirements and register items. Keeps an audit trail of who changed what.
7. Price reference
   - Loads the NDIS Pricing Schedule and Support Catalogue for a given financial year.
   - Checks a support item, unit and price against the maximum price limit for the participant's location.
   - No automatic claim lodgement in v1.
8. Dashboard and task list
   - Shows open gaps, due reporting clocks, expiring checks, and overdue reviews.
9. Accounts and roles
   - Organisation, user invitation, owner and coordinator roles, audit log.

### 4.2 Out of scope for v1 (explicitly)

- Automatic claim lodgement to the NDIA. Claim-file export is a Phase 2 item, and only after the NDIA's current channels are confirmed.
- Participant plan management, plan-managed invoicing and banking integration.
- Rostering, timesheets and payroll (these are a separate market category, and existing tools cover them well).
- Full clinical records and progress notes. The product records compliance events, not clinical care.
- Legal advice. The product drafts and prompts. A qualified person approves.
- Guaranteed "compliant" or "audit passed" status. The product reports readiness against its checklist, not a certification.
- Native mobile apps. v1 is responsive web.
- Multi-country or NDIS-equivalent schemes outside Australia.

### 4.3 Explicitly deferred (Phase 2 and later)

- Claim-file export in the format accepted by the NDIA channels (confirm format and access first).
- Integrations with common provider software (CRM, accounting, rostering).
- Read-only auditor portal.
- Commission portal assistance beyond the reporting timeframes (for example, pre-filled forms, if the Commission permits).

## 5. Regulatory anchors (verified 2026-10-22)

| Area | What the product must support | Source |
|---|---|---|
| Reportable incidents | Death, serious injury, abuse or neglect, unlawful sexual or physical contact, and sexual misconduct: notify within **24 hours**. Unauthorised restrictive practice: notify within **5 business days**, or **24 hours** if it caused harm. | NDIS Commission, reportable incidents page |
| Incident portal | From **12 October 2026**, new incidents (24-hour and 5-day reports) are lodged in the new NDIS Commission Portal. Incidents lodged before that date stay in the old portal. The product must record which portal applies. | NDIS Commission, reportable incidents page |
| Price limits | 2026-27 pricing takes effect 1 July 2026. Pricing is now split into the Annual Pricing Review, the NDIS Pricing Schedule and the NDIS Support Catalogue. From **1 January 2027**, recommended maximum prices for some Social, Community and Civic Participation supports for unregistered providers fall by 10%, and indexation stops for those items. | NDIS pricing pages, Hunter Care Group summary (verify against the NDIS source before build) |
| Practice Standards | Practice Standards and Quality Indicators (November 2021 version): core and supplementary modules. | NDIS Commission PDF (2021) |
| Privacy | Privacy Act 1988 and the Australian Privacy Principles, which apply to most providers. Participant data is sensitive information. | To confirm with privacy counsel |

Note: the pricing summary and the Practice Standards version both need checking against the official sources at build time. Pricing changes every 1 July, so the product must load prices by financial year, not hard-code them.

## 6. Success measures for the scope

- Phase 0: at least 10 provider interviews, and at least 5 with a paid or letter-of-intent pilot. Plan section 2 defines the 3 to 4 commitment band.
- Requests logged in Phase 0 (billing and invoicing, participant budgets, participant service agreements, rostering integration) go to the Phase 2 list. They are not Phase 1 work.
- Phase 1: 5 pilot providers complete onboarding and the gap assessment within 60 minutes, and 3 keep using it weekly for 30 days.
- Incident register: 100% of test incidents show the correct reporting deadline and portal.

## 7. Key risks

| Risk | Impact | Mitigation |
|---|---|---|
| AI drafts policies that are wrong or out of date | Provider harm, liability | Human approval gate, versioned sources, clear "draft" labels, legal review of templates before launch |
| Regulatory change (Practice Standards, portal, pricing) | Product becomes wrong | Versioned rule packs by financial year, a named owner for regulatory updates |
| Sensitive participant data breach | Serious harm, notifiable breach | Minimise personal data, encryption, Australian hosting (decision D4), access logging, incident plan |
| Users treat readiness as certification | Misplaced trust | Plain-language disclaimers, readiness wording, no "compliant" badge |
| Small market, slow sales cycle | Runway | Phase 0 willingness-to-pay test before build |

## 8. Decisions needed from you

| # | Decision | My recommendation |
|---|---|---|
| D1 | Confirm the product reading in section 1 | Providers, compliance-first |
| D2 | Target provider size for launch | 1 to 30 staff, NDIS registered, Victoria or NSW first (both are high-volume, and you can test regional differences) |
| D3 | Pricing model | Per organisation tier by staff count, with a free onboarding checklist as the entry point |
| D4 | Data hosting | Australian region for all participant data (strongest buyer comfort; check cost) |
| D5 | Legal review budget | Yes. Templates and AI prompts need a lawyer or qualified compliance consultant before launch |
| D6 | Team | You (product), one full-stack engineer, a contract compliance advisor |
| D7 | Brand and domain | Ozzieai.com.au, product name "NDIS Wizard". Check trademark availability for "NDIS Wizard" before launch |

## 9. Not yet known (to find out in Phase 0)

- Whether the NDIA's current claim channels allow a third-party tool to submit claims, and on what terms.
- Whether the Commission's new portal has an API or bulk-upload route.
- How much of the price data (Support Catalogue) can be redistributed in a SaaS product.
- The actual pain point that makes an owner buy: audit fear, a recent incident, or growth.
