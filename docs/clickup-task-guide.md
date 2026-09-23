## Principles

1. **ClickUp tracks the work; the repo keeps the result.** Every task links to its output file in the repo, and every output file links back to its task.
2. **One person, one deliverable.** If a task needs two people or two outputs, split it.
3. **Finishable in about a week or less.** Bigger than that means it's really a set of tasks.
4. **Tie it to a goal.** Every task says which problem-statement goal or open question it serves. If it serves none, question whether it's needed.
5. **Write for a cold reader.** Put the context in the task. Nobody should need a hallway conversation to understand it.
6. **Say what "done" means.** A task with no definition of done never finishes.
7. **Someone else signs off.** Every task names a reviewer. Review happens in ClickUp (`In Review`), since we commit directly to the repo and have no pull-request gate.


## Status flow

`To Do` → `In Progress` → `In Review` → `Done`



## Task template

Use this for most tasks. Keep it short and plain.

```
Title: <verb + deliverable, e.g. "Explain how brushless motors and ESCs work">

Goal: <one sentence: what exists when this is done>
Why it matters: <problem-statement goal or open question this serves>
Context / inputs: <links, prior tasks, things to read first>
Output: <repo path, e.g. research/components/motors-escs.md>
Definition of done: <quantiative/qualitative critereon, checklist>
Reviewer: <name>
```


## Good task vs. bad task

- Bad: "Research batteries."
- Good: "Compare 1S–4S LiPo options for a sub-250 g indoor drone within our budget; recommend one and list safety handling requirements. Output: `research/power/lipo-options.md`. Done when: template complete, ≥3 cited sources, reviewed by <name>."

## Closing a task

1. Output file committed and its path pasted into the task.
2. Definition-of-done checklist ticked.
3. Status set to `In Review`, reviewer tagged.
4. Reviewer approves in a ClickUp comment.
5. Status set to `Done`. Follow-up work becomes new tasks; don't leave it buried in the write-up.
