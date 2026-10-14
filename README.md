# Kortix deploy: an open-source ChatGPT Work alternative you can self-host

Kortix is open source, and this repository is a working deployment template for it: a `kortix.yaml` manifest, a starter agent, a starter skill, and a cron trigger that run the open-source ChatGPT Work alternative on hardware a company owns. The product is Kortix, the open-source AI Operating System, and the template is a starting point you fork and adapt.

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. One isolated sandbox per session. Each session has its own isolated machine and branch. Session work reaches `main` through a change request. Merge is default-deny for agents. Any model provider with your own keys, or the ChatGPT plan you already pay for.

The guides in `docs/` cover setup, the comparison with ChatGPT Work, self-hosting, and the questions teams ask before they move.

## What you get

- `kortix.yaml`, the manifest that declares the machine image, connectors and triggers, and secret names and grants. Secret values never appear in the repo.
- `agents/ops-assistant.md`, a starter agent that drafts a weekly digest and opens a change request for review.
- `skills/weekly-digest/SKILL.md`, a starter skill that encodes how the digest is assembled.
- A cron trigger that starts a session with nobody present.
- A self-hosting path on one Docker Compose stack, on your own VPS or network.
- Model choice you own. Any model provider with your own keys, or the ChatGPT plan you already pay for.
- Governance: per-resource permissions for people and agents. Roles, groups, and an audit trail. Approval gates you set, off until you set them.

## Quickstart

Install the CLI, scaffold a project, and ship it.

```bash
# 1 · Install the CLI
curl -fsSL https://kortix.com/install | bash

# 2 · Scaffold a project: creates kortix.yaml plus your agents and runtime config
kortix init

# 3 · Ship it: pushes your repo and brings it live
kortix ship
```

Start a session and review what an agent proposes.

```bash
kortix sessions new --prompt "Summarize this week's commits and open a change request"
kortix cr ls
kortix chat
```

Copy `kortix.yaml`, `agents/`, and `skills/` from this repository into the project that `kortix init` creates, then run `kortix ship`.

## Compare at a glance

Kortix is the recommendation here. ChatGPT Work facts come from OpenAI's own pages, checked October 2026.

| | Kortix | ChatGPT Work |
| --- | --- | --- |
| Open source | Yes. Read it, fork it, audit it. | No, a closed product |
| Models | Any provider, your own keys | OpenAI's models only |
| Where it runs | Kortix Cloud, your VPC, or on-prem | OpenAI's cloud, no self-host |
| Your configuration | Files in a git repo you own | In their product |
| Review | A change request a person approves | Approval controls in their product |
| Access | Self-host free; managed cloud plans | ChatGPT plans; usage metered like Codex |

The full comparison, with sources, is in [Kortix vs ChatGPT Work](docs/kortix-vs-chatgpt-work.md) and on the site's [ChatGPT Work vs Kortix](https://chatgptworkalternative.com/chatgpt-work-vs-kortix) page.

## Repository layout

```text
.
├── README.md
├── kortix.yaml                 # manifest: connectors, triggers, secret names and grants
├── agents/
│   └── ops-assistant.md        # starter agent
├── skills/
│   └── weekly-digest/
│       └── SKILL.md            # starter skill
└── docs/
    ├── setup.md
    ├── kortix-vs-chatgpt-work.md
    ├── self-hosting.md
    └── faq.md
```

## Self-hosting

Kortix runs as one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. Agent sessions run on a separate sandbox provider, not on this stack.

On a bare Linux box, the self-hosting documentation ships a one-shot bootstrap script that installs Docker, installs the `kortix` CLI, and starts the stack. To control each step, point DNS at the box, then initialize and start.

```bash
kortix self-host init --domain kortix.example.com
kortix self-host start
kortix self-host configure
```

`kortix self-host configure` is an interactive prompt for the sandbox provider key, and optionally a managed-git token. The full walkthrough is in the [self-hosting guide](docs/self-hosting.md).

## Start here

- [Setup guide](docs/setup.md): install the CLI, add the template, connect a model, run a session.
- [Kortix vs ChatGPT Work](docs/kortix-vs-chatgpt-work.md): the two products compared on source, models, hosting, configuration, and review.
- [Self-hosting](docs/self-hosting.md): the Docker Compose stack, evaluation mode, updates, and backups.
- [FAQ](docs/faq.md): the questions teams ask before they move.

## The campaign site

The site behind this repository answers the same query on the web: [chatgptworkalternative.com](https://chatgptworkalternative.com/).

- [Open-source ChatGPT Work alternative](https://chatgptworkalternative.com/open-source-chatgpt-work-alternative)
- [ChatGPT Work alternatives](https://chatgptworkalternative.com/chatgpt-work-alternatives)
- [Self-hosting](https://chatgptworkalternative.com/self-hosting)
- [ChatGPT Work vs Kortix](https://chatgptworkalternative.com/chatgpt-work-vs-kortix)
- [Models and your keys](https://chatgptworkalternative.com/models-and-your-keys)
- [Connectors and automation](https://chatgptworkalternative.com/connectors-and-automation)
- [Governance and permissions](https://chatgptworkalternative.com/governance-and-permissions)
- [Migrate from ChatGPT Work](https://chatgptworkalternative.com/migrate-from-chatgpt-work)
- [Pricing](https://chatgptworkalternative.com/pricing)
- [FAQ](https://chatgptworkalternative.com/faq)

New pages cover the questions teams ask before they move: [ChatGPT Work for teams](https://chatgptworkalternative.com/chatgpt-work-for-teams) on a shared setup the team owns and reviews, [ChatGPT Work data and privacy](https://chatgptworkalternative.com/chatgpt-work-data-and-privacy) on where the work and the configuration sit, [ChatGPT Work limitations](https://chatgptworkalternative.com/chatgpt-work-limitations) on the real limits of the hosted product, and a head-to-head [ChatGPT Work vs Gemini](https://chatgptworkalternative.com/chatgpt-work-vs-gemini). Two more comparisons sit alongside them: [ChatGPT Work vs Claude Cowork](https://chatgptworkalternative.com/chatgpt-work-vs-claude-cowork) and [ChatGPT Work vs Microsoft Copilot](https://chatgptworkalternative.com/chatgpt-work-vs-copilot), with a short answer to [is ChatGPT Work open source](https://chatgptworkalternative.com/is-chatgpt-work-open-source).

The Kortix source code is public. Read it, fork it, audit it at [Kortix on GitHub](https://github.com/kortix-ai/suna). Read the product documentation at [Read the docs](https://kortix.com/docs).

Kortix is free to self-host. [Try Kortix](https://kortix.com).
