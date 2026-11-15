# tiny-chess-01

A 4 KB chess engine: 0x88 board, negamax + alpha-beta + transposition table +
killer/history ordering + null-move pruning + late-move reductions + PVS
(principal variation search) + quiescence with delta pruning, 10,000 nodes
a move. v2.3 adds a tapered PeSTO-style evaluation over the v2.2 search:
the middlegame piece-square tables are kept, and an endgame table is
derived from them (each square's value shifts toward the centre as
material comes off), blended by game phase and maintained incrementally
alongside the middlegame sum, plus futility pruning of quiet moves at
low depth. LMR and the 30000 history-table cap are unchanged from v2.2.
`main.py` is the whole engine, packed from `engine.py` (kept with the
build transcripts) with `makefun compress`. No model calls; it talks
only to the env.
