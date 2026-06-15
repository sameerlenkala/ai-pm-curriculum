# WEEK 3: AI PRODUCT STRATEGY, METRICS & LAUNCH

## Unit 7: AI Product Strategy — Feasibility, User Value, GTM

### The AI Product Lens

Most AI products fail not because the AI is bad, but because:
1. Users don't care (feature solves no real problem)
2. You can't measure value (is the AI actually helping?)
3. Cost/latency kills the experience (model is too slow or expensive)
4. Edge cases break trust (hallucination on an important task damages confidence)

Before starting any AI feature, run it through all three lenses: **feasibility**, **user value**, and **economics**.

### Feasibility Assessment Framework

Before building, ask:

**Q1: Is the Task Solvable by AI?**

| Task | Feasible? | Why |
|------|-----------|-----|
| Summarize a document | ✓ Yes | Clear input/output; easy to review |
| Recommend a product | ~ Maybe | Depends on data quality and recommendation criteria |
| Diagnose a disease | ✗ No | Hallucination risk too high; legal liability |
| Classify customer feedback | ✓ Yes | Clear categories; easy to evaluate accuracy |
| Generate legal documents | ✗ No | Liability; must be reviewed by a licensed attorney |
| Write product descriptions | ✓ Yes | Output is easy to review and iterate |
| Automate invoice processing | ✓ Yes (with caveats) | High accuracy on structured data; needs human review for exceptions |

**Red Flags:**
- Task requires 100% accuracy (medical, legal, financial decisions)
- No ground truth to evaluate against
- User harm if wrong (safety-critical systems)
- Task is inherently ambiguous with no clear correct answer

**Green Lights:**
- Task is currently manual and time-consuming
- Output can be reviewed quickly by a human
- Mistakes are recoverable (no irreversible actions)
- Clear, measurable definition of "good"

---

**Q2: Do You Have the Data?**

**For RAG:** Do you have documents or databases to ground the model?
- ✓ Yes, indexed and updated regularly → Go
- ~ Some, but incomplete or stale → Risky; define what's missing first
- ✗ No, or all outdated → Don't use RAG; fix the data problem first

**For Fine-tuning:** Do you have 100+ labeled examples?
- ✓ Yes, high-quality labels → Can fine-tune
- ~ 10–50 examples → Start with few-shot prompting instead
- ✗ < 10 examples → Use base model with a well-crafted system prompt

**For Agents:** Do you have APIs or tools to call?
- ✓ Yes, stable and documented → Good
- ~ Some, but unreliable → Agents will fail often; fix tooling first
- ✗ No → You can't build a useful agent

---

**Q3: Economics — Does the Cost/Benefit Work?**

**Cost Structure:**
- LLM inference: $0.001–$0.05+ per query (varies by model and prompt length)
- Retrieval: ~$0.0001–$0.001 per query (vector DB)
- Every 500ms of additional latency: ~3% fewer users complete the interaction
- Infrastructure: $100–$1,000/month for a basic RAG setup; more at scale

**Benefit:**
- Time saved per user (hours/week × hourly cost)
- Error reduction (fewer support tickets, manual corrections)
- Revenue uplift (higher conversion, better retention)
- Headcount efficiency (same team handles more volume)

**Breakeven Calculation — GO:**
```
Cost per query = $0.01
Queries per month = 100,000
Total monthly cost = $1,000

Benefit per query = $0.05 (time saved + error reduction)
Total monthly benefit = $5,000

Net = +$4,000/month → Build it
```

**Breakeven Calculation — NO GO:**
```
Cost per query = $0.05
Queries per month = 100,000
Total monthly cost = $5,000

Benefit per query = $0.03 (minor time savings)
Total monthly benefit = $3,000

Net = -$2,000/month → Don't build it; improve the problem differently
```

**Cost Levers to Pull:**
- Use a smaller/cheaper model for simple sub-tasks
- Enable prompt caching (can cut costs 80–90% on high-volume, repeated prompts)
- Batch offline tasks (process at night, not real-time)
- Cache frequent query results (if the same query is asked repeatedly)

---

### User Value: The Jobs-to-Be-Done Framework

Don't ask users "Do you want AI?" Ask what problem they're solving.

**Bad Framing:**
> "We're adding AI to summarize your documents."

**Good Framing:**
> "Today, you spend 2 hours a week reading meeting notes. We auto-summarize so you get the key points in 2 minutes — and you can drill in when something needs attention."

**User Value Checklist:**
- [ ] Does the AI make an existing task meaningfully faster?
- [ ] Does it reduce errors or decisions the user doesn't enjoy making?
- [ ] Does it enable capabilities the user couldn't have otherwise?
- [ ] Can the user understand and verify the AI's output?
- [ ] Is latency acceptable? (< 2s for chat, < 10s for batch tasks)
- [ ] Is the cost justified by the value delivered?
- [ ] Does it fit naturally into the user's existing workflow?

### Go-to-Market Strategy for AI Features

**Phase 1: Validation (1–2 weeks)**
- Build an MVP with your chosen model
- Test with 10–20 internal power users or a small beta group
- Measure: Accuracy, latency, cost per query
- Gate question: "Is this actually useful?" If no, pivot before investing more.

**Phase 2: Alpha (2–4 weeks)**
- Roll out to 1% of eligible users or a hand-picked cohort
- Monitor: Accuracy, latency, cost, user satisfaction, error patterns
- Collect feedback on edge cases and failure modes
- Gate question: "Are users getting value, and are failure modes manageable?"

**Phase 3: Beta (4–8 weeks)**
- 10–30% of users
- A/B test: AI-assisted vs. manual baseline
- Measure ROI: Time saved, error reduction, NPS delta
- Gate question: "Is ROI positive and stable?" If yes, proceed to GA.

**Phase 4: General Availability**
- Roll out to 100% of eligible users
- Monitor for model drift (accuracy degrading over time)
- Plan the model upgrade cycle (new model versions, index refreshes)
- Define the on-call escalation path when the AI fails

---

## Unit 8: Metrics, Evaluation & Risk Management for AI Features

### Success Metrics Framework

**Tier 1: Core Metrics (What Determines Success)**

*Pick 1–2 per product. These are your north star.*

| Metric | Example | How to Measure |
|--------|---------|----------------|
| **Accuracy** | "85% of AI summaries rated ≥ 4/5 by users" | Sample outputs weekly; human raters or user thumbs up/down |
| **User Satisfaction** | "Users rate AI responses 4.5/5" | Post-interaction survey (1 question, frictionless) |
| **Time Saved** | "AI saves users 30 min/week" | Time-on-task measurement; user self-report |
| **Error Rate Reduction** | "AI classification errors down 40% vs. manual" | Compare AI vs. human on shared test set |
| **Adoption** | "60% of eligible users use the feature weekly" | Feature flag + event tracking |
| **Task Completion Rate** | "Users complete 80% of AI-assisted workflows without abandoning" | Funnel analysis |

---

**Tier 2: Health Metrics (Monitor Continuously)**

These don't define success, but they tell you when something is breaking.

| Metric | Red Flag Threshold | Action |
|--------|-------------------|--------|
| **Latency (p95)** | > 5 seconds | Optimize retrieval, switch to faster model, add caching |
| **Hallucination Rate** | > 10% of sampled outputs wrong | Add/improve RAG, lower temperature, add citation requirement |
| **Cost Per Query** | Rising week-over-week with no usage growth | Audit prompt length, enable caching, consider smaller model for easy tasks |
| **User Complaint Rate** | > 5% of feedback negative | Investigate category (accuracy? speed? UX?); A/B test fix |
| **Model Drift** | Accuracy declining month-over-month | Refresh index, update system prompt, evaluate new model |

---

### Evaluation: How to Actually Measure Quality

**Gold Standard: Human Evaluation**
- Sample 100–200 AI outputs; have human raters score each (1–5)
- Calculate: % rated ≥ 4 (your accuracy target)
- Cost: 5–10 hours for 200 samples
- Frequency: Weekly for first month, then monthly once stable

**Fast: Automated Metrics**
- BLEU / ROUGE score (for summarization)
- Exact match (for Q&A with known answers)
- RAGAS framework (for RAG systems — measures retrieval quality and answer faithfulness)
- Cost: ~$0 compute; requires setup time
- Caveat: Automated metrics don't always correlate with user satisfaction

**Hybrid: Spot-Check + Automated**
- Run automated checks on all 1,000+ queries per week
- Flag suspicious outputs (low confidence, certain topics)
- Have a human review only the flagged subset
- Cost: Moderate; balances scale with quality

**Evaluation Process:**
```
1. Define your quality threshold (e.g., "≥ 4/5 rating = good")
2. Run 100 representative queries through the AI
3. Have 2–3 humans rate outputs independently (blind to each other)
4. Calculate inter-rater agreement; resolve disagreements
5. Track the % that meet your threshold week-over-week
6. If it drops below target, investigate root cause before shipping anything new
```

---

### Red Flags & Risk Management

**Risk 1: Hallucination on High-Stakes Tasks**

| Risk | How to Detect | Mitigation |
|------|---------------|-----------|
| AI invents facts (e.g., wrong policy, wrong price) | Weekly sample review; user complaint tracking | Require source citations; add RAG; human review gate for high-confidence outputs |
| Users overtrust AI and stop verifying | Track "override rate" — how often users edit AI output | Label outputs clearly as "AI suggestion"; show confidence scores; design for review |

---

**Risk 2: Bias & Fairness**

| Risk | How to Detect | Mitigation |
|------|---------------|-----------|
| Model performs worse for certain user groups (languages, demographics) | Segment accuracy metrics by user cohort | Test on diverse inputs pre-launch; add bias audit to quarterly review |
| Recommendations favor certain outcomes unfairly | A/B test AI recommendations vs. baseline; audit recommendation distribution | Publish recommendation criteria; allow user override |

---

**Risk 3: Data Privacy & Security**

| Risk | How to Detect | Mitigation |
|------|---------------|-----------|
| Sensitive user data sent to 3rd-party LLM API | Audit data flow; review what's in prompts | Use on-premise models for sensitive data; encrypt in transit; negotiate no-logging agreements with providers |
| PII leaking into RAG index | Audit what gets indexed | Scrub PII before indexing; access-control the index to match user permissions |

---

**Risk 4: Cost Spiral**

| Risk | How to Detect | Mitigation |
|------|---------------|-----------|
| Token costs grow as usage scales | Track $/query and total LLM spend weekly | Set budget alerts; enable prompt caching; batch offline queries; route simple tasks to cheaper models |
| Retrieval infrastructure scales poorly | Monitor vector DB query costs and latency | Cache frequent retrieval results; archive stale documents |

---

**Risk 5: Model Degradation Over Time**

| Risk | How to Detect | Mitigation |
|------|---------------|-----------|
| Accuracy declines gradually (data drift or model provider changes) | Weekly automated spot-check; monthly human eval | Retrain/update monthly; alert on accuracy threshold breach; maintain evaluation dataset |

---

### Communicating AI Risk to Stakeholders

**To Executives (Cost/ROI framing):**
> "We'll launch the AI feature to 5% of users first, which caps our risk exposure. Expected ROI is 3x if we hit 85% accuracy. We'll measure this weekly. If accuracy drops below 80%, we pause and investigate before expanding."

**To Engineering (Technical risk framing):**
> "The top risks are hallucination (mitigated by RAG + citations) and latency (we've modeled < 2s at p95). We'll monitor both in staging and have a rollback plan ready for launch."

**To Customers (Trust framing):**
> "Our AI assistant is designed to help, not replace, human judgment. Every AI suggestion shows its source so you can verify. You're always in control."

---

## Capstone: Write an AI Feature PRD

**Task:** Using everything you've learned, write a 1-page PRD for an AI feature.

**Pick a Use Case:**
- Customer support chatbot
- Code review assistant
- Sales email draft generator
- Meeting note summarizer
- Product recommendation engine
- Content moderator
- Or your own idea

---

### AI Feature PRD Template

**Title:** [Feature Name]

**Problem Statement:**
- What problem does this solve? (1–2 sentences)
- Why now? (What's changed — new capability, new user pain, competitive pressure?)
- Business impact if solved (time/cost/revenue estimate)

**User Story:**
> As a [user role], I want [capability], so that [benefit].

**Goals:**
- Primary goal: (e.g., "Reduce average support response time by 50%")
- Success metric: (e.g., "Avg response time < 2 hours; AI suggestion accuracy ≥ 85%")

**Non-Goals:**
- What are we explicitly NOT doing? (e.g., "Not replacing human agents; not handling escalated complaints")

**Architecture Approach:**
- Model: (e.g., Claude Sonnet 4.6) and why this tier
- Approach: (Prompting / RAG / Fine-tuning / Agent / Reasoning model) and why
- Latency target: (e.g., < 3 seconds end-to-end)
- Cost estimate: (e.g., ~$0.02 per interaction at expected volume)
- Special requirements: (e.g., structured output required; prompt caching enabled)

**Key Risks & Mitigations:**

| Risk | Impact | Mitigation |
|------|--------|-----------|
| Hallucination | Users get incorrect info; trust erodes | RAG + citations; human review for low-confidence outputs |
| Bias | Feature underperforms for some user groups | Pre-launch testing across diverse segments |
| Cost spiral | Margins impacted as usage grows | Prompt caching + cheapest suitable model; budget alerts |
| Latency | Users abandon feature | Cache frequent queries; use fast model tier for simple tasks |

**Success Metrics (Tier 1):**
- Accuracy: ≥ 85% of AI outputs rated 4+ / 5 by users
- Adoption: ≥ 50% of eligible users engage weekly within 60 days
- Time saved: ≥ 30 min/week per active user

**Acceptance Criteria:**

```
Given: A support request submitted by a user
When: The agent opens the AI suggestions panel
Then:
  - Response rendered within 3 seconds (p95)
  - Suggestion is relevant to the user's issue (rated ≥ 4/5)
  - Source citation included for every factual claim
  - Low-confidence suggestions flagged ("Review before sending")
  - Agent can edit, send, or dismiss
```

**Rollout Plan:**
- Week 1–2: Alpha with 10–20 internal testers
- Week 3–4: Beta with 5% of users; monitor Tier 2 health metrics
- Week 5–6: GA if all Tier 1 metrics hit threshold

---

### Example PRD (Filled In)

**Title:** AI Customer Support Assistant

**Problem Statement:**
Our support team handles 10,000 tickets/month, 40% of which are FAQ-level questions. Manual responses take 5–10 minutes each, driving average response time to 4+ hours. We're losing customers to competitors who respond in under 30 minutes. AI-suggested responses could cut resolution time by 80% for FAQ tickets.

**User Story:**
> As a support agent, I want the AI to suggest a response to common questions so I can review, edit, and send — instead of drafting from scratch.

**Goals:**
- Reduce average support response time from 4 hours to < 30 minutes for FAQ tickets
- Increase support agent capacity by 30% (same headcount, more tickets resolved)
- Achieve 85% user satisfaction rating on AI-assisted responses

**Non-Goals:**
- Fully automated support without human review
- Handling escalated, sensitive, or legal complaints
- Multi-language support (English only for V1)

**Architecture:**
- Model: Claude Sonnet 4.6 (~$3k/month at 100k suggestions/month)
- Approach: RAG (knowledge base + recent FAQs indexed nightly) + few-shot prompting for brand voice
- Latency: < 2 seconds for suggestion to appear in agent UI
- Cost per ticket: ~$0.03
- Prompt caching: Enabled for system prompt + policy documents (saves ~$800/month)
- Structured output: JSON response with `suggestion`, `source_doc`, `confidence_score`

**Key Risks:**

| Risk | Mitigation |
|------|-----------|
| AI hallucinates wrong policy | Index only verified docs; require citation; hide suggestions with confidence < 70% |
| Agents stop reviewing suggestions | Track edit rate; alert if drops below 20% (suggests blind trust) |
| Biased toward certain ticket types | Test on diverse ticket categories pre-launch; monthly segment audit |
| Nightly index misses same-day policy changes | Real-time override index for urgent policy updates |

**Metrics:**
- Accuracy: 85% of suggestions rated "good" or "excellent" by agents
- Adoption: 60% of agents use feature daily by Week 6
- Time saved: 3+ minutes per ticket → capacity for 4 extra tickets/day per agent

**Acceptance Criteria:**
```
Given: A support ticket about returns
When: Agent opens the AI suggestions panel
Then:
  - 1–3 suggested responses within 2 seconds
  - Each suggestion cites source doc (e.g., "Returns Policy v3.1, Section 2")
  - Confidence score shown (e.g., "91% confident")
  - Suggestions with < 70% confidence hidden by default
  - Agent can edit, approve, or dismiss
```

---

**Week 3 Deliverable: Your AI Feature PRD**

Write a 1-page PRD using the template above for your chosen use case. Use real estimates where you can; use "TBD" for unknowns and note what you'd need to find out.

---

**End of Week 3**

You now understand:
- How to assess AI feasibility before building
- How to measure AI feature success with real metrics
- How to identify and communicate risks
- How to write an AI Feature PRD

**Time Spent:** ~12–15 hours
**Total Curriculum:** ~40 hours over 3 weeks

---

## Final Glossary

For the full glossary with detailed explanations, see the [Syllabus](AI_PM_Curriculum_Syllabus.md). Below is a quick-reference table for the terms most relevant to product decisions.

| Term | One-Line Definition | When You Need It |
|------|---------------------|-----------------|
| **Token** | Smallest LLM unit (~4 chars) | Estimating cost and latency |
| **Context Window** | Max tokens the model processes at once | Planning RAG chunking; conversation history limits |
| **Hallucination** | Confident false output | Deciding if RAG + human review is needed |
| **RAG** | Feed model external docs before answering | Any task needing current or private data |
| **Fine-tuning** | Retraining model on your data | Only with 100+ examples and a stable, specific use case |
| **Agent** | LLM that picks tools and loops | Multi-step, conditional workflows |
| **Structured Output** | LLM returns JSON/structured data | When AI output feeds another system |
| **Prompt Caching** | Reuse processed prompt sections | Reducing cost on high-volume, large-prompt features |
| **Reasoning Model** | Model that thinks before answering | Complex analysis where quality > speed |
| **Inference** | Running the model (you pay per token) | Cost estimation and budgeting |
| **MCP** | Standard protocol for connecting LLMs to tools | Evaluating agent architecture decisions |

---

## Post-Curriculum Resources

After finishing this course, deepen your knowledge with:

**Books:**
- "Prompt Engineering Guide" (free, GitHub / promptingguide.ai) — hands-on prompting depth
- "Designing Machine Learning Systems" by Chip Huyen — systems thinking for production AI

**Courses (Self-Paced, Free):**
- DeepLearning.AI: "Building Systems with LLMs" (2 hours) — https://www.deeplearning.ai/short-courses/
- DeepLearning.AI: "Building & Evaluating Advanced RAG" (1.5 hours)

**Hands-On:**
- Build a simple RAG system with LangChain (official tutorial, 2–4 hours)
- Test Claude, GPT-4o, and Llama 3.3 on your own use case — compare outputs side by side
- Try the Anthropic cookbook: https://github.com/anthropics/anthropic-cookbook

**Stay Current:**
- Weekly: The Batch (DeepLearning.AI newsletter) — https://www.deeplearning.ai/the-batch/
- Monthly: Hugging Face papers digest — https://huggingface.co/papers
- Ongoing: Anthropic research blog — https://www.anthropic.com/research

---

## Your AI PM Toolkit

After this curriculum, you should feel confident:

✓ Reviewing an AI feature proposal from engineering — knowing what questions to ask
✓ Writing user stories and acceptance criteria for AI features
✓ Estimating cost, latency, and accuracy tradeoffs before committing to build
✓ Spotting hallucination, bias, privacy, and cost spiral risks early
✓ Communicating AI strategy and risk to executives, engineers, and customers
✓ Building a PRD for an AI-powered product
✓ Defining success metrics that tie AI quality to business outcomes
✓ Choosing between models, architectures, and approaches with confidence

---

## Feedback Loop

This curriculum is free and will evolve. If you:
- Find a resource that works better than what's listed
- Notice gaps in the content
- Have questions that aren't answered here

Share them. Good feedback makes this better for the next PM who reads it.

Good luck, and welcome to the AI PM community.
