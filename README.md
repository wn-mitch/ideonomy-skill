# ideonomy — plain & rich

> *Ideas are natural phenomena. They have properties. They live along dimensions. They can be sliced, negated, recombined, and re-instantiated like any other natural object.*
> — after Patrick Gunkel, via Grace Kind

A pair of skills that turn any idea into a populated neighborhood of related ideas, by applying combinations of *ideonomic operators* — negate, substitute, combine, abstract, re-instantiate, find-the-tree — drawn from a randomized tuple at every invocation.

Every call picks a different combination of operators, organons, and dimensional prompts from a catalog of millions of distinct method-tuples. The agent doesn't get to fall back on its default brainstorming moves. That's the whole point.

The two skills share one brain (operators × organons × dimension-prompts × picker × cooldown) and differ only in how they render the artifact:

| Skill | Rendering | Best channel |
|---|---|---|
| **`ideonomy-plain`** | Plain Markdown lists, fenced-code-block tables, no Unicode box-drawing. | Anywhere — including SMS bridges, Telegram, plain Slack DMs, and any context where Unicode might mangle. |
| **`ideonomy-rich`** | Performative ASCII art: figlet banners, Unicode box-drawing, density gradients, visible ideonomy-machinery layers (tuple legend, dimensions surfaced, operator-named dividers, ideonomy trail). | Terminals, READMEs, blog posts with monospace code blocks, fixed-width-font emails, ttyrec sessions. |

Default to `ideonomy-plain`. Use `ideonomy-rich` when you know the medium can hold the art.

---

## Try the rite

```bash
$ ~/.claude/skills/ideonomy-plain/bin/pick    # or ideonomy-rich; same picker
```

```
=== IDEONOMY METHOD TUPLE (this invocation) ===

OPERATORS:
  - abstraction-lift
  - cross-domain-reinstantiation

ORGANONS:
  - periodic-grid

DIMENSION-PROMPTS:
  - longevity
  - autonomy
  - reversibility

==============================================

[…bodies of each picked method file follow, ready for the agent to apply…]
```

Then ask your agent to apply the tuple to your idea. What you'll get back: five or ten unfamiliar variants of the idea, organized into the picked organon, with the picked operators visible in how the agent got there. Sometimes the result is brilliant. Sometimes it's nonsense. Both are useful — the nonsense tells you which dimensions of your idea were load-bearing.

Run it ten times on the same idea. The expansions won't repeat.

---

## The bargain

Each skill folder is fully self-contained — drop either or both into any agent's `skills/` directory and they load. No installer, no symlinks, no build step.

```bash
git clone git@github.com:latentwill/ideonomy-skill.git
cp -R ideonomy-skill/ideonomy-plain  <your-skills-folder>/
cp -R ideonomy-skill/ideonomy-rich   <your-skills-folder>/   # optional
```

Common destinations:

| Agent | Skills folder |
|---|---|
| Claude Code | `~/.claude/skills/` |
| Cowork | `~/Library/Application Support/Claude/local-agent-mode-sessions/skills-plugin/<global-uuid>/<workspace-uuid>/skills/` |
| Anything else with a Claude-style skill loader | wherever it puts `SKILL.md`-based skills |

The agent picks `ideonomy-plain` vs `ideonomy-rich` automatically based on the channel — that's why both skills carry their own description. Default to `ideonomy-plain` if you only want one.

Pure bash + standard tools (`awk`, `sort`, `find`, `curl` only for the optional `--random-org` flag). `ideonomy-rich` additionally benefits from `figlet` / `boxes` / `toilet` if installed (`brew install figlet boxes toilet`), but always falls back to the public `asciified.thelicato.io` API.

> **Maintainer note:** the operator/organon/dimension-prompt catalog and `bin/pick` live in `ideonomy-plain/`. `ideonomy-rich/` carries duplicate copies so it can drop in alone — when you change a method file or the picker, update both folders. (`diff -r ideonomy-plain/methods ideonomy-rich/methods` to check.)

---

## What's inside

```
ideonomy-skill/
├── ideonomy-plain/        ← portable rendering (default)
│   ├── SKILL.md
│   ├── bin/pick           ← the chooser
│   ├── methods/           ← operators, organons, dimension-prompts
│   └── examples/
└── ideonomy-rich/         ← monospace-rich rendering
    ├── SKILL.md
    ├── bin/pick           ← thin wrapper → ../ideonomy-plain/bin/pick
    └── rendering/         ← per-organon ASCII recipes
                              (chart, tree, list, atlas, scale, cycle, dictionary)
```

The catalog (single source of truth):

| Path | Count | Role |
|---|---|---|
| `ideonomy-plain/methods/operators/` | 8 | The ideonomic operations: negate, substitute, combine, organon-construct, identify-dimensions, find-trees, abstraction-lift, cross-domain-reinstantiate |
| `ideonomy-plain/methods/organons/` | 17 | Structured-artifact types — list, chart, graph, atlas, scale, dictionary, tree, plus matrix, cycle, spectrum, timeline, lattice, map, notation, procedure, state-machine, periodic-grid |
| `ideonomy-plain/methods/dimension-prompts/` | 29 | Question templates that surface an idea's axes — longevity, polarity, autonomy, naturalness, reversibility, … |
| `ideonomy-plain/bin/pick` | 1 | The chooser. ~1.7M distinct tuples in default mode; ~900M in `--more`. |

There is deliberately no `recipes/` directory — no saved-combinations layer. Combinations are what the picker produces by drawing operators × organons × dimension-prompts; freezing past combinations into named recipes pulls the picker toward defaults and works against the random-selection mechanism that makes the skill useful in the first place. A handful of historical recipe sketches survive under `ideonomy-plain/examples/historical-recipes/` for browsing only; they are not part of the active catalog.

`bin/pick` flags (intentionally few): `--more` (bigger tuple), `--less` (smaller), `--print` (skip the bodies), `--random-org` (true randomness via random.org's HTTP API), `--seed N` (deterministic, for testing).

---

## Silent self-improvement

**Mtime memory.** Every picked file gets `touch`ed at the end of the run. The picker weights against recently-touched files on a one-hour half-life, so within a single session the catalog *rotates* — methods you used five minutes ago are much less likely to come up again. The filesystem is the memory; no log file, no state directory.

When a tuple produces a notably useful expansion, the agent may grow the catalog by promoting *down* into primitives — a new operator, organon, or dimension-prompt. Never up into a saved-combinations layer; that's the trap that re-introduces defaults.

---

## The lineage

**Patrick Gunkel** (1937–2017) — MIT futurist, originator of *ideonomy*: the science of ideas. He spent decades producing thousands of pages of monographs, lists, charts, and divisions cataloguing the structural anatomy of human thought. His original site lives at:

→ **[ideonomy.mit.edu](https://ideonomy.mit.edu)**

The PDFs there are wild. Mendeleev-table-grade wild. Gunkel was working at a level of generality most people never visit, and the scanned monographs (Orange, Bright Green, Blue, Pastel Green, Yellow) are dense beyond reading. They are also the source. Browse them, get lost, come back changed.

**Grace Kind** ([gracekind.net](https://gracekind.net)) — independent writer and researcher whose three essays translate Gunkel into something a present-day reader can actually use:

- [Introduction to Ideonomy](https://gracekind.net/writing/ideonomy/intro)
- [Properties and Dimensions](https://gracekind.net/writing/ideonomy/propertiesanddimensions)
- [Negation](https://gracekind.net/writing/ideonomy/negation)

This skill is built directly on her synthesis. Every operator, every organon she explicitly names, every worked example here traces to her writing. The dimension-prompts and recipes are original to this skill but follow the method she describes. **If you build on this, credit Grace and link her work.**

---

## Why this exists

LLMs are powerful brainstormers, but left to their own devices they produce variations of the same handful of moves: list-the-obvious, scale-it-up, add-a-feature, remove-a-feature, give-it-an-app. The space they actually explore is small, and after a few invocations the user can predict the next response.

Ideonomy is a different shape: identify the *dimensions* of an idea, then operate on them. The space of *all the ideas adjacent to this one* is enormous and weird. The picker forces the model into corners of that space it would not otherwise visit. The corner you get sent to this run is not the corner you got sent to last run, because the picker doesn't repeat.

The result, when it works, is the model producing variants you couldn't have produced — not because the model is smarter, but because it was forced into an angle of approach you wouldn't have asked for.

---

## License

Code (`bin/pick`): MIT.

Prose (`SKILL.md`, `README.md`, `methods/**.md`, `examples/`): Creative Commons Attribution 4.0. Reuse, remix, redistribute — with credit to Grace Kind and Patrick Gunkel.

---

<sub>*fnord*</sub>
