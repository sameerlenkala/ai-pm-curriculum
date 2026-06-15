# AI PM Curriculum: Curated Free Resources

A ranked list of the best free courses, blogs, papers, and tools to supplement each unit. All links have been verified and are free (no paywalls). Check resource dates — AI moves fast.

---

## Unit 1: What Are LLMs? (Tokens, Training, Inference)

### Tier 1 (Essential — Start Here)

**1. Anthropic Research Blog**
- URL: https://www.anthropic.com/research
- Type: Blog posts and explainers
- Time: 20–30 min (browse for training/inference topics)
- Why: First-person explanations of LLM fundamentals from an LLM maker
- What to Read: Look for posts on scaling, training, and "how Claude works"
- Action: Summarize in 1 paragraph: "What is an LLM and how does it work?"

**2. 3Blue1Brown: "Neural Networks" (Episodes 1–2 ONLY)**
- URL: https://www.youtube.com/watch?v=aircAruvnKk
- Type: Video series
- Time: 30 min (stop after Episode 2)
- Why: Best visual, intuitive explanation of how neural networks learn — no math required
- What to Watch: Stop after "Gradient Descent"; skip backpropagation
- Action: After watching, explain "How does a network learn?" out loud to someone

**3. Hugging Face: NLP Course — Chapter 1**
- URL: https://huggingface.co/learn/nlp-course/chapter1/1
- Type: Interactive course
- Time: 20 min
- Why: Good hands-on mental model of how LLMs are structured
- What to Read: Skim for concepts; don't memorize architecture details
- Action: Draw a simple diagram of how text flows through a Transformer

---

### Tier 2 (Optional Deep Dive)

**4. "Attention Is All You Need" — Visual Summary**
- URL: https://medium.com/@b.terracer/attention-is-all-you-need-summary-d36d2c8f71a1
- Type: Medium article (summary, not the original paper)
- Time: 15 min
- Why: Understand what "Transformer" architecture means at an intuitive level
- Note: Read this summary; the original paper is too math-heavy for most PMs

**5. Papers With Code: NLP Leaderboards**
- URL: https://paperswithcode.com/area/natural-language-processing
- Type: Interactive leaderboard
- Time: 15 min browsing
- Why: See what tasks LLMs excel at vs. struggle with
- Action: Find 3 tasks where Claude outperforms GPT-4, and 3 where it loses

---

## Unit 2: LLM Behavior & Limitations

### Tier 1 (Essential)

**1. Anthropic: "Constitutional AI & Safety" (Blog Post)**
- URL: https://www.anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback
- Type: Blog + explainer
- Time: 15–20 min
- Why: Understand how modern LLMs are trained to reduce hallucination and harmful outputs
- What to Read: Focus on "How is Constitutional AI different from standard training?"
- Action: Write down 2 ways hallucination happens and 1 way to prevent each

**2. Prompting Guide: LLM Limitations and Failure Modes**
- URL: https://www.promptingguide.ai/introduction/basics
- Type: Free online guide
- Time: 15 min
- Why: Clear, practical overview of what LLMs can't do
- What to Read: Sections on limitations, biases, and failure modes
- Action: List 5 tasks LLMs struggle with that are relevant to your product domain

**3. "Hallucinations in LLMs: A Survey" (Paper Summary)**
- URL: https://huggingface.co/papers/2309.01219
- Type: Hugging Face paper digest
- Time: 10 min
- Why: Understand the different types of hallucinations (factual, logical, temporal)
- Note: Read the summary tab only; don't read the full paper

---

### Tier 2 (Optional)

**4. "On the Dangers of Stochastic Parrots" — Summary**
- URL: https://medium.com/@emilymbender/on-the-dangers-of-stochastic-parrots-6f6eff39f9e5
- Type: Medium article
- Time: 20 min
- Why: Understand bias and societal risks of large language models
- Note: This is a summary of the original academic paper; read summary, not original

**5. LLM Benchmark Tracker**
- URL: https://paperswithcode.com/area/natural-language-processing
- Type: Interactive leaderboard
- Time: 15 min browsing
- Why: See empirical evidence of where LLMs succeed and fail across tasks

---

## Unit 3: Commercial LLM Landscape

### Tier 1 (Essential)

**1. Epoch.ai: Model Tracker**
- URL: https://epoch.ai/
- Type: Interactive dashboards
- Time: 15–20 min
- Why: Best live comparison of all major models on cost, speed, and quality
- What to Do: Browse the model benchmarks and cost comparisons; filter by your requirements
- Action: Answer: Which model is fastest? Cheapest? Best reasoning? Fill in your Capability Matrix.

**2. Anthropic: Claude Models & Pricing**
- URL: https://www.anthropic.com/pricing
- Type: Official product/pricing page
- Time: 10 min
- Why: Understand the Haiku / Sonnet / Opus tiers — cost, context, and use cases
- Action: Note cost per 1M tokens for each tier; calculate monthly cost at your estimated volume

**3. OpenAI: Model Reference**
- URL: https://platform.openai.com/docs/models
- Type: Official documentation
- Time: 10 min
- Why: Understand GPT-4o vs. o1 vs. o3 — what each is for and how they differ
- Action: Compare GPT-4o (general purpose) vs. o3 (reasoning) on latency and cost

**4. Google: Gemini Models Overview**
- URL: https://ai.google.dev/gemini-api/docs/models/gemini
- Type: Official documentation
- Time: 10 min
- Why: Understand Gemini 2.0 Flash (cheap/fast) vs. Gemini 2.5 Pro (long context)
- Action: Note the context window size and cost difference between Flash and Pro

**5. Meta: Llama Models**
- URL: https://www.llama.com/
- Type: Official site
- Time: 10 min
- Why: Understand open-source positioning, Llama 3.x quality, and commercial licensing
- Action: Note: Can you use Llama 3.3 commercially? What are the self-hosting requirements?

---

### Tier 2 (Optional)

**6. Hugging Face: Open LLM Leaderboard**
- URL: https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard
- Type: Interactive leaderboard
- Time: 10 min
- Why: Compare open-source models (Llama, Mistral, Gemma, etc.) on quality benchmarks
- Action: Sort by average score; identify the top 3 open-source models and their trade-offs

**7. Prompting Guide: Model Comparisons**
- URL: https://www.promptingguide.ai/models/models
- Type: Comparison guide
- Time: 20 min
- Why: Structured decision framework for model selection
- Action: Use the comparison as a starting point for your Unit 3 self-check

---

## Unit 4: Retrieval-Augmented Generation (RAG)

### Tier 1 (Essential)

**1. DeepLearning.AI: "Building and Evaluating Advanced RAG"**
- URL: https://www.deeplearning.ai/short-courses/building-evaluating-advanced-rag/
- Type: Free video course (Andrew Ng)
- Time: 1–1.5 hours
- Why: Best practical intro to RAG — covers retrieval pipeline, chunking, evaluation
- What to Learn: How indexing, retrieval, and generation fit together
- Action: After watching, sketch a RAG architecture diagram for your use case

**2. LangChain: RAG Tutorial (Official)**
- URL: https://python.langchain.com/docs/tutorials/rag/
- Type: Code tutorial + documentation
- Time: 45–60 min (reading + skimming code)
- Why: See actual RAG implementation; LangChain is the most common RAG framework
- What to Do: Read through the flow; don't memorize code — understand the steps
- Action: Write pseudocode: Chunk → Embed → Store → Retrieve → Generate

**3. Pinecone: "What is a Vector Database?"**
- URL: https://www.pinecone.io/learn/vector-database/
- Type: Blog post with diagrams
- Time: 15 min
- Why: Understand how RAG stores and retrieves embeddings at scale
- Action: Explain in 2 sentences: "What is a vector database and why does RAG need one?"

**4. LlamaIndex: Chunking Strategies**
- URL: https://docs.llamaindex.ai/en/stable/optimizing/production_rag/
- Type: Documentation
- Time: 15 min
- Why: Understand how chunk size affects retrieval quality
- Action: List 3 chunking strategies (fixed-size, sentence-based, semantic) and when to use each

---

### Tier 2 (Optional)

**5. "RAG for LLMs: A Survey" (Paper Summary)**
- URL: https://huggingface.co/papers/2312.10997
- Type: Paper summary on Hugging Face
- Time: 20 min
- Why: Comprehensive overview of RAG approaches and research directions
- Note: Read the summary; skip the full paper

**6. RAGAS: RAG Evaluation Framework (GitHub)**
- URL: https://github.com/explodinggradients/ragas
- Type: Open-source library + documentation
- Time: 30 min (read docs)
- Why: Standard framework for measuring RAG quality — covers retrieval precision, faithfulness, answer relevance
- Action: Understand the 4 metrics: Context Precision, Context Recall, Faithfulness, Answer Relevance

---

## Unit 5: Agents, Tool Use & Agentic Loops

### Tier 1 (Essential)

**1. Lilian Weng: "LLM-powered Autonomous Agents"**
- URL: https://lilianweng.github.io/posts/2023-06-23-agent/
- Type: Long-form blog post (authoritative, widely cited)
- Time: 45–60 min
- Why: The best conceptual overview of agentic loops, tool use, memory, and planning
- What to Read: Focus on "Agent Components" and "Tool Use" sections
- Action: Summarize the ReAct pattern (Reason → Act → Observe) in 1 paragraph

**2. Anthropic: Tool Use Documentation**
- URL: https://docs.anthropic.com/en/docs/build-with-claude/tool-use
- Type: Official documentation
- Time: 20 min
- Why: See how Claude handles tool definitions, tool calls, and responses
- What to Learn: Tool schema format, how the model decides when to call a tool
- Action: Write a tool definition (in plain language) for a tool relevant to your use case

**3. OpenAI: Function Calling Guide**
- URL: https://platform.openai.com/docs/guides/function-calling
- Type: Official documentation
- Time: 20 min
- Why: Understand the standard tool-use pattern across providers
- Action: Compare how OpenAI and Anthropic define tools — what's similar, what's different?

**4. Anthropic: Model Context Protocol (MCP)**
- URL: https://www.anthropic.com/news/model-context-protocol
- Type: Blog post + specification
- Time: 20 min
- Why: MCP is becoming the standard way to connect LLMs to external tools; important for agent architecture decisions
- Action: Explain in 2 sentences: "What problem does MCP solve, and why does it matter for PMs?"

---

### Tier 2 (Optional)

**5. OpenAI Cookbook: Agent Examples**
- URL: https://github.com/openai/openai-cookbook
- Type: GitHub code examples
- Time: 1 hour browsing
- Why: See real agent patterns (search, database queries, multi-step workflows)
- Action: Find 1 example you understand and could explain to a non-technical stakeholder

**6. "Multi-Agent Systems" (Research Overview)**
- URL: https://huggingface.co/papers/2308.03675
- Type: Paper summary
- Time: 20 min
- Why: Understand how multiple agents can coordinate on complex tasks
- Note: Skim; don't memorize

---

## Unit 6: Fine-Tuning vs. Prompting vs. RAG vs. Reasoning Models

### Tier 1 (Essential)

**1. OpenAI: Fine-Tuning Guide**
- URL: https://platform.openai.com/docs/guides/fine-tuning
- Type: Official documentation
- Time: 15 min
- Why: Clear decision framework from a model provider on when fine-tuning makes sense
- What to Read: "When to use fine-tuning" and "Preparing training data"
- Action: For 3 tasks from your domain, decide: fine-tune or prompt?

**2. Prompting Guide: Techniques Overview**
- URL: https://www.promptingguide.ai/techniques
- Type: Interactive guide
- Time: 20 min
- Why: Master zero-shot, few-shot, and chain-of-thought prompting — the cheapest tools in your arsenal
- What to Learn: Few-shot examples, chain-of-thought, in-context learning
- Action: Write a few-shot prompt for a task relevant to your use case

**3. Anthropic: Prompt Engineering Guide**
- URL: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview
- Type: Official documentation
- Time: 20 min
- Why: Anthropic's own guidance on getting the best outputs from Claude
- Action: Apply 2 techniques from this guide to a prompt you're working on

**4. Anthropic: Prompt Caching**
- URL: https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching
- Type: Official documentation
- Time: 15 min
- Why: Understand how to reduce costs by 80–90% on high-volume features with repeated context
- Action: Identify 1 place in your product where prompt caching would apply

**5. OpenAI: Structured Outputs**
- URL: https://platform.openai.com/docs/guides/structured-outputs
- Type: Official documentation
- Time: 15 min
- Why: Understand how to guarantee the model returns valid, parseable JSON
- Action: Design a JSON schema for an AI feature output in your product

---

### Tier 2 (Optional)

**6. "In-Context Learning Survey" (Research)**
- URL: https://huggingface.co/papers/2301.00234
- Type: Paper summary
- Time: 15 min
- Why: Understand how and why few-shot learning works under the hood

**7. Anthropic: Extended Thinking (Reasoning)**
- URL: https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking
- Type: Official documentation
- Time: 15 min
- Why: Understand when and how to use reasoning mode for complex tasks
- Action: Identify 1 use case in your product where extended thinking would improve quality

---

## Unit 7: AI Product Strategy

### Tier 1 (Essential)

**1. a16z: "10 Questions to Ask Before Building an AI Product"**
- URL: https://a16z.com/how-to-evaluate-ai-products/
- Type: Blog post (Andreessen Horowitz)
- Time: 15 min
- Why: The 10 questions here are a practical feasibility checklist for any AI feature
- Action: Apply all 10 questions to your proposed feature before Week 3 deliverable

**2. "Jobs-to-Be-Done Framework" (Clayton Christensen)**
- URL: https://www.youtube.com/watch?v=F0e9tZBjZH8
- Type: YouTube video (10 min)
- Time: 10 min
- Why: Forces you to frame AI features around user problems, not technology capabilities
- Action: Reframe your AI feature: "What job does the user want done, and how does AI help them do it faster/better?"

**3. DeepLearning.AI Short Courses: AI Product & Strategy**
- URL: https://www.deeplearning.ai/short-courses/
- Type: Free video courses
- Time: 2–3 hours (browse catalog for product/strategy-focused courses)
- Why: Product thinking applied to AI — feasibility, GTM, metrics mindset
- Action: Pick 1 course relevant to your use case and complete it this week

---

### Tier 2 (Optional)

**4. Chip Huyen: "Designing Machine Learning Systems" (Blog)**
- URL: https://huyenchip.com/machine-learning-systems-design/
- Type: Long-form blog / free book chapters
- Time: 1 hour (skim; use as reference)
- Why: Deep dive into real-world AI system design — reliability, deployment, monitoring
- Note: Technical at times; skim for PM-relevant sections

**5. "Building AI Products" — Hugging Face Blog**
- URL: https://huggingface.co/blog
- Type: Blog
- Time: 30 min browsing
- Why: Case studies and patterns from teams shipping real AI products
- Action: Find 1 post about a use case similar to yours and note their lessons learned

---

## Unit 8: Metrics, Evaluation & Risk Management

### Tier 1 (Essential)

**1. Anthropic: Evaluations (Evals) Overview**
- URL: https://www.anthropic.com/research/evaluations
- Type: Research page + blog posts
- Time: 20–30 min
- Why: Understand how Anthropic thinks about evaluating model quality and safety
- Action: For your use case, define 1 accuracy metric and 1 health metric

**2. RAGAS: RAG Evaluation Framework**
- URL: https://github.com/explodinggradients/ragas
- Type: Open-source library + documentation
- Time: 30 min (read docs, understand metrics)
- Why: The standard framework for measuring RAG system quality
- Action: Understand the 4 core metrics: Context Precision, Context Recall, Faithfulness, Answer Relevance

**3. NIST AI Risk Management Framework**
- URL: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf
- Type: Government standard (PDF)
- Time: Skim Sections 1, 3, and 4 (~45 min)
- Why: The most authoritative framework for AI risk — covers bias, fairness, safety, and governance
- Action: List 5 risks from the framework that are relevant to your AI feature

**4. "Measuring Hallucination in LLMs"**
- URL: https://huggingface.co/blog/hallucination
- Type: Blog post
- Time: 15 min
- Why: Specific techniques for detecting and quantifying hallucinations in your feature
- Action: Design a simple test: what 10 queries would you run to detect hallucinations in your feature?

---

### Tier 2 (Optional)

**5. "Fairness and Bias in AI: A Survey"**
- URL: https://huggingface.co/papers/2301.01814
- Type: Paper summary
- Time: 20 min
- Why: Understand bias beyond accuracy — representation, allocation, and measurement

**6. "Cost Optimization for LLM Applications"**
- URL: https://www.hyperplane.dev/p/cost-optimization-for-llm-applications
- Type: Blog post
- Time: 20 min
- Why: Practical techniques for managing LLM costs at scale — caching, batching, model routing
- Action: List 3 cost reduction techniques applicable to your feature

---

## Bonus: Hands-On Tools to Try

Spend 1–2 hours exploring these. They're not reading — they're interactive learning.

**1. Claude (Anthropic)**
- URL: https://claude.ai
- What to Do: Test prompts, experiment with temperature and system prompts
- Learning: Experience Claude's behavior firsthand; try edge cases and see how it fails

**2. ChatGPT (OpenAI)**
- URL: https://chat.openai.com
- What to Do: Run the same prompts on ChatGPT that you ran on Claude
- Learning: See differences in tone, structure, and failure modes between models

**3. LangChain Quickstart**
- URL: https://python.langchain.com/docs/get_started/quickstart
- What to Do: Follow the quickstart tutorial (beginner-friendly)
- Learning: See RAG, chains, and agents in actual code — even if you don't write code yourself

**4. Prompting Guide — Interactive Playground**
- URL: https://www.promptingguide.ai/
- What to Do: Work through techniques: chain-of-thought, zero-shot, few-shot
- Learning: Hands-on prompting practice with immediate feedback

**5. Hugging Face Spaces**
- URL: https://huggingface.co/spaces
- What to Do: Try community-built demos (RAG chatbots, summarizers, classifiers)
- Learning: See what's possible with open-source models in a low-code environment

**6. Anthropic Cookbook**
- URL: https://github.com/anthropics/anthropic-cookbook
- What to Do: Browse code examples — RAG, tool use, structured output, prompt caching
- Learning: See production patterns for the techniques covered in Unit 6

---

## Resource Efficiency Guide

**If You Have 10 Hours:**
1. Anthropic Research Blog — browse for LLM fundamentals (30 min)
2. 3Blue1Brown Neural Networks, Eps 1–2 (30 min)
3. Epoch.ai model tracker (20 min)
4. DeepLearning.AI RAG course (1.5 hours)
5. Lilian Weng: "LLM-powered Autonomous Agents" (45 min)
6. Prompting Guide: Techniques (20 min)
7. RAGAS evaluation framework docs (30 min)
8. Hands-on: Test prompts on Claude and ChatGPT (1 hour)
9. Write Week 1 + Week 2 deliverables (1.5 hours)
10. a16z: 10 Questions Before Building (15 min)

**If You Have 20 Hours:**
Add:
- HuggingFace NLP Course Ch. 1 (20 min)
- Unit 2 hallucination + Constitutional AI posts (30 min)
- Claude and OpenAI pricing pages (20 min)
- Anthropic tool use + MCP docs (40 min)
- OpenAI fine-tuning guide + Prompt caching docs (30 min)
- NIST AI Risk Framework (45 min)
- Week 3 PRD writing (1.5 hours)

**If You Have 40 Hours (Full Curriculum):**
- Complete all Tier 1 resources for every unit
- Spend 2–3 hours per unit hands-on: testing models, sketching architectures, writing prompts
- Complete all 3 weekly deliverables (Capability Matrix, Decision Tree, PRD)
- Explore Tier 2 resources for your most relevant units
- 3–4 hours on Anthropic Cookbook code examples (even just reading them builds intuition)

---

## How to Use This Resource List

**During Each Unit:**
1. Read Tier 1 resources (essential) — do the "Action" at the end of each
2. Skim Tier 2 resources if you want depth on that topic
3. Try hands-on tools if listed
4. Answer the unit's self-check questions

**Weekly:**
- Complete the deliverable (Capability Matrix, Decision Tree, PRD)
- Review the glossary in the Syllabus for unfamiliar terms
- Discuss with a colleague: "Explain what you learned this week in 5 minutes"

**Post-Curriculum:**
- Bookmark this file
- Return to specific sections when you hit a live decision at work
- Re-read Unit 6 (architecture decisions) and Unit 8 (metrics/risk) quarterly

---

## Feedback & Updates

AI moves fast. If a resource link breaks, a model is deprecated, or you find something better — note it. This is a living document.

Good luck with your learning.
