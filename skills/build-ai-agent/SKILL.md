---
name: build-ai-agent
description: Build a client's AI sales and support agent in Linkiasoft CRM the Linkiasoft way, from the business brief to a requirements questionnaire (Word) the client fills, to a fully configured agent with its documents, website and catalogue embedded as knowledge (RAG). Use when the user wants to create, set up or prepare an AI agent, chatbot or auto-reply assistant for a business, write its prompt, send the client the AI requirements form, or turn a filled form into a working agent.
---

# Build an AI agent

Four stages. Start with `get_ai_agent_guide`: it holds the house playbook, the system prompt structure, every setting, this workspace's tool catalog and a reference agent. Follow it exactly. If the user names one of their best agents, pass it as `reference_agent_id` and copy its structure, not its facts.

## 1. Brief
Collect what the business sells, prices, what makes it different, how long it has operated, where it works, its website, products and documents, its customers and how a sale closes. Ask for every file they have (policies, brochures, price lists, catalogues). Missing facts become questions in stage 2. Never guess them.

## 2. Requirements questionnaire (Word)
Produce a **.docx** (not PDF) for the client using the section list in the playbook: identity, catalogue, policies, sales flow, hand-offs, tone, forbidden topics, greeting and fallback, follow-up, hours, channels, documents. Then add the system's features as yes/no choices.
- Write it in the client's language, with a short "why we ask" under each section.
- Pre-fill what the brief already answered so the client only confirms.
- Leave clear empty answer boxes.

## 3. Client fills it
When the filled document comes back, read every answer. List what is missing or contradictory and ask the user before building.

## 4. Build
1. `create_ai_agent`. The agent is created switched off. Write `system_prompt` in the playbook's section order and the client's dialect. Never repeat what the runtime adds by itself: the identity line, language, tone, greeting logic, guardrails, opt-out handling and the tool list.
   - `guardrails`: arrays of short sentences.
   - `tool_instructions`: one "when to use" line for every enabled tool.
   - `followup`, `handoff`, `schedule`: as the client answered.
2. Knowledge (RAG):
   - Policies, brochures, FAQs and website text go in with `add_ai_knowledge_document`, one per topic with a clear title. Enable `searchDocuments`.
   - Catalogues, price lists and branch lists go in as CSV with `add_ai_knowledge_table`. Run `dry_run` first and map the column customers ask by as `what` and location columns as `where`. Enable `searchKnowledge`.
3. Add answers to the hard questions (objections, price edge cases) with `update_ai_knowledge`.
4. Check with `get_ai_agent`: every source is indexed, and every tool has its note.
5. Show the user a short review: persona, prompt sections, tools, guardrails, follow-up, hand-off, knowledge, and anything still missing.
6. Only on the user's clear yes: `activate_ai_agent`, then `assign_ai_agent_to_channel` for each chosen channel (ids from `list_channels`).

Rules:
- Every price, number, address and policy comes from the client's answers or files. Nothing is invented.
- Never switch an agent on or put it on a channel without the user's yes. Both make it answer real customers unattended.
- Enable only the tools the flow needs.
- Changes to a live agent (`update_ai_agent`) apply to its next reply, so confirm them first.
- Tell the user they can review and fine-tune the agent in AI Agents in the Linkiasoft app.
