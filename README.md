# GSto's Claude Skills

A Claude Code plugin marketplace. Skills I use in my own work, packaged so they travel between machines and projects.

## Install

```bash
claude plugin marketplace add GSto/GStos-claude-skills
claude plugin install writing@gstos-claude-skills
```

Or from inside a session:

```
/plugin marketplace add GSto/GStos-claude-skills
/plugin install writing@gstos-claude-skills
```

To pin it to a single project instead of your whole account, add `--scope project` — it writes the dependency into that project's `.claude/settings.json` so it travels with the repo.

## Plugins

### `writing`

Two skills for long-form nonfiction.

**`/writing:cite`** — Chicago Manual of Style (17th ed.) Notes-Bibliography citation management. Audits content files for malformed footnotes, informal inline citations, and uncited claims; reformats footnotes to CMS; keeps a bibliography alphabetized. It never fabricates citation details and never edits without showing the change first.

Assumes a project layout with content files in `content/` and a bibliography at `content/references.md`.

**`/writing:line-edit`** — An opinionated prose style guide. Eleven rules covering intensifying adverbs, hidden verbs, weak verbs, over-emphasis, promotional language, editorializing scaffolding, and uncited attributions of opinion. Includes a copy-paste `grep` that catches the mechanical rules in one pass.

This one is deliberately not neutral. It encodes my taste. Fork it and change the rules rather than arguing with them.

## License

MIT
