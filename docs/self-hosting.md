# Self-hosting Kortix, the open-source ChatGPT Work alternative

Kortix is open source and self-host is free, so a company can run the whole thing on hardware it controls. This guide uses the real commands from the Kortix docs, checked October 2026, at [Read the docs](https://kortix.com/docs).

Kortix runs as one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. The stack has no Redis and no separate worker. Agent sessions run on a separate sandbox provider, not on this stack. Platinum is the default provider, and Daytona remains available as a legacy fallback.

## Requirements

- A Linux box for the one-shot script, or any OS for the manual path.
- A domain with an A or AAAA record for the domain and for `api.<domain>`, both pointing at the box, and ports 80 and 443 open.
- The bundled Caddy proxy uses those ports to issue a TLS certificate.
- A sandbox provider key, set after the stack starts.

## One-shot bootstrap

On a bare Linux box, the self-hosting documentation ships a one-shot bootstrap script that installs Docker, installs the `kortix` CLI, and starts the stack in a single command. It runs on Linux only. On another OS, use the manual path.

## Manual path

Install the CLI, point DNS at the box, open ports 80 and 443, then initialize and start.

```bash
# Install the CLI
curl -fsSL https://kortix.com/install | bash

# Initialize the instance
kortix self-host init --domain kortix.example.com

# Start the stack
kortix self-host start

# Watch it come up
kortix self-host status
kortix self-host logs
kortix self-host doctor
```

## Evaluation mode (no domain)

To try Kortix with no domain, use a Cloudflare tunnel instead.

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use this mode for evaluation and not for production.

## Configure the sandbox provider

After the stack starts, set your sandbox provider key.

```bash
kortix self-host configure
```

`configure` is an interactive prompt for the sandbox provider key, and optionally a managed-git token. Sign up in the dashboard, then connect your own LLM key in the model picker. Self-hosted instances use your own key by default.

## Memory limit

Each API container has a 640 MiB memory limit by default. Keep this default on an 8 GiB host. Use a 1 GiB limit on a 16 GiB host when API traffic reaches the default limit.

```bash
kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m
docker stats --no-stream
```

## Updates

Every instance updates itself automatically. To pin an exact version instead:

```bash
kortix self-host update --tag 0.9.84
```

Turn the updater off with `--auto-update off`.

## Backups

Kortix has no separate backup system. Each instance stores its data as two directories under `~/.config/kortix/self-host/<instance>/`.

- `volumes/db/data`: the Postgres database.
- `volumes/storage`: file storage.
- The instance's `.env` file: every secret and signing key it uses.

Back up all three before you run a destructive command.

## After the stack is up

The template in this repository drops into the same project flow as a cloud instance. Add `kortix.yaml`, `agents/ops-assistant.md`, and `skills/weekly-digest/SKILL.md`, then run a session. The [setup guide](setup.md) walks through it. The campaign site's [self-hosting](https://chatgptworkalternative.com/self-hosting) page answers the hosting questions a team asks first.
