# ideonomy-skill

A Claude Code skill for expanding ideas using **ideonomy** — Patrick Gunkel's "science of ideas," as synthesized in [Grace Kind's essays at gracekind.net](https://gracekind.net/writing/ideonomy/intro).

The skill teaches an agent to slice, negate, recombine, and re-instantiate any idea using ideonomic operators (negation, substitution, combination, abstraction, etc.) applied to identified dimensions of the idea, captured as structured artifacts called *organons* (lists, charts, scales, atlases, dictionaries, trees).

A small `bin/pick` shell script selects a random combination of operators, organons, dimension-prompts, and recipes on each invocation, so the agent doesn't fall into the same default brainstorming moves every time. The combinatorial space runs into the millions of distinct method tuples.

## Install

```bash
# Clone wherever you keep code
git clone https://github.com/<you>/ideonomy-skill ~/Code/ideonomy-skill

# Symlink into your personal skills directory
ln -s ~/Code/ideonomy-skill ~/.claude/skills/ideonomy
```

After install, the skill is discoverable as `ideonomy` and invokable via the `Skill` tool.

To use it from a different agent harness, point the harness at the repo's `SKILL.md`. The pick script is at `bin/pick`; everything is plain bash + standard tools (`awk`, `sort`, `curl` for the optional `--random-org` flag).

## What's in the catalog

| Path | Count | What it is |
|---|---|---|
| `methods/operators/` | 8 | Ideonomic operations from Grace's essays — negation, substitution, combination, organon-construction, dimension-identification, tree-finding, abstraction-lift, cross-domain re-instantiation. |
| `methods/organons/` | 7 | Structured-artifact types Grace names in her intro — list, chart, graph, atlas, scale, dictionary, tree. |
| `methods/dimension-prompts/` | 25 | Question templates that surface dimensions of an arbitrary idea. Grace describes the method; this catalog provides ready-to-pick prompts. |
| `methods/recipes/` | 8 | Pre-composed multi-step workflows — negation cascade, cross-domain lift, atlas of perspectives, etc. |

## Try it

```bash
$ bin/pick
=== IDEONOMY METHOD TUPLE (this invocation) ===

OPERATORS:
  - abstraction-lift
  - substitution

ORGANONS:
  - scale

DIMENSION-PROMPTS:
  - longevity
  - autonomy
  - reversibility

RECIPE:
  - cross-domain-lift

==============================================

----- /…/operators/abstraction-lift.md -----
[body of abstraction-lift]
…
```

The agent reads everything that follows the header and applies the operators (in order) to the user's idea, using the picked organon as the output form.

## Attribution

- **Patrick Gunkel** (1937–2017) — MIT futurist; originator of ideonomy.
- **Grace Kind** ([gracekind.net](https://gracekind.net)) — synthesized Gunkel's framework in three essays: [Introduction to Ideonomy](https://gracekind.net/writing/ideonomy/intro), [Properties and Dimensions](https://gracekind.net/writing/ideonomy/propertiesanddimensions), [Negation](https://gracekind.net/writing/ideonomy/negation). All operators, organons, and worked examples in this skill trace to her essays. The catalog of dimension-prompts and recipes here is original to this skill but follows the method Grace describes.

If you build on this, please credit Grace and link back to her writing.

## License

The code (`bin/pick`) is MIT.

The prose in `methods/` and `SKILL.md` adapts and extends Grace Kind's published essays. It is shared under [Creative Commons Attribution 4.0 (CC-BY-4.0)](https://creativecommons.org/licenses/by/4.0/) — reuse with attribution to Grace Kind and Patrick Gunkel.
