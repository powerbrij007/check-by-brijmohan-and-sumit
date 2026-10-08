# Course Plan Audit Studio — GitHub Pages Edition

A static, privacy-first batch auditor for Course Plan DOCX and PDF files. It can be hosted directly on GitHub Pages; no server, database, API key or upload backend is required. The default Academic Year is **2026-2027**.

## Main capabilities

**Release 3.2 — file-reading and audit UX fix**

- Select multiple DOCX/PDF files
- Select a complete device folder with the browser folder chooser
- Drag and drop a batch of files
- Process all supported files locally in the browser
- Match faculty/course assignments against the embedded reference data
- Apply the Course Plan validation rules
- Run the browser-converted trained classifier for Pass/Fail/Review/N/A recommendations
- Show rule/model agreement and confidence
- Search and filter file results
- Explain every failed and review check
- Download one consolidated CSV report
- Download one professionally formatted Microsoft Word `.docx` dashboard report with a populated contents index, file-wise validation dossiers and the closing note “A little help from Brijmohan”
- Print/save the dashboard as PDF
- Edit academic session/year, audit stage and import/export reference data
- Use lifecycle-aware auditing: Planning, Mid-Semester or Completion
- Normalize equivalent session/year formats before comparison
- Restrict Course Outcome detection to the actual Expected Course Outcomes section
- Treat a blank Practical value as zero for theory-only courses when L/T are present
- Treat non-AI highlighting as a manual-review item instead of an automatic failure
- Preserve deterministic rule results as authoritative while keeping the ML classifier advisory

## Privacy

Selected documents never leave the browser. The application has no upload endpoint. All libraries, the reference data and the converted trained model are included in the repository.

Browser security does not permit a website to read a typed local folder path. Users must select the folder through **Select folder**. Chrome, Edge and other Chromium-based browsers provide the best folder-selection support.

## GitHub Pages deployment

### Option 1: automatic workflow

1. Create a GitHub repository.
2. Upload all files and folders from this package to the repository root.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, select **GitHub Actions**.
5. Push to the `main` branch. The included workflow publishes the site.

### Option 2: deploy directly from a branch

1. Upload this package to the root of the `main` branch.
2. Open **Settings → Pages**.
3. Select **Deploy from a branch**.
4. Choose `main` and `/ (root)`.

## Local testing

Opening ES modules directly through `file://` may be blocked by browsers. Start a local server:

```bash
python3 -m http.server 8080
```

Then open <http://localhost:8080>.

## Included data

- Course catalogue: 157 records
- Faculty/course assignments: 110 records
- Academic-session settings are stored in the user's browser
- Converted classifier source fingerprint: `23e0dfd5f73e236a3d804ac62d97a30c8857193dd1729df039b0b598444d6035`

## v3.2 fixes

8. Fixed a regression in DOCX parsing where the extracted document data was built but not returned to the audit engine.
9. PDF parsing now runs without requiring a PDF.js worker file, reducing worker-loading failures on static hosting.
10. DOCX/PDF readers now return clear errors for empty/unreadable files; scanned/image-only PDFs are explicitly reported as requiring OCR.

## v3.1 audit fixes

The regression audit against the supplied CSEG3055 course plan identified and addressed the following v3.0 issues:

1. Generic `Course` label extraction could capture the document heading `COURSE PLAN`; course extraction now prefers the structured table field.
2. Theory-only L-T-P rows with a blank Practical value are interpreted as `P=0` when appropriate.
3. `July-Dec 2026` and `July - December 2026` are compared canonically.
4. `Academic Year: 2026` can match a configured `2026-2027` academic year when the session year agrees.
5. CO detection is scoped to the Expected Course Outcomes section so sample indirect-assessment CO5-CO7 labels do not contaminate the course result.
6. Yellow highlighting on a non-AI course produces Review rather than an automatic Fail, because template highlighting requires context/visual verification.
7. Actual-delivery completeness is lifecycle-aware: it is not mandatory during Planning, becomes a reviewable mid-semester condition, and is mandatory at Completion.

## Limitations

- Scanned PDFs without a text layer require OCR before automatic validation.
- PDF highlight colours and signatures require manual visual confirmation.
- Browser folder access requires an explicit user selection; a web page cannot silently read a local path.
- The explainable audit rules remain authoritative. Model predictions are advisory and disagreements are highlighted.
