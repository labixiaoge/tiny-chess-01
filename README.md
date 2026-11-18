[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/labixiaoge/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/labixiaoge/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01

A chess engine in 3,799 bytes of Python 3.13 (stdlib only).

## Design

- 0x88 board, negamax + alpha-beta, quiescence over captures,
  promotions and check evasions (with delta pruning).
- Transposition table (2^17 slots, one packed int per entry),
  MVV-LVA + killer + history move ordering, late-move reductions,
  null-move pruning, futility pruning, check extensions,
  iterative deepening with a FIXED node budget of 180,000
  nodes/move (deterministic: no clock, no unseeded randomness).
- Incremental piece-square-table eval (Michniewski tables),
  material + PST, bishop-pair bonus (+30), passed-pawn bonus
  (endgames), king pawn shield, endgame king centralisation,
  repetition detection.
- Speaks the make.fun env protocol (`MAKEFUN_ENV_URL`):
  `POST /game`, `/move`, `/resign`; UCI moves.

## Files

- `main.py` — the engine, lzma-compressed, latin-1 source
  encoding (readable form: `dev7/src5.py` in the source repo).
- `LICENSE` — MIT.

## Verification (local, Python 3.12, 1 CPU)

- perft: startpos 20/400/8902/197281; Kiwipete, pos3–6 all OK.
- Deterministic: same position twice gives the same move.
- ~50k nodes/s; worst move ~5.4 s at the 180k budget
  (limit 10 s/move).
- Practice trials (packed engine, local), 6 games each:
  trial-0 (v5): 5W 0D 1L, Elo 1,654 (v2/v3/v4: 4W, Elo 1,451).
