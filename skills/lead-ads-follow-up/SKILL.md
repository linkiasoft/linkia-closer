---
name: lead-ads-follow-up
description: Follow up leads from Facebook and Instagram lead forms and missed phone calls in Linkiasoft CRM. Use when the user asks about lead form leads, whether new leads were contacted fast enough, which forms or ads bring qualified leads, or who called and was not called back.
---

# Lead ads and call-back follow-up

1. Check what is connected: `list_lead_forms` lists the lead forms with page, status, last lead time and per-form settings (stage, tags, owner or round-robin, call task, welcome template). If it says Lead Ads are not connected, tell the user to connect them in Integrations → Facebook & Instagram Lead Ads and stop here. `list_ad_accounts` shows the connected Meta ad accounts.
2. New lead-form leads: `list_leads` with `source` "Facebook Lead Ad" or "Instagram Lead Ad" (the form name follows it) and a recent `date_from`. For a lead, `get_customer_timeline` shows whether anyone has called or chatted since it arrived.
3. Speed to lead: leads with no call, chat or note since they arrived need action now. Suggest `create_task` ("Call within 5 minutes") for the owner, or `assign_conversation` if a chat exists. Forms whose leads keep waiting probably have no owner or call task in their settings; say so.
4. Missed calls: `list_missed_calls` with `not_called_back_only: true`. With the user's approval, `create_callback_tasks` creates one "Call back <name>" task per call (at most 50), assigned to the first agent the call rang unless the user picks someone.
5. Quality: `get_lead_quality_by_source` and `get_ad_performance` show which sources, forms and ads bring qualified leads and sales; `get_call_insights` gives the summary and QA score of a recorded call.
6. Summarise: new leads and how fast they were contacted, who is still waiting, tasks you created, and which forms or ads bring the best leads.

Rules:
- Do not message lead-form leads unless the user asks and the lead agreed to be contacted on WhatsApp; outside the 24-hour window only approved templates can be sent.
- Phone numbers come masked; never try to reconstruct them.
