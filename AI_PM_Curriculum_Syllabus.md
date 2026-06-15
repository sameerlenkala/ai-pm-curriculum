# AI PM Learning Curriculum: 3-Week Intensive
## For Non-Technical Product Owners Managing AI Products

---

## Overview
This curriculum teaches you to:
- Understand what LLMs/AI systems can and can't do (and why)
- Evaluate technical feasibility and engineering tradeoffs
- Define success metrics for AI features
- Lead informed conversations with engineers and stakeholders
- Identify risks and edge cases early

**Pace:** ~10–15 hours/week across 3 weeks
**Format:** Self-paced modules + free resources + discussion prompts

---

## 3-Week Structure

### **Week 1: AI Foundations & LLM Fundamentals**
**Goal:** Build mental models of how LLMs work (non-technical, intuitive)

- **Unit 1:** What Are LLMs? (Tokens, Training, Inference)
- **Unit 2:** LLM Behavior & Limitations (Hallucinations, Stochasticity, Context Windows)
- **Unit 3:** Commercial LLM Landscape (Anthropic, OpenAI, Google, Meta, Open-Source)
- **Deliverable:** "LLM Capability Matrix" — compare 3 models on cost, speed, reasoning

### **Week 2: Retrieval, Context & Advanced Patterns**
**Goal:** Understand how to augment LLMs with external data and multi-step reasoning

- **Unit 4:** Retrieval-Augmented Generation (RAG) — Why, How, Tradeoffs
- **Unit 5:** Agents, Tool Use & Agentic Loops — Decision-Making Systems
- **Unit 6:** Fine-Tuning vs. Prompting vs. RAG vs. Reasoning Models — When to Use What
- **Deliverable:** "Architecture Decision Tree" — pick the right approach for a use case

### **Week 3: Product Strategy, Metrics & Launch**
**Goal:** Bridge technical understanding into product decisions and success measurement

- **Unit 7:** AI Product Strategy — Feasibility, User Value, GTM
- **Unit 8:** Metrics, Evaluation & Risk Management for AI Features
- **Capstone:** Write a PRD for an AI feature using everything you've learned

---

## Free Resource Index
(By unit — detailed links and reviews in Resources.md)

| Unit | Resource | Type | Time | Why It Matters |
|------|----------|------|------|----------------|
| 1–2 | Anthropic Research Blog | Blog series | 1h | Best non-technical LLM explainer from an LLM maker |
| 1–2 | 3Blue1Brown "Neural Networks" (Eps 1–2) | Video | 30m | Intuitive foundations, no math required |
| 1–3 | Epoch.ai Model Tracker | Interactive | 30m | Live model landscape, cost, speed comparisons |
| 4 | "Building & Evaluating Advanced RAG" (Andrew Ng) | Video course | 1.5h | Practical RAG fundamentals |
| 4–5 | LangChain documentation | Reference | 2h | See RAG and agent patterns in real code |
| 5 | Lilian Weng: "LLM-powered Autonomous Agents" | Blog post | 1h | Best conceptual explainer of agentic loops |
| 6 | Prompting Guide (promptingguide.ai) | Free site | 1h | Prompting techniques + decision framework |
| 7–8 | a16z: "10 Questions Before Building an AI Product" | Blog | 15m | Product feasibility and metrics mindset |

---

## Study Tips

**Active Learning:**
- Summarize each unit in your own words (1–2 paragraphs)
- Draw diagrams (LLM flow, RAG architecture, agentic loops)
- Write prompts and test them on Claude/ChatGPT (see what breaks)

**Conversation Prep:**
- After each unit, write 3 questions you'd ask an engineer
- At end of week, do a mock technical review with a colleague

**Glossary:**
- Keep a running "AI PM Glossary" as you go (see section below)

---

## Glossary (Quick Reference)

### Core Concepts

**Token**
- Smallest unit the LLM processes. ~1 token ≈ 4 characters in English
- Matters for: cost (charged per token), latency, context window limits

**Context Window**
- Maximum number of tokens the model can "see" at once
- Claude Sonnet 4.6 / Opus 4.8: 200k tokens (~150k words); GPT-4o: 128k; Gemini 2.5 Pro: 1M+
- Tradeoff: Larger windows = more grounding, higher cost/latency

**Temperature**
- Controls randomness (0 = deterministic, higher = more creative)
- 0–0.3: Factual tasks (QA, summarization, classification)
- 0.7–1.0: Creative tasks (brainstorming, ideation, copywriting)
- Note: Some providers allow values up to 2.0, but above 1.0 is rarely useful in production

**Prompt Engineering**
- Writing and structuring prompts to get better outputs
- Few-shot: Showing examples in the prompt
- Chain-of-thought: "Let's think step by step"

**Hallucination**
- LLM confidently making up false information
- Common with factual queries without external grounding
- RAG + retrieval + human review reduces this significantly

**Fine-tuning**
- Retraining the model on custom data (expensive, slow)
- Use when: Task requires domain-specific language or very specific output format
- Don't use when: You can solve it with prompting or RAG

**Retrieval-Augmented Generation (RAG)**
- Feed the LLM relevant context documents before asking a question
- Reduces hallucinations, enables use of current/private data
- Tradeoff: Adds latency, requires vector DB + embedding model

**Agent / Agentic Loop**
- System where an LLM decides which tools to call and in what order
- LLM reasons → picks a tool → executes → loops until done
- Examples: Customer support bot, data analysis assistant

**Structured Output**
- Forcing the model to return data in a fixed format (JSON, XML, etc.)
- Critical when AI output feeds into another system (database, API, UI)

**Prompt Caching**
- Storing the result of processing a large, repeated prompt section
- Subsequent requests reuse the cache at ~10% of normal cost
- Important for cost optimization on high-volume features

**Vector Embedding**
- Converts text into a numerical representation (list of numbers)
- Similar texts → similar embeddings
- Used for semantic search in the RAG retrieval step

**Reasoning Model**
- A model that "thinks" through a problem step-by-step before answering
- Higher quality on complex tasks; slower and more expensive
- Examples: OpenAI o1/o3, Claude with extended thinking

**LLM vs. Foundation Model vs. Generative AI**
- **Foundation Model:** Big model trained on broad data (can do many tasks)
- **LLM:** Foundation model trained primarily on text
- **Generative AI:** Broader category (images, video, audio, text)

---

## Assumptions & Scope

**What This Covers:**
- Text-based LLMs (Claude, ChatGPT, Llama, etc.)
- Product strategy for AI features (not MLOps or data engineering)
- Evaluation and metrics for AI outputs
- When to build vs. buy vs. partner

**What This Doesn't Cover:**
- Deep learning math or neural network internals
- Training your own LLM from scratch (not practical for most PMs)
- Computer vision, multimodal, or non-text AI (though image input is now common — ask your engineering team if multimodal is relevant to your use case)
- Advanced prompt engineering recipes (covered lightly; see Resources.md for depth)

---

## Success Criteria

By end of Week 3, you should be able to:

✓ Explain to a CEO why an LLM-based feature works (and its limitations)
✓ Evaluate a technical proposal: "Should we fine-tune, use RAG, or just prompt?"
✓ Write user stories + acceptance criteria for an AI feature
✓ Define success metrics for AI outputs (accuracy, latency, cost, user satisfaction)
✓ Spot red flags in an AI roadmap (hallucination risk, token cost, data privacy)
✓ Read a research paper abstract and extract what's relevant to your product

---

## Next Steps

Start with **Week 1, Unit 1** below.

Spend ~4–5 hours on each unit (reading + digesting + writing notes).
Do the weekly deliverables.
Check in with the glossary constantly.

---

# WEEK 1: AI FOUNDATIONS & LLM FUNDAMENTALS

## Unit 1: What Are LLMs? (Tokens, Training, Inference)

### Core Idea
An LLM is a machine learning system trained to predict the next word (or "token") in a sequence, billions of times. This simple task—learned at massive scale—produces surprising intelligence.

### Key Mental Model

**Training Phase (what happened before you used it):**
1. Anthropic (or OpenAI, etc.) collected massive amounts of text (books, web, code)
2. Showed the model: "Here are 100 words. What comes next?"
3. Model guessed wrong millions of times and adjusted
4. After seeing billions of examples, it got very good at predicting text

**Inference Phase (what happens when you ask it a question):**
1. You write: "What is the capital of France?"
2. Model predicts the next token: " Par"
3. Predicts again: "is"
4. Keeps predicting until it outputs a stop signal
5. You read: "The capital of France is Paris."

**Why This Matters as a PM:**
- The model isn't "looking up" facts; it's pattern-matching from training data
- It can't reason perfectly; it simulates reasoning
- Each prediction has inherent uncertainty (it picks from a probability distribution)

### Tokens: The Atomic Unit

A **token** is how the model breaks down text into chunks.

**Examples:**
- "Hello" = 1 token
- "Hello world" = 2 tokens
- "Jagdalpur" = 1–2 tokens (depends on tokenizer)
- "!" = 1 token

**Why It Matters:**
- **Cost:** LLM APIs charge per token (typically $0.001–$0.01 per 1k input tokens depending on model; check provider pricing pages)
- **Speed:** Processing 100k tokens takes longer than 1k
- **Limits:** Context window = max tokens you can feed the model

**Rule of Thumb:** ~1 token ≈ 4 characters or 0.75 words

### Context Window: The Model's Memory

The **context window** is the maximum number of tokens the model can process at once. It's the model's working memory.

**Current Models (2026):**
- Claude Sonnet 4.6 / Opus 4.8: 200k tokens (~150,000 words)
- GPT-4o: 128k tokens
- Gemini 2.5 Pro: 1M+ tokens (for extremely long documents)
- Llama 3.3 70B: 128k tokens

**What Fits in 200k Tokens?**
- ~150 pages of text
- A medium-sized codebase (50k lines)
- A conversation + 20 relevant documents

**Product Implication:**
If your feature needs to analyze a 500-page contract, you need RAG (see Week 2) or a model with a very large context window. You can't always just pass it all at once — cost and latency matter too.

### Temperature: Randomness Dial

When the model predicts the next token, it doesn't always pick the most likely one. It samples from a probability distribution.

**Temperature = 0:**
- Always pick the most likely token
- Deterministic (same input = same output)
- Use for: Customer support scripts, factual Q&A, code generation

**Temperature = 0.7:**
- Mix of likely and less-likely tokens
- Somewhat variable
- Use for: General chat, summaries, content drafts

**Temperature = 1.0:**
- High randomness
- Creative but less reliable
- Use for: Brainstorming, ideation

**Note:** Some providers allow values above 1.0 (up to 2.0), but this is rarely useful in production features. Stick to 0–1 unless you have a specific reason.

**PM Implication:**
If you're building a chatbot that answers FAQs, use temperature 0. If you're building a creative writing assistant, use 0.7–1.

---

### Reading & Resources

**Essential:**
1. **Anthropic Research Blog** (20 min read)
   - URL: https://www.anthropic.com/research
   - Browse for posts on training, inference, and how Claude works
   - Focus on: "What is an LLM" style explainers

2. **3Blue1Brown: "Neural Networks" (Episodes 1–2 only)** (30 min video)
   - URL: https://www.youtube.com/watch?v=aircAruvnKk
   - Skip the math; watch for intuition on how neural networks learn
   - Stop after Episode 2 (don't need the backpropagation deep dive)

**Optional Deep Dive:**
- Hugging Face NLP Course, Chapter 1 (free, interactive): https://huggingface.co/learn/nlp-course/chapter1/1

---

### Self-Check: Do You Understand Unit 1?

After reading, you should be able to answer:

1. **"Why does my LLM hallucinate?"** — Because it's predicting the next token based on patterns, not retrieving facts. Without external context (RAG), it can confidently output false information.

2. **"If I double my context window, what happens?"** — Cost and latency increase, but you can feed more context. Useful for longer documents or conversations.

3. **"What's the difference between training and inference?"** — Training is when Anthropic built the model (expensive, one-time). Inference is when you use it (you pay per token, per call).

4. **"Why does temperature matter?"** — It controls randomness. 0 = reliable, 1 = creative. Pick based on your use case.

---

## Unit 2: LLM Behavior & Limitations

### The Capability Cliff

LLMs are surprisingly good at many tasks but hit hard limits in others.

**What LLMs Are Good At:**
- Summarizing text
- Answering questions (if context is provided)
- Writing and editing
- Code generation and debugging
- Reasoning through multi-step problems (especially reasoning models)
- Creative writing and brainstorming
- Translation
- Classifying and categorizing content

**What LLMs Struggle With:**
- Counting precisely (e.g., "Count the exact number of words")
- Recent events past their knowledge cutoff
- Math with large numbers (unless using a calculator tool)
- Perfect factuality without grounding (hallucinations)
- Multi-step logic requiring 100% accuracy (medical diagnosis, legal contracts)
- Handling highly ambiguous or contradictory instructions

**As a PM:** This shapes feature scope. If your feature requires hallucination-free factual accuracy, RAG is mandatory. If it needs perfect math, add a calculator tool. If it needs real-time data, use APIs.

### Hallucinations: Confident Lies

A hallucination is when the model generates plausible-sounding but false information *while appearing confident*.

**Why It Happens:**
- The model is predicting tokens, not retrieving from a database
- It's pattern-matching from training data
- If the training patterns suggest a plausible-sounding answer, it outputs that, even if wrong

**Example:**
```
User: "Who is the current CEO of Acme Corp?"
Model (trained in 2022): "John Smith has been CEO since 2019."
Reality: Sarah Chen became CEO in 2024.
Problem: Model outputs stale info with high confidence.
```

**How to Reduce Hallucinations:**
1. **RAG:** Feed the model current/relevant documents before answering
2. **Citations:** Require the model to cite the source for every claim
3. **Lower stakes tasks:** Use for draft-writing, not medical or legal advice
4. **Temperature = 0:** Reduces randomness; increases consistency
5. **Human review gate:** For high-stakes outputs, always have a human verify

**PM Implication:** If your feature answers factual questions about dynamic data (company info, user-specific info, policy details), use RAG or live APIs. Never rely on the model's memory for current facts.

### Stochasticity: The Randomness Problem

Every inference is slightly different (unless temperature = 0).

**Example:**
```
Prompt: "Summarize this article in 1 sentence."
Run 1: "The startup secured Series B funding."
Run 2: "A startup raised $50M in Series B."
Run 3: "New funding round for emerging company."
```

**Implication:**
- You can't rely on exact output matching
- Don't build features that require character-perfect consistency
- QA testing is harder (same input, slightly different output each time)
- Fix: Use temperature = 0 during testing; use semantic correctness checks, not exact-match checks

### Context Window & Grounding

The context window is your tool for grounding the model.

**Scenario 1: No Context**
```
User: "Is this company a good investment?"
Model: Outputs based on training data patterns
Risk: High — likely hallucination
```

**Scenario 2: With Context (RAG)**
```
User: "Is this company a good investment?"
System: Retrieves latest 10-K, earnings report, news articles
Model: Summarizes the retrieved documents
Risk: Lower (assuming retrieved docs are accurate and current)
```

**PM Implication:** Always design for context. What documents, APIs, or databases should feed into the LLM to ground its answers?

---

### Reading & Resources

**Essential:**
1. **Anthropic: "Constitutional AI & Safety"** (15–20 min)
   - URL: https://www.anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback
   - Why: Understand how modern LLMs are trained to reduce harmful outputs
   - Focus on: "How is Constitutional AI different from standard RLHF?"

2. **Prompting Guide: LLM Limitations** (10 min)
   - URL: https://www.promptingguide.ai/introduction/basics
   - Focus on: Sections covering LLM limitations and failure modes
   - Action: List 5 tasks LLMs struggle with in your domain

**Optional:**
- "Hallucinations in LLMs: A Survey" (Hugging Face paper digest): https://huggingface.co/papers/2309.01219

---

### Self-Check: Do You Understand Unit 2?

1. **"My support team is concerned about the chatbot giving wrong answers. What do I do?"** — Implement RAG to ground responses in your knowledge base, tune temperature low, and require the model to cite sources. Add a human review step for low-confidence outputs.

2. **"Can I use an LLM to diagnose medical conditions?"** — Not alone. It hallucinates. You'd need strict guardrails, mandatory human review, integration with verified medical databases, and legal/liability coverage.

3. **"Why is my QA testing flaky?"** — Temperature > 0 means outputs vary. Use temperature = 0 for testing, or build tests that check for semantic correctness rather than exact-match strings.

---

## Unit 3: Commercial LLM Landscape

### The Major Players (2026)

> **Note:** Model pricing and specs change frequently. Always verify at the provider's pricing page before making decisions.

| Model | Maker | Approx. Cost (per 1M tokens) | Speed | Best For | Notes |
|-------|-------|------------------------------|-------|----------|-------|
| **Claude Haiku 4.5** | Anthropic | ~$0.80 in / $4 out | Very fast | High-volume, latency-sensitive tasks | Cheapest Anthropic model; great for simple tasks |
| **Claude Sonnet 4.6** | Anthropic | ~$3 in / $15 out | Fast | Best all-rounder; balanced reasoning + safety | 200k context; go-to for most use cases |
| **Claude Opus 4.8** | Anthropic | ~$15 in / $75 out | Moderate | Complex analysis, hard reasoning tasks | Most powerful Anthropic model |
| **GPT-4o** | OpenAI | ~$2.50 in / $10 out | Fast | General-purpose, strong tool use, multimodal | 128k context; excellent ecosystem |
| **o3 / o1** | OpenAI | $10–60+ in | Slow (10–30s) | Math, logic, complex multi-step reasoning | "Thinks" before answering; not for real-time chat |
| **Gemini 2.5 Pro** | Google | ~$1.25 in / $10 out | Fast | Very long context (1M+ tokens), search grounding | Best for processing entire codebases or long docs |
| **Gemini 2.0 Flash** | Google | ~$0.10 in / $0.40 out | Very fast | Budget-conscious, high-volume, real-time | Surprisingly good quality for the price |
| **Llama 3.3 70B** | Meta (open-source) | ~$0.23 in / $0.23 out (via API) | Fast | Cost-sensitive, on-premise, private data | Open-source; self-hostable; good quality |

### Key Tradeoffs

**Cost vs. Quality:**
- Claude Haiku 4.5 and Gemini 2.0 Flash: Cheapest, good for simple tasks
- Claude Sonnet 4.6 / GPT-4o: Mid-tier cost, strong quality, best starting point
- Claude Opus 4.8 / o3: Highest cost, use only where quality is critical

**Speed vs. Reasoning:**
- Fastest: Haiku 4.5, Gemini 2.0 Flash, GPT-4o (milliseconds to ~2 seconds)
- Best reasoning: Claude Opus 4.8, o3 (may take 5–30 seconds to "think")
- Use fast models for chat and real-time features; reasoning models for batch/offline analysis

**Context Window:**
- Claude Sonnet/Opus: 200k (excellent for most use cases)
- GPT-4o: 128k
- Gemini 2.5 Pro: 1M+ (for entire codebases, very long documents)

**Privacy / Data Control:**
- Open-source (Llama 3.3): Run on your own servers — data never leaves your infrastructure
- Closed (Anthropic, OpenAI, Google): Data sent to their servers — check terms of service

### Decision Tree: Which Model?

```
Q1: Is this a complex reasoning task (math, audit, multi-step logic)?
├─ YES → Claude Opus 4.8 or OpenAI o3 (best reasoning)
└─ NO → Go to Q2

Q2: Is high-volume throughput or low cost the priority?
├─ YES → Claude Haiku 4.5 or Gemini 2.0 Flash
└─ NO → Go to Q3

Q3: Is data privacy critical (can't send data to 3rd-party)?
├─ YES → Llama 3.3 70B (self-hosted)
└─ NO → Go to Q4

Q4: Do you need >200k token context?
├─ YES → Gemini 2.5 Pro
└─ NO → Claude Sonnet 4.6 (best all-rounder)
```

### Open-Source vs. Closed Models

**Closed (Anthropic, OpenAI, Google):**
- ✓ Best quality out-of-the-box
- ✓ No infrastructure burden
- ✓ Regular model updates from provider
- ✗ Vendor lock-in
- ✗ Data privacy concerns (inputs may be logged unless you have an enterprise agreement)
- Cost: Pay per inference

**Open-Source (Llama 3.x, Mistral):**
- ✓ Run on your servers (full data privacy)
- ✓ Customize / fine-tune freely
- ✓ Lower long-term cost at high scale
- ✗ Weaker out-of-box quality vs. frontier closed models
- ✗ You manage all infrastructure, updates, and scaling
- Cost: Hardware + ops team

**PM Implication:**
- Prototype with Anthropic/OpenAI (fast, no ops overhead, high quality)
- At scale or with sensitive data: evaluate Llama 3.x or self-hosted options
- Enterprise deals with Anthropic/OpenAI often include no-logging agreements

---

### Reading & Resources

**Essential:**
1. **Epoch.ai: Model Tracker** (15 min interactive)
   - URL: https://epoch.ai/
   - Browse the model comparison dashboards
   - Filter by cost, speed, and reasoning quality
   - Updated regularly with new models

2. **Anthropic: Claude Models & Pricing** (10 min)
   - URL: https://www.anthropic.com/pricing
   - Compare Haiku, Sonnet, Opus tiers
   - Understand context window and cost per token

3. **OpenAI: Model Comparison** (10 min)
   - URL: https://platform.openai.com/docs/models
   - Compare GPT-4o, o1, o3 — understand when to use each

4. **Meta: Llama Models** (10 min)
   - URL: https://www.llama.com/
   - Understand open-source positioning, commercial use terms

---

### Self-Check: Do You Understand Unit 3?

1. **"We need to launch next week and cost is tight. What model?"** — Claude Haiku 4.5 or Gemini 2.0 Flash. ~10x cheaper than Sonnet/Opus. Quality hit on complex tasks, but fine for simple classification or chat.

2. **"Our enterprise customer won't let us send data to cloud APIs."** — Self-hosted Llama 3.3 70B on your own infrastructure. Or negotiate a data processing agreement with Anthropic/OpenAI (enterprise tier often includes no-logging).

3. **"Engineering wants to use o3 for our real-time chat feature. Should we?"** — No. o3 takes 5–30 seconds to "think." For real-time chat, use GPT-4o or Claude Sonnet 4.6. Reserve reasoning models for offline/batch tasks.

---

## Week 1 Deliverable: LLM Capability Matrix

**Task:** Compare 3 models on the use case you're most likely to build.

**Pick a Use Case:**
- Customer support chatbot
- Document summarizer
- Code review assistant
- Content generator
- Data analyst (Q&A over databases)

**Fill in the Matrix:**

| Dimension | Claude Sonnet 4.6 | GPT-4o | Llama 3.3 70B |
|-----------|-------------------|--------|---------------|
| **Reasoning Quality** | | | |
| **Approx. Cost (per 1M tokens)** | | | |
| **Latency** | | | |
| **Context Window** | | | |
| **Safety / Alignment** | | | |
| **Privacy / Data Control** | | | |
| **Best For This Use Case?** | | | |
| **Key Trade-offs** | | | |

**Write 2–3 Sentences:** Which would you pick and why?

**Example Answer:**
> For a customer support chatbot, I'd pick Claude Sonnet 4.6. It's best at nuanced reasoning (handling edge cases), has a 200k context window (can hold customer history + full knowledge base), and Anthropic's safety alignment makes it reliable for public-facing use. Cost is ~$3k/month at our scale, which is acceptable. GPT-4o would also work and has a slightly lower input cost; Llama 3.3 would be cheapest but requires self-hosting and engineering overhead.

---

**End of Week 1 (Units 1–3)**

You now understand:
- How LLMs work (token prediction, training, inference)
- Their limitations (hallucination, stochasticity, knowledge cutoff)
- The commercial landscape (which model for which job)

**Time Spent:** ~12–15 hours
**Next:** Week 2 — Augmenting LLMs with Retrieval, Agents & Advanced Patterns
