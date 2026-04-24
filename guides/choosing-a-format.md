# Choosing a Tournament Format

The format decides everything else: match count, time budget, fairness, and how much work the organizer does after each round. Pick format before picking date.

---

## The five questions

Answer these before looking at formats.

1. **How many players?** 4-16 is a different problem than 64+.
2. **How much time?** One evening vs. a week vs. a 12-week league.
3. **Should everyone play multiple games?** Yes → avoid single elimination.
4. **Do you have reliable pairings software?** No → avoid Swiss with rating-based pairings.
5. **Is fair ranking more important than a clear winner?** Yes → Round Robin. No → knockout.

---

## Decision tree

```
Need a clear winner fast?
├─ YES → Single Elimination (N-1 matches, log2(N) rounds)
│   └─ Worry about bad luck in round 1? → Double Elimination instead
│
└─ NO, fair ranking matters
    ├─ Small field (≤16)?
    │   └─ YES → Round Robin (N*(N-1)/2 matches)
    │
    └─ Large field (16+)?
        ├─ Need elimination feel? → Groups + Playoff
        └─ Need full ranking? → Swiss System (ceil(log2(N)) rounds)
```

---

## Match counts by format (16 players)

| Format | Matches | Rounds | Duration (1 court, 30 min/match) |
|--------|---------|--------|----------------------------------|
| Single Elimination | 15 | 4 | ~7.5 hours |
| Double Elimination | 30 | 8 | ~15 hours |
| Round Robin | 120 | 15 | ~60 hours (needs multiple courts or weeks) |
| Groups (4×4) + Playoff (8) | 31 | ~5 | ~15 hours |
| Swiss (4 rounds) | 32 | 4 | ~16 hours |

For 16 players, Round Robin is only realistic as a league over weeks. Groups + Playoff or Double Elimination are one-weekend friendly.

---

## When each format wins

### Single Elimination wins when
- Prize money or spot allocation (winner takes all)
- Tight time window (one afternoon)
- Players know the risk (bad match-up in round 1 = you're out)
- Common in tennis Grand Slams, cup competitions

### Double Elimination wins when
- Players deserve a second chance (esports, fighting games)
- You can afford ~2× match count
- Bracket reset in Grand Final is acceptable

### Round Robin wins when
- Ranking every player matters, not just crowning a winner
- Field is small (≤16) or league runs over weeks
- Used for: small-club leagues, group stage of larger tournaments, BO16 qualification

### Groups + Playoff wins when
- Large field, limited time
- You want both ranking (within group) and a knockout finale
- Used for: World Cup, most major team-sport tournaments

### Swiss System wins when
- Large field (64+), no time to play everyone
- Strong-vs-strong pairings produce meaningful ranking
- Used for: chess, MTG, Pokémon TCG, debate competitions

---

## Common mistakes

**Mistake 1: Round Robin with 16+ players in one day.** You cannot play 120 matches in a day on one court. Use Groups + Playoff, or spread over weeks.

**Mistake 2: Single Elimination with no seeds.** Two top players meeting in round 1 wastes the bracket. Use standard seeding (1 vs N, 2 vs N-1, etc).

**Mistake 3: Swiss without tiebreakers.** Ending with 5 players on 4/5 and no tiebreaker = angry players. Always specify Buchholz + Sonneborn-Berger.

**Mistake 4: Double Elimination without a grand-final reset rule.** If losers-bracket winner beats winners-bracket winner once, they have the same number of losses only after reset. State the rule before the tournament, not after.

**Mistake 5: Round Robin scoring without a draw policy.** Tennis rarely has draws, chess usually does. Pick `win=3, draw=1, loss=0` or `win=1, draw=0.5, loss=0` up front.

---

## Try it online

Generate a ready-to-use bracket for any format:

- [Single Elimination (16 players)](https://honeycup.ru/en/tournament-bracket/tennis/single-elimination/16)
- [Double Elimination (16)](https://honeycup.ru/en/tournament-bracket/tennis/double-elimination/16)
- [Round Robin (8)](https://honeycup.ru/en/tournament-bracket/tennis/round-robin/8)
- [Groups + Playoff (16)](https://honeycup.ru/en/tournament-bracket/tennis/groups-playoff/16)
- [Swiss (32 chess players)](https://honeycup.ru/en/tournament-bracket/chess/swiss/32)

All free, no signup, printable PDF export.
