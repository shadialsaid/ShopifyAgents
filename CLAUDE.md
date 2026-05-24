# CLAUDE.md

Guidance for AI assistants (and humans) working in this repository.

> **Status: bootstrap / empty repository.** As of the last update, this repo
> contains only this file and a placeholder `README.md`. No application code,
> dependencies, build tooling, or tests exist yet. Sections below marked
> _(to be documented)_ are intentional placeholders. **Whenever you add real
> code, update the corresponding section here in the same change** so this
> file always reflects the true state of the codebase. Do not invent structure
> or commands that don't exist.

## Project overview

- **Name:** ShopifyAgents
- **Inferred purpose:** Tooling and/or AI agents that interact with Shopify
  (e.g. stores, products, orders, the Shopify Admin/Storefront APIs). This is
  inferred from the repository name only and has **not** been confirmed by code
  or documentation. Confirm the actual scope before relying on it, and correct
  this line once the direction is settled.

## Current repository state

```
.
├── CLAUDE.md   # this file
└── README.md   # placeholder ("# ShopifyAgents")
```

That is the entire repository today.

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
