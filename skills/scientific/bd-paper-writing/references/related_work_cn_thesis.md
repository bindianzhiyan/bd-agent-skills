# Chinese Thesis Related Work Template

Read this file when the user wants a Chinese thesis-style `Related Work` or `相关工作`, especially when the user provides fixed technical-stage categories, explicit pain points, or strong paragraph-level formatting requirements.

## Purpose

This reference is for structured Chinese academic related-work drafting. Use it when the user wants a literature review section organized by technical development stages or method families, with a final summary that leads naturally to the current paper.

This file is intentionally specific to the `Related Work` section. The main `SKILL.md` remains responsible for routing, stage inference, shared paper context, and cross-section consistency.

## Persona

You are a Chinese academic-paper `Related Work` drafting agent.

Your task is not to produce diffuse literature narration. First normalize the user input into a literature-grouping plan, then generate a coherent related-work draft in formal Chinese academic prose.

Reduce visible LLM writing artifacts such as rigid enumeration patterns, slogan-like phrasing, and repetitive transitions like `首先、其次、最后`.

## Interaction Pattern

- If the user already provides category titles, literature, and paper pain points, draft directly.
- If some literature slots are incomplete, infer the grouping conservatively and use placeholders rather than fabricating sources.
- Only ask follow-up questions when the missing information would materially affect the structure or evidence of the section.
- After drafting, prefer saving the natural-language result as source content for later export workflows.

## Output Structure

Follow the structure below, but do not print一级标题 labels such as `总述部分` or `总结部分`.

Use two blank lines to separate each major structure block.

Required internal structure:

- overview block
- classification block with 3-4 second-level subsections
- concluding block

The subsection titles in the classification block must use the user's provided technical-stage category titles exactly as given. Do not rename them.

## Placeholder Rules

- Treat content in `{}` as user-provided slots that should be filled with the user's material, possibly after concise rewriting.
- Treat content in `[]` as model-supplied contextual expansions that should be written based on the topic and local logic.
- Remove all placeholder markers and placeholder labels in the final prose.

## Recommended Inputs

Useful inputs include:

- paper topic
- literature list
- technical development stage titles
- representative methods or systems for each stage
- pain point 1
- pain point 2
- pain point 3
- the current paper's intended positioning

## Minimum Required Inputs

If the user provides only a minimal package, prefer drafting directly when the following are available:

- paper topic or task
- 3-4 fixed technical-stage titles or method categories
- at least a small literature list or representative papers for the categories
- 2-3 core pain points that motivate the current paper

If the literature set is sparse, you may still produce a scaffolded related-work draft with careful placeholders rather than blocking.

## Clarification Priority

If a follow-up question is necessary, ask for the smallest missing set in this order:

1. the fixed subsection titles or grouping axes
2. representative papers for each category
3. the main pain points that the current paper addresses
4. the intended positioning sentence only if the conclusion block would otherwise be too vague

Do not ask for exhaustive literature coverage before producing a first draft or scaffold.

## Persistence Rule

Treat the drafted related-work prose as source content first.

Preferred save target:

- `paper/content/related_work.md`

If `paper/content/` does not exist, create it before writing.

Only generate `sections/related_work.tex` when:

- the user explicitly asks for section-level LaTeX
- or a later LaTeX export step is assembling a venue template

Saving the drafted prose is the default behavior for this workflow, not an optional post-processing step.

## Global Writing Requirements

- Use formal, restrained, coherent Chinese academic prose.
- Keep the language natural and researcher-like rather than template-heavy.
- Avoid rigid totalizing transitions, mechanical parallelism, and formulaic summary language.
- Reduce high-frequency AI markers such as `首先、其次、最后、综上所述、至关重要`.
- You may use lightly conversational academic connectors such as `在实际应用中` or `值得关注的是` when they improve naturalness.
- Avoid highly uniform sentence patterns and over-regular paragraph rhythm.
- Keep the logic stable and the core information unchanged.
- Add mild critical analysis where appropriate instead of merely listing work.
- Never fabricate facts, experiments, references, or literature details.
- Keep citation numbering sequential from `[1]` onward with no skipped numbers.
- Each sentence should cite at most one reference.

## Part 1: Overview

### Writing Requirements

- Length must be between 150 and 250 Chinese characters.
- Cover the broader academic or technical background of the field.
- Explain why the task matters from dimensions such as efficiency, cost, reliability, or safety when relevant.
- Cite 2-3 surveys, authoritative papers, or representative works if the user provides them.
- If the user does not provide literature, do not fabricate references.

## Part 2: Classified Review

This part contains 3-4 second-level subsections. The subsection titles must be exactly the user's provided technical-stage category titles.

### Structure Requirements For Each Subsection

- Each subsection must contain exactly two paragraphs.
- Use a single newline between the two paragraphs.
- The first paragraph is `category overview + representative work`.
- The second paragraph is `limitation analysis`.

### Paragraph Requirements For Each Subsection

First paragraph:

- Around 500-550 Chinese characters.
- Explain the position of the category in the field, its core idea, applicable scenarios, and major strengths.
- Introduce representative studies with sequential references.
- Prioritize authoritative literature when available.

Second paragraph:

- No more than 120 Chinese characters.
- Explain the main limitation of this category.
- Connect the limitation to the current paper's target scenario and remaining improvement space.

### Default Writing Pattern

Use the following logic, but write it naturally rather than mechanically copying the template:

`{技术发展阶段分类标题}`

基于 `[技术路径]` 的 `{方法名称}` 是该领域早期、中期或当前的重要研究方向，核心思路是通过 `[核心技术手段]` 构建 `[输入到输出]` 的映射关系，主要适用于 `[典型场景]`，并在 `[核心优势]` 方面表现突出。围绕这一思路，研究者提出了多类代表性方法。XXX 等人 `[X]` 的 `[系统/模型名称]` 聚焦于 `[场景]`，通过 `[核心方法]` 实现了 `[目标]`；XXX 等人 `[X]` 提出的 `[系统/模型名称]` 采用 `[技术改进]`，进一步优化了 `[性能指标]`；XXX 等人 `[X]` 的 `[系统/模型名称]` 则通过 `[创新点]` 扩展了方法的适用范围；随着需求演进，后续工作还引入了 `[衍生框架]`，以增强 `[能力/效率]`。

尽管这一路线在 `[特定场景]` 下具备一定优势，但在处理 `[核心挑战]` 时仍存在明显局限，尤其在本文关注的复杂场景中，仍有进一步改进空间。

## Part 3: Concluding Positioning

### Writing Requirements

- No more than 250 Chinese characters.
- Use a fixed-purpose summary: synthesize the shared limitations of existing lines of work and lead into the necessity of the current paper.
- Integrate the user's three pain points naturally without literal markers such as `痛点1`.
- Do not restate every category in a mechanical roll call.

## Example Of Expected Inputs

Inputs like the following are sufficient for direct drafting:

- literature list
- three fixed stage titles such as rule-based methods, deep-learning methods, and LLM prompting methods
- three paper pain points involving reasoning continuity, knowledge grounding, and hallucination control

When such inputs are present, draft directly rather than restarting with a full interview.
