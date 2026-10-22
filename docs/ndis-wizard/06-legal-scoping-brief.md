# Legal Scoping Brief

Supports: 03-plan.md task 0.3 (legal scoping call) and PRD section 9 (release gates 1 to 3)
Status: Draft v0.1, for review before sending to counsel
Date: 2026-10-22

## 1. Purpose

We want a written scoping view, not a full opinion, on the legal risks of a readiness and reminders tool for registered NDIS providers. The aim is to decide what the product can do in v1, what wording it must use, and what must be in place before any pilot.

Ask counsel for:
1. A written memo on the questions in section 4, marked by priority.
2. A fee estimate for template and prompt review (PRD gate 1).
3. A list of the documents counsel would need before a pilot agreement can be drafted.

## 2. Product summary (for counsel)

- Users: registered NDIS providers (small and medium), their owners and coordinators.
- The product drafts policies and procedures with AI. A named person must review and approve each draft before use.
- It records incidents, tracks the reporting deadline (24 hours or 5 business days, per the NDIS Commission rules), and sends reminders.
- It tracks worker screening check reference numbers, issue and expiry dates, and training. It does not verify checks with any external system in v1.
- It holds a price reference loaded from NDIS pricing publications. It does not lodge claims or invoices in v1.
- It does not give legal advice and does not certify compliance. Every output carries a readiness-not-certification statement.
- Hosting: Australian region for participant data, subject to the decision on AI model hosting (scope D4).
- Scope limits: no participant plan management, no invoicing, no rostering in v1.

## 3. Facts verified on 2026-10-22 (check before sending)

| Fact | Source | Status |
|---|---|---|
| Death, serious injury, abuse or neglect, unlawful contact, and sexual misconduct: notify the NDIS Commission within 24 hours of awareness | NDIS Commission, reportable incidents page | Verified |
| Unauthorised restrictive practice: 5 business days, or 24 hours if harm occurred | NDIS Commission, reportable incidents page | Verified |
| New incidents lodged in the new NDIS Commission Portal from 12 October 2026 | NDIS Commission, reportable incidents page | Verified |
| 2026-27 pricing takes effect 1 July 2026; Pricing Schedule and Support Catalogue are separate publications | NDIS pricing pages and a secondary summary | Partly verified. Check the primary source |
| From 1 January 2027, recommended maximum prices for some Social, Community and Civic Participation supports for unregistered providers fall by 10% | Secondary summary | Not verified. Check the primary source |
| Practice Standards and Quality Indicators, November 2021 version | NDIS Commission PDF | Confirm the version is current |

## 4. Questions for counsel (priority order)

### P1: must answer before any pilot

1. **AI-drafted policies and reliance.** What disclaimers, approval workflow and records reduce the risk that a provider relies on an AI draft without review? Is the "AI draft, not approved" label plus a named Owner approval enough? What wording is safe for the product name, marketing and reports?
2. **Misleading conduct.** Under the Australian Consumer Law, what claims can we make about readiness, compliance, or time saved? Which words should we avoid (for example "compliant", "audit-ready", "guaranteed")?
3. **Privacy Act 1988 and the Australian Privacy Principles.** Which obligations apply to us as a service provider and to our customers? Participant information in incident records and worker records is sensitive information. What must the privacy policy and collection notices say?
4. **Notifiable data breaches.** Confirm our obligations if an incident or worker record is breached, and how the product's incident reminders interact with a provider's own reporting duties.
5. **Cross-border AI processing.** If any AI model is hosted outside Australia, what does that mean under the Privacy Act and our customers' obligations? Does the answer change scope decision D4?
6. **Limitation of liability and disclaimers.** What liability cap, indemnity and disclaimer wording suits a SaaS tool that informs regulatory reporting? Does a provider's use of the tool shift responsibility to the provider?

### P2: must answer before general launch

7. **Worker screening data.** We store screening check reference numbers and dates, not the check results. Does the NDIS worker screening legislation (NDIS (Worker Screening) Act 2018) or any state law limit storing or displaying this information? What about NSW Working With Children Check records?
8. **Incident and restrictive practice data.** Does the NDIS Commission's rules or state restrictive practice law limit who can see this information, or how long it must be kept? What is the right retention period (default 7 years in the PRD)?
9. **Price data use.** Can we load and display NDIS Pricing Schedule and Support Catalogue information in a paid SaaS product? What licence or terms of use apply, and must we credit the source?
10. **Automated decision-making.** Does any part of the product make decisions that affect people (for example, flagging a worker as non-compliant)? If so, what transparency duties apply, and do they commence in the period we will operate in? Check the current position.
11. **Terms and data processing.** What should the pilot agreement, the terms of service and the data processing terms cover, at minimum?
12. **Spam Act 2003.** Does our research outreach or product marketing need consent, identification and an unsubscribe mechanism? What is the position for the interview invitations in 05-outreach-message.md?

### P3: structural

13. **Entity structure.** Should the product sit in a separate company from Linkhaus to isolate liability and IP? Does that affect the brand choice (07-brand-options.md)?
14. **Brand and name.** Can "NDIS" appear in a product trade mark? Is a full IP Australia search and attorney clearance review the right next step? Our quick search found no records for the shortlisted names, which is not clearance.
14a. **Housekeep sound-alike risk (proposed product name Hauskeep).** Housekeep (housekeep.com) is an active UK home-cleaning marketplace with a large public presence. The Australian quick search found no Housekeep trade mark, but the name may still trade in Australia. Questions:
   - Does Housekeep trade or have goodwill in Australia? If so, could it claim passing off or misleading conduct against a name that sounds the same?
   - Is the risk materially higher because both names sit in consumer-facing service markets? (Our customers are NDIS providers, not households, but the names are close in sound.)
   - Should we choose a different name before any trade mark filing, or can we manage the risk through spelling, trade dress and disclaimers?
   - What search scope (phonetic variants, classes 9, 35, 42, 44) and what evidence of Housekeep's Australian use would counsel need before advising?
   - Does the Linkhaus trade mark filing (question 14b) change the answer?
14b. **Linkhaus trade mark.** The quick search found no Linkhaus records. Which classes should we file in before the product name is public? Does filing order matter when the product mark is the one that carries the market?
15. **Contractor IP.** The compliance advisor and any engineers will be contractors. What IP assignment and confidentiality terms do we need?
16. **Insurance.** What professional indemnity and cyber cover do we need before a pilot?

## 5. Information counsel will need

- The full PRD (02-prd.md) and the scope (01-scope.md).
- The interview script and consent wording (04-phase0-interview-script.md, section 3). The interviews collect no identifying information.
- Draft rule tables and the policy template list (to be prepared in Phase 0 task 0.4).
- The hosting and AI vendor options (Phase 0 task 0.7).
- A draft privacy policy and collection notice (not yet written).

## 6. Out of scope for this brief

- Full review of policy templates (PRD gate 1, separate engagement).
- Tax, employment, and corporate structuring advice beyond question 13.
- Any claim-lodgement or invoicing work (out of scope for v1).

## 7. Budget and timing

- Scoping call: 60 minutes. Target: within 2 weeks.
- Written memo on P1 questions: target within 4 weeks of the call.
- Budget: [to be confirmed by owner]. Plan section 6 notes that legal is milestone-based.
