---
name: apec-delegate
description: Global workflow for offloading useful subtasks across research, analysis, writing, file work, and coding to Antigravity Gemini Flash, with GPT-6 Luna fallback, so the primary Codex model can coordinate and review.
---

# Apec Delegate

For every request, look for bounded work that Gemini can complete and that reduces primary-model effort or context. Keep the primary model on requirements, task boundaries, review, and integration. Handle tiny or indivisible tasks directly when delegation overhead would outweigh the benefit.

## Invoke Gemini

From the relevant project or working directory, first confirm the exact model is listed by `agy models`, then run:

```sh
agy --model <exact-listed-model> --effort <low|medium|high> --print "<task, context, constraints, and expected result>" --output-format json
```

Use only when `agy` is installed and that model appears in `agy models`. Choose the lowest effort that fits: `low` for clear routine work, `medium` for multi-step tasks, `high` for complex or high-impact reasoning. Do not add permission-bypass flags. Parse the JSON result and report the selected model, status, error if any, and usage fields when present. A nonzero exit, `status: "ERROR"`, or empty response is a failed delegation; never describe it as completed work. If usage is present, report it as the CLI's recorded usage, not as proof of billing or a change in an account dashboard.

If the first call fails with a clearly transient service or connection error, retry once. For quota/rate-limit or authentication errors, do not retry. If a retry fails, stop and report the actual error and usage returned; do not silently switch models or accounts.

## Delegate and review

Give the worker only necessary context, relevant files or inputs, constraints, and acceptance criteria. Ask for a concise result, evidence, and changed-file list. Keep independent tasks separate and avoid overlapping ownership. Review outputs and diffs before use or integration. Respect existing authorization for external actions.

For coding work, also require the simplest sufficient change, no speculative scope or unrelated refactors, preserved local style, and task-appropriate verification. Do not assume the worker can read local skills.

If Gemini explicitly reports quota exhaustion or `agy` is unavailable, do the work directly when feasible and state that Gemini was not used. Use `GPT-6 Luna` through a supported Codex agent only when an alternate worker is appropriate to the request; disclose the model switch. Do not infer exhaustion from unrelated errors. Retry only safe transient failures, at most once. If no worker is available, do the task directly and state delegation was unavailable when relevant.
