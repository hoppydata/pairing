# Design-Notizen — Force Disposition in der nächsten Pairing-Tool-Generation

> **Status:** Reine Notizen/Optionen. **Kein** Tool-Code wird in diesem Schritt geändert. Dieses Dokument hält die Implikationen fest, damit die spätere Tool-Arbeit auf einer klaren Grundlage steht.
> Faktengrundlage: [`force-dispositions.md`](force-dispositions.md), [`mission-matrix.md`](mission-matrix.md), [`secondary-missions.md`](secondary-missions.md).

---

## Kernveränderung: Pairing wird zweidimensional

Heute modelliert das Tool **eine** Dimension:

- **Fraktion × Fraktion** → 0–20-Score. Quelle `TEAM_DATA.matrix` (`index.html` ~Z.1318), Fallback `META` (~Z.1354), Ranking-Logik in `getScore`/`scoreNum` (~Z.1545–1570) und den `rank*`-Funktionen (~Z.1734–1804). Strategie-Ableitung in `computeStrategy` (~Z.2057–2180).

In der 11. Edition kommt eine **zweite** Dimension dazu:

- **Disposition × Disposition** → Mission (asymmetrisch) → ein **Matchup-Bias**, der das Fraktions-Matchup verschiebt.
- Die Disposition ist im **Turnier bei Listenabgabe fix** (siehe [`force-dispositions.md`](force-dispositions.md)). Damit ist sie ein **planbarer, vom Gegner unabhängiger Listen-Parameter** — wie die Fraktion selbst. Jeder unserer Spieler **und** jeder erwartete Gegner hat genau eine Disposition.

Das echte Matchup ist künftig also eine Funktion von **(unsere Fraktion, unsere Disposition) vs. (Gegner-Fraktion, Gegner-Disposition)**.

---

## Was die Transkript-Analyse fürs Tool bedeutet

Aus [`mission-matrix.md`](mission-matrix.md) lassen sich konkrete, modellierbare Effekte ableiten:

1. **Disposition-Bias ist real und gerichtet.** Beispiele:
   - **Purge the Foe** ist generisch stark (gegen T&H, Disruption, Priority Assets im Vorteil), nur Recon/Triangulation kontert es.
   - **Priority Assets** ist generisch schwach (nur gegen T&H gut).
   - **Take and Hold** leidet gegen alles Kill-fähige (alle Gegner haben Kill-Boni gegen T&H), glänzt aber mit Durability-Skews.
   - **Reconnaissance** hat den höchsten Score-Floor → „sicherer" Punkt, gut für eine Blunter-/Anker-Rolle im Team.
2. **Safe-Score-Differenz ≈ Mission-Bias.** Sam Popes Safe/Min-Schätzungen je Zelle liefern eine erste **numerische** Grundlage für ein Bias-Gewicht (z.B. Safe-Score-Delta der beiden Paarungs-Missionen als Pseudo-VP-Vorteil).
3. **Floor-Wert ist team-strategisch.** Der Min-Score (Floor) misst, wie viel man bei schlechtem Matchup noch holt — relevant für die „Deliver-don't-win"/„Pin"-Strategien in [`../pairing-strategy.md`](../pairing-strategy.md).

---

## Offene Designfragen (für die spätere Tool-Arbeit)

Bewusst als Optionen, noch nicht entschieden:

- **Datenmodell:** Bekommt jeder Spieler/jede Liste in `TEAM_DATA` ein `disposition`-Feld? Und jeder erwartete Gegner ein angenommenes/bekanntes?
- **Bias-Quelle:** Eine **Disposition × Disposition → Bias**-Lookup-Tabelle (analog `META`, ~25 Zellen) aus den Safe/Min-Schätzungen — oder konservativer nur eine qualitative Vorteil/Nachteil-Markierung?
- **Score-Komposition:** Wie verrechnet man den Mission-Bias mit dem bestehenden 0–20-Fraktions-Score? Additiver Offset, getrennte Anzeige, oder gewichtete Summe?
- **Draft-Integration:** Wie greift das in den bestehenden Defender/Attacker-Draft (`screen-s1*`/`screen-s2*`) und `computeStrategy` (~Z.2057–2180)? Beeinflusst die Disposition, **wen** man als Defender/Attacker schickt?
- **UI:** Disposition pro Spieler sichtbar machen; ggf. den Mission-Namen + Bias im Matchup-Callout anzeigen.
- **Sekundäre:** Aus [`secondary-missions.md`](secondary-missions.md) — sollen Rollen-Tags (Kill / Action / Hold) modelliert werden, da Sekundäre Killing/Midboard belohnen?

---

## Anknüpfungspunkte im bestehenden Code/Datenbestand

- `data/team-data.json` — `factions`, `playerFactions`, `matrix` (Quelle der Wahrheit; ein Dispositions-Feld käme hierher).
- `index.html` — `TEAM_DATA` (~Z.1318), `META` (~Z.1354), `FACTION_TABLE_PREFS` (~Z.1406), State `S` (~Z.1441), `getScore` (~Z.1545), `rank*` (~Z.1734–1804), `computeStrategy` (~Z.2057–2180).
- [`../pairing-strategy.md`](../pairing-strategy.md) — Rollenmodell (Hammer/Anvil/Tech/All-Rounder/Wildcard), Defender/Attacker-Mindset; eine Disposition lässt sich als zusätzliches Rollen-Attribut lesen.
- [`../pairing-rules.md`](../pairing-rules.md) — der Pairing-Sequenz-Ablauf bleibt; nur die Bewertung je Paarung wird reicher.
