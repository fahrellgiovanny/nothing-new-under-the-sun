---
name: nothing-new-under-the-sun
description: >
  Research-first mindset that runs BEFORE any build decision, new dependency,
  new system, or feature request. Search existing solutions (codebase,
  dependencies, packages, GitHub repos, APIs, SaaS, templates) before writing
  code. Output a REUSE / USE / FORK / BUY / INTEGRATE / BUILD verdict with an
  evidence matrix. Trigger when someone proposes a new feature, asks to add a
  dependency, says "build X", "add X", "we need X", or any time greenfield
  code is considered.
license: MIT
metadata:
  author: fahrellgiovanny
  version: "1.0.0"
---

# There Is Nothing New Under The Sun

Before proposing any implementation, determine whether code should exist.
The first answer to a feature request is never "let me write code" —
it is "let me find an existing solution first."

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

## Search order

1. **This repository first.** Search the codebase for existing implementations,
   helpers, or utilities that already solve the problem. REUSE beats USE.
2. **Existing dependencies.** Check the project manifest — a package already
   in the tree may cover the need.
3. **Public packages** (registries) for mature, maintained solutions.
4. **GitHub repositories** — stars, last commit, open issues, bus factor.
5. **APIs and SaaS** — when an external service solves it without owning code.
6. **Examples and templates** — reference implementations to fork or adapt.
7. **License compatibility** with the project's constraints.

## For every candidate, provide

- **Name**
- **URL**
- **Popularity** — stars, weekly downloads
- **Maintenance status** — last commit, open issues, bus factor
- **License** — and compatibility with the project's licensing
- **Estimated integration effort** — S / M / L

## Verdict

Output exactly one verdict:

```
REUSE     — already in this repository or internally available?
USE       — an existing dependency already solves it?
FORK      — an open-source project solves it (vendor or fork)?
BUY       — a SaaS product solves it?
INTEGRATE — an API solves it?
BUILD     — only now, and only with written justification
```

BUILD is the last resort, not the default. If you reach BUILD, cite the
candidates you rejected and why none of them fit.

## Output format

For quick research, return the verdict and matrix inline. For research that
will be referenced later, write the report to a docs or research directory
using a standard format.

## Agent versus skill

This prompt exists in two forms:

- **Skill** (this file) — loaded by the orchestrator during normal sessions.
  Research is performed before implementation. A BUILD verdict with
  justification unlocks code generation.
- **Agent** — a separate, permission-bound definition that enforces read-only
  research. The agent cannot edit files, install packages, or run writes.
  Use when research must be auditable or when the user wants a guaranteed
  read-only boundary.

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
- Never expose local files, credentials, or private repository information.
