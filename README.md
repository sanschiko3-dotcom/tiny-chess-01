[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/sanschiko3-dotcom/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/sanschiko3-dotcom/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01

A 4 KB chess engine: 0x88 board, negamax + alpha-beta + transposition
table + killer/history ordering + null-move pruning + late-move
reductions + PVS + quiescence with delta pruning and mate-distance
pruning, 16,000 nodes a move with a 6-second time cap so the trial
never runs out of wall time. Tapered PeSTO-style evaluation
(middlegame/endgame piece-square tables blended by phase, maintained
incrementally), plus futility pruning at low depth.

Opening book: trained offline against the kit's house opponents (a
250k/500k-node teacher vs nodes-100k, all 40 openings, both colours);
only lines where the teacher kept an edge were kept, and the top 5 fit
the 4 KB cap: Scandinavian white (+304), Ruy Lopez Berlin white
(+246), Sicilian Alapin white (+107) and black (+98), Italian white
(+94). Keyed by sum(ord(opening id)); if the moves played match the
stored line's prefix the next book move is played, else normal search.
Local practice grade of the book version: Elo 1326 (3W/1D/4L).

v2.5 rewrote the engine from scratch in its build session; v2.6 evolves
it here: merged FEN loader with eval init, unified leaper/slider move
generation, mate-distance pruning, 16,000-node budget with a 6s/move
cap, leaner move sort. Same board, eval, LMR and book; check extension
tried and dropped (it ate nodes without depth gain). Verified
move-for-move against v2.5 on 10 test positions (legal moves,
board/eval/hash after make/unmake, root best move) plus castling,
en-passant, promotion, stalemate and checkmate sanity positions.
Local practice grade trial 0: Elo 1396 (3W/2D/3L).

`main.py` is the whole engine, packed from `engine.py` with `makefun
compress`. No model calls; it talks only to the env.
