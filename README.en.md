# Poetry TeX Template

[中文说明](./README.md)

This repository provides a Chinese poetry book template built with `LuaLaTeX + LuaTeX-ja`. It includes:
- Automatic table-of-contents entries from poem titles
- Single-page centered layout for each poem
- Optional poem notes (footnotes)
- Full-page figure insertion
- Chinese-numbered page and figure labels

For reuse, start from:
- `src/poetry.template.tex`: reusable template (recommended starting point)
- `src/poetry.tex`: author's full poetry collection (reference)
- `poetry.ltjruby`: legacy Lua helper script (optional, not required for base compilation)

## 1. Requirements

Install the following first:
- TeX Live (or equivalent distribution) with `lualatex`
- `luatexja`, `luatexja-fontspec`, `luatexja-ruby`
- Chinese fonts (at least one Song-style font and one Kai-style font)

Default fonts in the template:
- Main font: `STSONG`
- Bold font: `STZHONGS`
- Kai font: `KaiTi`

If these fonts are unavailable on your system, update the font config section in `src/poetry.template.tex`.

## 2. Quick Start

1. Copy the template and create your own manuscript:
```powershell
Copy-Item src/poetry.template.tex src/my-poetry.tex
```

2. Edit `src/my-poetry.tex` and replace:
- Title (`你的詩集標題`)
- Preface text
- Sample poems and figure captions
- Font settings (if needed)

3. Compile from the repository root:
```powershell
lualatex --interaction=nonstopmode --halt-on-error src/my-poetry.tex
```

Notes:
- Compile twice to stabilize ToC and references.
- If compiling from `src/`, use the same command with filename `my-poetry.tex`.

## 3. Template Commands

### `\PoemWithNote`

```tex
\PoemWithNote{Title}{Poem body}{Note}
```

- `Title`: added to ToC.
- `Poem body`: use `\par` for line breaks.
- `Note`: optional; use `{}` when empty.

Example:
```tex
\PoemWithNote{Moon Night}{
Moon sinks, bell fades\par
River clears, wild goose late\par
}{Written on an autumn night.}
```

### `\PoemFigure`

```tex
\PoemFigure[angle][width]{image path}{caption}{label}
```

Example:
```tex
\PoemFigure[90][0.8\textwidth]{../img/anshun.png}{Temple at Night}{fig:example}
```

## 4. FAQ

### Q1: Missing font errors

Update the font section at the top of the template:
```tex
\newcommand{\PoetryMainFont}{Your Song font name}
\newcommand{\PoetryBoldFont}{Your bold font name}
\newcommand{\PoetryKaiFont}{Your Kai font name}
```

### Q2: Wrong or empty table of contents

Make sure `\tableofcontents` exists and compile twice.

### Q3: Images are not shown

Check image paths relative to your `.tex` file. On Windows, prefer `/` as path separator.

## 5. Reuse Notes

If you republish or adapt this template, keep a link to this repository and note your style changes (page size, fonts, footnote style, etc.) for easier maintenance.
