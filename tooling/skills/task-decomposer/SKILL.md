---
name: "task-decomposer"
description: Turn a person's objective into a verified list of atomic, actionable tasks (each with input, output, done-test, and time estimate) written to a Markdown document. Use whenever the user gives a goal, assignment, project, deliverable, or chore and wants steps, a breakdown, a task list, or a plan they can execute — including phrasing like "how do I tackle this", "what should I do first", "break this down", "plan this out", or "make this actionable", even if they never say "decompose". Gates the objective first and hands ill-defined ones to prompt-refiner before decomposing. Do NOT use for "should I pursue this / is this worth doing" (use idea-intake), for clarifying an objective when no task list is wanted (use prompt-refiner), or for calendar scheduling.
---

# Task Decomposer

Objective in, reviewed task list out. The executor is always the **human user**; do not optimize for agent execution. Rule tags like `[R7]` map to `references/evidence.md` (source, evidence tier, confidence). Read that file only when the user asks why a rule exists or a rule needs changing.

Related skills: an idea-intake PURSUE ledger can seed this skill (its must-be entries become done-conditions and constraints). Prompt-refiner is the clarification engine this skill calls; do not duplicate its questioning here.

## Pipeline

### 1. Gate (silent, before any output)

Evaluate the objective against:

```
READY := Unambiguous ∧ Singular ∧ Verifiable ∧ Feasible ∧ Complete ∧ HasDoneCondition   [R3]
```

| Predicate | Fails when |
|---|---|
| Unambiguous | Two or more plausible readings would produce different task sets |
| Singular | Bundles several outcomes with no stated priority |
| Verifiable / HasDoneCondition | No observable state says "finished", and none can be reasonably inferred |
| Feasible | Conflicts with a stated constraint (time, tools, skill) |
| Complete | Missing information without which the first task cannot be written |

Route by outcome:

- **All pass** → continue.
- **Fails, but one reading clearly dominates** → continue, and log the reading as an assumption (A1, A2, …) in the document. Asking costs the user a turn; only pay it when the answer changes the plan. [E1]
- **Fails on a material ambiguity, missing done-state, or unranked multi-outcome** → invoke prompt-refiner: read its SKILL.md and run its workflow, seeding it with the failing predicates as the weaknesses to probe. Resume at step 2 with its Refined Objective. State the routing in one line.
- **Already atomic** (passes A1–A6 below as given) → skip to step 3 and emit a single task, no milestones.

Correctness and appropriateness of the objective are not gated: they need domain context and the user's own judgment. Commitment is assumed because the user asked for a plan. [R3]

### 2. Decompose

1. Write the **done-state**: one or two verifiable sentences. [R2]
2. Split into 2–6 **milestones**, each ending in an externally observable checkpoint. Depth is capped at objective → milestone → task; shallow plans fail less. [R5]
3. Split milestones into tasks until every task passes the atomic test:

```
A1  One verb-first action producing one output artifact                 [R2]
A2  Fits one focused work session (P1)                                   [R1]
A3  Done-test is observable; no "understand", "look into", "work on"     [R2, R3]
A4  No embedded decision; make a needed decision its own task whose
    output is the decision                                               [E2]
A5  Inputs exist already or are produced by a listed predecessor
A6  Stop rule: splitting further would not change what the user does
    next, or a miss on this step is cheap                                [E2]
```

4. **Coverage check**: the tasks together equal the done-state, with no overlap between them. [E3]
5. **Unfamiliar work** (the user lacks the knowledge to do the step): emit a time-boxed **spike** whose output is a written answer, list, or decision. Learning goals outperform outcome targets on novel tasks. Tasks that depend on the spike are marked ⚠ provisional. [R2, E5]
6. Insert an explicit VERIFY task after every 3 dependent tasks that produce no externally observable artifact (P3). Long unverified chains compound errors. [R5, X4]

### 3. Enrich

Per task: `In`, `Out`, `Done when`, `Est`, `Start when`, and `⚠` only when genuinely uncertain (say why).

- **Estimates**: unpacking (step 2) is the primary method. Give a range low–high, where high is roughly an 80%-confidence value. Use focused hours in 0.25 steps; never days, because units shift estimates. If the user supplies ≥3 comparable past durations, anchor to them; otherwise do not ask. [R4, R9]
- **Buffer**: one visible line at plan level (P2). Never pad individual tasks. [R9, X1, X3]
- **Start when**: tasks with a predecessor read `After T-xx`. Tasks with none read `When ___ (pick a time/place)`, left blank for the user to fill; they are the ones whose start depends on a cue the skill cannot know. Tell the user once to fill and read the blanks aloud. [R7] Reference predecessors only (never "before T-xx"), so dependencies stay acyclic and machine-readable.
- **Parked**: anything in the objective's wording that is deliberately excluded goes under Parked, so nothing floats unassigned. [R8, weak]

Parameters (unsourced; tune with evals): **P1** session ceiling ≤ 2 h unless the user states another. **P2** buffer +30% on the total for novel work (a floor, not a method). **P3** verify spacing = 3. **P4** plan cap ≈ 40 atomic tasks in full detail; beyond that, fully decompose the first two milestones and leave later ones at milestone level with "expand when reached".

### 4. Verify (silent, one revision pass)

Score the draft against this rubric, fix failures, then emit. Raw first-draft plans are often not executable as written. [Q3, X5]

```
T1 verb-first, single action, single output artifact     P1 tasks cover the done-state, no overlap
T2 In and Out explicit                                   P2 every objective element is a task or Parked
T3 Done-test observable, no judgment call                P3 every task has Start when; roots have blanks
T4 no embedded decision                                  P4 dependencies acyclic; P3 spacing respected
T5 estimate is a range, one unit; spike if knowledge gap P5 no over-splitting (A6)
T6 fits one session                                      P6 gate decision consistent; assumptions logged
                                                         P7 exactly one visible buffer line, no per-task padding
```

### 5. Emit

Write `<slug>-tasks.md` to the outputs directory (`/mnt/user-data/outputs/` if it exists, else the working directory) and present the file. Use this template exactly:

```markdown
# {Refined objective: verb-first, one line}

**Done-state:** {verifiable}
**Effort:** {Σlow}–{Σhigh} focused h · buffer +{P2}% → {total range} h
**Status:** DRAFT. Edit assumptions and estimates before executing.

## Assumptions
- A1 {reading or constraint assumed}. Edit if wrong.

## M1 — {milestone name}
**Checkpoint:** {observable output}

- [ ] **T-01 — {verb-first title}** · est {lo}–{hi} h
  - In: {inputs/prereqs}
  - Out: {artifact}
  - Done when: {observable test}
  - Start when: After T-00 | When ___ (pick a time/place)
  - ⚠ {only if uncertain: reason}

## Parked
- {excluded item}
```

Then reply in chat with **at most** these lines, and do not restate the tasks: gate result (pass / assumptions logged / routed to prompt-refiner); task count, effort range with buffer, and number of ⚠ flags; a review checkpoint asking the user to edit or confirm before executing, since the plan is a draft [R6]. Do not claim the plan will "free the mind" or improve motivation; that evidence is weak [R8].

### 6. ClickUp offer

If ClickUp tools are present or found via tool_search, end the chat reply with one line offering to create the tasks there. Do nothing until the user accepts. On acceptance: load the tool schemas, confirm the target list, then create tasks (name `T-xx title`, description from In/Out/Done when, estimate from the range, dependencies where supported). If no ClickUp tools exist, say nothing about ClickUp.

## Never

Use a fixed multiplier as the estimation method [X1]; cite "8/80" as a rule [X2]; pad tasks invisibly [X3]; chain more than ~5 unverified steps [X4]; present an unreviewed plan as final [X5]; leave a distal objective without proximal tasks [X6]; ask questions the gate does not require [E1].
