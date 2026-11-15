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

v2.4 adds an opening book on top of v2.3. The book was trained offline
against the kit's own house opponents: a 250k/500k-node teacher played
5 rounds per opening against nodes-100k, over all 40 openings in both
colours (80 lines). Only lines where the teacher kept a real edge to the
final position (endScore >= 40, best +304) were kept, truncated to the
earliest round reaching the edge, and the top 5 fit the 4 KB cap:
Scandinavian white (+304), Ruy Lopez Berlin white (+246), Sicilian
Alapin white (+107) and black (+98), Italian white (+94). The book is
keyed by sum(ord(opening id)) and looked up before search; if the moves
played so far match the stored line's prefix the next book move is
played, otherwise the engine falls back to its normal search. `main.py`
is the whole engine, packed from `engine.py` (kept with the build
transcripts) with `makefun compress`. No model calls; it talks only to
the env.
