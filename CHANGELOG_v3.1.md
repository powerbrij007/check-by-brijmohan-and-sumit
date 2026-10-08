# Changelog — Course Plan Audit Studio

## 3.2
- Removed page-number logic from audit results and exports.
- Fixed DOCX reader regression: extracted DOCX text/tables are now returned correctly to the audit engine.
- Hardened PDF text extraction by disabling the optional PDF.js worker dependency.
- Added explicit errors for unreadable/empty DOCX files and scanned/image-only PDFs.
- L-T-P failure evidence instructs users to replace default placeholders such as `(Add number of Credits)` with `0` when a value is not available.


## Audit hardening

This release follows a regression audit of v3.0 using a real UPES CSEG3055 course plan.

### Fixed
- Course-name extraction no longer mistakes the document heading `COURSE PLAN` for the course field.
- Theory-only L-T-P validation accepts a blank Practical cell as zero when Lecture and Tutorial are explicitly present.
- Session comparison now canonicalizes equivalent month-range formats.
- Academic-year comparison recognizes a single-year document value such as `2026` against a configured academic year `2026-2027` when appropriate.
- Course Outcome detection is restricted to the Expected Course Outcomes section and no longer counts sample-template CO labels.
- Non-AI yellow highlighting is a Review condition rather than an automatic failure.
- Actual-delivery validation is lifecycle-aware through Planning, Mid-Semester and Completion stages.

### Preserved design decisions
- Rule-engine results remain authoritative.
- ML predictions remain advisory and disagreements remain visible.
- Documents remain locally processed in the browser.

## v3.2 patch
- Removed unreliable page-number references from validation results, CSV export, and DOCX audit tables.
- L-T-P failures now explicitly instruct users to remove placeholders such as **(Add number of Credits)** and enter `0` when a value is not available.


## v3.3 faculty extraction hardening
- Improved DOCX faculty-name extraction for merged/form-style tables and label/value cells.
- Added faculty-name aliases (`Name of Faculty`, `Faculty Name`).
- Preserves honorifics such as `Dr.` in the displayed extracted name.
- Normalizes common honorifics only when matching the faculty against reference-grid assignments.
- Regression target: `C_Programming_CSEG_1041_Vinod_Kumar.docx` → `Dr. Vinod Kumar`.
