# Run the open source Kortix starter: setup

Kortix is the open-source AI Management System. The steps below install the CLI, create or link a project, push the manifest, start a session, and review the change request the agent opens.

## Prerequisites

- A Kortix account on [Kortix](https://kortix.com), or a self-hosted instance. `self-hosting.md` covers the self-hosted path.
- The `kortix` CLI. It ships as a prebuilt binary for macOS and Linux; Windows is not supported.
- A model key for the provider you want to use, or the ChatGPT plan you already pay for.

## 1. Install the CLI

```bash
curl -fsSL https://kortix.com/install | bash
```

The installer downloads a prebuilt binary for macOS and Linux. Update it later with `kortix update`.

## 2. Create or link a project

Scaffold a new project:

```bash
kortix init my-app
cd my-app
```

`kortix init` creates a project directory with the general-purpose starter. Its `kortix.yaml` declares `kortix_version: 2` and runs the OpenCode harness. This repository is already a project of that shape, so from a clone you can skip this step and run `kortix ship` directly. To link an existing clone to a project you already created:

```bash
kortix projects link <project-id>
```

## 3. Ship the manifest

```bash
kortix ship
```

`kortix ship` lints your `kortix.yaml`, commits local changes, pushes your branch, and prompts for any missing secret or connection. Run it each time you want your local changes on the cloud project. The first run creates the cloud project and repo if you have not linked one yet.

## 4. Start a session

```bash
kortix sessions new --prompt "Draft this week's report from the repo and open a change request" --wait
```

Each session runs in its own sandbox, on its own branch. `--wait` blocks until the session is ready. The agent works inside an isolated Linux machine with your repo and tools already on it.

To attach a terminal to a running session:

```bash
kortix connect
```

## 5. Review the change request

When a session has commits ready, the agent opens a change request. Nothing reaches the default branch without a review.

```bash
kortix cr ls
kortix cr diff 1
kortix cr merge 1
```

`kortix cr ls` lists change requests for the linked project. `kortix cr diff <cr>` shows the unified patch. `kortix cr merge <cr>` merges it into the default branch.

## Where to go next

`self-hosting.md` covers running open source Kortix on your own infrastructure. `chatgpt-work-vs-kortix.md` explains how this setup compares with OpenAI's ChatGPT Work. [Read the docs](https://kortix.com/docs) for the full command surface.
