# Pairing Tool — Improvement Backlog

Items are grouped by theme and roughly ordered by value within each group.
Each item has a **size** estimate (S = 1 session, M = 2–3 sessions, L = multi-session).

> **Status (2026-05-08):** All strategy and UX items below are **shipped**. The only open item is `3a` (Norge data), and it is *intentionally* left incomplete — see note.

---

## 1. Strategy Gap Closures ✅ all done

Features identified in the training recordings that the tool didn't yet surface.

### 1a. Post-Round Matrix Recalibration prompt `S` ✅
**What:** After the results screen is shown, compare each locked game's matrix score against the actual result. Surface a "sanity check" prompt: "Your matrix had Player X at 14 vs Faction Y — if the actual game was closer to 8, tap to update."
**Why:** The strategy guide calls stale estimates the most dangerous compound error — a wrong 14 you keep treating as a counter can distort pairings across multiple rounds.
**Acceptance:** Results screen shows per-game delta between matrix score and (manually entered) actual score. One-tap to update the matrix entry in place.
**Shipped:** `buildRecalibCard()` at index.html:3407, rendered into `#results-recalib`. Repositioned 2026-05-07 to sit directly under the game breakdown so it isn't buried below the fold.

---

### 1b. Estimation Integrity Check `S` ✅
**What:** On the Setup / Composition screen, flag any player whose personal scores are systematically higher than meta by a meaningful gap (e.g. personal avg ≥ meta avg + 3 across the five opponent factions).
**Why:** Optimistic self-assessment cascades — one inflated 14 that should be an 8 can flip a round result. The strategy frames the matrix as a team social contract; overconfidence breaks it silently.
**Acceptance:** Warning row in Composition Analysis: "Player's self-ratings are +N above meta on average — verify with team before pairings."

---

### 1c. Process-of-Elimination Defender Recommendation `S` ✅
**What:** For each of our players, count how many of the 5 opponent factions they appear in as a top-2 counter (score ≥ 13). The player with the fewest appearances is the defender candidate — they're least needed as an attacker.
**Why:** Currently the tool recommends defenders by average score. The strategy guide uses a different criterion: who is *least valuable as an attacker* — those counters should be freed up to attack, not locked away as the defender.
**Acceptance:** Composition Analysis (or defender suggestion panel) adds a "Defender candidate by elimination" row with the player name and a one-line reason.

---

### 1d. Mirror-Match Leverage Warning in Attacker Offer `S` ✅
**What:** On the Stage 1 / Stage 2 attacker-selection screen, if both of our selected attackers score 9–11 vs the opponent's defender, show a warning: "Both offers are draws — no leverage. The opponent can accept either and nothing bad happens."
**Why:** The strategy says a good offer pairs one clear win with one that forces a *different kind of concession*. Two equally neutral offers hand the opponent the initiative.
**Acceptance:** Inline warning chip on attacker selection when both selected scores fall in the 9–11 range.

---

### 1e. Pre-Round Branch Planning Panel `M` ✅
**What:** A lightweight "pre-game prep" step before Stage 1, with two fill-in slots:
- "If they defend with [faction], our plan is…"
- "If they defend with [faction], our plan is…"
Pre-populate the likely opponent defenders from Composition Analysis.
**Why:** The strategy says plan two branches before you sit down — in-the-moment reactive decisions under time pressure are where captains lose leverage. Making this explicit in the tool reinforces the habit.
**Acceptance:** Optional step between Setup and Stage 1. Can be skipped. Saved plans shown as a reference panel during the draft.

---

### 1f. Symmetric opponent attacker prediction `S` ✅
**What:** `attackerSuggestOpponent` previously sorted by *our* score (factions we beat hardest). Replaced with `rankFactionAttackersOpp` which sorts by the opponent's expected score (`oppMetaScore`) — what they'd actually send. Suggestion list now shows two columns: "Their score (est)" and "Our score".
**Why:** A skilled opponent picks attackers the same way we do — where *they* score best. Our previous list was the inverse of reality.
**Acceptance:** "Opponent likely sends" list reorders so the top entry is the faction with the highest opponent-perspective score. Both columns visible.

---

### 1g. Lookahead table-pick hint when losing rolloff `S` ✅
**What:** When we lose the rolloff, an info chip appears at S1 pick 2 and S2 pick 3 if a within-tolerance alternative table yields a higher *team* total (current pick + future pick) than the greedy local choice. Threshold: ≥2 VP team gain at S1, ≥3 VP at S2 (stricter since only Game 5 follows).
**Why:** Greedy single-pick optimisation hides the team angle. The strategy guide explicitly calls out: pick 2 captain might do better taking a less-significant table when this opens up a much-better option for pick 3.
**Acceptance:** Chip appears only when loser, before the relevant pick is made, and only when team net gain exceeds the threshold. Does not auto-pick — purely advisory.

---

## 2. UX / Bug Fixes ✅ all done

Quality-of-life issues noticed in recent sessions.

### 2a. Empty toast on startup `S` ✅
**What:** An empty toast notification appears centered at the bottom of the screen when the app loads.
**Why:** Regression — something is triggering `toast('')` or `toast(undefined)` on init.
**Acceptance:** No toast appears on cold load unless a real error condition is met.

### 2b. Half-visible element at the bottom `S` ✅
**What:** An element is partially visible / clipped at the bottom of the viewport throughout the session (not just on scroll).
**Why:** Likely a sticky or fixed-position element with a z-index or overflow issue.
**Acceptance:** No stray element visible at the bottom in normal use.

---

## 3. Data & Matrix

### 3a. Norge Scores Completion `ongoing` — intentionally left incomplete
**What:** Norge's matrix entries are sparse on purpose.
**Why:** This is the live canary that confirms the META fallback path is firing. As long as Norge's row has missing personal scores, the italic `~N` placeholders and the meta-coloured cells in the matrix prove the fallback chain (`getScore()` → personal → META) is working end to end. Filling them in completely would erase that observability.
**Action:** Do not auto-fill. If real games happen, update by hand — but only the cells that have actual results.

---

## 4. Opponent UX & Clarity ✅ all done

New items identified 2026-05-08.

### 4a. Opponent panel — "leverage" view `S` ✅
**What:** During the draft the captain stares at the opponent right-panel chips and suggestion list. Right now the `attackerSuggestOpponent` table shows "Their score (est) | Our score" — correct but not instantly actionable.
**Why:** Under pairing stress you need to read "they will probably send X — our best answer is Y at score Z." The current layout forces the captain to do that translation in their head.
**Acceptance:** The opponent attacker prediction panel gains a third column (or inline badge) showing the best player we can send against each predicted opponent army and the resulting score. Colour coding unambiguous from our perspective.

---

**Shipped:** `attackerSuggestOpponent` at index.html:1885 — col3 = "We exploit with", colour-coded via `scClass`.

---

### 4b. Terrain sensitivity badge on draft chips `S` ✅
**What:** Add a visible marker to faction chips and suggestion rows for any faction whose terrain preference magnitude (`|dense| + |open| ≥ 3`) is high.
**Why:** Table-sensitive armies (e.g. World Eaters `dense +3`, Tau `open +3`) are the ones opponents commit early to grab the right table. Seeing a badge during the draft primes the captain: "this faction will fight for a table — expect it in the first offer." The tool already has `FACTION_TABLE_PREFS` with all 28 factions but only shows the delta after pairings are locked on the table-pick screen.
**Acceptance:** A small icon or label (e.g. `⛰+` or `table`) appears on any chip / suggestion row for terrain-sensitive factions. Visible during S1 Defender, S1 Attacker, S1 Refusal, and S2 draft phases.

---

**Shipped:** `buildFactionChips` calls `terrainBadge()` — visible on all S1/S2 draft phases and suggestion rows.

---

### 4c. Asset-aware strategy callout `M` ✅
**What:** `computeStrategy` only fires on threshold crossings (red ≤5, pin ≥14, deliver <10). It never tells the captain: "here is your strongest asset right now and here is the target to use it on."
**Why:** Under pairing stress the captain needs an affirmative action, not just a warning. The existing functions `rankFactionsOpponentPerspective()` and `rankPlayerAttackers()` already compute the expected opponent defender and our best counter — but this data is buried in suggestion sub-panels, not surfaced as a clear instruction.
**Acceptance:** Every strategy callout (including "No Urgent Flags") gains a secondary **action line**: the top expected opponent defender, our best counter-player, and the score. Example: *"Expected: Tau (avg opp 13). Best answer: Player 3 — scores 13."* The action line fires even in "none" state so the captain always has a concrete read-out.

---

**Shipped:** `computeAssetLine()` at index.html:1965 — wired into all 5 strategy types including `none`.

---

### 4d. Global ⓘ collapse for verbose explainer text `S` ✅
**What:** Add a small ⓘ toggle button next to verbose description text throughout the UI. Collapsed by default — headline always visible, paragraph/bullets expand on click.
**Why:** Under pairing pressure, long explanatory text in strategy callouts, suggestion panel subtitles, and lookahead hint paragraphs adds noise. The information is valuable to study beforehand or explain to a new captain, but it competes with the signal during live pairings.
**Scope:** (1) Strategy callout body + bullets (`renderStrategyCallout`, line 1981). (2) Suggestion table subtitles (`buildSuggestHTML`). (3) Lookahead hint paragraphs (`s1t-lookahead`, `s2t-lookahead`).
**Acceptance:** ⓘ button present on all three panel types. Collapsed on first render each time. CSS `max-height` transition. No state persisted. Mobile layout unaffected.

---

**Shipped:** ⓘ toggle on `renderStrategyCallout` (line 2111), `buildSuggestHTML` title detail (line 1807), S1/S2 lookahead panels (lines 3238, 3320).

---

### 4e. Strategy callout copy tightening `S` ✅
**What:** All bullet text in `computeStrategy` is verbose — written for a reader with time. Tighten to ≤8 words per bullet, imperative form. The body sentence format is good; keep it.
**Why:** Goes hand-in-hand with 4d. Even in expanded state, bullets should be scannable in half a second. Strip re-explanation from bullets — they should extend the body, not repeat it.
**Acceptance:** All five callout types (trash / avoid / pin / deliver / none) have bullets of ≤8 words each, imperative, no redundant qualifiers.
**Shipped:** All bullets in `computeStrategy` rewritten to ≤8 words, imperative, 2026-05-09.

---

## Session Notes

| Session    | Items worked                                                                                                         |
|------------|----------------------------------------------------------------------------------------------------------------------|
| 2026-05-04 | 1b (implemented, unverified)                                                                                         |
| 2026-05-05 | 1b (verified), 2a, 2b, 1c, 1d, 1a, 1e, 1f, 1g                                                                        |
| 2026-05-06 | Out-of-backlog: global back-button navigation                                                                        |
| 2026-05-07 | Out-of-backlog: setup-screen polish (PRIMARY/FALLBACK badges), persistent Match Matrix card during pairing, full META refresh from current dataslate, recalib card lifted on Results |
| 2026-05-08 | Backlog housekeeping: marked 1a–1g + 2a/2b complete; reframed 3a as intentional fallback canary; added section 4 (4a–4e) |
| 2026-05-09 | 4a–4d confirmed already shipped; 4e: tightened all strategy bullet copy to ≤8 words imperative form |
