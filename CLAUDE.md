# LLM Wiki

A personal knowledge base maintained by Claude Code.
Based on Andrej Karpathy's LLM Wiki pattern .

## Purpose

This wiki is a structured, interlinked knowledge base about the topics covered in a course of bioinformatics.
Claude maintains the wiki. The human curates sources, asks questions, and guides the analysis.

## Folder structure

```
raw/               -- source documents (immutable -- never modify these)
raw/graphics/      -- curated figures; high relevance -- always check when ingesting
wiki/pages/        -- markdown pages maintained by Claude
wiki/glossary/     -- atomic entries: one file per term, concept, or exercise
wiki/index.md      -- table of contents for the entire wiki
wiki/study_path.md -- the suggested way to study the material in the wiki
wiki/exam_prep.md  -- concepts and questions that will be usefull during examination
wiki/log.md        -- append-only record of all operations
```

## Ingest workflow

When the user adds a new source to `raw/` and asks you to ingest it:

1. Read the full source document
2. Discuss key takeaways with the user before writing anything
3. Create a summary page in `wiki/` named after the source
4. Create or update concept pages for each major idea or entity
5. Add wiki-links ([[page-name]]) to connect related pages
6. Update `wiki/index.md` with new pages and one-line descriptions
7. For each new term, concept, or exercise introduced by the source, create an atomic entry in `wiki/glossary/` following the **Glossary entry format** below
8. Update `wiki/exam_prep.md` with key concepts that are useful to grasp the material, flashcards, Atomic question & answer. A set of sections to review the key ideas linearly.
9. Update `wiki/study_path.md` . This will be the place to go when the learner doesn't know what to study next in the wiki.
10. If you ingest a file that is some sort of exercise use the template `tempates/exercise.md` to generate a the related file and then add it to the `wiki/index.md` in a section dedicated to exercises.
11. Append an entry to `wiki/log.md` with the date, source name, and what changed

A single source may touch 10-15 wiki pages. That is normal.

## Page format

Every wiki page should follow this structure:

```markdown
# Page Title

**Summary**: One to two sentences describing this page.

**Sources**: List of raw source files this page draws from if possible using obsidian links.

**Last updated**: Date of most recent update.

---

Main content goes here. Use clear headings and short paragraphs.

Link to related concepts using [[wiki-links]] throughout the text.

Embed relevant figures from raw sources inline, immediately after the paragraph that references them:
- Standalone image file: `![caption](../../raw/image.png)`
- PDF figure: `[[raw/source.pdf#page=N|Caption – source]]`

## Related pages

- [[related-concept-1]]
- [[related-concept-2]]
  
## Other sources
Here you can specify material form the web or books that cover the same material or some closely related informations. Can be links to web pages, chapters of books, youtube videos, links to articles or papers.

## Tests your self
Flashcards, Q&A, mnemonics... whatever can be useful to test preparation about the topic covered in this page
```

## Glossary entry format

Each file in `wiki/glossary/` is an atomic note about a single term, concept, or problem. The filename is the entry's title (spaces are allowed — e.g., `Shine-Delgarno sequence.md`).

Every entry must begin with Obsidian frontmatter that declares its type and, where relevant, its course module:

```yaml
---
tags:
  - __DEFINITION   # or __CONCEPT or __EXECUTABLE
  - Module1        # optional: course module this entry belongs to
---
```

### Types

| Tag | When to use | Content |
|-----|-------------|---------|
| `__DEFINITION` | A specific term that needs a precise definition | Concise definition; add graphics or links when relevant |
| `__CONCEPT` | A broader idea that requires brief explanation | Short explanation; feel free to add links to graphics or online resources |
| `__EXECUTABLE` | A problem or exercise the learner should be able to solve | Brief strategy to approach and solve the challenge |

### Rules for glossary entries

- One entry per file — never combine multiple terms in one file.
- Filename = the exact term or question as it would appear in an exam or textbook.
- Add a module tag (e.g., `Module1`, `Module2`) whenever the entry belongs to a specific course module.
- Graphics and wiki-links (`[[page-name]]`) are welcome inside entries.
- Do not add the standard page-format headers (Summary, Sources, Last updated) — the frontmatter is sufficient.

### Optional elements

**Footnotes** — use Obsidian footnote syntax (`[^1]` in text, `[^1]: ...` at the end of the file) when a word or phrase in the main definition might trip up the reader but is too tangential to explain inline. Good candidates: jargon assumed by the definition, notation differences (e.g. DNA vs RNA alphabet), or a prerequisite concept the reader may not have. Do not footnote things that are already obvious from context.

**# TLDR** — add a `# TLDR` section (before the footnotes block) when the core idea can be captured in one or two sentences and there is a real chance the reader will grasp "enough" from that alone. Good candidates: definitions where the intuition is simple but the formal explanation is long, or concepts with a memorable one-liner. Omit it when the entry is already brief or when a shortcut would mislead.

## Imagery

Wiki pages should be enriched with visuals from the raw source material whenever they aid understanding:

- **Embedded images**: if the raw folder contains standalone image files (`.png`, `.jpg`, `.svg`, etc.) use a standard markdown embed: `![description](../../raw/filename.png)`
- **PDF page references**: for figures inside a PDF, link directly to the page using an Obsidian page-anchor: `[[raw/source.pdf#page=12|Figure 3 – Protein folding diagram]]`. Obsidian renders this as a clickable link that opens the PDF at that page.
- **`raw/graphics/` subfolder**: this folder contains curated, high-relevance figures. When ingesting or updating a page, always check this folder for graphics related to the topic. Every image found there that is relevant to a page **must** be embedded and accompanied by a paragraph explaining what the figure shows and why it matters.
- Place visuals inline, immediately after the paragraph that references them, not at the end of the page.
- Prefer figures that show a process, structure, or comparison — screenshots of plain text add little value.
- Always caption every image with a brief description and the source reference.

## Citation rules

- Every factual claim should reference its source file or online reference
- Use the format (source: filename.pdf or source link) linking the page when necessary `[[item-in-raw-foloder#page=123|better name to identify]]`
- If two sources disagree, note the contradiction explicitly
- If a claim has no source, mark it as needing verification
## Question answering

When the user asks a question:

1. Read `wiki/index.md` first to find relevant pages
2. Read those pages and synthesize an answer
3. Cite specific wiki pages in your response
4. If the answer is not in the wiki, say so clearly
5. If the answer is valuable, offer to save it as a new wiki page

Good answers should be filed back into the wiki so they compound over time.

## Lint

When the user asks you to lint or audit the wiki:

- Check for contradictions between pages
- Find orphan pages (no inbound links from other pages)
- Identify concepts mentioned in pages that lack their own page
- Flag claims that may be outdated based on newer sources
- Check that all pages follow the page format above
- Check that all `wiki/glossary/` entries have valid frontmatter with at least one recognised type tag (`__DEFINITION`, `__CONCEPT`, `__EXECUTABLE`)
- Report findings as a numbered list with suggested fixes

## Rules

- Never modify anything in the `raw/` folder
- Always update `wiki/index.md` and `wiki/log.md` after changes
- Keep page names lowercase with hyphens (e.g. `machine-learning.md`)
- Write in clear, plain language
- When uncertain about how to categorize something, ask the user
- Whenever a formula, equation, or mathematical expression is relevant, write it using LaTeX syntax: inline with `$...$` and display (block) with `$$...$$`
