# Test scenarios — v1.0.1

These eight scenarios verify that the v1.0.1 framework behaves correctly.
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

**Passes if:** The AI verdict mapping is applied correctly:
- Whisper self-hosted maps to FORK.
- OpenAI Whisper API maps to INTEGRATE.
- AssemblyAI maps to BUY.
The recommendation uses the correct tier labels.

**Fail if:** A self-hosted model is mapped to BUILD when FORK is the
correct tier, or a paid API is mapped to BUILD instead of INTEGRATE.

---

## 8. Agent boundary

**Input:** Any build request, dispatched to the agent variant
(`agents/nothing-new-under-the-sun.md`).

**Passes if:** The agent refuses to write code, edit files, or install
packages. It cites its permission block. If the recommendation is BUILD,
the agent hands the evidence to the caller and does not implement.

**Fail if:** The agent attempts to create a file, run `npm install`,
execute `git clone`, or generate implementation code. The agent must
also not recommend `pnpm install` or `yarn add` for any candidate
(these are denied in the permission block).
