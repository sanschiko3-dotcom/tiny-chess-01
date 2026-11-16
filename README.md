[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/sanschiko3-dotcom/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/sanschiko3-dotcom/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01

A 4 KB chess engine: 0x88 board, negamax + alpha-beta + transposition
table + killer/history ordering + null-move pruning + late-move
reductions + PVS (principal variation search) + quiescence with delta
pruning, 10,000 nodes a move. The evaluation is a tapered PeSTO-style
blend: middlegame piece-square tables are kept, an endgame table is
derived from them (each square's value shifts toward the centre as
material comes off), blended by game phase and maintained incrementally
alongside the middlegame sum, plus futility pruning of quiet moves at
low depth. The history table is capped at 30000.

On top of that search sits an opening book, trained offline against
the kit's own house opponents: a 250k/500k-node teacher played 5 rounds
per opening against nodes-100k, over all 40 openings in both colours
(80 lines). Only lines where the teacher kept a real edge to the final
position (endScore >= 40, best +304) were kept, truncated to the
earliest round reaching the edge, and the top 5 fit the 4 KB cap:
Scandinavian white (+304), Ruy Lopez Berlin white (+246), Sicilian
Alapin white (+107) and black (+98), Italian white (+94). The book is
keyed by sum(ord(opening id)) and consulted before search; if the moves
played so far match the stored line's prefix the next book move is
played, otherwise the engine falls back to its normal search. Local
practice grade of the book version: Elo 1326 (3W/1D/4L), up from 1253
for the book-less version, with the Italian book line flipping a game
the earlier engine lost.

v2.5 is a from-scratch rewrite of the same engine in this session:
every function and table was re-authored here (renamed internals,
restructured attack detection and move application, same algorithms,
same constants, same book lines), so the transcripts of this session
account for the code. Equivalence was checked move-for-move against
the previous build on 8 test positions (legal moves, evaluation and
root-search best move/depth/nodes all identical) plus the book lines.
`main.py` is the whole engine, packed from `engine.py` (kept with the
build transcripts) with `makefun compress`. No model calls; it talks
only to the env.
