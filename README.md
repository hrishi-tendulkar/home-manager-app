# 🏡 Home Manager

> A personal project to simplify running a household — automating the recurring, low-grade decisions a home demands. One assistant, available everywhere, grounded against an actual data model — not a chat over context.

**Status:** Personal product. Built for and used daily by one household (mine).

![Dashboard](./screenshots/01-dashboard.png)

---

## The problem

A home is a long-running system of contracts, schedules, and small commitments. Lawn every other Thursday. HVAC spring tune-up. The drip on the kitchen faucet ignored since April.

Most home-tracking apps capture *tasks* but not *structure*. Nothing knows "Spotless Home Services" was the vendor that came last Saturday, that gutter cleaning is seasonal, or that the replacement faucet is already in the garage. Three months in, the app is a graveyard of stale checkboxes.

## The wedge

The data model has to come *before* the UI. If a chat assistant is going to answer "how much have I spent on services this year?" or "is the faucet still open?" with real numbers, the schema underneath has to model the home as objects, not strings.

That's the whole bet: **chat is the last mile of an AI product, not the product.**

## What it does

- Models a home as five first-class objects: **Home, Services, Open Loops, Records, Assistant**.
- Tracks recurring services in a 3-tier hierarchy — **Category → Service → Visit** — so spend and cadence roll up from real history.
- Treats **Open Loops** (Maintenance / Project / Fix) as their own object, with Done, Snooze, and Not-applicable as first-class outcomes — because on any given Saturday the real question is "do I owe this thread my attention this weekend, yes or no."
- Surfaces one **Assistant**, available everywhere, that has read every Service, Visit, Open Loop, and Record. It answers against the data — not in conversation.
- Parses receipts and documents into the same model so unstructured inputs become evidence the assistant can cite.

![Open loop detail](./screenshots/06-open-loop-kitchen-faucet.png)
![Assistant grounded in home data](./screenshots/08-ai-chat.png)

## Key product decisions

**Built a real Category → Service → Visit model instead of a flat task list.**
*Why:* A flat list captures what to do, not what you've done. After three months it becomes a graveyard. The hierarchy is what lets spend, cadence, and vendor history roll up — and it's what gives the assistant something to be grounded against.

**Open Loops are a separate first-class object, not a checklist row.**
*Why:* A home accumulates threads, not to-dos. "Not applicable" and "snooze" are valid outcomes alongside "done." The dashboard should reflect what's actually true.

**One assistant, everywhere — but the assistant is not the entry point.**
*Why:* The chat field sits *below* the dashboard. Structured surfaces lead; the assistant supports. Grounding beats conversation.

**Only suggest follow-ups the assistant can actually deliver.**
*Why:* A wrong suggestion is worse than no suggestion. Each follow-up is a tiny commitment ("I can answer this too"). The assistant only proposes queries it has the data to run.

**Collapsed vendors, contracts, and contacts into Services. Refused gamification, streaks, social.**
*Why:* Earlier drafts separated vendors, contracts, and contacts. Merging them made the assistant dramatically easier to ground. A home manager is for a household, not a feed; the reward is the faucet eventually gets fixed.

## Stack

- **Frontend:** React 18 + Vite + TypeScript, shadcn/ui (Radix), Tailwind, React Router, TanStack Query, react-hook-form + Zod
- **Backend:** Supabase (Postgres + Auth + Storage) + Edge Functions (Deno/TypeScript)
- **AI/LLM:** OpenAI `gpt-4o-mini` for parsing/routing, `gpt-4o` for heavier reasoning
- **Notable architecture:** Function decomposition aligned to cognitive jobs — `route-conversation`, `parse-analytics-query`, `execute-analytics`, `compose-analytics-response`, `parse-log-request`, `parse-document`, `generate-alerts`. Analytics questions run through a **parse → execute → compose** pipeline against the home graph, not freeform chat over context.

## Status

A personal product, in daily use. Built for an audience of one to test whether grounded structure actually makes an AI assistant feel different. (It does.) Not productized for distribution — it's a working demonstration of the structure-before-chat principle.

---

### What I learned

Consumer AI products lose by making the chat *the* product. Without a structured substrate the assistant has nothing to remember, and every question is a fresh conversation. The model and the schema are co-equal design surfaces: the schema constrains what the assistant can confidently say, and the assistant repays the schema by making it browsable.

---

*Source code available on request. Reach out via LinkedIn.*
