# Research Notes: HTML to DOCX Conversion Libraries

## Date: 2025-12-04

## Objective
Evaluate and compare various npm packages for converting HTML to DOCX format, focusing on browser and server compatibility.

## Methodology
1. Install all packages
2. Analyze each package individually
3. Tournament-style comparison (1v2, winner vs 3, etc.)
4. Final recommendation

---

## Installation Log

Successfully installed 27 packages:
- 19 non-scoped packages
- 8 scoped packages (@types, @turbodocx, @packback, @mark-beeby, @gc123, @adalat-ai, @kaipeng, @ckeditor)

---

## Package Categories Identified

### Category 1: altChunk/MHT-based (Legacy Approach)
These packages embed HTML as MHT (MHTML) in DOCX using Word's altChunk feature. Only works with MS Word.

- html-docx-js (original, CoffeeScript)
- html-docx-fixed
- html-docx-js-typescript
- html-docx-ts
- html-docx-js-version-updated
- html-docx-js-extends
- html-docx-js-a13
- html-docx-js-typescript-papersize-thenn
- html-docx-typescript
- html-docx-js-typescript-modify
- html-docx-js-extension-typescript
- html-docx-ts-improve
- pt-html-docx-js
- @gc123/html-docx-js
- @kaipeng/html-docx-js
- html-docx
- yk-html-to-docx

### Category 2: Native OOXML Generation (Modern Approach)
These packages generate proper Office Open XML, compatible with Word, LibreOffice, Google Docs.

- html-to-docx (privateOmega)
- html-to-docx-lite
- html-to-docx-typescript
- @turbodocx/html-to-docx
- @packback/html-to-docx
- @mark-beeby/html-to-docx
- @adalat-ai/html-to-docx

### Category 3: Specialized/Framework-Specific
- prosemirror-docx (ProseMirror integration)
- @ckeditor/ckeditor5-export-word (CKEditor 5 plugin, cloud-based)

### Category 4: Type Definitions Only
- @types/html-docx-js

---

## Tournament Comparisons

### Round 1: altChunk Libraries

**html-docx-js vs html-docx-fixed**
- Both use same approach (altChunk)
- html-docx-fixed is a fork with fixes
- WINNER: html-docx-js (original, better documented)

**html-docx-js-typescript vs html-docx-ts**
- Both TypeScript rewrites
- html-docx-js-typescript: v0.1.5, more tests
- html-docx-ts: v0.0.5, header/footer support
- WINNER: html-docx-ts (more features)

**html-docx-js-extends vs html-docx-js-a13**
- html-docx-js-extends: multi-section support, TypeScript
- html-docx-js-a13: bundled UMD, minimal
- WINNER: html-docx-js-extends (more features)

**html-docx-js-typescript-papersize-thenn vs html-docx-js-version-updated**
- papersize-thenn: adds custom paper sizes
- version-updated: updated jszip
- WINNER: html-docx-js-typescript-papersize-thenn (unique feature)

### Round 2: Native OOXML Libraries

**html-to-docx vs @turbodocx/html-to-docx**
- html-to-docx: v1.8.0, original, comprehensive
- @turbodocx: v1.18.1, fork with RTL support, unit tests
- WINNER: @turbodocx/html-to-docx (more active, more features, RTL support)

**html-to-docx-lite vs html-to-docx-typescript**
- html-to-docx-lite: v2.0.1, Vite-based, modern
- html-to-docx-typescript: v1.3.2, TypeScript types
- WINNER: html-to-docx-lite (more modern tooling)

**@packback/html-to-docx vs @mark-beeby/html-to-docx**
- @packback: v1.4.2, uses docx library, CLI, TypeScript
- @mark-beeby: v1.6.4-rc.63, table column widths, many deps
- WINNER: @packback/html-to-docx (cleaner, uses standard docx library)

**@adalat-ai/html-to-docx vs html-to-docx (original)**
- Both forks of privateOmega's html-to-docx
- @adalat-ai: fork with bug fixes
- WINNER: html-to-docx (original, more contributors)

### Round 3: Specialized Libraries

**prosemirror-docx**
- Unique: Works with ProseMirror documents, not HTML
- Uses docx library (peer dependency)
- Active maintenance (Curvenote)
- Best for: ProseMirror-based editors

**@ckeditor/ckeditor5-export-word**
- Commercial CKEditor 5 plugin
- Cloud-based conversion (requires CKEditor Cloud Services)
- Obfuscated code
- Not standalone - requires full CKEditor integration

---

## Final Tournament

### Semi-Finals

**Best altChunk: html-docx-js-extends**
- TypeScript support
- Multi-section documents
- Header/footer support
- Active-ish maintenance

vs

**Best Native OOXML: @turbodocx/html-to-docx**
- v1.18.1 (most active)
- RTL support
- Unit tests
- Proper OOXML generation
- Works with all word processors

**WINNER: @turbodocx/html-to-docx**
Reason: Native OOXML is universally compatible, not just MS Word

---

**@packback/html-to-docx vs html-to-docx-lite**

- @packback: Uses docx library, TypeScript, CLI
- html-to-docx-lite: Vite-based, modern bundling

**WINNER: @packback/html-to-docx**
Reason: Better architecture using docx library, TypeScript native

---

### Finals

**@turbodocx/html-to-docx vs @packback/html-to-docx**

| Criteria | @turbodocx | @packback |
|----------|-----------|-----------|
| Version | 1.18.1 | 1.4.2 |
| TypeScript | No (JS only) | Yes |
| Tests | Yes (Jest) | Yes (Jest) |
| Browser Support | Yes (UMD/ESM) | Needs bundler |
| Node Support | Yes | Yes (Node 18+) |
| RTL Support | Yes | No |
| Table Support | Yes | Yes |
| Image Support | Yes (axios) | Yes (via docx) |
| CLI | No | Yes |
| Dependencies | 12 runtime | 1 runtime (docx) |
| Active | Very active | Active |

**OVERALL WINNER: @turbodocx/html-to-docx**

Reasons:
1. Most complete feature set
2. RTL language support
3. Browser and Node.js ready
4. Active maintenance with many contributors
5. Comprehensive HTML element support
6. Unit tested

**RUNNER-UP: @packback/html-to-docx**

Reasons:
1. Clean architecture (uses docx library)
2. TypeScript native
3. Minimal dependencies
4. CLI included
5. Modern Node.js (18+)

---

## Special Mentions

1. **prosemirror-docx** - Best if using ProseMirror
2. **html-docx-js-extends** - Best altChunk option if MS Word-only is acceptable
3. **html-to-docx-lite** - Best for modern Vite-based projects

---

## Key Findings

1. **altChunk approach is obsolete**: Only works with MS Word, not LibreOffice/Google Docs
2. **Native OOXML is future-proof**: Works everywhere
3. **TypeScript adoption is mixed**: Many packages still JavaScript-only
4. **Most packages are forks**: html-docx-js spawned 10+ forks, html-to-docx spawned 5+
5. **@turbodocx is the most actively maintained** with most features

---

## Detailed Top-3 Comparison (Added 2025-12-04)

See `comparison/detailed-comparison.md` for the full 20-factor analysis.

### Quick Summary

| # | Factor | @turbodocx | @packback | html-to-docx-lite |
|---|--------|-----------|-----------|------------------|
| 1 | Bundle Size | 1.66 MB | 215 KB | 262 KB |
| 2 | Dependencies | 12 | 1 | 10 |
| 3 | TypeScript | .d.ts | Native | None |
| 4 | Tests | Jest | Jest | Example only |
| 5 | HTML Coverage | Full | Quill-specific | Full |

**Overall Scores:**
- @turbodocx/html-to-docx: 8.15/10 (WINNER)
- html-to-docx-lite: 7.05/10
- @packback/html-to-docx: 6.40/10

**Recommendation for "works every time" + comprehensive:** `@turbodocx/html-to-docx`
