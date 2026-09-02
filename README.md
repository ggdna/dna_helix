# dna_helix

The DNA layer that tells a repo how to author a DNA layer of its own.

It carries only that one topic and is one of the layers
[dna_ggdna](https://github.com/ggdna/dna_ggdna) composes, so a repo gets
it by taking the umbrella rather than by naming it.

## Guides

- `dna/doc/guides/dna-guide.md` — the `dna/` layout and the `dot-`
  escape, what belongs in `_dna.json` and `_vars.json`, the three
  override mechanisms, and publishing one layer to both registries

## Skills

- `/dna` — checks a layer against the DNA guide: paths that would not
  instantiate, layers that are not dependencies, variables nothing
  declares, and manifests that drifted apart

## Layers

Orthogonal, and parent-less like every topic layer of this organization.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file,
  set to `ggdna` here

## Usage

Reach it through the umbrella:

```bash
pnpm add -D @ggdna/dna-ggdna   # TypeScript projects
dart pub add dev:dna_ggdna     # Dart projects
gg dna init
```

Naming this layer directly is for a repo that wants the authoring topic
and nothing else:

```bash
pnpm add -D @ggdna/dna-helix
dart pub add dev:dna_helix
```

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
