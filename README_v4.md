# Course Plan Audit Studio v4.0

Fresh rebuild based on the v3.3 client-side application and the audit rules learned from real 2026 course plans.

## New audit architecture
- Grid/master-data validation, with support for authoritative `aiIntegrated` when present in Grid/imported reference JSON.
- Canonical metadata and cross-section consistency checks.
- Course type inference: Theory Only, Lab Only, Theory + Lab.
- Practical-credit dependency checks for lab syllabus, delivery, and monitoring.
- Canonical CO validation and undefined-CO review.
- Placeholder/template detection and faculty/designation/prerequisite reconciliation.
- AI declaration vs course-specific evidence, while excluding generic institutional AI guidance.
- Reference relevance and label/URL mismatch checks.
- Lifecycle stages: Planning, First Monitoring, Mid-Semester, Second Monitoring, Completion.
- Completion and compliance scores shown independently.
- Existing local DOCX/PDF parsing, CSV/Word reporting, model advisory layer, and browser-only privacy retained.

## Important Grid note
The bundled v3.3 `grid-data.js` contains allocations/catalog data but does not expose an AI-integrated field in the records inspected during this rebuild. v4.0 supports `aiIntegrated`, `ai_integrated`, or `ai` fields when the authoritative Grid is updated/imported; until then, GRID-06 reports Review rather than inventing a value.
