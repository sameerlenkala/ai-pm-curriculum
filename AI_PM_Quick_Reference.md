# AI PM Quick Reference Guide

**Use this during meetings, when reviewing proposals, or when talking to engineers.** Bookmark it.

---

## The 3 Big Questions (Ask These First)

| Question | Why It Matters | Red Flags |
|----------|---|---|
| **What problem does this AI solve that can't be solved otherwise?** | If the answer is "just because AI sounds cool," stop. | "We want to add AI" (no problem defined) |
| **Can we measure success?** | If you can't measure it, you can't improve it. | "Hard to measure AI quality" |
| **Is the ROI positive?** | Cost of building + running the AI vs. benefit to users/business. | Cost per query > benefit |

---

## Model Decision Flowchart (In a Meeting)

```
"Which model should we use?"

Q1: Do we need sub-second latency (realtime chat)?
├─ YES → Use GPT-4o or Gemini 2.0 (fastest)
└─ NO → Go to Q2

Q2: Is cost critical (<$1k/month budget)?
├─ YES → Use Llama 2 (self-hosted) or Mixtral
└─ NO → Go to Q3

Q3: Do we need long context (>100k tokens) or high safety?
├─ YES, long context → Gemini 2.0
├─ YES, high safety → Claude 3.5 Sonnet
└─ BALANCED → Claude 3.5 Sonnet
```

**Rule of Thumb:**
- **Fast & general:** GPT-4o
- **Best reasoning & safety:** Claude 3.5 Sonnet
- **Cheap:** Llama 2 (self-hosted)
- **Long docs:** Gemini 2.0

---

## Architecture Decision Flowchart (In a Meeting)

```
"Should we fine-tune, prompt, or use RAG?"

Q1: Do you have 100+ labeled examples?
├─ YES → Can fine-tune
└─ NO → Go to Q2

Q2: Does the task need recent/external data?
├─ YES → Use RAG (retrieve documents first)
└─ NO → Go to Q3

Q3: Can you solve it with prompting + few examples?
├─ YES → Just prompt (cheapest, fastest)
└─ NO → Combine approaches (RAG + fine-tuning)
```

**Decision Matrix:**

| Approach | Cost | Time to Build | Quality | When to Use |
|----------|------|---|---|---|
| **Prompting** | $0 | Hours | Good | Simple tasks, fast iteration |
| **Few-shot Prompting** | $0 | Hours | Good | Need style/format control |
| **RAG** | $100–1k/mo | Days | Best | Factual tasks, external data |
| **Fine-tuning** | $1k–100k | Days–Weeks | Best | Need domain-specific behavior |
| **Agents** | $100–1k/mo | Days | Good | Multi-step workflows |

---

## Risk Checklist (Before Launching)

- [ ] **Hallucination Risk:** Does the task tolerate false info? If not, use RAG + human review.
- [ ] **Bias Risk:** Does the model perform equally for all user segments? Test on diverse data.
- [ ] **Cost Risk:** At scale, will token costs spiral? Set a budget alert.
- [ ] **Latency Risk:** Will users accept the response time? Measure and set SLA.
- [ ] **Data Privacy Risk:** Are we sending sensitive data to 3rd-party APIs? Check terms.
- [ ] **Model Degradation:** Will accuracy decline over time? Plan retraining schedule.

---

## Metrics Cheat Sheet

**Pick 1–2 Primary Metrics (That Determine Success)**

| Use Case | Primary Metric | Target |
|----------|---|---|
| Customer support chatbot | Accuracy (% of responses rated ≥4/5) | 85%+ |
| Code review assistant | False positive rate (bugs suggested but don't exist) | <5% |
| Content summarizer | ROUGE score (similarity to human summary) | >0.40 |
| Recommendation engine | Click-through rate (% of recommendations clicked) | +10% vs. baseline |
| Meeting notes | User satisfaction (NPS or CSAT) | >4/5 |

**Tier 2 (Monitor Weekly)**

| Metric | Red Flag | Action |
|--------|----------|--------|
| Latency | >5 seconds | Optimize prompts, use faster model, add caching |
| Token cost | Rising week-over-week | Review usage, optimize prompts, batch process |
| Hallucination rate | >10% of outputs false | Add RAG, reduce temperature, add verification step |
| User complaints | >5% negative feedback | Investigate type of error; consider rollback |

---

## Glossary (One-Liners)

| Term | Definition | Implication |
|------|---|---|
| **Token** | Atomic unit; ~4 chars = 1 token | Costs $, limits context, affects latency |
| **Context Window** | Max tokens the model can process (e.g., 200k) | Determines how much doc/history fits |
| **Hallucination** | Confident false output | Risk for factual tasks; mitigate with RAG |
| **Temperature** | Randomness (0=deterministic, 1=creative) | 0 for factual, 0.7–1 for creative |
| **Prompt Engineering** | Writing queries to get better outputs | No cost; high ROI |
| **Few-Shot** | Showing examples in the prompt | Better quality than zero-shot; no retraining |
| **RAG** | Feed model external documents before answering | Reduces hallucinations; adds retrieval latency |
| **Fine-Tuning** | Retraining model on your data | Expensive ($1k–100k); only if 100+ examples |
| **Embedding** | Text converted to numbers for similarity search | Enables semantic search (RAG) |
| **Agent** | LLM that picks tools and loops | Multi-step workflows; adds latency |
| **Inference** | Running the model (user-facing) | Pay per token for this |
| **Training** | Building the model (done by vendor) | Don't do this unless you have to |

---

## Answering Common Questions in Meetings

**Q: "Why is this hallucinating?"**
A: "The model is predicting the next token based on patterns, not retrieving facts. Without external data (RAG), it can confidently output false info. We need to: (1) ground it with RAG, (2) add human review, or (3) lower stakes of the task."

**Q: "Can we just fine-tune to fix this?"**
A: "Only if we have 100+ examples of the behavior we want. If we have <50 examples, few-shot prompting is cheaper and faster. If the data changes often, RAG is better than fine-tuning."

**Q: "Will this cost us too much?"**
A: "At [X] queries/month with [model], cost is $[Y]/month. ROI is positive if each query saves >$[Y/queries] in time or errors. Here's the math: [show calculation]."

**Q: "Why is the response slow?"**
A: "We're adding 500ms for retrieval (searching documents) + 2s for model thinking + 500ms for APIs. Total ~3s. We can optimize by: (1) faster vector DB, (2) fewer document chunks, or (3) use a faster model."

**Q: "Can it make decisions or just suggest?"**
A: "It can suggest with high confidence, but shouldn't make decisions without human review. Risk level depends on task. For low-stakes (copywriting): AI decides. For high-stakes (medical): AI suggests, human decides."

**Q: "What if the model changes (e.g., OpenAI releases a new model)?"**
A: "We evaluate new models quarterly on our metrics. Switch if ROI improves (faster, cheaper, better quality). Our code is abstracted so switching is easy (1–2 day migration)."

**Q: "How do we know if it's actually working?"**
A: "We measure [metric] weekly. If it stays above [threshold], it's working. If it drops, we investigate root cause and iterate. Here's the baseline: [show current performance]."

---

## Red Flags (When to Pump the Brakes)

| Red Flag | What It Means | What to Do |
|----------|---|---|
| "Hard to measure AI quality" | You can't define success | Pause. Define 1 metric. Then build. |
| "The AI sometimes hallucinates" + "This is high-stakes" | Liability risk | Add human review, use RAG, lower stakes, or don't use AI |
| "Token costs are spiraling" | Economics don't work | Optimize prompts, reduce queries, use cheaper model |
| "Engineers want to fine-tune immediately" | Premature complexity | Start with prompting. Only fine-tune if it fails. |
| "Users are frustrated by slowness" | Latency kills UX | Reduce retrieval time, use faster model, cache results |
| "We're building AI for AI's sake" | No real problem | Stop. Go back to the 3 Big Questions. |
| "Model accuracy dropped this week for no reason" | Data drift or model degradation | Investigate; plan retraining or index update |

---

## Conversation Starters (To Use with Your Team)

**With Engineering:**
> "Let's think through our approach. We have 50 examples of the format we want. Should we fine-tune or use few-shot prompting? What are the tradeoffs?"

**With Product:**
> "I want to make sure we're solving a real problem here. What would users do today without AI? And how much time would this save them?"

**With Data:**
> "For RAG to work, we need documents indexed by [date]. Can we update the index daily? What's the cost of frequent indexing?"

**With Leadership:**
> "We're investing $X/month in this AI feature. At our scale, that's $Y per user per month. We expect it to pay back in [Z weeks] through [metric]. Here's the sensitivity analysis: [show if metric changes by ±10%]."

---

## Template: Quick AI Feature Decision Memo

Use this 1-pager to propose/evaluate an AI feature.

---

**Feature:** [Name]

**Problem:** 
[1 sentence: What user problem does this solve?]

**Approach:**
- Model: [Claude 3.5 Sonnet / GPT-4o / Llama / etc.]
- Architecture: [Prompting / RAG / Fine-tuning / Agents]
- Why: [2 sentences explaining the choice]

**Feasibility:**
- Can we build this? [Yes/No + why]
- Do we have the data? [Yes/No/Partial]
- Cost estimate: [$X/month at Y scale]

**Key Risk:**
[1 risk + mitigation]

**Success Metric:**
[1 metric + target]

**Recommendation:**
[Build / Don't build / Build with conditions]

---

**Example:**

**Feature:** AI Customer Support Copilot

**Problem:** 
Support team spends 4 hours answering FAQs; response time is too slow.

**Approach:**
- Model: Claude 3.5 Sonnet
- Architecture: RAG (index knowledge base + recent FAQs)
- Why: Claude's reasoning handles edge cases; RAG ensures accuracy without hallucination

**Feasibility:**
- Can we build this? Yes (RAG is standard pattern)
- Do we have the data? Yes (300 KB of KB articles + 50 recent FAQs)
- Cost estimate: $3k/month at 100k tickets/month

**Key Risk:**
Hallucination on new topics not in KB → Mitigate with low confidence threshold + require agent review

**Success Metric:**
85% of suggestions rated "good" or "excellent" by agents

**Recommendation:**
Build. ROI is 3x in month 1 if we hit 85% quality. Plan 4-week alpha/beta before GA.

---

## Weekly Check-In Template (For Your Backlog)

Every Friday, ask:

- [ ] **Accuracy:** Did our AI metric hit target this week?
- [ ] **Cost:** Did we stay under budget?
- [ ] **Latency:** Are responses within SLA?
- [ ] **User Feedback:** Any complaints or issues?
- [ ] **Model Quality:** Did accuracy drift or stay stable?

If any answer is "No," investigate and flag blocker.

---

## Further Reading (When You Need Depth)

- **Cost optimization:** [Hyperplane blog on LLM costs](https://www.hyperplane.dev)
- **Evaluation frameworks:** [RAGAS GitHub](https://github.com/explodinggradients/ragas)
- **Safety/bias:** [NIST AI Risk Framework](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf)
- **Architecture patterns:** [Patterns for AI Engineering (free book)](https://www.patterns.dev)

---

## One Last Thing

**Before you launch any AI feature, ask:**

1. Does it solve a real problem?
2. Can we measure success?
3. Is the ROI positive?
4. Have we identified and mitigated the top 3 risks?

If yes to all four, build it. If no to any, iterate until you can say yes.

Good luck.

