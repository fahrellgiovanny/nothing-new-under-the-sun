# There Is Nothing New Under The Sun

**A research-first agent skill. Search existing solutions before you add code or dependencies.**

[![skills.sh](https://skills.sh/b/fahrellgiovanny/nothing-new-under-the-sun)](https://skills.sh/fahrellgiovanny/nothing-new-under-the-sun)

---

## Purpose

AI coding agents start by writing code. This skill starts with a
different rule: **existing solutions already cover most problems.**
Search existing solutions before you create new ones.

## Decision ladder

Start at the top. Move down only when a step fails.

```
REUSE     — a solution exists in the repository or the organization.
USE       — a dependency in the project manifest solves it.
FORK      — an open-source project solves it. Vendor or fork the code.
BUY       — a SaaS product solves it.
INTEGRATE — an API solves it.
BUILD     — only now. Write justification for the new code.
```

BUILD is the last choice. Do not start with it.

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

### Dedicated read-only agent

Copy `agents/nothing-new-under-the-sun.md` to the agent directory of your
platform. Configure the platform to deny the write, edit, and package
install permissions.

## Workflow

This skill directs the agent through six search stages:

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

The agent produces an evidence matrix for every candidate.

| Name | URL | Popularity | Maintenance | License | Effort |
|---|---|---|---|---|---|
| candidate-a | github.com/... | 5K stars | active since 2024 | MIT | S |
| candidate-b | npmjs.com/... | 2M DL/week | last commit 2023 | Apache-2.0 | M |

The agent then returns one verdict with justification.

## Example

```
User: "We need a rate limiter for the API."
Agent (skill loaded):
  REUSE  — No rate limiter exists in the codebase.
  USE    — express-rate-limit is already in node_modules,
           version 7.x, MIT license. The package is mature
           (3K stars, updated last week). Use it directly.
  Verdict: USE express-rate-limit. No new code or new dependency needed.
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
| **Writes code** | Yes, after a justified BUILD verdict | No |
| **Use for** | Daily development sessions | Auditable decisions |
| **Permissions** | Set in the host platform | Set in the agent definition |

Use the skill for daily work. Dispatch the agent when the read-only
boundary must be guaranteed.

## Philosophy

AI coding agents write code first. They produce 50 lines for a problem
that one import solves. They build an auth system when three mature
libraries exist. They build a service when an API already does the job.

This skill inverts that default. It tells the agent: find the existing
solution before you create one.

The philosophy: **there is nothing new under the sun.** Your problem is
not unique. Existing work covers most of it. Find that work before you
build.

## Repository structure

```
nothing-new-under-the-sun/
├── README.md
├── LICENSE
├── SKILL.md
└── agents/
    └── nothing-new-under-the-sun.md
```

## Prior art

This skill follows a long tradition of research-first and build-versus-buy
analysis. Direct influences:

- The Agent Skills specification and ecosystem.
- Build-versus-buy analysis in enterprise architecture.
- Prior-art search in patent and open-source contexts.
- Dependency-check-first workflows in modern package managers.

Related skills use different approaches. `search-first` focuses on package
and MCP discovery. `skill-scout` evaluates capability gaps. `before-you-build`
runs product pre-mortems. `research` provides citation guidance.

This skill differs from all of them. It requires a six-outcome verdict and
an auditable evidence matrix.

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
