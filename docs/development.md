# Development setup

## Prerequisites

- Node.js 24 or newer
- pnpm 11 or newer
- Docker Desktop for PostgreSQL and Redis local services

## Workspace layout

```text
apps/
  web/       Next.js interface
  api/       Fastify HTTP API
  worker/    Background extraction and ingestion jobs
packages/
  domain/    Shared domain rules and validation
  config/    Shared tooling configuration
```

The root workspace intentionally has no production dependencies yet. Each service will be added with its own package manifest after its responsibility and test boundary are defined.

## Local configuration

Copy `.env.example` to `.env` when local services are introduced. Keep real credentials in the untracked `.env` file. Groq is optional in the first vertical slice; link extraction must work without it.

