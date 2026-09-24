# TalentTrace product scope

## User problem

Technical interviewers often receive a resume and a repository link without a reliable way to connect stated experience to specific, reviewable implementation evidence. Manual preparation is slow and inconsistent.

TalentTrace helps an authorized hiring team prepare for an interview by organizing job requirements, resume claims, selected repository evidence, and interview findings in one workspace.

## First-release boundaries

- Support text-based PDF resumes first. Scanned PDFs show an explicit unsupported state.
- Extract only the resume content and embedded hyperlink destinations needed for the workflow.
- Require explicit selection of a candidate-authorized public repository.
- Snapshot a bounded repository commit and inspect source as text; never run its code.
- Present citations, uncertainty, and editable human feedback.
- Do not make hiring decisions, rank candidates automatically, or infer authorship or honesty.

## Evidence model

| Type | Meaning |
| --- | --- |
| Resume claim | Statement found in the uploaded resume. |
| Observed evidence | A cited source file/line or extracted document passage. |
| Unknown | A requirement for which the available material provides no reliable evidence. |
| Human finding | Interviewer feedback entered after review or interview. |

