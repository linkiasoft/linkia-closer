---
name: cod-orders
description: Run cash-on-delivery (COD) store orders in Linkiasoft CRM for Egyptian and other COD e-commerce stores connected through Shopify. Use when the user asks which orders are not confirmed yet, wants to find an order by number or phone, cancel an order, fix a delivery address, add an order note, or review confirmation, delivery and return rates.
---

# COD orders

1. Unconfirmed orders: call `list_unconfirmed_orders` (default: placed more than 6 hours ago, last 7 days). Group by `confirmation_status`:
   - `pending` / `sent` / `read`: the WhatsApp confirmation is out but the customer has not answered.
   - `no_answer`: no reply after the reminder; a phone call is the next step.
   - `needs_call`: the customer asked to talk to someone; call first.
   Show the oldest first with hours waiting, total and store.
2. One order: `find_orders` with the order number (`1042` or `#1042`) or the customer's phone (local `01…` numbers work), then `get_order` for items, address, tracking and history. `get_customer_timeline` shows the customer's chats and earlier orders, useful to spot repeat refusers.
3. Actions, only when the user asks and after showing the order:
   - `update_order_address` when the customer corrects the address (address line and city are required; governorate goes in `province`).
   - `add_order_note` for courier instructions such as "deliver after 5 pm".
   - `cancel_order` needs a reason (`customer`, `inventory`, `fraud`, `declined`, `other`). It restocks by default. Confirm the order number with the user first; cancelling cannot be undone from here. Only set `notify_customer` when the user asks for the store's cancellation email.
   - For chats that need a person, `create_task` ("Call Mona about order #1042") or `assign_conversation` on the linked conversation.
4. Rates and trends: `get_cod_order_stats` (by governorate, product, courier or source) for confirmation, delivery and return rates, and `get_product_performance` for products with high return rates.
5. Summarise: how many orders wait and since when, which need a call, what you changed, and where returns come from.

Rules:
- There is no tool to resend the WhatsApp confirmation for one order; the store's COD flow sends it. If the user wants to nudge a customer, draft a message and use `send_message` (inside the 24-hour window, or with an approved template) after the user confirms.
- Phone numbers, emails and address lines come masked when the workspace masks personal data; never try to reconstruct them.
- Orders created in chat or imported from before the store was connected are not in the unconfirmed list.
