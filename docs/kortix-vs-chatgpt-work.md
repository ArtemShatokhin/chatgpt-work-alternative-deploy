# Kortix vs ChatGPT Work

Kortix is open source. ChatGPT Work is not. That difference shapes where each product runs, who holds the configuration, and what your team can change without asking a vendor.

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer. ChatGPT Work is an agent inside ChatGPT, from OpenAI, that takes action across apps and files and returns finished work such as sheets, slides, docs, and web apps. OpenAI launched it on July 9, 2026, according to [OpenAI's launch post](https://openai.com/index/chatgpt-for-your-most-ambitious-work).

## The two products on the facts

This comparison uses each vendor's own material, checked October 2026. Kortix rows come from the product documentation at [Kortix](https://kortix.com/docs) and the [Kortix on GitHub](https://github.com/kortix-ai/suna) repository. ChatGPT Work rows come from OpenAI's [product page](https://openai.com/chatgpt-work) and its [launch post](https://openai.com/index/chatgpt-for-your-most-ambitious-work).

| | Kortix | ChatGPT Work |
| --- | --- | --- |
| Open source | Yes. Read it, fork it, audit it. | No, a closed product |
| Models | Any provider, your own keys | OpenAI's models only |
| Where it runs | Kortix Cloud, your VPC, or on-prem | OpenAI's cloud, no self-host |
| Your configuration | Files in a git repo you own | In their product |
| Review | A change request a person approves | Approval controls in their product |
| Access | Self-host free; managed cloud plans | ChatGPT plans; usage metered like Codex |

## Source and ownership

Kortix is open source, so you can read the code that runs your agents, fork it, and audit it. The configuration lives in a git repo you own: `kortix.yaml` declares the machine image, connectors, and triggers, and secret names and grants. Secret values never appear in the repo.

ChatGPT Work is a closed product, and its configuration lives inside ChatGPT. OpenAI documents the controls an admin holds: centralized access, connected tools, and the actions ChatGPT can take, reached through the [Admin Console and Compliance API](https://openai.com/index/chatgpt-for-your-most-ambitious-work). You manage those controls inside OpenAI's product rather than in a file you can diff.

## Models

Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or sign in with your OpenCode Console account for OpenCode Zen and Go. The provider is your choice, and the key stays yours.

ChatGPT Work runs on OpenAI's models only. GPT-6 Astra has run in ChatGPT Work since September 9, 2026 ([OpenAI Help Center](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex)). The model is OpenAI's, and you do not choose the provider.

## Where it runs

Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. You can put the whole instance on a box you control.

ChatGPT Work runs on OpenAI's cloud on the web and in the mobile app. In the desktop app it also uses your local files and apps, and the [product page](https://openai.com/chatgpt-work) lists no self-hosted option. Your work runs on OpenAI's infrastructure.

## Reach into your tools

Connector credentials are brokered server-side and never enter the machine. You set each tool to Allow, Ask, or Block, down to the arguments of each call.

ChatGPT Work connects through plugins, with more than 1,400 available on the [product page](https://openai.com/chatgpt-work). OpenAI says plugins connect ChatGPT to Slack and Microsoft Teams, Google Drive and SharePoint, email, calendars, CRMs, and project trackers. The two products differ on where the credential lives and who can change the rule.

## Review and governance

Kortix runs each session in one isolated sandbox on its own branch. Session work reaches `main` through a change request. Merge is default-deny for agents. For people and agents, Kortix has per-resource permissions, roles, groups, and an audit trail. Approval gates are yours to set and are off until you set them.

ChatGPT Work gives a workspace admin controls for access, connected tools, and the actions the agent may take, and OpenAI adds an auto-review step that checks important actions before they run. That model lives in OpenAI's product, and you configure it there.

## Which one fits

Kortix fits a company that wants to own the stack: the code, the configuration, the model keys, and the machine it all runs on. It is the open-source ChatGPT Work alternative for teams whose security review asks where the data lives and who can change the agent's reach.

ChatGPT Work fits a team that already pays for ChatGPT, wants an agent inside that app, and is content to run it on OpenAI's cloud with OpenAI's models. It arrives with the ChatGPT desktop app and the tools those teams already connect.

Migration steps for a team moving from one to the other are on the campaign site's [migrate from ChatGPT Work](https://chatgptworkalternative.com/migrate-from-chatgpt-work) page, and the shorter overview is at [open-source ChatGPT Work alternative](https://chatgptworkalternative.com/open-source-chatgpt-work-alternative).
