# WEEK 2: RETRIEVAL, CONTEXT & ADVANCED PATTERNS

## Unit 4: Retrieval-Augmented Generation (RAG)

### The Problem RAG Solves

**Scenario Without RAG:**
```
User: "What's our Q3 revenue?"
LLM: "Your Q3 revenue was $2.3M."
Reality: Actually $4.1M, but the model guessed based on training data.
Risk: High. Hallucination.
```

**Scenario With RAG:**
```
User: "What's our Q3 revenue?"
System retrieves: Latest earnings spreadsheet, Q3 report
LLM: "According to your Q3 earnings report, revenue was $4.1M."
Risk: Low. Grounded in actual data.
```

RAG = **Retrieval-Augmented Generation**: Fetch relevant documents, feed them to the LLM, then generate an answer.

### How RAG Works (4 Steps)

**Step 1: Index (One-Time Setup)**
- Take your documents (PDFs, web pages, database records, Slack threads)
- Break into chunks (~300 words each, overlapping)
- Convert each chunk to a **vector embedding** (list of numbers representing meaning)
- Store in a **vector database** (e.g., Pinecone, Weaviate, Postgres with pgvector)

**Step 2: Retrieve (Per Query)**
- User asks: "What's our refund policy?"
- Convert their question to a vector
- Find the most similar document chunks (cosine similarity)
- Grab top 3–5 chunks

**Step 3: Augment**
- Inject those chunks into the LLM prompt
- "Here's context: [documents]. Now answer the user's question."

**Step 4: Generate**
- LLM uses the context to answer accurately
- User gets grounded, up-to-date response

### Why RAG Matters as a PM

**Hallucinations ↓** — Model answers from docs, not memory
**Recency ↑** — Can index fresh data daily
**Factuality ↑** — Users can verify by reading source docs
**Cost ↓** — Don't need to fine-tune (cheaper than retraining)

### RAG Architecture Decisions

**Q1: What Should We Retrieve From?**
- Documents (PDFs, web pages): Use document vectors
- Structured data (databases, spreadsheets): Use hybrid (both keyword search + vectors)
- Real-time data (stock prices, weather): Use APIs, not RAG

**Q2: How Often to Update the Index?**
- Real-time data → Daily or hourly indexing
- Slow-moving docs → Weekly or monthly
- Cost tradeoff: More frequent = more ops cost

**Q3: Chunk Size?**
- Too small (100 tokens): Lose context
- Too large (1000 tokens): Noisy, mixes topics
- Sweet spot: 200–400 tokens with 50-token overlap

**Q4: How Many Chunks to Retrieve?**
- Too few (1): Miss context, poor answers
- Too many (20): Bloat prompt, raise cost, LLM ignores later chunks
- Sweet spot: 3–5 chunks

### Common RAG Mistakes

**Mistake 1: Indexing Everything**
- Problem: Retriever returns irrelevant docs, LLM gets confused
- Fix: Be selective. Only index documents that answer your use case

**Mistake 2: Stale Index**
- Problem: User asks about Q4 results, system gives Q3
- Fix: Update index frequency based on data velocity

**Mistake 3: No Retrieval Verification**
- Problem: User can't tell if the answer came from a real source
- Fix: Have LLM cite the source document and page number

**Mistake 4: Semantic Search Only**
- Problem: Keyword matches are missed ("CEO" vs. "Chief Executive Officer")
- Fix: Use hybrid search (both keyword + semantic)

### RAG Trade-offs

| Aspect | Pro | Con |
|--------|-----|-----|
| **Cost** | Cheaper than fine-tuning | Adds retrieval infra (vector DB, embeddings) |
| **Latency** | Faster than training | Adds retrieval lookup (~100–500ms) |
| **Quality** | Great for factual tasks | Can fail if retrieval misses relevant docs |
| **Flexibility** | Easy to update docs | Requires careful chunking + indexing |

---

## Unit 5: Agents, Tool Use & Agentic Loops

### What Is an Agent?

An **agent** is an LLM that can decide which tools to use and execute them iteratively.

**Simple vs. Agent Approaches:**

**Without Agent (Deterministic):**
```
User: "Get my last 5 invoices and calculate total."
System: Call DB directly, sum, return.
Problem: Can't handle complex or ambiguous requests.
```

**With Agent (Reasoning):**
```
User: "Get my last 5 invoices and calculate total."
Agent thinks: "I need to (1) fetch invoices, (2) filter to last 5, (3) sum."
Agent picks tool: "list_invoices"
System: Returns [inv1, inv2, inv3, inv4, inv5]
Agent thinks: "Good, now I sum them."
Agent picks tool: "calculate"
System: Returns $45,230
Agent responds: "Your last 5 invoices total $45,230."
Benefit: Flexible, can reason through the steps.
```

### The Agentic Loop

```
LLM decides
    ↓
Pick a tool (or stop)
    ↓
Tool executes
    ↓
Return result to LLM
    ↓
LLM thinks "what next?"
    ↓
Repeat until done
```

### When to Use Agents

**Good Use Cases:**
- Multi-step workflows (check stock → compare to benchmarks → recommend)
- Conditional logic (if error, retry differently)
- Real-time data (call APIs, not retrieval)
- User clarification (agent asks "Did you mean X or Y?")

**Bad Use Cases:**
- Simple retrieval (just use RAG)
- Latency-critical (agents add thinking time)
- One-shot tasks (overkill)

### Tool Use Best Practices

**Keep Tools Simple:**
- Good: `get_invoice(invoice_id: string)`
- Bad: `process_financial_data(query: string)` (too vague)

**Provide Clear Descriptions:**
```
Tool: "get_weather"
Description: "Get current weather for a city. Returns temp, humidity, conditions."
Parameter: city (string)
```

**Handle Tool Errors Gracefully:**
- Agent calls a tool
- Tool fails (API down, bad parameter)
- Agent should retry or pick a different tool
- If all tools fail, agent returns "I couldn't complete that."

**Limit Tool Calls:**
- Prevent infinite loops: Max 5–10 tool calls per query
- Timeout: If agent thinks for >10 seconds, stop and return partial result

---

## Unit 6: Fine-Tuning vs. Prompting vs. RAG — When to Use What

### The Decision Tree

```
Do you need the model to learn domain-specific format/language?
├─ Yes, and you have 100+ examples → Fine-tune
├─ Yes, but <100 examples → Prompting (few-shot)
└─ No → Go to Q2

Q2: Does the task need recent/external data?
├─ Yes → RAG (or Agents + tools)
└─ No → Go to Q3

Q3: Is the base model insufficient (e.g., reasoning)?
├─ Yes → Pick a stronger model or fine-tune
└─ No → Use prompting
```

### Fine-Tuning

**What It Is:** Retraining the model on your specific data to change behavior.

**When to Use:**
- You have 100+ training examples
- The model needs to learn a specific format or style
- You want deterministic behavior
- Examples: Customer support responses in your brand voice, medical diagnosis templates

**Cost:**
- Training: $1k–$100k depending on model size and dataset
- Inference: Usually same as base model (sometimes cheaper)
- Time: 1–7 days for training

**Risk:**
- You lose the model's general knowledge if overfitted
- Expensive to update (need to retrain)

**Implication:** Only fine-tune if you have the data and the use case justifies the cost.

### Prompting (Few-Shot)

**What It Is:** Giving the model examples in the prompt.

**Example:**
```
"Here are examples of good customer support responses:

Q: Why is my order delayed?
A: I apologize for the delay. I'm checking your order status now. 
Can you provide your order ID?

Now answer this:
Q: Can I return this item?
A: [LLM generates answer in the same style]"
```

**When to Use:**
- <100 examples (too few to fine-tune)
- Task is clear from examples
- You want flexibility (change examples without retraining)

**Cost:**
- Free (just longer prompts = slightly higher token cost)
- No training time

**Limitation:**
- Only works for relatively simple tasks
- Model can ignore examples if conflicted

**Implication:** Start here. It's fast and cheap.

### RAG

**When to Use:**
- Task needs external data (documents, databases)
- Data changes frequently
- You want citations/verification

**vs. Fine-tuning:**
- RAG: Dynamic data, flexible, no training
- Fine-tuning: Static behavior, deterministic, requires examples

**Implication:** RAG + prompting > fine-tuning for most PM use cases.

### Comparison Table

| Dimension | Fine-Tuning | Prompting (Few-Shot) | RAG |
|-----------|-------------|---------------------|-----|
| **Setup Time** | Days | Hours | Hours–Days |
| **Cost** | $1k–100k | ~$0 (token cost) | $100–1k (infra) |
| **Flexibility** | Low (need to retrain) | High (change prompt) | High (update docs) |
| **Latency** | Fast | Fast | Slower (retrieval) |
| **Quality on Simple Tasks** | Best | Good | Good |
| **Quality on Dynamic Data** | Poor | Okay | Best |
| **Requires Examples?** | Yes (100+) | Yes (3–5) | No |

---

## Week 2 Deliverable: Architecture Decision Tree

**Task:** For your use case from Week 1, decide: Should you fine-tune, prompt, or use RAG?

**Use Case:** _(Repeat from Week 1)_

**Fill in:**

| Question | Answer | Implication |
|----------|--------|------------|
| Do you have 100+ labeled examples? | | |
| Does the task require external/dynamic data? | | |
| How often does the task definition change? | | |
| What's your latency requirement? | | |
| What's your budget for training? | | |

**Decision:** Fine-tune / Prompt (few-shot) / RAG / Combination

**Justification:** 2–3 sentences explaining the tradeoff.

**Example Answer:**
> **Use Case:** Customer support chatbot
> - Examples: ~50 support conversations (not enough for fine-tuning)
> - Data: Knowledge base + FAQ (perfect for RAG)
> - Latency: 2–3 seconds acceptable
> - Budget: $5k/month
> **Decision:** RAG + Prompting
> **Justification:** We have a large knowledge base that changes weekly, so fine-tuning would be outdated fast. RAG lets us update docs on the fly. We'll use few-shot prompting to style responses in our brand voice without retraining.

---

**End of Week 2 (Units 4–6)**

You now understand:
- How to augment LLMs with external data (RAG)
- How to build multi-step reasoning systems (Agents)
- When to fine-tune vs. prompt vs. use RAG

**Time Spent:** ~12–15 hours
**Next:** Week 3 — Product Strategy & Metrics

