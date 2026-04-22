# First Principles Thinking in Software Engineering

**Date:** 2026-04-22  
**Category:** engineering  
**Tags:** `first-principles`, `engineering-discipline`, `design`, `architecture`, `philosophy`  
**Related:** [What AI Assistants Mean by "Mental Model"](ai-assistant-mental-model-260420a.md)

---

## TL;DR

- **First principles** reasoning means stripping a problem down to its irreducible truths and building up from there — rather than reasoning by analogy from what already exists
- In software engineering, it is the practice of questioning **why** a design, pattern, or tool is used, not just accepting that it is used
- It produces better architects and debuggers: people who can reason about systems that have never been built before and trace failures to their true root cause
- The discipline requires separating **constraints** (things that cannot change) from **conventions** (things that happen to be done a certain way)
- Philosophically, it descends from Aristotle's *archai* and runs through Descartes and Feynman — the idea that understanding means being able to derive, not just recall

---

## What First Principles Thinking Is

A **first principle** is a foundational proposition that cannot be deduced from any other proposition within a given domain. To reason from first principles is to refuse to accept inherited assumptions — and instead trace back to the bedrock facts that cannot be further reduced.

The opposite is **reasoning by analogy**: solving new problems by copying solutions from similar-looking old problems. Analogy is fast. First principles is slower, but it gets you somewhere that analogy cannot: genuinely novel ground.

In practice, first principles reasoning means asking:

- What do I actually **know** is true here, as opposed to what is conventional?
- What are the real **constraints** — physics, requirements, business rules — and which "constraints" are just habits?
- If I started with only those constraints, what solution would I build?

---

## The Philosophical Lineage

The concept is old. Aristotle used the term *archai* — translated as "first principles" — to describe the irreducible starting points of any science. For Aristotle, you could not understand something by citing something else; you had to reach bedrock.

Descartes extended this in the 17th century by applying radical doubt: stripping away everything that could be questioned until only certainties remained — his *cogito* is the famous result. The method was not about doubt as paralysis, but doubt as a **tool for finding solid ground**.

Richard Feynman captured it in modern scientific practice. He was famous for refusing to accept received explanations and insisting on being able to derive things himself. His notebooks would rebuild derivations from scratch not because he distrusted textbooks, but because **you do not truly understand something you cannot derive**.

Elon Musk popularized the term for business audiences through SpaceX's battery cost problem: rather than accepting market pricing as a constraint, he decomposed the battery into its raw materials and asked what those cost — which exposed that conventional pricing was convention, not physics. This is the canonical modern example.

---

## How It Applies to Software Engineering

### Distinguishing constraints from conventions

Most codebases are full of decisions inherited without scrutiny. First principles thinking demands that an engineer be able to answer, for any significant design decision:

> "Is this a hard constraint, or is it just how we've always done it?"

A **constraint** might be: this system must respond in under 100ms; this must run on-premises with no internet access; compliance requires immutable audit logs.

A **convention** might be: we always use a message bus here; we always build microservices; we always use this ORM. Those choices may be correct — but if the engineer cannot derive *why* from the constraints, they are on shaky ground when circumstances change.

### Debugging

Cargo-cult debugging — trying things until something works — is reasoning by analogy at its worst. First principles debugging is different: it means forming a **model** of the system, identifying what must be true if the symptoms are observed, and tracing back to the cause.

A first principles debugger asks:

1. What is the observed behavior?
2. What would have to be true in the system for this to happen?
3. What assumption in my model does this violate?
4. Where is the actual discrepancy between model and reality?

This is slower in the moment but produces **genuine understanding** — and makes the problem less likely to recur.

### Architecture and design

The most damaging tendency in software architecture is **pattern cargo-culting**: adopting microservices, event sourcing, hexagonal architecture, or any pattern not because the problem demands it, but because it is what sophisticated teams do.

First principles architecture starts from constraints:

| Question | What you are deriving |
|---|---|
| What are the actual load characteristics? | Whether distribution is necessary |
| What are the failure modes that matter most? | Whether event sourcing's audit trail is worth its complexity |
| What are the team's actual coordination costs? | Whether service decomposition helps or hurts |
| What does the system need to get right forever? | Where to invest in correctness vs. velocity |

The output is a design you can **justify from the problem**, not a design borrowed from a company with different scale, constraints, and team structure.

### Writing code

At the micro level, first principles thinking shows up as: **every line of code should be able to justify its own existence**.

Abstractions should exist because complexity is genuinely reduced. Functions should be split because the problem has a natural seam there. Dependencies should be added because the cost of building the thing in-house exceeds the cost of the dependency — and that cost has been thought through.

The discipline also resists **premature optimization** and **premature abstraction** equally — both are ways of introducing complexity before it has been earned by a real constraint.

---

## The Discipline It Builds

First principles thinking is not a technique used once. It is a **mode of intellectual engagement** that, practiced consistently, changes how engineers relate to complexity.

Engineers who reason from first principles tend to:

- Ask *why* more often than *how*
- Be more useful in novel situations where no prior pattern applies
- Build simpler systems because they do not carry over unnecessary complexity from reference architectures
- Produce more maintainable code because the reasoning behind it is preserved, not just the artifact
- Fail more instructively — when something breaks, they know where to look because they know why it was built the way it was

The cost is that it is **slower up front**. It requires the willingness to sit with a problem before reaching for a solution. In environments that reward the appearance of fast progress, this is genuinely hard to practice.

---

## Common Failure Modes

| Failure | Description |
|---|---|
| **Analogy by default** | Applying a known pattern to a new problem because it superficially resembles problems the pattern solved before |
| **Constraint confusion** | Treating business conventions, team habits, or inherited tooling choices as if they were hard constraints |
| **Analysis paralysis** | Using first principles as an excuse to over-examine rather than a method for reaching solid ground faster |
| **Cargo-cult adoption** | Adopting the vocabulary of first principles without actually questioning the assumptions underneath |
| **Sycophantic design** | Designing to satisfy reviewers rather than constraints — the social version of reasoning by analogy |

---

## A Working Heuristic

Before committing to a significant engineering decision, ask:

1. **What problem am I actually solving?** (Not the stated problem — the real one.)
2. **What are the non-negotiable constraints?** (Separate these from preferences.)
3. **If I had no prior art to borrow from, what would I build?**
4. **Does my actual design match that answer? If not, why not?**

The gap between answer 3 and your actual design is worth naming. Sometimes the gap is justified — prior art exists for a reason. But it should be a **conscious choice**, not an inherited default.

---

## Sources

[1] [Aristotle, *Posterior Analytics*, Book I](https://classics.mit.edu/Aristotle/posterior.1.i.html)  
[2] [Descartes, *Meditations on First Philosophy* (1641)](https://www.earlymoderntexts.com/assets/pdfs/descartes1641.pdf)  
[3] [Richard Feynman on Understanding vs. Knowing](https://fs.blog/feynman-technique/)  
[4] [Elon Musk on First Principles (TED Interview, 2013)](https://www.ted.com/talks/elon_musk_the_mind_behind_tesla_spacex_solarcity)  
[5] [Farnam Street — First Principles: Elon Musk on the Power of Thinking for Yourself](https://fs.blog/first-principles/)
