# SCORM Course Generator

A **standalone web application** that turns a form (or a Markdown / Word document) into a complete, ready-to-import **SCORM 2004 (4th Edition)** course chapter, or a multi-chapter package, with an Opale-inspired pedagogical structure: grains, sequences, objectives, pedagogical boxes, glossary and self-assessment.

It is a **single HTML file** with no server, no installation, no build step and no external library. Everything runs in your browser and your content never leaves your computer.

---

## Features at a glance

| Area | What you get |
|---|---|
| **Authoring** | Metadata form, grain editor, 13 block types, 11 pedagogical boxes, drag-and-drop, undo/redo, chapter templates |
| **Discipline-independent** | Neutral defaults and discipline profiles (general, sciences, computer science, humanities, languages, health, law & management) that adapt the blocks offered |
| **Assessment** | 7 question types, per-answer feedback, objective-linked results, formative or summative mode, attempts limit, answer shuffling |
| **SCORM tracking** | Resume, completion criteria, score, interactions, objectives, session time, LOM metadata |
| **Import / export** | Import Markdown and Word (.docx), export Markdown, project files (.json), multi-chapter packages |
| **Look and feel** | 5 themes + custom colours, font choice, dark mode, text size buttons, print stylesheet, offline mode |

## Quick start

1. Download `Generateur_Cours_SCORM.html`.
2. Open it in a modern browser (Chrome or Edge recommended; Firefox 113+ and Safari 16.4+ also work).
3. Work through the four tabs:
   1. **Metadata**: profile, module, teacher, level, language, objectives, theme, assessment settings.
   2. **Content (grains)**: add grains, then blocks inside each grain.
   3. **Summary & quiz**: key takeaways, glossary, references and final quiz questions.
   4. **Multi-chapter package** (optional): assemble several chapters in one package.
4. Click **Preview**, then **Verify**, then **Export SCORM (.zip)**.
5. Upload the ZIP to your LMS (Moodle, Chamilo, Open edX, SCORM Cloud…) as a *SCORM package*.

> Downloads rely on the browser: open the file locally (`file://`) or from any web server.

## Authoring

### Metadata and profiles

Module, short code (logo), level, teacher, academic year, department, chapter number and title, cover icon, description, keywords, prerequisites, learning objectives (`text | Bloom level`), pass mark, estimated duration, rights/licence, and course language (**English** or **French**).

The **discipline profile** only filters what the editor offers (blocks, box types, default cover icon). Content already in a grain is never removed when you change profile.

### Blocks

| Block | Description |
|---|---|
| Paragraph | Light Markdown: `**bold**`, `*italic*`, `` `code` `` |
| Heading | Sub-title inside a grain |
| List | Bulleted or numbered |
| Table | One row per line, cells separated by `\|`, first line = header |
| Pedagogical box | Definition, Property / Theorem, Remark, Warning, Important, Example, Tip, Method, Concept, Key takeaway, Going further (custom title optional) |
| Formula | LaTeX, rendered with MathJax (enabled automatically) |
| Quotation | With author / source |
| Code | Labelled code block with basic syntax highlighting |
| Multi-tab code | The same algorithm in several languages |
| Sequence label | Opale-style “Sequence n · Title” tag |
| Interactive exercise | Statement, optional code, answer revealed on click |
| Mini-quiz | Single-choice self-check with instant feedback (not part of the SCORM score) |
| Image | Uploaded, resized (max 1000 px), embedded; **alternative text required**, caption, width |

### Editing comfort

- Sections and sub-sections with automatic numbering (1, 1.1, 2…), three colour themes per grain.
- **Drag and drop** (⠿ handle) for grains and blocks, including between grains; up/down buttons, duplicate, collapse.
- **Undo / redo** (↶ ↷, Ctrl+Z / Ctrl+Y, 40 levels).
- **Chapter templates**: lecture, practical work, case study.
- **Verify** detects missing metadata, untitled grains, images without alternative text, invalid quizzes, unknown objectives, and offline-mode conflicts.
- Project files (`.json`) and automatic browser save.

### Writing syntax

**Multi-tab code**: start each tab with a `###` line.

```text
### Pseudocode
x ← 1
### C
int x = 1;
```

**Table**: cells separated by `|`.

```text
Type | Pseudocode | C
Integer | Integer | int
```

**Glossary**: `term | definition`. **Objectives**: `text | Bloom level`.

## Assessment

Final quiz question types: **single choice, multiple choice, true/false, short text** (case- and accent-insensitive, several accepted answers separated by `|`), **numeric** (with tolerance), **ordering** and **matching**.

- Per-answer feedback for choices: `Answer text :: comment`.
- Link each question to an objective (`O1`, `O2`…) to get an objective-by-objective result.
- **Formative** mode (check button per question) or **summative** mode (correction only on submission).
- Maximum number of attempts, optional shuffling of answers, configurable pass mark.

## SCORM tracking

The generated course detects SCORM 2004 (and SCORM 1.2) APIs and reports:

- **Resume**: current page and visited pages are restored on relaunch.
- **Completion criterion**: all pages visited, quiz passed, or both.
- **Score, pass/fail status**, one **interaction per question** (with its SCORM type), **objectives**, session time and exit mode.
- **LOM / Dublin Core metadata** in the manifest (title, language, description, keywords, author, duration, rights).

## Import and export

### Markdown

```markdown
---
module: Biology
code: BIO1
chapter: The cell
teacher: Dr X
keywords: cell, membrane
duration: 45
---
## Structure          <!-- ## = section, ### = sub-section, #### = heading -->
Paragraph text.

> [!WARNING] Title
> Warning box text.
```

Supported: front-matter metadata (`module, code, level, teacher, year, dept, chapter, num, lang, keywords, description, duration, license`), lists, tables, fenced code, quotations, `$$…$$` formulas and boxes through `> [!NOTE|TIP|WARNING|IMPORTANT|DEFINITION|EXAMPLE|METHOD|PROPERTY|SUMMARY|MORE]`.

### Word (.docx)

Heading styles become sections, plus bold/italic, lists and tables. Images in the document are not imported. You choose to replace the current grains or append to them.

### Markdown export

Exports text, lists, tables, code, quotations and boxes. Mini-quizzes, images and interactive exercises are not exported faithfully.

### Multi-chapter package

In the fourth tab, add the current project or several `.json` files, order the chapters and export one ZIP: **one SCO per chapter** (`ch1/`, `ch2/`…), a course menu in the LMS, and course-level metadata.

## Appearance

Five themes (Ocean, Forest, Burgundy, Slate, Violet) or custom colours, and three font choices. Generated courses include a dark-mode toggle, text size buttons and a print stylesheet. **Offline mode** removes every external resource (Google Fonts, MathJax); system fonts are used and formulas are not rendered.

## Output

A single chapter ZIP contains, at its root:

```text
imsmanifest.xml    # SCORM 2004 manifest with LOM metadata (one SCO)
index.html         # content, CSS, navigation, SCORM runtime, quiz engine
```

A multi-chapter package contains `imsmanifest.xml` plus `ch1/index.html`, `ch2/index.html`, …

## Technical notes

- Pure HTML, CSS and vanilla JavaScript; the ZIP is built by a small built-in writer, and `.docx` files are read with the browser’s native decompression.
- Online mode loads *Outfit* and *Fira Code* from Google Fonts (system fallbacks otherwise) and MathJax from a CDN when formulas are used.
- Images are stored as data URIs inside `index.html`; large images increase file size.
- Browser storage keys: `scormgen` (current project), `scormgen_pk` (package chapters). Export project files before clearing browser data.
- Tested in headless Chromium with a simulated SCORM 2004 API. Please report results on real LMS platforms.

## Limitations and ideas

- No right-to-left layout (Arabic) yet.
- Fonts are not embedded; offline mode falls back to system fonts.
- Every quiz question is worth one point; no weighting.
- Syntax highlighting is generic, not language-specific.
- Undo/redo does not cover the list of chapters of a package.
- Ideas: audio/video blocks, per-language highlighting, RTL support, question weighting, xAPI / cmi5 export.

## Contributing

Issues and pull requests are welcome. Please mention your browser and LMS when reporting a problem.


## License

Dr. Ammar Ladjailia

Souk Ahras university -Algeria- 41000

a.ladjailia@univ-soukahras.dz

The project is licensed under the MIT License.
