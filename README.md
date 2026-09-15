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

Three skills for long-form nonfiction. They divide cleanly: `line-edit` handles how a sentence reads, `cite` handles whether a claim is sourced, `fact-check` handles whether it is true.

**`/writing:cite`** — Chicago Manual of Style (17th ed.) Notes-Bibliography citation management. Audits content files for malformed footnotes, informal inline citations, and uncited claims; reformats footnotes to CMS; keeps a bibliography alphabetized. It never fabricates citation details and never edits without showing the change first.

Assumes a project layout with content files in `content/` and a bibliography at `content/references.md`.

**`/writing:line-edit`** — An opinionated prose style guide. Eleven rules covering intensifying adverbs, hidden verbs, weak verbs, over-emphasis, promotional language, editorializing scaffolding, and uncited attributions of opinion. Includes a copy-paste `grep` that catches the mechanical rules in one pass.

This one is deliberately not neutral. It encodes my taste. Fork it and change the rules rather than arguing with them.

**`/writing:fact-check`** — Verifies factual claims against real sources. Built around one rule: recall proposes, source disposes. Every claim exits as CONFIRMED, CONTRADICTED, or UNRESOLVED, each with a quoted passage and a URL. There is no "probably" — a claim the model merely believes is UNRESOLVED until a source says otherwise.

It exists because the opposite is the default failure mode. Asked to audit citations, a model will helpfully volunteer corrections from memory that read exactly like findings and have not been checked. This skill makes that impossible to do by accident, and `cite` is explicitly barred from doing it at all.

### `gsto`

Workflow tools for working with Claude Code.

**`/gsto:scout`** — Research and present options before any plan or implementation. At the start of a non-trivial task, it goes and finds out how the thing is actually done, then returns 2–4 real options, the concrete tradeoff for each, anything surprising it turned up, the questions it needs answered, and a recommendation with a confidence level. It does not plan or implement until you've picked one.

It interrupts the instinct to start issuing instructions before anyone has checked how the problem is usually solved.

## License

MIT
