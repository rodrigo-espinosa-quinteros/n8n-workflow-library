n8n Workflow Library
A collection of case studies documenting the architecture, design decisions, and
automation patterns behind n8n workflows built for real clients and personal use
across different industries and use cases.

What's here: Each entry documents a production or near-production workflow — not just what it does, but why it was built that way: trigger design, data handling decisions, AI integration patterns, error handling, and lessons learned from real deployments.

Who this is for: Teams evaluating my work, collaborators exploring automation architecture patterns, or practitioners looking for real-world n8n implementation references.

Workflows
Workflow	Trigger	Domain	Key Patterns
PR Monitoring & Crisis Alert	Scheduled (hourly)	Public Relations	AI triage, risk-based routing, parallel CRM + alert output
AI Agent for WhatsApp	Event-driven (webhook)	Conversational AI / Sales	Stateful per-user memory, intent normalization, tool-calling, CRM logging
Webinar Email Campaign with Open Tracking	Scheduled (one-time) + Manual	Email Marketing	JS deduplication, batch + wait rate limiting, self-hosted pixel tracking
Automated Financial Reporting	Scheduled (monthly) + Manual	Business Intelligence	Two-stage JS + AI pipeline, strict JSON contracts, dual delivery
Recurring Patterns
Across these deployments, a few architectural decisions appear consistently:

Scheduled + manual dual triggers — every scheduled workflow also includes a manual trigger. This allows safe testing and emergency re-execution without modifying the schedule or waiting for the next run.

JavaScript for computation, AI for interpretation — code nodes handle aggregation, deduplication, normalization, and formatting with deterministic precision. AI nodes handle classification, analysis, and natural language generation. Neither does the other's job.

Strict JSON contracts at AI boundaries — when AI output feeds into downstream nodes, the system prompt defines the exact schema required and the user message injects exact values. This produces reliable, parseable outputs and eliminates formatting failures.

Parallel output branches — alerts and audit trails run as separate branches rather than sequentially. A Telegram alert and a CRM record are independent deliverables; one should never depend on the other completing successfully.

Environment variables for portability — client-specific values (feed URLs, chat IDs, phone numbers) are externalized as environment variables, making workflows deployable across clients without structural changes.

Integrations Used
n8n OpenAI (GPT-4.1-mini · GPT-5) WhatsApp Business API Google Sheets Microsoft Outlook Telegram Odoo RSS Feeds Webhooks

Built by Rodrigo Espinosa Quinteros
Guatemala 🇬🇹 | AI Automation Architect | Bilingual EN/ES
