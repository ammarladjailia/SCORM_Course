# SCORM Course Generator

A **standalone web application** that turns a simple form into a complete, ready-to-import **SCORM 2004 (4th Edition)** course chapter, with an Opale-inspired pedagogical structure (grains, sequences, objectives, glossary, self-assessment).

No server, no installation, no build step: it is a single HTML file that runs entirely in your browser. Your content never leaves your computer.

---

## Features

- **Metadata form**: module, short code, level, teacher, academic year, department, chapter number and title, cover icon, keywords, description, prerequisites, learning objectives (with Bloom levels), pass mark.
- **Two course languages**: English or French (interface of the generated course, buttons, feedback messages and SCORM runtime messages).
- **Grain editor**: sections and sub-sections with automatic numbering (1, 1.1, 2…), three colour themes, reordering, duplication and collapsing.
- **Rich content blocks**:

  | Block | Description |
  |---|---|
  | Paragraph | Light Markdown: `**bold**`, `*italic*`, `` `code` `` |
  | Heading | Sub-title inside a grain |
  | List | Bulleted or numbered |
  | Table | One row per line, cells separated by `\|`, first line = header |
  | Callout boxes | Definition, Remark, Important, Example, Concept (custom title optional) |
  | Code | Labelled code block with basic syntax highlighting |
  | Multi-tab code | Same algorithm in several languages (Pseudocode, C, Java…) |
  | Interactive exercise | Statement, optional code, answer revealed on click |
  | Mini-quiz | Single-choice self-check with instant feedback and explanation |
  | Sequence label | Opale-style “Sequence n · Title” tag |
  | Image | Uploaded, resized (max 1000 px) and embedded; caption and width |

- **Automatic pages**: cover page, prerequisites, objectives table, synthesis (key takeaways, glossary, references) and final quiz.
- **SCORM runtime included**: completion status and quiz score are sent to the LMS (SCORM 2004 and SCORM 1.2 APIs detected).
- **Live preview**, **validation** before export, **project save/load** (`.json`) and browser auto-save.
- Optional **MathJax** support for `$…$` and `$$…$$` formulas.

## Quick start

1. Download `Generateur_Cours_SCORM.html`.
2. Open it in a modern browser (Chrome or Edge recommended; Firefox and Safari should also work).
3. Fill in the three tabs:
   1. **Metadata**
   2. **Content (grains)**: add grains, then blocks inside each grain.
   3. **Summary & quiz**: takeaways, glossary, references, final quiz questions.
4. Click **Preview** to check the result, **Verify** to detect problems, then **Export SCORM (.zip)**.
5. Upload the ZIP to your LMS (Moodle, Chamilo, Open edX, SCORM Cloud…) as a *SCORM package*.

> The download button relies on the browser: open the file locally (`file://`) or from any web server.

## Writing syntax

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
Real | Real | float
```

**Glossary**: `term | definition`, one per line. **Objectives**: `text | Bloom level`, one per line. **Quiz answers**: one answer per line, then the number of the correct one.

## Output

The exported ZIP contains, at its root:

```text
imsmanifest.xml    # SCORM 2004 manifest (one SCO)
index.html         # the whole chapter: content, CSS, navigation, SCORM runtime, quiz
```

The chapter has a header, progress bar, side navigation, previous/next buttons, interactive blocks, and a final quiz graded on submission (score sent to the LMS; pass mark configurable).

## Project files

Use **Project (.json)** to save your work and **Open** to reload it. The same data is also stored automatically in the browser’s local storage, so clear it only after exporting a project file.

## Technical notes

- Pure HTML, CSS and vanilla JavaScript; the ZIP is built by a small built-in writer, so there is no external library.
- The generated course loads *Outfit* and *Fira Code* from Google Fonts (system fallbacks are used offline); MathJax is loaded from a CDN only if enabled.
- Images are stored as data URIs inside `index.html` (large images increase file size).
- One chapter = one SCO. To build a multi-chapter course, export each chapter and combine them in your LMS.

## Limitations and ideas

- Quiz questions are single-answer (no multiple-answer, matching or free-text questions yet).
- Syntax highlighting is generic and not language-specific.
- No multi-chapter manifest or SCORM sequencing rules.
- Ideas: multiple-answer questions, per-language highlighting, audio/video blocks, multi-SCO packages, theme customisation.

## Contributing

Issues and pull requests are welcome. Please describe the LMS and browser you tested with when reporting a problem.

## License

Dr. Ammar Ladjailia

Souk Ahras university -Algeria- 41000

a.ladjailia@univ-soukahras.dz

The project is licensed under the MIT License.
