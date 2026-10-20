![Linkiasoft](assets/logo.png)

# Linkia Closer

**Turn chats into sales.** Linkia Closer is the [Linkiasoft CRM](https://linkiasoft.com) plugin for Claude.

Ask about your Linkiasoft CRM workspace in plain language and act on
the answer: sales and pipeline, WhatsApp, Instagram, Messenger and Telegram conversations, how
fast your team replies, which click-to-WhatsApp ads bring real buyers, and cash-on-delivery store
orders. With your workspace admin's permission, Claude can also tag leads, create tasks, reply to
a customer, build a segment and send a broadcast after you confirm the audience, and create
automations such as auto-replies, follow-ups and order confirmations.

## What's inside

- **Linkia Closer connector** (`https://mcp.linkiasoft.com/mcp`): more than 80 tools that read and
  act on your workspace with your own permissions.
- **Skills** that teach Claude how to use them well:
  - `business-review` — weekly or monthly review with the numbers that matter and what to do next.
  - `team-reply-audit` — who replies slowly, what was left unanswered, and coaching notes.
  - `ad-performance-review` — which ads bring buyers, lead quality by source, Meta event health.
  - `segment-and-broadcast` — build an audience, preview and confirm, then send or schedule.
  - `inbox-triage` — who is waiting, what customers ask about, what the AI handed off, and quick actions.
  - `cod-orders` — unconfirmed cash-on-delivery orders, order lookup, address fixes and cancellations.
  - `lead-ads-follow-up` — Facebook and Instagram lead-form leads, speed to lead, and missed-call call-backs.
  - `build-automation` — turn a description or a ready-made template into an automation, as a draft until you publish it.

## Install

- **Claude (web and desktop):** Customize → Plugins → Add → Add marketplace → `linkiasoft/linkia-closer`, then install **Linkia Closer**.
- **Claude Code:**

```
/plugin install linkia-closer --marketplace linkiasoft/linkia-closer
```

## Use it

1. Install the plugin, open its **Connectors** tab and connect **Linkia Closer**.
2. Sign in to Linkiasoft and approve what Claude may do. Your plan must include AI assistant
   connections, and a workspace admin can limit or turn them off in **Settings → AI assistants**.
3. Ask, for example: "How did this week compare with last week?", "Who on my team replies
   slowest?", "Which ads brought buyers last month?", "Draft our winter promo to Cairo customers
   who ordered twice".

## Data

The plugin itself stores nothing and runs no code on your machine. The connector sends your
requests to Linkiasoft at `mcp.linkiasoft.com`, which reads your workspace with your permissions
and returns results to Claude; Anthropic processes them to answer you. Phone numbers and emails
are masked by default, and reading message text, sending messages and exporting customer lists are
off until a workspace admin allows them. Every change Claude makes is recorded in your workspace's
activity log as "via Claude". See the "AI Assistants" section of the
[Linkiasoft privacy policy](https://crm.linkiasoft.com/privacy-policy).

## Support

Email support@linkiasoft.com.
