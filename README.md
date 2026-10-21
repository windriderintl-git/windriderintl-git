# Robert Sanberg

CEO of [WindRider](https://windrider.com), an outdoor gear and sun-protection apparel brand. Since 2024 I've designed and run the AI agent platform that handles much of the company's operations work. I design the architecture and direct AI coding tools (Claude Code, OpenAI Codex) to write the code; I read and review it, and everything lives in Git.

The platform's code is private because it runs a live business. This page describes how it works. I'm happy to walk through it on a screen share.

## What it does

About 110 agents: 12 orchestrator agents take work from an Asana board and delegate it to about 100 specialist agents. Separately, about 100 scheduled jobs run on timers. The work covers customer support drafts, paid ad creative, email marketing, analytics, inventory, bookkeeping and the weekly business review.

## How it's built

- **Dispatcher (TypeScript).** Signed Asana webhooks feed a queue for each agent; each agent's runner starts a headless Claude Code session. Every run is logged. 2,080 runs completed so far.
- **Shared memory (TypeScript MCP server; SQLite with full-text and semantic search).** Agents check it before acting. It holds 4,100+ learnings plus standing directives and blocked actions. Task outcomes are logged with a hypothesis and re-checked at 7, 30 and 90 days.
- **Monitoring.** An operations dashboard for agents, scheduled jobs and approvals, with Slack alerts and health checks for stalled runs and broken integrations.
- **Model choice.** I watch token usage and assign work to different models to keep quality up and usage down.

## Safety

- The whole system runs on its own virtual machine, isolated from day one.
- A person approves anything that spends money, publishes or contacts a customer. Approval has to be written by a human: I found and fixed a case where agent-written "APPROVED" text could pass as sign-off.
- Data the agents read from outside systems is treated as untrusted, never as instructions.
- Credentials live in one place. Agents pause automatically after 3 failures in an hour, and agent-to-agent handoffs are capped at 3.

## Testing

- A plan-review agent gives a pass, revise or reject verdict before plans and system changes run.
- Automated tests on the dispatcher, including a replay of 139 real tasks from a duplicate-task incident, confirming the fix stops every one.

## What I retired

Two other orchestration systems I built, measured and shut down. One (~169,000 lines) never published a landing page and needed a median of 24 human touches per goal. The lesson: a second orchestrator has to earn its place.

## Public projects here

- **[whisperapp](https://github.com/windriderintl-git/whisperapp)**: friends of mine were paying $15 a month for Wispr Flow, a dictation app, so I built a free, open-source (MIT) replacement that runs entirely on your own computer. Hold a hotkey and speak; it transcribes with Whisper, cleans up the text with a local AI model and matches the tone to the app you're typing in. No subscription, nothing sent to the cloud.
- **[AIIMNIFY](https://github.com/windriderintl-git/AIIMNIFY)**: packages internal notes and Claude/Codex skills for sharing, stripping out private information first.
- **[soth-mockup](https://github.com/windriderintl-git/soth-mockup)**: a 12-page website redesign mockup for a community organization.

[LinkedIn](https://www.linkedin.com/in/robert-sanberg-a81a956)
