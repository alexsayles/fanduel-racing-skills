# Business Case Template

Use this template when drafting and publishing the business case.
Populate every section — mark unknowns as `TBD — [what's needed]`, never leave a section blank.

---

## Chat Draft Format (show user before publishing)

```
# Business Case: [Feature Name]

**FPDISCO**: [FPDISCO-XXX]

---

## The Opportunity
[2–3 sentences. What is the feature and why does it matter right now?
Lead with the business hook — revenue, competitive pressure, or user pain at scale.]

## Customer Problem
[Specific, quantified if possible. Who is affected (casual / core / med+)?
What data or research supports this? e.g. "23% of core bettors drop off at X step (session analysis, Q3 2024)"]

## Revenue Impact
| Scenario | Method | Estimate |
|---|---|---|
| Conservative | [e.g. 1% lift on bet conversion × $X handle] | $[X]K/yr [est.] |
| Base case | [method] | $[X]K/yr [est.] |
| Optimistic | [method] | $[X]K/yr [est.] |

Cost of not building: [revenue at risk, competitive exposure, or "not quantified"]

## Strategic Alignment
**OKR / Pillar**: [e.g. "Grow core bettor engagement — increase avg bets/session"]
**Time sensitivity**: [deadline, competitive trigger, or "none identified"]

## Success Metrics
| Metric | Baseline | Target | Timeframe |
|---|---|---|---|
| [Primary KPI] | [X%] | [Y%] | [e.g. 90 days post-launch] |
| [Secondary KPI] | [X] | [Y] | [timeframe] |

**Guardrails** (must not regress): [e.g. checkout abandonment rate, page load time]

## Sizing
- **Design**: [S / M / L] (~[X] sprints)
- **Tech**: [S / M / L / Needs spike]

## Open Questions
- [Question 1 — what needs to be answered in discovery]
- [Question 2]
```

---

## Confluence HTML Structure

When publishing, use this HTML. Replace `[PLACEHOLDERS]` with real content.

```html
<h1>Business Case: [FEATURE NAME]</h1>

<p>
  <strong>FPDISCO:</strong> <a href="https://fanduel.atlassian.net/browse/[FPDISCO-XXX]">[FPDISCO-XXX]</a>
</p>

<hr/>

<h2>The Opportunity</h2>
<p>[2–3 sentence hook. Business value first.]</p>

<h2>Customer Problem</h2>
<p>[Specific, quantified pain point. Cite data source if available.]</p>

<h2>Revenue Impact</h2>
<table>
  <thead>
    <tr><th>Scenario</th><th>Method</th><th>Estimate</th></tr>
  </thead>
  <tbody>
    <tr><td>Conservative</td><td>[method]</td><td>$[X]K/yr [est.]</td></tr>
    <tr><td>Base case</td><td>[method]</td><td>$[X]K/yr [est.]</td></tr>
    <tr><td>Optimistic</td><td>[method]</td><td>$[X]K/yr [est.]</td></tr>
  </tbody>
</table>
<p><strong>Cost of not building:</strong> [risk or "not quantified"]</p>

<h2>Strategic Alignment</h2>
<p><strong>OKR / Pillar:</strong> [OKR]<br/>
<strong>Time sensitivity:</strong> [deadline or trigger]</p>

<h2>Success Metrics</h2>
<table>
  <thead>
    <tr><th>Metric</th><th>Baseline</th><th>Target</th><th>Timeframe</th></tr>
  </thead>
  <tbody>
    <tr><td>[Primary KPI]</td><td>[X%]</td><td>[Y%]</td><td>[timeframe]</td></tr>
    <tr><td>[Secondary KPI]</td><td>[X]</td><td>[Y]</td><td>[timeframe]</td></tr>
  </tbody>
</table>
<p><strong>Guardrails:</strong> [must-not-regress metrics]</p>

<h2>Sizing</h2>
<ul>
  <li><strong>Design:</strong> [S/M/L] (~[X] sprints)</li>
  <li><strong>Tech:</strong> [S/M/L/Needs spike]</li>
</ul>

<h2>Open Questions</h2>
<ul>
  <li>[Question 1]</li>
  <li>[Question 2]</li>
</ul>
```

---

## Drafting Notes

- **"The Opportunity" section** is the most important — write it last, after all data is in.
  It should answer: *why this, why now, how big*.
- **Revenue table**: always show the method alongside the number. A number without a method
  is not credible. Mark estimates `[est.]` — don't hide uncertainty.
- **Guardrail metrics** are easy to forget but important for alignment. Always ask.
- **Open Questions** should be things that are genuinely unresolved, not rhetorical. If
  discovery has already answered something, don't list it.
