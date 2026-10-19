# dna_helix

English | [Deutsch](README.de.md)

Gives a repo the guide and the skill to author a DNA layer of its own and
publish it to pub.dev and npm.

## Motivation

Building a DNA layer has rules of its own: the `dna/` layout and the
`dot-` escape, what goes into `_dna.json` and `_vars.json`, how later
layers override a file, and publishing one layer to two registries. These
rules used to come with dna_ggdna. A topic layer cannot take dna_ggdna:
the umbrella lists every topic layer, and the engine refuses the cycle.
So the guide and the skill were split out into this parent-less layer,
which a topic layer can consume as well.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-helix   # TypeScript projects
dart pub add dev:dna_helix     # Dart projects
gg dna init
```

`gg dna init` places a test that instantiates and verifies the DNA on
every test run. It copies the guide to `doc/guides/` and the skill to
`.claude/skills/dna/`.

A ggdna repo usually gets the layer through the umbrella instead of
naming it:

```bash
pnpm add -D @ggdna/dna-ggdna   # TypeScript projects
dart pub add dev:dna_ggdna     # Dart projects
gg dna init
```

Type `/dna` in Claude Code to have the layer checked against the DNA
guide. The skill lists its findings first and fixes only what you
confirm.

## Guides

- `dna/doc/guides/dna-guide.md` — how to start a layer and why a topic
  layer has no parent, the `dna/` layout and the `dot-` escape, what
  belongs in `_dna.json` and `_vars.json`, the three override mechanisms,
  publishing one layer to both registries, and verifying it with the
  placed test

## Skills

- `/dna` — checks a layer against the DNA guide: paths that would not
  instantiate, layers that are not dependencies, variables nothing
  declares, and manifests that drifted apart

## Scope

The layer is only about authoring layers. It ships nothing a repo needs
that only consumes DNA; the engine that instantiates the layers is helix,
and the topics themselves come from the topic layers.

## Layers

The layer is orthogonal: `dna/_dna.json` lists no parent layers. It
stays parent-less on purpose, so that every other layer can consume it
without closing a cycle back through the umbrella. Today
[dna_ggdna](https://github.com/ggdna/dna_ggdna) lists it as its first
layer; the other umbrellas and the topic layers do not.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file,
  set to `ggdna` here; `mustOverride` in `dna/_dna.json` marks it, so
  every repo that lists this layer sets it in its own `dna/_vars.json`

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.

Edit the files below `dna/`, not their copies in `doc/` and `.claude/`,
which the test overwrites.

## License

MIT — see [LICENSE](LICENSE).
