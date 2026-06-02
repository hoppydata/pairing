# MEMORY FILE — WH40k 11th Edition Core Rules Reference (for Claude's future use)

> **Purpose:** This is an internal reference for Claude to answer Daniel's WH40k 11th-edition rules questions accurately in future conversations. Daniel plays competitive 40k (Grey Knights / Space Marines, White Scars interest), organizes tournaments (Würfelkommando, Div Kom, Upper Austria), communicates in German, fact-checks rigorously, and wants concise, precise, actionable answers. **Answer rules questions in German unless he writes in English.**
>
> **Source hierarchy & reliability:**
> 1. **Official Core Rules PDF (88 pp, GW, verified 2026-06-01)** — authoritative for everything in sections 01–24 below. Section numbers (e.g. 13.09) are the official internal reference numbers; cite them when useful.
> 2. **Official Warhammer-Community previews** — used for Army Building / Missions / Detachments, which are NOT in the Core Rules PDF.
> 3. **Faction Focus articles** — for Detachment specifics (see separate Faction docs).
>
> **What is NOT in the Core Rules PDF:** Detachment Points, Force Dispositions, Missions, Deployment maps, faction Detachments. Those come from preview/mission material — flag the lower confidence when answering.
>
> Output files Daniel has: `WH40k_11te_Edition_Regeln_Zusammenfassung.md` (Update 1), `_Update2.md` (Faction Focuses pt.1), `_Update3.md` (Faction Focuses pt.2 incl. Grey Knights), `_GRUNDREGELN_final.md` (official-verified core rules, German), and combined PDFs.

---

## CONFIRMED CORE RULES (official, section-numbered)

### Battle round structure (14.02)
- Each battle round: Start → both Player Turns → End. Same player goes first every round (mission decides).
- Turn = Start of Turn → Command → Movement → Shooting → Charge → Combat → End of Turn.

### Command phase (08)
- Order: Start → gain **+1 CP** → **Battle-shock** → Command Abilities → End.
- Battle-shock test (in active player's Command phase) for each unit that is **already battle-shocked OR at half-strength or below**. A battle-shocked unit stops being so only if its test **succeeds**. Effects: OC 0, no Stratagems, Desperate Escape on Fall Back.

### Engagement / cohesion (02.09, 03.04)
- **Engagement range = 2" horizontal AND 5" vertical.**
- Cohesion: each model ≤2"h/5"v from ≥1 other model; ≤9"h/5"v from ALL others. Out-of-cohesion at End of Turn → destroy models until restored.

### Movement (03, 09)
- Types: Remain Stationary; Normal (M"); Advance (M"+D6, then no charge/action); Fall Back (M", Orderly or Desperate Escape); Disembark; Ingress (reserves arrival).
- Move through friendly models OK; not through enemy models (exceptions: Desperate Escape, FLY, Monster/Vehicle 17.01).

### FLY / "Take to the skies" (21.03)
- On Normal/Advance/Fall-Back/Charge move, FLY unit may "take off": **−2" max distance**. Then: ignore all vertical distance; move through ALL model types (incl. Monster/Vehicle) and ALL terrain categories (horizontal + vertical).

### MOBILE keyword (terrain 13.06) — **the answer to the recurring "MOUNTED" question**
- **No "MOUNTED" rules section or keyword exists in the Core Rules PDF (zero occurrences).** MOUNTED persists only as a datasheet category (e.g. gets no cover benefit).
- **MOBILE** models can move **horizontally through dense terrain** (like INF/BEASTS/SWARM) but **NOT vertically**. Which units have MOBILE = on the datasheet, not core rules.
- Super-Heavy Walker (24.35) may opt into MOBILE for a move (then through models + terrain ≤4" high; roll D6, on 1 battle-shocked).
- **When Daniel asks about Outriders/bikes:** the movement mechanic is MOBILE; confirm specifics from the unit's datasheet, which Claude has not seen.

### Shooting (10)
- Types: Normal (unengaged, not advanced); Assault (unengaged + advanced + [ASSAULT]); Close Combat Shooting (engaged + [CLOSE COMBAT] or Monster/Vehicle); Indirect Fire (target gets cover; no hit re-rolls; unmod 1–5 miss, 1–3 if stationary & visible to a friend).

### Attack sequence (04, 05)
- Hit: unmod 6 = crit, unmod 1 = fail, else ≥ BS/WS.
- Wound table: S≥2×T → 2+; S>T → 3+; S=T → 4+; S<T → 5+; S≤½T → 6+.
- Save: AP worsens save; Inv ignores AP. Allocate by groups, wounded models first.
- Mortal wounds (06.02): normal damage first, then mortals.
- **Hazard roll / [HAZARDOUS]** (06.03, 24.15): roll D6 per model/weapon → 1–2 = 1 MW (3 MW if all Monster/Vehicle). [HAZARDOUS] rolled AFTER the unit resolves all its attacks.

### Charge (11)
- Declare if enemy ≤12", not engaged, not advanced/fell-back. Charge roll 2D6 = max distance.
- **Select targets AFTER the roll** (within 12" and within rolled distance).
- While moving: each model closer to target; any that can end ≤1" must; any that can end engaged must.
- After: engaged with ALL charge targets, NOT engaged with non-targets. Charging unit gains **Fights First** until end of turn.

### Combat phase (12): Pile In → Fight → Consolidate
- **Pile In (12.03):** both players, **active player resolves all first**, then opponent. Max 3". Eligible: engaged / charged this turn / selected for overrun.
- **Fight (12.04)** — two stages, ALTERNATING selection:
  1. **Resolve Fights First Combats:** starting with the active player, players alternate selecting one eligible Fights-First unit each. When none remain eligible → go to stage 2.
  2. **Resolve Remaining Combats:** starting with whoever moved the sequence to this stage, players alternate selecting one eligible unit each.
  - If a Remaining-stage fight makes a NEW Fights-First unit eligible → jump back to stage 1.
  - NB: it is alternating, NOT "all your units first." Correct an earlier preview-era oversimplification if it resurfaces.
- **Overrun Fight (12.06):** unit unengaged (or was at start of Fight step) that BECAME engaged during the Fight phase → may make one extra pile-in move, then fights. Can pull previously-unengaged enemies into engagement (they then become eligible to fight).
- **Consolidate (12.07/12.08):** both players, active first, max 3". Modes: Continuous (if engaged); Engagement (≤5" to enemy — pulling in a not-yet-fought enemy lets opponent fight it); Objective (≤5" to objective).
- **Counter-Offensive** (Stratagem, 2 CP): your unit gains Fights First, must be selected next.

### Terrain (13)
- **Terrain feature** = physical scenery; **terrain area** = defined footprint.
- Categories: **Exposed** (13.03, free move, scant cover), **Light** (13.04, cover, no movement block), **Dense** (13.05, blocks big models, hides squads).
- Movement (13.06): Exposed/Light free for all; Dense → INF/BEASTS/SWARM/MOBILE horizontal, INF/BEASTS/SWARM also vertical, others only through ≤2"-high sections else climb. End-of-move on elevated surfaces only for INF/BEASTS/SWARM/FLY/MONSTER.
- Vertical move: stay ≤½" horizontally of the feature; add up+down distance to move.
- **Benefit of Cover (13.08): worsen attacker's BS/Hit by 1** (NOT +1 save). Applies to INF/BEASTS/SWARM in a terrain area, or any unit not fully visible through intervening terrain. **Monsters/Vehicles/MOUNTED don't get it from being in terrain** — only via "not fully visible."
- **Hidden (13.09):** model is INF/BEASTS/SWARM in a terrain area **containing ≥1 DENSE feature**, AND its unit made no ranged attacks this turn or previous turn. Hidden = visible only to enemies within **detection range 15"** (unless modified).
- **Obscuring (13.10):** terrain areas with light/dense features block lines of sight passing fully through them.
- **Solid (13.11):** dense features block LoS through openings ≤3" above ground.
- **Plunging Fire (22.05):** from elevated terrain (or TOWERING within 12") → +1 BS vs ground targets.

### Objectives (14)
- Each objective sits on a terrain area; "within range" = within that area.
- Control level = sum of OC within range. Higher controls; tie = nobody (unless Secured).
- **Secured (14.03):** stays controlled even with no models present, until opponent's control level is higher at end of a phase.

### Stratagem usage (15.01)
- Same stratagem max **once per phase**. Default: **a unit can't be targeted by more than one stratagem per phase** (no stacking).
- Core stratagems with exact values: Command Re-roll (1, charge re-roll = 1 die); Insane Bravery (1, once per battle); Epic Challenge (1, [PRECISION] for a character); Rapid Ingress (1, arrival at end of enemy Movement, not round 1); Fire Overwatch (1, snap shots); Smoke Screen (1); Heroic Intervention (1; modes Leap to Defend / Into the Fray +1 CP, cap charge at 6, any target ≤6"); Counter-Offensive (2); Explosives (1, ex-"Grenades": engaged ≤6", D6 4+ = 1 MW); Crushing Impact (1, ex-"Tank Shock": after Monster/Vehicle charge, roll D6=Toughness, each 6 self-MW, each 5+ enemy-MW, max 6).
- **Snap shots (15.09):** target ≤24", hit ONLY on unmod 6, no re-rolls.

### Transports (18)
- Disembark modes — set-up distance **Rapid/Tactical 3", Combat 6"**:
  - Rapid (transport moved Normal/Ingress): no charge after; inherits transport's ingress restrictions (e.g. >8" from enemy).
  - Tactical (transport stationary/not yet moved): unit may then Normal/Advance.
  - **Combat (6"):** hazard roll per model; may be set up engaged with enemies the transport is engaged with; unit is **battle-shocked** and **can't charge**. NOT a free assault.
  - Emergency (transport destroyed): 6", hazard roll per model.

### Attached units (19, 24.22/24.34)
- Leader can attach or run solo; Support MUST attach at muster. Max 1 Leader + 1 Support per bodyguard.
- Attacks use highest T of bodyguard models. Unit has ALL keywords of components (e.g. PSYKER carries for ANTI-PSYKER).
- **Leader/Support keep their own datasheet abilities as long as the model leads a unit — even after the bodyguard unit is destroyed — IF it started the battle in an attached unit.**

### Ingress / reserves
- Ingress move = arriving from strategic reserves (deep strike, teleport, etc.); must be set up **>8" from enemies** (was 9" in 10th). Charge from deep strike still needs a 9 on 2D6 (the 9" gap).

### Key universal abilities (24)
- **Duplicated abilities don't stack (24.02)** — choose one occurrence; for numbered/keyworded weapon abilities choose per attack (Scouts special case: lowest value not shared by all).
- CHASSIS (17.02): large baseless models; measure to nearest point.
- Monster/Vehicle (17.01): move through non-M/V models; shooting at engaged M/V = −1 hit; engaged M/V may shoot the unit it's engaged with.
- Lone Operative (called "Loner Agent 24.24" in some text): visible/targetable by indirect only within 12".
- [HEAVY] (24.16): +1 hit if unit essentially stationary / moved ≤3". [LANCE] (24.21): +1 wound if charged this turn. [SUSTAINED HITS X], [LETHAL HITS], [TWIN-LINKED], [TORRENT], [RAPID FIRE X], [ANTI-X Y+], [BLAST], [PRECISION] — standard.
- Keyword renames: Pistol → Close Combat/Close Quarters; Grenades → Explosives; Tank Shock → Crushing Impact; Deep Strike/Reserves → Ingress move.

### Actions (16)
- Not eligible if: off battlefield, AERODYNE/FORTIFICATION, battle-shocked, Ld 0/–, engaged (unless TITANIC), advanced/fell-back, already did an action. After acting: no shoot (except TITANIC), no charge. Moving (other than pile-in/consolidate) cancels it.

---

## ARMY BUILDING / MISSIONS (preview-sourced — NOT in Core Rules PDF; lower confidence)

- **Detachment Points:** Incursion 1000 pts = 2 DP; Strike Force 2000 pts = 3 DP. Detachments cost 1–3 DP. Old codex detachments mostly 2 DP; all new Faction-Focus detachments 1 DP.
- Enhancement limit: 2 (Incursion) / 4 (Strike Force). Unit limit 2/3, ×2 for Battleline.
- **Detachment tags:** one detachment per tag-family per army (DOOMED, ENGINES, AUXILIARIES, LIONS, REVEREND, ARMOURY, ONSLAUGHT, FLYBLOWN, RETALIATION, ABHUMAN, ARMIGERS, …).
- **Enhancement [Upgrade] tag:** one slot, up to 3 non-character units, pay points per unit.
- **5 Force Dispositions:** Take and Hold / Disruption / Purge the Foe / Priority Assets / Reconnaissance. Compare both players' dispositions → asymmetric primary missions. Tournament: fixed at list submission. Pickup: choose per game.

---

## FACTION NOTES RELEVANT TO DANIEL

### Grey Knights (Faction Focus 2026-05-20) — Daniel's faction
- New 1-DP detachments: **Argent Assault** (Paladins; Dauntless Champions = +1 to wound when punching up; Psychic Celerity +1 charge for a Terminator; Aura of Vengeance gives attacker [HAZARDOUS]); **Fires of Purgation** (Purgation Squads; battle-shock pinning; Boons of Deimos +2 S → S10 psycannon; Focused Immolation Dev+Sustained); **Immaterial Interdiction** (Interceptors; Echojump surge D6+1" then can still charge; Astral Overlap = Stealth; Blades from the Beyond = Lance).
- [PSYCHIC] weapons (universal): ignore BS/WS/hit modifiers; count as "psychic attacks."
- Combine new 1-DP detachment with existing 2-DP codex detachment (e.g. Argent Assault + Hallowed Conclave).

### Opponent box (Armageddon): Space Marines vs Orks. Land Speeder 14" move; Ork Wartrakk Rokkit S10 D3.

---

## OPEN ITEMS / WATCHLIST
- Outrider/bike datasheets — confirm MOBILE keyword presence when datasheet visible.
- Dedicated White Scars detachment (not yet released as of late May 2026).
- Faction Focuses still pending late May: Aeldari, Necrons, Adeptus Mechanicus, Leagues of Votann, Imperial Agents, Genestealer Cults (GSC said "Monday").
- German official rulebook: cross-check keyword names (MOBILE, Lone Operative) when available.

## CHANGELOG OF CORRECTIONS (so Claude doesn't reintroduce old errors)
- Engagement range is 2"h **and 5"v** (vertical component initially missed).
- Hidden requires a **DENSE** feature in the area (not any terrain).
- Combat Disembark set-up distance is **6"** (not 3"); unit is battle-shocked, can't charge.
- Fight order is **two-stage alternating** (Fights First, then Remaining), starting with active player — NOT "all active player's units first."
- Overrun Fight is **confirmed official** (12.06): triggered by becoming engaged during the Fight phase, grants one extra pile-in.
- "Risk roll" (leak translation) = official **"hazard roll"**.
- "Arrival move" (leak) = official **"ingress move"**.
