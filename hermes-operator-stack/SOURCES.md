# Sources

Canonical upstream projects and documentation used as the reference layer for the Hermes Operator Stack.

## Hermes Agent

- Main repository: https://github.com/NousResearch/hermes-agent
- Google Meet plugin: https://github.com/NousResearch/hermes-agent/tree/main/plugins/google_meet
- Built-in plugin docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/built-in-plugins.md
- Kanban docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/kanban.md
- Telephony skill: https://github.com/NousResearch/hermes-agent/blob/main/optional-skills/productivity/telephony/SKILL.md
- Shopify skill: https://github.com/NousResearch/hermes-agent/blob/main/optional-skills/productivity/shopify/SKILL.md

## Google Ads

- Official Google Ads MCP: https://github.com/googleads/google-ads-mcp
- Google Skills repository: https://github.com/google/skills
- Google Ads MCP setup skill: https://github.com/google/skills/blob/main/skills/ads/google-ads-api-mcp-setup/SKILL.md

## Usage note

The master prompt intentionally tells the executing agent to re-check the installed CLI's `--help` output and current upstream documentation before relying on commands or API behavior that may have changed.

Do not replace official integrations with random forks merely because a fork appears newer. If an official component cannot satisfy a requirement, inspect and disclose the third-party dependency before using it.
