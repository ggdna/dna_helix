# dna_helix

[English](README.md) | Deutsch

Gibt einem Repo den Guide und den Skill, um eine eigene DNA-Schicht zu
schreiben und auf pub.dev und npm zu veröffentlichen.

## Motivation

Eine DNA-Schicht zu bauen hat eigene Regeln: der Aufbau von `dna/` und
das `dot-`-Escape, was in `_dna.json` und `_vars.json` gehört, wie
spätere Schichten eine Datei überschreiben, und wie man eine Schicht in
zwei Registries veröffentlicht. Diese Regeln kamen früher mit dna_ggdna.
Eine Themen-Schicht kann dna_ggdna aber nicht einbinden: Das Umbrella
listet jede Themen-Schicht, und die Engine lehnt den Zyklus ab. Deshalb
wurden Guide und Skill in diese Schicht ohne Eltern ausgelagert, die auch
eine Themen-Schicht einbinden kann.

## Verwendung

Als Dev-Dependency eintragen und einmal initialisieren:

```bash
pnpm add -D @ggdna/dna-helix   # TypeScript projects
dart pub add dev:dna_helix     # Dart projects
gg dna init
```

`gg dna init` legt einen Test ab, der die DNA bei jedem Testlauf
instanziiert und prüft. Er legt den Guide in `doc/guides/` ab und den
Skill in `.claude/skills/dna/`.

Ein ggdna-Repo bekommt die Schicht meist über das Umbrella, statt sie
selbst zu nennen:

```bash
pnpm add -D @ggdna/dna-ggdna   # TypeScript projects
dart pub add dev:dna_ggdna     # Dart projects
gg dna init
```

Tippe `/dna` in Claude Code, um die Schicht gegen den DNA-Guide prüfen zu
lassen. Der Skill listet zuerst die Befunde auf und behebt nur, was du
bestätigst.

## Guides

- `dna/doc/guides/dna-guide.md` — wie man eine Schicht anlegt und warum
  eine Themen-Schicht keine Eltern hat, der Aufbau von `dna/` und das
  `dot-`-Escape, was in `_dna.json` und `_vars.json` gehört, die drei
  Override-Mechanismen, das Veröffentlichen einer Schicht in beide
  Registries und die Prüfung mit dem abgelegten Test

## Skills

- `/dna` — prüft eine Schicht gegen den DNA-Guide: Pfade, die sich nicht
  instanziieren ließen, Schichten, die keine Dependencies sind, Variablen,
  die nirgends deklariert sind, und Manifeste, die auseinanderlaufen

## Umfang

Die Schicht dreht sich nur um das Schreiben von Schichten. Sie liefert
nichts, was ein Repo braucht, das DNA nur nutzt; die Engine, die die
Schichten instanziiert, ist helix, und die Themen selbst kommen aus den
Themen-Schichten.

## Schichten

Die Schicht ist orthogonal: `dna/_dna.json` nennt keine Eltern-Schichten.
Sie bleibt bewusst ohne Eltern, damit jede andere Schicht sie einbinden
kann, ohne über das Umbrella einen Zyklus zu schließen. Heute listet
[dna_ggdna](https://github.com/ggdna/dna_ggdna) sie als erste Schicht;
die anderen Umbrellas und die Themen-Schichten tun das nicht.

## Variablen

- `dnaCopyrightHolder` — der Name im Lizenzkopf jeder Datei, hier auf
  `ggdna` gesetzt; `mustOverride` in `dna/_dna.json` markiert ihn, daher
  setzt ihn jedes Repo, das diese Schicht einbindet, in seiner eigenen
  `dna/_vars.json`

## Entwicklung

Der Ordner `dna/` ist handgeschriebene Quelle und wird nie generiert. Das
Repo instanziiert seine eigene DNA — nach Änderungen `dart test` laufen
lassen; vorher committen, denn eine Datei, die die DNA überschreiben
würde, darf keine uncommittete Arbeit enthalten.

Bearbeite die Dateien unter `dna/`, nicht ihre Kopien in `doc/` und
`.claude/`, die der Test überschreibt.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
