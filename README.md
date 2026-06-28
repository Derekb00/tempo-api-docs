# Tempo API Documentation

Developer documentation for the Tempo API, a multi-tenant scheduling and publishing
platform for X (Twitter). The site is generated with [Fern](https://buildwithfern.com)
from a single OpenAPI source of truth and managed as docs-as-code: versioned in Git,
reviewed through pull requests, and rebuilt on every change.

**Live docs:** https://derekbaggett.docs.buildwithfern.com

## Project structure

```
fern/
  fern.config.json     Organization and CLI version
  generators.yml       API spec reference and optional SDK generators
  docs.yml             Navigation, theme, and API reference wiring
  openapi/openapi.yml  OpenAPI 3.1 source of truth (20 paths, 34 operations)
  pages/               Hand-written MDX guides
    introduction.mdx
    quickstart.mdx
    authentication.mdx
    scheduling-model.mdx
    errors.mdx
preview/index.html     Static preview of the rendered site
```

The narrative guides are hand-authored; the full API reference is generated from the
spec, so it never drifts from the API.

## Local development

```bash
npm install -g fern-api
fern check          # validate the OpenAPI spec and docs config
fern docs dev       # local preview at http://localhost:3000
```

## Publishing

```bash
fern login
fern generate --docs    # publishes to derekbaggett.docs.buildwithfern.com
```

Client SDKs can be generated from the same spec:

```bash
fern generate --group ts-sdk
```

## Notes

Example IDs and a few sample response bodies are illustrative. No source code or
credentials from the Tempo application are included in this repository.
