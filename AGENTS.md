<!-- BEGIN contech-context -->
## Contech Context SMFS Retrieval

Use SMFS when a task needs grounded evidence from private construction or
engineering corpora. Codex owns decomposition and final synthesis; SMFS
mounts the corpus as a local filesystem with semantic search.

### Required SMFS Protocol

1. Mount the default corpus container for the task:

   ```bash
   contech-context smfs-mount --repo .
   ```

   Fresh installs allow/default the `structural-engineering-corpora`
   container tag. This is a prototype corpus currently centered on notes
   related to concrete design to Eurocode 2 (EC2). Use
   `contech-context use <container-tag> --repo .` to switch containers.
   Long container tags on macOS may need a short SMFS home such as `/tmp/h`;
   record it with `contech-context containers smfs-home /tmp/h --repo .`
   or pass `--smfs-home /tmp/h --save-smfs-home` when mounting. Prefer
   persisting in the lock so agents read `smfs.smfs_home`; one-shot env or
   flag overrides require the same `HOME` on later native `smfs` commands.

2. Read `<mount>/profile.md` once for the corpus overview, where
   `<mount>` is `smfs.mount_path` from `contech-context.lock`
   (`./memory/mount` by default). If `smfs.smfs_home` is set in the lock
   or `CONTECH_CONTEXT_SMFS_HOME` was used for mounting, run `smfs` list,
   status, logs, unmount, and grep commands with that value as `HOME`.
3. For the first search inside a mounted SMFS path, change into the mount
   and use native semantic grep:

   ```bash
   cd <mount> && HOME=<smfs_home> smfs grep "Focused construction or engineering question"
   ```

   Omit the `HOME=<smfs_home>` prefix only when no SMFS home override is
   configured.

4. Do not run `smfs grep` from the repo root, do not pass the mount as a
   path argument, and do not use a contech-context grep wrapper.
5. Treat retrieval budgets as hard stops. For direct lookup and yes/no
   trap questions, run at most two focused semantic greps and at most
   three shell commands total. For cross-chapter synthesis, run 3-6
   focused semantic greps and at most three shell commands total; batch
   several bounded `smfs grep` pipelines in one shell command when that
   keeps the workflow compact. For each relevant chapter, copy the most
   specific exact heading title from the profile or digest into a grep
   query, then add the question's key symbols or terms. When a question
   compares concepts or says something is useful "again", cite one baseline
   paragraph for the original concept and one paragraph for the new
   combined-case concept. When batching,
   change into the mount once:
   `cd <mount> && { HOME=<smfs_home> smfs grep "<query1>" | sed -n "1,80p"; HOME=<smfs_home> smfs grep "<query2>" | sed -n "1,80p"; }`.
   If cross-chapter greps return relevant text but no visible paragraph
   refs for a required concept, use the final command for one scoped
   literal fallback on exact visible wording:
   `cd <mount> && rg -n "<exact visible phrase|symbol>" . | sed -n "1,40p"`.
   Once the budget is spent, stop searching and answer only from visible
   paragraph-backed evidence, or abstain. Avoid `pwd`, `ls`, repeated
   broad searches, broad `rg`, guessed source paths, and command loops.
6. Do not use `rg`, `grep`, `find`, or built-in search inside the SMFS
   mount before `smfs grep`. This is important: semantic grep is the
   retrieval surface.
7. After `smfs grep` returns candidate files or excerpts, inspect only
   those returned files and nearby lines literally with shell tools such
   as `sed`, `awk`, or `cat`.
   If the first semantic grep returns only `(unknown)` snippets with no
   visible paragraph refs for an answerable question, do not guess source
   paths from profile or digest filenames. Use the final command to combine
   one exact follow-up native `smfs grep` with one scoped literal fallback
   from inside the mount for exact visible text:
   `cd <mount> && { HOME=<smfs_home> smfs grep "<exact visible phrase|symbol>" | sed -n "1,80p"; rg -n "<exact visible phrase|symbol>" . | sed -n "1,40p"; }`.
   Then cite visible paragraph refs or real returned path/line evidence
   from the mount, or abstain. `(unknown)` chunks with visible refs such as
   `[p106]` are citable paragraph-backed evidence; `(unknown)` chunks
   without visible refs are routing hints only.
   For unsupported or corpus-scope questions, read `profile.md`, run one
   focused semantic grep, and default to abstention unless that one grep
   returns direct paragraph-backed support for the exact requested topic.
   Do not run synonym searches, second greps, `rg`, `find`, or broad
   source inspection just to prove absence.
9. `/profile.md` and returned source files are valid evidence when they
   are inside the mounted corpus. Label the source type when citing
   evidence.
10. Cite only visible paragraph refs copied from SMFS output or literal
    file inspection. Treat `(unknown)` snippets and unanchored
    generated-memory snippets without visible refs as routing hints, not
    final citable evidence.
    If needed for an answerable question, run one exact focused follow-up
    `smfs grep` to obtain paragraph-backed evidence.
    When a chunk contains a heading ref and later sentence/formula refs,
    cite the ref immediately attached to the sentence or formula you use,
    not the section heading ref.
    When paragraph-backed hits cover multiple requested subparts, answer
    each covered subpart and abstain only for unsupported remainders.
    Preserve operative evidence wording such as "may be neglected",
    "satisfy equilibrium", "serviceability", "direct load paths", and
    formula symbols.
    Before declaring a subpart unsupported, scan the visible `smfs grep`
    output for all paragraph-backed hits, not just the first hit.
11. Preserve exact engineering notation from evidence, including
    subscripts and LaTeX-style symbols such as `V_{Rd,c}`, `M_{tmax}`,
    `b_e`, `f_{ck}`, `\gamma_c`, and `d`.
    Use standard EC2 notation `V_{Rd,c}` for shear resistance of members
    without shear reinforcement, even if retrieved text has OCR/case
    variants such as `v_{Rd,C}`.
    Format formulas with readable multiplication spacing, for example
    `0.17 b_e f_{ck} d^2` instead of compressed
    `0.17b_ef_{ck}d^2`.
12. If the question names a symbol, repeat that exact symbol in the
    corrected answer. For coefficient traps, state the corrected
    expression with the named symbol, not only the numeric coefficient.
13. When an answer uses a formula, define the non-obvious symbols if the
    corpus gives those definitions. For geometry variables such as `b_e`,
    include the effective-width context, for example edge or corner
    column geometry when the evidence distinguishes them. If the corpus
    defines multiple cases for a symbol, include the relevant cases. For
    flat-slab `b_e`, look for and report both edge and corner
    effective-width cases when present. Include the corner-column case as
    well as the edge-column case when the evidence distinguishes both.
14. For yes/no trap questions, start with an explicit `Yes` or `No`,
    give the corrected value or location, and add one disambiguating
    detail when the question names a false alternative.
15. If the mounted corpus does not support the answer, abstain or ask a
   narrower in-corpus question. Do not fill corpus gaps from memory, and
   do not answer unsupported questions without a `References:` section
   containing copied paragraph-backed quotes.

### Installed Cursor guidance

- `.cursor/rules/contech-context-retrieval.mdc`
- `.cursor/rules/contech-context-citations.mdc`
- `.cursor/rules/contech-context-routing.mdc`
- `.cursor/skills/planning-contech-context-queries/SKILL.md`
- `.cursor/skills/using-contech-context/SKILL.md`
- `.cursor/skills/troubleshooting-contech-context/SKILL.md`

The root `contech-context.lock` keeps the repo-owned SMFS allowlist. It
must not contain API keys or private corpus dumps.

Keep API keys, raw auth headers, `.env.local`, and private corpus dumps
out of committed files.
<!-- END contech-context -->
