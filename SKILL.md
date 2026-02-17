---
name: skill-doc-formatter
displayName: Skill Doc Formatter | ClawHub
description: Formats SKILL.md (OpenClaw/Cursor skill docs) for optimal display on ClawHub. Produces a consistent structure—Description, Installation, Usage with benefit-focused examples, and Commands—so skill pages are clear and scannable.
version: 1.0.0
---

# Skill Doc Formatter | ClawHub

Formats **SKILL.md** skill documentation for optimal display on ClawHub. Output uses a consistent structure so skill pages are easy to scan: **Description**, **Installation**, **Usage** (with examples that showcase benefits), and **Commands**.

## When to use

- Preparing or updating a skill for publication on ClawHub
- Converting an existing SKILL.md into the ClawHub-recommended layout
- Generating usage examples from a skill's description when examples are missing
- Standardizing multiple skills to the same doc structure

## Target structure (ClawHub-optimized)

The formatter produces or normalizes these sections:

| Section | Purpose |
|--------|--------|
| **Description** | One clear blurb (from frontmatter `description` + optional short intro). What the skill does and when to use it. |
| **Installation** | How to install: `clawhub install <skill>`, `git clone`, or other steps. Copy-paste ready. |
| **Usage** | How to use the skill: steps, scenarios, or workflow. Concise. |
| **Examples** | Concrete examples that showcase benefits (e.g. before/after, sample commands with outcomes). Generated if missing. |
| **Commands** | All CLI commands in one block with brief descriptions. Absolute paths or placeholders like `<skill-dir>`. |

## How to run

From the skill you want to format, or from the formatter skill:

```bash
# Format a skill by path (output to stdout)
python3 /path/to/skill-doc-formatter/scripts/format_skill_doc.py /path/to/other-skill/SKILL.md

# Write formatted result back to a new file
python3 scripts/format_skill_doc.py /path/to/skill/SKILL.md -o /path/to/skill/SKILL.clawhub.md

# Use formatter's own SKILL.md as input (demo)
python3 scripts/format_skill_doc.py SKILL.md
```

Options:

- `-o FILE` — Write output to FILE instead of stdout.
- `--generate-examples` — Generate example usage blocks from the description when Examples section is missing or thin.
- `--inplace` — Overwrite the input SKILL.md with the formatted version (use with care; prefer `-o` for review).

## What the script does

1. **Parse** the existing SKILL.md (YAML frontmatter + markdown body).
2. **Map** existing `##` sections to Description / Installation / Usage / Examples / Commands (by title and content).
3. **Normalize** section order and headings to the ClawHub structure.
4. **Extract or generate**:
   - Description: frontmatter `description` + first paragraph or intro.
   - Installation: looks for "install", "clawhub", "clone", "npm" etc.; otherwise adds a placeholder.
   - Usage: keeps or merges "Usage", "When to use", "How to use" content.
   - Examples: keeps existing examples; with `--generate-examples`, adds 1–2 benefit-focused examples from the description.
   - Commands: collects fenced bash/code blocks and list items that look like CLI commands; merges into one **Commands** section.
5. **Emit** a single markdown document with clean headings and optional table of contents.

## Manual template

If you prefer to edit by hand, use this structure in your SKILL.md:

```markdown
---
name: your-skill
displayName: Your Skill | OpenClaw Skill
description: One-sentence description. Use when [trigger scenarios].
version: 1.0.0
---

# Your Skill Name

Short intro: what it does and why it matters (1–2 sentences).

## Description

Clear description: what the skill does and when to use it. Scannable.

## Installation

```bash
clawhub install your-skill
# or: git clone https://github.com/Org/your-skill.git workspace/skills/your-skill
```

## Usage

1. Step or scenario one.
2. Step or scenario two.
3. When to run which command (point to Commands below).

## Examples

**Example 1: [benefit]**  
*Scenario:* User wants to do X.  
*Action:* Run `your-command --foo`.  
*Outcome:* Brief result that showcases the benefit.

**Example 2: [benefit]**  
(Same pattern.)

## Commands

```bash
python3 <skill-dir>/scripts/script.py command [options]   # What it does
python3 <skill-dir>/scripts/script.py other              # What it does
```

- **command** — Short description.
- **other** — Short description.
```

## Requirements

- Python 3.7+
- Input: valid SKILL.md with YAML frontmatter (at least `name`, `description`).

## Files in this skill

- `SKILL.md` — This file (instructions for the formatter skill).
- `scripts/format_skill_doc.py` — Parser and formatter script.
- `TEMPLATE_CLAWHUB_SKILL.md` — Copy-paste template for ClawHub-optimized SKILL.md.
