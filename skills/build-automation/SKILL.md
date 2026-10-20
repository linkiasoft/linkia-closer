---
name: build-automation
description: Build a Linkiasoft CRM automation (flow) from a plain-language description or a ready-made template. Use when the user wants an auto-reply, a welcome message, a keyword or comment reply, a follow-up when a customer goes quiet, a COD order confirmation, an abandoned-checkout reminder, a hand-off to a person, a satisfaction survey, or asks to automate any step in WhatsApp, Instagram, Messenger or store orders.
---

# Build an automation

1. Understand the goal: what starts it (a message, a keyword, a comment, a new lead, a stage change, a new or changed order, an abandoned checkout, a finished call), what it should send or do, and what happens when the customer does not answer.
2. Check the library first: `list_automation_templates` (pass `locale: "ar"` for Arabic messages). If a template fits, use it: `create_automation` with `template_id` and a clear `name`. Templates land as drafts; the user can adjust the wording in the app's builder.
3. Otherwise build a custom flow:
   - Call `get_automation_guide`. It lists every trigger and step with its config fields and output handles, and this workspace's real channels, approved templates, lead stages, users and stores. Use only those ids; ask the user when one is missing (for example which WhatsApp number or which stage).
   - Exactly one `trigger` node. Keep node keys short snake_case. Leave positions out; they are laid out automatically.
   - Branch with buttons (`interactive_message`), reply options (`wait_for_reply`) or a step's output handles, never with conditions on edges.
   - Official WhatsApp numbers can only send free text inside the 24-hour window. Proactive messages (order confirmations, reminders days later) need an approved template.
4. Show the user the plan in plain words (trigger, each step, each branch, the exact messages) before creating it.
5. Create it with `create_automation`; it is always saved as a draft. If it comes back with problems, fix each one and try again; nothing was created.
6. Going live: only when the user says so, `publish_automation` makes the draft the live version and `resume_automation` switches it on. A live automation acts on real customers without anyone watching, so confirm each step first.
7. After it has run, `get_automation_runs` shows completed and failed runs and the most common errors; `pause_automation` stops it.

Rules:
- Never switch an automation on without the user's clear yes.
- Do not invent template names, channel ids, stage keys or user ids; take them from the guide.
- Tell the user they can open and edit the draft in Automations in the Linkiasoft app.
