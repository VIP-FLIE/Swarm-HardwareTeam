---
name: prompt-refiner
description: "Refine and improve project objectives and prompts through professional analysis and exploratory questioning. Use this skill whenever a user presents a project idea, objective, task description, or prompt that could benefit from clarification—whether it's vague, ambitious, multi-faceted, or missing key details. The skill provides domain-agnostic expert critique, identifies ambiguities and weaknesses, offers actionable recommendations, and adaptively asks clarifying questions until the objective is sharp and well-defined. Trigger on any request that involves planning, defining, or articulating a goal or task, even if the user doesn't explicitly ask for refinement."
---

# Prompt Refiner Skill

## Overview

This skill helps users transform loose, ambiguous, or incomplete project objectives into sharp, actionable, well-defined goals. It operates in two phases:

1. **Professional Analysis Phase**: Critically examine the objective for gaps, ambiguities, assumptions, and opportunities for improvement—acting as a domain expert would.
2. **Exploratory Questioning Phase**: Ask adaptive, targeted questions to clarify remaining ambiguities and lock in critical details until the objective is truly refined.

The output is a structured analysis presented conversationally, showing the original objective, identified strengths and weaknesses, professional recommendations, and a refined version of the objective informed by the user's answers.

## When to Use This Skill

- **Multi-faceted projects**: Multiple competing goals or unclear priorities
- **Research or planning queries**: Where success criteria and scope are undefined
- **Creative or business ideas**: Before execution, lock in what "done" actually looks like
- **Ambiguous prompts for other tasks**: Before diving into writing, coding, or analysis
- **Any user-provided objective that could benefit from expert critique**: Even if they don't ask for it

## Workflow

### Phase 1: Professional Critical Analysis

When the user presents their objective, perform a thorough expert analysis. To do this well:

1. **Identify what's stated explicitly** and note what's implicit or missing
2. **Ask yourself**: What assumptions is this objective making? What could go wrong? What's unclear?
3. **Think like a domain expert**: If this were a real project you were advising on, what questions would you raise? What traps do you see?
4. **Be constructive but honest**: Point out both strengths (what's clear, feasible, well-scoped) and weaknesses (ambiguities, scope creep risks, undefined success criteria, missing dependencies)
5. **Suggest improvements**: Offer 2–4 concrete, actionable recommendations based on professional best practices

Present this analysis in the following structure:

#### Original Objective
State the user's objective as they provided it.

#### Weaknesses
What's ambiguous, under-specified, at risk of scope creep, or missing? Be specific. Examples:
- Undefined success criteria
- Unclear timeline or resource constraints
- Conflicting goals
- Missing dependencies or prerequisites
- Assumptions that may not hold
- Vague scope ("build an app" vs. "iOS app that syncs data to cloud")

#### Recommendations
Suggest 2–4 actionable improvements a professional would make. Examples:
- Define success metrics explicitly
- Clarify constraints (time, budget, skill level, tools)
- Break multi-faceted goals into ranked priorities
- Specify the user's role and the user's audience
- Identify blockers or dependencies

### Phase 2: Exploratory Questioning

After presenting your analysis, ask adaptive, open-ended questions to clarify ambiguities and lock in critical details. Follow these principles:

1. **Ask iteratively**: Don't dump all questions at once. Ask 3-5 questions, listen to the answers, then ask the next round based on what you learned.
2. **Be targeted**: Focus questions on the weaknesses and ambiguities you identified in Phase 1, not generic questions.
3. **Adapt to the domain**: Adjust question depth and style based on what the objective actually is (a business plan asks different questions than a creative writing project).
4. **Stop when ambiguity is resolved**: You don't need a fixed number of questions. Ask until the objective is clear enough to act on.
5. **Summarize understanding**: After each round of answers, briefly confirm what you've learned and what still needs clarification.

### Phase 3: Present the Refined Objective

Once you've gathered enough information, present a **Refined Version** of the objective. This should be:
- **Specific**: Concrete, not abstract
- **Scoped**: Time, resource, and capability boundaries are clear
- **Measurable**: Success criteria are defined or implied
- **Actionable**: A professional could hand this to a team and they'd understand what to build/create/do

## Example Workflow

**User input**: "I want to write a book about productivity"

**Phase 1 Analysis**:
- **Strengths**: Clear topic area, ambitious
- **Weaknesses**: Genre undefined (self-help vs. memoir vs. narrative), audience unknown, scope massive, timeline missing, research depth undefined
- **Recommendations**: 
  1. Specify genre and sub-topic
  2. Define your target reader
  3. Set a realistic word count and timeline
  4. Decide: original research or synthesis of existing ideas?

**Phase 2 Questioning**:
- Q: "Are you writing for busy professionals, students, or a general audience?"
- [User answers]
- Q: "Is this a how-to guide, a conceptual exploration, or something combining research with personal story?"
- [User answers]
- Q: "Do you have a target word count and timeline in mind?"
- [Continue adaptively based on answers]

**Phase 3 Refined Objective**:
"A 50,000-word practical guide on productivity for busy professionals in tech, covering time-blocking, deep work, and habit stacking. Target completion: 12 months. Audience: mid-career engineers and managers. Mix of original research (surveys) and synthesis of existing productivity frameworks."

## Guidelines for Objectivity and Professionalism

- **Be honest, not cheerleading**: Point out real weaknesses and risks, not just validate the idea
- **Reference domain standards**: "In software projects, undefined requirements lead to X" or "Business plans typically include Y"
- **Avoid opinion**: Distinguish between objective ambiguities ("success criteria aren't defined") and subjective preferences ("this idea is boring")
- **Acknowledge constraints**: If the user has real limitations (time, budget, skill), work with them, don't dismiss them
- **Ask *why* behind answers**: Sometimes the user's first answer hides deeper assumptions—probe gently

## Special Cases

### The objective is already well-defined
If the user's objective is already clear, specific, and bounded, acknowledge this and ask if they want to explore it further or if they're ready to proceed. Don't force refinement where it's not needed.

### The objective is so loose it's unscoped
If the objective is extremely broad ("I want to be more creative" or "change the world"), begin with a clarifying conversation to understand what's actually driving them, then help them narrow to a concrete, actionable project.

### Conflicting goals
If the objective has multiple competing aims, help the user rank them or separate them into distinct sub-projects.

---

## Output Format

Present the analysis conversationally in chat. Structure it as:

```
## Original Objective
[User's stated objective]

## Weaknesses
- [Weakness 1]
- [Weakness 2]

[Continue to questioning phase]

## Refined Objective
[Final refined version based on all answers]
```

Keep the tone professional, constructive, and collaborative. You're a critic, not a skeptic.