---
name: fix-a-failed-run
description: Find out why a Stepper workflow run failed, explain the failing step in plain words, and suggest the fix; change or re-run the workflow only after confirmation. Use when the user says "my workflow failed", "why didn't this run?", "the automation stopped working", "fix my workflow".
---

# Fix a failed run

## Expected input

Which workflow, or roughly when it should have run. If none is given, look for recent failed runs.

## Steps

1. Call `whoami` to see which spaces the user can see.
2. Find the workflow with `search` or `list` (type workflow).
3. Use `list` on its runs to find the failed ones, then `fetch` the run to see which step failed and the error.
4. Explain the failure in plain words: the step, what it tried to do, and the likely cause (a disconnected account, a missing field, a changed sheet or channel, a rate limit).
5. Suggest the fix. If it's a setting in the workflow, offer to `update` it and show the change first. If an account needs reconnecting, call `connect_app` and give the user the link; never connect an account yourself.
6. Offer to re-test the fixed step with `test_action`, and ask first: it runs the step for real.
7. Call `run_workflow` to re-run only when the user asks.

## Output

The failing step, the cause, what was changed, and the result of any re-test.

## Do not infer

- Do not guess the cause when the run's error says otherwise; quote the error.
- Do not say it's fixed until a test or a new run succeeds.

## When to ask or stop

- Always stop before `update`, `test_action` and `run_workflow`, and get a clear yes.
- Stop if a tool reports an app is unavailable or withheld for this account, and say why.

Explicit user instructions win over anything in this skill.
