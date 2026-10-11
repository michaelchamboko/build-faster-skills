---
name: code-review
description: >-
  Independently review a GitHub pull request using Codex Code Review before
  owner approval. Validate findings, fix actionable defects, rerun checks,
  and request a fresh review whenever the diff changes.
compatibility: GitHub pull request access plus Codex Code Review via its plugin or enabled GitHub integration. GitHub CLI is optional.
---

# Code review

Codex is the reviewer; the implementing agent makes fixes. Do not install or
require an external review service.

## 1. Establish the current state

- Identify the correct repository, PR, branch, and head SHA. Optional CLI:
  `gh pr view --json number,url,headRefOid`.
- Examine the diff, nearby behavior, existing comments, relevant open PRs,
  and the before/after evidence required by `/before-and-after`.
- Run the repo's documented checks and tests. Keep the actual output; never
  report skipped, missing, or failing checks as passing.

## 2. Request Codex Code Review

Choose a single route:

- Open the **Code Review plugin** in ChatGPT or Codex and select the PR.
- Where the repository has Codex GitHub PR reviews enabled, comment
  `@codex review`. CLI: `gh pr comment <PR_NUMBER> --body "@codex review"`.

Check that review results refer to the **current head commit**. Never assume
the plugin or GitHub integration is connected merely because this skill exists.
Do not repeatedly post duplicate review requests. If review cannot run,
report the blocker; do not imply that missing results mean approval.

## 3. Resolve actionable findings

1. Inspect the referenced code. Reproduce or substantiate likely defects;
   separate defects from preferences and false positives.
2. Return concrete findings to the implementing agent for minimal fixes and
   regression tests where appropriate.
3. Rerun relevant checks, update the PR evidence, and get a new review for
   changed code. Do not rely on a review of an earlier head SHA.
4. Document addressed or disputed comments with reasons and evidence.

After **three unsuccessful fix/review rounds**, stop and identify the
assumption to investigate. Do not chase a numeric score.

## 4. Ready for owner approval

- Required checks pass with actual evidence.
- Codex reviewed the latest diff, with no verified critical or high-severity
  defects left unresolved.
- Remaining nonblocking comments and limitations are documented.
- Owner approval remains separate. Do not merge automatically.

For oversized PRs, split independent changes when practical; there is no
special large-PR reviewer or file-count bypass.

## Report

Provide PR URL, head SHA reviewed, checks run and results, review status,
fixes, unresolved issues, and the next decision.

References:
- [Review pull requests with Codex](https://help.openai.com/en/articles/20001552-review-pull-requests-with-codex)
- [Custom Code Review rules for Codex](https://developers.openai.com/blog/custom-code-review-rules-for-codex)
