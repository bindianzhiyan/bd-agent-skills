---
name: paper-writing
description: Use this skill when the user wants help drafting, revising, restructuring, or polishing an academic paper, especially the Introduction, Method, or Related Work sections of a conference or journal manuscript. This skill is also relevant when the user wants a paper outline, section-level planning, contribution framing, venue-aware scholarly tone, or a later export to LaTeX.
---

# Paper Writing

This skill helps draft and revise research-paper prose with a strong focus on `Introduction`, `Method`, and `Related Work`.

Default to natural-language output. Only switch to LaTeX when the user explicitly asks for LaTeX or provides a template that should be filled.

## Current Scope

This version fully supports:

- `Introduction`
- `Method`
- `Related Work`
- NeurIPS 2026 section-level LaTeX export for drafted content

This version does not yet provide full section-specific workflows for:

- `Abstract`
- `Experiments`
- `Conclusion`
- `Rebuttal`
- full-paper end-to-end LaTeX authoring beyond the currently supported export templates

When the user asks for unsupported sections, provide a high-level outline or a lightweight draft, but do not pretend the skill has the same depth there as it does for `Introduction`, `Method`, and `Related Work`.

## Input Strategy

This skill uses a two-layer input model:

1. shared paper context
2. section-specific inputs

Do not force `Introduction` and `Related Work` to use the same detailed prompt template. They share paper-level context, but each section may require different fields, constraints, and output logic.

### Shared Paper Context

Reuse these inputs across sections whenever available:

- paper title
- research task or topic
- target method or system name
- problem setting
- research goals
- contribution points
- target venue or paper type if known

If the user already provided these once, do not keep asking for them again.

### Section Routing

When the user asks for a specific section, route to that section's own writing workflow and only request the fields that matter there.

- `Introduction` needs problem framing, technical gap, method overview, contribution mapping, and optional chapter arrangement.
- `Method` needs module structure, mechanism roles, intermediate resources, process flow, and how the modules support the final objective.
- `Related Work` needs literature grouping material, comparison axes, representative papers, and the paper's positioning against prior work.

If the user asks for both sections together, preserve one shared set of paper-level claims while letting each section use its own local inputs.

## Stage Inference

Do not force the user through a fixed multi-turn interview from the beginning.

Instead, infer the current working stage from the user's input and act accordingly. Treat stage detection as an internal routing decision, not something that must always be exposed to the user.

### Default Stage Policy

- If the user provides rich structured inputs for a section, draft that section directly.
- If the user provides partial materials, first organize them into a section plan or slot map.
- If the user provides only a broad request, ask a minimal set of clarification questions.
- If the user provides an existing draft, switch to revision mode instead of re-drafting from scratch.

### Typical Internal Stages

Useful internal stages include:

- `collect_context`
- `section_planning`
- `intro_drafting`
- `method_planning`
- `method_drafting`
- `related_work_planning`
- `related_work_drafting`
- `revision`
- `latex_export`
- `latex_export_neurips`

These are internal workflow labels, not mandatory user-visible steps.

### Minimal-Question Rule

Only ask follow-up questions when the missing information would materially reduce output quality.

Prefer:

- one short clarification turn
- the smallest missing field set
- conservative placeholders when possible

Avoid:

- restarting from the beginning when enough information is already present
- asking for fields that are not necessary for the current section
- turning every request into a long interactive intake flow

When a section-specific reference defines `Minimum Required Inputs` or `Clarification Priority`, follow that narrower rule instead of using a generic intake pattern.

## Core Behavior

Follow these principles for every task:

1. Establish the paper's central claim before writing paragraphs.
2. Keep the problem statement, gap, method framing, and contribution list consistent across sections.
3. Prefer precise scholarly prose over marketing language.
4. Do not invent citations, datasets, metrics, baselines, or experimental results.
5. If key facts are missing, make the smallest reasonable assumptions and label placeholders clearly.

Use placeholders such as:

- `[CITATION]`
- `[DATASET]`
- `[BASELINE]`
- `[RESULT]`
- `[VENUE REQUIREMENT]`

## Minimal Context To Infer Or Ask For

When the user does not provide complete context, infer what you safely can from the conversation. If crucial facts are still missing, ask only for the smallest missing set needed to produce good prose.

The most useful shared inputs are:

- research topic and task
- paper type or target venue if known
- core method or idea
- what gap in prior work the paper addresses
- 2-4 contribution points
- any must-mention baselines, datasets, or claims

If some of these are missing, continue with a structured draft and explicit placeholders instead of blocking.

## Default Workflow

Use this workflow unless the user asks for something narrower.

1. Infer the current stage from the user's input.
2. Identify the section target: outline, `Introduction`, `Method`, `Related Work`, or revision.
3. Extract the paper's thesis, gap, method identity, and contribution claims.
4. Decide whether the input is sufficient for direct drafting or whether a minimal clarification turn is needed.
5. Decide the output depth:
   - bullet outline
   - paragraph plan
   - polished prose
   - prose plus LaTeX formatting
6. Ensure the paper workspace exists before drafting or exporting.
7. Draft the section with internally consistent terminology.
8. Save the drafted source content into the paper workspace.
9. Run a quick self-check for logic, redundancy, citation placeholders, and tone.

## Introduction Workflow

The goal of the `Introduction` is to explain why the problem matters, what is missing in current approaches, what the paper does, and why that contribution is meaningful.

This section may use a more structured input format than other sections. That is expected.

### Introduction-Specific Inputs

Use these inputs when available:

- paper title
- research background
- `technology/method`
- target advantages or goals
- `problem 1`
- `problem 2`
- `problem 3`
- `innovation 1`
- `innovation 2`
- `innovation 3`
- experimental results or claimed outcomes
- chapter organization if the user already has one
- literature list for background support if provided

If the user provides a highly templated input package, preserve its factual structure while rewriting it into natural academic Chinese.

If the user provides only rough notes, infer the same slots conservatively before drafting.

If the user is asking for a Chinese thesis-style introduction with explicit subsection expectations, read `references/intro_cn_thesis.md` and follow that reference as the section-specific template.

### Introduction Stage Routing

- If the user provides a slot-filled package with background, method, problems, innovations, and results, enter `intro_drafting` directly.
- If the user provides topic plus method but no clean problem mapping, enter `section_planning` and first organize the material into gap, problems, method, and contributions.
- If the user provides an existing introduction, enter `revision`.
- If the user asks for LaTeX output after the prose is already stable, enter `latex_export`.

Unless the user requests a different structure, organize the introduction with this logic:

1. Context and importance of the problem
2. Concrete limitation or gap in existing work
3. Main idea of the proposed approach
4. Why the approach matters
5. Contribution summary
6. Optional paper roadmap sentence

### Introduction Writing Rules

- Open with the research problem, not with vague hype.
- Narrow from broad context to a crisp technical gap.
- State the gap in a way that sets up the method naturally.
- Introduce the method at the level the user needs:
  - high-level intuition for early drafting
  - more concrete mechanism for polishing
- Present contributions as specific claims, not generic positives.
- Keep the contribution list parallel in grammar and scope.
- Avoid overclaiming with words like "revolutionary", "groundbreaking", or "solves" unless strongly justified.
- When writing in Chinese academic style, reduce visible LLM patterns such as rigid serial markers, slogan-like phrasing, or repetitive transition formulas.
- If the user provides section-level formatting constraints, follow them even when they are more specific than the default workflow.
- Keep detailed subsection templates, paragraph-by-paragraph requirements, and thesis-formatting specifics in references rather than duplicating them here.

### Introduction Output Modes

Choose the format that best matches the request:

- If the user is still thinking: provide an outline or paragraph plan.
- If the user has core content but weak phrasing: rewrite into polished prose.
- If the user has a draft: revise for logic, flow, and contribution framing.
- If the user asks for LaTeX: return introduction prose wrapped in appropriate section structure.

### Introduction Self-Check

Before finalizing, verify:

- the problem is understandable to the intended audience
- the gap is explicit
- the proposed approach is introduced before the contribution list
- the contributions match what the introduction actually claims
- terminology is consistent

## Method Workflow

The goal of the `Method` section is to explain why the method is needed, how its core structures are organized, what each structure does, what intermediate resources or representations it produces, and how the full pipeline leads to the target output.

This section often expects a strongly structured input package with fixed subsection names. That is expected.

### Method-Specific Inputs

Use these inputs when available:

- paper title
- method name
- method short name
- `problem 1`
- `problem 2`
- `problem 3`
- overall target
- method structure list
- `structure 1 name`
- `structure 2 name`
- `structure 3 name`
- `structure 4 name`
- stage names or subprocess names
- intermediate representation
- reasoning mechanism
- global retrieval or enhancement strategy
- mechanism names for final control or alignment
- structure linkage description
- target scenarios
- literature list if the user provides one

If the user provides a highly templated method input package, preserve its factual structure while rewriting it into natural academic Chinese.

If the user is asking for a Chinese thesis-style method section with explicit numbered subsections, read `references/method_cn_thesis.md` and follow that reference as the section-specific template.

### Method Stage Routing

- If the user provides method name, problems, overall goal, and a four-part structure, enter `method_drafting` directly.
- If the user provides modules or notes but the structure is still loose, enter `method_planning` and first normalize the material into total overview plus `3.1` to `3.4`.
- If the user provides an existing method draft, enter `revision`.
- If the user asks for LaTeX after the prose is stable, enter `latex_export`.

Unless the user requests another structure, organize the method section with this logic:

1. one overview paragraph under `3 方法描述`
2. one subsection for foundational resources or parsing
3. one subsection for intermediate reasoning or representation
4. one subsection for retrieval, knowledge, or context enhancement
5. one subsection for final generation and control

### Method Writing Rules

- Explain why each structure exists before describing its internal mechanism.
- Emphasize what each structure produces and how that output supports later structures.
- Preserve user-provided subsection numbering and titles when they are part of the required format.
- Compress formulas, algorithm blocks, and figure references into plain academic description rather than reproducing symbolic notation.
- Keep terminology consistent for method name, intermediate representation, knowledge resources, and final target output.
- Reduce visible LLM patterns such as rigid serial phrasing, slogan-like repetition, or templated transitions.
- If the user provides section-level formatting constraints, follow them even when they are more specific than the default workflow.
- Keep detailed subsection templates, paragraph-by-paragraph requirements, and thesis-formatting specifics in references rather than duplicating them here.

### Method Output Modes

- If the user is still designing the pipeline: provide a subsection plan or normalized structure map.
- If the user has a module list but rough language: rewrite into polished method prose.
- If the user has a draft: revise for module logic, terminology, and structural coherence.
- If the user asks for LaTeX: return method prose wrapped in the requested section structure.

### Method Self-Check

Before finalizing, verify:

- the total overview clearly states problems, method identity, structures, and linkage
- each subsection explains purpose, mechanism, outputs, and downstream support
- the structure order matches the actual pipeline logic
- the intermediate representation and control mechanisms are explained in prose rather than raw notation
- terminology is consistent across all subsections

## Related Work Workflow

The goal of `Related Work` is not to list papers one by one. The goal is to position the paper against prior work in a clear comparative structure that makes the paper's niche obvious.

This section often expects a different input package from `Introduction`.

### Related-Work-Specific Inputs

Use these inputs when available:

- literature list
- technical-stage category titles
- representative baseline papers
- grouping preferences from the user
- comparison axes such as retrieval, reasoning, alignment, hallucination control, or intermediate representation
- which limitations of prior work are most relevant to the present paper
- pain points or core challenges that the current paper addresses
- the paper's intended positioning sentence or novelty claim

If the user does not provide a complete literature set, produce a section scaffold with citation placeholders instead of fabricating sources.

If the user is asking for a Chinese thesis-style related-work section with fixed category titles or stage-based subsections, read `references/related_work_cn_thesis.md` and follow that reference as the section-specific template.

### Related Work Stage Routing

- If the user provides a literature list plus comparison focus, enter `related_work_drafting`.
- If the user provides papers but no grouping logic, enter `related_work_planning` and first cluster them by comparison axis.
- If the user provides a rough related-work draft, enter `revision`.
- If the user provides too little literature support, ask only for the most necessary missing papers or proceed with a scaffold and placeholders.

Unless the user requests another style, organize related work by themes or comparison axes, not by timeline.

Useful grouping patterns include:

- method families
- problem settings
- supervision regimes
- modeling assumptions
- evaluation settings
- known limitations

### Related Work Writing Rules

- Group prior work into 2-4 coherent categories.
- Give each category a short framing sentence before naming examples.
- Summarize the shared strength or focus of that category.
- State the limitation most relevant to the current paper.
- Use the final sentences to explain how the present paper differs.
- Respect user-provided subsection titles when they represent fixed technical stages or required headings.
- Keep detailed citation-order constraints, paragraph templates, and Chinese thesis-formatting specifics in references rather than duplicating them here.

Avoid:

- long laundry lists of papers with one clause each
- repeating the introduction's full motivation
- attacking prior work unfairly
- claiming novelty without a comparison basis

### Related Work Output Modes

- If the literature set is incomplete: provide a thematic scaffold with citation placeholders.
- If the user gives a paper list: cluster the papers and turn them into comparative prose.
- If the user gives a rough draft: rewrite for grouping, compression, and sharper positioning.
- If the user asks for LaTeX: return prose wrapped in the requested section structure.

### Related Work Self-Check

Before finalizing, verify:

- papers are grouped by a meaningful axis
- each group has a clear common thread
- the section explains limitations relevant to the current paper
- the transition to the current work feels justified
- no citations appear fabricated

## Cross-Section Consistency

When multiple supported sections are involved in the same task:

- use the same naming for the problem, method, and setting
- make sure the gap in the introduction matches the limitations discussed in related work
- make sure the method section directly addresses the problems raised in the introduction
- make sure the related-work positioning supports the need for the method design
- make sure the claimed contribution is supported by how prior work is positioned
- avoid repeating the same sentences across sections
- allow different local input structures for each section without forcing a single shared template

## Style Guidance

Target a research-paper tone:

- clear
- restrained
- technically specific
- logically progressive

Prefer:

- "prior methods often struggle with ..."
- "existing approaches typically assume ..."
- "in contrast, our approach ..."

Avoid:

- sales language
- unsupported novelty claims
- conversational filler
- fake certainty when evidence is missing

## LaTeX Behavior

Default output is plain scholarly prose.

Only produce LaTeX when:

- the user explicitly asks for LaTeX
- the user shares a template or section skeleton
- the task is clearly in final formatting mode

If no template is provided, keep LaTeX minimal and portable.

If the user asks for NeurIPS formatting, read `references/latex_neurips_2026.md` and use the assets in `assets/neurips_2026/`.

Current LaTeX support is intentionally scoped:

- export drafted `Introduction` and `Related Work` content into NeurIPS 2026 section structure
- export drafted `Method` content into NeurIPS 2026 section structure
- preserve placeholders conservatively when bibliography or metadata is incomplete
- avoid pretending that the full paper is ready if only a subset of sections exists

### LaTeX Architecture

Use this separation of responsibilities:

- keep official and reusable template files in `assets/`
- keep venue-specific export rules in `references/`
- let section workflows generate and save section-level source content
- let a final LaTeX export step assemble the full document

Do not treat `references/` as storage for the actual NeurIPS template files.

For NeurIPS export:

- section workflows should first produce natural-language source drafts
- section workflows may optionally generate local LaTeX for their own section bodies when the user explicitly asks for section-level LaTeX
- section workflows should not generate full standalone papers
- the final `latex_export_neurips` step is responsible for copying the template shell, reading saved section source files, wiring `\input{sections/...}`, and keeping document-level formatting consistent
- when `paper/neurips/main.tex` already exists, treat it as the canonical main file and update it in place rather than creating an alternative standalone `.tex` file
- when `paper/neurips/main.tex` does not exist, initialize it by copying `assets/neurips_2026/paper_draft_template.tex` rather than regenerating a fresh main file from scratch

### Content Persistence

Do not rely on chat history alone for multi-stage paper assembly.

When a section is drafted, save its natural-language source content to a stable paper workspace so later export steps can reuse it.

Use a two-layer structure:

- source content layer for editable prose
- export layer for venue-specific LaTeX output

Preferred workspace layout:

- `paper/content/introduction.md`
- `paper/content/method.md`
- `paper/content/related_work.md`
- `paper/neurips/main.tex`
- `paper/neurips/sections/introduction.tex`
- `paper/neurips/sections/method.tex`
- `paper/neurips/sections/related_work.tex`

The source content layer is the canonical editable version. LaTeX files are derived export artifacts unless the user explicitly wants to edit LaTeX directly.

When a NeurIPS paper workspace already exists, do not switch to a generic thesis `ctex` main file unless the user explicitly asks for a separate Chinese thesis template.

### Workspace Creation Rule

Creating and using the paper workspace is the default behavior, not an optional enhancement.

If `paper/` does not exist in the working skill/project directory, create it with the expected subdirectories before saving or exporting content.

At minimum, ensure these directories exist when needed:

- `paper/content/`
- `paper/neurips/`
- `paper/neurips/sections/`

When drafting a supported section:

- `Introduction` must be saved to `paper/content/introduction.md`
- `Method` must be saved to `paper/content/method.md`
- `Related Work` must be saved to `paper/content/related_work.md`

Do not only return the drafted prose in chat when the task is a drafting request. Persist the drafted prose to the workspace as part of the normal workflow unless the user explicitly asks for a chat-only response.

## Failure Modes To Avoid

Do not:

- fabricate references or author names
- invent numerical improvements
- collapse `Related Work` into an annotated bibliography
- write an `Introduction` that never states the actual contribution
- use inconsistent names for the same method or setting

## Expansion Notes

Future versions of this skill may add dedicated workflows for `Abstract`, `Method`, `Experiments`, `Conclusion`, rebuttal writing, and venue-specific LaTeX packaging.

For now, treat this skill as a strong specialist for `Introduction` and `Related Work`, with light support for surrounding paper-structure tasks.
