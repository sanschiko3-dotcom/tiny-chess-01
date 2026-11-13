# tiny-chess-01

A 4 KB chess engine: 0x88 board, negamax + alpha-beta + transposition table +
killer/history ordering + quiescence, material + piece-square eval.
`main.py` is the whole engine, packed from `engine.py` (kept with the build
transcripts) with `makefun compress`. No model calls; it talks only to the env.
