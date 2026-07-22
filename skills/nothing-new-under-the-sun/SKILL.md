---
name: nothing-new-under-the-sun
description: >
  Research-first scouting agent skill that runs BEFORE any build decision,
  new dependency, new system, or feature request. Search existing solutions
  (codebase, dependencies, packages, GitHub repos, APIs, SaaS, templates)
  before writing code. Output a REUSE / USE / FORK / BUY / INTEGRATE / BUILD
  recommendation with an evidence matrix. Uses five-component long-term
  business value framing. Trigger when someone proposes a new feature, asks
  to add a dependency, says "build X", "add X", "we need X", or any time
  greenfield code is considered.
license: MIT
metadata:
  author: fahrellgiovanny
  version: "1.0.1"
---

# There Is Nothing New Under The Sun

## Core principle

Every tier decision must maximize long-term business value. Use five
components:

1. **Reliability** — will it keep working under real load and failure modes?
2. **Strategic value** — does owning it create competitive protection or
   unique customer benefit?
3. **Adaptability** — can it change as the business changes?
4. **Total cost of ownership** — build, run, and replace costs over its life.
5. **Speed to value** — how soon does the business benefit?

No tier is inherently best. The tier order — REUSE → USE → FORK → BUY →
INTEGRATE → BUILD — is a search order, not a preference order. Your
situation determines which tier maximizes value.

Commodities weight TCO and speed. Core competencies weight strategic value
and adaptability. Reliability matters in every situation.

## When to use

- Someone proposes a new feature, system, helper, or module.
- Someone asks to add a dependency.
- Someone says "we need X", "build X", "add X", or "write a helper for X."
- An architecture decision needs evidence before committing to new code.
- Any request that would expand the surface area of existing code.

## When NOT to use

- Bug fixes inside existing files (no new system being proposed).
- Pure refactors that preserve behavior and dependencies.
- Content or data entry into existing modules.
- Routine edits where the module already exists.
- Style or lint changes.

## Establish context first

Before you search for candidates, answer these six questions. If any
question cannot be answered, ask the user before you continue.

1. **Time horizon** — how many years must this decision serve?
2. **Scale** — current load, projected peak load, and the point where the
   best answer would change.
3. **Failure cost** — what breaks if this fails? What is the business
   impact?
4. **Team capability** — does the team have the skill, time, and domain
   knowledge to build, maintain, and operate it?
5. **Commodity or core** — see next section.
6. **Volatility** — how fast does the strategy or technology change?

**Constraints** — any regulatory, security, or compliance requirements.

## Commodity or core competency

Use this test: *"If a buyer or user knew we built it ourselves, would they
care?"*

- **No = commodity.** Buyers do not care who built the PDF generator or the
  auth flow. They want the result. Let a seller handle it.
- **Yes = core competency.** Buyers choose your product because of the
  matching algorithm, the recommendation engine, or the latency you control.

Classify by the majority of value. Describe any differentiated slice
separately. A commodity system with one differentiated sub-component needs a
compound recommendation.

## Tier search (fair-search evidence)

Search in this order. Move to the next tier only when you find no viable
candidate.

1. **REUSE** — already in the repository or internally available.
2. **USE** — an existing dependency solves it.
3. **FORK** — an open-source project solves it. Vendor or fork.
4. **BUY** — a SaaS product solves it.
5. **INTEGRATE** — an API solves it.
6. **BUILD** — viable when no earlier tier fits. Cite the search.
7. **License** — check license compatibility at every step.

## Evidence matrix

For every candidate, fill one row with the five components.

| Candidate | Reliability | Strategic value | Adaptability | TCO | Speed to value |
|-----------|-------------|-----------------|--------------|-----|----------------|

Label undifferentiated commodity slices as "Neutral (commodity)" or "Zero
for commodity" in the strategic value column.

## Long-term value assessment

After you fill the matrix, assess each component.

### Reliability

Examine real load records, outage history, MTTR, and dependency maturity.
For existing products: cite uptime, incident history, and adoption at scale.
For BUILD: "Unknown" is a real risk.

### Strategic value

Core competencies earn high strategic value only from BUILD or FORK. USE
and BUY deliver near-zero strategic value for core work. Commodities earn
neutral or zero strategic value from all tiers. For commodities, the right
tier is the one with the best TCO and speed.

### Adaptability

Can the team change it? USE depends on upstream roadmaps. BUY depends on
vendor roadmaps. BUILD gives full control. FORK gives control after the
initial fork cost.

### Total cost of ownership

Include build, run, and replace costs over the time horizon. USE: annual
maintenance hours. BUY: subscription at projected scale. BUILD: initial
build hours plus annual maintenance. FORK: merge-cost estimate.

### Speed to value

Days (USE/BUY), weeks (INTEGRATE), months (BUILD), years (large BUILD).

## Recommendation

You are a senior engineer addressing another senior engineer. Give them
everything they must know to accept or reject with confidence.

The recommendation must cite the five components. It must include:

- The tier recommendation.
- Why this wins — one concrete reason per relevant component.
- Confidence (HIGH / MEDIUM / LOW).
- Re-evaluation cadence or trigger.
- Missing information, if any.

## Compound recommendations

When a request has a commodity slice and a differentiated slice, split the
recommendation:

```
Recommendation (compound): USE X for the commodity slice.
BUILD for the differentiator slice.
```

## AI verdict mapping

When the request involves an AI model:

| Form | Tier |
|------|------|
| Local model (self-hosted) | USE |
| Paid API | INTEGRATE |
| Finished AI product | BUY |
| Open-source AI framework | FORK |

## Handle incomplete inputs

If context questions cannot be answered, ask the user. Do not guess. If no
candidate exists after a full search, state that. Never fabricate a
candidate or a verdict.

## Citation format

Every claim must cite its source in this exact format:

```
web_search: "<exact query>" on <date>
web_fetch: <exact URL> on <date>
grep: <path>
read: <path>:<lines>
shell: <command>
unavailable: <reason>
```

Citations without the exact query, URL, or path do not count. If a search
channel is unavailable, record `unavailable: <reason>`.

## Agent versus skill

This prompt exists in two forms:

- **Skill** (this file) — loaded during normal sessions. Research runs
  before implementation. A BUILD recommendation unlocks code generation.
- **Agent** — a permission-bound definition that enforces read-only
  research. The agent cannot edit files, install packages, or run writes.
  Use when research must be auditable or the read-only boundary must be
  guaranteed.

## What to do next

1. Write a short proposal: the decision, the evidence, the re-evaluation
   trigger.
2. Plan the smallest testable increment: POC (BUY/INTEGRATE), a spike
   (REUSE/USE/FORK), or the smallest increment that proves technical risk
   (BUILD).
3. Set a re-evaluation date proportional to the time horizon.

## The good habit

Ask these questions right after the recommendation and before the next
similar decision:

1. Did I search wide enough?
2. Did confirmation bias steer me?
3. Which component actually decided this?
4. What could make this recommendation wrong in a year?

## Hard rules

- Never jump to BUILD without a documented search.
- Never recommend a dependency without checking its license.
- Flag copyleft and share-alike licenses for project-specific legal review.
- If a candidate is already in the repository, REUSE wins — do not propose a
  new dependency.
- If two candidates are roughly equal, prefer the one with the safer license
  and higher bus factor.
- Research must be read-only. Hard enforcement belongs in each host's
  permission or sandbox configuration.
- Report unavailable search channels instead of claiming complete coverage.
- Citations must use the exact format. Citations without the exact query,
  URL, or path do not count.
- Never expose local files, credentials, or private repository information.

## Examples

### Example A — commodity, compound recommendation

```
# Request
Should we build our own auth, or use Auth0?

# Context
- Time horizon: 5 years.
- Scale: 10k MAU now, 500k projected. Auth0 cost steepens above ~200k MAU.
- Failure cost: catastrophic.
- Team capability: strong web team; no identity engineer.
- Commodity or core: mostly commodity; enterprise SAML may be a
  differentiated slice.
- Volatility: medium.
- Constraints: SOC 2, GDPR, likely SAML for enterprise.

# Evidence matrix
| Candidate | Reliability                | Strategic value       | Adaptability      | TCO (5 yr)                | Speed to value |
|-----------|----------------------------|-----------------------|-------------------|---------------------------|----------------|
| next-auth | 5M weekly (npm 2026-07-22) | Neutral (commodity)   | Medium (adapters) | ~$0 + 40 hr/yr            | 1 week         |
| Auth0     | Billions/day (trust page)  | Weak                  | Medium (config)   | ~$25k/yr@10k MAU; scales  | 3 days         |
| BUILD     | Unknown                    | Zero for commodity    | High (unneeded)   | 2000 hr + 500 hr/yr       | 6+ months      |

# Recommendation (compound)
USE next-auth for the commodity slice. Small BUILD layer over next-auth
callbacks for enterprise SSO, only when the first enterprise customer
asks for it.

# Why this wins
- Reliability: next-auth proven at scale (5M weekly, no critical CVE in
  2 yr).
- Strategic value: engineering time saved goes to real product work.
- Adaptability: adapters cover passkeys, OAuth, SAML.
- TCO: near zero license; no per-MAU bill.
- Speed to value: one week to production.

# Confidence
MEDIUM. Re-evaluate at 100k MAU, first enterprise SSO request, or any
next-auth security incident.

# Missing information
Growth curve for cost projection; SSO timing.
```

### Example B — core competency, BUILD correct

```
# Request
Should a ride-hailing company build or buy its driver-rider matching
algorithm?

# Context
- Time horizon: 10 years.
- Scale: 500k drivers, 20M riders, ~1M requests/hour.
- Failure cost: catastrophic. Poor matching kills the marketplace.
- Team capability: existing operations research and ML team.
- Commodity or core: core competency. Matching quality IS the product.
- Volatility: high. Strategy evolves constantly.
- Constraints: regional pricing and worker-classification laws.

# Tier search (fair-search evidence)
- REUSE: none. Citation: grep "matching" in src/ — no application matching.
- USE: no npm package solves marketplace matching at scale.
  Citation: web_search "ride hailing matching npm" 2026-07-22 — no hits.
- FORK: no viable open source engine at scale.
  Citation: web_fetch github.com/topics/ride-hailing 2026-07-22 — toy
  projects only.
- BUY: no seller offers marketplace matching as a product.
  Citation: web_search "ride hailing matching vendor" 2026-07-22.
- INTEGRATE: routing APIs solve routing, not matching.
  Citation: web_fetch mapbox.com/directions-api 2026-07-22.
- BUILD: viable and expected for the industry.

# Recommendation (compound)
BUILD the matching engine. INTEGRATE routing and mapping APIs (commodities
where sellers offer proven products).

# Why this wins
- Reliability: BUILD carries unproven-code risk; every competitor faced
  the same risk. Reliability builds through iteration.
- Strategic value: matching IS the product. Only BUILD supplies this.
- Adaptability: BUILD gives full control; strategy changes weekly.
- TCO: high build cost; zero seller cost; no lock-in.
- Speed to value: 6-12 months for MVP; compounding gains over 10 years.

# Confidence
HIGH.

# Re-evaluation cadence
Yearly. Some sub-components (ETA prediction, geocoding) may commoditize.

# Missing information
None material.
```
