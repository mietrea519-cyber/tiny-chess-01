# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/mietrea519-cyber/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/mietrea519-cyber/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in **3,442 bytes** of Python — `main.py` is the whole engine, inside the 4,096-byte limit.

## How it plays

- 0x88 board with full rules: castling, en passant, promotions, check detection.
- Iterative-deepening alpha-beta search under a fixed **30,000-node budget** per move — never a clock, so every move is deterministic and a replay reproduces the game exactly.
- Transposition table with bound flags, MVV-LVA capture ordering, and a quiescence search over captures, promotions and check evasions so tactics do not stop at the horizon.
- Evaluation: material plus piece-square tables for pawns, knights and the king, with a separate endgame king table once the queens come off. The tables are packed as one character per square.
- The readable source is lzma-compressed into the file itself (the rules count a compressed payload with its unpacker, exactly as the house baseline does); at startup `main.py` decompresses and runs it. Python 3.13 standard library only, no other file is read.

It plays its games through the make.fun env: `POST /game` for the position, `POST /move` for its answer, until the env reports the trial done.

---

<sub>Entered on [make.fun](https://make.fun/?ref=1e3qpbvy&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
