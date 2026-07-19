# Contributing to KayaEOS

Thank you for your interest in KayaEOS! 🚀

## Ways to Contribute

### Proposing a New Playbook

1. Review the existing playbooks first
2. Use the `playbooks/_template.md` template
3. Mark `status: proposed` in the YAML frontmatter
4. Open a PR

### Improving an Existing Playbook

1. Open an issue (bug or enhancement)
2. Make the change
3. Update the playbook version number (`version` field in frontmatter)
4. Open a PR

### Adding a New Agent to the Catalog

1. Use the `agents/_template.md` template
2. Ensure no overlap with existing agents
3. Open a PR

## Playbook Writing Guidelines

- Every playbook must start with YAML frontmatter delimited by `---`
- Required fields: `id`, `title`, `version`, `status`, `agent`
- Each section must begin with a `##` heading
- Steps must be written as ordered lists (`1.`)
- Use imperative mood for AI comprehension ("Do X", "Verify Y", "Commit Z")

## AI Adapter Layer

Adapter files (`adapters/`) are auto-generated from canonical sources.
Do not edit them manually; update the canonical source and regenerate the adapter instead.

## Commit Messages

Use Conventional Commits:

```
feat: add new ui-design playbook
fix: correct step ordering in code-review playbook
docs: update ADR template
```

## Versioning Policy

- **MAJOR**: Breaking changes in the Engineering Constitution
- **MINOR**: New playbook, new agent, new section
- **PATCH**: Content corrections and clarifications

## Questions?

Feel free to open an issue. All questions and suggestions are welcome.
