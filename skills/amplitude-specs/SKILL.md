---
name: amplitude-specs
description: >
  Generate complete Amplitude event tracking specifications for new FanDuel Racing features.
  Use this skill whenever the user wants to write, draft, or generate Amplitude event specs,
  analytics tracking specs, or event specifications for a FanDuel Racing feature — even if they
  just say "write specs for X", "amplitude spec", "tracking plan", "event spec", or describe
  a new racing feature and ask what events to track. Also triggers when the user shares a Figma
  link or screenshots and wants analytics coverage defined for a racing UI.
---

# Amplitude Specs — FanDuel Racing

You are generating a professional Amplitude event specification document for a new FanDuel Racing feature, following the exact format and conventions used across the existing Racing Amplitude Specifications in Confluence.

## Step 1 — Gather inputs

If the user hasn't already provided all of the following, ask for them now (you can ask in a single message):

- **Feature name** — short title (e.g. "Quick Picks", "Same Race Parlays in Lobby")
- **Feature description** — explain the intended user flows and interactions in enough detail to reason about what events to track
- **Figma URL** — link to the designs (optional but strongly encouraged)
- **Jira INIT ticket** — the INIT ticket link (optional)
- **PAI peer review ticket** — the specs sign-off ticket link (optional)
- **Is this a cross-sell (XS) feature?** — if yes, event names must be prefixed `FDR XS`
- **Screenshots** — if the user has already shared images in the conversation, use them

If the user has already provided all or most of these in their message, skip directly to Step 2.

## Step 2 — Load reference examples from Confluence

Before drafting the spec, fetch 2 of the following existing spec pages from Confluence to ground yourself in the exact format, event naming conventions, and property patterns. Use `mcp__305f2946-a092-4ddc-9700-bfcff2f14313__getConfluencePage` with `cloudId: fanduel.atlassian.net` and `contentFormat: markdown`.

| Page ID | Feature |
|---|---|
| `309352759542` | Same Race Parlays in Lobby |
| `309435957404` | Home Page |
| `308223672706` | FDR Amplitude Specifications - Parity Feature: My Bets |

Fetch them in parallel. You don't need to show the user these pages — they are purely for your reference.

## Step 3 — Draft the spec

Generate the full spec document. Follow these rules precisely:

### Document structure (use this exact order and heading hierarchy)

```
[JIRA table]

### Designs
[figma link]

---

### Analytics Outcomes

The goal of tracking [feature name] is to:

- [outcome 1]
- [outcome 2]
- [outcome 3]

---

### Events & Properties Specifications

Please ensure events inherit [global properties](https://fanduel.atlassian.net/wiki/spaces/FAW/pages/307779174499).

_A reminder that the below are specifications - not recommendations - that are then translated to the Amplitude tracking plan. It is important these are exactly followed. Not following these, or adding anything additional, will likely result in not being added to the tracking plan._

[events table]

---

### Property Descriptions

[property descriptions table]

---
```

### JIRA table format

| **JIRA** | **Ticket** |
|---|---|
| **INIT** | [jira link or TBD] |
| **Specs Peer Review Sign-Off** **Do not build until peer reviewed** | [pai link or TBD] |

### Events & Properties table format

| **User Action** | **Dev Ask** | **Event Name** | **Properties** |
|---|---|---|---|

- **User Action**: plain English description of the user gesture or system trigger (e.g. "User views the Quick Picks module", "User selects a horse")
- **Dev Ask**: one of exactly three values:
  - `New Event`
  - `Existing event. Ensure this event is triggered and respective properties are amended`
  - `New global property`
- **Event Name**: Title Case with spaces, wrapped in backticks (e.g. `` `Quick Pick Horse Selected` ``)
- **Properties**: one property per line, format `PropertyName:<description or allowed values>`. Always include `Module` as the first property with a snake_case value. Use `<angle brackets>` for dynamic values. Use `"quoted strings"` for fixed enumerated values.

### Property Descriptions table format

| **Property Name** | **Description** | **Notes** |
|---|---|---|

### Cross-sell (XS) events

If this is an XS feature, prefix every new event name with `FDR XS ` (e.g. `` `FDR XS Quick Pick Horse Selected` ``).

### Thinking about which events to include

A good spec covers:
1. **Page/module viewed** — a view event when the feature/section is first seen
2. **Primary interactions** — the key taps/clicks that drive the feature's purpose (selecting, toggling, submitting)
3. **Conversion moments** — any action that leads to a bet being placed (Add To Betslip, Bet Submitted, Bet Confirmed, Bet Success); for these, use "Existing event" Dev Ask and note only the properties that differ
4. **Edge cases** — errors, empty states, dismissals if they are analytically interesting

Don't over-specify. A focused set of events that answers the Analytics Outcomes is better than exhaustive coverage of every pixel.

### Analytics Outcomes

Write 3–4 concise bullet points that explain the *business purpose* of the tracking — what decisions the data will inform. Look at the feature description and ask: what would a PM want to measure? Examples:
- Engagement rate with the module
- Conversion from view → bet placement
- Which selections or configurations are most popular
- How the feature drives traffic to downstream pages

### Global properties reminder

All events inherit global properties automatically (Page Path, Product, Page Name, Balance, Site Version, Site Platform, Jurisdiction, Site Device Type, Site Device Family, Android Distribution Method, App Version). Do **not** list these in the Properties column unless a spec explicitly amends them.

## Step 4 — Present the spec

Display the full spec as a clean Markdown document in the conversation. Then ask:

> "Would you like me to publish this as a Confluence page under [Racing Amplitude Specifications](https://fanduel.atlassian.net/wiki/spaces/FAW/pages/308223607933)?"

## Step 5 — Publish to Confluence (if requested)

If the user says yes, use `mcp__305f2946-a092-4ddc-9700-bfcff2f14313__createConfluencePage` to create the page with:

- `cloudId`: `fanduel.atlassian.net`
- `spaceKey`: `FAW`
- `parentId`: `308223607933`
- `title`: `FDR Amplitude Specifications - [Feature Name]`
- `contentFormat`: `html`
- Convert the Markdown spec to clean Confluence-compatible HTML before publishing. Use standard HTML tables (`<table>`, `<tr>`, `<th>`, `<td>`), headings (`<h3>`), and lists (`<ul>`, `<li>`). Wrap code/event names in `<code>` tags.

After publishing, share the direct Confluence page link with the user.
