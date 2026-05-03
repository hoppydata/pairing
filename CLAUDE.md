# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository documents the pairing rules for 40K team match play — specifically the 5-game pairing sequence used to determine match-ups between two teams per round.

## Contents

- [pairing-rules.md](pairing-rules.md) — The canonical rules document covering the full Stage 1 / Stage 2 sequence, table choice order, and final pairing summary.
- [index.html](index.html) — Single-file browser UI for running the pairing sequence interactively. Open directly in any browser (no build step). Team data is baked in; pick 5 opponent factions to auto-build the matrix.
- [data/team.md](data/team.md) — Human-readable version of the full team assessment matrix (all factions, 0–20 scale).
- [data/team-data.json](data/team-data.json) — Machine-readable team matrix. This is the source of truth loaded by index.html. Update here when scores change.
- [data/meta.md](data/meta.md) — Notes on the global meta matrix and its differential→0–20 conversion.
- [data/pairing-strategy.md](data/pairing-strategy.md) — Pairing coach strategy guide: the matrix concept, team size variants (5/6/8 players, odd vs. even), roster roles, defender/attacker mental model, and the foundational strategies (take out the trash, avoiding a red, pin, deliver-don't-win).
- [data/pairing-uktc-guide.md](data/pairing-uktc-guide.md) — UKTC ITT beginner walkthrough of the Defenders & Attackers draft. External community guide stored verbatim as reference.

## Editing the Rules

The rules document is plain Markdown. When making changes:

- Preserve the table choice order: Team A → Team B → Team B → Team A → Remaining table
- Game 5 is always the two refused attackers from Stage 2 paired against each other on the last remaining table
- The Table Choice Token transfers from Team A to Team B after Stage 1 table picks

## Updating Player Scores

Edit `data/team-data.json`. The `matrix` object is keyed by player name → faction name → score (0–20).
After editing the JSON, also update the inline `TEAM_DATA` constant in `index.html` (search for `const TEAM_DATA`).
Norge's scores are incomplete — add entries as results come in.

## Score Scale
- 0–20 personal matrix: 10 = even, 20 = full win, 0 = full loss
- Meta differential → 0–20: `round(diff / 5) + 10`, clamped [0, 20]
