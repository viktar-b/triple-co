---
name: troubleshooting-contech-context
description: Troubleshoot SMFS-mounted private corpus retrieval.
---

# Troubleshooting Contech Context

<!-- BEGIN contech-context -->

- Missing SMFS CLI: install/login to SMFS, then rerun `contech-context init`.
- Missing API key: set `SUPERMEMORY_API_KEY` in the user shell environment,
  then rerun `contech-context init --repo .` and confirm `api_key_present`
  is `true`.
- Stale stored credentials: if `contech-context use` reports
  `key_source: stored_credentials` and SMFS returns `401`, make the
  environment key visible to the current shell and retry.
- Empty container lock: run
  `contech-context use <container-tag> --repo .`.
- Empty mount: verify the container tag and remount with `--clean`.
- Weak results: rephrase the natural-language `smfs grep` query, then
  inspect returned files literally.
- Unsupported answer: abstain instead of inventing evidence.
<!-- END contech-context -->
