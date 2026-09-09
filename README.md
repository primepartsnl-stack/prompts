# Prompt Library

Long-form AI build and operator prompts, kept in separate project folders so each pack can be shared with one clean link.

## Projects

### 1. AI Customer Service Dashboard

[`ai-customer-service-dashboard/`](./ai-customer-service-dashboard/)

Full build specification and visual references for an AI ecommerce customer-service dashboard.

Main prompt: [`customer-service.md`](./ai-customer-service-dashboard/customer-service.md)

### 2. Hermes Operator Stack

[`hermes-operator-stack/`](./hermes-operator-stack/)

Master execution prompt for configuring Hermes Agent as a business operator across Google Meet, telephony, Google Ads, Shopify, and Hermes Kanban/multi-agent workflows.

Main prompt: [`hermes-operator-master-setup.md`](./hermes-operator-stack/hermes-operator-master-setup.md)

## Structure

Each project lives in its own folder and keeps its main prompt, README, sources, and supporting files together. Open the project README first when sharing a pack with someone else.

## Important

These prompts are designed for AI agents that can inspect files, use a terminal, and execute work. Integrations and APIs can change, so the prompts tell the executing agent to verify current upstream documentation instead of blindly trusting stale commands.

Never commit API keys, OAuth tokens, `.env` files, browser auth state, or other secrets to this repository.
