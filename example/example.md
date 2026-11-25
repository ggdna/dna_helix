# Example

`dna_helix` is a DNA layer: it ships the guide for building, configuring and
publishing a DNA layer and the `/dna` skill, no library code. Declare it as
a dev dependency and instantiate it once:

```bash
dart pub add dev:dna_helix    # Dart projects
pnpm add -D @ggdna/dna-helix  # TypeScript projects
gg dna init
gg dna build
```

Then type `/dna` in Claude Code to start or check a layer of your own.
