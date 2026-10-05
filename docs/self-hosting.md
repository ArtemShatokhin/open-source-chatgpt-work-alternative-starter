# Self-host open source Kortix on your own infrastructure

Kortix is the open-source AI Management System, and you can run the whole platform yourself: on a laptop, a VPS, your VPC or an on-prem network. Self-hosting gives you the agents, skills, memory and connector config in a repo you own, with no dependency on Kortix's cloud.

## What runs where

Kortix runs as one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. Agent sessions run on a separate sandbox provider, not on this stack. The default provider is Daytona; Platinum and E2B are also supported. Connector credentials are brokered server-side and never enter the sandbox machine.

## The one-command path

On a bare Linux box, the one-shot bootstrap script installs Docker, the `kortix` CLI, and the stack in a single command. It runs on Linux only; [Read the docs](https://kortix.com/docs) for the exact invocation. On another OS, install the CLI directly and use the manual path below.

## The manual path

Install the CLI:

```bash
curl -fsSL https://kortix.com/install | bash
```

Point an A/AAAA record for your domain and for `api.<domain>` at the box's IP, then open ports 80 and 443. The bundled Caddy proxy uses them to issue a TLS certificate.

```bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

Run `kortix self-host status`, `kortix self-host logs` and `kortix self-host doctor` while the stack starts.

### Evaluation with no domain

To try Kortix without a domain, use a Cloudflare tunnel:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use this mode for evaluation rather than production.

## Model keys and the sandbox provider

After the stack starts, set your sandbox provider key:

```bash
kortix self-host configure
```

`configure` prompts for the sandbox provider key and, optionally, a managed-git token. Sign in to the dashboard, then connect your own LLM key in the model picker. Self-hosted instances use your own key by default. Kortix is model-agnostic: connect OpenAI, Anthropic, Google or any OpenAI-compatible endpoint, per agent, per session or per message.

## Updates, memory limits and backups

Every instance updates itself automatically. Pin an exact version instead:

```bash
kortix self-host update --tag 0.9.84
```

Turn the updater off with `kortix self-host update --auto-update off`. Each API container has a 640 MiB memory limit by default; on a 16 GiB host, raise it when API traffic reaches the limit:

```bash
kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m
```

Confirm the applied limit with `docker stats --no-stream`. Kortix has no separate backup system. Each instance stores its data as two directories under `~/.config/kortix/self-host/<instance>/`: `volumes/db/data` for Postgres and `volumes/storage` for files. The instance's `.env` file holds every secret and signing key. Back up all three before a destructive command.

## Read more

[Read the docs](https://kortix.com/docs) covers the self-hosting architecture and every `kortix self-host` subcommand. The companion site has a plain-language [self-hosting guide](https://chatgptworkalternative.com/self-hosting.html) that walks the same stack.
