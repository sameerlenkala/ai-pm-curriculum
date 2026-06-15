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
- **Unit 3:** Commercial LLM Landscape (OpenAI, Anthropic, Meta, Open-Source)
- **Deliverable:** "LLM Capability Matrix" — compare 3 models on cost, speed, reasoning

### **Week 2: Retrieval, Context & Advanced Patterns**
**Goal:** Understand how to augment LLMs with external data and multi-step reasoning

- **Unit 4:** Retrieval-Augmented Generation (RAG) — Why, How, Tradeoffs
- **Unit 5:** Agents, Tool Use & Agentic Loops — Decision-Making Systems
- **Unit 6:** Fine-Tuning vs. Prompting vs. RAG — When to Use What
- **Deliverable:** "Architecture Decision Tree" — pick the right approach for a use case

### **Week 3: Product Strategy, Metrics & Launch**
**Goal:** Bridge technical understanding into product decisions and success measurement

- **Unit 7:** AI Product Strategy — Feasibility, User Value, GTM
- **Unit 8:** Metrics, Evaluation & Risk Management for AI Features
- **Capstone:** Write a PRD for an AI feature using everything you've learned

---

## Free Resource Index
(By unit — detailed links and reviews below)

| Unit | Resource | Type | Time | Why It Matters |
|------|----------|------|------|---|
| 1–2 | Anthropic's "Building Claude" | Blog series | 1.5h | Best non-technical LLM explainer |
| 1–2 | 3Blue1Brown "Neural Networks" (partial) | Video | 2h | Intuitive foundations (skip heavy math) |
| 1–3 | LLM Index (Epoch.ai) | Interactive | 30m | Model landscape and tradeoffs |
| 4 | "RAG from Scratch" (Andrew Ng) | Video | 1h | Practical RAG fundamentals |
| 4–5 | LangChain documentation | Reference | 2h | See RAG/Agent patterns in action |
| 5 | OpenAI Agents cookbook | Code examples | 1.5h | Tool use patterns |
| 6 | Patterns for AI Engineering | Free book | 2h | RAG vs. fine-tuning decision framework |
| 7–8 | Replit's "Ship AI Products" | Course | 1.5h | Product + metrics mindset |

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
- Keep a running "AI PM Glossary" as you go (see separate file)

---

## Glossary (Quick Reference)

### Core Concepts

**Token**
- Smallest unit the LLM processes. ~1 token ≈ 4 characters in English
- Matters for: cost (charged per token), latency, context window limits

**Context Window**
- Maximum number of tokens the model can "see" at once
- Claude 3.5: 200k tokens (~150k words); GPT-4: 128k
- Tradeoff: Larger windows = more grounding, higher cost/latency

**Temperature**
- Controls randomness (0 = deterministic, 1 = creative)
- 0–0.3: Factual tasks (QA, summarization)
- 0.7–1: Creative tasks (brainstorming, ideation)

**Prompt Engineering**
- Writing + structure to get better outputs
- Few-shot: Showing examples in the prompt
- Chain-of-thought: "Let's think step by step"

**Hallucination**
- LLM confidently making up false information
- Common with factual queries without grounding
- RAG + retrieval fixes this partially

**Fine-tuning**
- Retraining the model on custom data (expensive, slow)
- Use when: Task requires domain language or very specific format
- Don't use when: You can solve it with prompting or RAG

**Retrieval-Augmented Generation (RAG)**
- Feed the LLM relevant context documents before asking a question
- Reduces hallucinations, enables domain knowledge
- Tradeoff: Adds latency, requires vector DB + embedding model

**Agent / Agentic Loop**
- System that decides which tools to call and in what order
- LLM reasons → picks a tool → executes → loops until done
- Examples: Customer support bot, data analysis assistant

**Vector Embedding**
- Converts text into a numerical representation (list of numbers)
- Similar texts → similar embeddings
- Used for semantic search (RAG retrieval step)

**LLM vs. Foundation Model vs. Large Language Model**
- **Foundation Model:** Big model trained on broad data (can do many tasks)
- **LLM:** Foundation model trained on text
- **Generative AI:** Broader category (images, video, audio)

---

## Assumptions & Scope

**What This Covers:**
- Text-based LLMs (ChatGPT, Claude, Llama, etc.)
- Product strategy for AI features (not ML ops, MLOps, or data engineering)
- Evaluation and metrics for AI outputs
- When to build vs. buy vs. partner

**What This Doesn't Cover:**
- Deep learning math or neural network internals
- Training your own LLM from scratch (not practical for most PMs)
- Computer vision, multimodal, or non-text AI
- Advanced prompt engineering recipes (covered lightly; see resources for depth)

---

## Success Criteria

By end of Week 3, you should be able to:

✓ Explain to a CEO why an LLM-based feature works (and its limitations)
✓ Evaluate a technical proposal: "Should we fine-tune, use RAG, or just prompt?"
✓ Write user stories + acceptance criteria for an AI feature
✓ Define success metrics for AI outputs (accuracy, latency, cost, user satisfaction)
✓ Spot red flags in an AI roadmap (hallucination risk, token cost, data privacy)
✓ Read a research paper and extract what's relevant to your product

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
4. Keeps predicting until it outputs a period (stop signal)
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
- **Cost:** LLM APIs charge per token (e.g., $0.003 per 1k input tokens)
- **Speed:** Processing 100k tokens takes longer than 1k
- **Limits:** Context window = max tokens you can feed the model

**Rule of Thumb:** ~1 token ≈ 4 characters or 0.75 words

### Context Window: The Model's Memory

The **context window** is the maximum number of tokens the model can process at once. It's the model's working memory.

**Current Models:**
- Claude 3.5 Sonnet: 200k tokens (~150,000 words)
- GPT-4 Turbo: 128k tokens
- Llama 2: 4k tokens (older)
- Your custom fine-tuned model: Depends on your setup

**What Fits in 200k Tokens?**
- ~150 pages of text
- A medium-sized codebase (50k lines)
- A conversation + 20 relevant documents

**Product Implication:**
If your feature needs to analyze a 500-page contract, you need RAG (see Week 2) or chunking strategy. You can't just pass it all at once.

### Temperature: Randomness Dial

When the model predicts the next token, it doesn't always pick the most likely one. It samples from a probability distribution.

**Temperature = 0:**
- Always pick the most likely token
- Deterministic (same input = same output)
- Use for: Customer support scripts, factual Q&A, code generation

**Temperature = 0.7:**
- Mix of likely and less-likely tokens
- Somewhat variable
- Use for: General chat, summaries, creative content

**Temperature = 1.0:**
- High randomness
- Very creative but less reliable
- Use for: Brainstorming, ideation

**PM Implication:**
If you're building a chatbot that answers FAQs, use temperature 0. If you're building a creative writing assistant, use 0.7–1.

---

### Reading & Resources

**Essential:**
1. **Anthropic Blog: "How Claude Works"** (20 min read)
   - URL: https://www.anthropic.com/research/claude-architecture
   - Best non-technical explanation of LLM behavior
   - Focus on: "Training" and "Inference" sections

2. **3Blue1Brown: "Neural Networks" (Episodes 1–2 only)** (20 min video)
   - URL: https://www.youtube.com/watch?v=aircAruvnKk
   - Skip the math; watch for intuition
   - Stop after Episode 2 (don't need backpropagation deep dive)

**Optional Deep Dive:**
- OpenAI's "Language Models are Unsupervised Multitask Learners" (paper summary, not full paper)
- Attention Is All You Need (visual explanation, not math)

---

### Self-Check: Do You Understand Unit 1?

After reading, you should be able to answer:

1. **"Why does my LLM hallucinate?"** — Because it's predicting the next token based on patterns, not retrieving facts. Without external context (RAG), it can confidently output false information.

2. **"If I double my context window, what happens?"** — Cost and latency increase, but you can feed more context. Useful for longer documents or conversations.

3. **"What's the difference between training and inference?"** — Training is when Anthropic built the model (expensive, one-time). Inference is when you use it (you pay per token).

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
- Reasoning through multi-step problems
- Creative writing and brainstorming
- Translation

**What LLMs Struggle With:**
- Counting (e.g., "Count the words in this sentence")
- Recent events (knowledge cutoff)
- Math with large numbers
- Perfect factuality (hallucinations)
- Multi-step logic requiring perfect accuracy (medical diagnosis, legal contracts)
- Handling ambiguous instructions

**As a PM:** This shapes feature scope. If your feature requires hallucination-free factual accuracy, RAG is mandatory. If it needs perfect math, add a calculator tool.

### Hallucinations: Confident Lies

A hallucination is when the model generates plausible-sounding but false information *while appearing confident*.

**Why It Happens:**
- The model is predicting tokens, not retrieving from a database
- It's pattern-matching from training data
- If the pattern says "Paris is probably the capital of France," it outputs that even if you asked about Italy

**Example:**
```
User: "Who is the current CEO of Acme Corp?"
Model (trained in 2022): "John Smith has been CEO since 2019."
Reality: Sarah Chen became CEO in 2024.
Problem: Model outputs old info confidently
```

**How to Reduce Hallucinations:**
1. **RAG:** Feed the model current/relevant documents
2. **Retrieval verification:** Have the model cite sources
3. **Lower stakes tasks:** Use for draft-writing, not legal advice
4. **Temperature 0:** Reduces creativity, increases reliability

**PM Implication:** If your feature answers factual questions about dynamic data (stock prices, company news, user-specific info), use RAG or live APIs.

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
- Don't build features that require pixel-perfect consistency
- QA testing is harder (same input, slightly different output each time)

### Context Window & Grounding

The context window is your tool for grounding the model.

**Scenario 1: No Context**
```
User: "Is this company a good investment?"
Model: Hallucinates based on training data
Risk: High
```

**Scenario 2: With Context (RAG)**
```
User: "Is this company a good investment?"
System: Retrieves latest 10-K, earnings report, news
Model: Summarizes retrieved docs
Risk: Lower (assuming docs are accurate)
```

**PM Implication:** Design for context. What documents, APIs, or databases should feed into the LLM?

---

### Reading & Resources

**Essential:**
1. **Anthropic: "Constitutional AI & Safety"** (15 min)
   - Understanding limitations by design
   - URL: https://www.anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback

2. **OpenAI's "Limitations of Language Models"** (blog post, 10 min)
   - URL: https://openai.com/blog/language-models-are-few-shot-learners
   - Focus on capability boundaries

**Optional:**
- Hallucination studies (academic, skip for now; revisit if building fact-critical features)

---

### Self-Check: Do You Understand Unit 2?

1. **"My support team is concerned about the chatbot giving wrong answers. What do I do?"** — Implement RAG to ground responses in your knowledge base, and tune temperature low. Add a "confidence score" or citation so agents can verify.

2. **"Can I use an LLM to diagnose medical conditions?"** — Not alone. It hallucinates. You'd need: strict guardrails, human review, integration with medical databases, and legal liability coverage.

3. **"Why is my QA testing flaky?"** — Temperature > 0 means outputs vary. Use temperature = 0 for testing, or build tests that check for semantic correctness, not exact match.

---

## Unit 3: Commercial LLM Landscape

### The Big Players

| Model | Maker | Cost (per 1M tokens) | Speed | Best For | Notes |
|-------|-------|-----|-------|----------|-------|
| Claude 3.5 Sonnet | Anthropic | $3 input, $15 output | Fast | Balanced reasoning + safety | Best all-rounder; 200k context |
| GPT-4o | OpenAI | $5 input, $15 output | Fast | General-purpose, multimodal | Good reasoning; 128k context |
| Llama 2 70B | Meta (open-source) | $0.99 input, $0.99 output (via API) | Slow | Cost-sensitive, on-premise | Open-source; lower quality |
| Gemini 2.0 | Google | $2.50 input, $10 output | Very fast | Long context, search integration | 2M context window (experimental) |
| Mixtral 8x7B | Mistral (open-source) | $0.27 input, $0.81 output | Fast | Budget-conscious | Emerging; lower quality |

### Key Tradeoffs

**Cost vs. Quality:**
- Claude 3.5 Sonnet: Higher cost, better reasoning
- Llama 2: Lower cost, weaker on complex tasks
- Use Llama for simple classification; Claude for nuanced analysis

**Speed vs. Reasoning:**
- Fastest: GPT-4o, Gemini 2.0 (milliseconds)
- Better reasoning: Claude 3.5 Sonnet (seconds, but more accurate)
- Use fast models for chat; reasoning models for batch/offline analysis

**Context Window:**
- Claude: 200k (great for docs, code)
- GPT-4: 128k
- Gemini: 2M (for research, code review, long documents)

**Ecosystem:**
- OpenAI: Most integrations, best DevOps tooling
- Anthropic: Best safety/alignment, great documentation
- Meta: Open-source (you run it yourself)

### Decision Tree: Which Model?

```
Do you need sub-second latency for chat?
├─ Yes → GPT-4o or Gemini 2.0
└─ No → Go to Q2

Q2: Is cost critical (< $1k/month)?
├─ Yes → Llama 2 or Mixtral (self-hosted or cheap API)
└─ No → Go to Q3

Q3: Do you need long context (>100k tokens) or safety?
├─ Safety = Claude 3.5 Sonnet
├─ Long context = Gemini 2.0
└─ Balanced = Claude 3.5 Sonnet
```

### Open-Source vs. Closed Models

**Closed (OpenAI, Anthropic, Google):**
- ✓ Best quality
- ✓ No infrastructure burden
- ✗ Vendor lock-in
- ✗ Data privacy concerns (your inputs may be logged)
- Cost: Pay per inference

**Open-Source (Llama, Mistral):**
- ✓ Run on your servers (privacy)
- ✓ Customize / fine-tune
- ✓ Lower long-term cost at scale
- ✗ Weaker out-of-box quality
- ✗ You manage infrastructure
- Cost: Hardware + ops

**PM Implication:**
- Prototype with OpenAI/Anthropic (fast, no ops)
- If scaling or sensitive data: evaluate self-hosted open-source

---

### Reading & Resources

**Essential:**
1. **Epoch.ai: LLM Leaderboard** (15 min interactive)
   - URL: https://epoch.ai/api-track
   - Filter by cost, speed, reasoning ability
   - Updated monthly

2. **Hugging Face: Open LLM Leaderboard** (10 min)
   - URL: https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard
   - Compare open-source models
   - See benchmarks

3. **Anthropic vs. OpenAI: Comparative Analysis** (blog post, 15 min)
   - URL: https://www.anthropic.com/research/constitutionalaim
   - Understand the philosophy differences

---

### Self-Check: Do You Understand Unit 3?

1. **"We need to launch next week and cost is tight. What model?"** — Llama 2 via Replicate ($0.99/M tokens) or self-hosted. Quality hit, but 10x cheaper than Claude.

2. **"Our enterprise customer won't let us send data to OpenAI servers."** — Self-hosted Llama 2 on your infrastructure, or Anthropic (more privacy-focused).

3. **"We're processing 10B tokens/month. What's the cost difference between Claude and GPT-4?"** — Claude: ~$150k/month. GPT-4: ~$200k/month. At scale, self-hosted Llama might be $50k/month on hardware.

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

| Dimension | Claude 3.5 Sonnet | GPT-4o | Llama 2 70B |
|-----------|-----------|---------|-----------|
| **Reasoning Quality** | | | |
| **Cost (per 1M tokens)** | | | |
| **Latency (ms)** | | | |
| **Context Window** | | | |
| **Safety/Alignment** | | | |
| **Best For This Use Case?** | | | |
| **Trade-offs** | | | |

**Write 2–3 Sentences:** Which would you pick and why?

**Example Answer:**
> For a customer support chatbot, I'd pick Claude 3.5 Sonnet. It's best at nuanced reasoning (handling edge cases in support), has a 200k context window (can hold customer history + entire knowledge base), and Anthropic's constitutional AI makes it safer for public-facing use. Cost is ~$3k/month at our scale, which is acceptable. GPT-4o would be faster but less safe; Llama would be cheaper but require self-hosting and would struggle with complex support scenarios.

---

**End of Week 1 (Units 1–3)**

You now understand:
- How LLMs work (token prediction, training, inference)
- Their limitations (hallucination, stochasticity, knowledge cutoff)
- The commercial landscape (which model for which job)

**Time Spent:** ~12–15 hours
**Next:** Week 2 — Augmenting LLMs with Retrieval & Agents

