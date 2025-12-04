# HTML to DOCX Conversion Libraries: Comprehensive Analysis

## Executive Summary

This research evaluated **27 npm packages** for converting HTML to DOCX format, with focus on browser and server compatibility. After thorough analysis and tournament-style elimination, we identified clear winners for different use cases.

### Top Recommendations

| Rank | Package | Use Case | Browser | Node.js |
|------|---------|----------|---------|---------|
| 1 | **@turbodocx/html-to-docx** | General purpose, RTL support | Yes | Yes |
| 2 | **@packback/html-to-docx** | TypeScript projects, minimal deps | Bundler | Yes |
| 3 | **html-to-docx-lite** | Modern Vite projects | Yes | Yes |
| 4 | **prosemirror-docx** | ProseMirror editors | Yes | Yes |

---

## Methodology

1. Installed all 27 packages via npm
2. Analyzed each package for: version, author, license, dependencies, browser/server support, conversion approach, code quality
3. Categorized packages by conversion technique
4. Conducted tournament-style elimination within categories
5. Final head-to-head comparison of category winners

---

## Package Categories

### Category 1: altChunk/MHT-based (17 packages)

These packages embed HTML as MHT (MHTML) inside DOCX using Microsoft Word's `altChunk` feature.

**How it works:**
1. Converts HTML to MHTML format
2. Creates minimal DOCX structure with JSZip
3. Embeds MHTML as an "alternate chunk"
4. Word converts the HTML when opening the file

**Limitations:**
- Only works with Microsoft Word 2007+
- Does NOT work with LibreOffice, Google Docs, Pages
- Relies on Word to do actual conversion

**Packages:**
- html-docx-js (original, 2015)
- html-docx-fixed, html-docx-js-typescript, html-docx-ts
- html-docx-js-extends, html-docx-js-a13, html-docx
- And 10 more forks/variants...

**Best in Category:** `html-docx-js-extends` - TypeScript, multi-section support, headers/footers

### Category 2: Native OOXML Generation (7 packages)

These packages generate proper Office Open XML documents that work everywhere.

**How it works:**
1. Parses HTML to Virtual DOM or AST
2. Maps HTML elements to WordprocessingML
3. Generates valid OOXML structure
4. Creates ZIP archive with all required XML files

**Benefits:**
- Works with MS Word, LibreOffice, Google Docs
- Full control over document structure
- No external conversion needed

**Packages:**
- html-to-docx (original by privateOmega)
- @turbodocx/html-to-docx (actively maintained fork)
- @packback/html-to-docx (uses docx library)
- html-to-docx-lite, html-to-docx-typescript
- @mark-beeby/html-to-docx, @adalat-ai/html-to-docx

**Best in Category:** `@turbodocx/html-to-docx` - Most features, RTL support, active maintenance

### Category 3: Specialized (2 packages)

- **prosemirror-docx**: Exports ProseMirror documents to DOCX (not HTML)
- **@ckeditor/ckeditor5-export-word**: CKEditor 5 plugin, requires cloud services

### Category 4: Types Only (1 package)

- **@types/html-docx-js**: TypeScript definitions for html-docx-js

---

## Detailed Package Comparison

### Top Tier (Recommended)

| Package | Version | Approach | TypeScript | Browser | RTL | Tables | Images | Tests |
|---------|---------|----------|------------|---------|-----|--------|--------|-------|
| @turbodocx/html-to-docx | 1.18.1 | OOXML | No | UMD/ESM | Yes | Yes | axios | Jest |
| @packback/html-to-docx | 1.4.2 | OOXML (docx) | Yes | Bundler | No | Yes | docx | Jest |
| html-to-docx-lite | 2.0.1 | OOXML | No | Vite | No | Yes | Yes | No |
| prosemirror-docx | 0.6.1 | OOXML (docx) | Yes | Yes | No | Yes | Yes | Vitest |

### Mid Tier (Viable Alternatives)

| Package | Version | Approach | TypeScript | Notes |
|---------|---------|----------|------------|-------|
| html-to-docx | 1.8.0 | OOXML | No | Original, less active now |
| html-docx-js-extends | 0.1.8 | altChunk | Yes | Multi-section, MS Word only |
| html-to-docx-typescript | 1.3.2 | OOXML | Yes | TypeScript port of html-to-docx |
| @mark-beeby/html-to-docx | 1.6.4-rc.63 | OOXML | No | Table column widths support |

### Legacy Tier (Use with Caution)

| Package | Version | Notes |
|---------|---------|-------|
| html-docx-js | 0.3.1 | Original altChunk library, 2015 |
| html-docx-js-typescript | 0.1.5 | TypeScript port, no updates since 2020 |
| html-docx-ts | 0.0.5 | Header/footer support |
| html-docx-js-a13 | 1.3.3 | Bundled UMD, minimal |
| Other forks... | Various | Minor variations, mostly inactive |

---

## Winner Analysis: @turbodocx/html-to-docx

### Why It Wins

1. **Most Active Maintenance**: v1.18.1 with regular updates, 20+ contributors
2. **RTL Language Support**: Unique feature for Hebrew, Arabic content
3. **Comprehensive HTML Support**: h1-h6, p, lists, tables, images, links, blockquotes
4. **Browser Ready**: UMD and ESM builds included
5. **Unit Tested**: Jest test suite included
6. **Feature Rich**: Headers, footers, page numbering, custom margins, line numbers

### Installation

```bash
npm install @turbodocx/html-to-docx
```

### Basic Usage

```javascript
import HTMLtoDOCX from '@turbodocx/html-to-docx';

const html = '<h1>Hello World</h1><p>This is a paragraph.</p>';

const docxBlob = await HTMLtoDOCX(html, null, {
  table: { row: { cantSplit: true } },
  footer: true,
  pageNumber: true,
});

// Save blob as .docx file
```

### Supported Elements

- Headings: h1, h2, h3, h4, h5, h6
- Text: p, strong, b, i, em, u, br, span
- Lists: ol, ul, li (with various list-style-types)
- Tables: table, thead, tbody, tr, th, td (with colspan/rowspan)
- Media: img (base64 and URLs)
- Links: a (href)
- Other: blockquote, pre, code

---

## Runner-Up: @packback/html-to-docx

### Why Consider It

1. **Clean Architecture**: Uses the `docx` library under the hood
2. **TypeScript Native**: Full type definitions
3. **Minimal Dependencies**: Just 1 runtime dependency (docx)
4. **CLI Included**: Command-line interface for quick conversions
5. **Modern Node.js**: Requires Node 18+

### Installation

```bash
npm install @packback/html-to-docx
```

### Basic Usage

```typescript
import { HtmlToDocx } from '@packback/html-to-docx';

const converter = new HtmlToDocx();
const html = '<h1>Title</h1><p>Content</p>';
const docxBuffer = await converter.convert(html);
```

---

## Special Cases

### For ProseMirror Users: prosemirror-docx

```typescript
import { defaultDocxSerializer } from 'prosemirror-docx';
import { Document, Packer } from 'docx';

const docx = defaultDocxSerializer.serialize(prosemirrorNode, {
  document: { title: 'My Document' }
});
const buffer = await Packer.toBuffer(docx);
```

### For CKEditor Users: @ckeditor/ckeditor5-export-word

Note: Requires CKEditor 5 and CKEditor Cloud Services subscription.

### For MS Word-Only Environments: html-docx-js-extends

If you only need to support Microsoft Word and want simpler code:

```typescript
import { asBlob, createWord } from 'html-docx-js-extends';

// Simple conversion
const blob = await asBlob(htmlString, {
  orientation: 'portrait',
  margins: { top: 1440 }
});

// Multi-section document
const word = createWord('document.docx');
word.addSection(html1, { orientation: 'portrait' });
word.addSection(html2, { orientation: 'landscape' });
const blob = await word.build();
```

---

## Decision Matrix

| If You Need... | Use This |
|----------------|----------|
| Universal compatibility | @turbodocx/html-to-docx |
| RTL language support | @turbodocx/html-to-docx |
| TypeScript + minimal deps | @packback/html-to-docx |
| Vite/modern tooling | html-to-docx-lite |
| ProseMirror integration | prosemirror-docx |
| CKEditor integration | @ckeditor/ckeditor5-export-word |
| MS Word only + simple | html-docx-js-extends |
| Legacy browser support | html-docx-js (with caveats) |

---

## Key Findings

1. **altChunk is obsolete**: The legacy approach (html-docx-js and forks) only works with MS Word. Use native OOXML generation instead.

2. **Fork fragmentation**: html-docx-js spawned 15+ forks with minimal differences. html-to-docx has 5+ active forks.

3. **@turbodocx is the clear winner**: Most active, most features, best compatibility.

4. **TypeScript adoption is incomplete**: Many packages are still JavaScript-only or have outdated TypeScript.

5. **Testing varies widely**: Only top-tier packages have meaningful test suites.

---

## Files in This Research

- `README.md` - This report
- `notes.md` - Detailed research notes and tournament brackets
- `files_list.md` - Complete package inventory
- `packages/` - Copied package sources for analysis

---

## Conclusion

For new projects requiring HTML to DOCX conversion:

**Use `@turbodocx/html-to-docx`** for general-purpose conversion with maximum compatibility and features.

**Use `@packback/html-to-docx`** if TypeScript support and minimal dependencies are priorities.

Avoid the legacy altChunk-based packages (html-docx-js and its many forks) unless you specifically only need Microsoft Word support and want simpler code.
