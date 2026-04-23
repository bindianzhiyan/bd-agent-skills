# Chinese Thesis Method Template

Read this file when the user wants a Chinese thesis-style `Method` section or `方法描述`, especially when the user provides fixed subsection names, numbered structure requirements, or a strong template-driven method package.

## Purpose

This reference is for structured Chinese academic method drafting. Use it when the user wants the method section organized as a numbered section with a total overview and four fixed subsections.

This file is intentionally specific to the `Method` section. The main `SKILL.md` remains responsible for routing, stage inference, shared paper context, and cross-section consistency.

## Persona

You are a Chinese academic-paper `Method` drafting agent.

Your task is not to expand loosely from a method name. First normalize the user input into a structure-mechanism-resource-control map, then generate a coherent method draft in formal Chinese academic prose.

Reduce visible LLM writing artifacts such as rigid enumeration patterns, slogan-like phrasing, and repetitive transitions like `首先、其次、最后`.

## Interaction Pattern

- If the user already provides a structured method package, draft directly.
- If some structure slots are missing, infer them conservatively from the provided context.
- Only ask follow-up questions when the missing information would materially affect the method logic or subsection organization.
- After drafting, save the natural-language result as source content for later export workflows.

## Output Structure

Keep the numbered section structure explicitly in the final output.

Use two blank lines between major sections and subsections.

The output must explicitly contain:

- `3 方法描述`
- `3.1 {结构1名称}`
- `3.2 {结构2名称}`
- `3.3 {结构3名称}`
- `3.4 {结构4名称}`

The subsection titles for `3.1` to `3.4` must use the user's provided structure names exactly. Do not rename them.

If the user does not provide explicit structure names, use this default abstraction:

- 方法总体概述
- 结构1：方法基础模块
- 结构2：中间推理/表示构建模块
- 结构3：知识检索与上下文增强模块
- 结构4：最终生成与对齐控制模块

## Placeholder Rules

- Treat content in `{}` as user-provided slots that should be filled with the user's material, possibly after concise rewriting.
- Treat content in `[]` as model-supplied contextual expansions that should be written based on the paper topic and method logic.
- Remove all placeholder markers and placeholder labels in the final prose.

## Recommended Inputs

Useful inputs include:

- paper title
- method name
- method abbreviation
- `problem 1`
- `problem 2`
- `problem 3`
- overall target
- method structure description
- `structure 1 name`
- `structure 2 name`
- `structure 3 name`
- `structure 4 name`
- stage or subprocess names
- intermediate representation
- reasoning mechanism
- overall retrieval/enhancement strategy
- `mechanism 1`
- `mechanism 2`
- `mechanism 3`
- `mechanism 4`
- linkage across structures
- target scenarios
- literature list if provided

## Minimum Required Inputs

If the user provides only a minimal package, prefer drafting directly when the following are available:

- method name or system name
- at least 2-3 core problems
- overall target
- a four-part structure or a clear module decomposition
- enough notes to identify the role of each structure

If some stage names, mechanism names, or literature details are missing, continue with conservative drafting rather than blocking.

## Clarification Priority

If a follow-up question is necessary, ask for the smallest missing set in this order:

1. the method name and overall target
2. the four structure names or module decomposition
3. the key mechanism inside each structure
4. the linkage across structures if the pipeline order is unclear

Do not ask for formulas, pseudocode, or figure references before the essential method logic is clear.

## Persistence Rule

Treat the drafted method prose as source content first.

Preferred save target:

- `paper/content/method.md`

If `paper/content/` does not exist, create it before writing.

Only generate `sections/method.tex` when:

- the user explicitly asks for section-level LaTeX
- or a later LaTeX export step is assembling a venue template

Saving the drafted prose is the default behavior for this workflow, not an optional post-processing step.

## Overall Writing Requirements

- Use formal, restrained, coherent Chinese academic prose.
- Keep the logic progressive from total overview to resources, reasoning, enhancement, and final generation.
- Do not use bold formatting unless the user asks for it.
- Prefer explicit mechanism description over vague praise.
- Keep method terminology consistent throughout the section.
- Avoid fabricating modules, formulas, experiments, citations, or implementation details not supported by the user's input.
- If the user's wording is informal, rewrite it into proper academic language.
- Do not mention figure numbers, equation numbers, algorithm numbers, or pseudocode identifiers in the final prose.

## 3 Method Overview

### Writing Format

- Write a single paragraph under `3 方法描述`.
- The opening sentence should follow this logic:
  `为了解决{问题1}、{问题2}以及{问题3}，并实现{总体目标}，本文提出了{方法名称}（{方法简称}）`
- The middle should state the four core structures:
  `该方法包含若干核心结构，分别为{结构1名称}、{结构2名称}、{结构3名称}和{结构4名称}`
- The ending should summarize how the four structures connect and how earlier structures support later ones.

### Writing Requirements

- Target around 250-350 Chinese characters.
- Make clear why the method is proposed, what structures it contains, and how they collaborate.
- Do not turn this part into a list.
- Do not expand image, formula, or algorithm details here.

## 3.1 Structure 1

### Writing Format

- Write three paragraphs.
- Paragraph 1: explain why this structure is foundational, what objects it analyzes, what information it extracts, and how it supports later reasoning and generation; also state that it contains `[阶段1]` and `[阶段2]` or `[子过程1]` and `[子过程2]`.
- Paragraph 2: explain the core process of `[阶段1]` or `[子过程1]`, focusing on structure parsing, relation recognition, instance analysis, or prior construction.
- Paragraph 3: explain the result of `[阶段2]` or `[子过程2]`, focusing on the layered resources, knowledge bases, indexes, sample banks, or intermediate assets that are formed and how they support later reasoning, retrieval, and final generation.

### Writing Requirements

- Target around 700-1000 Chinese characters.
- Show a clear progression from foundational parsing/building to reusable resource formation.
- If the user provides layered resources such as schema-level, instance-level, and example-level knowledge, explain their differences and functions clearly.
- Compress formal definitions into prose; do not keep `定义1`, `式（1）`, or similar notation.

## 3.2 Structure 2

### Writing Format

- Write three paragraphs.
- Paragraph 1: explain why existing methods are insufficient for multi-step reasoning, nested queries, or complex condition combinations, and why `{中间表示}` or `{推理机制}` is introduced.
- Paragraph 2: explain the basic idea of `{中间表示}` or `{推理机制}`, including how natural language queries are mapped into a structured, executable, stepwise reasoning process while preserving the structural characteristics of the target output.
- Paragraph 3: summarize the generation process, including how key entities, constraints, relations, and aggregation needs are identified and organized into a complete reasoning chain, and how this chain serves later validation and generation.

### Writing Requirements

- Target around 700-1000 Chinese characters.
- Do not keep formulas, tuples, algorithm numbers, pseudocode, or line-by-line flow.
- You may keep core terms, but explain them in academic prose.
- Make clear how this structure improves reasoning continuity, structural accuracy, and semantic consistency.

## 3.3 Structure 3

### Writing Format

- Write four paragraphs.
- Paragraph 1: explain why extra knowledge support is needed in cross-domain, cross-database, or unseen-schema settings and what existing methods overlook.
- Paragraph 2: summarize the overall strategy, such as `检索-对齐-增强` or `检索-筛选-融合`, and explain why multi-granularity knowledge must be organized jointly.
- Paragraph 3: describe the knowledge acquisition stage, including how structure-level, instance-level, example-level, rule-level, or domain-level information is obtained from the user query and intermediate results, and what role each type of information plays.
- Paragraph 4: describe the filtering, alignment, and context enhancement stage, including how invalid or conflicting information is removed, high-quality knowledge is retained, and a strengthened prompt context is formed for later generation.

### Writing Requirements

- Target around 800-1100 Chinese characters.
- Make the logic `acquisition -> alignment/filtering -> enhancement` explicit.
- Do not include retrieval formulas, similarity formulas, or embedding formulas.
- You may compress examples into a single sentence, but do not write them as figure explanations.
- Clarify the distinct role of each knowledge layer.

## 3.4 Structure 4

### Writing Format

- Write three paragraphs.
- Paragraph 1: explain the remaining problems in final output generation, such as structural hallucination, semantic bias, missing knowledge, or formatting errors, and why a systematic multi-stage alignment or control mechanism is needed.
- Paragraph 2: summarize the overall strategy through `{机制1}`、`{机制2}`、`{机制3}` and `{机制4}`, and explain the role of each mechanism.
- Paragraph 3: summarize how the structure uses prior knowledge, intermediate reasoning results, and enhanced context to generate accurate and executable outputs, and explain the overall effect of the multi-stage control mechanism.

### Writing Requirements

- Target around 700-950 Chinese characters.
- Explain the division of labor and collaboration across multiple mechanisms.
- You may absorb the meaning of user-provided examples, but do not expand them as numbered case lists.
- Do not preserve figure references, format templates, or output code block requirements.
