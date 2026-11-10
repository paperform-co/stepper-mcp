---
name: build-a-workflow
description: Build a Stepper workflow that acts on a trigger (a new form submission, a schedule, a webhook or an app event), test its steps, and publish it after confirmation. Use when the user says "when someone submits…", "automate…", "every time X happens do Y", "send this to my CRM/sheet/Slack".
---

# Build a workflow

## Expected input

What should start the workflow, what should happen after it, and which apps are involved.

## Steps

1. Call `whoami` to see which spaces the user can write to.
2. Call `get_help` with the workflow topic before drafting. Do not guess syntax.
3. If the trigger is a form, find it with `search` or `list`.
4. For each app the workflow needs, look for a usable account with `list` (type connection). If there isn't one, call `connect_app` and give the user the link it returns; never connect an account yourself. If the user connected one that this space can't use yet, offer `share_connection`.
5. Call `create` with the drafted workflow. It loads a sample for the trigger so steps can use real field names; if it reports no sample was stored, call `load_trigger_samples` with the workflow's id and the trigger's node id, so the sample is saved on the draft. Use `resolve_parameters` and `list_parameter_options` to fill app-specific values such as which sheet or which channel; ask when there are several.
6. Offer to test each app step with `test_action`, and ask before each one: it runs the step for real (a row is written, a message is sent) and spends credits. Show the user what it wrote.
7. Summarise the trigger and each step in plain words. Offer to publish, and call `publish` only after an explicit yes.
8. To run a published workflow on demand, call `run_workflow` only when the user asks. If a run failed, use `list` and `fetch` on its runs and explain the failing step and what to change.

## Output

The trigger, each step in plain words, which accounts it uses, the test results, and whether it is published.

## Do not infer

- Do not invent field mappings, recipients, channel names or spreadsheet columns. Ask, or read them with `list_parameter_options`.
- Do not say a step works until `test_action` has run it.
- Do not use an account the user hasn't connected or shared with this space.

## When to ask or stop

- Always stop before `publish`, `run_workflow` and each `test_action`, and get a clear yes.
- Stop if a tool reports an app is unavailable or withheld for this account, and say why.

Explicit user instructions win over anything in this skill.
