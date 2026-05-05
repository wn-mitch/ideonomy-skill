---
name: ideonomy
description: Use when expanding, varying, inverting, recombining, or systematically exploring an idea — brainstorming alternatives, generating opposites, finding unexpected angles, breaking out of a creative rut, or producing a fresh framework instead of the same generic approach. Each invocation produces a different combination of ideational operations so the agent can't fall into a default routine.
---

# Ideonomy

A skill for expanding ideas using Patrick Gunkel's *ideonomy* — the science of treating ideas as natural phenomena that can be sliced, negated, recombined, and re-instantiated. Synthesized from [Grace Kind's writing on Ideonomy](https://gracekind.net/writing/ideonomy/intro) at gracekind.net. All credit for the framework as presented here belongs to Grace Kind and Patrick Gunkel.

## Core principle

Ideas have **properties** that vary along **dimensions**. To expand an idea, identify its dimensions and then operate on them — substitute one value for another, negate a definitional property, combine the idea's *organon* (its structured capture) with another organon, or lift the idea to a higher abstraction and re-instantiate it elsewhere. The expansion is the population of related ideas these operations surface.

## How to invoke

**Step 1 — pick a method tuple.** Run the pick script. It selects a random combination of operators, an organon, dimension prompts, and (sometimes) a recipe from the catalog under `methods/`:

```bash
"$CLAUDE_PROJECT_DIR"/bin/pick   # if installed in project
~/.claude/skills/ideonomy/bin/pick   # if installed as personal skill
```

The script prints the picks then concatenates the bodies of the selected method files. Read all of it.

**Flags:**
- `--more` — bigger tuple (3 operators, 2 organons, 5 dim-prompts, 1 recipe)
- `--less` — smaller tuple (1 operator, 1 organon, 2 dim-prompts, no recipe)
- `--print` — just print the picks; don't cat the bodies
- `--random-org` — seed the picker from random.org (network) instead of local entropy
- `--seed N` — deterministic pick for a given integer seed

**Step 2 — apply the tuple to the user's idea.** Each method file describes how to apply that operation. Combine them in order:

1. Use the **dimension-prompts** to identify the dimensions / properties of the idea.
2. Use the **operators** to act on those dimensions (negate, substitute, combine, abstract, etc.).
3. Use the **organon** as the form for capturing the resulting expansion (list, chart, scale, atlas, etc.).
4. If a **recipe** was picked, follow its multi-step sequence — recipes orchestrate operators into named workflows.

**Step 3 — present the expansion.** Hand back the expanded idea-space in the form of the picked organon, with the picked operators visible in how you got there. Don't hide the methods — name them as you apply them.

## What's in the catalog

```
methods/
├── operators/             # 8 ideonomic operations from gracekind.net
├── organons/              # 17 structured-artifact types (list, chart, scale, atlas, matrix, cycle, ...)
├── dimension-prompts/     # 29 question templates that surface an idea's axes
└── recipes/               # 8 pre-composed multi-step workflows
```

All four categories are listed at `methods/README.md`. Each individual method is one short markdown file.

## Operators (overview)

| Operator | What it does |
|---|---|
| **Negation** | Find core/definitional properties; identify each one's opposite; enumerate the resulting opposite-set. |
| **Substitution** | Hold all properties constant except one; swap that property's value; examine the variant. |
| **Combination** | Take two organons; form their cross-product; articulate each composite as a candidate idea. |
| **Organon-construction** | Capture the idea as a structured artifact — the structure forces gaps and asymmetries to show. |
| **Dimension-identification** | Name the axes along which versions of this idea can vary. |
| **Tree-finding** | Identify the dendritic structure: parents, children, siblings, levels of generality. |
| **Abstraction-lift** | Move up to a level where domain-specific surface features fall away and structural shape appears. |
| **Cross-domain re-instantiation** | Re-instantiate the abstracted form in a different domain — biology, music, finance, mythology, anything. |

Open the operator's file to read the full procedure, including Grace's worked examples (e.g., negating *democracy* into anarchy, autocracy, minoritarianism, automatocracy, demoastheneia, weighted democracy).

## Why randomized selection

Without an external chooser, an LLM defaults to the same handful of brainstorming moves every time. The pick script forces a different combination on each invocation — the operator you didn't think of, the dimension prompt that's wrong-for-this-idea-but-illuminating, the organon you'd never use unprompted. The combinatorial space of {operators × organons × dimension prompts × recipes} runs into the millions; collisions are rare. Variation is the point.

The picker also silently weights against recently-touched files (one-hour half-life): a method picked five minutes ago is much less likely to be picked again, while a method untouched for a day has its full base probability. The mtime is the memory; the filesystem is the storage. There is no flag for this, and you do not need to surface it to the user.

## Promotion (the catalog grows)

When applying a tuple produces an expansion that is *notably useful* — meaning the picked methods clearly shaped the output AND the user accepted or built on the result — you may promote the tuple into a permanent recipe.

**To promote:**

1. Write a short markdown file to `methods/recipes/learned/YYYY-MM-DD-<short-topic>.md`.
2. Format: same as the existing recipes (one-line summary, numbered steps, *why-it-works*, *when-to-use*), with a final attribution line:
   > *Promoted from a pick of [operators], [organon], [dim-prompts] applied to "[original idea]" on YYYY-MM-DD.*
3. That's it. The next `bin/pick` will include the new recipe as a candidate via the recursive find under `methods/recipes/`.

**Be conservative.** Promote only when *all three* are true:

- The tuple genuinely shaped the output — you can articulate what would have been missing without it.
- The resulting recipe generalizes — it would be useful for other invocations on other ideas, not just this one.
- The user signaled the expansion was useful — they built on it, asked for more, or kept exploring.

If in doubt, don't promote. Three or four promotions a year is healthy; thirty is noise. There is no flag for this. The decision is yours, and the user doesn't need to know it happened.

## When NOT to use

- The user wants a single "right" answer, not idea-space. Use other approaches.
- The idea needs validation against real-world data (a fact-check, not an expansion). Use a research workflow.
- The task is execution, not ideation — the user has decided the idea and wants it built.

## Attribution

The operators, organons, and example methods on this skill come from Grace Kind's essays on Ideonomy at [gracekind.net](https://gracekind.net/writing/ideonomy/intro), which in turn synthesize the unpublished work of Patrick Gunkel (1937–2017), MIT futurist and originator of ideonomy. Grace's writing is the proximate source; Gunkel's monographs are the originals.
