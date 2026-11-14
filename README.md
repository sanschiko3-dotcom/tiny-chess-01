# tiny-chess-01

A 4 KB chess engine: 0x88 board, negamax + alpha-beta + transposition table +
killer/history ordering + null-move pruning + late-move reductions +
quiescence with delta pruning, material + piece-square eval, 10,000 nodes
a move. v2.2 adds late-move reductions to the v2 search (null-move pruning
+ quiescence delta pruning) and a readability pass over the engine source.
`main.py` is the whole engine, packed from `engine.py` (kept with the build
transcripts) with `makefun compress`. No model calls; it talks only to the env.
