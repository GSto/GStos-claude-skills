---
name: line-edit
description: An opinionated prose style guide (banned intensifiers, weak verbs, AI-tell phrases, no em dashes). Load before drafting or editing any prose that ships under the author's name — book chapters, newsletter posts, landing copy, long-form email.
user-invocable: true
argument-hint: [scan|edit] [file-or-topic]
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Line Edit

A house style, not a neutral linter. These rules were written for long-form nonfiction and govern any prose the author publishes under their own byline: book chapters, newsletter posts, marketing copy. They do not govern code, commit messages, or your own replies in conversation.

The rules are deliberately opinionated. Fork this skill and change them rather than arguing with them.

Two modes:

- **Draft mode** (default when writing new prose): apply the rules silently as you write. No report.
- **Scan mode** (`/line-edit scan <file>`): report violations with line numbers and suggested rewrites. Do not edit.
- **Edit mode** (`/line-edit edit <file>`): scan, show the diff, get a go-ahead, then edit.

Never edit a file in scan mode. Never edit quoted material in any mode.

## The rules

### 1. Cut adverbs that intensify rather than modify

`just`, `that`, `basically`, `entirely`, `extremely`, `completely`, `exactly`, `very`, `really`, `literally`, `actually`, `certainly`, `probably`

Delete first, rewrite only if the sentence breaks. `that` is often load-bearing; check before cutting.

### 2. Cut prepositional phrases that repeat the obvious

`in the story`, `in the article`, `in the movie`, `in the city`

### 3. Cut phrases that grow on verbs

`seems to`, `tends to`, `should have to`, `tries to`

"It tends to slow you down" becomes "It slows you down."

### 4. Replace abstract nouns that hide active verbs

`considerations` becomes `considers`. `judgement` becomes `judges`. `observation` becomes `observes`.

Watch for the `-tion`, `-ment`, `-ance`, `-ity` endings.

### 5. No em dashes

Use a comma, a colon, a period, or parentheses. This one is absolute.

### 6. Never edit quotes

Quoted material stays exactly as sourced, typos and all. If a quote violates every other rule, it still stands. Flag it in a scan report only to confirm it is a quote, never to suggest a fix.

### 7. Flag weak low-power verbs

`achieve`, `advance`, `alter`, `award`, `commit`, `deliver`, `enhance`, `fail`, `harness`, `improve`, `produce`, `provide`, `recognize`, `reimagine`, `serve`, `succeed`, `support`, `utilize`, `work`

These are advisory, not banned. Point them out and offer a more specific verb. Do not swap them automatically in edit mode without showing the swap.

### 8. Cut over-emphasizing phrases

`stands as`, `serves as`, `is a testament`, `plays a vital/significant/crucial role`, `underscores its importance`, `leaves a lasting impact`, `watershed moment`, `key turning point`, `deeply rooted`, `steadfast`, `solidifies`

### 9. Cut promotional language

`rich/vibrant cultural heritage/tapestry`, `breathtaking`, `must-visit`, `must-see`, `stunning natural beauty`, `enduring legacy`, `lasting legacy`, `nestled`, `in the heart of`

### 10. Cut editorializing scaffolding

`It's important to note`, `it's important to remember`, `it's important to consider`, `it is worth`, `no discussion would be complete without`, `this article wouldn't exist without`

Delete the frame and keep the claim. "It's important to note that bugs compound" becomes "Bugs compound."

### 11. Remove uncited attributions of opinion

`Industry reports`, `Observers have noted`, `Some people say`, `Some critics argue`, `studies show`, `research suggests`, `experts say`

Either name the source with a real citation (use the `cite` skill) or cut the claim. Do not invent a source. If you suspect the claim is not merely unsourced but wrong, that is a `fact-check` job, not a line edit.

## Mechanical pass

Run this first in scan mode. It catches rules 1, 3, 5, and 8 through 11 by pattern. Rules 2, 4, 6, and 7 need judgment and a read.

```bash
grep -nEi "\b(just|basically|entirely|extremely|completely|exactly|very|really|literally|actually|certainly|probably)\b|\b(seems|tends|tries) to\b|—|\b(stands as|serves as|is a testament|plays a (vital|significant|crucial) role|underscores its importance|leaves a lasting impact|watershed moment|key turning point|deeply rooted|steadfast|solidifies)\b|\b(breathtaking|must-visit|must-see|nestled|in the heart of|vibrant tapestry|(enduring|lasting) legacy)\b|it'?s important to (note|remember|consider)|no discussion would be complete|\b(industry reports|observers have noted|some (people say|critics argue)|studies show|research suggests|experts say)\b" "<file>"
```

The hit count is not the score. Skim every hit for context before acting: an intensifier inside a quote stays, and `just` sometimes means "fair."

## Scan output format

```
## <filename>

### Mechanical (rules 1, 3, 5, 8-11)
- L12  "actually"          delete
- L31  "—"                 replace with comma
- L44  "tends to slow"     "slows"

### Judgment (rules 2, 4, 7)
- L18  "provide value"     weak verb, consider "pay off" or name the value
- L52  "considerations"    hidden verb, consider "considers"

### Untouched (rule 6)
- L3   Swizec quote, left as sourced
```

Rank by line number, not severity. Cap the report at the file. Do not sprawl into adjacent files unless asked.

## Behavioral rules

1. **Voice over compliance.** The author's rhythm wins over a rule when the two fight. A sentence stripped of everything is not better prose. Rule 5 is the only absolute.
2. **Show before you edit.** In edit mode, present the before/after and wait for the go-ahead. Batch the whole file into one approval, not one prompt per line.
3. **Do not rewrite for style beyond these rules.** No reordering paragraphs, no adding transitions, no tone changes. This is a line edit, not a rewrite.
4. **Do not fabricate to satisfy rule 11.** Cutting an uncited claim is correct. Inventing a citation is not.
5. **Respect the project's drafting convention.** If the project's CLAUDE.md says new drafts go to the console rather than straight into files, follow that unless told otherwise.
