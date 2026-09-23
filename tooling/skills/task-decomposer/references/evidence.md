# Evidence Map for task-decomposer

Read only when asked why a rule exists or when changing a rule. Tags match SKILL.md.
Evidence tiers: meta-analysis > RCT > observational > expert guidance. "Transfer" = applicability to one human planning coursework/research/build/writing tasks.

## Contents
1. Adopted rules R1–R9 (deep-research pass)
2. Additional rules E1–E5, Q3 (quick-search pass)
3. Excluded rules X1–X6
4. Unsourced parameters P1–P4
5. Unresolved conflicts and unverified items

---

## 1. Adopted rules (deep-research pass)

| ID | Rule | Sources | Tier | Transfer | Confidence |
|---|---|---|---|---|---|
| R1 | Decompose distal objectives into proximal subgoals, each completable in one work session. **No primary study gives a numeric formula scaling task size to project size.** | Bandura & Schunk 1981, JPSP 41(3):586–598, DOI 10.1037/0022-3514.41.3.586 (children, math); Locke & Latham 2002, Am Psychol 57(9):705–717, DOI 10.1037/0003-066X.57.9.705 | RCT; meta-analysis | Med; High | High (qualitative) |
| R2 | Tasks are specific, measurable, hard-but-attainable; for unfamiliar tasks use learning/process goals, not outcome targets. | Locke & Latham 2002 (as above); Klein, Wesson, Hollenbeck & Alge 1999, J Appl Psychol 84(6):885–896, DOI 10.1037/0021-9010.84.6.885 (goal commitment, 83 samples) | Meta-analysis | High | High |
| R3 | Gate decomposition on Unambiguous ∧ Singular ∧ Verifiable ∧ Feasible ∧ Complete plus an explicit done-condition. Correct/Appropriate/Conforming are not automatable. | ISO/IEC/IEEE 29148:2018; INCOSE Guide to Writing Requirements; Locke & Latham 2002 (specificity + feedback prerequisites) | Expert guidance (standards) | Med–High | Med–High. Standards target system specs, not personal objectives. |
| R4 | Unpack before estimating. Unpacking lengthens estimates; it reduced actual bias only in the two experiments with timed real tasks; effect is larger for complex tasks. | Kruger & Evans 2004, JESP 40(5):586–598, DOI 10.1016/j.jesp.2003.11.001 | RCT (5 experiments) | High | High for direction; exact statistics UNVERIFIED (paywalled). |
| R5 | Shallow depth; checkpoint every 1–2 atomic steps; insert verification steps; prefer decomposition-first plus replanning. Error compounds multiplicatively: at 0.95 per step, 5 steps ≈ 0.77 and 10 steps ≈ 0.60. | DisasterBench (arXiv 2025); "Understanding the planning of LLM agents: a survey," arXiv 2402.02716; "Illusion of diminishing returns," arXiv 2509.09677 | Observational; expert review | Med | Med. Benchmarks are agent-execution; principle transfers. SKILL.md operationalizes as P3 = 3 because every task already carries a done-test. |
| R6 | Surface the plan as an editable draft with uncertainty flags and a human review checkpoint. | "Plan-Then-Execute," CHI 2025, arXiv 2502.01390, DOI 10.1145/3706598.3713218 | Controlled HCI study | High | High |
| R7 | Attach an if-then start cue to tasks; encourage rehearsal. Effects larger with contingent if-then format, high motivation, and rehearsal. | Gollwitzer & Sheeran 2006, Adv Exp Soc Psych 38:69–119, DOI 10.1016/S0065-2601(06)38002-1 (94 tests, d = .65; getting-started d = .61); Sheeran, Listrom & Gollwitzer 2024, Eur Rev Soc Psychol 36(1):162–194, DOI 10.1080/10463283.2024.2334563 (642 tests, .27 ≤ d ≤ .66) | Meta-analysis | High | High. SKILL.md uses `After T-xx` for dependent tasks and a blank user-filled cue for root tasks. |
| R8 | Writing a concrete plan for open loops may free attention. Adopt cautiously; do not claim benefits to the user. | Masicampo & Baumeister 2011, JPSP 101(4):667–683, DOI 10.1037/a0024192 | RCT (6 studies) | Med | Low–Med. No direct replication found. The Zeigarnik memory effect largely fails to replicate (Ghibellini & Meier 2025, Humanit Soc Sci Commun 12, Art. 962, DOI 10.1057/s41599-025-05000-w; d_z = 0.15); the Ovsiankina resumption effect holds. The 2025 meta-analysis tests recall, not the intrusive-thought paradigm. |
| R9 | Estimation stack: unpack → reference-class anchor if ≥3–5 comparable past tasks exist → p80 range plus project-level buffer for residual variance. Standardize the unit. | Kruger & Evans 2004; Flyvbjerg 2006, PMJ 37(3):5–15; Flyvbjerg 2008, Eur Plan Stud 16(1):3–21; Jørgensen 2016, IST, DOI 10.1016/j.infsof.2016.01.003 (hours vs. days, d 0.52–0.64); Moløkken-Østvold & Jørgensen 2003; Budzier & Flyvbjerg 2012; Jørgensen 2005 | RCT; observational | High (unpacking, units); Med (reference class) | Med–High. Mean software overrun ≈ 30–40%; worst 18% of public IT projects +130% budget. |

## 2. Additional rules (quick-search pass; secondary sources unless noted)

| ID | Rule | Sources | Tier | Confidence |
|---|---|---|---|---|
| E1 | Route only when clarification changes the outcome; when one reading dominates, proceed and log the assumption. LLMs tend to assume a single reading; models can be trained to ask judiciously and to answer directly otherwise; entropy over user intents predicts when clarification helps. | Zhang, Knox & Choi, "Modeling Future Conversation Turns to Teach LLMs to Ask Clarifying Questions," ICLR 2025, arXiv 2410.13788; Zhang et al., "Clarify When Necessary," NAACL Findings 2025, DOI 10.18653/v1/2025.findings-naacl.306 | Observational (benchmarks, QA/NLP) | Med. Transfer from QA ambiguity to objective readiness is unverified. |
| E2 | Stop decomposing when probability of inadequate performance × cost is acceptable (hierarchical task analysis P×C rule); decompose as-needed when the executor cannot perform a step (ADaPT). | Annett & Duncan 1967, Occup Psychol 41:211–227 (seen via secondary summaries); Prasad et al., "ADaPT," NAACL Findings 2024, pp. 4226–4252, arXiv 2311.05772 | Expert guidance; observational (LLM executors) | Med. ADaPT's principle transfers, its results do not. |
| E3 | Children must sum to exactly 100% of the parent's work, with no overlap. | PMI Practice Standard for Work Breakdown Structures, 2nd ed., 2006 (seen via secondary summaries) | Expert guidance | High that the rule exists; untested on personal tasks. |
| E4 | Work-package criteria: confidently estimable, not further divisible, meaningful deliverable, completable without more information. The 8–80 hour guideline is project-scale. | Secondary lecture/blog summaries; see X2 | Expert guidance | Low–Med. Primary PMI text not opened. Qualitative criteria kept; numbers not adopted. |
| E5 | Unpacking removes the tendency to underestimate without guaranteeing accuracy (people become equally likely to overestimate). Informal 559-task self-report: actuals ≈ 1.7× estimates on average (median 1.4×), worst for writing and coding. | Kruger & Evans 2004; Forsyth & Burt 2008, Mem Cognit 36(4):791–798 (seen via secondary summaries); community blog report of 559 tasks (informal) | RCT; anecdote | Low–Med. |
| Q3 | Run a self-critique/refine pass before surfacing a plan; raw LLM plans reach human-teacher quality only after a simulate-reflect-refine loop; only 35–73% of planned steps may be executable depending on model. | npj Science of Learning 2025, DOI 10.1038/s41539-025-00300-x; VECSR, arXiv 2505.02144; arXiv 2507.23589 | Observational | Med. |

Merged tags: the start-cue evidence (quick pass E6) is R7; loop closure (E7) is R8.

## 3. Excluded rules

| ID | Excluded | Why |
|---|---|---|
| X1 | A single fixed time multiplier as the primary estimation method | Overrun variance is large (mean ≈ 30%, worst decile +130%); at best a floor. Use unpacking + reference class. |
| X2 | "8/80" as an empirically grounded sizing law | Practitioner heuristic (commonly attributed to Verzuh), often mislabeled as PMBOK; no primary PMBOK text found; no validation for individual executors. |
| X3 | Per-task hidden padding | Invites Parkinson's law; use one visible project-level buffer. |
| X4 | Long unverified plan chains (> ~5 steps) | Error compounding: 0.95⁵ ≈ 0.77, 0.95¹⁰ ≈ 0.60. |
| X5 | Treating raw LLM plans as executable | Executable-and-correct rates as low as 35%; fidelity 23–73% by model. |
| X6 | Distal-only goals | Barely better than no goal (Bandura & Schunk 1981). |

## 4. Unsourced parameters (tune with evals)

| ID | Default | Rationale |
|---|---|---|
| P1 | Session ceiling ≤ 2 h | Operationalizes R1 "one work session"; user-overridable. Variable scaling was the user's choice; no numeric size rule exists in the evidence. |
| P2 | Buffer +30% for novel work | Consistent with mean overrun ≈ 30–40% (R9); floor only. |
| P3 | Explicit VERIFY task after 3 dependent tasks without an observable artifact | R5 says checkpoint every 1–2 steps; done-tests already act as per-task checkpoints. |
| P4 | ≈ 40 atomic tasks in full detail; beyond, expand first two milestones only | Guards against X4 (long unverified chains); coarse-to-fine detail is standard PM practice. |

## 5. Unresolved conflicts and unverified items

1. **Where unpacking works.** The deep-research pass says unpacking helps most under epistemic uncertainty (it surfaces hidden steps); a preliminary 2023 conference poster (Carney & Ülkümen, perceived uncertainty) reports unpacking raised estimates only under aleatory uncertainty. Boundary unsettled. SKILL.md keeps unpack-always (R4, RCT) and handles knowledge gaps with spikes, which does not depend on the resolution.
2. **Unpacking direction.** Kruger & Evans: unpacking raises and debiases estimates. Xiao 2025 (CMU dissertation): unpacking can lower perceived effort and produce more ambitious plans. Reconciled by task complexity; boundary unsettled.
3. **Goal-difficulty function.** Locke & Latham report a near-linear relation; Kyllo & Landers 1995 (sport) found only moderately difficult goals significant.
4. **Zeigarnik foundation of R8** is weakened; the plan-making finding itself is unreplicated.
5. **Fixed buffer vs. outside view.** Practitioners endorse ~20–30% buffers; Flyvbjerg argues any inside-view multiplier is inferior to reference-class forecasting. Unresolved for low-stakes individual tasks.
6. **8/80 provenance** is muddled (PMI, Verzuh, an unrelated healthcare rule). No primary citation confirmed.
7. **Not yet transferred from idea-intake:** brainstorming/writing-with-AI findings. Candidate carry-overs: visible assumptions list (kept as Assumptions), evidence-based stop conditions instead of round caps (kept as A6), user keeps the final call (kept as R6 review checkpoint). Diverge/converge turn-splitting and the regime diagnostic were left out because they add turns without value when the objective is already clear.
