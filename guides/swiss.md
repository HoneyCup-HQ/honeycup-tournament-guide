# Swiss System — Complete Guide

Players with equal scores face each other each round. No eliminations. Fixed number of rounds (typically `ceil(log2(N))`), regardless of player count.

Also known as: **Swiss**, **Swiss pairing**, **швейцарская система**.

---

## When to use

- Large fields (32+) where Round Robin is impossible
- You want meaningful ranking, not just a single winner
- Chess, MTG, Pokémon TCG, debate tournaments, some esports
- Time-boxed event (e.g. one weekend = 5-7 rounds for 32-128 players)

---

## Round count

| Players | Rounds | Matches per round | Total matches |
|---------|--------|-------------------|---------------|
| 8       | 3      | 4 | 12 |
| 16      | 4      | 8 | 32 |
| 32      | 5      | 16 | 80 |
| 64      | 6      | 32 | 192 |
| 128     | 7      | 64 | 448 |

Formula: `rounds = ceil(log2(N))`. For odd player counts, one player gets a bye each round.

---

## Pairing rules

### Round 1

Two common methods:

**Top half vs bottom half (standard):**
- Sort players by rating / seed
- Pair 1 vs N/2+1, 2 vs N/2+2, ..., N/2 vs N

**Random:**
- Shuffle and pair sequentially

### Round N+1

**Core rule:** pair players with equal scores, avoid rematches, keep color balance (chess).

Algorithm (Dutch / FIDE Swiss):

1. Sort all players by current score, descending
2. Within each score group, sort by rating
3. Pair top half of group against bottom half
4. If odd count in a group: "float" the bottom player down to the next group
5. Check no rematch. If rematch forced, swap one pair.
6. Check color balance (chess). Rebalance if possible.

**Simpler alternative: Monrad pairing.** Just pair sequentially within score group (1 vs 2, 3 vs 4, ...). Used in casual tournaments.

---

## Tiebreakers

Essential — Swiss almost always produces ties. Apply in order:

1. **Buchholz** — sum of opponents' final scores.
   _Rewards players who faced strong opposition._
2. **Buchholz Cut-1** — Buchholz minus lowest opponent score.
   _Reduces effect of an opponent who dropped out or had a disastrous tournament._
3. **Sonneborn-Berger** — sum of defeated opponents' scores + half sum of drawn opponents' scores.
   _Classic chess tiebreaker._
4. **Cumulative (aggregate)** — sum of scores after each round.
   _Rewards starting strong._
5. **Direct match** — who won when tied players met.
6. **Rating performance** — Elo-based performance rating.

**Recommended default for chess:** Buchholz → Buchholz Cut-1 → Sonneborn-Berger → Direct match.

---

## Byes

If player count is odd, one player each round gets a bye.

**Bye scoring:**
- **Full point bye** (default): bye = 1 point
- **Half point bye:** bye = 0.5 point (less rewarding, fairer for strong players forced into a bye)

**Who gets the bye?**
- Lowest-rated player in the bottom score group who has not already had a bye
- A player cannot receive two byes in one tournament

---

## Color balance (chess only)

Each player should have roughly equal white/black counts. Pairing algorithm tries to:

1. Alternate colors each round
2. Never give a player the same color three times in a row
3. Balance total white/black across the tournament

When forced to break rules, prefer "equalization" over "alternation" — i.e. player with fewer whites gets white.

---

## Accelerated pairing

For very large fields (128+), standard Swiss takes too many rounds for strong players to meet. **Accelerated pairings** boost the top players' scores in round 1-2 virtually, forcing them to meet each other sooner.

Used in large chess Swiss opens. Not needed for ≤64 players.

---

## Common mistakes

**Mistake 1: Too few rounds.** 32 players in 4 rounds means top players may not meet at all. Minimum = `ceil(log2(N))`.

**Mistake 2: No tiebreakers stated.** Tied co-winners at end, no rule → arguments. Always announce tiebreakers at registration.

**Mistake 3: Forced rematch.** Pairing software allowed a rematch when an alternative was available. Use tested software.

**Mistake 4: Ignoring color balance.** Player plays white 4 times out of 5 → unfair. Balance rules matter in chess.

**Mistake 5: Mixing accelerated and standard mid-tournament.** Confuses players and software. Pick one from round 1.

---

## Try Swiss online

Generate a Swiss bracket with correct pairings and tiebreakers:

- [Chess Swiss — 16 players](https://honeycup.ru/en/tournament-bracket/chess/swiss/16)
- [Chess Swiss — 32 players](https://honeycup.ru/en/tournament-bracket/chess/swiss/32)
- [Chess Swiss — 64 players](https://honeycup.ru/en/tournament-bracket/chess/swiss/64)
- [Table tennis Swiss — 16 players](https://honeycup.ru/en/tournament-bracket/table-tennis/swiss/16)

Auto-generated pairings (Dutch system), Buchholz + Sonneborn-Berger tiebreakers, printable PDF.
