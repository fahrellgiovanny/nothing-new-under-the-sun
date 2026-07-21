# There Is Nothing New Under The Sun

**A research-first AI agent skill for dependency, API, SaaS, prior-art, and build-versus-buy decisions before writing code.**

[![skills.sh](https://skills.sh/b/fahrellgiovanny/nothing-new-under-the-sun)](https://skills.sh/fahrellgiovanny/nothing-new-under-the-sun)

---

Most AI coding agents start with code generation. This skill starts with a
different assumption: **someone has probably already solved most of the
problem.** Before creating new code, search existing solutions first.

## The decision ladder

Before any implementation, climb the ladder from top to bottom:

```
REUSE     — already in the repository or internally available?
USE       — an existing dependency already solves it?
FORK      — an open-source project solves it (vendor or fork)?
BUY       — a SaaS product solves it?
INTEGRATE — an API solves it?
BUILD     — only now, and only with written justification
```

Building from scratch is the last resort, not the default.

## Installation

### Agent Skills CLI (recommended — any compatible agent)

```bash
npx skills add fahrellgiovanny/nothing-new-under-the-sun
```

### GitHub CLI

```bash
gh skill install fahrellgiovanny/nothing-new-under-the-sun nothing-new-under-the-sun --agent <agent-id> --scope user
```

### Manual install

Copy `SKILL.md` into your agent's skills directory:

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

For agents without native skill directories (Aider, etc.), use the
`/read <path/to/SKILL.md>` command or include the prompt in your session
manually. The Markdown prompt works with any LLM.

### Dedicated read-only agent

Copy `agents/nothing-new-under-the-sun.md` into your platform's agent or
subagent directory. Configure the platform to deny edit, write, and package
installation permissions.

## How it works

When someone proposes a new feature, dependency, or system, this skill
directs the agent to:

1. **Search the active repository first** — maybe the solution already exists.
2. **Check existing dependencies** — a package already in the tree may cover
   the need.
3. **Search public registries** (npm, PyPI, crates.io, etc.) for mature packages.
4. **Search GitHub repositories** — stars, maintenance, bus factor, license.
5. **Search for APIs and SaaS products** — sometimes code is the wrong answer.
6. **Search for examples and templates** to fork or adapt.

For every candidate found, the skill produces an evidence matrix:

| Name | URL | Popularity | Maintenance | License | Effort |
|---|---|---|---|---|---|
| candidate-a | github.com/... | 5K stars | active since 2024 | MIT | S |
| candidate-b | npmjs.com/... | 2M DL/week | last commit 2023 | Apache-2.0 | M |

The agent then returns exactly one verdict with justification.

## Example

```
User: "We need a rate limiter for the API."
Agent (with skill loaded):
  REUSE  — No existing rate limiter in the codebase.
  USE    — express-rate-limit is already in node_modules,
           version 7.x, MIT license. Mature (3K stars,
           updated last week). Use it directly.
  Verdict: USE express-rate-limit. No new code or dependency needed.
```

## Agent compatibility

This skill follows the [Agent Skills specification](https://agentskills.io/specification)
and works with any compatible agent. Tested with:

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

For agents without native skill support, paste the prompt or use `/read`.

## Skill versus agent

| | Skill | Agent |
|---|---|---|
| **When loaded** | Automatically, before any build proposal | Invoked explicitly or dispatched |
| **Can write code?** | Yes, after a justified BUILD verdict | No — read-only |
| **Best for** | Day-to-day development sessions | Auditable decisions, compliance |
| **Permission enforcement** | Host platform configuration | Built into the agent definition |

Use the skill for everyday development. Dispatch the agent for hard research
where the read-only boundary must be guaranteed.

## Why this exists

AI coding agents default to generating code. They will write fifty lines for
a problem solved by one import. They will build an auth system when three
mature libraries exist. They will create an entire service when an API already
covers the need.

This skill inverts that default. It forces the agent to exhaust existing
solutions before creating new ones. It turns "let me write that" into
"let me find that first."

The philosophy: **there is nothing new under the sun.** Your problem is
probably not unique. Someone has probably solved most of it. Find them before
you build.

## Repository structure

```
nothing-new-under-the-sun/
├── README.md                               ← You are here
├── LICENSE                                 ← MIT
├── SKILL.md                                ← Portable skill (Agent Skills spec)
└── agents/
    └── nothing-new-under-the-sun.md        ← Read-only agent definition
```

## Prior art

This skill builds on a long tradition of research-first and build-versus-buy
thinking in software engineering. Direct inspirations include:

- The Agent Skills specification and ecosystem.
- Build-versus-buy analysis in enterprise architecture.
- Prior-art search in patent and open-source contexts.
- Dependency-check-first workflows in modern package managers.

Similar skills exist with different trade-offs: ECC `search-first` focuses on
package and MCP discovery, `skill-scout` evaluates broad capability gaps,
`before-you-build` does product pre-mortems, and `research` provides strong
citation guidance. This skill distinguishes itself with a strict six-outcome
evidence contract and an auditable candidate matrix.

## Security

- This skill is Markdown only. It contains no scripts, executables, or
  runtime code.
- Research must be read-only. The skill provides instructions; hard
  enforcement requires each host's own permission or sandbox configuration.
- Never execute candidate installation commands during research.
- Request approval before installing, copying, or importing a candidate.
- Review skills.sh security audit results before installation.

## License

MIT — see [LICENSE](./LICENSE).

---

*"The thing that hath been, it is that which shall be; and that which is done
is that which shall be done: and there is no new thing under the sun."* —
Ecclesiastes 1:9 (KJV)
