---
name: segment-and-broadcast
description: Build an audience segment in Linkiasoft CRM and prepare or send a WhatsApp, SMS or email broadcast to it. Use when the user wants to message a group of customers, win back inactive buyers, promote an offer, or asks who would receive a campaign.
---

# Segment and broadcast

Broadcasts reach real customers and cannot be unsent. Follow these steps in order and never skip the confirmation.

1. **Audience.** Turn the user's description into a segment filter and call `preview_segment` (kind `customers` for buyers, `leads` for prospects). Show the count, how many have a phone or email, how many opted out, and two or three sample names.
   - Useful filters: `orderCountMin`, `lastOrderFrom`/`lastOrderTo` (win-back), `governorates`, `tags`, `stages`, `adIds`, `lastInboundFrom`.
   - If the user wants to reuse it, save it with `create_segment`.
2. **Number and template.** Call `list_channels` (type `whatsapp`) to pick the sending number, then `list_templates` with `status: APPROVED`.
   - If no approved template fits, write one with the user and call `submit_template` (category `MARKETING` for promotions, `UTILITY` for transactional; variables as `{{1}}`, `{{2}}` with one example each; up to 3 quick-reply buttons). Meta reviews it, usually within minutes to a day; check again with `list_templates`. Nothing reaches customers until a broadcast is sent.
3. **Draft.** Call `draft_broadcast` with the channel and the segment.
   - WhatsApp needs an approved template. Never invent a template name.
   - Map template variables to `first_name`, `name`, `email`, `phone` or a fixed value.
   - Drafting sends nothing.
4. **Preview.** Call `preview_broadcast` (pass `send_at` when scheduling). Show the user, in one short block: recipient count, template or subject, sample recipients, units left this month, and every warning (night-time send, empty audience, not enough units).
5. **Confirm.** Ask the user to confirm the exact recipient count. Do not continue on a vague "ok"; the count must match.
6. **Send or schedule.** Call `send_broadcast` or `schedule_broadcast` with `confirm_recipient_count` and the `preview_token` from step 4. If the tool says the audience or draft changed, go back to step 4.
7. Afterwards, `get_broadcast_performance` shows delivery and failures. To stop a send in progress, use `pause_broadcast` (later `resume_broadcast`) or `cancel_broadcast`; `retry_failed_broadcast` resends only the failed messages.

Rules:
- Drafting, previewing and submitting templates work even when the workspace has sending turned off. Only `send_broadcast` and `schedule_broadcast` need a workspace admin to allow sending in Settings → AI assistants; if they are missing, prepare the draft and preview and tell the user to switch sending on and start a new chat.
- People who opted out are excluded automatically. Never try to message them another way.
