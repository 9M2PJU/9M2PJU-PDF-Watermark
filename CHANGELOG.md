# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-01-15

### Major Changes
- **Standard Professional Theme**: Complete UI overhaul to a "Clean Slate" standard theme. Replaced custom/experimental colors with semantic, neutral utility classes (`btn-primary`, `bg-panel`) for a professional look.
- **Performance**: Implemented main-thread yielding in the PDF processing loop to prevent UI freezing during large file uploads.

### Fixed
- **PDF Page Overflow**: Addressed image overflow in PDFs by enforcing strict `margin: 0` in `img2Pdf` and explicit image dimensions.
- **Async Race Condition**: Fixed a critical bug where rapid config changes caused duplicate pages. Replaced promise chains with serialized `async/await` logic in `loadPdf`.
- **Security**: Hardened strict Content Security Policy (CSP) and added `rel="noopener noreferrer"` to all external links.

### Technical
- **Build System**: Migrated build process to `pnpm`.
- **Docs**: configured `docs/` folder for GitHub Pages deployment.

## [1.1.0] - 2026-01-15

### Fixed
- **PDF Page Overflow Bug**: Fixed an issue where watermarked PDFs would have single pages split into 2 pages due to image overflow. The `doc.image()` function now explicitly constrains the watermarked image to fit within the exact page dimensions.

### Technical Details
- Added explicit `width` and `height` parameters to `doc.image()` call in `img2Pdf` function (`src/util.ts`)
- This ensures the watermarked image fits perfectly within each PDF page boundary without any overflow
