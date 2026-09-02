# dna_helix

The DNA layer that tells a repo how to author a DNA layer of its own.

It carries only that one topic. The whole set of ggdna topic layers is
composed by [dna_ggdna](https://github.com/ggdna/dna_ggdna), which lists
this layer among them.

## Guides

- `dna/doc/guides/dna-guide.md` — the `dna/` layout and the `dot-`
  escape, what belongs in `_dna.json` and `_vars.json`, the three
  override mechanisms, and publishing one layer to both registries

## Skills

- `/dna` — checks a layer against the DNA guide: paths that would not
  instantiate, layers that are not dependencies, variables nothing
  declares, and manifests that drifted apart

## Layers

Orthogonal, and parent-less on purpose. Every ggdna topic layer consumes
this one, so a parent here would close a cycle back through the umbrella —
the engine rejects a graph in which the consuming repo reappears.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file,
  set to `ggdna` here

## Usage

A topic layer of this organization declares it as a dev-dependency and
initializes once:

```bash
pnpm add -D @ggdna/dna-helix   # TypeScript projects
dart pub add dev:dna_helix     # Dart projects
gg dna init
```

Any other repo takes `dna_ggdna` instead — it brings this layer along
with the rest of the set.

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
