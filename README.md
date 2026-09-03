# 🤝 AI Multi-Agent Business Operations Assistant

A multi-agent AI system built in n8n that acts as a business's virtual front
desk reading a customer's message, understanding what they actually need,
and orchestrating multiple specialist AI agents to handle scheduling,
knowledge-based questions, and escalation, then composing everything into
one natural, professional customer reply.

## 🎯 Problem This Solves

Most AI chatbots can only do one thing at a time answer a question, or
take a booking, but not both together, and they rarely know when to hand
off to a human. Real customer messages are rarely that simple: a single
message often contains a booking request, a policy question, and an
implicit expectation of a quick, coherent human-sounding reply all at
once. This system solves that by using a genuine multi-agent architecture,
where a central orchestrator reads the full request, delegates to the
right specialist agents in parallel, and merges their work into a single,
polished response the way a well-run human front desk actually operates.

## ⚙️ How It Works

1. **Trigger:** A webhook receives a customer's message
2. **Orchestrator Agent:** Reads the message and determines, in one pass,
   whether the customer needs scheduling, a knowledge-based answer,
   human escalation any combination of the three, since these are not
   mutually exclusive
3. **Parallel Specialist Delegation:**
   - **Scheduling Agent:** Checks real Google Calendar availability and
     books an actual appointment, generating a direct, clickable
     confirmation link
   - **Knowledge Agent (RAG):** Embeds the customer's specific question,
     retrieves the most relevant chunks from a Pinecone vector database
     built on real company policy documents, and drafts an answer
     grounded only in that retrieved content never guessed
   - **Escalation Agent:** Runs independently of the other two; if the
     Orchestrator flags the message as needing human attention (anger,
     legal threats, explicit request for a manager), an internal alert
     is sent immediately and the customer-facing flow is bypassed
4. **Response Composer:** For non-escalation cases, the outputs from the
   Scheduling and Knowledge agents are merged and passed to a final AI
   step that writes one warm, natural, professional email never two
   separate robotic replies
5. **Delivery:** The composed email is sent directly to the customer,
   including their confirmed appointment time and a direct link to view
   the calendar event

## 🧠 Why This Is a Genuine Multi-Agent System

This isn't a single AI call with a few if/else branches. Each specialist
agent operates independently, with its own tools, its own reasoning step,
and its own failure mode the Orchestrator's job is purely to route and
delegate, and the Response Composer's job is purely to synthesize. A
customer message needing both a booking and a policy answer triggers two
agents running in parallel, whose outputs are only combined at the very
end this mirrors how real agentic AI systems are architected in
production, not a simplified demo shortcut.

## 🛠️ Tech Stack

- **Automation:** n8n (self-hosted)
- **Orchestration & Reasoning:** OpenAI GPT-4o (intent classification and
  task delegation)
- **Scheduling:** Google Calendar API real availability checks and
  event creation
- **Knowledge Retrieval (RAG):** Pinecone vector database + OpenAI
  embeddings (`text-embedding-3-small`), built on a dedicated company
  knowledge base
- **Response Synthesis:** OpenAI GPT-4o-mini (final reply composition)
- **Delivery:** Gmail API
- **Testing:** Postman (webhook simulation across multiple real-world
  scenarios)

## 🔑 Key Learnings

- A single Switch node (one-of-many routing) is the wrong tool when
  multiple outcomes can be true simultaneously this project uses
  independent, parallel IF nodes instead, since a customer request can
  need scheduling, a knowledge answer, both, or neither, all at once
- Google Calendar's "Get many" action returns no output when a queried
  time range has zero existing events, which halts the workflow by
  default — resolved by enabling "Always Output Data" in that node's
  settings, since an empty calendar is a valid, expected state, not an
  error
- Vector store nodes return retrieved content nested inside a `document`
  object (e.g., `document.pageContent`), not as a flat `text` field
  always inspect real node output before writing downstream parsing code
  rather than assuming a field structure
- After a Merge node combines multiple branches, `.item` references can
  fail with "paired item data unavailable" since n8n can no longer
  determine a single matching source item; `.first()` resolves this
  reliably
- Plain-text emails render exactly as the source string is formatted
  explicit prompt instructions to write continuous paragraphs (rather
  than manually broken lines) are necessary for the AI's output to
  render as natural, professional prose rather than fragmented text
- A working demo requires testing genuinely different real-world
  scenarios, not just one happy path this system was validated against
  a combined booking-and-question message, and a separate,
  clearly-escalation-worthy message, to confirm both the delegation logic
  and the escalation bypass work independently and correctly

## 📋 Setup Instructions

1. Import the main workflow JSON into your n8n instance
2. Create a Pinecone index and load `business-knowledge-base.md` into it
   using a separate one-time loader workflow (Manual Trigger → Vector
   Store "Insert Documents" → Default Data Loader → Embeddings OpenAI)
3. Connect your own OpenAI, Google Calendar, Pinecone, and Gmail
   credentials
4. Update the Google Calendar reference to your own calendar
5. Send a test request to the webhook with a customer name, email, and
   message
6. Activate the workflow

## 🚀 Future Enhancements

- Smarter scheduling logic that parses the customer's exact stated time
  preference (e.g., "Thursday morning") against real calendar
  availability, rather than defaulting to the next available standard
  slot
- Support for rescheduling and cancellation requests as additional
  agent capabilities
- A voice channel (phone-based) using the same underlying agent
  architecture, allowing customers to reach the same system by call or
  by message

## 📌 Status

Fully functional tested end-to-end across multiple real-world
scenarios, including a combined scheduling-and-knowledge-question
request and a distinct escalation-only request, with real calendar
bookings, real RAG-grounded answers, and real email delivery confirmed.

## 🎥 Demo

[Watch the walkthrough](PASTE_YOUR_VIDEO_LINK_HERE)

## 👤 Built By

Noor ul Ain — Agentic AI Developer specializing in Python, machine
learning, and AI-powered multi-agent automation using n8n.
