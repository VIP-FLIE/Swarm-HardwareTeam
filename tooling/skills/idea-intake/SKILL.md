---
name: idea-intake
description: "Domain-agnostic ideation-to-MVPr facilitation skill, grounded in design-thinking, lean-startup, effectuation, and Discovery-Driven-Planning research. Use when the user has a raw idea, problem, or want in ANY domain — travel plans, product concepts, Obsidian vault features, mechanical designs, business ideas, campus organizations, creative projects — and wants to explore, define, and rapidly prototype it toward a minimum viable product/representation (MVPr). Trigger on '/idea-intake', 'is this idea worth pursuing', 'help me think through this', 'explore this idea', 'should I do this', or any unscoped concept presented without a clear go/no-go decision already made. Does NOT produce a formal specification document. Terminates with a living assumption ledger and an explicit PURSUE/REFINE/SHELVE verdict — the ledger itself is the artifact carried forward, not a handoff to another skill. Do NOT trigger if the user has already decided to proceed and just wants a document produced directly."
---

# Idea-Intake

Domain-agnostic ideation and MVPr (minimum viable product/representation) facilitation skill. One recursive primitive — **Diverge → Diverge → Converge → Decide → Ledger Update → Stop-Check** — applied at three scales (Framing, Criteria, Prototype), entered and paced according to an explicit upfront regime diagnostic (causal vs. effectual).

The goal is viability validation and rapid convergence toward a tested MVPr, not documentation. This skill can — and should — terminate an idea without producing a polished artifact if it doesn't hold up. There is no downstream handoff: the assumption ledger produced here *is* the plan, in the Discovery-Driven-Planning sense of a living, continuously-revised document. If the user later wants a formal specification produced from a PURSUE verdict, that is a separate, explicit ask — not something this skill routes into automatically.

---

## Why This Shape (design rationale, condensed)

- **No forced phase order.** d.school treats its stages as non-sequential modes; Discovery-Driven Planning is built entirely around revising a plan as assumptions resolve. A rigid Define → Lock → Prototype pipeline contradicts both. The three scales below are zoom levels of one loop, not sequential gates.
- **Regime determines entry and rigidity, not the user's domain.** Causal reasoning (fixed goal, find the means) and effectual reasoning (fixed means, let the goal emerge) are empirically distinct modes of expert decision-making under different levels of uncertainty (Sarasvathy, 2001; Chandler et al., 2011, validated construct study). Forcing an effectual user through upfront goal-locking produces a false, brittle target. Forcing a causal user through open-ended means-inventory wastes their already-clear direction.
- **Divergence and convergence never share a turn.** This is the single most robust finding across both the classic brainstorming-vs-brainwriting literature (Diehl & Stroebe, 1987) and recent human-AI co-ideation studies — mixing generation and evaluation degrades both. Enforced structurally: the agent's divergent step always ends the turn on a check-in question, and convergence only happens in the following turn — not just a formatting convention within one message.
- **User generates first, always.** Preserves human agency and avoids LLM anchoring/premature-convergence effects documented in AI-augmented ideation research (arXiv 2402.14978; Creativity & Cognition 2026).
- **Stop conditions are evidence-based, not round-counted.** A fixed round cap produces premature verdicts on genuinely open ideas and wastes time on tightly-bounded ones.

---

## Phase 0 — Regime Diagnostic (explicit, first move)

Ask this directly before anything else. Do not infer silently.

```
"Before we start — is this closer to:
 (a) You have a fairly fixed goal or outcome in mind, and need to
     figure out the way there, OR
 (b) You have means, interest, or resources in hand, but the actual
     goal or shape of the solution is still genuinely open?"
```

| Answer | Regime | Effect on the loop below |
|---|---|---|
| (a) | **Causal** | Default entry at Framing scale. Ledger tends to lock earlier. Lean/DDP-flavored questioning. |
| (b) | **Effectual** | Routes to the **Means Inventory** pre-loop step (below) before entering the Loop. Ledger stays loose longer; success criteria are allowed to crystallize from what gets built, not the reverse. Affordable-loss framing for risk (invest only what's affordable to lose, not what maximizes projected return). |
| Unsure | **Hybrid** | Ask one diagnostic follow-up ("If this completely failed, would that feel like a wasted afternoon or a real loss?" — low stakes/high ambiguity usually signals effectual) then route. |

**Regime is stored, not fixed.** If mid-loop evidence contradicts the stated regime (a "fixed goal" turns out to be a means in disguise; an "open means" user is actually anchored to one hidden outcome), flag the mismatch plainly and ask whether to re-route. Do not silently keep operating on a stale regime label.

---

## Pre-Loop Step — Means Inventory (effectual/hybrid entries only)

**Causal entries skip this entirely** and go straight to Framing scale, below.

This exists because "what do I have" and "what could I build" are categorically different questions — Sarasvathy's bird-in-hand principle treats means-taking-stock as its own move, distinct from generating solution candidates. Folding it into Prototype scale muddies that scale's job (candidate concepts → shortlisted MVPr) with a different one (raw resources → plausible directions), and testing showed the seam reappears anyway once a direction has to get chosen before anything is actually prototyped.

```
DIVERGE (user first)   — what do you actually have: who you are, what
                          you know, whom you know — regardless of
                          whether it points at a direction yet.
DIVERGE (agent second)  — surface means the user undervalued or didn't
                          name (dormant network ties, institutional
                          access, adjacent skills). Generative only —
                          no clustering or ranking yet. End the turn
                          here with a check-in: more to add, or ready
                          to converge?
CONVERGE (agent)        — runs only on the next turn, after the user
                          responds. Cluster the means into 2–3
                          plausible directions. Don't shortlist a
                          testable prototype yet — that's the next
                          scale's job.
DECIDE (user)           — pick a direction to carry forward.
```

**Output of this step**: the chosen direction plus an affordable-loss constraint, entered into the ledger using the same format as any other pass (e.g., `A-01 | build-team pipeline direction selected | — | open | Means Inventory`). Then proceed into the Loop below — usually landing at Prototype scale with the chosen direction as its diverge seed, though Criteria is fair game if the means-inventory pass surfaced a clear want instead.

---

## The Loop (one primitive, three scales)

```
1. DIVERGE (user first)   — user generates candidate options/answers.
                             Agent stays silent-but-listening this step —
                             no priming, no examples offered yet.
2. DIVERGE (agent second)  — agent adds options the user hasn't raised.
                             Push non-obvious angles: SCAMPER prompts,
                             analogy, constraint-removal, reversal.
                             Generative only — no ranking, no "best/
                             strongest" language, no feasibility
                             commentary. End the turn here: ask whether
                             the user has more to add or is ready to
                             converge. Do not perform step 3 in this
                             same message — the check-in question is
                             the end of this turn, not a rhetorical
                             pause.
3. CONVERGE (agent)        — runs only on the next assistant turn,
                             after the user responds (even a one-word
                             "go ahead"). Only then evaluate/organize:
                             clusters, compares, rates against current
                             ledger criteria. This is the agent's
                             strongest role (LLM evaluation performs
                             comparably to expert reviewers in this
                             specific mode — arXiv 2402.14978).
4. DECIDE (user)           — user makes the actual selection or
                             ranking. Final call always stays with
                             the user.
5. LEDGER UPDATE           — add/revise entries; tag Kano class and
                             status. Shown in full, every pass.
6. STOP-CHECK              — evaluate convergence conditions (below).
                             If not met, run the loop again — same
                             scale or a different one, per what the
                             pass revealed.
```

### The three scales

| Scale | Diverge produces | Converge produces |
|---|---|---|
| **Framing** | Candidate problem statements / Jobs-to-be-Done (functional, emotional, social) | 1–5 "How Might We" questions |
| **Criteria** | Candidate success criteria, wants, constraints | Kano-classified ledger entries (must-be / performance / delighter) |
| **Prototype** | Candidate concepts, sketches, approaches, representations | Shortlisted MVPr candidate(s) to build/test |

**No forced order.** Causal entries typically start at Framing and move down. Effectual entries land here via Means Inventory (above), usually entering at Prototype scale with the chosen direction as the seed, and let Criteria populate retroactively from what the prototype reveals. The agent recommends a starting scale based on the Phase 0 answer but never forces one — if the user wants to jump straight to Prototype on their first message, follow them there and backfill the ledger as it emerges.

---

## Assumption Ledger

Persistent, visible, continuously updated — **shown in full after every loop pass**, not gated behind a request.

```
| ID   | Statement                          | Kano Class  | Status      | Source (round/scale) |
|------|-------------------------------------|-------------|-------------|-----------------------|
| A-01 | [falsifiable want/criterion/belief] | must-be     | open        | Criteria, R1          |
| A-02 | ...                                 | delighter   | validated   | Prototype, R2         |
```

**Kano classes**:
- **Must-be** — its absence kills viability; its presence is barely noticed. These define the floor for "viable."
- **Performance** — satisfaction scales roughly linearly with how well it's delivered.
- **Delighter** — unexpected, differentiating; not required, but at least one target delighter should be identified before calling an MVPr "done."
- **Indifferent / reverse** — use only if it comes up; don't force every entry into the three main buckets.

**Status**: open (untested) → validated (evidence supports it) → invalidated (evidence contradicts it — do not quietly drop invalidated entries, keep them visible with the invalidation noted; this is where re-framing signals live).

This ledger **is** the DDP-style living plan. There is no separate "lock-in" step that freezes it — it is revised every pass, for the life of the engagement.

---

## Stop Conditions (not a round cap)

Evaluate after every pass. None of these are phase-boundary gates — they're continuously-checked exit criteria:

- All **must-be** ledger entries are validated, or have a concrete, near-term test path.
- The **riskiest** open entries specifically (not all entries) have been tested.
- New divergent output is producing variations on existing options, not genuinely new ones (diminishing returns).
- User and agent agree the current MVPr representation is sufficient to justify the next real commitment of time/resources.
- At least one target **delighter** has been identified (not necessarily validated) if the domain has any differentiation dimension at all.

If none are met, loop again. If the user wants to stop before they're met, that's their call — state plainly which stop conditions are still unmet before honoring it.

---

## Verdict (terminates the engagement)

State exactly one, with 1–2 sentences of justification. Do not default to PURSUE.

```
PURSUE
  Must-be criteria cleared or have a tested path. Riskiest assumptions
  tested. → Output: final ledger table + verdict + rationale.
  Nothing else. No downstream document is generated automatically.

REFINE
  Genuine merit, but one or more must-be entries remain open/invalidated,
  or resolving one revealed a new open question. → Loop back into
  whichever scale the open entry belongs to. Do not restart from
  Phase 0 unless the regime itself is now in question.

SHELVE
  A must-be entry cannot plausibly be satisfied, or the idea doesn't
  survive its own stress-test. → State the blocker plainly. Document
  the reasoning in-chat. Produce no further artifact.
```

**On PURSUE**: the deliverable is the ledger itself, not a spec. If the user separately asks for a formal write-up (a proposal, a spec, a design doc), that is a new, explicit request to handle on its own terms — not an automatic next phase of this skill.

---

## Bias-Mitigation Pass (cross-cutting, silent by default)

Runs every pass; not a phase the user sees. Nine biases design thinking research (Liedtka, 2015) identifies as ideation's usual failure modes — self-check against these when framing questions or critiquing prototypes:

```
projection bias            — assuming others want what you want
egocentric empathy gap      — misjudging others' states from your own
hot/cold empathy gap        — misjudging decisions made in a different
                               emotional state than your current one
focusing illusion           — overweighting whatever's salient right now
say/do gap                  — stated preference vs. actual behavior
planning fallacy            — underestimating time/cost/difficulty
confirmation bias           — seeking evidence that fits the existing idea
endowment effect            — overvaluing the option already chosen
availability bias           — overweighting easily-recalled examples
```

Surface one explicitly only when it's clearly live ("this reads like an endowment-effect trap because you're the one who proposed option A") — don't recite the checklist at the user.

---

## Special Cases

### User pushes for PURSUE despite an open must-be entry
State plainly which entry is unresolved and why that keeps the verdict at REFINE. Don't override the honest assessment to match the user's preference.

### Regime mismatch discovered mid-loop
Flag it plainly, propose re-routing (e.g., "this is looking more effectual than causal — want to loosen the ledger and let criteria follow the prototype instead?"), and let the user decide whether to switch.

### Idea spans multiple unrelated Criteria-scale entries with no clear priority
Surface this explicitly: ask the user to rank which 2–3 entries matter most rather than resolving all with equal weight in one pass.

### User already suspects SHELVE but wants to explore anyway
Proceed, but flag early that the stated blocker will likely resurface at verdict time unless something changes. Don't pre-empt the verdict.

### User wants a formal spec/document after PURSUE
This skill doesn't produce one. Treat it as a new, separate request — write it directly, scaled to what's actually needed, using the final ledger as your source material. Do not invoke a retired handoff format or reference a deprecated skill.

---

## Guidelines

- **Be a critic, not a cheerleader.** SHELVE is a successful outcome, not a failure of the skill.
- **No fixed taxonomy at the Framing scale.** Don't sort ideas into domain buckets ("this is a travel idea"). Extract the actual problem/JTBD directly.
- **Ledger visibility is not optional.** Full table, every pass — this is the mechanism that replaces a locked, one-time success-criteria step.
- **Respect the exploratory/bounded distinction within any scale.** A genuinely open idea shouldn't be forced to a verdict by round 3; a tightly-scoped one shouldn't be allowed to ramble.
- **The ledger is the plan.** Resist the urge to translate it into prose documentation unless the user asks for that separately.

---

## Example Walkthrough (compressed)

```
Idea: "Obsidian plugin for FSRS review stats"

Phase 0: Causal (fixed goal — surface review stats in-vault; means
         (coding ability, existing pipeline) already known)

Framing scale, Pass 1:
  Diverge (user): wants at-a-glance retention/streak visibility
  Diverge (agent): also consider per-deck breakdown, trend-over-time,
                    a dashboard vs. a sidebar widget. Ends turn:
                    "anything else, or ready to converge?"
  [user: "go ahead"] — separate turn begins here
  Converge: HMW "How might we surface FSRS trend data without adding
             a new UI surface to maintain?"
  Ledger: A-01 "must show retention trend" (must-be, open)
          A-02 "per-deck breakdown" (performance, open)

Criteria scale, Pass 1:
  Kano-classify further wants → A-03 "zero added UI chrome" (delighter,
    open) — ranks above per-deck breakdown as differentiation target

Prototype scale, Pass 1:
  Diverge (user): render inside existing dashboard note via Dataview
  Diverge (agent): alternative — command-palette popup, or
                    codeblock-embedded chart. Ends turn: "more angles,
                    or converge on these?"
  [user: "converge"] — separate turn begins here
  Converge: Dataview-embedded chart rated highest against A-01/A-03
  Ledger updated: A-01 validated (feasible in existing pipeline),
                  A-03 validated (no new UI surface needed)

Stop-check: must-be cleared, one delighter validated, new options
            are variations not novelty → PURSUE

Verdict: PURSUE — "Dataview-embedded trend chart satisfies the
  must-be with zero new UI surface, which was the target delighter.
  Per-deck breakdown remains open as a performance-tier follow-up."

Output: final ledger table + verdict. No handoff artifact generated.
```
