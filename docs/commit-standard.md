## Format

```
<type>: <imperative title, 72 characters or fewer>

<one or two sentences on what changed and why>
- Added `path/to/file.md`: <why>
- Modified `path/to/file.md`: <why>
- Removed `path/to/file.md`: <why>

ClickUp: <task-id> (https://app.clickup.com/t/<task-id>)
```

If AI helped write the commit, disclose so by adding its `Co-Authored-By:` trailer after the ClickUp line.


## Types

No scope. Use one of these four tags:

| Type | Use for |
|------|---------|
| `research` | New or updated research output under `research/` |
| `fix` | Correcting an error in existing content or tooling |
| `docs` | Guides, standards, the problem statement |
| `chore` | Housekeeping: `.gitignore`, renames, restructuring |

If none fits, the change may be two changes or constitute a new tag. Split it or update the docs.


## Title rules

- Start with the lowercase type, a colon, and a space.
- 72 characters or fewer, including the type.
- Name the deliverable, not the activity. "add brushless motor and ESC overview", not "work on research".


## Description rules

- Open with a brief overview of what changed and why.
- List every file changed as `Added`, `Modified`, or `Removed`, each with a short reason. Renames count as `Removed` plus `Added`, or say "Renamed" with both paths.
- Keep the "why" specific. "Fixes wrong voltage range" beats "updates content".


## ClickUp footer

- Every commit ends with `ClickUp: <task-id> (<link>)`.
- If no task applies (tooling tweaks, typo fixes), write `ClickUp: none`. Never leave the line out, so a missing reference is always deliberate.
- One task per commit. Unrelated changes get separate commits.


## Examples

Good:

```
research: add brushless motor and ESC overview

Covers how brushless motors and ESCs work, so the team can pick
components for the initial build.
- Added `research/components/motors-escs.md`: full write-up using the
  research output template, 4 cited sources

ClickUp: 86abc123 (https://app.clickup.com/t/86abc123)
```

```
fix: correct LiPo cell voltage range in battery notes

The nominal and full-charge voltages were swapped for 2S packs.
- Modified `research/power/lipo-options.md`: swapped values and added
  the datasheet source

ClickUp: none
```

Bad:

```
updated stuff
```

No type, not imperative, no description, no file list, no ClickUp line.


## Before you commit

- [ ] Type is one of `research`, `fix`, `docs`, `chore`
- [ ] Title is imperative and 72 characters or fewer
- [ ] Description says why, and lists every file changed
- [ ] Footer has the ClickUp ID and link, or `ClickUp: none`
- [ ] The commit covers one task only
