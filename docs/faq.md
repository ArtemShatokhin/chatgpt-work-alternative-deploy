# FAQ: the open-source Kortix ChatGPT Work alternative

Kortix is open source, and these are the questions a company asks before it moves its work onto it. Each answer stands on its own. The longer list is on the campaign site's [FAQ](https://chatgptworkalternative.com/faq) page.

## Is Kortix open source?

Yes. Kortix is the open-source AI Operating System, and the source is public at [Kortix on GitHub](https://github.com/kortix-ai/suna). You can read the code that runs your agents, fork it, and audit it. The configuration is files in a git repo you own, so the version of your agents and connectors is diffable like any other code.

## Can a company self-host Kortix?

Yes, and self-host is free. Kortix runs as one Docker Compose stack for the frontend, the API, the LLM gateway, and the Supabase distribution. You install it with `kortix self-host init` and `kortix self-host start`, or with the one-shot bootstrap script on a bare Linux box. The [self-hosting guide](self-hosting.md) has the commands.

## How is Kortix different from ChatGPT Work?

Kortix is open source and runs on Kortix Cloud, in your VPC, or on your own network. ChatGPT Work is a closed product from OpenAI that runs on OpenAI's cloud with OpenAI's models. Both return finished work from an agent. Kortix lets you own the code, the configuration, and the model keys, and ChatGPT Work keeps those inside its own product.

## Which models can I use with Kortix?

Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or a sign-in with your OpenCode Console account for OpenCode Zen and Go. The provider choice is yours and the key stays yours. Kortix does not lock you to one model vendor, so a team can switch providers without moving its agents.

## How do I move my team from ChatGPT Work to Kortix?

Start by exporting the work your team repeats, such as a weekly report or a triage step, and turn each one into an agent file plus a skill in a Kortix project. Keep the same tools through connectors, set each to Allow, Ask, or Block, and run one workflow end to end before you move the rest. The campaign site has a [migrate from ChatGPT Work](https://chatgptworkalternative.com/migrate-from-chatgpt-work) page.

## What does Kortix cost?

Self-host is free. On the managed cloud, Free is $0 with 200 credits per month and 1 project. Paid plans start at $50 a month for 5,000 credits, and members are free, sharing one credit pool. ChatGPT Work follows the usage structure of OpenAI's Codex, so a heavier task uses more of a plan. Prices change, so check the campaign site's [pricing](https://chatgptworkalternative.com/pricing) page for the current numbers.

## Can I run Kortix without a domain?

Yes, for evaluation. Instead of a domain you can start the stack behind a Cloudflare tunnel with `kortix self-host init --tunnel cloudflare`. The tunnel URL changes on every restart, so use it to try Kortix and not to run production. For production, point an A or AAAA record for the domain and for `api.<domain>` at the box.

## Is Kortix a good fit if I only want a chat window?

No. If the job is a chat window or search over company documents, a product built for that fits better. Kortix runs agents that return finished work and take real actions in your tools, and each session runs in its own sandbox on its own branch. The [open-source ChatGPT Work alternative](https://chatgptworkalternative.com/open-source-chatgpt-work-alternative) page covers who it fits.
