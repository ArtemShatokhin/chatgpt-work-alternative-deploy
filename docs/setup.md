# Setup: run the open-source Kortix template

Kortix is open source, and this guide takes you from a bare machine to a running project built from this template. You install the `kortix` CLI, scaffold a project, add the template's manifest, agent, and skill, connect a model, and start a session.

## 1. Install the CLI

```bash
curl -fsSL https://kortix.com/install | bash
kortix --version
```

The CLI runs on macOS and Linux, and on Windows under WSL. It installs the `kortix` binary and the runtime config the project uses.

## 2. Scaffold a project

```bash
kortix init
```

This creates `kortix.yaml` and the project's runtime config. New projects use a v2 manifest and the OpenCode harness. OpenCode is the harness for the agent loop, and `kortix.yaml` is the Kortix layer that sits around it.

## 3. Add the template

Copy these three files from this repository into the project that `kortix init` created:

- `kortix.yaml`
- `agents/ops-assistant.md`
- `skills/weekly-digest/SKILL.md`

The manifest declares the machine image, connectors and triggers, and secret names and grants. Secret values never appear in the repo. The template ships one cron trigger and one agent:

```yaml
triggers:
  - slug: weekly-digest
    type: cron
    cron: '0 0 9 * * 1-5'
    prompt: Summarize this week's commits and open a change request with the digest.

agents:
  ops-assistant:
    file: agents/ops-assistant.md
    connectors: all
```

An agent is `agents/<name>.md` for behavior plus an `agents.<name>` block in `kortix.yaml` for governance. The `.md` file is a stock OpenCode agent file. Edit the prompt in `agents/ops-assistant.md` to describe the job your team needs.

## 4. Connect a model

Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or sign in with your OpenCode Console account for OpenCode Zen and Go. Models are BYOK in the app, so your provider key is configured after the instance starts and never has to sit in this repository.

The [models and your keys](https://chatgptworkalternative.com/models-and-your-keys) page on the campaign site covers the provider options.

## 5. Run a session

```bash
kortix sessions new --prompt "Summarize this week's commits and open a change request"
kortix cr ls
kortix chat
```

Each session gets its own isolated sandbox on its own branch. The agent works there, commits what it produces, and opens a change request. You review the diff and merge. Merge is default-deny for agents, and a session can never merge a change request it opened itself.

## 6. Ship or self-host

```bash
kortix ship
```

`kortix ship` pushes your repo and brings the project live on Kortix Cloud. To run it on your own box instead, follow the [self-hosting guide](self-hosting.md).

## Where the template talks to your tools

Connectors give an agent reach into apps and APIs. The campaign site's [connectors and automation](https://chatgptworkalternative.com/connectors-and-automation) page lists what a trigger and a connector can do, and [governance and permissions](https://chatgptworkalternative.com/governance-and-permissions) covers the Allow, Ask, and Block rules you set per call.
