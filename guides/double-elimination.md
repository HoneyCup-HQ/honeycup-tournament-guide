# Double Elimination — Complete Guide

A player is eliminated only after **two** losses. The bracket has two halves — winners and losers — that feed into a grand final.

Also known as: **double-elim**, **DE**, **двойная олимпийка**.

---

## When to use

- Players deserve a second chance after one bad match (esports, fighting games, board games)
- You have time for ~2× matches of single elimination
- Want to reward consistent performance over a single good day

---

## Match count

For `N` participants (bracket size, power of 2), total matches = `2N - 2` (with reset) or `2N - 3` (no reset).

| Players | Matches (max with reset) | Rounds |
|---------|--------------------------|--------|
| 4       | 7  | 4 |
| 8       | 15 | 6 |
| 16      | 31 | 8 |
| 32      | 63 | 10 |

---

## Structure

Two brackets:

1. **Winners bracket (WB):** plays like single elimination. Loser of a WB match drops to the losers bracket at a specific position.
2. **Losers bracket (LB):** loser of any LB match is eliminated. Winner of LB final plays in grand final.

**Grand Final:** winner of WB vs. winner of LB.

---

## The advancement algorithm

For each WB round `r`, losers drop into LB at specific positions so they meet new opponents (not the player who just knocked them out).

Example for 8-player DE:

```
WB Round 1: 4 matches → losers drop to LB Round 1
WB Round 2: 2 matches → losers drop to LB Round 3
WB Round 3 (WB Final): 1 match → loser drops to LB Final

LB Round 1: 2 matches (only WB-R1 losers)
LB Round 2: 2 matches (LB-R1 winners vs WB-R2 losers)
LB Round 3: 1 match (LB-R2 winners play each other)
LB Round 4: 1 match (LB-R3 winner vs ???)
LB Final:   1 match (vs WB-R3 loser)
```

**Key rule:** drop-pattern avoids immediate rematches. The WB-R2 loser does not drop into the same LB round as the player who just beat them in WB-R1.

---

## Grand Final: the reset problem

The WB winner has **0 losses** entering the Grand Final.
The LB winner has **exactly 1 loss**.

If WB winner beats LB winner → tournament over, WB winner champion.
If LB winner beats WB winner → both now have 1 loss → **bracket reset** — they play one more match.

**Why reset matters:** without it, the LB winner has to beat the WB winner **twice** to be champion. The WB winner only has to win **once**. Not symmetric, not fair.

**Without reset (some esports tournaments):** LB winner needs to beat WB winner once to win. Simpler but unfair to WB winner.

**State the rule before the tournament.** Both versions exist. HoneyCup platform uses reset by default.

---

## Seeding

Seed the WB like single elimination:

- **1 vs N, 2 vs N-1, ...** (standard seeding) — highest seed meets lowest
- **Random** — for casual tournaments
- **Pool-based** — group-stage finishers seeded by pool rank

LB positions are derived from WB seeding — no separate LB seeding needed.

---

## Edge cases

**Walkover in WB R1.** Player receives a win, advances. Opponent does not drop to LB (they never played a real match). Byes in WB produce no LB entry.

**No-show in LB.** Standard walkover — other player advances.

**3-player group winner bracket?** Double Elimination is defined for power-of-2 brackets. For non-power-of-2 player counts, use byes in WB R1 to reach the nearest power of 2.

---

## Logistics for clubs

- **Physical court usage:** at peak (early rounds of both brackets running in parallel) you need N/2 courts. Most clubs run brackets sequentially.
- **Round duration:** same cap rules as round-robin. One slow match blocks both brackets.
- **Spectator clarity:** print a visible bracket. Players and viewers often lose track of where in LB they are.

---

## Common mistakes

**Mistake 1: No bracket reset rule stated in advance.** Organizer decides mid-tournament → accusations of bias. State reset rule at registration.

**Mistake 2: Rematches in LB R2.** If the drop pattern is wrong, WB-R1 loser meets their R1 opponent again in LB-R2. Use a correct drop table or a tested tool.

**Mistake 3: Undersized bracket.** 10 players in an 8-bracket forces weird byes. Round up to 16 or down to 8.

**Mistake 4: Counting DE as "2× single elimination."** It's ~2× matches but only the LB takes the extra time. Plan for WB running fast, LB running behind.

---

## Try DE online

Generate a double-elimination bracket:

- [Tennis DE — 8 players](https://honeycup.ru/en/tournament-bracket/tennis/double-elimination/8)
- [Tennis DE — 16 players](https://honeycup.ru/en/tournament-bracket/tennis/double-elimination/16)
- [Esports DE — 16 players](https://honeycup.ru/en/tournament-bracket/esports/double-elimination/16)
- [Table tennis DE — 16 players](https://honeycup.ru/en/tournament-bracket/table-tennis/double-elimination/16)

Auto-generated bracket with correct drop pattern, grand-final reset rule, live scoring, printable PDF.
