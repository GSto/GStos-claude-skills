---
name: scout
description: Research and present options before any plan or implementation. Use at the start of any non-trivial task — a design decision, a new feature, a tool choice, a piece of writing — especially when the instinct is to start issuing instructions.
---

Before proposing anything, go find out how this is actually done.

Look in this repo first — existing patterns, prior art, anything in the repo's specs, docs, or resource directories that already covers adjacent ground. Then look outward if it's warranted: docs, the source of the libraries involved, how comparable projects handle it.

Come back with:

- **2–4 real options**, each one something a reasonable person would actually pick. Not one real option and two strawmen.
- **The tradeoff for each** — what it costs, what it forecloses, what it's betting on. Be concrete: name the failure mode, not "may be less flexible."
- **What you found that surprised you**, if anything. Constraints the user probably doesn't know about. Prior art they've forgotten they wrote.
- **The questions you need answered.** Ask them one at a time if there are more than two — don't batch them into a wall that gets skimmed.
- **Your recommendation, and how confident you are.** If the evidence genuinely points one way, say so plainly rather than performing neutrality.

Do not write a plan yet. Do not start implementing. Do not create files.

If the research turns up that the user is asking the wrong question, say that instead of answering the question as asked.

Once the options are laid out and the user has picked one, then plan.
