---
name: planning-contech-context-queries
description: Plan focused SMFS corpus lookups for private construction and engineering evidence.
---

# Planning Contech Context Queries

<!-- BEGIN contech-context -->

Use when a task needs evidence from a mounted private corpus.

1. Break the task into focused evidence questions. Codex owns decomposition,
   retrieval sequencing, and final synthesis; SMFS only returns mounted corpus
   evidence.
2. Read `<mount>/profile.md`.
3. Run one focused `smfs grep` before any literal search. Treat budgets
   as hard stops: direct lookup and yes/no trap questions get at most two
   semantic greps and three shell commands total; cross-chapter synthesis
   gets 3-6 focused semantic greps and at most three shell commands total.
   Unsupported or corpus-scope probes get one focused semantic grep and
   default to abstention unless direct paragraph-backed support is visible.
   Batch bounded `smfs grep` pipelines in one shell command when useful.
   For each relevant chapter, copy the most specific exact heading title
   from the profile or digest into a grep query, then add key symbols or
   terms. When a question compares concepts or says something is useful
   "again", cite one baseline paragraph for the original concept and one
   paragraph for the new combined-case concept. When batching, pass `<mount>`
   to each native grep.
4. Inspect only returned files and nearby lines literally.
5. Preserve exact engineering symbols from evidence in the answer and
   repeat symbols named in the question. Define non-obvious formula
   symbols when the corpus gives definitions.
6. Abstain when the mounted corpus does not support the answer.
<!-- END contech-context -->
