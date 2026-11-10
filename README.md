# Stepper MCP: skills for AI assistants

Build and fix workflows from your AI assistant. Describe what should happen when a form is submitted, on a schedule or when an app event fires, and it builds the workflow in Stepper, tests each step against your connected apps, and publishes it once you confirm. When a run fails, it explains the failing step and fixes it with you.

This repo connects your assistant to Stepper's MCP server and adds skills that show it how to do each job well.

## Install

**Skills (Claude Code, Cursor, Codex and other agents)**

```
npx skills add paperform-co/stepper-mcp
```

**MCP server:** add `https://api.paperform.app/mcp/stepper` as a remote MCP server in your client (a custom connector in ChatGPT or Claude, or `mcp.json` in Cursor). You sign in with your Stepper account the first time you use it.

It's also listed in the official MCP registry as `io.stepper/stepper`.

Want an agent to act in your apps with only the actions you allow? That's a Stepper Skill Set, served at `https://mcp.stepper.io/skill-sets/mcp`. See https://stepper.io/skill-sets/.

## Skills

| Skill | Use it to |
| --- | --- |
| `build-a-workflow` | Build, test and publish a workflow |
| `fix-a-failed-run` | Find why a run failed and fix the failing step |

Try:

- "When someone submits my contact form, add them to HubSpot and post in #sales."
- "My invoice workflow failed last night. What went wrong?"

## How it works

The repo contains skills (Markdown instructions) and one remote MCP server, `https://api.paperform.app/mcp/stepper`. It runs no code on your computer.

When you connect, you sign in through Paperform's own sign-in page and choose what your assistant may do. It then works only in the account and spaces you approved. The tools check with you before anything is published, run or changed.

Stepper is made by Paperform. If your account also has Paperform or Papersign, the same connection can use those too.

## Links

- About Stepper and MCP: https://stepper.io/mcp/
- Privacy policy: https://paperform.com/privacy/
- Terms: https://paperform.com/terms/

## Licence

MIT. See [LICENSE](LICENSE).
