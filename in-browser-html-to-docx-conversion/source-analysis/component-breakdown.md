# @turbodocx/html-to-docx Component Breakdown

## Overview

This analysis breaks down the `@turbodocx/html-to-docx` package (v1.18.1) to understand what's being used, what's optional, and what can be removed to reduce package size.

**Total Source Files:** 32 files
**Total Source Lines:** ~7,565 lines
**NPM Dependencies:** 11 runtime dependencies

---

## Dependency Graph

```
html-to-docx.js (Entry Point)
├── docx-document.js (Document Assembly)
│   ├── schemas/* (XML Templates)
│   │   ├── content-types.js
│   │   ├── core.js
│   │   ├── document-rels.js
│   │   ├── document.template.js
│   │   ├── font-table.js
│   │   ├── generic-rels.js
│   │   ├── numbering.js
│   │   ├── rels.js
│   │   ├── settings.js
│   │   ├── styles.js
│   │   ├── theme.js
│   │   └── web-settings.js
│   ├── utils/image.js (Image Processing)
│   ├── namespaces.js
│   └── constants.js
├── helpers/render-document-file.js (HTML→XML Conversion)
│   ├── helpers/html-parser.js (HTML to VDOM)
│   │   └── vdom/index.js (VNode/VText Classes)
│   ├── helpers/xml-builder.js (XML Generation - LARGEST FILE)
│   │   ├── utils/color-conversion.js
│   │   ├── utils/unit-conversion.js
│   │   ├── utils/font-family-conversion.js
│   │   ├── utils/vnode.js
│   │   ├── utils/url.js
│   │   └── utils/truthy-check.js
│   └── utils/options-utils.js
└── jszip (Document Packaging)
```

---

## Component Analysis

### 1. ESSENTIAL CORE (Cannot Be Removed)

| File | Lines | Purpose | Required By |
|------|-------|---------|-------------|
| `html-to-docx.js` | 143 | Entry point, ZIP assembly | - |
| `docx-document.js` | 641 | Document class, relationship management | Entry point |
| `helpers/render-document-file.js` | 620 | HTML→XML conversion engine | Entry point |
| `helpers/xml-builder.js` | **4,037** | Core XML element building | render-document-file |
| `helpers/html-parser.js` | 391 | HTML→VDOM parsing | render-document-file |
| `vdom/index.js` | 144 | VNode/VText classes | html-parser |
| `constants.js` | 246 | Configuration defaults | Multiple |
| `namespaces.js` | 42 | XML namespace definitions | Multiple |

**Core Total: ~6,264 lines (83% of codebase)**

### 2. SCHEMA TEMPLATES (Required but Potentially Simplifiable)

| File | Lines | Purpose | Can Simplify? |
|------|-------|---------|---------------|
| `schemas/content-types.js` | 24 | DOCX content type declarations | No |
| `schemas/core.js` | 45 | Document metadata (title, author) | Yes - hardcode values |
| `schemas/document-rels.js` | 16 | Document relationships | No |
| `schemas/document.template.js` | 60 | Base document XML template | No |
| `schemas/font-table.js` | 45 | Font declarations | Yes - if single font |
| `schemas/generic-rels.js` | 15 | Header/footer relationships | No |
| `schemas/numbering.js` | 18 | List numbering template | No |
| `schemas/rels.js` | 13 | Package relationships | No |
| `schemas/settings.js` | 15 | Document settings | No |
| `schemas/styles.js` | 121 | Heading/paragraph styles | Yes - if no headings |
| `schemas/theme.js` | **199** | Office theme (colors, fonts) | **Yes - can hardcode** |
| `schemas/web-settings.js` | 8 | Web settings | No |

**Schema Total: ~579 lines (8% of codebase)**

### 3. UTILITY MODULES (Required)

| File | Lines | Purpose | Can Remove? |
|------|-------|---------|-------------|
| `utils/unit-conversion.js` | 62 | px/pt/cm/inch → TWIP/EMU | No |
| `utils/color-conversion.js` | 61 | RGB/HSL/Hex conversion | No |
| `utils/font-family-conversion.js` | 18 | Font family parsing | No |
| `utils/vnode.js` | 3 | VNode child checker | No |
| `utils/url.js` | 8 | URL validation | No |
| `utils/truthy-check.js` | ~5 | Zero/truthy check | No |
| `utils/xml-escape.js` | 9 | XML special char escaping | No |
| `utils/options-utils.js` | 94 | Options normalization | No |

**Utility Total: ~260 lines (3% of codebase)**

### 4. IMAGE PROCESSING (OPTIONAL)

| File | Lines | Purpose | Can Remove? |
|------|-------|---------|-------------|
| `utils/image.js` | **409** | Image download, caching, SVG handling | **YES** |

**Image Features:**
- URL image download with retry logic
- LRU caching to prevent duplicate downloads
- Base64 encoding/decoding
- MIME type detection from magic bytes
- SVG dimension parsing
- SVG→PNG conversion (requires `sharp`)

**If you DON'T need images, you can:**
1. Remove `utils/image.js` entirely (-409 lines)
2. Remove image handling from `render-document-file.js` (~100 lines)
3. Remove image handling from `xml-builder.js` (~200 lines)
4. Remove `axios` dependency (for URL downloads)
5. Remove `lru-cache` dependency
6. Remove `image-size` dependency

**Estimated savings: ~700 lines of code + 3 npm dependencies**

---

## NPM Dependencies Analysis

| Dependency | Size (approx) | Purpose | Can Remove? |
|------------|---------------|---------|-------------|
| `xmlbuilder2` | ~150KB | XML generation | No (core) |
| `jszip` | ~100KB | ZIP file creation | No (core) |
| `htmlparser2` | ~80KB | HTML parsing | No (core) |
| `lodash` | **~500KB** | `cloneDeep` only | **PARTIAL** |
| `html-entities` | ~15KB | HTML entity decoding | No (core) |
| `html-minifier-terser` | ~100KB | HTML preprocessing | **YES** |
| `axios` | ~50KB | HTTP requests for images | **YES** (if no remote images) |
| `lru-cache` | ~20KB | Image caching | **YES** (if no images) |
| `image-size` | ~30KB | Image dimension detection | **YES** (if no images) |
| `mime-types` | ~50KB | MIME type lookup | **YES** (if no images) |
| `nanoid` | ~1KB | Unique ID generation | No (tiny) |
| `color-name` | ~5KB | CSS color name lookup | No (core) |

### Dependency Reduction Opportunities

1. **Replace `lodash` with specific functions** (-500KB)
   - Only uses `cloneDeep` - can use native `structuredClone()` or a small polyfill

2. **Remove `html-minifier-terser`** (-100KB)
   - Only used in preprocessing (can be skipped via `skipHTMLMinify: true`)

3. **Remove image dependencies if not needed** (-150KB)
   - `axios`, `lru-cache`, `image-size`, `mime-types`

---

## OPTIONAL FEATURES (Can Be Stripped)

### Feature: RTL (Right-to-Left) Support
**You mentioned you don't need RTL.**

Located in:
- `xml-builder.js`: ~50 lines handling `direction: 'rtl'`
- `docx-document.js`: direction property handling
- `constants.js`: `defaultDirection: 'ltr'`

**Savings: ~50-100 lines**

### Feature: Line Numbering
Located in:
- `docx-document.js`: `lineNumber`, `lineNumberOptions`
- `xml-builder.js`: line number XML generation

**Savings: ~30 lines**

### Feature: Headers/Footers
Located in:
- `docx-document.js`: `generateHeaderXML`, `generateFooterXML`
- `schemas/generic-rels.js`
- Multiple schema files

**Savings: ~150 lines**

### Feature: Custom Heading Styles
Located in:
- `schemas/styles.js`: ~80 lines for heading1-6 styles
- `constants.js`: `defaultHeadingOptions`

**Savings: ~100 lines if you only need basic paragraphs**

### Feature: SVG Image Support
Located in:
- `utils/image.js`: `convertSVGtoPNG`, `parseSVGDimensions`
- `constants.js`: `SVG_UNIT_TO_PIXEL_CONVERSIONS`, `svgHandling` option

**Savings: ~100 lines + optional `sharp` dependency**

---

## SIZE REDUCTION STRATEGIES

### Strategy 1: Minimal Build (No Images)
Remove all image handling if you only convert text/tables.

**Remove:**
- `utils/image.js` (409 lines)
- Image-related code in `xml-builder.js` (~200 lines)
- Image-related code in `render-document-file.js` (~100 lines)
- Dependencies: `axios`, `lru-cache`, `image-size`, `mime-types`

**Estimated savings: 30-40% code reduction**

### Strategy 2: Replace Lodash
Replace `lodash` with:
```javascript
// Instead of: import { cloneDeep } from 'lodash';
// Use: structuredClone(obj) // Modern browsers + Node 17+
// Or: JSON.parse(JSON.stringify(obj)) // For simple objects
```

**Estimated savings: ~500KB from bundle**

### Strategy 3: Skip HTML Minification
Set `preprocessing.skipHTMLMinify: true` and remove `html-minifier-terser`.

**Estimated savings: ~100KB from bundle**

### Strategy 4: Inline Schemas
Hardcode XML templates instead of generating them dynamically if your use case is fixed.

**Estimated savings: ~300 lines**

---

## THE LARGEST FILE: xml-builder.js (4,037 lines)

This is 53% of the source code. It handles:

### Exported Functions:
```javascript
export {
  buildParagraph,      // ~800 lines - Text, inline styles, links
  buildTable,          // ~600 lines - Table structure
  buildNumberingInstances, // ~100 lines - List numbering
  buildLineBreak,      // ~20 lines
  buildIndentation,    // ~50 lines
  buildTextElement,    // ~100 lines
  buildBold,           // ~20 lines
  buildItalics,        // ~20 lines
  buildUnderline,      // ~20 lines
  processImageSource,  // ~100 lines - Image processing
  buildDrawing,        // ~400 lines - Image/drawing XML
  fixupLineHeight,     // ~30 lines
};
```

### Internal Functions (supporting the above):
- Border handling: ~300 lines
- Color parsing: ~150 lines
- Font/style handling: ~200 lines
- Table cell/row processing: ~500 lines
- Image dimension calculations: ~200 lines

### What CANNOT be removed from xml-builder.js:
- `buildParagraph` - Core functionality
- `buildTextElement` - Core functionality
- Color/font utilities - Used everywhere

### What CAN be removed if not needed:
- `buildTable` + table utilities (~600 lines) - if no tables
- `buildDrawing` + image utilities (~500 lines) - if no images
- `buildNumberingInstances` (~100 lines) - if no lists

---

## RECOMMENDED MINIMAL CONFIGURATION

For your use case ("works every time" + "comprehensive" without RTL):

```javascript
const options = {
  // Skip preprocessing to remove html-minifier-terser dependency
  preprocessing: {
    skipHTMLMinify: true
  },
  // Skip image processing if not needed
  imageProcessing: {
    // Or remove image code entirely
  },
  // Use default LTR (RTL code still present but not executed)
  direction: 'ltr'
};
```

---

## FILE-BY-FILE DEPENDENCY MATRIX

| File | Depends On | Depended By |
|------|------------|-------------|
| `html-to-docx.js` | docx-document, schemas, render-document-file, jszip | - |
| `docx-document.js` | schemas, namespaces, constants, utils/image | html-to-docx |
| `render-document-file.js` | html-parser, xml-builder, vdom, image, lru-cache | html-to-docx, docx-document |
| `xml-builder.js` | vdom, image, constants, all utils | render-document-file |
| `html-parser.js` | vdom, html-entities, htmlparser2 | render-document-file |
| `vdom/index.js` | - | html-parser, xml-builder, render-document-file |
| `utils/image.js` | constants, axios, mime-types | xml-builder, render-document-file, docx-document |
| `constants.js` | lodash | Nearly everything |
| `namespaces.js` | - | schemas, xml-builder, render-document-file |

---

## CONCLUSION

The package is well-structured but has significant size due to:

1. **xml-builder.js** (4,037 lines / 53%) - The core conversion engine, difficult to reduce
2. **Image handling** (700+ lines across multiple files) - Can be removed if not needed
3. **Heavy dependencies** (lodash, html-minifier-terser) - Can be replaced/removed

### Quick Wins for Size Reduction:
1. Replace `lodash` with `structuredClone` (saves ~500KB)
2. Remove `html-minifier-terser` with `skipHTMLMinify: true` (saves ~100KB)
3. If no images: remove 4 dependencies + 700 lines of code (saves ~200KB)

### Estimated Total Potential Savings:
- **Dependencies:** ~800KB
- **Source code:** ~25-40% reduction (if images not needed)

The "essential core" that cannot be removed is approximately **5,500 lines** for basic HTML→DOCX conversion (paragraphs, styles, tables, lists).
