---
description: Generate developer docs, a README, and a non-technical PDF spec for this project
argument-hint: [optional notes, e.g. "skip the PDF" or "brand color is teal"]
---

You are generating documentation for the project in the current working directory.

If the user added any notes, follow them closely:
$ARGUMENTS

## Step 1 — Study the repo first (don't write anything yet)
Explore before documenting. Work out:
- What the project is and who it's for.
- How it runs: entry points, dependencies, build/run commands, dev vs production.
- The architecture and how the parts relate.
- Folder/file organization, naming conventions, error-handling and logging style.
- The patterns and idioms the team repeats.
Treat any existing README as suspect — if it looks stale or wrong, say so and don't trust it.

## Step 2 — Produce three documents

1. **PROJECT_DOC.md** — the developer deep-dive. Cover: what it is, the architecture
   (with a simple ASCII diagram), how the code is organized, the data model, the key
   request/data flows, authentication, and any billing/background-job logic. Explain
   the *why*, not just the *what*. Call out the flows that are easy to get wrong.

2. **README.md** — a quick start that hands off to PROJECT_DOC for depth. Include: a
   one-paragraph overview, the stack, how to run locally vs in production, formatting,
   dependencies, and deploy steps. Keep it short.

3. **docs/<NAME>_PROJECT_SPECIFICATION.pdf** — a non-technical specification for
   stakeholders, with real diagrams. Build it as a styled HTML file with inline SVG
   diagrams (cover page, contents, plain-language sections, a glossary), then render
   it to PDF with headless Chrome:

   "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless \
     --disable-gpu --no-pdf-header-footer \
     --print-to-pdf="docs/NAME_PROJECT_SPECIFICATION.pdf" "docs/NAME_PROJECT_SPECIFICATION.html"

   (On Linux, use `google-chrome` or `chromium` instead of the macOS path.)

## Tone for all of it
Write like a teammate explaining the project to a new hire — not like a spec generator.
Use contractions, explain trade-offs, and avoid heavy **bold** markers and rigid
numbered tables-of-contents in the markdown files. The PDF is for non-technical readers,
so keep its language plain and let the diagrams carry the structure.

## Finish
Briefly tell the user which files you created or changed, and flag anything you were
unsure about (e.g. a stale README you replaced, or a section you guessed at).
