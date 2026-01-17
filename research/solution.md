# LaTeX workflow improvements with modern AI tools (2026)

## Goal
Make LaTeX writing and debugging faster, less error-prone, and more AI-friendly by combining:
- a strong local editor setup (fast feedback)
- a reproducible build pipeline (latexmk)
- a “lint + language” layer (ChkTeX + LanguageTool/LTeX)
- an AI assistant loop that is constrained by logs, diffs, and minimal patches

---

## 1) Quick overview of current LaTeX tooling & editors

### Editors
- **Overleaf**: easiest collaboration & compile, great for teams; slower for large projects; limited local automation.
- **VS Code** (LaTeX Workshop): very popular local workflow; fast compile, log view, PDF sync; integrates well with AI assistants.
- **TeXstudio / TeXmaker**: classic LaTeX IDEs; strong features; weaker AI integration.
- **Vim/Neovim** (vimtex) / Emacs (AUCTeX): power-user workflows; very fast; steeper learning curve.
- **Typst** is an alternative ecosystem, but this repo focuses on LaTeX.

### Build tools
- **latexmk**: best “one command build” orchestration (handles reruns, bibliography, etc.).
- **tectonic**: reproducible engine with auto package fetching; nice for CI/prototyping (not always compatible with complex setups).

### Quality tools
- **ChkTeX**: LaTeX linter (common mistakes, style issues).
- **LTeX / LanguageTool**: grammar/spell checking in TeX/Markdown.
- **BibLaTeX/Biber** tooling + DOI helpers for references.

---

## 2) Main workflow problems users hit

1) **Slow debug loop**
   - Compile errors buried in logs.
   - One missing brace triggers a cascade of unrelated errors.

2) **Non-AI-friendly error messages**
   - Logs are long; “error at line X” may not match the real root cause.
   - AI helpers often guess without seeing the exact log + surrounding lines.

3) **Fragile project structure**
   - Multi-file inputs, packages, and bibliography make “it works on my machine” common.
   - Missing fonts/packages break CI or collaborators’ builds.

4) **Citations & bibliography friction**
   - Broken keys, inconsistent styles, DOI lookup, duplicated entries.

5) **Collaboration pain**
   - Merge conflicts in .tex and .bib.
   - Lack of consistent formatting rules.

---

## 3) Ideas/tools to improve the experience

### A) AI-assisted debugging with guardrails
Create a “debug mode” that always bundles:
- last compile log (filtered to errors + last 50 lines around each)
- the failing file excerpt (±30 lines around error line)
- a minimal diff patch proposal

The AI should be instructed to:
- propose **smallest possible change**
- explain *why* the log points to that change
- avoid broad refactors unless requested

### B) Structured log parser
Add a small script (optional) that:
- extracts **root cause candidates**
- groups errors by file and line
- surfaces “first error” prominently
- outputs a short `build_report.md` for humans/AI

### C) “Lint + language” by default
- Run **ChkTeX** on changed .tex files (pre-commit or CI).
- Run **LTeX/LanguageTool** locally for grammar/spelling.
This catches a lot of issues before compile.

### D) Reproducible builds
- Standardize on **latexmk** and a pinned TeX distribution strategy:
  - either a container (CI) or a documented install path
  - optional: tectonic for simple projects

### E) Opinionated project layout
Recommended layout:
- `/src` for .tex chapters
- `/figures` for images
- `/bib` for bibliography
- `/out` ignored by git
- one entrypoint `main.tex`

### F) Simple formatting conventions
- Enforce consistent line wrapping (e.g., 80–100 chars where sensible)
- Use `%` comments sparingly
- Prefer one sentence per line in prose to reduce merge conflicts

---

## 4) Recommended “best today” workflow

### Local (VS Code + LaTeX Workshop)
1) Install TeX distribution (TeX Live / MiKTeX)
2) Install VS Code extensions:
   - LaTeX Workshop
   - LTeX (LanguageTool) for TeX
3) Configure:
   - latexmk build recipe
   - forward/inverse search
   - show errors in Problems panel

Suggested habits:
- compile on save (or on demand for large projects)
- keep PDF viewer side-by-side
- when error happens: copy the *first error block* + relevant file excerpt into the AI prompt

### CI (GitHub Actions)
- Run `latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex`
- Upload PDF artifact
- If compile fails: upload `main.log` as artifact for quick debugging

### AI usage pattern (fast and safe)
When something breaks, give the AI:
- the first error + 20–50 lines around it from the log
- the relevant .tex excerpt around the line
Ask for:
- minimal patch
- explanation
- follow-up check steps

---

## 5) Optional prototype/config suggestions

### Prototype A: VS Code settings snippet (example)
Create `/prototype/vscode-settings.json` (optional) with:
- latex-workshop latexmk recipe
- default build tool
- synctex

### Prototype B: CI workflow (example)
Add `.github/workflows/latex.yml` running latexmk and uploading PDF/log artifacts.

(These are optional; the core deliverable is this research doc.)

---

## 6) Summary
The biggest wins come from:
1) **latexmk everywhere** (local + CI)
2) **better log surfacing** (first error + context)
3) **lint + language layer** (ChkTeX + LTeX)
4) **AI prompts constrained by logs + diffs** (minimal patching)
