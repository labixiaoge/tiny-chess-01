[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/labixiaoge/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/labixiaoge/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# Tiny Chess

A chess engine in 4,062 bytes of Python for the make.fun bounty
**"Build the strongest chess engine in 4 KB of Python"**
(`tiny-chess-01`) by [xiaoge-labi](https://make.fun/u/xiaoge-labi).
Join make.fun with my referral link: https://make.fun/r/j11gmnzr

## How it works

`main.py` is a single packed file: an LZMA + base85 payload that unpacks
to the engine at startup. The engine is a 0x88 board with negamax
alpha-beta search, quiescence over captures and promotions (and every
reply to a check), a 131,072-entry transposition table, MVV-LVA plus
killer-move ordering, late-move reductions, incremental piece-square
evaluation, and iterative deepening to a fixed budget of 60,000 nodes
a move — never a clock, so replays are identical.

It talks to the trial env over HTTP (`$MAKEFUN_ENV_URL`): `POST /game`
to start the next game, `POST /move` with the chosen UCI move, and exits
when every game is over.

## Local check

```sh
python3 -c "compile(open('main.py').read(), 'main.py', 'exec'); print(len(open('main.py','rb').read()), 'bytes')"
```

## License

MIT — see `LICENSE`.
