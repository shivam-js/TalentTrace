# Initial architecture

## Why a modular monolith first

TalentTrace needs a web interface, HTTP API, and durable background processing, but its first release does not need independently deployed microservices. A pnpm workspace will keep boundaries clear while making local development and debugging practical for one developer.

```text
Browser
  -> Next.js web application
  -> Fastify API
       -> PostgreSQL (application data, audit events, full-text search)
       -> Redis (background-job queue)
       -> private object storage (uploaded documents and snapshots)
  -> Worker (PDF extraction and repository ingestion)
```

## Planned workspace boundaries

| Package | Responsibility | Must not do |
| --- | --- | --- |
| `apps/web` | Recruiter workflow and evidence-review UI | Access the database directly. |
| `apps/api` | Authentication, authorization, REST API, durable records | Parse large uploads in a request handler. |
| `apps/worker` | Bounded, retry-safe extraction and ingestion jobs | Make authorization decisions without validated job context. |
| `packages/domain` | Shared types, validation schemas, permissions and domain rules | Depend on Next.js or UI code. |
| `packages/config` | Shared TypeScript, lint and test configuration | Contain secrets. |

## Data and processing choices

- PostgreSQL is the database engine; the team writes SQL through migrations and Drizzle where it improves maintainability.
- Redis plus BullMQ provides durable retries and controlled concurrency for document and repository processing.
- The uploaded original document is private. Extraction results retain page/source references so a reviewer can inspect the basis for a link or claim.
- Each repository inspection is tied to a selected commit SHA and constrained by repository, file-count, size and type limits.

## AI and retrieval choices

Deterministic parsing handles resume text and embedded links. PostgreSQL full-text search is the baseline retrieval method; a local embedding adapter may add semantic retrieval when the machine can run it. Groq is used only for bounded, structured drafting after evidence has been retrieved. The API validates structured output and retains its cited sources.

## Security baseline

- Every record belongs to an organization; authorization checks happen server-side for each operation.
- IDs do not grant access by themselves.
- Environment variables and uploaded resumes are never committed.
- Repository content is treated as untrusted data and is never executed.

