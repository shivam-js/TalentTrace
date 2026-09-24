# TalentTrace

TalentTrace is an evidence-based technical hiring workspace for human interviewers. It connects job requirements, resume claims, and candidate-authorized repository evidence to produce reviewable technical interview briefs.

## Product principles

- Distinguish a resume claim, observed code evidence, an unknown, and a human finding.
- Cite the source of each technical observation.
- Keep the human interviewer in control; TalentTrace does not automatically hire, reject, or label candidates.
- Process only candidate-authorized public repositories in the first release and never execute submitted code.

## First vertical slice

1. A recruiter signs in and creates an application.
2. A synthetic PDF resume is uploaded.
3. TalentTrace extracts text and actual embedded destinations behind GitHub, LinkedIn, and portfolio labels.
4. The recruiter reviews and corrects those links before they are used.

## Planned stack

Next.js, React, TypeScript, Fastify, PostgreSQL, Redis, Docker Compose, GitHub Actions, local embeddings, and Groq for selective structured AI drafting.

## Status

Phase 0: product definition and project foundation.

