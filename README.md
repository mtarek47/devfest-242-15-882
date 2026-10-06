# Tender Document Package Builder

**AI DevFest 2026 — AI Vibe-Coding Contest (Solo)**

- **Participant Name:** Tarek Parvez
- **Registration Number:** 242-15-882
- **Public Live HTTPS Website:** https://mtarek47.github.io/devfest-242-15-882/
- **GitHub Repository:** https://github.com/mtarek47/devfest-242-15-882

---

## 1. How to Run the App

This is a 100% frontend web application running entirely in the browser without any backend dependencies.

### Option A: Direct Browser Execution
Open [`index.html`](file:///c:/Users/Administrator/Desktop/devfest-242-15-882/index.html) or `Tender Package Builder.html` directly in Google Chrome (or any modern browser).

### Option B: Local Web Server
Run Python's built-in HTTP server or any static server:
```bash
python -m http.server 8000
```
Then navigate to: `http://localhost:8000`

### Option C: Live Hosted Website
Visit the official live deployment on GitHub Pages:
**https://mtarek47.github.io/devfest-242-15-882/**

---

## 2. Main Features Completed (Problem Statement Section 4, 5, 6)

1. **Load Requirements (4.1):**
   - Seamlessly parses `requirements.json`.
   - Displays tender metadata (Tender ID, Title, Procuring Entity, Bidder, Submission Deadline).
   - Renders all tender requirements sorted in exact ascending order.

2. **File Upload & Validation (4.2):**
   - Multi-file PDF uploader supporting both file dialog and drag-and-drop.
   - Real-time page count calculation and file size display using client-side `pdf-lib`.
   - Strict file validation: non-PDF files (e.g. `company_logo.png` or files lacking `%PDF-` header) are instantly rejected with clear bilingual alerts.
   - Enforcement of maximum 30 files and 50 MB total limit.
   - Safe handling of damaged or encrypted PDFs without crashing.
   - Individual removal of any uploaded file.

3. **Document Matching (4.3):**
   - Intuitive dropdown for assigning uploaded files to tender requirements.
   - Enforces strict 1-to-1 matching rules (one document gets at most one file; one file goes to at most one document).
   - Flexible editing: change or undo matches with single-click remove buttons.

4. **Expiry Date Verification (4.4 & 5):**
   - Automatic conditional display of expiry date input for documents where `has_expiry = true`.
   - Real-time comparison against the tender's `submission_deadline`.
   - Correctly enforces that expiry dates on the exact day of the deadline remain valid (`OK`).

5. **Instant Status Engine (4.5 & 5):**
   - Dynamically calculates and displays exactly one color-coded status badge per requirement:
     - **Missing:** Required document with no file matched (Blocks package).
     - **Expiry date needed:** File matched to expiry-tracked requirement but no date provided (Blocks package).
     - **Expired:** Expiry date is strictly before submission deadline (Blocks package).
     - **Not provided:** Optional document with no file matched (Does not block).
     - **OK:** File matched and expiry date valid / on or after submission deadline (Does not block).
   - Instant live updates across all status badges and header summary statistics upon any modification.

6. **Content Duplicate Detection (4.6):**
   - Calculates cryptographic SHA-256 hashes of all uploaded file contents.
   - Automatically detects identical files regardless of filename (e.g. `experience_cert.pdf` and `experience_cert (1).pdf`).
   - Visually flags duplicates in the uploaded file manager.
   - Prohibits duplicate files from being assigned across different required documents.

7. **Smart Package Generation & Guardrails (4.7 & 6):**
   - Disables the "Generate Package" button whenever blocking issues exist, with an explicit itemized breakdown of blocking issues.
   - Enables generation with verified feedback once all blocking issues are resolved.
   - **Section 6 Compliance:**
     - **Cover Page (6.1):** Clean English cover page containing Tender ID, Title, Procuring Entity, Bidder Name, Submission Deadline, Package Creation Date, and ordered list of included documents with page counts.
     - **Document Sequence (6.2):** Retains original multi-page documents in their correct requirement order, omitting non-provided optional documents.
     - **Footer (6.3 & 6.4):** Imprints `<tender_id> | Page X of Y` across every page (including cover) on a dedicated, non-obscuring bottom margin.

8. **Package Download (4.8):**
   - Automatically prompts download as `<tender_id>_Package.pdf` (e.g., `T-2026-0417_Package.pdf`) with live preview option.

9. **Bilingual English & Bengali Localization (4.9):**
   - Complete bilingual toggle supporting natural Bengali and English translations.
   - Dynamic document title switching (`title_en` vs `title_bn`).

---

## 3. Bonus Features Implemented (Problem Statement Section 7)

- **Smart Auto-Match:** One-click intelligent matching algorithm that matches filenames to requirements and favors valid certificates over expired ones.
- **Demo Sample Pack Loader:** 1-click demo button that instantly loads sample tender requirements and prepares testing.
- **Export Checklist (CSV):** Exports a complete audit-ready CSV checklist of all requirements, matched files, page counts, expiry dates, and statuses.
- **Index Page / Table of Contents:** Optional checkbox to generate a dedicated Table of Contents page right after the cover.
- **Save & Restore Workspace:** LocalStorage persistence alongside JSON project file export/import.
- **Digital Seal & Signature:** Supports uploading a PNG seal or signature image stamped onto document packages.
- **Graceful Error Handling:** Protects against corrupted, damaged, or password-protected PDF files.

---

## 4. Known Problems

- In very rare instances where a scanned PDF contains malformed xref tables, `pdf-lib` safely catches the error and alerts the user rather than crashing the interface.
- Standard PDF Helvetica font embedding adheres strictly to ASCII/WinAnsi characters; English is used on the cover page in accordance with Section 6.1.

---

## 5. AI Tools Used

- **Google Antigravity Agent (Gemini 3.8 Flash High):** Used for architecture design, frontend implementation, rule validation, Bengali localization, testing, and deployment workflows.

---

## 6. Most Useful Prompt

> *"Build a complete, browser-only Tender Document Package Builder web app in index.html matching all requirements in Sections 4, 5, and 6 of the problem statement. Ensure strict duplicate file prevention via SHA-256 hash, live status verification against submission deadline, disabled generation with explicit blocking reasons, cover page assembly in English with non-overlapping footer '<tender_id> | Page X of Y', full English/Bangla localization, and bonus tasks including auto-matching, CSV checklist export, and project saving."*
