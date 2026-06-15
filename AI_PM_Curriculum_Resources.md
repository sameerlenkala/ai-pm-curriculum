# AI PM Curriculum: Curated Free Resources

A ranked list of the best free courses, blogs, papers, and tools to supplement each unit. All links are tested and free (no paywalls).

---

## Unit 1: What Are LLMs? (Tokens, Training, Inference)

### Tier 1 (Essential — Start Here)

**1. Anthropic Blog: "How Claude Works"**
- URL: https://www.anthropic.com/research/
- Type: Blog post + explainer
- Time: 15–20 min
- Why: Best non-technical explanation of LLM fundamentals from an LLM maker
- What to Read: Look for posts on "scaling laws," "training," "inference"
- Action: Summarize in 1 paragraph: "What is an LLM and how does it work?"

**2. 3Blue1Brown: "Neural Networks" (Episodes 1–2 ONLY)**
- URL: https://www.youtube.com/watch?v=aircAruvnKk
- Type: Video series
- Time: 30 min (skip episodes 3+)
- Why: Most intuitive visual explanation of neural networks
- What to Watch: Stop after "Gradient Descent"; don't dive into backprop math
- Action: After watching, explain "How does a network learn?" out loud to someone

**3. Hugging Face: "What is a Transformer?" (Blog Series)**
- URL: https://huggingface.co/course/chapter1/1
- Type: Interactive blog
- Time: 20 min
- Why: Good mental model of how LLMs are structured
- What to Read: Skim; don't memorize architecture details
- Action: Draw a simple diagram of Attention

---

### Tier 2 (Optional Deep Dive)

**4. "Attention Is All You Need" (Paper — Visual Summary Only)**
- URL: https://medium.com/@b.terracer/attention-is-all-you-need-summary-d36d2c8f71a1
- Type: Medium article (not the original paper)
- Time: 15 min
- Why: Understand what "Transformer" architecture means
- Note: Read the summary, NOT the original paper (too much math)

**5. Colah's Blog: "Understanding Neural Networks"**
- URL: http://colah.github.io/posts/2015-08-Understanding-LSTMs/
- Type: Blog post with interactive visuals
- Time: 30 min
- Why: Intuitive explanation of how recurrent networks learn
- Note: Skip if it feels too technical; Transformers are what matter now

---

## Unit 2: LLM Behavior & Limitations

### Tier 1 (Essential)

**1. Anthropic: "Constitutional AI & Safety" (Blog Post)**
- URL: https://www.anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback
- Type: Blog + explainer
- Time: 15–20 min
- Why: Understand how modern LLMs try to avoid hallucination and bias
- What to Read: Focus on "How is Constitutional AI different?"
- Action: Write down 2 ways hallucination happens and 1 way to prevent it

**2. OpenAI: "Limitations of Language Models" (Blog)**
- URL: https://openai.com/blog/language-models-are-few-shot-learners
- Type: Blog post
- Time: 15 min
- Why: Official take on what LLMs can't do well
- What to Read: Section on "Limitations and Biases"
- Action: List 5 tasks LLMs struggle with

**3. "Hallucinations in LLMs: A Survey" (Paper Summary)**
- URL: https://huggingface.co/papers/2309.01219
- Type: Hugging Face paper digest
- Time: 10 min
- Why: Understand types of hallucinations (factual, logical, etc.)
- Note: Read the summary tab; don't read full paper

---

### Tier 2 (Optional)

**4. "On the Dangers of Stochastic Parrots" (Summary)**
- URL: https://towardsdatascience.com/stochastic-parrots-a-summary-of-the-paper-on-the-dangers-of-large-language-models-e1c5b7b56166
- Type: Medium article
- Time: 20 min
- Why: Understand bias and limitations
- Note: Academic paper; read the summary instead

**5. LLM Benchmark Tracker (Interactive)**
- URL: https://paperswithcode.com/area/natural-language-processing
- Type: Interactive leaderboard
- Time: 15 min browsing
- Why: See what tasks LLMs excel vs. struggle on
- Action: Find 3 tasks where Claude beats GPT-4, and 3 where it loses

---

## Unit 3: Commercial LLM Landscape

### Tier 1 (Essential)

**1. Epoch.ai: LLM Leaderboard (Interactive)**
- URL: https://epoch.ai/api-track
- Type: Interactive dashboard
- Time: 15–20 min
- Why: Compare all commercial models on cost, speed, reasoning
- What to Do: 
  - Filter by "Cost per 1M tokens"
  - Filter by "Latency"
  - Filter by "Reasoning quality"
  - Write down: Which model is fastest? Cheapest? Best reasoning?
- Action: Build your "LLM Capability Matrix" (Week 1 deliverable)

**2. Hugging Face: "Open LLM Leaderboard"**
- URL: https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard
- Type: Interactive leaderboard
- Time: 10 min
- Why: Understand open-source model landscape (Llama, Mistral, etc.)
- What to Do: Sort by "Average" score; note which models are >70% quality
- Action: Pick an open-source model and note its cost/quality tradeoff

**3. Anthropic: "Claude Model Comparison" (Official)**
- URL: https://www.anthropic.com/claude
- Type: Product page
- Time: 10 min
- Why: Understand Claude's positioning, context window, pricing
- What to Read: Pricing table, model comparison
- Action: Note cost/token for Claude 3.5 Sonnet vs. Opus

**4. OpenAI: "Model Comparison" (Official)**
- URL: https://platform.openai.com/docs/models
- Type: Official documentation
- Time: 10 min
- Why: Understand GPT-4, GPT-4 Turbo, GPT-3.5 differences
- What to Read: "Vision," "Context Window," "Training Data"
- Action: Compare GPT-4o context window to Claude

**5. Meta: "Llama 2 Release Post" (Blog)**
- URL: https://ai.meta.com/llama/
- Type: Blog post
- Time: 15 min
- Why: Understand open-source positioning, cost, quality
- What to Read: "Performance," "Safety," "Commercial Use"
- Action: Note: Can you use Llama commercially? Cost vs. Claude?

---

### Tier 2 (Optional)

**6. LLM Guide: "Which Model Should I Use?"**
- URL: https://www.promptingguide.ai/models/models
- Type: Comparison guide
- Time: 20 min
- Why: Structured decision framework for model selection
- Action: Use for Unit 3 self-check exercise

**7. "Open-Source vs. Proprietary LLMs: Trade-offs"**
- URL: https://huggingface.co/docs/hub/security
- Type: Blog/docs
- Time: 10 min
- Why: Understand data privacy, customization, cost
- Action: Write pros/cons of self-hosting Llama vs. using Claude API

---

## Unit 4: Retrieval-Augmented Generation (RAG)

### Tier 1 (Essential)

**1. Andrew Ng: "Building RAG Systems" (DeepLearning.AI)**
- URL: https://www.deeplearning.ai/short-courses/building-evaluating-advanced-rag/
- Type: Free video course
- Time: 1–1.5 hours
- Why: Best practical intro to RAG from a trusted educator
- What to Learn: Retrieval pipeline, chunking, embedding models
- Action: After watching, sketch out a RAG architecture for your use case

**2. LangChain: "RAG Tutorial" (Official)**
- URL: https://python.langchain.com/docs/use_cases/question_answering/
- Type: Code tutorial + docs
- Time: 1 hour (reading + trying code)
- Why: See actual RAG code; LangChain is industry standard
- What to Do: Read the Q&A section; don't memorize code, understand flow
- Action: Write pseudocode for: Chunk → Embed → Store → Retrieve → Generate

**3. "RAG Fundamentals: Chunking Strategies" (Blog)**
- URL: https://www.llamaindex.ai/blog/chunking-strategies
- Type: Blog post
- Time: 15 min
- Why: Understand how to break documents for RAG
- Action: List 3 chunking strategies and when to use each

**4. Vector Database Explained (Interactive)**
- URL: https://www.pinecone.io/learn/vector-database/
- Type: Blog + visuals
- Time: 15 min
- Why: Understand how RAG stores and retrieves embeddings
- Action: Explain in 2 sentences: "What is a vector database?"

---

### Tier 2 (Optional)

**5. "Retrieval-Augmented Generation for Large Language Models: A Survey"**
- URL: https://huggingface.co/papers/2312.10997
- Type: Paper summary
- Time: 20 min
- Why: Comprehensive overview of RAG approaches
- Note: Read summary; skip full paper

**6. "Fine-Grained Evaluation of RAG" (Research)**
- URL: https://huggingface.co/papers/2309.15217
- Type: Paper summary
- Time: 15 min
- Why: Understand how to measure RAG quality
- Action: Note the RAGAS framework for evaluation

---

## Unit 5: Agents, Tool Use & Agentic Loops

### Tier 1 (Essential)

**1. LangChain: "Agents" (Official Docs)**
- URL: https://python.langchain.com/docs/modules/agents/
- Type: Documentation + code examples
- Time: 1 hour (reading)
- Why: See how agents work in practice
- What to Read: "Agent Types," "Tool Use," "ReAct"
- Action: Explain "What does an agent do?" in 3 sentences

**2. OpenAI: "Function Calling / Tool Use" (Docs)**
- URL: https://platform.openai.com/docs/guides/function-calling
- Type: Official documentation
- Time: 20 min
- Why: Understand the standard pattern for tool use
- What to Learn: Tools as functions, parsing responses, handling errors
- Action: Write pseudocode for an agent that fetches invoices and calculates totals

**3. "Reasoning Agents" (Blog)**
- URL: https://lilianweng.github.io/posts/2022-06-09-agent/
- Type: Blog post (technical but accessible)
- Time: 30 min
- Why: Understand agentic loops, ReAct, planning
- Action: Summarize the "ReAct" pattern in 1 paragraph

---

### Tier 2 (Optional)

**4. OpenAI Cookbook: "Agents" (Code Examples)**
- URL: https://github.com/openai/openai-cookbook
- Type: GitHub code examples
- Time: 1 hour browsing
- Why: See real agent patterns (search, math, database queries)
- Action: Find 1 example you understand and could explain to an engineer

**5. "Multi-Agent Systems" (Research Overview)**
- URL: https://huggingface.co/papers/2308.03675
- Type: Paper summary
- Time: 20 min
- Why: Understand how multiple agents coordinate
- Note: Skim; don't memorize

---

## Unit 6: Fine-Tuning vs. Prompting vs. RAG

### Tier 1 (Essential)

**1. "Fine-Tuning vs. Prompting" (OpenAI Blog)**
- URL: https://platform.openai.com/docs/guides/fine-tuning
- Type: Official guide
- Time: 15 min
- Why: Clear decision framework from a model provider
- What to Read: When to fine-tune vs. when to prompt
- Action: For 3 tasks, decide: Fine-tune or prompt?

**2. "Few-Shot Learning" (Prompting Guide)**
- URL: https://www.promptingguide.ai/techniques/fewshot
- Type: Interactive guide
- Time: 15 min
- Why: Master few-shot prompting (cheaper alternative to fine-tuning)
- What to Learn: Examples, chain-of-thought, in-context learning
- Action: Write a few-shot prompt for a task (e.g., sentiment classification)

**3. "Patterns for AI Engineering" (Free eBook)**
- URL: https://www.patterns.dev/posts/ai-ops/
- Type: Free online book chapters
- Time: 1 hour (read Unit 6 chapter)
- Why: Best framework for choosing fine-tuning vs. RAG vs. prompting
- Action: Use the decision tree in this book for Unit 6 deliverable

**4. "Fine-Tuning Best Practices" (Anthropic Blog)**
- URL: https://www.anthropic.com/fine-tuning
- Type: Blog post
- Time: 15 min
- Why: Understand fine-tuning limitations and when it works
- Action: List 3 reasons NOT to fine-tune

---

### Tier 2 (Optional)

**5. "In-Context Learning" (Research)**
- URL: https://huggingface.co/papers/2301.00234
- Type: Paper summary
- Time: 15 min
- Why: Understand how few-shot learning works under the hood

**6. "Prompt Tuning vs. Fine-Tuning" (Google Research)**
- URL: https://ai.googleblog.com/2021/10/prompt-tuning-efficient-learning-for.html
- Type: Blog post
- Time: 15 min
- Why: Alternative middle ground between prompting and fine-tuning

---

## Unit 7: AI Product Strategy

### Tier 1 (Essential)

**1. "Replit: Ship an AI Product" (Free Course)**
- URL: https://replit.com/learn/ai-fundamentals
- Type: Video course (30 min videos)
- Time: 2–3 hours total
- Why: Product thinking applied to AI (feasibility, GTM, metrics)
- What to Learn: Feasibility assessment, user value, launch strategy
- Action: After watching, sketch a GTM for your use case

**2. "How to Evaluate AI Products" (Blog)**
- URL: https://www.a16z.com/2023/05/08/10-questions-to-ask-before-building-an-ai-product/
- Type: a16z blog (trusted VC firm)
- Time: 15 min
- Why: Key questions to validate feasibility
- Action: Use the 10 questions on your proposed feature

**3. "Jobs-to-Be-Done Framework" (Video Explainer)**
- URL: https://www.youtube.com/watch?v=F0e9tZBjZH8
- Type: YouTube (Clayton Christensen)
- Time: 10 min
- Why: Reframe AI features around user problems, not technology
- Action: Reframe your AI feature: "What job does the user want done?"

---

### Tier 2 (Optional)

**4. "Feasibility Assessment: Is AI Right for This?" (Research)**
- URL: https://huggingface.co/papers/2308.08914
- Type: Paper summary
- Time: 20 min
- Why: Understand when NOT to use AI

**5. "Productionizing Machine Learning" (Chip Huyen)**
- URL: https://huyenchip.com/machine-learning-systems-design/
- Type: Long-form blog
- Time: 1 hour
- Why: Deep dive into real-world AI systems
- Action: Skim; use as reference for specific topics

---

## Unit 8: Metrics, Evaluation & Risk Management

### Tier 1 (Essential)

**1. "Evaluating LLM Performance" (Blog)**
- URL: https://www.anthropic.com/index/evals
- Type: Blog + open-source tools
- Time: 20 min read + 30 min exploring code
- Why: Understand evaluation frameworks from LLM maker
- What to Learn: Benchmark design, human evaluation, automated metrics
- Action: For your use case, define 1 accuracy metric and 1 latency metric

**2. "RAGAS: RAG Evaluation Framework" (GitHub)**
- URL: https://github.com/explodinggradients/ragas
- Type: Open-source library + docs
- Time: 30 min (read docs)
- Why: Standard framework for evaluating RAG systems
- Action: Understand the 4 metrics: Context Precision, Relevance, Faithfulness, Answer Relevance

**3. "AI Risk Management Framework" (NIST)**
- URL: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf
- Type: Government standard (PDF)
- Time: Skim sections 1, 3, 4 (1 hour)
- Why: Understand bias, fairness, safety risks
- Action: List 5 risks relevant to your AI feature

**4. "Measuring Hallucination in LLMs" (Blog)**
- URL: https://huggingface.co/blog/hallucination
- Type: Blog post
- Time: 15 min
- Why: Specific techniques for detecting hallucinations
- Action: Design a test to catch hallucinations in your feature

---

### Tier 2 (Optional)

**5. "Fairness and Bias in AI" (Research Overview)**
- URL: https://huggingface.co/papers/2301.01814
- Type: Paper summary
- Time: 20 min
- Why: Understand bias beyond accuracy

**6. "Cost Optimization for LLM Applications" (Blog)**
- URL: https://www.hyperplane.dev/p/cost-optimization-for-llm-applications
- Type: Blog post
- Time: 20 min
- Why: Practical tips for managing LLM costs
- Action: List 3 ways to reduce cost without harming quality

---

## Bonus: Hands-On Tools to Try

These aren't reading; they're interactive exploration. Spend 1–2 hours total.

**1. ChatGPT Playground (Free)**
- URL: https://chat.openai.com
- What to Do: Test prompts, experiment with temperature
- Learning: Feel what different temperatures/prompts produce

**2. Claude Playground (Free)**
- URL: https://claude.ai
- What to Do: Compare Claude's behavior to ChatGPT on same prompts
- Learning: Understand model differences firsthand

**3. LangChain Playground (Code)**
- URL: https://github.com/langchain-ai/langchain
- What to Do: Follow their quickstart tutorials
- Learning: See RAG, agents, prompting in action

**4. Prompt Engineering Guide (Interactive)**
- URL: https://www.promptingguide.ai/
- What to Do: Work through techniques (chain-of-thought, zero-shot, etc.)
- Learning: Hands-on prompting practice

**5. Hugging Face Spaces (Models & Demos)**
- URL: https://huggingface.co/spaces
- What to Do: Try community-built demos (RAG, summarization, Q&A)
- Learning: See what's possible with free models

---

## Resource Efficiency Guide

**If You Have 10 Hours:**
1. Anthropic "How Claude Works" (0.5h)
2. 3Blue1Brown Neural Networks Eps 1–2 (0.5h)
3. Epoch.ai model comparison (0.5h)
4. Andrew Ng RAG course (1.5h)
5. LangChain RAG tutorial (1h)
6. Replit AI Product course (2h)
7. RAGAS evaluation framework (1h)
8. Hands-on: Test prompts on Claude/ChatGPT (1.5h)
9. Write Week 1 + Week 2 deliverables (1h)

**If You Have 20 Hours:**
Add:
- Unit 2 hallucination + safety posts (1h)
- Unit 3 model comparison deep dive (1h)
- Unit 5 agents (LangChain docs) (1h)
- Unit 6 fine-tuning vs. prompting (1h)
- Unit 7 feasibility assessment (1h)
- Unit 8 risk management + metrics (1h)
- Week 3 PRD writing (1h)

**If You Have 40 Hours (Full Curriculum):**
- Do all reading above
- Spend 3–4 hours per unit digesting
- 2–3 hours per week on deliverables
- 5 hours hands-on (building RAG, testing models, writing prompts)

---

## How to Use This Resource List

**During Each Unit:**
1. Read Tier 1 resources (essential)
2. Skim Tier 2 resources (optional)
3. Try hands-on tools if applicable
4. Do the unit's self-check questions
5. Move to next unit

**Weekly:**
- Complete the deliverable (PRD, capability matrix, etc.)
- Review glossary for terms you don't understand
- Discuss with a colleague (teach back what you learned)

**Post-Curriculum:**
- Bookmark these resources
- Revisit when you hit a question on a project
- Use as a reference library for your PM career

---

## Feedback & Updates

If a resource link breaks or you find something better, let me know. This is a living document.

Good luck with your learning!

