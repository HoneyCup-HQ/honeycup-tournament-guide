# HoneyCup Tournament Guide

Free, open guide to amateur tournament formats — JSON schemas, printable brackets, and format explainers. Curated by the team behind [HoneyCup](https://honeycup.ru), a free online tournament bracket generator for amateur clubs and organizers.

**License:** [CC-BY-4.0](LICENSE) — free to use and adapt, credit required.

---

## What's in this repo

| Folder | Content |
|--------|---------|
| [`formats/`](formats/) | JSON schemas for 6 tournament formats |
| [`guides/`](guides/) | Markdown explainers per format (rules, when to use, edge cases) |
| [`printable/`](printable/) | Ready-to-print PDF bracket templates (8/16/32 players) |
| [`examples/`](examples/) | Sample tournament data (fixtures for each format) |

---

## Quick start: which format do I need?

| Format | Use when |
|--------|----------|
| **Single Elimination** | Short event (one evening), 8-128 players, fast resolution |
| **Double Elimination** | You want a second chance for everyone. 8-32 players, ~2× matches of single |
| **Round Robin** | Every player plays every other. Best for 4-16 players, league format, fair ranking |
| **Groups + Playoff** | Large tournaments (16+ players), group stage filters to knockout (e.g. World Cup) |
| **Swiss System** | Chess, trading card games, large fields. Players face others with similar scores |

Not sure? Read [guides/choosing-a-format.md](guides/choosing-a-format.md).

---

## Round Robin quick reference

For `N` players, Round Robin produces `N * (N-1) / 2` matches:

| Players | Matches | Rounds |
|---------|---------|--------|
| 4       | 6       | 3      |
| 6       | 15      | 5      |
| 8       | 28      | 7      |
| 10      | 45      | 9      |
| 12      | 66      | 11     |
| 16      | 120     | 15     |

Match order follows the **circle method** — one player fixed, others rotate. No player sits idle more than one round.

Generate a printable bracket online:
[honeycup.ru/en/tournament-bracket/tennis/round-robin/8](https://honeycup.ru/en/tournament-bracket/tennis/round-robin/8) · [chess](https://honeycup.ru/en/tournament-bracket/chess/round-robin/8) · [table tennis](https://honeycup.ru/en/tournament-bracket/table-tennis/round-robin/8)

---

## Double Elimination structure

Two brackets:

1. **Winners** (upper) — lose once, drop to losers
2. **Losers** (lower) — lose twice, eliminated

**Grand Final:** winner of winners vs. winner of losers. If the losers-side winner beats the winners-side winner, a **bracket reset** is played — because the winners-side winner had 0 losses coming in.

See [guides/double-elimination.md](guides/double-elimination.md) for the full advancement algorithm.

Try it online: [honeycup.ru/en/tournament-bracket/tennis/double-elimination/16](https://honeycup.ru/en/tournament-bracket/tennis/double-elimination/16)

---

## Swiss System rules

- **Round 1:** pair by seed (top half vs bottom half) or randomly
- **Round N+1:** pair players with equal scores, avoid repeat matchups
- **Tiebreakers:** Buchholz, Sonneborn-Berger, cumulative score

Number of rounds typically `ceil(log2(N))` — 32 players = 5 rounds.

See [guides/swiss.md](guides/swiss.md) for pairing rules and tiebreakers.

Try it online: [honeycup.ru/en/tournament-bracket/chess/swiss/16](https://honeycup.ru/en/tournament-bracket/chess/swiss/16)

---

## Why this repo exists

I built HoneyCup after watching three tennis clubs run tournaments on paper and Excel. Good format knowledge is scattered: Wikipedia has rules but no fixtures, Challonge has a tool but no explainer, blog posts repeat the same four paragraphs.

This repo collects what I learned building the platform — JSON schemas that actually encode the rules, printable templates that match what clubs use, and plain-language guides.

If it saves you an afternoon in Excel, it did its job.

---

## Related links

- Main platform: [honeycup.ru](https://honeycup.ru) — free, no signup, 6 sports × 6 formats
- Landing index: [honeycup.ru/en/bracket](https://honeycup.ru/en/bracket)
- EN version: [honeycup.ru/en](https://honeycup.ru/en)
- RU version: [honeycup.ru/ru](https://honeycup.ru/ru)

---

## Contributing

Spotted a rule error? [Open an issue](https://github.com/HoneyCup-HQ/honeycup-tournament-guide/issues).
Have a better diagram or fixture? PR welcome.

**License:** Content under [CC-BY-4.0](LICENSE). Schemas, guides and PDFs are free to use with credit to HoneyCup.
