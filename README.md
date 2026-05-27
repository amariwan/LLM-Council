# LLM Council

> Run any high-stakes decision through 5 independent AI advisors, let them peer-review each other anonymously, and get a synthesized verdict — not just one AI's opinion.

A Claude skill by [Aland Baban](https://tasiomind.dev).

---

## The Problem

You ask one AI a question, you get one answer. That answer might be great or completely off. You have no way to tell because you only saw one perspective.

**The LLM Council fixes this.**

---

## How It Works

```
Your Question
     │
     ▼
┌─────────────────────────────────────────┐
│         5 Independent Advisors          │
│  Contrarian · First Principles ·        │
│  Expansionist · Outsider · Executor     │
└─────────────────────────────────────────┘
     │
     ▼
┌─────────────────────────────────────────┐
│      Anonymized Peer Review             │
│  Each advisor reviews all others        │
│  (responses labeled A–E, no names)      │
└─────────────────────────────────────────┘
     │
     ▼
┌─────────────────────────────────────────┐
│         Chairman Synthesis              │
│  Agreements · Conflicts · Blind Spots   │
│  → Clear Recommendation                 │
└─────────────────────────────────────────┘
```

---

## The Five Advisors

| Advisor | What They Do |
|---|---|
| **The Contrarian** | Assumes a fatal flaw exists. Digs for what's wrong, what's missing, what will fail. |
| **The First Principles Thinker** | Strips assumptions. Asks: *"What problem are we actually solving?"* Often concludes you're asking the wrong question. |
| **The Expansionist** | Finds hidden upsides and adjacent opportunities everyone else is missing. |
| **The Outsider** | Zero context, zero bias. Catches the "curse of knowledge" — things obvious to you but confusing to others. |
| **The Executor** | Strictly practical. Asks: *"What do you do Monday morning?"* Flags ideas without a clear path to action. |

**Built-in tensions that produce better answers:**
- Contrarian vs. Expansionist → downside vs. upside
- First Principles vs. Executor → rethink everything vs. just ship it
- Outsider → keeps everyone grounded in reality

---

## When to Use It

**Good council questions** (high stakes, real tradeoffs):
- *"Should I take the job offer or stay and negotiate?"*
- *"Which architecture makes more sense for this system?"*
- *"I'm thinking of pivoting from X to Y — am I crazy?"*
- *"Here's my pitch deck. What's weak?"*
- *"Should I hire someone or build the automation first?"*

**Bad council questions** (don't waste it on these):
- *"What's the capital of France?"* — one right answer
- *"Write me a function that does X"* — creation task, not a decision
- *"Summarize this article"* — processing task, not judgment

---

## Trigger Phrases

Say any of these to activate the council:

| Trigger | Type |
|---|---|
| `council this` | Mandatory |
| `run the council` | Mandatory |
| `war room this` | Mandatory |
| `pressure-test this` | Mandatory |
| `stress-test this` | Mandatory |
| `debate this` | Mandatory |
| `should I X or Y` + real stakes | Strong |
| `I can't decide` + real stakes | Strong |
| `I'm torn between` + real stakes | Strong |
| `validate this` + real stakes | Strong |

---

## Output Format

```markdown
## Council Verdict: {Topic}

### Where the Council Agrees
- High-confidence points multiple advisors converged on independently

### Where the Council Clashes
- Genuine disagreements with both sides presented

### Blind Spots the Council Caught
- Insights that only emerged during peer review

### The Recommendation
A clear, direct recommendation. Not "it depends."

### The One Thing to Do First
**A single concrete next step.**
```

---

## Installation

This is a Claude skill (`.skill` file) for use with [Claude's skills system](https://docs.claude.com).

1. Download `llm-council.skill`
2. Install it in your Claude environment
3. Use any trigger phrase when you have a real decision to make

---

## Key Design Decisions

**Anonymized peer review** — Advisor responses are relabeled A–E before review to eliminate identity and positional bias. Advisors don't know whose work they're critiquing.

**Chairman autonomy** — The Chairman can override the majority. If 4/5 advisors agree but the dissenter has the stronger logical argument, the Chairman sides with the dissenter and explains why.

**Parallel execution** — All 5 advisors run simultaneously. No sequential bleed-through where early responses influence later ones.

**No hedging** — Each advisor leans fully into their assigned lens. The other advisors cover the angles they're not covering. That's the point.

---

## Credits

Built by [Aland Baban](https://tasiomind.dev).
