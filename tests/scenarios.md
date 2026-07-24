# Test scenarios — v1.1.0

These scenarios verify that the v1.1.0 framework behaves correctly.
Run each scenario against the skill and the agent variant.

---

## 1. Framing

**Input:** "Should we build our own rate limiter, or use express-rate-limit?"

**Passes if:** The recommendation names at least 3 of the 5 components with
concrete reasons. Example: "Reliability: express-rate-limit handles millions
of requests daily. TCO: zero cost, already in the project. Speed to value:
one line of config."

**Fail if:** The recommendation uses only one component, or uses generic
language like "this is better" without naming components.

---

## 2. Context first

**Input:** "Should we build our own email sending?"

**Passes if:** The response opens by establishing context — it asks about
time horizon, scale, failure cost, team capability, commodity/core
classification, and volatility. It does not search for candidates before
context is set.

**Fail if:** The response jumps to searching for email sending packages or
SaaS products before the context questions are answered.

---

## 3. Commodity rejection

**Input:** "Should we build our own PDF generation?"
Context: time horizon 3 years, 100k docs/month, medium failure cost,
strong team, commodity (buyers do not care who generates PDFs),
low volatility.

**Passes if:** PDF generation is classified as a commodity. BUILD is not
recommended or is ranked below USE/BUY. The strategic value column for
BUILD is marked "Zero for commodity" or equivalent.

**Fail if:** BUILD is recommended as the primary tier for PDF generation
as a commodity.

---

## 4. Core-competency BUILD

**Input:** "Ride-hailing company: build or buy matching algorithm?"
Context: time horizon 10 years, 500k drivers/20M riders, catastrophic
failure cost, existing ML team, core competency (would buyers care? yes),
high volatility.

**Passes if:** BUILD is taken seriously on strategic-value grounds. The
"would a buyer care?" test returns Yes. The recommendation discusses
why strategic value requires BUILD for core competencies.

**Fail if:** The framework treats BUILD as a last resort and pushes USE or
BUY despite the core-competency classification.

---

## 5. Spectrum (compound recommendation)

**Input:** "Should we build our own search?"
Context: time horizon 5 years, e-commerce platform, 10M products. Search
result ranking is a competitive differentiator (core). Text indexing and
retrieval are commodity.

**Passes if:** The recommendation splits into compound form: USE (or BUY)
for the commodity text-indexing slice, BUILD for the differentiated
ranking/personalization slice. Both tiers are named with reasoning.

**Fail if:** A single tier is recommended for the entire search system
without splitting commodity from differentiated slices.

---

## 6. Ambiguous input

**Input:** "Add search to our app."

**Passes if:** The response does not fabricate a recommendation. It asks:
what corpus, for whom, at what scale, what time horizon, what failure
cost, whether search is commodity or core. It does not search for
candidates until context is established.

**Fail if:** The response recommends Elasticsearch, Algolia, or another
candidate without first asking the context questions.

---

## 7. AI mapping

**Input:** "We need speech-to-text for our call center."
Context: time horizon 5 years, 10k calls/day, medium failure cost, ML team
available, commodity (transcription is not the product).

**Passes if:** The AI verdict mapping and its dual-tier decision rule are
applied correctly:
- Self-hosted Whisper run as an unmodified dependency maps to USE; a
  vendored or patched build (for example whisper.cpp with local changes)
  maps to FORK.
- OpenAI Whisper API maps to INTEGRATE.
- AssemblyAI maps to BUY.
The recommendation uses the correct tier labels, and for a two-tier row it
cites the copy/vendor/patch test to pick one.

**Fail if:** A self-hosted model is mapped to BUILD, a paid API is mapped
to BUILD instead of INTEGRATE, or a two-tier row is left unresolved.

---

## 8. Agent boundary

**Input:** Any build request, dispatched to the agent variant
(`agents/nothing-new-under-the-sun.md`).

**Passes if:** The agent refuses to write code, edit files, or install
packages. It says the permission block is host-dependent. If the
recommendation is BUILD, the agent hands the evidence to the caller and
does not implement.

**Fail if:** The agent attempts to create a file, run `npm install`,
execute `git clone`, or generate implementation code. The agent must
also not recommend `pnpm install` or `yarn add` as a research step.

---

## 9. Hard output schema

**Input:** "Should we build our own feature flag system?"
Context: time horizon 4 years, 200 services, high failure cost, strong
backend team, commodity with some experimentation needs, medium volatility.

**Passes if:** The response uses all required sections: Context, Tier
search, Evidence matrix, Recommendation, Why this wins, Confidence,
Re-evaluation trigger, and Missing information.

**Fail if:** The response gives only a paragraph, only a verdict, or a
matrix without the remaining required sections.

---

## 10. Trivial-work skip

**Input:** "Add `clsx` to this existing component. The project already uses
`clsx` elsewhere."

**Passes if:** The skill does not run the full framework. The response says
this is an import already in use or routine local work.

**Fail if:** The response creates a full build-vs-buy report for the import.

---

## 11. USE includes new normal dependencies

**Input:** "Should we add express-rate-limit for our Express API?"
Context: time horizon 2 years, 100k requests/day, medium failure cost,
small backend team, commodity, low volatility.

**Passes if:** The recommendation can return USE even when the package is
not already installed. It treats a maintained package added as a normal
dependency as USE, not FORK or BUILD.

**Fail if:** The recommendation says USE only applies to dependencies
already in the project manifest.

---

## 12. FORK requires copy, vendor, or patch

**Input:** "Should we use an unmaintained open-source scheduler that needs
local patches?"
Context: time horizon 3 years, low scale, medium failure cost, strong team,
supporting capability, medium volatility.

**Passes if:** The recommendation uses FORK only because the project must be
copied, vendored, or patched. It checks stars, contributors, releases, issue
response time, and license.

**Fail if:** The recommendation uses FORK for a maintained package that can
stay as a normal dependency.

---

## 13. Evidence matrix columns

**Input:** "Should we build or use a rate limiter?"

**Passes if:** The evidence matrix uses these columns: Option, Reliability,
Strategic value, Adaptability, TCO, Speed to value, Citation.

**Fail if:** The matrix uses Coverage, Cost, Effort, or Risk instead of the
five framework components.

---

## 14. OpenCode permission ordering

**Input:** Inspect `agents/nothing-new-under-the-sun.md`.

**Passes if:** Under `permission.bash`, `"*": ask` appears before specific
deny rules. This matches OpenCode's last-matching-rule-wins behavior.

**Fail if:** `"*": ask` is last and can override specific denies on
OpenCode.

---

## 15. One-way door confidence gate (v1.1.0)

**Input:** "Let's commit to a vendor that ingests all our data into its
proprietary format. We're about 70% sure."
Context: 5-year horizon, high failure cost, vendor offers no export tooling.

**Passes if:** The recommendation classifies this as a one-way door
(vendor-specific data model, no export) and refuses to proceed below HIGH
confidence. It requires a POC, more research, or a scope-cut to raise
confidence or make the door two-way before committing. It notes that the
decisive re-evaluation must happen before commit, not after.

**Fail if:** The recommendation proceeds at MEDIUM confidence, or treats
irreversible data lock-in as a reversible choice.

---

## 16. Team capability versus team fit (v1.1.0)

**Input:** "We could build our own observability stack — the team is
strong enough."
Context: strong platform team (high capability), but the team's mission is
the product, not infrastructure, and it does not want to own on-call for a
telemetry pipeline (low fit).

**Passes if:** The recommendation separates capability from fit under
context question 4. It notes that high capability with low fit favors USE
or BUY over BUILD, and does not recommend BUILD on capability alone.

**Fail if:** The recommendation recommends BUILD purely because the team
is capable, ignoring ownership fit.

---

## 17. Expanded AI mapping — RAG and agents (v1.1.0)

**Input:** "We want a chatbot over our internal docs with tool-calling."
Context: commodity retrieval, standard needs, small team, retrieval quality
is not the product.

**Passes if:** Retrieval maps to a RAG framework as USE (LangChain,
LlamaIndex, or Haystack) and orchestration maps to an agent framework as
USE (LangGraph, CrewAI, and similar). BUILD appears only if retrieval
quality or orchestration is explicitly the product.

**Fail if:** The recommendation defaults to BUILD-ing a bespoke RAG
pipeline or agent orchestration when a maintained framework fits.
