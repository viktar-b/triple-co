---
name: using-contech-context
description: Use a mounted SMFS corpus as grounded evidence for Codex work.
---

# Using Contech Context

<!-- BEGIN contech-context -->

Default command flow:

```bash
contech-context init
contech-context guide --format json
contech-context smfs-mount --repo .
cat ./memory/mount/profile.md
cd ./memory/mount && smfs grep "Focused question"
```

After semantic grep returns candidates, inspect returned files only when
SMFS returns real paths; do not construct paths from digest filenames.
Avoid `pwd`, `ls`, repeated broad searches, and broad `rg`; read
`profile.md` and run within the hard retrieval budget. If the first
semantic grep returns only `(unknown)` snippets with no visible paragraph
refs for an answerable question, run one exact follow-up native `smfs grep`
with distinctive symbols, headings, or formula text plus one scoped literal
fallback in the same final command. Cite returned paragraph refs or real
returned path/line evidence, or abstain if none is visible. For cross-chapter
synthesis, use one scoped literal fallback only when relevant SMFS text lacks
paragraph refs for a required concept, and only on exact visible wording. For unsupported or
corpus-scope questions, read `profile.md`, run one focused semantic grep,
and default to abstention unless direct paragraph-backed support is
visible for the exact requested topic; do not run synonym searches,
second greps, `rg`, `find`, or broad source inspection just to prove
absence. Preserve exact engineering notation such as
`V_{Rd,c}`, `M_{tmax}`, `b_e`, `f_{ck}`,
`\gamma_c`, and `d`; use standard EC2 `V_{Rd,c}` for shear resistance of
members without shear reinforcement even if retrieved text has OCR/case
variants such as `v_{Rd,C}`. Format formulas with readable multiplication
spacing, for example `0.17 b_e f_{ck} d^2` instead of compressed
`0.17b_ef_{ck}d^2`. Define non-obvious formula symbols when evidence gives
definitions, especially geometry variables such as `b_e`. Cite only visible
paragraph refs; generated or `(unknown)` snippets without refs are routing
hints, not final evidence. If the question names a symbol, repeat that exact
symbol in the corrected answer. When paragraph-backed hits cover multiple
requested subparts, answer each covered subpart and abstain only for unsupported
remainders; preserve operative evidence wording such as "may be neglected",
"satisfy equilibrium", "serviceability", and "direct load paths". Before declaring
a subpart unsupported, scan the visible `smfs grep` output for all paragraph-backed
hits, not just the first hit. For flat-slab `b_e`, report both edge and
corner effective-width cases when evidence distinguishes both.
<!-- END contech-context -->
