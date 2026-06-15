# WEEK 2: RETRIEVAL, CONTEXT & ADVANCED PATTERNS

## Unit 4: Retrieval-Augmented Generation (RAG)

### The Problem RAG Solves

**Scenario Without RAG:**
```
User: "What's our Q3 revenue?"
LLM: "Your Q3 revenue was $2.3M."
Reality: Actually $4.1M, but the model guessed based on training data patterns.
Risk: High. Hallucination.
```

**Scenario With RAG:**
```
User: "What's our Q3 revenue?"
System retrieves: Latest earnings spreadsheet, Q3 report PDF
LLM: "According to your Q3 earnings report, revenue was $4.1M."
Risk: Low. Grounded in actual data.
```

RAG = **Retrieval-Augmented Generation**: Fetch relevant documents, feed them to the LLM as context, then generate an answer. The model answers from the documents, not from memory.

### How RAG Works (4 Steps)

**Step 1: Index (One-Time Setup)**
- Take your documents (PDFs, web pages, database records, Slack threads)
- Break into chunks (~300 words each, with some overlap)
- Convert each chunk to a **vector embedding** (a list of numbers representing its meaning)
- Store in a **vector database** (e.g., Pinecone, Weaviate, pgvector in Postgres)

**Step 2: Retrieve (Per Query)**
- User asks: "What's our refund policy?"
- Convert their question to a vector embedding
- Find the most similar document chunks (cosine similarity search)
- Grab top 3–5 matching chunks

**Step 3: Augment**
- Inject those chunks into the LLM prompt
- "Here's context: [document chunks]. Now answer the user's question."

**Step 4: Generate**
- LLM uses the retrieved context to answer accurately
- User gets a grounded, up-to-date response

### Why RAG Matters as a PM

**Hallucinations ↓** — Model answers from your documents, not its training memory
**Recency ↑** — Can index fresh data daily or even hourly
**Factuality ↑** — Users can verify answers by reading the cited source
**Cost ↓** — Cheaper than fine-tuning (no model retraining needed)
**Updatability ↑** — Update the index when docs change; no model changes required

### RAG Architecture Decisions

**Q1: What Should We Retrieve From?**
- Documents (PDFs, web pages, wikis): Standard document vectors
- Structured data (databases, spreadsheets): Hybrid approach (keyword + vectors, or text-to-SQL)
- Real-time data (stock prices, live inventory): Use live APIs, not RAG

**Q2: How Often to Update the Index?**
- Fast-changing data → Hourly or daily indexing
- Slow-moving docs (policy manuals, FAQs) → Weekly or monthly
- Cost tradeoff: More frequent indexing = more compute cost

**Q3: Chunk Size?**
- Too small (50–100 tokens): Loses context; fragments meaning
- Too large (1,000+ tokens): Noisy, mixes topics, wastes context space
- Sweet spot: 200–400 tokens with 50-token overlap

**Q4: How Many Chunks to Retrieve?**
- Too few (1 chunk): Risk missing relevant context
- Too many (20+ chunks): Bloats the prompt, raises cost, LLM ignores later chunks
- Sweet spot: 3–5 chunks

### Common RAG Mistakes

**Mistake 1: Indexing Everything**
- Problem: Retriever returns irrelevant docs; LLM gets confused
- Fix: Be selective. Only index documents that are relevant to your use case

**Mistake 2: Stale Index**
- Problem: User asks about Q4 results; system returns Q3 data
- Fix: Match index refresh frequency to how often your data changes

**Mistake 3: No Source Citations**
- Problem: User can't verify if the answer came from a real document
- Fix: Require the LLM to cite the source document and section

**Mistake 4: Semantic Search Only**
- Problem: Keyword matches are missed ("CEO" vs. "Chief Executive Officer")
- Fix: Use hybrid search (keyword + semantic similarity)

**Mistake 5: No Retrieval Quality Check**
- Problem: Retriever returns wrong docs; LLM answers confidently from them
- Fix: Log what's being retrieved; spot-check monthly; track user feedback

### RAG Trade-offs

| Aspect | Pro | Con |
|--------|-----|-----|
| **Cost** | No model retraining needed | Adds retrieval infrastructure (vector DB, embeddings) |
| **Latency** | Relatively fast | Adds retrieval lookup (~100–500ms per query) |
| **Quality** | Excellent for factual, grounded tasks | Fails if retrieval misses relevant docs |
| **Flexibility** | Easy to update docs without model changes | Requires careful chunking + indexing design |

---

## Unit 5: Agents, Tool Use & Agentic Loops

### What Is an Agent?

An **agent** is an LLM that can decide which tools to use, execute them, observe the results, and decide what to do next — iteratively, until it completes a task.

**Simple vs. Agent Approaches:**

**Without Agent (Deterministic):**
```
User: "Get my last 5 invoices and calculate total."
System: Runs a fixed query → sums results → returns.
Limitation: Breaks if request is ambiguous or multi-step.
```

**With Agent (Reasoning):**
```
User: "Get my last 5 invoices and calculate total."
Agent reasons: "I need to (1) list invoices, (2) filter to last 5, (3) sum the amounts."
Agent calls: list_invoices(limit=5)
Result: [inv1, inv2, inv3, inv4, inv5]
Agent reasons: "Now I'll sum them."
Agent calls: calculate(numbers=[...])
Result: $45,230
Agent responds: "Your last 5 invoices total $45,230."
```

### The Agentic Loop

```
User sends request
        ↓
LLM reasons about what to do
        ↓
Pick a tool (or decide to stop)
        ↓
Tool executes
        ↓
Result returned to LLM
        ↓
LLM reasons: "What next?"
        ↓
Repeat until task complete
```

### Model Context Protocol (MCP)

**What It Is:** An open standard (created by Anthropic, now widely adopted) that defines how LLMs connect to external tools and data sources.

**Why It Matters as a PM:** Before MCP, every team had to build custom integrations between their LLM and their tools. MCP standardizes this — if your tool exposes an MCP server, any MCP-compatible LLM client can use it.

**Analogy:** Think of MCP like USB-C. Before USB-C, every device had different connectors. MCP is the universal connector for LLM tools.

**PM Implication:** When evaluating AI agents, ask your engineering team: "Are we using MCP, or building custom tool integrations?" MCP reduces build time and future maintenance.

### When to Use Agents

**Good Use Cases:**
- Multi-step workflows (check inventory → compare to threshold → create order)
- Conditional logic (if error, retry with different parameters)
- Real-time data needs (call live APIs, not just retrieve documents)
- User clarification needed (agent asks "Did you mean X or Y?")

**Bad Use Cases:**
- Simple one-shot retrieval (just use RAG)
- Latency-critical features (agents add multiple round-trips)
- When the tool sequence is always the same (use deterministic code instead)

### Tool Design Best Practices

**Keep Tools Simple and Atomic:**
- Good: `get_invoice(invoice_id: string) → Invoice`
- Bad: `process_financial_data(query: string)` (too vague; agent can't predict what it does)

**Write Clear Tool Descriptions:**
```
Tool: "get_weather"
Description: "Returns current weather for a given city. 
              Outputs temperature (°C), humidity (%), and conditions."
Parameter: city (string, required)
```

**Handle Tool Errors Gracefully:**
- If a tool fails (API down, bad parameter), the agent should retry or pick a different approach
- If all tools fail, the agent should return "I wasn't able to complete that" rather than silently hallucinating a result

**Prevent Infinite Loops:**
- Set a maximum number of tool calls per query (typically 5–10)
- Set a timeout: if the agent hasn't finished in X seconds, return a partial result

---

## Unit 6: Fine-Tuning vs. Prompting vs. RAG vs. Reasoning — When to Use What

### The Decision Tree

```
Q1: Do you need the model to learn domain-specific format or style?
├─ YES, and you have 100+ examples → Fine-tune
├─ YES, but < 100 examples → Prompting (few-shot)
└─ NO → Go to Q2

Q2: Does the task need current or external data?
├─ YES → RAG (or Agents + live tools)
└─ NO → Go to Q3

Q3: Is the task complex, multi-step, or requires deep reasoning?
├─ YES → Reasoning model (Claude Opus 4.8 extended thinking, OpenAI o1/o3)
└─ NO → Go to Q4

Q4: Can you solve it with clear instructions?
├─ YES → Prompting (zero-shot or few-shot)
└─ NO → Combine approaches (RAG + fine-tuning, or Agents + prompting)
```

### Fine-Tuning

**What It Is:** Retraining the model on your specific data to change its default behavior.

**When to Use:**
- You have 100+ high-quality labeled examples
- The task requires a very specific output format or brand voice
- You want highly consistent, deterministic behavior across all outputs
- Examples: Medical report templates, legal document formatting, brand-specific tone

**Cost:**
- Training: $1k–$100k depending on model size and dataset volume
- Inference: Same as base model (sometimes cheaper if you use a smaller fine-tuned model)
- Time: Days to weeks for training + evaluation

**Risks:**
- Can lose general knowledge if overfitted on narrow data
- Expensive to update (must retrain when requirements change)
- Requires ongoing data curation

**Implication:** Only fine-tune when you have the labeled data, a stable use case, and the cost is justified. Most PMs overestimate how often fine-tuning is the right answer.

### Prompting (Few-Shot)

**What It Is:** Giving the model examples directly in the prompt to guide its format and behavior.

**Example:**
```
"Here are examples of great customer support responses:

Q: Why is my order delayed?
A: I apologize for the delay. I'm checking your order status now. 
Could you provide your order ID so I can get more details?

Now answer this:
Q: Can I return this item?
A: [LLM generates in the same style]"
```

**When to Use:**
- < 100 examples (too few for fine-tuning)
- You want to change behavior without retraining
- Fast iteration is important (change the prompt, test immediately)

**Cost:**
- Near-zero (slightly higher token cost from longer prompts)
- No training time; iteration is instant

**Limitation:**
- Only works for relatively simple style/format guidance
- Model may deviate from examples on unusual inputs

**Implication:** Start here every time. It's the cheapest and fastest option. Only escalate to fine-tuning if prompting demonstrably fails.

### RAG

**When to Use:**
- Task needs external data (documents, databases, knowledge bases)
- Data changes frequently (daily, weekly)
- Users need to verify answers (citations required)

**vs. Fine-tuning:**
- RAG: Dynamic data, flexible, no training, updatable in real time
- Fine-tuning: Static behavior, deterministic, requires labeled examples

**Implication:** For most PM use cases, RAG + prompting outperforms fine-tuning. Reach for fine-tuning only when behavior/format — not data — needs to change.

### Structured Outputs

**What It Is:** Forcing the model to return data in a fixed, machine-readable format (JSON, XML, etc.) rather than free-form prose.

**Why It Matters:**
Without structured outputs, LLMs return natural language. When your feature uses that output programmatically (storing in a database, rendering in a UI, calling a downstream API), you need to parse it — and free-form text parsing is fragile. The model may slightly change its phrasing and break your parser.

**Example:**
```
Without Structured Output (fragile):
"The customer sentiment is positive. They mentioned they love the speed 
and found the interface intuitive. I'd rate satisfaction at 8 out of 10."

With Structured Output (reliable):
{
  "sentiment": "positive",
  "themes": ["speed", "intuitive interface"],
  "satisfaction_score": 8,
  "confidence": "high"
}
```

**When to Use:**
- Any AI output that's consumed by code rather than read by a human
- Classification tasks (sentiment, category, priority level)
- Data extraction from documents (names, dates, amounts)
- Any feature where output consistency and reliability is required

**How to Enable:**
Most major models (Claude, GPT-4o) support JSON mode or structured output schemas. You define the output schema; the model guarantees it conforms.

**PM Implication:** If your AI feature's output feeds into another system, structured outputs should be a non-negotiable requirement in your acceptance criteria. It reduces bugs and engineering maintenance significantly.

### Prompt Caching

**What It Is:** Storing the processed result of a large, repeated prompt section (like a system prompt or a set of documents) so subsequent calls reuse it instead of re-processing from scratch.

**How It Works:**
```
Without Caching:
Every API call → Full system prompt (5,000 tokens) + user query processed fresh
Cost: Full input token price × every call

With Caching:
First call → Process system prompt + cache it
Subsequent calls → Cache hit (charged at ~10% of normal input price)
Cost: 90% cheaper for the repeated portion
```

**When to Use:**
- Large, stable system prompts (product instructions, personas, policy documents)
- RAG pipelines where the same documents are retrieved repeatedly
- Multi-turn conversations where you're passing growing history on every turn

**Supported by:** Anthropic Claude, OpenAI GPT-4o (with prompt caching beta)

**PM Implication:** On high-volume AI features, prompt caching can be the difference between positive and negative unit economics. When reviewing infrastructure costs with engineering, always ask: "Is prompt caching enabled?" For a feature running 1M queries/month with a large system prompt, this can save tens of thousands of dollars monthly.

### Reasoning Models

**What They Are:** Models that internally work through a problem step-by-step before returning an answer — like showing their work. This produces higher quality on complex tasks but is slower and more expensive.

**How They Differ from Standard Models:**
```
Standard Model:
User → LLM → Answer (1–3 seconds)
Good for: Most tasks, real-time features

Reasoning Model:
User → LLM thinks... (5–60 seconds extended reasoning) → Answer
Good for: Hard problems where quality matters more than speed
```

**Examples:**
- OpenAI: o1, o3
- Anthropic: Claude Opus 4.8 with extended thinking enabled

**When to Use:**
- Complex mathematical or logical problems
- Multi-step analysis (evaluating a business proposal, reviewing a contract)
- Code generation for complex algorithms
- Any task where a human expert would "think carefully" before answering

**When NOT to Use:**
- Real-time chat features (latency is unacceptable)
- Simple tasks like summarization or classification (overkill; expensive)
- High-volume pipelines where cost per query must be low

**Hybrid Architecture:**
For many products, the right answer is: use a fast model for routine tasks, and escalate to a reasoning model only when the request is complex. Your engineering team can route based on a complexity classifier or user intent.

**PM Implication:** Reasoning models are not a drop-in upgrade — they change the latency and cost profile of your feature significantly. If someone proposes using o3 or extended thinking for a feature, ask: "What's the expected latency? What's the cost per query? Is a standard model failing on this task today?"

### Full Comparison Table

| Dimension | Fine-Tuning | Few-Shot Prompting | RAG | Structured Output | Prompt Caching | Reasoning Models | Agents |
|-----------|-------------|-------------------|-----|------------------|----------------|-----------------|--------|
| **Setup Time** | Days–Weeks | Hours | Hours–Days | Hours | Hours | Hours | Days |
| **Cost** | $1k–100k training | ~$0 | $100–1k/mo infra | ~$0 | Saves 80–90% on repeated context | 5–10x per query | $100–1k/mo infra |
| **Flexibility** | Low (retrain to change) | High | High | High | High | High | High |
| **Latency** | Fast | Fast | Slower (+100–500ms) | Fast | Same or faster | Slow (5–60s) | Slowest |
| **Best For** | Domain format/style | Simple tasks, fast iteration | Factual + external data | Output fed into systems | High-volume features with large prompts | Complex reasoning tasks | Multi-step workflows |
| **Requires Examples?** | Yes (100+) | Yes (3–5) | No | No | No | No | No |

---

## Week 2 Deliverable: Architecture Decision Tree

**Task:** For your use case from Week 1, decide on your architecture approach.

**Use Case:** _(Repeat from Week 1)_

**Fill in:**

| Question | Answer | Implication |
|----------|--------|------------|
| Do you have 100+ labeled examples? | | |
| Does the task require external or frequently updated data? | | |
| Is the task complex enough to require deep reasoning? | | |
| Does AI output feed into another system (database, API, UI)? | | |
| What's your latency requirement? | | |
| What's your per-query budget? | | |

**Decision:** Fine-tune / Few-shot prompting / RAG / Reasoning model / Combination

**Justification:** 2–3 sentences explaining the tradeoff.

**Example Answer:**
> **Use Case:** Customer support chatbot
> - Examples: ~50 support conversations (not enough for fine-tuning)
> - Data: Knowledge base + FAQ documents (perfect for RAG)
> - Latency: 2–3 seconds acceptable
> - Output: Suggested response shown to human agent (no structured output needed)
> - Budget: $5k/month
>
> **Decision:** RAG + Few-Shot Prompting
>
> **Justification:** We have a large knowledge base that changes weekly, so fine-tuning would be outdated fast. RAG keeps answers current. Few-shot examples in the prompt will handle the brand voice without retraining. We'll enable prompt caching for our system prompt to reduce costs at scale.

---

**End of Week 2 (Units 4–6)**

You now understand:
- How to augment LLMs with external data (RAG)
- How to build multi-step reasoning systems (Agents)
- When to fine-tune vs. prompt vs. RAG vs. use a reasoning model
- How structured outputs and prompt caching affect your product's reliability and economics

**Time Spent:** ~12–15 hours
**Next:** Week 3 — Product Strategy & Metrics
