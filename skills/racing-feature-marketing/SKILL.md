---
name: racing-feature-marketing
description: >
  Write product marketing copy (email + in-app messages) for a FanDuel Racing feature
  and publish it to Confluence. Use this skill whenever the user wants to write marketing
  copy, draft comms, create email or in-app messages, announce a feature to users, or
  generate messaging for a launch. Triggers on phrases like "write copy for", "draft
  email for", "in-app message for", "marketing copy for", "feature announcement",
  "comms for", or "create messaging for". Always use this skill when the user is working
  on a FanDuel Racing feature and wants to communicate it to users — even if they don't
  say "marketing" explicitly.
---

# FanDuel Racing — Feature Marketing Copy

This skill gathers feature context from the user, generates email and in-app marketing
copy in two variants each, then publishes everything to Confluence under a new page in
the FDR Transformational Work section.

**Audience for the copy**: FanDuel Racing users — younger, tech-savvy, semi-frequent
players. Confident bettors who want speed and signal, not fluff.

**Voice**: Time-sensitive, confident, outcome-oriented. Horse racing is about the moment —
write like the gates are about to open.

---

## Org & API Constants

- **Cloud ID**: `fanduel.atlassian.net`
- **Confluence Space**: Racing Product — space key `RP`
- **Confluence Parent Page**: Marketing Copy — page ID `311817110081` (child of FDR Transformational Work)
- **Confluence MCP tool**: `mcp__305f2946-a092-4ddc-9700-bfcff2f14313__createConfluencePage`
- **Content format**: `html`

---

## Step 1 — Gather Inputs

Ask the user for the following. Ask all at once in a single message — don't drip-feed
questions one at a time.

**Required:**
- **Feature name** — what is it called?
- **What it does** — 1-2 sentences describing the feature and the problem it solves
- **How users interact with it** — the specific action: tap X, navigate to Y, swipe to Z
- **FPDISCO ticket URL** — for linking in the Confluence page

**Optional (ask, but proceed without if not provided):**
- Any specific audience segment or timing context for this launch

---

## Step 2 — Generate Copy

Produce 4 pieces of copy. Present all 4 in chat for the user to review before publishing.

### Copy Rules
- **Lead with the benefit, not the feature name.** The user cares what they gain, not
  what it's called.
- **One primary action per message.** Every piece ends with a single clear CTA.
- **In-app should be noticeably shorter and punchier than email.** Email can breathe a
  little; in-app should be tight enough to read at a glance.
- **Variant A — Baseline**: Clear, direct, benefit-first. The message that can't miss.
- **Variant B — Creative**: Same value prop, but with a sharper angle, unexpected hook,
  or more evocative framing. Takes a small creative risk.

### Output Format (show in chat)

```
## Email

### Variant A — Baseline
**Subject:** [subject line]

[body]

[CTA]

---

### Variant B — Creative
**Subject:** [subject line]

[body]

[CTA]

---

## In-App Message

### Variant A — Baseline
**Subject:** [subject line]

[body — shorter/punchier than email]

[CTA]

---

### Variant B — Creative
**Subject:** [subject line]

[body — shorter/punchier than email]

[CTA]
```

After presenting the copy, ask: "Ready to publish to Confluence, or would you like to
adjust anything first?"

---

## Step 3 — Publish to Confluence

Once the user approves, create a single page directly under parent `310251095510`:

- **Title**: `[Feature Name] — Marketing Copy`
- **Parent ID**: `311817110081`
- **Content format**: `html`
- **Body**: use the HTML structure below — feature summary, FPDISCO link, date, then all 4 copy variants

### HTML Structure

```html
<div data-type="panel-info">
  <p><strong>Feature:</strong> [feature summary]</p>
  <p><strong>FPDISCO:</strong> <a href="[disco url]" data-card-appearance="inline">[disco url]</a></p>
  <p><strong>Generated:</strong> [today's date, e.g. July 14, 2026]</p>
</div>

<h2>Email</h2>

<h3>Variant A — Baseline</h3>
<p><strong>Subject:</strong> [subject]</p>
[body paragraphs as <p> tags]
<p><em>[CTA]</em></p>

<hr/>

<h3>Variant B — Creative</h3>
<p><strong>Subject:</strong> [subject]</p>
[body paragraphs as <p> tags]
<p><em>[CTA]</em></p>

<h2>In-App Message</h2>

<h3>Variant A — Baseline</h3>
<p><strong>Subject:</strong> [subject]</p>
[body as <p> tags]
<p><em>[CTA]</em></p>

<hr/>

<h3>Variant B — Creative</h3>
<p><strong>Subject:</strong> [subject]</p>
[body as <p> tags]
<p><em>[CTA]</em></p>
```

---

## Step 4 — Confirm

After the page is created, share its Confluence URL with the user.
