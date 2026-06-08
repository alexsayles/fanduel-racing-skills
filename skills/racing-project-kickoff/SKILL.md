---
name: racing-project-kickoff
description: >
  Kick off a new FanDuel Racing product initiative by creating the full Jira ticket set —
  Discovery (FPDISCO), Program (PONY), Initiative (INITRACING), and Design (UXDFLY) —
  wired together with the correct link types. Use this skill whenever the user wants to
  start a new discovery, create a discovery ticket, kick off a racing project, set up
  project tickets, spin up a new initiative, or begins describing a new racing feature
  idea they want to track in Jira. Also triggers when user says "new racing initiative",
  "kick off a project", "create a disco ticket", "start discovery on X", or similar.
  This skill handles the entire intake interview, ticket drafting, and Jira creation in
  one guided flow — always creates the full ticket set including skeleton INIT and Design
  tickets even when details are not finalized yet.
---

# Racing Project Kickoff

This skill guides you through creating a properly structured Jira ticket set for a new
FanDuel Racing initiative. It interviews the user, drafts ticket content, confirms before
creating anything, then creates and links all tickets.

**Always create all four ticket types** — FPDISCO, PONY, INITRACING, and UXDFLY. If
information is not available yet for INITRACING or UXDFLY, create them as clearly-marked
skeletons with [TBD] placeholders. Skeleton tickets are valuable: they reserve space in
the backlog, get the right team's attention early, and can be filled in as discovery
progresses. Never skip a ticket type because details are missing.

## Org & API Constants

- **Cloud ID**: `0bf6c0ec-bd17-4624-a17b-ec7588e91223`
- **Assignee** (default): `6421d06e5534b0bf74426fc5` (Alex Sayles)
- **FPDISCO** project key: `FPDISCO`, issue type `Idea` (id `12917`)
- **PONY** project key: `PONY`, issue type `Program` (id `11350`)
- **INITRACING** project key: `INITRACING`, issue type `Initiative` (id `11111`)
- **UXDFLY** project key: `UXDFLY`, issue type `Design Story` (id `11539`)
- **Link type IDs**:
  - `10613` — Genealogy: outward = "Parent of", inward = "Child of"
  - `11644` — Action item: outward = "has action item", inward = "action item from"

## Ticket Hierarchy & Link Types

```
PONY-XX (Program)
  └─[Genealogy: Parent of]──► FPDISCO-XXX (Discovery / Idea)
                                    ├─[Action item]──► INITRACING-XXXX (Initiative)
                                    │                       └─[Action item]──► UXDFLY-XXX (Design Story)
                                    ├─[Action item]──► UXDFLY-XXX (Design Story)
                                    └─[Action item]──► FNVPAX-XXX (Analytics — if exists)
```

---

## Phase 1 — Discovery Ticket Intake

Ask these questions conversationally — group related ones, move naturally. You need
enough to write all four tickets, including skeletons for INIT and Design.

### Core concept (ask first)
1. What is the working title of this feature?
2. Which workstream?
   - **Handicapping** — helping users analyze races and make better picks
   - **Wagering** — improving how users place and manage bets
   - **Watching** — video, replays, live feeds, content
   - **Platform** — infrastructure, cross-cutting, tooling

### Problem & motivation
3. What is the customer pain point? Who is the target user (casual / core / med+)?
4. Why now? Competitive signal, research finding, or strategic priority?

### Solution direction
5. High-level solution you are envisioning?
6. Do you have a prototype, Figma, or workshop notes? (Optional — can add later, use TBD)

### Success
7. What does success look like? Target metrics?
   - Examples: bet conversion lift, replay %, time to bet, adoption rate
8. Key open questions or hypotheses discovery needs to answer?

### Scope & sizing
9. Anything explicitly out of scope?
10. Rough size estimate?
    - Design: S (1 sprint) / M (2-3 sprints) / L (4+ sprints)
    - Tech: S / M / L / Needs spike

### Program linkage
11. Which PONY program does this roll up to? Ask if they know the key (e.g. PONY-80),
    or search with: `project = PONY AND issuetype = Program ORDER BY created DESC`
    Offer to create a new PONY ticket if this does not fit an existing program.

---

## Phase 2 — Confirm & Create

Show the user a summary of all four tickets before creating anything:

```
About to create:
  1. PONY-new   — "[summary]"  (or link to existing PONY-XX)
  2. FPDISCO-new — "[summary]"
  3. INITRACING-new — "[summary]" ⚠️ Skeleton — details TBD
  4. UXDFLY-new — "Design: [summary]" ⚠️ Skeleton — awaiting PM confirmation

Links:
  • PONY-XX  [Parent of] → FPDISCO-new
  • FPDISCO-new [has action item] → INITRACING-new
  • FPDISCO-new [has action item] → UXDFLY-new
  • FPDISCO-new [has action item] → FNVPAX-new  (if ticket exists)
  • INITRACING-new [has action item] → UXDFLY-new

Confirm? (yes / make changes)
```

Wait for explicit confirmation before calling any Jira APIs.

---

## Phase 3 — Create Tickets & Links

Create in this order so each key is available for linking:

### 1. Create PONY (if new)
```
project: PONY
issuetype id: 11350
summary: [program name]
description: [one paragraph — what this program organizes, strategic goal,
             what types of discovery tickets will live under it]
assignee: 6421d06e5534b0bf74426fc5
```

### 2. Create FPDISCO (Discovery)
```
project: FPDISCO
issuetype id: 12917  ← CRITICAL: must be Idea, not Story/Task/Epic
assignee: 6421d06e5534b0bf74426fc5
```

FPDISCO description template:
```
## Background
[why now, competitive context, strategic fit]

## Customer Problem / Pain Point
[specific user need; note target user segment]

## Workstream
[Handicapping / Wagering / Watching / Platform]

## Solution Description
[high-level what we're building]

## Goal & Target Metrics
- Primary: [metric]
- Secondary: [metric]

## Hypotheses / Open Questions
[questions discovery needs to answer]

## Prototype / Design
[link, or TBD]

## Out of Scope
[items, or TBD]
```

### 3. Create INITRACING (Initiative — always, as skeleton if needed)
```
project: INITRACING
issuetype id: 11111
assignee: 6421d06e5534b0bf74426fc5
```

INITRACING description template:
```
## Overview
[feature description — reuse FPDISCO Overview; expand if spec detail is known]

## Customer Problem / Pain Point
[refined from discovery, or TBD]

## Solution Description
[more concrete than FPDISCO — specific interactions, data sources if known, or TBD]

## Expected Behavior
[TBD — to be defined as discovery progresses]

## Discovery Reference
FPDISCO-[XXX]
```

### 4. Create UXDFLY (Design — always, as skeleton)
```
project: UXDFLY
issuetype id: 11539  (Design Story)
summary: Design: [feature name]
assignee: leave unassigned
```

UXDFLY description template:
```
## ⚠️ SKELETON — Awaiting design team pickup

## Design Objectives
[2-3 sentences from the discovery brief]

## Key Constraints
- Must not interfere with primary betting flow
- Mobile-first, with desktop consideration

## Discovery Reference
FPDISCO-[XXX]

## Initiative Reference
INITRACING-[XXXX]

## Next Steps for Design Team
1. Review discovery ticket and prototype (if available)
2. Confirm scope and requirements with PM (Alex Sayles)
3. Begin exploration and wireframing
```

### 5. Create Links

PONY → FPDISCO (Genealogy, PONY is parent):
- type id: 10613, outwardIssue: PONY-XX, inwardIssue: FPDISCO-XXX

FPDISCO → INITRACING (Action item):
- type id: 11644, inwardIssue: FPDISCO-XXX, outwardIssue: INITRACING-XXXX

FPDISCO → UXDFLY (Action item):
- type id: 11644, inwardIssue: FPDISCO-XXX, outwardIssue: UXDFLY-XXX

FPDISCO → FNVPAX (Action item — only if FNVPAX ticket already exists):
- type id: 11644, inwardIssue: FPDISCO-XXX, outwardIssue: FNVPAX-XXX
- If no FNVPAX ticket exists yet, skip this link and note it in the Phase 4 summary

INITRACING → UXDFLY (Action item):
- type id: 11644, inwardIssue: INITRACING-XXXX, outwardIssue: UXDFLY-XXX

If unsure about link direction, fetch PONY-80 with fields=["issuelinks"] as reference.

---

## Phase 4 — Summary

After all tickets are created and linked, output:

```
✅ Tickets created:

  PONY-XX    [Program name]
             https://fanduel.atlassian.net/browse/PONY-XX

  FPDISCO-XXX  [Feature Name]
               https://fanduel.atlassian.net/browse/FPDISCO-XXX

  INITRACING-XXXX  [Feature Name]  ⚠️ Skeleton
                   https://fanduel.atlassian.net/browse/INITRACING-XXXX

  UXDFLY-XXX  Design: [Feature Name]  ⚠️ Skeleton
              https://fanduel.atlassian.net/browse/UXDFLY-XXX

Links wired:
  PONY-XX [Parent of] FPDISCO-XXX
  FPDISCO-XXX [has action item] INITRACING-XXXX
  FPDISCO-XXX [has action item] UXDFLY-XXX
  FPDISCO-XXX [has action item] FNVPAX-XXX  (or "⚠️ Skipped — FNVPAX ticket not yet created")
  INITRACING-XXXX [has action item] UXDFLY-XXX

Next steps:
  • Fill in INITRACING Expected Behavior as discovery progresses
  • Design team to pick up UXDFLY-XXX once initiative is scoped
  • Analytics: create FNVPAX experiment ticket once design is underway, then link to FPDISCO-XXX
```

Then ask:

```
Would you also like to build a business case for this feature?
Running /racing-business-case will draft a structured business case and publish it
to Confluence under FDR Transformational Work, linked back to FPDISCO-XXX.
(yes / no)
```

If yes, invoke the `racing-business-case` skill, passing the newly created FPDISCO ticket key as context so it skips the ticket lookup step.
