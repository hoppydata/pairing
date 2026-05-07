# Global Meta Matrix

**Updated:** 2026-05-07
**Source:** Faction × faction VP-delta screenshot (provided by user, current dataslate)
**Conversion formula:**
```
bracket = abs(delta) <= 5 ? 0 : min(ceil((abs(delta) - 5) / 5), 10)
score   = delta >= 0 ? 10 + bracket : 10 - bracket
```

10 = even, >10 favours us, <10 favours opponent. Self-cells (mirror match) set to 10.

## Player Factions

| Player    | Faction            |
|-----------|--------------------|
| Player 1  | Dark Angels        |
| Player 2  | Daemons            |
| Player 3  | Imperial Knights   |
| Player 4  | Astra Militarum    |
| Player 5  | Custodes           |

`Emperor's Children` is also tracked as a known meta presence even though it's not on our roster.

## Matrix (rows = our faction, columns = opponent faction)

| Our \ Opp | Ad Mech | Aeldari | Astra Militarum | Black Templars | Blood Angels | Chaos Knights | CSM | Custodes | Daemons | Dark Angels | Death Guard | Deathwatch | Drukhari | Emperor's Children | Grey Knights | GSC | Imperial Agents | Imperial Knights | Necrons | Orks | Sisters | SM (UM) | Space Wolves | Tau | T'sons | Tyranids | Votann | World Eaters |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Custodes** | 10 | 11 | 8 | 14 | 9 | 10 | 8 | 10 | 9 | 9 | 10 | 10 | 10 | 7 | 9 | 9 | 10 | 9 | 10 | 13 | 12 | 12 | 12 | 10 | 8 | 10 | 11 | 10 |
| **Astra Militarum** | 12 | 11 | 10 | 10 | 10 | 9 | 10 | 12 | 8 | 11 | 10 | 11 | 10 | 10 | 9 | 10 | 13 | 9 | 8 | 10 | 9 | 10 | 11 | 10 | 7 | 9 | 10 | 10 |
| **Daemons** | 12 | 13 | 12 | 9 | 10 | 10 | 10 | 11 | 10 | 10 | 10 | 11 | 12 | 9 | 11 | 9 | 5 | 11 | 11 | 11 | 10 | 9 | 11 | 10 | 10 | 12 | 10 | 10 |
| **Dark Angels** | 13 | 13 | 9 | 10 | 8 | 10 | 10 | 11 | 10 | 10 | 11 | 8 | 10 | 14 | 8 | 10 | 5 | 10 | 9 | 11 | 8 | 10 | 10 | 9 | 5 | 9 | 10 | 10 |
| **Imperial Knights** | 13 | 10 | 11 | 10 | 9 | 12 | 10 | 11 | 9 | 10 | 9 | 6 | 10 | 7 | 10 | 7 | 13 | 10 | 11 | 10 | 10 | 10 | 10 | 9 | 8 | 11 | 9 | 10 |
| **Emperor's Children** | 10 | 12 | 10 | 9 | 12 | 7 | 9 | 13 | 11 | 6 | 10 | 12 | 12 | 10 | 11 | 13 | 16 | 13 | 10 | 12 | 16 | 12 | 11 | 13 | 7 | 13 | 13 | 10 |
