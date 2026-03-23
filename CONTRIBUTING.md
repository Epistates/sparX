# Contributing to sparX

Thanks for your interest in improving sparX. Here's how to contribute.

## Adding a New Skill

1. Fork the repo
2. Create your skill directory: `.claude/skills/your-skill/`
3. Add a `SKILL.md` with proper frontmatter:

```yaml
---
name: your-skill
description: What it does and when to use it. Claude matches this against user messages.
argument-hint: "[expected arguments]"
---

# Your Skill Name

Instructions for Claude to follow when the skill is invoked.
```

4. Add supporting files if needed (templates, patterns, examples)
5. Test it locally by opening Claude Code in the sparX directory
6. Submit a PR

### Skill Quality Checklist

- [ ] `description` field uses natural language the user would actually say
- [ ] Instructions reference Phoenix scoring weights where relevant
- [ ] Character limits (280) are enforced if the skill produces post content
- [ ] Output includes a Phoenix Score block if the skill produces or evaluates content
- [ ] Supporting files use progressive disclosure (main SKILL.md is concise, details in separate files)
- [ ] No hardcoded paths — use relative paths from the skill directory

## Improving Existing Skills

- Fix a bug or edge case → PR with the change and a description of what went wrong
- Improve instructions → PR explaining why the new instructions produce better output
- Add supporting files (templates, examples) → PR with examples that demonstrate quality

## Updating Reference Docs

The `reference/` directory contains the algorithm knowledge base. If you have updated data on:
- Phoenix scoring weights
- Engagement timing data
- New penalty signals
- Content format performance

Submit a PR with your source. Include concrete examples where possible.

## Reporting Issues

Use the [issue templates](https://github.com/epistates/sparX/issues/new/choose):
- **Bug Report** — a skill isn't working as expected
- **Feature Request** — suggest a new skill or improvement

## Code of Conduct

Be helpful, be respectful. We're all trying to make better content.
