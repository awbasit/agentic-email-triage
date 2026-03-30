# AGENTIC EMAIL TRIAGE ON N8N

---

## PROBLEM STATEMENT

Knowledge workers spend ~2.6 hours daily managing email. A significant chunk is routine — acknowledgements, scheduling, FAQs. That's dead time that crowds out deep work.

I wanted to solve this with an AI agent that could triage, draft, and act on emails autonomously — with a human-in-the-loop gate for anything sensitive.

## WHAT I BUILT

An end-to-end intelligent email triage agent on n8n Cloud with three core agentic patterns:

* Multi-LLM Cost Routing 
Claude Haiku classifies every incoming email (routine / complex / spam) at fractions of a cent per call. Claude Sonnet only activates for drafting — where reasoning quality actually matters. Spam never touches a paid model at all.

* Conditional Agent Branching
A Switch node routes emails across three completely independent paths:
→ Routine → auto-draft and send
→ Complex → draft and escalate for approval
→ Spam → archive silently

* Human-in-the-Loop (HITL)
For complex emails, the agent drafts a reply, pauses execution using n8n's Wait node, and sends me a Pushover push notification with the draft and two tappable links — Approve and Reject. I tap one on my phone. The workflow resumes and acts accordingly. If I don't respond within 4 hours, it auto-saves as a Gmail draft.
