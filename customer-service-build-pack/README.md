# Customer Service Build Pack

This ZIP contains the long-form build specification and visual references for the AI ecommerce customer-service dashboard.

## Files

- `customer-service.md` — master build prompt/spec. Give this to Codex/Cursor/Claude Code or another coding agent.
- `references/01-dashboard-overview-reference.png` — primary desktop dashboard visual reference.
- `references/02-ticket-detail-reference.png` — inbox/ticket/order/AI-action visual reference.
- `references/03-daily-briefing-reference.png` — daily briefing/report visual reference.
- `references/04-carousel-dashboard-reference.png` — overall spatial/neumorphic polish reference.
- `reference-manifest.json` — reference roles and dimensions.

## Recommended instruction to the coding agent

> Read `customer-service.md` fully before editing code. Inspect the existing repository and every image in `references/`. Build the system end-to-end, then run the completion/self-review loop in the spec. Do not stop at a static UI or mocked integration.

The spec intentionally tells the coding agent to verify current provider docs if APIs have changed after the document date.
