# Hermes Operator Stack

A long-form execution prompt for turning a desktop, laptop, VPS, or server into a working **Hermes Agent operator stack**.

This is not a tutorial prompt. It tells an AI agent with terminal/computer access to inspect the machine, install or repair Hermes when needed, configure the integrations it can configure, stop only for credentials/approval, run smoke tests, and report exactly what is actually working.

## Main file

- [`hermes-operator-master-setup.md`](./hermes-operator-master-setup.md) — the complete master setup prompt. Copy the entire file into an AI agent with terminal/computer access.
- [`SOURCES.md`](./SOURCES.md) — canonical upstream projects/docs used as the reference layer for the setup.

## What it sets up

The stack is built around five capabilities:

1. **Google Meet** — join supported Meet calls, transcribe, summarize, and extract action items.
2. **Telephony** — Twilio/Bland/Vapi paths for approved SMS and phone-call workflows.
3. **Google Ads Operator** — connect the official Google Ads MCP, inspect real account data, and surface concrete diagnostics without pretending read-only tooling can make edits.
4. **Shopify Operator** — read and, when explicitly authorized, perform store operations through the Admin GraphQL API.
5. **Hermes Kanban** — durable multi-agent work with `researcher`, `coder`, `reviewer`, and `deploy` profiles handing tasks between each other.

The final phase connects those pieces into one **Hermes business operator** rather than leaving them as five unrelated integrations.

## How to use it

1. Open [`hermes-operator-master-setup.md`](./hermes-operator-master-setup.md).
2. Copy the complete prompt.
3. Paste it into an agent that can actually use the target machine's terminal/computer.
4. Let the agent begin with **Phase 0 — Environment Discovery** instead of manually installing random components first.
5. Complete OAuth/credential steps when requested.
6. Approve real-world side effects only when the agent presents the exact action it wants to perform.

If the receiving agent has no computer access, the prompt tells it to first choose the correct deployment target and bootstrap Hermes there instead of pretending the setup was completed.

## Supported deployment logic

The prompt can adapt the setup for:

- Windows desktop / Hermes Desktop
- native Windows CLI
- macOS
- Linux desktop
- Linux VPS/server
- WSL2
- deliberately containerized deployments

It is intentionally environment-aware: an existing healthy Hermes installation should be preserved rather than overwritten.

## Safety model

The prompt separates local setup from external side effects. It requires explicit approval before actions such as:

- purchasing a phone number;
- sending a real SMS or placing a real call;
- joining/transcribing a real meeting without established approval;
- making live Shopify mutations with material impact;
- spending money, deleting data, or deploying production changes.

Credentials, OAuth tokens, browser auth state, and `.env` files must not be committed to this repository.

## Completion states

Every capability is reported as one of:

- `DONE`
- `DONE — READ ONLY`
- `WAITING FOR USER AUTH`
- `WAITING FOR USER APPROVAL`
- `BLOCKED`
- `NOT APPLICABLE`

The prompt explicitly forbids claiming that something is installed, connected, or tested without verification.

## Size

The master prompt is roughly **7.1k words / 49k characters**, so use the raw file rather than copying fragments from screenshots or social posts.
