# National Taiwan University (NTU) Thesis/Dissertation LaTeX Template — English (Public Minimal)

建議下載後使用overleaf修改
等待勇者回報有沒有通過檢查
不保證任何結果風險自負
請確認格式規定有沒有更新
https://www.lib.ntu.edu.tw/node/103

This is an **NTU-wide public template** for **English theses/dissertations** (Master’s/Doctoral) with:
- **Minimal file set** (easy to maintain)
- **One-switch toggles** for common sections
- **Overleaf “no-traps” guardrails** (XeLaTeX-only, clear error messages)
- A **strict (FINAL) mode** to reduce formatting risk

> Source references (what this template implements):
> - **NTU Master’s Thesis / Doctoral Dissertation Format Guide** (components order, margins, pagination, cover layout).
> - **Guide for Submitting Electronic Theses and Dissertations** (single PDF + watermark + DOI + protection, done AFTER PDF).

---

## 0) What this template does (and does NOT do)

### Implemented in LaTeX (formatting)
- A4, **12pt**, **double spacing** (English)
- Margins (main text): **top/left/right 3 cm**, **bottom 2 cm**
- Cover & title page: **top 4 cm**, **bottom 3 cm**, centered, **1.5 line spacing**, required font sizes
- Pagination:
  - Cover/title page: **no page number**
  - Frontmatter: **roman numerals**, starts at **i** on the Certificate page
  - Main text: **arabic numerals**, starts at **1** on Chapter 1
- Required components order (cover → title page → certificate → abstracts → TOC → main text → references → appendix)

### NOT in LaTeX (post-PDF operations)
- **Watermark / DOI / PDF security** must be applied **after** you generate the final single PDF.
- See: `docs/after_pdf_checklist.tex`

### E-thesis cover vs printed cover (critical)
- **E-thesis PDF cover**: **no spine/side bar**, **must** include **NTU watermark + DOI**, and **must NOT show a page number**.
- **Printed outer cover (with spine)**: **has spine/side bar**, and **does NOT** include watermark/DOI.
- Remove any labels like **proposal/draft/final version** from the cover before submission.

---


## NTU format requirements (summary)

This template follows the **common NTU baseline rules**:

### Document components order
Cover → Title page → Certificate (Acceptance Certificate) → (Optional) Acknowledgement/Dedication → Chinese Abstract + Keywords → English Abstract + Keywords → Table of Contents → (Optional) List of Figures/Illustrations → (Optional) List of Tables → Main text → References → (Optional) Appendices.

### Core formatting (English thesis/dissertation)
- English font: **Times New Roman, 12pt**
- Line spacing: **double-spaced** (English)
- Margins (main text): **top/left/right 3 cm**, **bottom 2 cm**
- Page number at **bottom center**
- Frontmatter uses **roman numerals** starting at **i** on the Certificate page; Chapter 1 starts at arabic **1**
- Abstracts: **each no longer than 3 pages**; English theses still require a **Chinese abstract**
- Keywords: **5–7** recommended (both Chinese and English)

### Printing (for hard copies)
- Printed on **A4** paper; if the thesis/dissertation exceeds **80 pages**, double-sided printing is required (≤80 pages may be single-sided; color pages may be single-sided).
- **Library baseline**: typically **1 paperback + 1 hardcover** (unit-specific exceptions exist; e.g., some departments require 2–3 copies). Always confirm with your department and the Library.
- **Spine/outer cover** is for **printed copies only**; the **e-thesis PDF cover should NOT include a spine**.


## 1) Quick start (Overleaf)

1. Upload this ZIP to Overleaf.
2. **Menu → Compiler → XeLaTeX**  
   - This template will **stop** with a clear error if you compile with pdfLaTeX/LuaLaTeX.
3. **Menu → Main file → `main.tex`**
4. If you changed compiler/fonts: **Menu → Recompile from scratch**, then Recompile.

### How to verify you are really using XeLaTeX
Open the log:
- ✅ correct: `This is XeTeX...`
- ❌ wrong: `This is pdfTeX...`

---

## 2) Fonts (FINAL vs DRAFT)

NTU format rules require English text in **Times New Roman 12pt**.

### FINAL (recommended / strict compliance)
Default setting is strict:
- `\StrictNTUFontstrue` (in `config.tex`)
- If **Times New Roman** is missing, compilation **stops** to prevent accidental non-compliant output.

**Overleaf FINAL fix (recommended):**
1. Upload Times New Roman font file(s) to the project (commonly: `fonts/TimesNewRoman.ttf`)
2. In `config.tex`, set:
   - `\def\MainFontFile{fonts/TimesNewRoman.ttf}`

### DRAFT (preview only)
If you only need a preview PDF:
- set `\StrictNTUFontsfalse`  
This allows fallback to `TeX Gyre Termes` (close, but **not** zero-risk for submission).

### Chinese font
The template prioritizes common Kai fonts (e.g., `cwTeXKai`) and falls back safely.
If you KNOW your environment has a specific font:
- set `\def\CJKFontOverride{...}` in `config.tex`.

---

## 3) Edit only `config.tex` (recommended)

### Required fields (common)
- Unit names (Chinese/English) for cover
- Thesis titles (Chinese/English)
- Author names (Chinese/English)
- Advisor names (Chinese/English)
- Defense date (ROC year + month; Gregorian month + year)
- Keywords (**5–7** recommended)

### One-switch toggles (safe)
In `config.tex` you can toggle sections ON/OFF:
- Certificate, Acknowledgement, Chinese/English abstract, LOF/LOT, Appendix
- Methods/Results/Discussion **content** toggles (see next section)

---

## 4) “One-switch” chapter-body toggles (TOC structure stays)

These toggles are designed to speed drafting/compiling:
- They hide ONLY the **body text** of Methods/Results/Discussion.
- The `\chapter{...}` titles remain, so **Table of Contents entries remain**.

In `config.tex`:
- `\IncludeMethodsContenttrue/false`
- `\IncludeResultsContenttrue/false`
- `\IncludeDiscussionContenttrue/false`
- Master switch: `\DraftFastCompiletrue` (hides all three bodies)

---


## ETD submission special requirements (POST-PDF)

These are **mandatory** for the PDF you upload to the NTU ETD system, but they are **NOT** implemented in LaTeX:

1. Convert/compile the entire thesis into **ONE single PDF** (must include cover/title page/frontmatter/main text/references/appendix).
2. Add **NTU watermark** to all pages  
   - Absolute scale **50%**, opacity **50%**, behind page, position **2.5 cm from top/right**
3. Add your own **DOI** to all pages  
   - Size **12**, opacity **100%**, behind page, position **1 cm from bottom/right**
4. Set **PDF protection**  
   - Do **NOT** set a **Document Open Password** (the Library will reject files that cannot be opened). Use **permissions/password for editing/copying restrictions** instead  
   - Allow **high-resolution printing**; restrict editing/copying (only “Content Copying for Accessibility” should remain allowed)
5. Re-open the file and verify security settings (Ctrl+D → Security).

Full checklist: `docs/after_pdf_checklist.tex`

## 5) Compliance audit (template vs NTU rules)

This template is checked against the NTU format guide and ETD submission manual.

### PASS (implemented by template)
- Page size: A4
- Font size: 12pt
- Spacing: English double spacing
- Margins (main text): top/left/right 3 cm, bottom 2 cm
- Pagination: roman (i starts at Certificate), arabic (1 starts at Chapter 1)
- Cover/title page layout: top 4 cm, bottom 3 cm, centered, 1.5 spacing, specified font sizes
- Components order: cover/title/certificate/abstracts/TOC/main/references/appendix

### Manual / out-of-scope (you must do)
- Watermark + DOI + PDF protection (after final PDF)  
  See `docs/after_pdf_checklist.tex`
- Printed copy requirements (binding color/spine/copy counts) can vary by unit — confirm with your department.

---

## 6) Minimal sample text policy
This public template intentionally keeps only:
- a few placeholder sentences per section
- short Chinese hints (to avoid confusion)
Everything else is removed to keep the template clean.

---

## Files
- `main.tex` — the thesis document
- `config.tex` — **edit this**
- `docs/after_pdf_checklist.tex` — post-PDF mandatory steps (NOT included in thesis)

---

## Version notes
- v8.1 → v9: cover/title page bottom margin set to **3 cm** (per NTU cover spec); added clearer NTU format summary + ETD post-PDF rules; kept file set minimal.


## Overleaf warnings about cwTeXKai bold (safe)
If you see warnings like:
- `Font shape 'TU/cwTeXKai(0)/b/n' undefined`
- `Some font shapes were not available, defaults substituted.`

This happens because some Kai fonts (e.g., `cwTeXKai`) do not provide a real **bold** face. The template enables **fake bold** for CJK automatically (via `AutoFakeBold`) so the PDF output is stable and the warning should disappear after a clean recompile.

If the warning persists:
1) Menu → **Clear cached files / Recompile from scratch**
2) Or override the CJK font in `config.tex` with a font that has bold (e.g., `Noto Serif CJK TC`).