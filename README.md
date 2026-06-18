# projectdocs

A Claude Code plugin that documents a project for you. Point it at a repo and it
explores the code first, then writes three things: a developer deep-dive
(`PROJECT_DOC.md`), a quick-start `README.md`, and a non-technical PDF spec for
stakeholders. You can also hand it specific instructions and it'll follow them.

## Install

This is a Claude Code plugin, so there's nothing to build or compile.

To install from a marketplace, register the marketplace repo, then install the plugin
by name:

```
/plugin marketplace https://github.com/Usama-Laeeq/ProjectDoc-Plugin.git
/plugin install projectdocs
```

## Use it

From inside any project you want documented:

```
/projectdocs
```

You can pass notes to steer the run. They get woven into how the docs come out:

```
/projectdocs skip the PDF
/projectdocs brand color is teal
/projectdocs only add a README, nothing else
```

## The PDF step

The non-technical spec renders through headless Google Chrome. On macOS the command
the plugin uses looks like this:

```
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless \
  --disable-gpu --no-pdf-header-footer \
  --print-to-pdf="docs/NAME_PROJECT_SPECIFICATION.pdf" \
  "docs/NAME_PROJECT_SPECIFICATION.html"
```

On Linux, swap the macOS path for `google-chrome` or `chromium`:

```
google-chrome --headless --disable-gpu --no-pdf-header-footer \
  --print-to-pdf="docs/NAME_PROJECT_SPECIFICATION.pdf" \
  "docs/NAME_PROJECT_SPECIFICATION.html"
```

On Windows, call the Chrome executable directly. From PowerShell (use the backtick `` ` ``
for line continuation):

```
& "C:\Program Files\Google\Chrome\Application\chrome.exe" --headless --disable-gpu `
  --no-pdf-header-footer `
  --print-to-pdf="docs/NAME_PROJECT_SPECIFICATION.pdf" `
  "docs/NAME_PROJECT_SPECIFICATION.html"
```

If Chrome lives somewhere else, check `C:\Program Files (x86)\Google\Chrome\Application\`
too. The path differs by install, but the flags are the same across all three platforms.

If Chrome isn't installed, the PDF step is the only thing that won't work — the two
markdown docs are unaffected.

## Layout

```
.claude-plugin/
  plugin.json        plugin metadata (name, description, version, author)
  marketplace.json   marketplace entry
commands/
  projectdocs.md     the /projectdocs command and its instructions
```

The real logic lives in `commands/projectdocs.md` — that's the prompt that tells Claude
how to explore a repo and what to write. Tweak it there if you want to change what the
docs cover or how they read.

## Author

Usama Laeeq
