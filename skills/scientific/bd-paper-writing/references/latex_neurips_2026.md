# NeurIPS 2026 LaTeX Export

Read this file when the user wants drafted paper content converted into NeurIPS 2026 LaTeX format.

## Purpose

This reference handles section-level export into the NeurIPS 2026 template. It is primarily intended for exporting drafted prose such as `Introduction` and `Related Work` into a valid template structure without overclaiming full-paper readiness.

Use the official template assets stored in:

- `assets/neurips_2026/neurips_2026.sty`
- `assets/neurips_2026/neurips_2026.tex`
- `assets/neurips_2026/checklist.tex`
- `assets/neurips_2026/paper_draft_template.tex`
- `assets/neurips_2026/sections/introduction.tex`
- `assets/neurips_2026/sections/method.tex`
- `assets/neurips_2026/sections/related_work.tex`

These files belong in `assets/`, not in `references/`. `references/` should only describe how to use the template.

`assets/neurips_2026/paper_draft_template.tex` is the canonical shell that should be copied to `paper/neurips/main.tex` for initialization. Do not synthesize a different main file layout when this asset is available.

## Scope

This workflow currently supports:

- converting drafted content into NeurIPS sectioned LaTeX
- reading previously saved section source files from a paper workspace
- storing exported section bodies in separate files under `sections/`
- preserving official package usage and checklist inclusion
- producing a clean submission-style shell for further editing
- assembling a paper from section files via one final export step

This workflow does not guarantee:

- a complete camera-ready paper
- fully normalized BibTeX integration
- automatic conversion of every citation into `natbib` commands

## Default Export Mode

Unless the user explicitly asks otherwise, export in anonymous submission mode:

- use `\usepackage{neurips_2026}`
- keep author information anonymized
- omit acknowledgments

If the user explicitly asks for preprint or camera-ready formatting, adjust the package option accordingly.

## Minimum Required Inputs

Prefer exporting directly when the following are available:

- paper title
- at least one drafted and saved source section such as `paper/content/introduction.md`, `paper/content/method.md`, or `paper/content/related_work.md`
- enough metadata to label the included sections correctly

If abstract, author block, or bibliography details are missing, keep conservative placeholders rather than blocking.

## Clarification Priority

If a follow-up question is necessary, ask for the smallest missing set in this order:

1. the paper title
2. which sections should be exported
3. whether the export is for anonymous submission, preprint, or final
4. bibliography format only if the user asks for compiled references rather than a draft shell

## Export Rules

- Preserve the official NeurIPS 2026 style usage.
- Do not modify the `.sty` file.
- Start by copying a clean template shell into the target paper workspace.
- If `paper/neurips/main.tex` already exists, update that file instead of creating a new main TeX file elsewhere.
- If `paper/neurips/main.tex` is missing, copy `assets/neurips_2026/paper_draft_template.tex` to that path and use it as the starting main file.
- Also copy the required support files from `assets/neurips_2026/` into `paper/neurips/`, including `neurips_2026.sty` and `checklist.tex`, if they are missing.
- If the paper workspace or `paper/neurips/` is missing, create it before export.
- Read source prose from the saved content layer whenever available.
- Keep the main paper file thin and place section bodies in `sections/` files.
- In the main paper file, include section files with `\input{sections/...}`.
- Put each generated section heading and body inside its own section file.
- Let section writers handle only their own section content, not the global preamble or full document wrapper.
- Escape LaTeX-sensitive characters when needed.
- Keep unsupported sections as comments or placeholders rather than fabricated content.
- If the user only has numbered references in plain text, preserve them conservatively instead of inventing citation keys.
- Keep the checklist inclusion in place unless the user explicitly asks for a stripped internal draft.

## Citation Handling

Use the safest available citation strategy:

- If the user has BibTeX keys or explicit `natbib` style references, use LaTeX citation commands consistently.
- If the user only has numbered references or citation placeholders, preserve bracketed references or placeholders in the draft and leave normalization for a later pass.
- Never invent citation keys.

## Section Mapping

Map drafted content into the nearest standard paper structure:

- `绪论` or `Introduction` -> `sections/introduction.tex`
- `方法描述` or `Method` -> `sections/method.tex`
- `相关工作` or `Related Work` -> `sections/related_work.tex`

If the user provides section headings in Chinese but requests NeurIPS formatting, convert the visible section titles to standard English unless the user explicitly wants a Chinese manuscript.

## Main File Priority

For NeurIPS export, prefer this priority order:

1. update existing `paper/neurips/main.tex`
2. if missing, copy `assets/neurips_2026/paper_draft_template.tex` to `paper/neurips/main.tex`
3. only create a separate generic `ctex` or thesis main file if the user explicitly requests a non-NeurIPS Chinese thesis template

## Output Expectation

For a standard export request, produce one clean `.tex` draft that:

- compiles against the copied NeurIPS assets once placeholders are filled
- contains the drafted sections already inserted
- leaves missing metadata as explicit TODO-style placeholders

The preferred assembly flow is:

1. copy `assets/neurips_2026/paper_draft_template.tex` into `paper/neurips/main.tex` if the main file is missing
2. read saved source drafts from `paper/content/`
3. create or reuse `sections/`
4. convert each needed source draft into its own `sections/*.tex` file
5. keep the main paper file responsible for `\title`, `\author`, `\begin{abstract}`, `\input{sections/...}`, references, appendix, and checklist

## Recommended Asset

Prefer `assets/neurips_2026/paper_draft_template.tex` as the base shell for section export, and use `assets/neurips_2026/neurips_2026.tex` as the authoritative formatting reference.
