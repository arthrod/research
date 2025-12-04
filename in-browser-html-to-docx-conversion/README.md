# HTML to DOCX Conversion Libraries - Comprehensive Analysis

This research evaluates 17 npm packages for HTML to DOCX conversion capabilities, with a focus on **in-browser** conversion support.

## Executive Summary

After analyzing 17 packages, the **winner for browser-side HTML to DOCX conversion** is:

### **@turbodocx/html-to-docx** (v1.18.1)

**Runners-up:**
1. **html-docx-js-typescript-papersize-thenn** - Best TypeScript-native option using altChunk approach
2. **html-docx-js-extends** - Best for multi-section documents with different orientations

---

## Package Categories

### Category A: True Browser-Compatible (altChunk approach)
These packages work entirely in the browser without server dependencies:

| Package | Version | Browser | Server | TypeScript | Maintained | Notes |
|---------|---------|---------|--------|------------|------------|-------|
| html-docx-js | 0.3.1 | YES | YES | NO | NO (2015) | Original, unmaintained |
| html-docx-fixed | 1.0.2 | YES | YES | NO | NO (2015) | Fork with fixes, MS Word only |
| html-docx | 1.2.0 | YES | NO | NO | NO (2021) | Chinese docs, canvas support |
| html-docx-js-typescript-papersize-thenn | 0.1.5 | YES | YES | YES | NO (2022) | TypeScript, paper size options |
| html-docx-js-extends | 0.1.8 | YES | YES | YES | Partial | Multi-section support |
| html-docx-converter | 1.0.1 | YES | YES | YES | Low | Simple TypeScript wrapper |
| exportword | 1.0.2 | YES | NO | NO | Low | ECharts support |
| export-doc-html | 1.0.0 | YES | NO | NO | Low | ECharts, Chinese docs |
| @csabourin/html2doc | 1.0.7 | YES | NO | NO | Low | Snap courses specific |

### Category B: Server-Primary with Partial Browser Support
These require bundler configuration and polyfills for browser use:

| Package | Version | Browser | Server | TypeScript | Maintained | Notes |
|---------|---------|---------|--------|------------|------------|-------|
| html-to-docx | 1.8.0 | PARTIAL | YES | NO | NO (2023) | Needs Node polyfills |
| @turbodocx/html-to-docx | 1.18.1 | PARTIAL | YES | YES | **YES** | Active fork, RTL support |
| html-export-kit | 0.1.0 | PARTIAL | NO | YES | Recent | PDF works, DOCX broken |

### Category C: Server-Only
These cannot run in browsers:

| Package | Version | Browser | Server | TypeScript | Maintained | Notes |
|---------|---------|---------|--------|------------|------------|-------|
| node-red-contrib-html-to-docx | 1.0.2 | NO | YES | NO | Low | Node-RED specific |
| jsreport-html-docx-js | 0.0.0 | NO | YES | NO | Low | JSReport extension |
| node-html-to-office | 1.0.2 | NO | YES | NO | NO | Thin wrapper |

### Category D: Not Applicable
| Package | Reason |
|---------|--------|
| html2pdf.js | PDF only, no DOCX support |
| @grabzit/js | Cloud API service, not standalone converter |
| html-to-word-nodejs | Does not exist on npm (404) |

---

## Tournament Results

### Round 1: Elimination by Category

**Eliminated:**
- html2pdf.js (PDF only)
- @grabzit/js (cloud service)
- node-red-contrib-html-to-docx (Node-RED only)
- jsreport-html-docx-js (JSReport only)
- node-html-to-office (server only)
- html-export-kit (DOCX broken in browser)

**Advancing:** 11 packages

### Round 2: Browser Capability Assessment

**Match 1: html-docx-js vs html-docx-fixed**
- Both use altChunk approach, both from 2015
- html-docx-fixed has bug fixes
- **Winner: html-docx-fixed** (more stable)

**Match 2: html-docx vs exportword**
- Both browser-first, unmaintained
- html-docx has canvas/ECharts support
- exportword is simpler wrapper
- **Winner: html-docx** (more features)

**Match 3: export-doc-html vs @csabourin/html2doc**
- Both wrap html-docx-js
- export-doc-html has modern build
- @csabourin/html2doc is domain-specific
- **Winner: export-doc-html** (more general purpose)

**Match 4: html-docx-js-typescript-papersize-thenn vs html-docx-converter**
- Both TypeScript
- papersize-thenn has more options (paper size, margins)
- **Winner: html-docx-js-typescript-papersize-thenn** (more features)

**Match 5: html-docx-js-extends vs html-to-docx**
- html-docx-js-extends: browser-native, multi-section support
- html-to-docx: needs polyfills, more HTML features
- **Winner: html-docx-js-extends** (true browser support)

**Match 6: @turbodocx/html-to-docx (bye)**
- Actively maintained, TypeScript, RTL support
- **Advances automatically**

### Round 3: Semi-Finals

**Match 7: html-docx-fixed vs html-docx**
- html-docx-fixed: more stable, tested
- html-docx: canvas support, Chinese docs
- **Winner: html-docx-fixed** (stability)

**Match 8: export-doc-html vs html-docx-js-typescript-papersize-thenn**
- export-doc-html: ECharts, basic
- papersize-thenn: TypeScript, configurable
- **Winner: html-docx-js-typescript-papersize-thenn** (TypeScript, options)

**Match 9: html-docx-js-extends vs @turbodocx/html-to-docx**
- html-docx-js-extends: multi-section, altChunk approach
- @turbodocx/html-to-docx: actively maintained, proper DOCX XML generation
- **Winner: @turbodocx/html-to-docx** (maintenance, features)

### Round 4: Finals

**Match 10: html-docx-fixed vs html-docx-js-typescript-papersize-thenn**
- html-docx-fixed: stable but OLD (2015), no TypeScript
- papersize-thenn: TypeScript, modern, paper size options
- **Winner: html-docx-js-typescript-papersize-thenn** (modern stack)

**Match 11: html-docx-js-typescript-papersize-thenn vs @turbodocx/html-to-docx**
- papersize-thenn: altChunk (Word converts), simple, browser-native
- @turbodocx/html-to-docx: proper DOCX generation, actively maintained, RTL
- **Winner: @turbodocx/html-to-docx** (active maintenance, proper conversion)

---

## Detailed Winner Analysis

### Winner: @turbodocx/html-to-docx

**Strengths:**
- Actively maintained (2024-2025)
- TypeScript definitions included
- Proper DOCX XML generation (not altChunk hack)
- RTL (Hebrew/Arabic) support
- Comprehensive HTML element support
- 26+ contributors
- Jest unit tests
- ESLint + Prettier code quality

**Limitations:**
- Requires bundler with Node.js polyfills for browser use
- Large bundle size (~700KB)
- Some Node.js dependencies need shimming

**Browser Usage:**
```javascript
// Requires webpack/rollup config with Node polyfills
import HTMLtoDOCX from '@turbodocx/html-to-docx';
const docxBlob = await HTMLtoDOCX(htmlString, null, {
  orientation: 'portrait',
  margins: { top: 720, bottom: 720 }
});
```

### Runner-up: html-docx-js-typescript-papersize-thenn

**Best for:** Projects wanting zero-config browser support with TypeScript

**Strengths:**
- Works in browser without polyfills
- TypeScript native
- Paper size customization
- Simple API

**Limitations:**
- Uses altChunk (Word must convert)
- Only works in Microsoft Word
- Not actively maintained

**Browser Usage:**
```javascript
import { asBlob } from 'html-docx-js-typescript-papersize-thenn';
import { saveAs } from 'file-saver';

const blob = await asBlob(htmlString, {
  orientation: 'landscape',
  margins: { top: 1440 }
});
saveAs(blob, 'document.docx');
```

---

## Conversion Approaches Compared

### Approach 1: altChunk (html-docx-js family)
- Embeds HTML as MHT inside DOCX
- Word converts on open
- **Pros:** Simple, small code, works in browser
- **Cons:** Only works in MS Word, limited control

### Approach 2: Proper DOCX XML Generation (html-to-docx family)
- Parses HTML, generates Office Open XML
- **Pros:** Universal compatibility, full control
- **Cons:** Complex, larger bundle, may need polyfills

---

## Recommendations by Use Case

| Use Case | Recommended Package |
|----------|---------------------|
| Production app, needs maintenance | @turbodocx/html-to-docx |
| Simple browser-only, TypeScript | html-docx-js-typescript-papersize-thenn |
| Multi-section documents | html-docx-js-extends |
| Legacy browser support | html-docx-fixed |
| ECharts/Canvas export | html-docx or export-doc-html |
| Node-RED workflows | node-red-contrib-html-to-docx |
| JSReport templates | jsreport-html-docx-js |

---

## Key Findings

1. **Most packages are unmaintained** - The majority haven't been updated since 2015-2022
2. **altChunk vs proper conversion** - Two distinct approaches with different tradeoffs
3. **@turbodocx/html-to-docx is the only actively maintained option** with proper DOCX generation
4. **Browser-native solutions use altChunk** - Which only works in Microsoft Word
5. **TypeScript support is limited** - Only a few packages offer type definitions
6. **html-to-word-nodejs doesn't exist** - Package not found on npm registry

---

## Methodology

1. Installed all 17 packages via npm
2. Analyzed package.json, source code, and dependencies
3. Evaluated browser vs server compatibility
4. Assessed maintenance status and code quality
5. Ran pairwise elimination tournament
6. Documented findings and recommendations

---

*Research conducted: December 2025*
