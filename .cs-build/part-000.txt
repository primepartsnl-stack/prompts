# customer-service.md — COMPLETE BUILD SPEC

> **Purpose**: This file is the master build specification for a production-grade, AI-powered ecommerce customer-service dashboard. It is intentionally exhaustive. Treat it as the source of truth for product behavior, visual design, data flow, integrations, safety, testing, and completion criteria.
>
> **Primary implementation rule**: read this file **completely before writing code**. Inspect the existing repository first. Preserve working architecture when sensible. If no viable app exists, create one. Do not stop at a scaffold or prototype. Continue implementation, testing, visual comparison, and bug fixing until every required acceptance criterion in this document passes, subject only to unavoidable tool/runtime limits.

---

# 0. Non-negotiable execution contract

You are building a real customer-service operating system for an ecommerce merchant. This is not a concept page, fake dashboard, static mockup, generic SaaS template, or UI-only prototype.

You must implement the full vertical slice:

1. authentication and tenant/store isolation;
2. Shopify connectivity;
3. inbox connectivity;
4. order/customer/fulfillment/tracking context;
5. customer-service ticket ingestion and normalization;
6. AI intent detection and decisioning;
7. strict tool boundaries;
8. AUTO and REVIEW modes;
9. policies and automation rules;
10. safe Shopify write actions;
11. replies and message threading;
12. audit logs;
13. analytics;
14. daily briefings;
15. dashboards matching the supplied reference images;
16. loading, empty, offline, retry, partial-data, revoked-token, rate-limit, and permission-denied states;
17. comprehensive tests;
18. visual-regression checks;
19. observability and logs;
20. production-safe configuration.

Do not invent successful backend behavior. If an integration is not configured, show a clear disconnected state and setup flow. Never fake a successful Shopify mutation, email send, refund, return, cancellation, reship, or address change.

Do not expose API keys or access tokens to the browser, the LLM, analytics tools, logs, screenshots, or error messages.

Do not give the LLM unrestricted network access or raw Shopify credentials. The LLM may interact only through narrow server-side tools defined in this specification.

Do not add fake “AI online”, “credits remaining”, fake system-health badges, fake status claims, made-up savings, or made-up analytics. Every metric must come from real stored events or be explicitly labeled demo/seed data in development.

---

# 1. Visual source of truth

The ZIP that contains this file includes four visual references. They are not decorative inspiration. They are implementation references.

Relative paths:

- `references/01-dashboard-overview-reference.png`
- `references/02-ticket-detail-reference.png`
- `references/03-daily-briefing-reference.png`
- `references/04-carousel-dashboard-reference.png`

## 1.1 Priority order when references conflict

1. **Dashboard overview reference** controls the desktop overview page layout.
2. **Ticket detail reference** controls inbox/ticket detail behavior and pane proportions.
3. **Daily briefing reference** controls the briefing card language, hierarchy, and compact report presentation.
4. **Carousel dashboard reference** controls overall polish, spatial depth, softness, whitespace, and brand feeling.
5. This markdown controls behavior, exact content requirements, states, safety, and technical architecture.

If a numeric design token below conflicts visually with the reference image, the **image wins**. Adjust the token until the rendered screenshot visually matches.

## 1.2 Visual-regression loop — mandatory

Do not eyeball once and stop.

For every primary screen:

1. run the app at the target desktop viewport;
2. capture a deterministic screenshot with seeded demo data;
3. compare the screenshot against the corresponding image reference;
4. inspect geometry first: page margins, sidebar width, card sizes, chart proportions, table row heights, whitespace;
5. inspect typography second: font size, weight, line height, tracking, truncation;
6. inspect surface styling third: fill, border, shadows, radius, elevation;
7. inspect color fourth;
8. fix the largest visible differences;
9. recapture;
10. repeat until no major visual mismatch remains.

There is no arbitrary “three tries” limit. Keep iterating while visible mismatch remains.

Recommended tooling when available:

- Playwright screenshots;
- pixel-diff tooling such as `pixelmatch` or equivalent;
- image overlays at 50% opacity;
- component-level Storybook visual snapshots if already present.

Pixel diff must not be treated as the sole criterion because the supplied references are image designs rather than exact DOM captures. Use structural visual judgment as well.

---

# 2. Product definition

The product is a merchant-facing customer-service dashboard for ecommerce.

The core promise:

> Incoming support messages are connected to Shopify customer/order/fulfillment context. The system can draft or safely execute routine customer-service actions, depending on configured policy and mode, while escalating uncertain or risky cases to a human.

The dashboard also acts as a customer-service intelligence layer:

- identifies recurring support problems;
- shows ticket and resolution trends;
- calculates verified automation rates;
- detects spikes in issue categories;
- produces a daily briefing;
- recommends operational fixes;
- lets the merchant decide which workflows are AUTO versus REVIEW.

---

# 3. Primary user journeys

## 3.1 First-time merchant setup

1. User signs in.
2. User creates or joins an organization/workspace.
3. User sees integration checklist.
4. User connects Shopify.
5. User connects an inbox provider: Gmail or Microsoft 365/Outlook. A generic provider adapter may be added later.
6. System validates tokens and required scopes.
7. System imports recent relevant Shopify objects required to correlate support tickets.
8. System imports recent support threads/messages.
9. System asks merchant to configure policies:
   - refund rules;
   - return window;
   - replacement/reship rules;
   - address-change rules;
   - cancellation rules;
   - high-value threshold;
   - escalation triggers;
   - tone of voice.
10. AUTO mode stays globally disabled until merchant explicitly enables at least one automation rule.
11. User lands on dashboard with real metrics or clearly marked empty states.

## 3.2 New inbound customer message

1. Inbox provider emits a change event or is reconciled by sync job.
2. Message is normalized into a provider-independent message model.
3. Thread/ticket is created or updated idempotently.
4. Customer identity is resolved by sender email and, when needed, merchant-selected order/customer.
5. Shopify context is fetched server-side.
6. Relevant policies are retrieved.
7. AI classifies intent and proposes a decision.
8. The policy engine independently validates whether 