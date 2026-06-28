# Tempo API Docs — Fern proof of concept

A complete, runnable [Fern](https://buildwithfern.com) documentation project for the **Tempo**
API (a multi-tenant X/Twitter scheduling platform). The entire site is generated from one
source of truth — an OpenAPI spec authored directly from Tempo's Next.js route handlers — and
managed as docs-as-code: versioned in Git, reviewed via PRs, and rebuildable in CI.

Built as a portfolio piece for the **NVIDIA Documentation Engineer / Technical Writer** role,
which calls for owning docs-as-code, API/SDK references, information architecture, and the
tooling underneath. NVIDIA itself runs on Fern, so this targets their actual stack.

## What's here

```
fern/
  fern.config.json     # Fern CLI + org config
  generators.yml       # SDK generators (TypeScript + Python) from the same spec
  docs.yml             # Site config: nav, theme, API reference wiring (information architecture)
  openapi/openapi.yml  # Source of truth — 20 paths, 34 operations, 14 schemas, dual auth
  pages/               # Hand-written MDX guides
    introduction.mdx
    quickstart.mdx
    authentication.mdx
    scheduling-model.mdx
    errors.mdx
preview/
  index.html           # Static preview of the rendered site (no install needed to view)
```

The narrative guides (concepts, quickstart, error model) are hand-authored; the full API
reference is generated from the spec, so it never drifts from the API.

## Run it

```bash
npm install -g fern-api      # or: npx fern-api <command>
cd fern

fern check                   # validate the spec and docs config
fern docs dev                # live local preview at http://localhost:3000
fern generate --docs         # build/publish the docs site
fern generate --group ts-sdk # generate the TypeScript SDK from the same spec
```

## Why this maps to the role

| Job requirement | Where it shows up |
| --- | --- |
| Docs-as-code, Git, Markdown | MDX pages + `docs.yml`, all Git-versioned and PR-reviewable |
| SDK / API references | `openapi/openapi.yml` drives the reference and generated SDKs |
| Information architecture & content design | `docs.yml` navigation; concept/quickstart/reference split |
| Build/publish workflow, CI checks | `fern check` as a CI guardrail; `fern generate` as the build |
| Technical depth to validate examples | Spec written from the real route handlers, not guessed |
| Automating reference docs | Reference + SDKs auto-generated from one spec |

## A note on accuracy

The spec mirrors Tempo's real endpoints, methods, auth model (Supabase Bearer JWT for users,
`CRON_SECRET` for cron), role gates, and `409` slot-conflict behavior. Host URL, example IDs,
and a few response bodies are illustrative placeholders, clearly marked, since this documents a
private app rather than a public service.
