---
name: ad-performance-review
description: Review click-to-WhatsApp and click-to-Messenger ad results in Linkiasoft CRM for a media buyer. Use when the user asks which ads bring leads or buyers, cost per lead, ROAS, lead quality by source, junk traffic, or whether Meta conversion events are working.
---

# Ad performance review

1. Call `get_ad_performance` for the period (default: last 30 days), sorted by `revenue`. Use `attribution: first_touch` when the user asks which ad first brought the customer, otherwise `last_touch`.
   - With an ad account connected the results include spend, cost per conversation, cost per qualified lead, CPA and ROAS. Use `group_by: campaign` or `adset` for a higher-level view.
   - If `currency_mismatch` is true, do not compare spend with revenue; say why ROAS is empty.
2. Call `get_lead_quality_by_source` with `group_by: ad` (or `source`) to separate ads that bring buyers from ads that bring junk (`junk_rate`).
3. If the user's question is about Meta optimisation, call `get_capi_health` to check that conversion events are being sent for the stages that matter, and list unmapped stages.
4. Answer as a media buyer would:
   - Scale: ads with the best revenue or qualified-lead rate per conversation.
   - Fix or pause: ads with many conversations but a high junk rate, low confirmation or high never-answered share (the problem may be reply speed, not the ad).
   - One measurement gap, if any (missing CAPI events, no spend connected).

Rules:
- Only click-to-message ads are tracked. Say so when the user asks about other ad types.
- Never invent spend. Without a connected ad account, report outcomes only.
- Sending audiences or conversions to Meta (`export_audience`, `send_offline_conversions`) changes data outside Linkiasoft. Do it only when the user asks, and confirm first.
