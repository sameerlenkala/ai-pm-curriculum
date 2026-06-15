# AI PM Curriculum: Master Index

## What You're Getting

A **free, 3-week intensive curriculum** designed for non-technical Product Owners managing AI products.

**4 Files in This Package:**

1. **AI_PM_Curriculum_Syllabus.md** — Main curriculum content (Week 1: Foundations)
2. **AI_PM_Curriculum_Week2.md** — Advanced patterns (Week 2: RAG & Agents)
3. **AI_PM_Curriculum_Week3.md** — Product strategy & metrics (Week 3: Launch)
4. **AI_PM_Curriculum_Resources.md** — Curated free courses & tools (all units)
5. **AI_PM_Quick_Reference.md** — Cheat sheet for meetings (bookmark this)

---

## How to Use This Curriculum

### Option 1: Full 3-Week Intensive (Recommended)
- **Week 1:** Read Units 1–3 in Syllabus (~15 hours)
  - Supplement with resources from **Resources.md**
  - Complete Week 1 deliverable (LLM Capability Matrix)
- **Week 2:** Read Units 4–6 in Week 2 file (~15 hours)
  - Supplement with resources
  - Complete Week 2 deliverable (Architecture Decision Tree)
- **Week 3:** Read Units 7–8 in Week 3 file (~15 hours)
  - Supplement with resources
  - Complete capstone (AI Feature PRD)

**Total Time:** ~45 hours (10–15 hrs/week over 3 weeks)

### Option 2: Self-Paced (2–3 Months)
- Do 1 unit per week (2–4 hours/week)
- Use **Quick Reference.md** to apply learning immediately
- Complete deliverables at your own pace

### Option 3: Just-in-Time (Reference)
- Use **Quick Reference.md** for meetings/decisions
- Deep-dive into specific units when you need them
- Return to Syllabus/Week 2/Week 3 for context

---

## File Guide

### Syllabus.md (Start Here)
**Contains:** Units 1–3, glossary, 3-week overview
- Unit 1: What Are LLMs?
- Unit 2: LLM Behavior & Limitations
- Unit 3: Commercial LLM Landscape
- Week 1 deliverable: LLM Capability Matrix

**When to Use:**
- First week of learning
- Need to understand LLM fundamentals
- Reviewing glossary of AI terms

### Week2.md
**Contains:** Units 4–6
- Unit 4: Retrieval-Augmented Generation (RAG)
- Unit 5: Agents & Tool Use
- Unit 6: Fine-Tuning vs. Prompting vs. RAG
- Week 2 deliverable: Architecture Decision Tree

**When to Use:**
- Second week of learning
- Need to decide between RAG/fine-tuning/prompting
- Building agents for multi-step workflows
- Choosing how to augment LLMs

### Week3.md
**Contains:** Units 7–8 + Capstone
- Unit 7: AI Product Strategy
- Unit 8: Metrics & Risk Management
- Capstone: Write an AI Feature PRD
- Final glossary + post-curriculum resources

**When to Use:**
- Third week of learning
- Need to assess feasibility of AI feature
- Writing success metrics
- Identifying risks before launch
- Writing PRD for AI product

### Resources.md
**Contains:** Curated free resources for each unit
- Ranked by tier (Essential / Optional)
- Links to blogs, courses, code tutorials
- Time estimate for each resource
- Action items (what to do after reading)

**When to Use:**
- During each unit, to supplement reading
- Need to understand a topic more deeply
- Looking for hands-on code examples
- Want current events/latest research

### Quick Reference.md (Bookmark This)
**Contains:** Decision flowcharts, checklists, templates
- Model selection flowchart
- Architecture decision flowchart
- Risk checklist
- Glossary (one-liners)
- Red flags
- Meeting conversation starters

**When to Use:**
- In meetings (need quick answer)
- Making a decision (use flowchart)
- Reviewing an engineer's proposal
- Presenting to leadership
- Writing an email/memo

---

## Weekly Structure (If Doing 3-Week Intensive)

### Week 1: Foundations
**Read:** Syllabus.md (Units 1–3)
**Supplement:** Resources.md (Unit 1–3 sections)
**Hands-On:** Try prompts on Claude/ChatGPT; compare models on Epoch.ai
**Deliverable:** LLM Capability Matrix (pick a use case, compare 3 models)
**Time:** 12–15 hours
**Check-In:** Can you explain how LLMs work to a non-technical person?

### Week 2: Advanced Patterns
**Read:** Week2.md (Units 4–6)
**Supplement:** Resources.md (Unit 4–6 sections)
**Hands-On:** Try LangChain RAG tutorial; sketch agent flow
**Deliverable:** Architecture Decision Tree (for your use case: RAG vs. fine-tuning vs. prompting?)
**Time:** 12–15 hours
**Check-In:** Can you decide whether to fine-tune, prompt, or use RAG for any task?

### Week 3: Product & Launch
**Read:** Week3.md (Units 7–8)
**Supplement:** Resources.md (Unit 7–8 sections)
**Hands-On:** Write success metrics for your use case
**Deliverable:** 1-Page AI Feature PRD (using template in Week3.md)
**Time:** 12–15 hours
**Check-In:** Can you identify top 3 risks for your AI feature and write a PRD?

---

## How to Use the Resources File

**For Each Unit:**

1. Start with **Tier 1 (Essential)** resources
   - 15–30 min per resource
   - Do the "Action" at the end
2. Skim **Tier 2 (Optional)** if you want depth
3. Try **Hands-On Tools** at the end (if listed)
4. Move to next unit

**Example for Unit 1:**
- Read Anthropic "How Claude Works" (15 min) ✓
- Watch 3Blue1Brown (20 min) ✓
- Use Hugging Face interactive guide (15 min) ✓
- Test prompts on ChatGPT (20 min) ✓
- Summarize in 1 paragraph: "What is an LLM?" ✓
- Move to Unit 2 ✓

---

## How to Use the Quick Reference

**Bookmark this file.** Use it:

- **In meetings:** Need a quick decision? Use the flowchart.
- **When stuck:** Red flags checklist or glossary.
- **When proposing:** Use the memo template.
- **When reviewing:** Use the checklist.
- **When answering questions:** Use "Answering Common Questions" section.

**Example:**
```
Engineering asks: "Should we fine-tune this model?"
You: [Open Quick Reference → Architecture Decision Flowchart]
"Let me check. Do we have 100+ labeled examples? No. 
Does it need external data? Yes. So we should use RAG, not fine-tune."
```

---

## Success Criteria

By the end of Week 3, you should be able to:

✓ Explain to a CEO how LLMs work (5 min pitch)
✓ Evaluate a technical proposal ("Should we fine-tune, RAG, or prompt?")
✓ Write user stories + acceptance criteria for AI features
✓ Define success metrics (accuracy, latency, cost, user satisfaction)
✓ Spot red flags (hallucination risk, cost spiral, bias, data privacy)
✓ Write an AI feature PRD
✓ Have informed conversations with engineers about tradeoffs
✓ Assess feasibility before committing to an AI feature

---

## Common Paths Through This Curriculum

### Path 1: "I need to evaluate an AI feature proposal next week"
1. Read Quick Reference.md top-to-bottom (1 hour)
2. Read Unit 3 (Models) + Unit 6 (Architecture) from Syllabus/Week2 (2 hours)
3. Read Unit 8 (Metrics & Risk) from Week3 (1 hour)
4. Use the checklist in Quick Reference when reviewing the proposal

**Time:** 4 hours. You'll be ready.

### Path 2: "I'm building an AI product from scratch"
1. Follow the full 3-week curriculum top-to-bottom
2. Supplement each unit with resources
3. Do the 3 weekly deliverables
4. Keep Quick Reference handy for ongoing decisions

**Time:** 40 hours over 3 weeks.

### Path 3: "I just need to sound smart in AI conversations"
1. Read Unit 1 + Unit 3 (Foundations + Models) (4 hours)
2. Skim Unit 4 (RAG basics) (1 hour)
3. Bookmark Quick Reference + Glossary

**Time:** 5 hours. You'll have enough context.

### Path 4: "I'm a PM and want to stay current with AI"
1. Read all main content (Syllabus + Week2 + Week3) (20 hours)
2. Check Resources.md monthly for new tools/papers
3. Use Quick Reference for decisions
4. Re-read Unit 8 (Metrics) quarterly to audit your metrics

**Time:** Initial 20 hours + 2 hours/month ongoing.

---

## Study Tips

**Active Learning (Not Just Reading):**
- After each unit, summarize in your own words (1 paragraph)
- Draw diagrams (LLM architecture, RAG pipeline, agent loop)
- Test concepts on real tools (Claude, ChatGPT, LangChain)
- Write prompts and see what works/breaks
- Teach someone else what you learned

**Accountability:**
- Find a study buddy (another PM, engineer, product person)
- Weekly check-ins: "What did you learn this week?"
- Share your deliverables; get feedback

**Connect to Your Work:**
- For each unit, identify 1 problem at your current job it applies to
- Write a quick note: "How could we use this?"
- By Week 3, you'll have a list of ideas

**Stay Updated:**
- Subscribe to TheAIIndex newsletter (monthly, 15 min)
- Follow Hugging Face on Twitter for new papers
- Revisit Resources.md quarterly for new tools

---

## Common Questions

**Q: Can I skip ahead to Week 3 (Metrics)?"**
A: Not really. Week 3 assumes you understand LLMs (Week 1) and architectures (Week 2). You'll get lost. Do Week 1 first.

**Q: I'm not technical. Will I understand this?"**
A: Yes. This curriculum is written for non-technical PMs. We skip the math entirely. If anything feels too technical, skip it; the one-liners in Quick Reference are enough.

**Q: Do I need to code?"**
A: No. But hands-on exploration helps. You don't need to write code; just follow tutorials, test models, look at example code.

**Q: What if I don't have time for 3 weeks?"**
A: Do the 2-hour quick path: Read Quick Reference.md + Unit 3 + Unit 8. You'll have enough context for most decisions.

**Q: Can I print this?"**
A: Yes. All files are markdown; they print cleanly. Or save as PDF.

**Q: Will this be outdated?"**
A: Fundamentals (how LLMs work, RAG, agents) won't change in 2024–2025. Model names/costs will shift. Check Resources.md for current models. The decision frameworks stay the same.

**Q: What happens after I finish?"**
A: You have a solid foundation. Next steps:
- Build something (AI feature at your company)
- Join AI PM communities (LinkedIn, Twitter)
- Stay current (2 hrs/month reading)
- Get hands-on (use Claude/GPT-4 weekly)

---

## Files at a Glance

| File | Purpose | Length | When to Use |
|------|---------|--------|---|
| **Syllabus.md** | Week 1 learning + foundations | 40 pages | Week 1; reference glossary |
| **Week2.md** | Week 2 learning + advanced patterns | 30 pages | Week 2 |
| **Week3.md** | Week 3 learning + product strategy | 35 pages | Week 3; capstone |
| **Resources.md** | Curated free resources, all units | 25 pages | Supplement each unit |
| **Quick Reference.md** | Cheat sheet for meetings | 15 pages | BOOKMARK THIS |

**Total:** ~150 pages of content (but you won't read all of it; select what you need)

---

## Let's Get Started

**Pick your path:**
- 3-week intensive? Start with Syllabus.md, Unit 1
- Self-paced? Start with Syllabus.md, but take 1 unit/week
- Just-in-time? Start with Quick Reference.md, then deep-dive as needed

**Questions?** Refer back to the relevant unit or check Resources.md for references.

**Ready?** Open Syllabus.md and start Unit 1.

Good luck.

