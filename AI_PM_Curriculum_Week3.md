# WEEK 3: AI PRODUCT STRATEGY, METRICS & LAUNCH

## Unit 7: AI Product Strategy — Feasibility, User Value, GTM

### The AI Product Lens

Most AI products fail not because the AI is bad, but because:
1. Users don't care (feature solves no real problem)
2. You can't measure value (is the AI actually helping?)
3. Cost/latency kills the experience (model is too slow or expensive)
4. Edge cases break trust (hallucination on important task)

### Feasibility Assessment Framework

Before building, ask:

**Q1: Is the Task Solvable by AI?**

| Task | Feasible? | Why |
|------|-----------|-----|
| Summarize a document | ✓ Yes | Clear input/output |
| Recommend a product | ~ Maybe | Depends on data quality |
| Diagnose a disease | ✗ No | Hallucination risk too high; liability |
| Classify customer feedback | ✓ Yes | Clear categories |
| Generate legal documents | ✗ No | Liability; needs legal review |
| Write product descriptions | ✓ Yes | Easy to review, iterate |

**Red Flags:**
- Task requires 100% accuracy (medical, legal, financial)
- No ground truth to evaluate against
- User harm if wrong (safety-critical)
- Task is inherently ambiguous

**Green Lights:**
- Task is currently manual/slow
- Output can be reviewed quickly
- Mistakes are recoverable
- Clear metrics for "good"

---

**Q2: Do You Have the Data?**

**For RAG:** Do you have documents or databases to ground the model?
- ✓ Yes, indexed daily → Good
- ~ Some, but incomplete → Risky
- ✗ No, or outdated → Don't do RAG

**For Fine-tuning:** Do you have 100+ labeled examples?
- ✓ Yes → Can fine-tune
- ~ 10–50 examples → Prompting instead
- ✗ <10 examples → Start with base model

**For Agents:** Do you have APIs/tools to call?
- ✓ Yes → Good
- ✗ No → Can't use agents

---

**Q3: Economics — Cost/Benefit?**

**Cost Structure:**
- LLM inference: $0.001–$0.05 per query (depends on model)
- Retrieval: $0.0001–$0.001 per query (vector DB)
- Latency cost: Every 500ms of wait time = ~3% fewer users
- Infrastructure: $100–1000/month for RAG setup

**Benefit:**
- Time saved per user (hours/week)
- Error reduction (fewer support tickets)
- Revenue uplift (better customer satisfaction)
- Cost savings (replacing headcount)

**Breakeven Calculation:**
```
Cost per query = $0.01
Queries per month = 100,000
Total monthly cost = $1,000

Benefit per query = Averages to $0.05 (time saved, error reduction)
Total monthly benefit = $5,000

Margin = $4,000/month
ROI = 4x in first month

✓ Build it
```

```
Cost per query = $0.05
Queries per month = 100,000
Total monthly cost = $5,000

Benefit per query = $0.03 (minor time savings)
Total monthly benefit = $3,000

Margin = -$2,000/month
ROI = Negative

✗ Don't build it; improve the problem differently
```

---

### User Value: The Jobs-to-Be-Done Framework

Don't ask users "Do you want AI?" Ask what problem they're solving.

**Bad Framing:**
> "We're adding AI to summarize your documents."

**Good Framing:**
> "Today, you spend 2 hours a week reading meeting notes. We can auto-summarize so you get the key points in 2 minutes."

**User Value Checklist:**
- [ ] Does the AI make an existing task faster?
- [ ] Does it reduce errors?
- [ ] Does it enable new capabilities?
- [ ] Can the user understand/verify the output?
- [ ] Is latency acceptable? (<2 seconds for chat, <10s for batch)
- [ ] Is the cost justified?

### Go-to-Market Strategy for AI Features

**Phase 1: Validation (1–2 weeks)**
- Build MVP with your chosen model (Claude, GPT-4, etc.)
- Test with 10–20 power users internally
- Measure: Accuracy, latency, cost per query
- Gate: "Is this actually useful?" If no, pivot.

**Phase 2: Alpha (2–4 weeks)**
- Roll out to 1% of users or a cohort
- Monitor: Accuracy, latency, cost, user satisfaction
- Collect feedback on edge cases
- Gate: "Are users happy?" If yes, expand.

**Phase 3: Beta (4–8 weeks)**
- 10–30% of users
- A/B test: AI-assisted vs. manual baseline
- Measure ROI: Time saved, error reduction, NPS
- Gate: "Is ROI positive?" If yes, full launch.

**Phase 4: General Availability**
- Roll out to 100%
- Monitor model performance (drift)
- Plan updates (new model, retrain)

---

## Unit 8: Metrics, Evaluation & Risk Management for AI Features

### Success Metrics Framework

**Tier 1: Core Metrics (What Matters Most)**

*Choose 1–2 per product.*

| Metric | Example | How to Measure |
|--------|---------|-----------------|
| **Accuracy** | "80% of AI summaries match human summaries" | Sample outputs, manual review |
| **User Satisfaction** | "Users rate AI responses 4.5/5" | Post-interaction survey |
| **Time Saved** | "AI saves 30 min/week per user" | User tracking, time logs |
| **Error Rate Reduction** | "AI classification errors down 40%" | Compare AI vs. human on test set |
| **Adoption** | "50% of eligible users use the feature" | Feature flag tracking |

---

**Tier 2: Health Metrics (Monitor Continuously)**

| Metric | Red Flag | Action |
|--------|----------|--------|
| **Latency** | >5 seconds | Optimize retrieval, use faster model |
| **Hallucination Rate** | >10% of outputs wrong | Add RAG, lower temperature, add verification |
| **Cost Per Query** | Rising week-over-week | Optimize prompts, batch process, use cheaper model |
| **User Complaints** | >5% of feedback negative | Investigate root cause (accuracy? speed? UX?) |
| **Model Drift** | Accuracy declining over time | Retrain, update index, gather new data |

---

### Evaluation: How to Actually Measure Quality

**Gold Standard: Human Evaluation**
- Have humans rate 100–200 AI outputs on a scale (1–5)
- Calculate: Accuracy (% rated ≥4), F1 score, precision, recall
- Cost: 5–10 hours for 200 samples
- Frequency: Weekly for first month, then monthly

**Fast: Automated Metrics**
- BLEU score (for summarization/translation)
- Exact match (for Q&A with known answers)
- Cost: ~$0
- Warning: May not correlate with user satisfaction

**Hybrid: Spot-Check + Aggregate**
- Automated check on 1000 queries
- Manual review of flagged/suspicious ones
- Cost: Moderate
- Frequency: Weekly

**Process:**
```
1. Pick a metric (e.g., "Summarization quality: ≥4/5 rating")
2. Run a batch of 100 queries through the AI
3. Have 2–3 humans rate outputs (blind to AI vs. baseline)
4. Calculate % that meet the threshold
5. If <80%, investigate and iterate
```

---

### Red Flags & Risk Management

**Risk 1: Hallucination on High-Stakes Tasks**

| Risk | Detection | Mitigation |
|------|-----------|-----------|
| AI invents facts (diagnosis, legal advice) | Manual review of sample outputs | Require human review before action, add citations, use RAG |
| Users trust AI too much | Survey users; track override rate | Clearly label "AI suggestions," show confidence scores |

---

**Risk 2: Bias & Fairness**

| Risk | Detection | Mitigation |
|------|-----------|-----------|
| Model performs worse for certain groups (e.g., accents, demographics) | Test on diverse data; track performance by segment | Retrain on balanced data, add bias audits pre-launch |
| Recommendations favor certain outcomes unfairly | A/B test AI recommendation vs. control | Publish recommendation criteria, allow user override |

---

**Risk 3: Data Privacy & Security**

| Risk | Detection | Mitigation |
|------|-----------|-----------|
| Sensitive user data sent to 3rd-party LLM API | Audit data flow; ask vendor about retention | Use on-premise models, encrypt in transit, request no-logging agreements |
| Model trained on user data without consent | Read terms of service | Use APIs with explicit data privacy (Anthropic, OpenAI private endpoints) |

---

**Risk 4: Cost Spiral**

| Risk | Detection | Mitigation |
|------|-----------|-----------|
| Token costs grow as usage scales | Track $ per query monthly | Set budget alerts, optimize prompts, batch process, use cheaper model |
| Retrieval adds up (vector DB, embeddings) | Monitor vector DB row count and queries | Index only essential docs, cache embeddings, use cheaper embedding model |

---

**Risk 5: Model Degradation Over Time**

| Risk | Detection | Mitigation |
|------|-----------|-----------|
| Accuracy declines after 3 months | Weekly spot-check of outputs | Retrain monthly, update docs, monitor for data drift |

---

### Communicating AI Risk to Stakeholders

**To Execs (Cost/ROI):**
> "We'll launch the AI feature to 5% of users first (lower risk). Expected ROI is 3x if we hit 85% accuracy. We'll measure this weekly and pause if accuracy drops below 80%."

**To Engineering (Technical Risk):**
> "The top risks are hallucination (mitigated by RAG) and latency (we've modeled <2s baseline). We'll monitor both in staging and have a rollback plan."

**To Customers (Trust):**
> "Our AI-assisted feature is designed to help, not replace, human judgment. We show you the sources for all recommendations so you can verify."

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

**PRD Template (Use This Structure):**

---

### AI Feature PRD Template

**Title:** [Feature Name]

**Problem Statement:**
- What problem does this solve? (1–2 sentences)
- Why now? (What's changed?)
- Business impact if solved (time/cost/revenue)

**User Story:**
- As a [user role], I want [capability], so that [benefit]

**Goals:**
- Primary goal: (e.g., "Reduce support response time by 50%")
- Success metric: (e.g., "Avg response time <2 hours")

**Non-Goals:**
- What are we NOT doing? (e.g., "Not replacing human agents")

**Architecture Approach:**
- Model choice: (Claude 3.5 Sonnet) and why
- Approach: (Prompting / RAG / Fine-tuning / Agent) and why
- Latency target: (e.g., <3 seconds)
- Cost estimate: (e.g., $0.02 per interaction)

**Key Risks & Mitigations:**

| Risk | Impact | Mitigation |
|------|--------|-----------|
| Hallucination | Users get wrong info | RAG + human review |
| Bias | Feature performs worse for some groups | Test on diverse data |
| Cost | Margins hurt if too expensive | Optimize prompts, cap usage |

**Success Metrics (Tier 1):**
- Accuracy: 85% of AI outputs rated ≥4/5
- Adoption: 50% of users engage
- Time saved: 30 min/week per user

**Acceptance Criteria (User-Facing):**

Given a support request in English
When the AI generates a response
Then it should:
- Return within 3 seconds
- Be relevant to the issue (rated 4+/5)
- Include source citations
- Flag uncertainty ("I'm not sure, please escalate")

**Rollout Plan:**
- Week 1–2: Alpha with 10 internal testers
- Week 3–4: Beta with 5% of users
- Week 5–6: GA if metrics hit thresholds

---

### Example PRD (Filled In)

**Title:** AI Customer Support Assistant

**Problem Statement:**
Support team is overwhelmed with FAQs (40% of tickets). Manual responses take 5–10 min each. This delays response time to 4+ hours. We're losing customers to competitors with faster support.

**User Story:**
As a support agent, I want the AI to suggest responses to common questions, so that I can respond faster and handle more tickets.

**Goals:**
- Reduce avg support response time from 4 hours to <30 min
- Increase support agent capacity by 25% (same headcount, more tickets)
- Hit 85% user satisfaction on AI responses

**Non-Goals:**
- Fully automated support (humans still review/send)
- Handling sensitive/escalated issues

**Architecture:**
- Model: Claude 3.5 Sonnet ($3k/month at 100k tickets/month)
- Approach: RAG (index knowledge base + recent FAQs)
- Latency: <2 seconds (agent waits for suggestions)
- Cost/ticket: $0.03

**Key Risks:**

| Risk | Mitigation |
|------|-----------|
| AI hallucinates wrong policies | Index only verified docs, require agent review |
| Takes support agent time to review | Show confidence score, hide low-confidence (<70%) |
| Biased towards certain customer segments | Test on diverse ticket types |

**Metrics:**
- Accuracy: 85% of suggestions rated "good/excellent"
- Adoption: 60% of agents use feature daily
- Time saved: 3 min per ticket → 4 extra tickets/day per agent

**Acceptance Criteria:**

Given a support ticket from a user asking about returns
When the agent opens the AI suggestions panel
Then the system should:
- Display 2–3 suggested responses within 2 seconds
- Cite the source document (e.g., "From Returns Policy v2.1")
- Show confidence score (e.g., "92% confident")
- Allow agent to edit and send, or dismiss

---

**Week 3 Deliverable: Your AI Feature PRD**

**Submit:** 1-page PRD using the template above for your chosen use case.

---

**End of Week 3**

You now understand:
- How to assess AI feasibility
- How to measure AI feature success
- How to identify and mitigate risks
- How to write an AI feature PRD

**Time Spent:** ~12–15 hours
**Total Curriculum:** ~40 hours over 3 weeks

---

## Final Glossary: Terms You'll Need to Know

| Term | Definition | PM Implication |
|------|-----------|-----------------|
| **Token** | Smallest unit LLM processes (~4 chars) | Charged per token; limits context size |
| **Context Window** | Max tokens LLM can process at once | Affects cost, latency, ability to handle long docs |
| **Prompt Engineering** | Writing/structuring queries for better outputs | Skill you can develop; no cost |
| **Temperature** | Randomness in LLM outputs (0 = deterministic) | 0 for factual tasks, 0.7+ for creative |
| **Hallucination** | LLM confidently making up false info | Major risk; mitigate with RAG + review |
| **RAG** | Feed LLM external docs before answering | Best way to ground model; requires index |
| **Fine-tuning** | Retraining model on your data | Expensive ($1k–100k); only if you have 100+ examples |
| **Agent** | LLM that picks tools and decides next steps | For multi-step workflows; adds latency |
| **Vector Embedding** | Text converted to numbers for similarity search | Powers RAG retrieval |
| **Vector DB** | Database of embeddings (Pinecone, Weaviate) | Infrastructure for RAG |
| **Accuracy** | % of outputs that are correct/useful | Primary success metric for AI |
| **Latency** | Time for LLM to return answer | Must be <2–5s for real-time use |
| **Inference** | Running the model (what users do) | Pay per token for this |
| **Training** | Building/retraining the model (done by vendor) | Don't do this unless you have to |

---

## Post-Curriculum Resources

After finishing this 3-week course, deepen your knowledge with:

**Books:**
- "Patterns for AI Engineering" (free, online) — architecture patterns
- "Prompt Engineering Guide" (free, GitHub) — hands-on prompting

**Courses (Self-Paced):**
- DeepLearning.AI: "Building Systems with LLMs" (2 hours)
- Replit: "Build an AI Product" (2 hours)

**Hands-On:**
- Build a simple RAG system with LangChain (tutorial, 4 hours)
- Test models (Claude, GPT-4) on your own use cases
- Attend AI PM office hours (LinkedIn, Twitter communities)

**Stay Current:**
- Weekly: TheAIIndex newsletter
- Monthly: Hugging Face arxiv digest
- Ad-hoc: Twitter #AITwitter, LessWrong (AI safety)

---

## Your AI PM Toolkit

After this curriculum, you should feel confident:

✓ Reviewing an AI feature proposal from engineering
✓ Writing user stories and acceptance criteria for AI features
✓ Estimating cost/latency/accuracy tradeoffs
✓ Spotting hallucination, bias, and cost risks early
✓ Communicating with executives, engineers, and customers about AI
✓ Building a PRD for an AI-powered product
✓ Defining success metrics that matter
✓ Choosing between models, architectures, and approaches

---

## Feedback Loop

This curriculum is free and will evolve. If you:
- Find a resource that's better than what's listed
- Notice gaps in the content
- Have questions not covered

Share them, and I'll update the curriculum for the next PM learning it.

Good luck, and welcome to the AI PM community.

