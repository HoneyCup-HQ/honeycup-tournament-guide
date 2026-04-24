# Round Robin — Complete Guide

Every participant plays every other participant once. The winner is the player with the most points after all matches are played.

Also known as: **all-vs-all**, **league format**, **круговая система**.

---

## When to use

- Small fields (4-16 players)
- Leagues that run over weeks (tennis clubs, amateur volleyball, chess clubs)
- Group stage of larger tournaments (4-6 players per group)
- When fair ranking of everyone matters more than a fast knockout

---

## Match count

For `N` participants, total matches = `N * (N-1) / 2`.

| Players | Matches | Minimum rounds* |
|---------|---------|-----------------|
| 4       | 6       | 3 |
| 5       | 10      | 5 (one player rests each round) |
| 6       | 15      | 5 |
| 8       | 28      | 7 |
| 10      | 45      | 9 |
| 12      | 66      | 11 |
| 16      | 120     | 15 |
| 20      | 190     | 19 |
| 32      | 496     | 31 |

\* With N-1 rounds for even N, N rounds for odd N (one bye per round).

---

## The circle method (scheduling)

Fix one player (say player 1). Rotate the rest clockwise each round.

Example for 6 players — position 1 fixed, others rotate:

```
Round 1:   1—6   2—5   3—4
Round 2:   1—5   6—4   2—3
Round 3:   1—4   5—3   6—2
Round 4:   1—3   4—2   5—6
Round 5:   1—2   3—6   4—5
```

After 5 rounds every pair has played once.

**For odd N**, add a "ghost" player. Whoever is paired with the ghost in round k gets a bye that round.

Python-like pseudocode:

```python
def round_robin_pairings(n):
    players = list(range(n))
    if n % 2:
        players.append(None)  # bye
    rounds = []
    for r in range(len(players) - 1):
        pairings = []
        for i in range(len(players) // 2):
            a = players[i]
            b = players[-1 - i]
            if a is not None and b is not None:
                pairings.append((a, b))
        rounds.append(pairings)
        players = [players[0]] + [players[-1]] + players[1:-1]
    return rounds
```

---

## Scoring

Most common scoring schemes:

| Sport / context | Win | Draw | Loss |
|-----------------|-----|------|------|
| Chess | 1 | 0.5 | 0 |
| Football (3-point) | 3 | 1 | 0 |
| Tennis (no draws) | 1 | — | 0 |
| Table tennis / billiards | 1 | — | 0 |

Games where ties are possible (chess, football) need explicit draw points.

---

## Tiebreakers

When players end with equal points, use tiebreakers **in order**:

1. **Direct match** — who won when they met
2. **Buchholz** — sum of opponents' final scores (favours players who beat strong opposition)
3. **Sonneborn-Berger** — sum of defeated opponents' scores + half sum of drawn opponents' scores
4. **Points ratio** — total points won / total played (tennis sets, football goals)
5. **Head-to-head points** — for 3+ way ties, mini-table among tied players only

**Recommended default:** Direct match → Buchholz → Sonneborn-Berger.

---

## Logistics for clubs

- **Court / table count:** `N/2` rounded down per round. 8 players = 4 matches running in parallel per round.
- **Round duration:** set a time cap. Tennis round = 1 hour. Chess round = 2 hours. Otherwise one slow match blocks the schedule.
- **Defaults for no-shows:** a forfeit = win for opponent, scored as `win-0` (tennis) or `win-0` (chess 1-0).
- **Printable schedule:** distribute to players before round 1. Reduces "who am I playing next?" questions by 90%.

---

## Edge cases

**Walkovers mid-tournament.** A player leaves after round 3 of 7. What happens to their already-played matches?
- **Option A (conservative):** Annul all their matches. Restart standings without them.
- **Option B (common in leagues):** Keep results as-is. Mark remaining rounds as walkover (win for opponent).

HoneyCup platform uses Option B by default.

**Odd N with a bye.** Whoever gets the bye in round k earns 1 point (or 0, depending on organizer rule). State the rule before the tournament.

---

## Related formats

- **Groups + Playoff** — round robin within groups, then knockout top N per group
- **Double Round Robin** — play everyone twice (home / away). Matches = `N * (N-1)`
- **Swiss System** — similar goal (rank everyone) but only `ceil(log2(N))` rounds

---

## Try a Round Robin online

Generate a printable bracket for your sport and size:

- [Tennis round robin — 8 players](https://honeycup.ru/en/tournament-bracket/tennis/round-robin/8)
- [Tennis round robin — 16 players](https://honeycup.ru/en/tournament-bracket/tennis/round-robin/16)
- [Chess round robin — 8 players](https://honeycup.ru/en/tournament-bracket/chess/round-robin/8)
- [Table tennis round robin — 8 players](https://honeycup.ru/en/tournament-bracket/table-tennis/round-robin/8)
- [Billiards round robin — 8 players](https://honeycup.ru/en/tournament-bracket/billiards/round-robin/8)

Auto-generated schedule, live scoring, printable PDF. Free, no signup.
