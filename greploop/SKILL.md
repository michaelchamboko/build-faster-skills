---
name: greploop
description: >-
  Legacy compatibility alias. For pull request reviews use the single
  code-review skill, which uses Codex Code Review instead of an external
  reviewer. This alias exists only for older skill references.
---

# Review compatibility alias

This skill previously implemented the original PR review loop. It no longer runs
a separate review service or its scoring and retry loop.

**Use [`/code-review`](../code-review/SKILL.md) for every GitHub pull request.**

- Check that tests and before/after evidence are available.
- Ask Codex Code Review to review the current pull-request diff.
- Have the implementing agent fix verified issues, rerun checks, and request
  another review if the head commit changes.
- Stop after three unsuccessful review/fix rounds and report the blocker.
- Report the reviewed head SHA and any unresolved findings; require owner
  approval before merging.

Large changes use the same review process. Split oversized pull requests
when practical instead of using a vendor-specific bypass.
