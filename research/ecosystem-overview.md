LaTeX Tooling Ecosystem Overview
================================

This document surveys today’s LaTeX tooling landscape to orient contributors before we design or evaluate AI-assisted improvements.

## Core Distributions & Compilers

- **TeX Live** (cross-platform) — Comprehensive distribution with standard packages; supports `pdflatex`, `xelatex`, `lualatex`.
- **MiKTeX** (Windows/macOS/Linux) — On-demand package installs, popular in enterprise environments.
- **TinyTeX** — Lightweight TeX Live variant tailored for reproducible builds, favored in R and CI pipelines.
- **Tectonic** — Modern “single command” compiler with automatic dependency resolution and caching.
- **Overleaf build servers** — Cloud-based compilation with collaborative sharing; integrates TeX Live with custom tooling.

## Editors & IDEs

- **Overleaf** — Browser-based collaborative editor, rich templates, real-time previews, Git sync.
- **VS Code (LaTeX Workshop, LaTeX-Utilities)** — Extensible environment with build recipes, linting, snippets, and integration hooks for AI assistants.
- **TeXstudio / TeXmaker / TeXworks** — Traditional cross-platform editors with built-in compilers and viewers.
- **Vim/Neovim (vimtex, nvim-latex)** — Highly customizable workflows with forward/inverse search and build integration.
- **Emacs (AUCTeX, CDLaTeX)** — Advanced macro expansion, preview-latex integration, RefTeX for citation management.
- **JetBrains IDEs (TeXiFy IDEA)** — Provides structure view, inspections, and Gradle-like build tasks.
- **Sublime Text, Atom, Zettlr** — Niche but active communities for hybrid Markdown/LaTeX authoring.

## Supporting Tooling

- **Linting & Formatting**: `chktex`, `lacheck`, `latexindent.pl`.
- **Bibliography Management**: BibLaTeX/Biber, JabRef, Zotero (with Better BibTeX), Citationsy.
- **Graphics & Diagrams**: TikZ/PGF, Inkscape (with PDF+LaTeX export), draw.io → `tikzcd`.
- **Equation Editors**: Mathpix Snip, Mathcha, LyX (WYSIWYM), Lumerical’s Equation Editor.
- **Continuous Integration**: GitHub Actions (latexmk, tectonic actions), GitLab CI templates, CircleCI or Azure pipelines with TeX Live docker images.
- **Packaging & Templates**: `cls`/`sty` repositories, university templates, ACM/IEEE macros, corporate branding kits.

## Emerging AI-Integrated Tools

- **ChatGPT / Claude / Gemini** integrations in Overleaf and VS Code extensions.
- **GitHub Copilot & Cursor** for inline LaTeX snippet generation and refactoring.
- **Codeium / Tabnine** for completions, especially in math-heavy contexts.
- **Mathpix Autocomplete & OCR** for turning handwritten notes into LaTeX equations.
- **Explain this error** bots embedded into editors (e.g., Overleaf’s log parsing assistant).

## Workflows & Deployment Targets

- **Academic Publishing**: Journal- or conference-specific templates, double-blind workflows, preprint variants (arXiv).
- **Technical Documentation**: Multi-language manuals, API references using Sphinx (with LaTeX output) or MkDocs.
- **Education**: Problem sets, exams, lecture notes with auto-grading integration (e.g., PrairieLearn, Gradescope).
- **Scientific Computing**: Jupyter→LaTeX pipelines, reproducible reports, SIAM/AMS format.
- **Business Reports**: Custom branding, financial reports, automated data tables via Pandoc or R Markdown.

## Observations

- Tooling is fragmented by platform and skill level; AI integration often favors cloud-based editors, leaving terminal-heavy users underserved.
- Compilation remains a pain point due to dependency management; newer tools (Tectonic, Dockerized TeX Live) aim to abstract complexity.
- Collaborative workflows rely on Git/Overleaf bridging, but metadata (comments, review states) is inconsistent across tools.
- AI offerings are mostly prompt-driven; few robust automations exist for project scaffolding, log triage, or semantic editing.

Use this overview to anchor research efforts and identify areas where AI enhancements could deliver the most leverage.

