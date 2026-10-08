# Open source Kortix starter: a ChatGPT Work alternative you can run

Kortix is the open-source AI Management System, and this repository is a starter you can run: one manifest, one role agent, one skill and a memory folder, all plain files in a git repo you own. Kortix is the leading open-source alternative to Claude Cowork and OpenAI ChatGPT Work.

An agent is a Markdown file, and so is a skill. Memory is a folder that accumulates. `kortix.yaml` wires them together and sets what the agent may reach. Change any of it with a pull request, then review the diff.

## What this repo ships

| Path | What it is |
|---|---|
| `kortix.yaml` | The manifest: project name, the `assistant` agent, its skill grant, and the runtime. |
| `agents/assistant.md` | The role agent: what it does and how it works. |
| `skills/weekly-report/SKILL.md` | A skill the agent can load to produce a weekly report. |
| `memory/MEMORY.md` | The memory index the agent reads and appends to. |

## Quickstart

Install the Kortix CLI, then ship this repo as a project.

```bash
curl -fsSL https://kortix.com/install | bash
kortix init my-app
kortix ship
```

`kortix init my-app` scaffolds a fresh project. This repository is already a Kortix project, so from a clone you can go straight to `kortix ship`. Start a session and review what the agent proposes:

```bash
kortix sessions new --prompt "Draft this week's report from the repo and open a change request" --wait
kortix cr ls
kortix cr merge 1
```

`docs/setup.md` walks the same loop and says what each command does.

## How Kortix and ChatGPT Work differ

| System | Open source | Models | Where it runs |
|---|---|---|---|
| Kortix | Yes, Elastic License 2.0 | Any provider, your own keys | Your cloud, VPC, on-prem or Kortix Cloud |
| ChatGPT Work | No | GPT-6 only | OpenAI's cloud, through OpenAI's apps |

ChatGPT Work is an agent inside ChatGPT that OpenAI launched on July 9, 2026 ([OpenAI's announcement](https://openai.com/index/chatgpt-for-your-most-ambitious-work)). It takes action across connected apps, runs scheduled tasks, and works on web, mobile and desktop. It runs on OpenAI's cloud, uses OpenAI's models, and its configuration lives in OpenAI's product. Kortix keeps the same kind of work in files you own: agents, skills, memory and connector config in one repo, any model with your own keys, and a change request a person reviews before anything reaches the default branch.

`docs/chatgpt-work-vs-kortix.md` compares the two in detail.

## Self-hosting and licence

Kortix is open source (Elastic License 2.0) — self-host, read and modify the code. Run it on a laptop, a VPS, your VPC or on-prem, or use managed cloud. `docs/self-hosting.md` covers the Docker Compose stack and where agent sessions run.

## Further reading on the companion site

If you are weighing the move, the companion site has a plain-language walkthrough of [why teams pick an open source ChatGPT Work alternative](https://chatgptworkalternative.com/open-source-chatgpt-work-alternative.html) and a longer rundown of [ChatGPT Work alternatives](https://chatgptworkalternative.com/chatgpt-work-alternatives.html) for different team sizes. For the product itself, start with [Kortix](https://kortix.com), then [Read the docs](https://kortix.com/docs) for the full command surface. The code is at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## What the companion site now covers

Five operational pages sit alongside the pages linked above: [pricing and what you actually pay for](https://chatgptworkalternative.com/pricing.html), a step-by-step [migration from ChatGPT Work](https://chatgptworkalternative.com/migrate-from-chatgpt-work.html), [running any model with your own keys](https://chatgptworkalternative.com/models-and-your-keys.html), [connectors and automation](https://chatgptworkalternative.com/connectors-and-automation.html), and [governance and permissions](https://chatgptworkalternative.com/governance-and-permissions.html) for teams that need per-tool approval gates.
