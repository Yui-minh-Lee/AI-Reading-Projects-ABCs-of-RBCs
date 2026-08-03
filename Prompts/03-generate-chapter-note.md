# Prompt: Generate Chapter Note

Use high reasoning.

Read `AGENTS.md` first.

Please process this chapter source file:

`Sources/Chapters/[CHAPTER_FILE]`

Create a direct-reading narrative lecture note at:

`ChapterNotes/[CHAPTER_NOTE_FILE]`

The note should largely replace first-pass reading of the original chapter while preserving approximately 80-90% of the chapter's core learning value. For central chapters, aim closer to 85-90%.

Use this structure:

# Chapter X — Lecture Note

> Importance: ★☆☆☆☆ to ★★★★★
> Suggested audit model: medium / high / xhigh
> Reading mode: careful / normal / skim
> Estimated note reading time: X minutes
> Source reliability: text OK / visuals need manual review / uncertain

## 0. How to read this note

## 1. Opening: 本章的核心问题

## 2. Main Lecture

## 3. Compact Summary: What You Must Retain

## 4. Figures, Tables, and Formulas to Check in the Original

## 5. Questions and Answers

Style rules:

- Main Lecture should be the largest section, roughly 65-80% of the note.
- Write in smooth, coherent Chinese prose.
- Explain the author's logic step by step.
- Do not hide non-obvious reasoning. If a conclusion or transition would make a reader ask "why does this follow?", explain the missing bridge.
- Integrate key concepts into the narrative instead of isolating them into glossary-like sections.
- Explain technical terms selectively, not repeatedly.
- Compact Summary should be short: 6-8 bullets maximum, 1-2 sentences each.
- Q&A should test understanding and stay concise.
- Preserve important English terms.
- If you create your own explanatory example, clearly mark it with `【】` and state that it is an added illustration, not from the source text.
- Do not copy long passages from the book.
- Do not fabricate page numbers.

Chart/table/formula rule:

If an important figure, table, formula, or visual framework may not be reliably captured from PDF text, add this warning near the relevant discussion:

> ⚠️【需要回原文看图】这里涉及重要图表/表格/公式，PDF 文本提取可能不足以完整保留信息。建议回到原文核对。

Do not screenshot or embed figures by default.

Other rules:

- Do not create separate glossary, concept, formula, or txt extraction files.
- Do not modify source files.
- Do not create a separate Q&A file unless I explicitly ask.
