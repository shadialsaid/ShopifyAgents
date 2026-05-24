# CLAUDE.md

Guidance for AI assistants (and humans) working in this repository.

> **Status: planning / pre-code.** As of the last update, this repo contains
> product documentation (`docs/`) but no application code, dependencies, build
> tooling, or tests yet. Sections below marked _(to be documented)_ are
> intentional placeholders. **Whenever you add real code, update the
> corresponding section here in the same change** so this file always reflects
> the true state of the codebase. Do not invent structure or commands that
> don't exist.

## Project overview

- **Name:** ShopifyAgents
- **Purpose:** A suite of autonomous AI agents for Shopify merchants. Two
  agents are specified so far (see `docs/`):
  - **Content Agent** — generates/optimizes/maintains store content (product
    descriptions, collection & landing copy, blog posts, SEO + GEO metadata).
  - **Marketing Agent** — plans/runs/optimizes lifecycle marketing across
    owned channels (email, SMS, and later WhatsApp/RCS/push).
  The two agents are designed to share services (brand voice, asset library,
  store connection, analytics). The tech stack is **not yet chosen**.

## Current repository state

```
.
├── CLAUDE.md   # this file
├── README.md   # placeholder ("# ShopifyAgents")
└── docs/
    ├── content-agent-prd.md     # PRD: Content Agent (draft v0.1)
    └── marketing-agent-prd.md   # PRD: Marketing Agent (draft v0.1)
```

That is the entire repository today — product docs only, no code yet. Start
with the PRDs in `docs/` to understand intended scope before writing code.

## Tech stack

_(to be documented)_ — No language, framework, package manager, or runtime has
been chosen yet. Once the first code lands, record here:
- primary language(s) and version(s)
- framework(s) and major libraries
- package manager and how dependencies are installed

## Development workflow

_(to be documented)_ — There is currently no build, run, test, or lint
tooling. As these are added, document the exact commands here, for example:
- install dependencies
- run the app / dev server locally
- run the test suite (and how to run a single test)
- lint / format / type-check

Keep this list accurate: an assistant should be able to copy a command from
here and have it work.

## Code structure & conventions

_(to be documented)_ — No source layout or coding conventions exist yet. When
the project takes shape, describe the directory layout, where new code belongs,
naming conventions, and any patterns to follow or avoid.

## Git & branch workflow

These conventions are active now and apply to all work in this repo:

- **Feature branches:** develop on a dedicated feature branch; do not commit
  directly to `main`. Create the branch locally if it does not exist.
- **Commits:** make clear, descriptive commit messages. Prefer new commits over
  amending or force-pushing published history.
- **Pushing:** push with `git push -u origin <branch-name>`. On transient
  network failures, retry with exponential backoff.
- **Pull requests:** do **not** open a PR unless explicitly asked.
- **Safety:** never skip hooks (`--no-verify`), never force-push to `main`, and
  avoid destructive git operations unless the user explicitly requests them.

## Notes for AI assistants

- This file is the source of truth for project conventions. Treat the
  _(to be documented)_ placeholders as a checklist to fill in as the codebase
  grows, and remove this note once the project is no longer in bootstrap state.
- Don't fabricate commands, file paths, or conventions. If something isn't
  established yet, say so or ask, rather than guessing.
