---
name: llm-council
description: >
  Run any high-stakes question, decision, or idea through a council of 5 AI advisors who independently analyze it, peer-review each other anonymously, and synthesize a final verdict. Based on Karpathy's LLM Council methodology.

  **Always trigger this skill** when the user says: "council this", "run the council", "war room this", "pressure-test this", "stress-test this", or "debate this". Also trigger for genuine decisions with real tradeoffs when combined with phrases like "should I X or Y", "which option", "what would you do", "is this the right move", "validate this", "get multiple perspectives", "I can't decide", or "I'm torn between".

  Do NOT trigger for: simple yes/no questions, factual lookups, single-answer technical questions, or casual "should I" without meaningful stakes or tradeoffs (e.g. "should I use markdown" is NOT a council question).

  Trigger criteria: genuine decision with stakes, multiple options, and context suggesting the user wants pressure-testing from multiple angles.
---

# LLM Council

Run a high-stakes question through 5 independent advisors → peer review → chairman synthesis → final verdict.

## Core Philosophy

One AI = one perspective. The council runs the question through 5 fundamentally different thinking lenses, anonymized peer review, and a chairman who synthesizes where they agree, where they clash, and what to actually do.

---

## The Five Advisors

| Advisor | Thinking Style |
|---|---|
| **The Contrarian** | Assumes a fatal flaw exists. Digs for what's wrong, missing, or will fail. |
| **The First Principles Thinker** | Ignores surface framing. Asks: "What problem are we *actually* solving?" Strips assumptions, rebuilds from scratch. |
| **The Expansionist** | Looks for hidden upsides and adjacent opportunities. Ignores risk (that's the Contrarian's job). |
| **The Outsider** | Zero industry context. Catches "curse of knowledge" — things obvious to the user but confusing to others. |
| **The Executor** | Strictly practical. Asks: "What do you do Monday morning?" Flags ideas without a clear, fast path to execution. |

**Natural tensions:** Contrarian vs. Expansionist (downside vs. upside), First Principles vs. Executor (rethink vs. just build it), Outsider keeps everyone grounded.

---

## Process

### Step 1: Frame the Question

Before launching the council:

1. **Identify if question qualifies.** If too vague, ask **one** clarifying question before proceeding.
2. **Synthesize a clear, neutral prompt** containing:
   - The core decision or question
   - Key context (stage, constraints, audience, metrics)
   - What's at stake

---

### Step 2: Convene the Council (All 5 in parallel)

Simulate all 5 advisors simultaneously. Each advisor:
- Leans **fully** into their assigned perspective — no hedging, no balance
- Keeps response to **150–300 words**
- Goes straight to analysis, no preamble

**Prompt each advisor with:**
```
You are [Advisor Name] on an LLM Council.
Your thinking style: [Advisor Description]

Question brought to the council:
---
[Framed Question]
---

Respond from your perspective. Be direct and specific. Don't hedge or try to be balanced. Lean fully into your assigned angle. The other advisors cover what you're not covering.

150-300 words. No preamble. Go straight into your analysis.
```

---

### Step 3: Peer Review (Anonymized)

1. **Collect all 5 advisor responses** and randomly label them **Response A through E** (eliminate identity/positional bias).
2. **Each advisor reviews all 5 anonymized responses** — answering 3 questions, max 200 words:

```
You are reviewing the outputs of an LLM Council. Five advisors answered:
---
[Framed Question]
---

Anonymized responses:
Response A: [...]
Response B: [...]
Response C: [...]
Response D: [...]
Response E: [...]

Answer directly, referencing responses by letter:
1. Which response is strongest? Why?
2. Which has the biggest blind spot? What's missing?
3. What did ALL five miss that the council should consider?

Under 200 words. Be direct.
```

---

### Step 4: Chairman Synthesis

A single Chairman receives the original question, de-anonymized advisor responses, and all 5 peer reviews. Synthesizes a final verdict.

**Chairman prompt:**
```
You are the Chairman of an LLM Council. Synthesize the advisors' work and peer reviews into a final verdict.

Question:
---
[Framed Question]
---

ADVISOR RESPONSES:
- The Contrarian: [...]
- The First Principles Thinker: [...]
- The Expansionist: [...]
- The Outsider: [...]
- The Executor: [...]

PEER REVIEWS:
[All 5 peer reviews]

Output the verdict using this exact structure:

## Where the Council Agrees
[Points multiple advisors converged on independently. High-confidence signals.]

## Where the Council Clashes
[Genuine disagreements. Present both sides. Explain why reasonable advisors disagree.]

## Blind Spots the Council Caught
[Insights that emerged only during peer review.]

## The Recommendation
[Clear, direct recommendation. Not "it depends." A definitive answer with reasoning.]

## The One Thing to Do First
[A single, concrete next step. Not a list. One thing.]

Be direct. Don't hedge.
```

**Chairman autonomy:** Can override majority. If 4/5 agree but the dissenter has the stronger argument, the Chairman sides with the dissenter and justifies why.

---

### Step 5: Present the Verdict

Output the full verdict in chat as clean Markdown. No HTML files, no attachments.

```markdown
## Council Verdict: {Short Topic}

### Where the Council Agrees
- {Point 1}
- {Point 2}

### Where the Council Clashes
- {Conflict 1}

### Blind Spots the Council Caught
- {Insight 1}

### The Recommendation
{Actionable recommendation}

### The One Thing to Do First
**{Single concrete step}**
```

---

### Step 6: Save Transcript (Optional)

Only if the user explicitly requests it or the decision is highly significant. Save the complete, unedited process to `council-transcript-[YYYY-MM-DD].md`.

---

## Important Notes

- **Parallel execution**: All 5 advisors run simultaneously — no sequential bleed-through.
- **Strict anonymity in peer review**: Always randomize to A–E before review step.
- **Chairman can override**: Minority view with stronger logic beats majority consensus.
- **Filter trivial questions**: Don't invoke for binary technical lookups or factual questions.
- **Output stays in chat**: Clean, scannable Markdown. Bullet-point heavy.
