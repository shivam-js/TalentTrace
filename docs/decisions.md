# Architecture decision log

## ADR-001: PostgreSQL is the primary database

**Decision:** Use PostgreSQL and write SQL through versioned migrations, with Drizzle for type-safe query construction where useful.

**Reason:** The workflow is relational: organizations, roles, jobs, candidates, applications, evidence, feedback and audit events need transactions and explicit access boundaries. PostgreSQL also provides full-text search and can support vectors later without introducing a separate database early.

## ADR-002: Groq is optional, not on the critical path

**Decision:** Use Groq through a provider adapter for structured drafting only. Core ingestion and evidence browsing work without a Groq key.

**Reason:** Free-tier capacity may be limited or change. A useful portfolio product must remain usable while quota is unavailable and should not send every processing step to a paid hosted model.

## ADR-003: The first release is assistive, not a decision engine

**Decision:** Present cited evidence and editable interview preparation. Do not automatically hire, reject, score trustworthiness, or assert authorship.

**Reason:** Repository and resume data are incomplete signals. This boundary is safer, easier to explain in interviews, and enables human accountability.

