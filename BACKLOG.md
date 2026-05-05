# Pairing Tool — Improvement Backlog

Items are grouped by theme and roughly ordered by value within each group.
Each item has a **size** estimate (S = 1 session, M = 2–3 sessions, L = multi-session).

---

## 1. Strategy Gap Closures

Features identified in the training recordings that the tool doesn't yet surface.

### 1a. Post-Round Matrix Recalibration prompt `S`
**What:** After the results screen is shown, compare each locked game's matrix score against the actual result. Surface a "sanity check" prompt: "Your matrix had Player X at 14 vs Faction Y — if the actual game was closer to 8, tap to update."
**Why:** The strategy guide calls stale estimates the most dangerous compound error — a wrong 14 you keep treating as a counter can distort pairings across multiple rounds.
**Acceptance:** Results screen shows per-game delta between matrix score and (manually entered) actual score. One-tap to update the matrix entry in place.

---

### 1b. Estimation Integrity Check `S`
**What:** On the Setup / Composition screen, flag any player whose personal scores are systematically higher than meta by a meaningful gap (e.g. personal avg ≥ meta avg + 3 across the five opponent factions).
**Why:** Optimistic self-assessment cascades — one inflated 14 that should be an 8 can flip a round result. The strategy frames the matrix as a team social contract; overconfidence breaks it silently.
**Acceptance:** Warning row in Composition Analysis: "Player's self-ratings are +N above meta on average — verify with team before pairings."

---

### 1c. Process-of-Elimination Defender Recommendation `S`
**What:** For each of our players, count how many of the 5 opponent factions they appear in as a top-2 counter (score ≥ 13). The player with the fewest appearances is the defender candidate — they're least needed as an attacker.
**Why:** Currently the tool recommends defenders by average score. The strategy guide uses a different criterion: who is *least valuable as an attacker* — those counters should be freed up to attack, not locked away as the defender.
**Acceptance:** Composition Analysis (or defender suggestion panel) adds a "Defender candidate by elimination" row with the player name and a one-line reason.

---

### 1d. Mirror-Match Leverage Warning in Attacker Offer `S`
**What:** On the Stage 1 / Stage 2 attacker-selection screen, if both of our selected attackers score 9–11 vs the opponent's defender, show a warning: "Both offers are draws — no leverage. The opponent can accept either and nothing bad happens."
**Why:** The strategy says a good offer pairs one clear win with one that forces a *different kind of concession*. Two equally neutral offers hand the opponent the initiative.
**Acceptance:** Inline warning chip on attacker selection when both selected scores fall in the 9–11 range.

---

### 1e. Pre-Round Branch Planning Panel `M`
**What:** A lightweight "pre-game prep" step before Stage 1, with two fill-in slots:
- "If they defend with [faction], our plan is…"
- "If they defend with [faction], our plan is…"
Pre-populate the likely opponent defenders from Composition Analysis.
**Why:** The strategy says plan two branches before you sit down — in-the-moment reactive decisions under time pressure are where captains lose leverage. Making this explicit in the tool reinforces the habit.
**Acceptance:** Optional step between Setup and Stage 1. Can be skipped. Saved plans shown as a reference panel during the draft.

---

## 2. UX / Bug Fixes

Quality-of-life issues noticed in recent sessions.

### 2a. Empty toast on startup `S`
**What:** An empty toast notification appears centered at the bottom of the screen when the app loads.
**Why:** Regression — something is triggering `toast('')` or `toast(undefined)` on init.
**Acceptance:** No toast appears on cold load unless a real error condition is met.

### 2b. Half-visible element at the bottom `S`
**What:** An element is partially visible / clipped at the bottom of the viewport throughout the session (not just on scroll).
**Why:** Likely a sticky or fixed-position element with a z-index or overflow issue.
**Acceptance:** No stray element visible at the bottom in normal use.

---

## 3. Data & Matrix

### 3a. Norge Scores Completion `ongoing`
**What:** Norge's matrix entries are incomplete. Fill in scores as results come in from actual games.
**Why:** Missing scores fall back to meta, which is less accurate for personal matchup history.
**Note:** No code change needed — edit `data/team-data.json` and sync `TEAM_DATA` in `index.html`.

---

## Session Notes

| Session | Items worked |
|---------|-------------|
| 2026-05-04 | 1b (implemented, unverified) |
| 2026-05-05 | 1b (verified), 2a, 2b, 1c, 1d, 1a, 1e |
