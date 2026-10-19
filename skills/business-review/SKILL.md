---
name: business-review
description: Weekly or monthly business review of a Linkiasoft CRM workspace. Use when the user asks how the business is doing, how this week or month compares with the last, where sales are lost, or wants a summary for the owner or a team meeting.
---

# Business review

Produce a short, numbers-first review the owner can act on.

1. Call `whoami` once to learn the workspace timezone and what this connection may do. Interpret "this week", "last month" and similar in that timezone.
2. Call `get_business_overview` for the period the user named (default: the last 7 days). It returns each metric with the previous period and the change.
3. Call `get_conversion_funnel` for the same period to find where conversations stop turning into sales. Note the `largest_drop`.
4. Call `get_response_time_impact` to see whether slow replies are costing sales.
5. If the overview shows store orders, call `get_cod_order_stats` (group by governorate) for confirmation, delivery and return rates and the revenue that came from chats.
6. Write the review:
   - Three to five headline numbers with their change, best first.
   - The single biggest problem, with the number that proves it (for example "41% of Instagram chats never get a reply").
   - Two or three concrete actions, each tied to a number.
   - Keep it under 250 words unless the user asks for more.

Rules:
- Quote only numbers the tools returned. If a metric is null, say it does not apply (for example no store connected) rather than guessing.
- Percentages from the tools are already in percent.
- If a tool returns `open_in_app`, end with that link so the user can open the full report.
