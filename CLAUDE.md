# CLAUDE.md — Bunny Box (Camden Fork)

Project context for Claude Code sessions. Read this first every time.

## Core Goal

This repo is a Camden-Winder fork of the Bunny Box BunnyBox installer. It ships Happy Hare MMU configuration and install scripts for three Qidi printer variants. Changes here are consumed by the Qidi Q2 Superuser AOI (`Camden-Winder/Qidi-Q2-superuser`) via the `BUNNYBOX_INSTALLER` URL.

## Repo Layout

```
Q2/
  install-bb-q2.sh              ← Q2 install script. Primary target for most sessions.
  config_hh-standalone/
    bunnybox_macros.cfg         ← Q2 BunnyBox macro file
    mmu/
      base/                     ← Happy Hare base config files (mmu_cut_tip.cfg, mmu_parameters.cfg, etc.)
      addons/                   ← Optional HH addon configs (blobifier, erec cutter, etc.)
      optional/                 ← client_macros.cfg, mmu_menu.cfg
      mmu_vars.cfg              ← User-tunable Happy Hare variables
    slicer_machine_gcodes_hh.md ← Slicer start/end gcode reference

Max4/
  install-bb-max4.sh            ← Max 4 install script
  config_hh-standalone/         ← Same structure as Q2/

Plus4/
  install-bb-p4.sh              ← Plus4 install script
  config_hh-standalone/         ← Same structure as Q2/

addons/
  PFS/                          ← Passive Filament Sensor hardware addon

aht10.py                        ← AHT10 humidity sensor Klipper plugin
klippy.py                       ← Klippy helper
```

## Critical Rules

1. **Never push to `main` directly** — all work goes on a `claude/*` branch; merge via PR.
2. **No versioning system** — this repo has no `AIO_VERSION` or equivalent. Do not add one.
3. **Q2 is the primary target.** When a session only specifies one variant, work on Q2. Do not touch Max4 or Plus4 unless explicitly instructed.
4. **Happy Hare's `install.sh` always runs last** and overwrites files from `config_hh-standalone/`. Any config file that must survive HH's install must be explicitly re-copied after `./install.sh` completes in `install-bb-q2.sh`.
5. **`sudo tee` pattern for elevated file writes** — never `echo > file` with sudo.
6. **No attribution** — do not add session links, generated-by footers, or attribution text to commits, PRs, or issue comments. Use `References #N` only, never `Closes #N`.
7. **Never create a PR to the upstream Wazzup repo** (`Wazzup77/Happy-Hare` or any other upstream). All PRs must target `Camden-Winder/Bunny-Box` only.

## Three Variants

| Variant | Script | Notes |
|---------|--------|-------|
| Q2 | `Q2/install-bb-q2.sh` | Primary. Runs Happy Hare then applies Q2-specific config overrides. |
| Max4 | `Max4/install-bb-max4.sh` | Do not touch unless explicitly instructed. |
| Plus4 | `Plus4/install-bb-p4.sh` | Do not touch unless explicitly instructed. |

## PR Conventions

- **Title format:** `[Q2/Max4/Plus4] — <short description>` or `docs — <short description>`
- Use `.github/PULL_REQUEST_TEMPLATE.md` for all PR bodies
- Include `References #N` in PR body and commit message when applicable
- Do not include Claude session links or attribution

## Troubleshooting Protocol

1. Diagnose before asking. Check the script, inspect the relevant section, form a hypothesis.
2. 3-attempt limit. After 3 failed attempts, stop and report.
3. Give one specific command or action, not a list of things to try.
4. Always include expected output alongside any command you ask the user to run.
