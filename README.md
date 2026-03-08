# Skill Doc Formatter

Formats SKILL.md files for optimal display on ClawHub. Produces a consistent structure: Description, Installation, Usage, Examples, and Commands.

## Quick Start

```bash
# Format a SKILL.md (output to stdout)
python3 scripts/format_skill_doc.py /path/to/skill/SKILL.md

# Format in-place
python3 scripts/format_skill_doc.py /path/to/skill/SKILL.md --inplace

# Generate examples if missing
python3 scripts/format_skill_doc.py /path/to/skill/SKILL.md --generate-examples

# Run security review on a skill
python3 scripts/security_review.py /path/to/skill/
```

## Features

- Parses YAML frontmatter and markdown body
- Maps variant section titles to canonical ClawHub names
- Merges duplicate sections and normalizes order
- Auto-generates benefit-focused examples from description
- Includes a security review checker for ClawHub compliance

## Security Review

The bundled `security_review.py` checks for:

- Missing requirements declarations
- Secrets being logged to files
- Missing referenced files
- Undocumented environment variables
- Persistent behavior without `always: true`
- Log file permission issues

## Requirements

- Python 3.7+
- PyYAML (optional, for full frontmatter parsing)

## License

OpenClaw Skill - See main OpenClaw repository for license information.
