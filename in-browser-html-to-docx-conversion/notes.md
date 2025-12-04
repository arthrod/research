# Research Notes: HTML to DOCX Conversion Libraries

## Goal
Evaluate and compare npm packages for HTML to DOCX conversion, focusing on browser-side and server-side capabilities.

## Methodology
1. Install all 18 packages using npm (bun had registry auth issues)
2. Copy packages from node_modules to organized folder structure
3. Analyze each package individually via subagents
4. Run pairwise elimination tournament comparisons
5. Compile final report with winner

## Progress Log

### Session Start
- Created project folder: `in-browser-html-to-docx-conversion`
- Created `files_list.md` with all 18 packages listed
- Starting package installation...

### Package Installation
- Installed 17 packages successfully via npm
- **Note:** `html-to-word-nodejs` does NOT exist on npm registry (404 error)
- Packages copied to `packages/` folder for analysis

### Packages Successfully Installed
1. html-export-kit
2. html-to-docx
3. html2pdf.js
4. node-red-contrib-html-to-docx
5. jsreport-html-docx-js
6. html-docx-fixed
7. html-docx
8. html-docx-js
9. exportword
10. export-doc-html
11. node-html-to-office
12. html-docx-converter
13. @csabourin/html2doc
14. html-docx-js-extends
15. html-docx-js-typescript-papersize-thenn
16. @turbodocx/html-to-docx
17. @grabzit/js

### Individual Package Analysis

**Analysis completed for all 17 packages:**

1. **html-export-kit** - PARTIAL browser (PDF works, DOCX broken due to Node.js deps in html-to-docx)
2. **html-to-docx** - PARTIAL browser (needs bundler+polyfills), full server support
3. **html2pdf.js** - PDF ONLY, no DOCX support (not relevant)
4. **node-red-contrib-html-to-docx** - SERVER ONLY (Node-RED specific)
5. **jsreport-html-docx-js** - SERVER ONLY (JSReport extension)
6. **html-docx-fixed** - YES browser, but OLD (2015), MS Word only
7. **html-docx** - YES browser, unmaintained (2021), canvas/ECharts support
8. **html-docx-js** - YES browser, VERY OLD (2015), altChunk approach
9. **exportword** - YES browser, wraps html-docx-js
10. **export-doc-html** - YES browser, wraps html-docx-js, ECharts support
11. **node-html-to-office** - SERVER ONLY (Node.js wrapper)
12. **html-docx-converter** - YES browser, TypeScript wrapper for html-docx-js
13. **@csabourin/html2doc** - YES browser, domain-specific (Snap courses)
14. **html-docx-js-extends** - YES browser, TypeScript, multi-section documents
15. **html-docx-js-typescript-papersize-thenn** - YES browser, TypeScript, paper size options
16. **@turbodocx/html-to-docx** - PARTIAL browser (needs polyfills), ACTIVELY MAINTAINED
17. **@grabzit/js** - Cloud API service (not standalone converter)

### Key Technical Findings

**Two Conversion Approaches Discovered:**

1. **altChunk Approach** (html-docx-js family)
   - Embeds HTML as MHT inside DOCX ZIP
   - Microsoft Word converts on open
   - Pros: Simple, browser-native, small bundle
   - Cons: Only works in MS Word (not LibreOffice/Google Docs)

2. **Proper DOCX XML Generation** (html-to-docx family)
   - Parses HTML, generates Office Open XML
   - Pros: Universal compatibility
   - Cons: Complex, larger bundle, needs Node polyfills for browser

### Tournament Results

**Winner:** @turbodocx/html-to-docx (v1.18.1)
- Actively maintained (2024-2025)
- TypeScript definitions
- Proper DOCX generation
- RTL support
- 26+ contributors

**Runner-up:** html-docx-js-typescript-papersize-thenn
- Best for zero-config browser support
- TypeScript native
- Uses altChunk (MS Word only)

### Lessons Learned

1. Most HTML-to-DOCX packages are abandoned (last updates 2015-2022)
2. Browser-native solutions all use the altChunk hack
3. True DOCX generation requires Node.js modules that need browser polyfills
4. @turbodocx/html-to-docx is the only actively maintained option
5. html-to-word-nodejs package doesn't exist despite being in search results

## Files Created
- `files_list.md` - Package tracking list
- `notes.md` - This research log
- `README.md` - Final comprehensive report
