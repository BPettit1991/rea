# NDIS Wizard SaaS: Delivery Plan

Product: NDIS Wizard (Ozzieai.com.au)
Status: Draft v0.1
Date: 2026-10-22
Depends on: 01-scope.md (decisions D1 to D7), 02-prd.md (requirements FR-1 to FR-9)

Timings assume a team of you (product), one full-stack engineer, and a contract compliance advisor. If the team is smaller, Phase 1 roughly doubles.

## 1. Plan at a glance

| Phase | Weeks | Goal | Exit gate |
|---|---|---|---|
| 0. Validate | 1 to 4 | Prove providers will pay and the rules are right | 10 interviews, 5 pilot commitments, legal questions answered |
| 1. Build MVP | 5 to 16 | Ship FR-1 to FR-9 (P0), plus FR-7 if ready | Internal test passes all acceptance criteria |
| 2. Pilot | 17 to 26 | 5 paying pilot providers | Pilot exit criteria (PRD section 7) |
| 3. Launch and extend | 27 onward | Public launch, then claim export and integrations | Decision based on pilot metrics |

Hard rule: no build work starts on FR-3 (AI drafts) or FR-4 (incidents) before the legal and rules checks in Phase 0 are complete. Code can be written against draft rules, but nothing ships on them.

## 2. Phase 0: Validate (weeks 1 to 4)

### Objectives
- Confirm the product reading in scope section 1 (decision D1).
- Confirm who buys (owner or coordinator), and what triggers a purchase.
- Confirm the rules the product depends on.

### Tasks

| # | Task | Owner | Output |
|---|---|---|---|
| 0.1 | Interview 10 registered providers (5 small, 5 medium). Use a fixed script: current tools, last audit or incident, cost of compliance, willingness to pay | You | Interview notes, pain-point summary |
| 0.2 | Landing page with the wizard's first step and a waitlist or pilot form | You | Conversion data on the offer |
| 0.3 | Legal scoping call with a privacy and disability-sector lawyer: AI-drafted policies, liability, privacy, price data licensing | You | Written advice on risks and required wording |
| 0.4 | Read the Commission's current incident guidance and the new portal documentation; confirm the 24-hour and 5-day rules and the 12 October 2026 portal boundary | You or advisor | Rule table signed off in writing |
| 0.5 | Confirm NDIA claim channels and whether third-party submission is permitted. Check whether the Support Catalogue can be shown in a SaaS product | You | Written answer; if negative, claim export moves out of the plan |
| 0.6 | Trademark search for "NDIS Wizard" and availability of the domain and social handles | You | Go or no-go on the name. Status 2026-10-23: product name is Complihaus. The owner holds complihaus.com.au. Quick IP Australia search finds no records. Run a full search and counsel review (legal brief 14a) |
| 0.7 | Choose the AI model host and region. Confirm Australian hosting is possible at a workable cost (decision D4) | Engineer | Hosting decision record |

### Phase 0 exit gate
- Proceed: 5 or more providers agree in writing to a paid or priced pilot. Written means a signed pilot agreement or letter of intent that states a price and a start date.
- Conditional commitments (for example, pending an IT review) are recorded separately. They do not count toward the 5 until the condition clears.
- Proceed with conditions: 3 or 4 written commitments, with at least one in a named segment. Before Phase 1 hiring, name the segment and the two further commitments needed to reach 5.
- Stop or pivot: fewer than 3 written commitments. Record the reason before building.
- 0.3 and 0.4 are complete. 0.5 is answered (even if the answer is "not in v1").
- Decisions D1 to D7 are recorded in the repository.

## 3. Phase 1: Build the MVP (weeks 5 to 16)

Built in four two-week sprints, each ending with a working, demoable slice.

### Sprint 1 (weeks 5 and 6): Foundations and onboarding
- Project setup, CI with linting, tests and secret scanning
- Accounts, organisations, roles (FR-9), MFA
- Onboarding wizard steps 1 to 4 (FR-1)
- Rule pack format: versioned data files for indicators, incident rules, holidays
- Audit log (append-only)
- Spike (2 days): rostering and HR data import feasibility for medium providers (PRD Q6). Output is a yes, no or partial decision with the blocking constraints.

Demo: a new owner signs up, completes the wizard, and sees their profile.

### Sprint 2 (weeks 7 and 8): Gap assessment and incident register
- Gap assessment generation and scoring (FR-2)
- Incident register with category rules, awareness time, deadline and portal logic (FR-4)
- Business-day calculation with holiday data
- Reminder job with retry and no duplicate sends

Demo: an incident entered at 9 am on a Friday gets a 24-hour deadline; a restrictive-practice incident gets a 5-business-day deadline with the correct holidays.

### Sprint 3 (weeks 9 and 10): Policies, workers and evidence
- Policy template library and AI draft generation with logging (FR-3)
- Policy approval workflow with versioning and review dates
- Worker register with expiry reminders (FR-5)
- Evidence vault with virus scanning and access control (FR-6)

Demo: an AI draft becomes an approved policy; an expiring screening check triggers a reminder.

### Sprint 4 (weeks 11 and 12): Dashboard, prices and hardening
- Dashboard and task list (FR-8)
- Price reference lookup with financial-year versioning (FR-7, P1; cut if late)
- Accessibility review (WCAG 2.2 AA), performance test at the PRD dataset size
- Backup restore test, security review, dependency audit

Demo: the owner's dashboard shows open gaps, reporting clocks and expiring items for the pilot dataset.

### Weeks 13 to 16: Stabilise, legal gates, pilot preparation
- Legal review of all templates and prompts (PRD section 9, gate 1)
- Penetration test (gate 4). Fix all high and critical findings before pilot users log in.
- Onboarding help, support process, pilot agreement, data processing terms
- Seed pilot data and a migration path for providers moving from spreadsheets

Phase 1 exit gate: every acceptance criterion in PRD sections FR-1 to FR-9 passes in automated or manual test. Legal gates 1 to 3 are closed.

## 4. Phase 2: Pilot (weeks 17 to 26)

- Onboard 5 pilot providers. Run a weekly 30-minute check-in with each.
- Track the metrics in PRD section 7 from the first login.
- Fix the top three issues raised each fortnight. Do not add features during the pilot unless a pilot provider cannot complete a required task.
- Start Phase 2 product work (claim export, if Phase 0 task 0.5 confirmed it) in parallel only if it does not slow pilot fixes.

Pilot exit criteria:
- Median time to gap assessment under 45 minutes
- At least 3 of 5 pilots active weekly at week 4 of the pilot
- Every incident in the pilot shows the correct deadline and portal (audited by the advisor)
- At least 2 pilots say they would pay at the proposed price (record the exact words)

If the exit criteria are missed, the plan goes back to Phase 0 for the failed area, not forward to launch.

## 5. Phase 3: Launch and extend (week 27 onward)

Launch scope:
- Public sign-up with a free onboarding checklist and a paid tier by staff count (decision D3)
- Published privacy policy, terms, and a "readiness, not certification" statement on every report
- Support process and status page

Extension candidates, ranked by pilot evidence (not chosen now):
1. Claim-file export (only if 0.5 confirmed the channel)
2. Price-update workflow with alerts when the NDIS price year changes
3. Read-only auditor access (time-limited share links)
4. Integrations with rostering or accounting tools (after pilot demand is clear; the Phase 1 spike in Sprint 1 sets the rostering and HR decision)

## 6. Team and roles

| Role | Who | Time | Responsibilities |
|---|---|---|---|
| Product owner | You | Full time | Scope, interviews, rule sign-off, pilot relationships, pricing |
| Engineer | To hire or contract | Full time from week 5 | Build, tests, hosting, security |
| Compliance advisor | Contract, disability sector | Part time, weeks 1 to 4 and 11 to 16 | Rule tables, templates, pilot audits |
| Legal | External lawyer | Milestone-based | Templates, AI drafting risk, privacy, data processing terms |
| Security tester | External firm | One engagement, weeks 13 to 15 | Penetration test |

If the engineer is not hired by week 5, Phase 1 moves right by the same number of weeks.

## 7. Recommended stack (proposal, to confirm in Phase 0.7)

| Layer | Recommendation | Alternative |
|---|---|---|
| App | TypeScript, Next.js, server-rendered, responsive | Any framework the engineer knows well |
| Database | Managed PostgreSQL in an Australian region | Any managed relational database with AU hosting |
| Files | Object storage in the same region, with virus scanning on upload | Same |
| Jobs | Managed queue or cron for reminders, with retries and a dead-letter view | Database-backed job queue |
| Auth | Managed identity provider with MFA and role claims | Self-hosted, only if the engineer has done it before |
| AI drafting | Claude API through a server-side service, with prompt and model version logged, and no participant identifiers sent | Other models if the Phase 0.7 review requires it |
| Email | Transactional email provider with AU or documented data handling | Same |
| Monitoring | Error tracking and uptime alerts, with no participant data in logs | Same |

Principles:
- Rule packs are data, versioned by financial year and rule set. Never hard-code a price or a deadline.
- Keep the AI feature behind a single service boundary, so it can be turned off or swapped without touching the register logic.
- Infrastructure as code from day one, so the AU region and backups are reproducible.

## 8. Workstreams and quality gates

| Workstream | Gate |
|---|---|
| Rules and content | Rule tables signed off in writing before build. Tested against a second reader |
| Legal | Gates 1 to 3 in PRD section 9 before pilot |
| Security and privacy | Threat model before Sprint 2. Penetration test before pilot. Data mapping of all personal information |
| Accessibility | WCAG 2.2 AA review in Sprint 4, and a screen-reader test on the wizard and incident form |
| Testing | Unit tests for all rule logic (deadlines, business days, portal boundary, expiry thresholds). Integration tests for role permissions. End-to-end test for the incident path |
| Release | Feature flags for AI drafts and price lookup, so either can be turned off in production |

## 9. Risk register (top 8)

| # | Risk | Likelihood | Impact | Response | Owner |
|---|---|---|---|---|---|
| R1 | Rule table is wrong (deadline, portal or Practice Standards mapping) | Medium | High | Written sign-off, second reader, test cases from the official text, rule version per assessment | Advisor |
| R2 | AI draft policy causes harm or is relied on without review | Medium | High | Human approval gate, "AI draft" labels, legal review of prompts, logging | You |
| R3 | Price data cannot be displayed in a SaaS product | Medium | Medium | Confirm in 0.5. Fallback: show the source reference and effective date only, not the price | You |
| R4 | Claim channel does not allow third-party submission | High | Medium | Remove claim export from v1 (already out of scope). Keep it in Phase 2 only if 0.5 is positive | You |
| R5 | Participant data breach | Low | High | Data minimisation, encryption, access logs, tested incident response plan, penetration test | Engineer |
| R6 | Sales cycle longer than runway | Medium | High | Phase 0 pilot commitments; price the pilot to get signed; keep build team small | You |
| R7 | Name or domain conflict | Low | Medium | Task 0.6 before brand spend | You |
| R8 | Scope creep into claims, rostering or clinical notes | High | Medium | Written out-of-scope list (scope 4.2). New requests go to the Phase 3 list, not Phase 1 | You |

## 10. First two weeks (actions to start now)

Week 1:
1. Confirm decisions D1 to D7 in writing (a short reply is enough for each).
2. Book the 10 provider interviews (task 0.1). Draft the interview script from PRD section 3.
3. Send the legal scoping brief (task 0.3) using the open questions in PRD section 8.
4. Start the trademark and domain check (task 0.6).

Week 2:
5. Build the landing page and pilot form (task 0.2).
6. Run the first 3 interviews. Update the personas in PRD section 3.
7. Request the Commission's current incident guidance review (task 0.4) and the NDIA claim channel answer (task 0.5).
8. Shortlist the engineer or contractor (role in section 6).

Review point: end of week 4. Go or no-go against the Phase 0 exit gate.

## 11. Open items this plan does not resolve

- Budget and runway (not in the brief). The plan needs a cost estimate before the engineer is hired.
- Whether you will be the day-to-day product owner or hand that to someone else.
- Whether the Ozzieai.com.au brand is the parent company or the product brand (decision D7).
