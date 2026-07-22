# There Is Nothing New Under The Sun

**A research-first scouting agent skill. Maximize long-term business value before you add code or dependencies.**

[![skills.sh](https://skills.sh/b/fahrellgiovanny/nothing-new-under-the-sun)](https://skills.sh/fahrellgiovanny/nothing-new-under-the-sun/nothing-new-under-the-sun)

---

## Purpose

AI coding agents start by writing code. This skill starts with a
different rule: **evaluate long-term business value before you create
new code.** Search existing solutions. Compare them on reliability,
strategic value, adaptability, total cost of ownership, and speed to
value. Then choose the tier that maximizes value for your situation.

The skill now uses a required output schema. Each recommendation includes
context, tier search, evidence matrix, recommendation, reasons, confidence,
re-evaluation trigger, and missing information.

Unlike cost-only build-vs-buy analyzers, this skill evaluates five
components of business value. A commodity (like auth or PDF generation)
wins on TCO and speed — USE or BUY the best seller. A core competency
(like a matching engine or recommendation system) wins on strategic
value and adaptability — BUILD or FORK. The framework has no preferred
answer. Your situation determines the right tier.

## Decision ladder

Start at the top. Move down only when a step finds no viable candidate.

```
REUSE     — a solution exists in the repository or the organization.
USE       — a dependency in the project manifest solves it.
FORK      — an open-source project solves it. Vendor or fork.
BUY       — a SaaS product solves it.
INTEGRATE — an API solves it.
BUILD     — viable when no earlier tier fits. Cite the search.
```

The order is a search order. It is not a preference order. Your
situation determines which tier maximizes value.

Skip the ladder for small local changes. Do not run it for bug fixes,
single-line fixes, existing imports, routine refactors, docs, style, or lint.

## Install

### Agent Skills CLI (recommended)

```bash
npx skills add fahrellgiovanny/nothing-new-under-the-sun
```

### GitHub CLI

```bash
gh skill install fahrellgiovanny/nothing-new-under-the-sun nothing-new-under-the-sun --agent <agent-id> --scope user
```

### Manual install

Copy `SKILL.md` to the skills directory of your agent.

| Agent | Path |
|---|---|
| OpenCode | `.opencode/skills/nothing-new-under-the-sun/SKILL.md` |
| Claude Code | `.claude/skills/nothing-new-under-the-sun/SKILL.md` |
| Codex CLI | `.agents/skills/nothing-new-under-the-sun/SKILL.md` |
| Cursor | `.cursor/skills/nothing-new-under-the-sun/SKILL.md` |
| Gemini CLI | `.gemini/skills/nothing-new-under-the-sun/SKILL.md` |
| GitHub Copilot | `.github/skills/nothing-new-under-the-sun/SKILL.md` |
| Windsurf | `.windsurf/skills/nothing-new-under-the-sun/SKILL.md` |
| Cline | `.cline/skills/nothing-new-under-the-sun/SKILL.md` |
| Roo Code | `.roo/skills/nothing-new-under-the-sun/SKILL.md` |
| Amp | `.agents/skills/nothing-new-under-the-sun/SKILL.md` |
| OpenHands | `/add-skill https://github.com/fahrellgiovanny/nothing-new-under-the-sun/tree/main/skills` |
| Hermes Agent | `~/.hermes/skills/nothing-new-under-the-sun/SKILL.md` |
| OpenClaw | `~/.openclaw/skills/nothing-new-under-the-sun/SKILL.md` |
| Kiro CLI | `~/.kiro/skills/nothing-new-under-the-sun/SKILL.md` |
| Factory Droid | `.factory/skills/nothing-new-under-the-sun/SKILL.md` |

Agents without native skill directories (Aider, for example) can read the
prompt with `/read <path/to/SKILL.md>`. The Markdown prompt works with
any LLM.

### Dedicated scouting agent

Copy `agents/nothing-new-under-the-sun.md` to the agent directory of your
platform. The scouting agent is read-only. It cannot write code or install
packages. Configure the platform to deny the write, edit, and package
install permissions.

## Workflow

The skill directs the agent through seven search stages:

1. **Search the repository.** The solution may already exist in the
   codebase.
2. **Check the dependencies.** A package in the project manifest may
   cover the need.
3. **Search public registries.** Look for mature packages on npm, PyPI,
   crates.io, and similar registries.
4. **Search GitHub repositories.** Examine the stars, maintenance status,
   bus factor, and license of each candidate.
5. **Search for APIs and SaaS products.** Some problems do not need code.
6. **Search for examples and templates.** Fork or adapt an existing
   reference.
7. **Check the license.** Verify compatibility with the project.

The agent fills a five-column evidence matrix for every candidate:

| Candidate | Reliability | Strategic value | Adaptability | TCO | Speed to value |
|-----------|-------------|-----------------|--------------|-----|----------------|

The agent then returns one recommendation with this required schema:

1. Context.
2. Tier search.
3. Evidence matrix.
4. Recommendation.
5. Why this wins.
6. Confidence.
7. Re-evaluation trigger.
8. Missing information.

## Examples

### Commodity: auth

```
# Request
Should we build our own auth, or use Auth0?

# Recommendation (compound)
USE next-auth for the commodity slice. Small BUILD layer over next-auth
callbacks for enterprise SSO, only when the first enterprise customer
asks for it.

# Why this wins
- Reliability: next-auth proven at scale (5M weekly, no critical CVE).
- Strategic value: identity is a commodity. Engineering effort goes to
  product work.
- Adaptability: adapters cover OAuth, passkeys, SAML.
- TCO: near zero license; no per-MAU bill.
- Speed to value: one week to production.
```

### Core competency: matching algorithm

```
# Request
Should a ride-hailing company build or buy its driver-rider matching
algorithm?

# Recommendation (compound)
BUILD the matching engine. INTEGRATE routing and mapping APIs.

# Why this wins
- Reliability: proven only through iteration; every competitor faced the
  same risk.
- Strategic value: matching IS the product. Only BUILD supplies this.
- Adaptability: BUILD gives full control; strategy changes weekly.
- TCO: high build cost but zero seller cost; no lock-in.
- Speed to value: 6-12 months to MVP; compounding gains over 10 years.
```

## Agent compatibility

This skill follows the [Agent Skills specification](https://agentskills.io/specification).
It works with any compatible agent.

**Compatible agents:**

- OpenCode
- Claude Code (Anthropic)
- Codex CLI (OpenAI)
- Cursor
- GitHub Copilot
- Gemini CLI (Google)
- Windsurf
- Cline
- OpenHands
- Hermes Agent (Nous Research)
- OpenClaw
- Roo Code
- Amp
- Kiro CLI
- Factory Droid

For agents without native skill support, paste the prompt or use the
`/read` command.

## Skill versus agent

| | Skill | Agent |
|---|---|---|
| **Loads when** | Before a build proposal, automatically | When invoked or dispatched |
| **Writes code** | Yes, after a justified BUILD recommendation | No |
| **Use for** | Daily development sessions | Auditable decisions |
| **Permissions** | Set in the host platform | Set in the agent definition |

Use the skill for daily work. Dispatch the scouting agent when the
read-only boundary must be guaranteed.

## Philosophy

AI coding agents write code first. They produce 50 lines for a problem
that one import solves. They build an auth system when three mature
libraries exist. They build a service when an API already does the job.

This skill inverts that default. It tells the agent: evaluate long-term
business value before you create new code.

The philosophy: **there is nothing new under the sun.** Your problem is
not unique. Existing work covers most of it. Find that work and compare
its value before you build.

## Repository structure

```
nothing-new-under-the-sun/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── skills/
│   └── nothing-new-under-the-sun/
│       └── SKILL.md
├── agents/
│   └── nothing-new-under-the-sun.md
└── tests/
    └── scenarios.md
```

## Prior art

This skill follows a long tradition of research-first and build-versus-buy
analysis. Direct influences:

- The Agent Skills specification and ecosystem.
- Build-versus-buy analysis in enterprise architecture.
- Prior-art search in patent and open-source contexts.
- Dependency-check-first workflows in modern package managers.
- Wardley Mapping and DDD Core/Supporting/Generic classification.

Related skills use different approaches. This skill differs from all of
them. It requires a six-tier recommendation, a five-component evidence
matrix, and strict citation format.

Enterprise-grade weighted-scoring tools (Agensi Build-vs-Buy Analyzer) and
strategic modeling frameworks (Wardley Mapping) exist. This skill targets a
different moment: the instant before an AI agent or engineer writes new
code. It runs in one turn and produces a defensible recommendation.

## Feedback

Report issues and request features at
[github.com/fahrellgiovanny/nothing-new-under-the-sun/issues](https://github.com/fahrellgiovanny/nothing-new-under-the-sun/issues).

## Security

- This skill contains only Markdown. It has no scripts, executables, or
  runtime code.
- WARNING: Agents run with full platform permissions. Configure each host
  to deny write, edit, and package install access during research.
- Do not run candidate install commands during research.
- Request approval before you install, copy, or import a candidate.
- Examine the security audit results on skills.sh before you install.

## License

MIT — see [LICENSE](./LICENSE).

---

*"The thing that hath been, it is that which shall be; and that which is done
is that which shall be done: and there is no new thing under the sun."* —
Ecclesiastes 1:9 (KJV)
