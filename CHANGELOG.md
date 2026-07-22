# Changelog

## v1.0.1

### Changed

- **Core principle** rewritten from "avoid BUILD" to five-component
  long-term business value framing: Reliability, Strategic value,
  Adaptability, Total cost of ownership, Speed to value.
- **Tier order is now a search order**, not a preference order. No tier is
  inherently best. Your situation determines the right tier.
- **Verdict renamed to Recommendation.** The recommendation addresses a
  senior engineer and gives them everything they must know to accept or
  reject with confidence.
- **Evidence matrix columns** replaced: Popularity/Maintenance/License/Effort
  → Reliability/Strategic value/Adaptability/TCO/Speed to value.
- **All prose rewritten in Simplified Technical English.** Sentences under
  20 words. Active voice. Common words. "Must" and "must not" replace
  "should," "might," and hedges.
- **README rewritten** to reflect the business-value framing. Prior-art
  section expanded with differentiation from enterprise tools.

### Added

- **Establish context first** — six questions before the framework runs:
  time horizon, scale, failure cost, team capability, commodity or core,
  volatility. Plus a Constraints line.
- **Commodity or core competency** test: "If a buyer knew we built it
  ourselves, would they care?"
- **Long-term value assessment** section — merged TCO, strategic
  differentiation, and reliability assessment with five subsections.
- **Compound recommendations** — split a request into commodity and
  differentiated slices with separate tier recommendations.
- **Strict citation format** — `web_search`, `web_fetch`, `grep`, `read`,
  `shell`, `unavailable`. Citations without exact query/URL/path do not
  count.
- **AI verdict mapping** — local model = USE, paid API = INTEGRATE,
  finished AI product = BUY, open-source AI framework = FORK.
- **Handle incomplete inputs** — if context cannot be answered, ask.
  Never fabricate.
- **What to do next** — proposal, testable increment, re-evaluation date.
- **The good habit** — reflection questions after each recommendation and
  before the next similar decision.
- **When NOT to use** expanded with style/lint changes.
- **Two embedded examples** — commodity-leaning (auth, compound USE+BUILD)
  and core-competency (matching, BUILD+INTEGRATE).
- **tests/scenarios.md** — eight scenario tests for the framework.
- **GitHub Issues link** in README.

### Migration

- The skill frontmatter `version` field changes from `"1.0.0"` to
  `"1.0.1"`. Reinstall the skill to get the updated prompt.
- Agent platforms that embed the old prompt must replace it with the
  v1.0.1 agent file. The permission block did not change.
- Old phrases to remove from any derived documents: "BUILD is the last
  resort," "BUILD is the last choice." Replace with: "BUILD is viable when no
  earlier tier fits. Cite the search."
- The old evidence matrix columns (Popularity, Maintenance, License, Effort)
  no longer appear. Replace matrix headers with the five components.
