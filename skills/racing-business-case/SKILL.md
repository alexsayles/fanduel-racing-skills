---
name: racing-business-case
description: >
  Build a structured business case for a new FanDuel Racing feature and publish it as a
  Confluence page linked back to the FPDISCO discovery ticket. Use this skill whenever
  the user wants to write a business case, build justification for a feature, create a
  case for prioritization, document why a feature should be built, or frame a feature
  opportunity for PM alignment or internal review. Also triggers on phrases like "business
  case for X", "make a case for this feature", "write up the opportunity", "justify this
  feature", "prioritization doc", or "why should we build X". Always use this skill when
  the user references a FPDISCO ticket and wants to go deeper on value, revenue impact,
  or strategic alignment — even if they don't use the words "business case" explicitly.
---

# FanDuel Racing — Business Case Builder

This skill interviews the user, pulls context from an existing FPDISCO ticket, drafts a
structured business case, confirms it, then publishes it as a Confluence page linked to
the FPDISCO.

**Audience**: Internal team / PM alignment (not exec-facing — direct, specific, no fluff)  
**Tone**: Clear and analytical. Real data over vague claims. Acknowledge uncertainty honestly.

---

## Org & API Constants

- **Cloud ID**: `0bf6c0ec-bd17-4624-a17b-ec7588e91223`
- **Confluence Space**: Racing Product — space key `RP`, space ID `307330777752`
- **Confluence Parent Page**: FDR Transformational Work — page ID `310251095510`
  - URL: https://fanduel.atlassian.net/wiki/spaces/RP/pages/310251095510/FDR+Transformational+Work
  - All business cases are published as child pages under this page
- **Default Assignee / Author**: Alex Sayles (`6421d06e5534b0bf74426fc5`)

---

## Phase 1 — Pull FPDISCO Context

Ask the user for the FPDISCO ticket key (e.g. `FPDISCO-142`). Then fetch it:

```
getJiraIssue(cloudId, issueIdOrKey: "FPDISCO-XXX", responseContentFormat: "markdown")
```

Extract and note:
- Feature name / summary
- Customer problem / pain point
- Workstream (Handicapping / Wagering / Watching / Platform)
- Solution description
- Goal & target metrics (if present)
- Sizing estimate (Design / Tech)
- Any hypotheses or open questions

If any of these are missing from the ticket, ask the user to fill them in before proceeding.

---

## Commercial KPI Knowledge Base

Read `references/kpis.md` before the interview. It contains current baselines you should
use to ground revenue estimates and provide context without asking the user for numbers
that are already known:

- Weekly handle & GGR by week (May 2026), with YoY and vs-plan deltas
- Platform split: FDR vs TVG handle, actives, and revenue
- Active user counts by state group and platform
- SBK cross-play cohort metrics (AHPU, ARPU, cross-play rate)
- NTG / x-sell activation trends
- Triple Crown event benchmarks
- Pre-calculated impact rules (e.g. "1% FDR handle lift ≈ $8–9M/year")

Use this data proactively. For example: if a feature targets SBK cross-sell, reference
the 1–2% baseline cross-play rate and ~$350 AHPU for that cohort. If a feature targets
new users, flag the -50% to -63% YoY NTG decline as the strategic context.

---

## Phase 2 — Business Case Interview

Ask only for information **not already in the FPDISCO ticket**. Group questions naturally and keep it conversational. You need answers to these:

### Revenue & Financial Impact
1. What is the estimated revenue opportunity? (e.g. bet conversion lift × handle, new
   user revenue, reduced churn value)
   - Ask for the *method* they used to estimate (e.g. "X% lift on Y metric × Z handle")
   - If they have a range, capture both optimistic and conservative
2. Is there a cost or investment required? (eng time, tooling, licensing)
3. Any revenue risk of *not* building this? (competitive loss, churn signal)

### Strategic Alignment
4. Which FanDuel Racing OKR or strategic pillar does this support?
   - Examples: Grow core bettor engagement, Increase new user activation, Improve
     product differentiation vs. TVG/DK Horse
5. Is there a deadline or time-sensitivity? (seasonal racing calendar, competitor move,
   research expiry)

### Success Metrics / KPIs
6. What is the *primary* success metric and its current baseline?
   - e.g. "Bet conversion rate — currently 18% on race card page"
7. What is the target lift and over what timeframe?
8. Any guardrail metrics (things that must not regress)?

### Problem Statement Depth (if thin in FPDISCO)
9. Do you have user research, session data, or customer feedback that quantifies the pain?
   - e.g. "X% of users drop off at step Y", "NPS feedback theme Z"

---

## Phase 3 — Draft the Business Case

Write the business case using the template in `references/template.md`. Populate every
section with real data from the FPDISCO ticket + interview answers.

**Key drafting rules:**
- Lead each section with the *so what*, not the background
- Use specific numbers wherever possible; flag estimates explicitly as `[est.]`
- Keep the whole doc under 600 words — this is an alignment doc, not a dissertation
- Do not invent data; if something is unknown, write "TBD — [what's needed to fill this]"

Read `references/template.md` now before drafting.

---

## Phase 4 — Confirm Before Publishing

Show the user the full draft in chat and ask:

```
Does this look right? Any changes before I publish to Confluence?
(yes / make changes)
```

Wait for explicit confirmation. Do not create the Confluence page until confirmed.

---

## Phase 5 — Publish to Confluence

### 5a. Confluence destination (pre-resolved — no search needed)

Publish directly to:
- **Space**: Racing Product (`RP`, ID `307330777752`)
- **Parent page**: FDR Transformational Work (ID `310251095510`)

### 5b. Create the Confluence page

```
createConfluencePage(
  cloudId: "0bf6c0ec-bd17-4624-a17b-ec7588e91223",
  spaceId: "307330777752",
  parentId: "310251095510",
  title: "Business Case: [Feature Name]",
  contentFormat: "html",
  body: [rendered HTML from template]
)
```

Use `contentFormat: "html"` for rich formatting (tables, headings, callout panels).
See `references/template.md` for the HTML structure to use.

### 5d. Link Confluence page back to FPDISCO

Add a remote link on the FPDISCO ticket pointing to the new Confluence page:
```
addCommentToJiraIssue(
  cloudId,
  issueIdOrKey: "FPDISCO-XXX",
  body: "📄 Business case published: [Confluence page URL]"
)
```

Also edit the FPDISCO ticket description to add the Confluence URL under a
`## Business Case` heading if one doesn't already exist.

---

## Phase 6 — Summary

Output:

```
✅ Business case published

  Feature: [Feature Name]
  Confluence: https://fanduel.atlassian.net/wiki/...
  FPDISCO: https://fanduel.atlassian.net/browse/FPDISCO-XXX (updated with link)

Key numbers captured:
  • Revenue opportunity: [X]
  • Primary KPI: [metric] — current [X]%, target [Y]%
  • Strategic pillar: [OKR]

Next steps:
  • Share Confluence link with stakeholders for async review
  • Update estimates as discovery progresses
  • Reference this doc when creating INITRACING scope
```
