# AI PM Quick Reference Guide

**Use this during meetings, when reviewing proposals, or when talking to engineers.** Bookmark it.

---

## The 3 Big Questions (Ask These First)

| Question | Why It Matters | Red Flags |
|----------|----------------|-----------|
| **What problem does this AI solve that can't be solved otherwise?** | If the answer is "just because AI sounds cool," stop. | "We want to add AI" with no problem defined |
| **Can we measure success?** | If you can't measure it, you can't improve it. | "AI quality is hard to measure" |
| **Is the ROI positive?** | Cost of building + running the AI must be less than the value it creates. | Cost per query > benefit per query |

---

## Model Decision Flowchart (In a Meeting)

```
"Which model should we use?"

Q1: Is this a complex reasoning task?
(math, legal analysis, multi-step logic, code audit)
├─ YES → Claude Opus 4.8 or OpenAI o3 (reasoning models)
└─ NO → Go to Q2

Q2: Is high-volume throughput or cost the top constraint?
├─ YES → Claude Haiku 4.5 or Gemini 2.0 Flash (fastest + cheapest)
└─ NO → Go to Q3

Q3: Is data privacy critical? (data can't leave your servers)
├─ YES → Llama 3.3 70B (self-hosted, open-source)
└─ NO → Go to Q4

Q4: Do you need > 200k token context?
(very long documents, large codebases)
├─ YES → Gemini 2.5 Pro (1M+ token context)
└─ NO → Claude Sonnet 4.6 (best all-rounder)
```

**Rules of Thumb:**
- **High volume / low cost:** Claude Haiku 4.5 or Gemini 2.0 Flash
- **Best all-rounder:** Claude Sonnet 4.6
- **Hardest tasks (quality over speed):** Claude Opus 4.8 or OpenAI o3
- **Very long documents:** Gemini 2.5 Pro
- **On-premise / private data:** Llama 3.3 70B (self-hosted)

> **Note:** Model pricing changes. Verify at anthropic.com/pricing, platform.openai.com/docs/models, and ai.google.dev before making budget decisions.

---

## Architecture Decision Flowchart (In a Meeting)

```
"How should we build this?"

Q1: Do you have 100+ labeled examples of the desired behavior?
├─ YES, and behavior is static → Fine-tune
└─ NO → Go to Q2

Q2: Does the task need current, external, or private data?
├─ YES → RAG (retrieve documents first, then generate)
└─ NO → Go to Q3

Q3: Is the task complex or multi-step?
(requires reasoning, conditional logic, multiple tools)
├─ YES → Agent (with MCP tools) or Reasoning model
└─ NO → Go to Q4

Q4: Can you solve it with clear instructions and a few examples?
├─ YES → Few-shot prompting (cheapest, fastest)
└─ NO → Combine: RAG + prompting, or Agent + prompting
```

**Architecture Decision Matrix:**

| Approach | Cost | Time to Build | Best For |
|----------|------|---------------|----------|
| **Zero-shot Prompting** | ~$0 | Hours | Simple tasks, fast iteration |
| **Few-shot Prompting** | ~$0 | Hours | Format/style control without retraining |
| **RAG** | $100–1k/mo infra | Days | Factual tasks, external/private data |
| **Fine-tuning** | $1k–100k training | Days–Weeks | Domain-specific format; 100+ labeled examples |
| **Agents** | $100–1k/mo infra | Days | Multi-step, conditional, tool-using workflows |
| **Reasoning Models** | 5–10x per query | Hours (config) | Complex analysis where quality > speed |
| **Prompt Caching** | Saves 80–90% on repeated prompts | Hours (config) | High-volume features with large system prompts |
| **Structured Outputs** | ~$0 | Hours (schema design) | When AI output feeds into another system |

---

## Risk Checklist (Before Launching)

- [ ] **Hallucination Risk:** Can the feature tolerate false information? If not, use RAG + source citations + human review.
- [ ] **Bias Risk:** Have you tested the model's performance across different user segments (languages, demographics, use cases)? It may perform worse for underrepresented groups.
- [ ] **Cost Risk:** Have you modeled cost at 10x current volume? Is a budget alert in place?
- [ ] **Latency Risk:** Have you measured p95 latency under load? Will users accept it?
- [ ] **Data Privacy Risk:** Are you sending sensitive user data to a 3rd-party API? Have you reviewed the provider's data retention terms?
- [ ] **Overtrust Risk:** Will users stop verifying AI output and blindly act on it? If so, design for review (confidence scores, citations, override tracking).
- [ ] **Model Degradation Risk:** Will accuracy decline over time as your data or the world changes? Plan a retraining/refresh schedule.

---

## Metrics Cheat Sheet

**Pick 1–2 Primary Metrics (Your North Star)**

| Use Case | Primary Metric | Target |
|----------|----------------|--------|
| Customer support chatbot | % of AI suggestions rated "good" or better | ≥ 85% |
| Code review assistant | False positive rate (bugs flagged that aren't real) | < 5% |
| Document summarizer | User satisfaction (CSAT or thumbs up/down) | > 4/5 |
| Recommendation engine | Click-through rate vs. baseline | +10% vs. control |
| Meeting notes | Time saved per user per week | ≥ 30 min |
| Classification feature | Accuracy vs. human baseline | ≥ 90% |

**Tier 2 Health Metrics (Monitor Weekly)**

| Metric | Red Flag | Action |
|--------|----------|--------|
| Latency (p95) | > 5 seconds | Optimize retrieval, faster model, add caching |
| Cost per query | Rising week-over-week | Enable prompt caching, optimize prompts, route to cheaper model |
| Hallucination rate | > 10% of sampled outputs wrong | Add/improve RAG, lower temperature, require citations |
| User complaint rate | > 5% negative feedback | Investigate error type; consider rollback |
| Model accuracy | Declining month-over-month | Refresh RAG index, update system prompt, evaluate new model |

---

## Glossary (One-Liners)

| Term | Definition | PM Implication |
|------|------------|----------------|
| **Token** | Atomic unit; ~4 chars = 1 token | Costs $, limits context, affects latency |
| **Context Window** | Max tokens the model can process (200k for Claude Sonnet/Opus 4.x) | Determines how much doc/history fits |
| **Hallucination** | Confident false output | Major risk for factual tasks; mitigate with RAG + citations |
| **Temperature** | Randomness dial (0 = deterministic, 1 = creative) | 0 for factual tasks; 0.7–1 for creative |
| **Prompt Engineering** | Writing queries to get better outputs | No cost; high ROI; start here before anything else |
| **Few-Shot** | Including examples in the prompt | Better quality than zero-shot; no retraining |
| **RAG** | Feed model external documents before answering | Reduces hallucinations; requires index infrastructure |
| **Fine-Tuning** | Retraining model on your data | Expensive ($1k–100k); only if 100+ examples and static use case |
| **Structured Output** | LLM returns JSON/structured data | Required when output feeds another system |
| **Prompt Caching** | Reuse processed prompt sections across calls | 80–90% cost savings on high-volume features with large prompts |
| **Reasoning Model** | Model that thinks before answering (o1, o3, Opus extended thinking) | For complex tasks; slow + expensive; not for real-time chat |
| **Agent** | LLM that picks tools and loops until done | Multi-step workflows; adds latency |
| **MCP** | Standard protocol for connecting LLMs to tools | Reduces custom integration work in agent architectures |
| **Embedding** | Text converted to numbers for similarity search | Powers RAG retrieval |
| **Inference** | Running the model (user-facing) | You pay per token for this |
| **Training** | Building the model (done by provider) | Don't do this unless you have to |

---

## Answering Common Questions in Meetings

**Q: "Why is this hallucinating?"**
A: "The model predicts the next token based on patterns, not actual facts. Without grounding it with external data (RAG), it can confidently output false information. We need to: (1) add RAG with source citations, (2) add a human review step for high-stakes outputs, or (3) reduce the stakes of the task."

**Q: "Can we just fine-tune to fix this?"**
A: "Only if we have 100+ high-quality labeled examples of the correct behavior. With fewer than 50, few-shot prompting is faster and cheaper. If the data changes frequently, fine-tuning will go stale — RAG is better."

**Q: "Will this cost too much?"**
A: "At [X] queries/month with [model], cost is $[Y]/month. That's ROI-positive if each query saves > $[Y/queries] in time or errors. Here's the math: [show calculation]. We can also enable prompt caching to cut costs by ~80%."

**Q: "Why is the response slow?"**
A: "Current breakdown: ~300ms retrieval + ~2s model inference + ~200ms API overhead = ~2.5s total. We can optimize by: (1) enabling prompt caching, (2) caching frequent retrieval results, (3) switching to a faster model tier for simple queries."

**Q: "Should we use a reasoning model for this?"**
A: "Depends on the task. Reasoning models (o3, Opus extended thinking) are 5–10x more expensive and take 5–30 seconds to respond. They're worth it for complex analysis where quality is paramount. For real-time chat or simple tasks, a standard model is better."

**Q: "What if the model changes (provider releases a new version)?"**
A: "We evaluate new models quarterly on our accuracy benchmark. Switching is straightforward if our integration is abstracted — typically a 1-day migration. We should always test a new model version on our evaluation dataset before rolling it out."

**Q: "Can it make decisions, or just suggestions?"**
A: "It can suggest with confidence levels, but should not make irreversible decisions without human review. The right threshold depends on the stakes. Low-stakes (copywriting, categorization): AI can decide. High-stakes (medical, legal, financial): AI suggests, human decides."

---

## Red Flags (When to Pump the Brakes)

| Red Flag | What It Means | What to Do |
|----------|---------------|------------|
| "Hard to measure AI quality" | You can't define success | Pause. Define 1 measurable metric. Then build. |
| "The AI sometimes hallucinates" + "This is high-stakes" | Liability or trust risk | Add human review, RAG + citations, or reduce the task scope |
| "Token costs are spiraling" | Unit economics don't work | Enable prompt caching; route easy queries to cheaper models; audit prompt length |
| "Engineers want to fine-tune immediately" | Premature complexity and cost | Start with prompting. Fine-tune only if prompting demonstrably fails. |
| "Users are frustrated by slowness" | Latency killing UX | Profile where time is spent; optimize top bottleneck first |
| "We're adding AI for AI's sake" | No real problem being solved | Go back to the 3 Big Questions |
| "Accuracy dropped this week for no reason" | Data drift, index staleness, or model provider change | Investigate; check if RAG index is stale; check provider change logs |
| "Engineering wants to use o3 for the chat feature" | Reasoning models for real-time chat = bad UX | Flag latency: 5–30s wait is unacceptable for chat. Use Sonnet or GPT-4o instead. |

---

## Conversation Starters (With Your Team)

**With Engineering:**
> "Before we finalize the architecture, can we walk through the decision tree? I want to make sure we've considered prompting before committing to fine-tuning, and that we've evaluated whether prompt caching makes the economics work at scale."

**With Product:**
> "I want to make sure we're solving a real problem. What would users do today without this AI feature? How much time does it cost them? That defines our value threshold."

**With Data:**
> "For RAG to work, we need our knowledge base indexed and updated on a schedule. What's the freshness requirement — daily? Real-time? And who owns that pipeline?"

**With Leadership:**
> "We're investing $X/month in this AI feature. At our scale, that's $Y per user per month. With prompt caching enabled, we can cut that to $Z. We expect payback in [W weeks] through [metric]. Here's the sensitivity: if accuracy drops to 70%, the ROI drops to [X]."

---

## Template: Quick AI Feature Decision Memo

One page. Use for proposals, reviews, or green-light decisions.

---

**Feature:** [Name]

**Problem:**
[1 sentence: What user problem does this solve? What's the current cost of not solving it?]

**Approach:**
- Model: [Claude Sonnet 4.6 / GPT-4o / Llama 3.3 / etc.] and why this tier
- Architecture: [Prompting / RAG / Fine-tuning / Agent / Reasoning model]
- Special: [Structured output? Prompt caching? Yes/No and why]
- Why this approach: [2 sentences]

**Feasibility:**
- Can we build this? [Yes/No/Partial + key constraint]
- Do we have the data? [Yes/No/What's missing]
- Latency target: [< X seconds at p95]
- Cost estimate: [$X/month at Y queries/month; per-query cost = $Z]

**Top Risk + Mitigation:**
[1 risk that could kill this feature + how you'd handle it]

**Success Metric:**
[1 primary metric + target threshold]

**Recommendation:**
[Build / Don't build / Build with conditions: what must be true first]

---

**Example:**

**Feature:** AI Customer Support Copilot

**Problem:**
Support team spends 4+ hours responding to FAQs; response time > 4 hours is losing customers to faster competitors.

**Approach:**
- Model: Claude Sonnet 4.6 (reasoning quality + 200k context for full KB)
- Architecture: RAG (knowledge base + FAQ index, refreshed nightly)
- Special: Structured output (JSON: suggestion + source_doc + confidence); Prompt caching for system prompt (saves ~$800/month)
- Why: Claude's instruction-following handles edge cases well; RAG ensures accuracy without fine-tuning; structured output feeds our agent UI reliably

**Feasibility:**
- Can we build this? Yes (RAG is standard; infra team has Pinecone already)
- Do we have the data? Yes (300KB of KB articles + 6 months of resolved tickets)
- Latency target: < 2 seconds
- Cost estimate: ~$3k/month at 100k suggestions/month ($0.03/suggestion)

**Top Risk + Mitigation:**
Hallucination on new topics not yet in KB → Confidence threshold: hide suggestions < 70% confidence; require agent review for all AI suggestions before sending

**Success Metric:**
85% of AI suggestions rated "good" or "excellent" by support agents within 30 days of launch

**Recommendation:**
Build. ROI is 3x in month 1 if accuracy target is met. Alpha with 10 internal agents for 2 weeks; gate to Beta only if ≥ 85% satisfaction.

---

## Weekly AI Feature Health Check

Every week, ask:

- [ ] **Accuracy:** Did our AI quality metric hit target?
- [ ] **Cost:** Did we stay within budget? Is cost/query trending up?
- [ ] **Latency:** Are responses within SLA at p95?
- [ ] **User Feedback:** Any unusual complaint patterns?
- [ ] **Index Freshness:** Is our RAG index up to date?
- [ ] **Model Drift:** Has accuracy changed vs. last month's baseline?

If any is "No" or "Unknown," investigate before shipping new features.

---

## Further Reading

- **Evaluation frameworks:** RAGAS for RAG quality — https://github.com/explodinggradients/ragas
- **Safety & bias:** NIST AI Risk Management Framework — https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf
- **Prompting techniques:** Prompting Guide — https://www.promptingguide.ai/
- **Production AI systems:** Chip Huyen's blog — https://huyenchip.com/
- **Anthropic cookbook (code examples):** https://github.com/anthropics/anthropic-cookbook

---

## One Last Thing

**Before you launch any AI feature, answer these four questions:**

1. Does it solve a real, measurable problem?
2. Can we measure success with a specific metric and target?
3. Is the ROI positive at expected volume?
4. Have we identified and mitigated the top 3 risks?

If yes to all four: build it.
If no to any: go back and fix that answer first.

Good luck.
