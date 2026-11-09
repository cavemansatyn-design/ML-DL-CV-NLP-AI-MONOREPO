# 04.2 — Robo-Football Game-Playing AI

## Notebook
`robo-football.ipynb`

A self-contained turn-based football game and AI-agent comparison environment.

## Game environment
- Board: **6 rows × 5 columns**.
- Each team has four outfield players and one goalkeeper (10 players total).
- Teams alternate turns.
- Goalkeepers move sideways on their own goal line.
- Dribbles move in one of eight directions and may be tackled by an adjacent opponent.
- Passes travel horizontally, vertically or diagonally and can be blocked by an opponent on the line.
- Shots are allowed in the attacking two rows; the opposing goalkeeper can save when within one column.

## Implemented agents and search
- Random/baseline action selection.
- Heuristic evaluation based on field position and possession.
- Structural heuristic considering support/defensive pressure.
- Minimax game-tree search.
- Alpha-beta pruning.
- Monte Carlo random rollouts.
- Game-playing and tournament helpers with alternating sides.
- Search-cost comparison and depth profiling.

## Automated rule checks
The notebook's assertions check:
- exactly 10 occupied player positions in the initial state;
- at least one legal action;
- action types are among dribble, pass, shoot and defend;
- applying legal actions preserves the player count and board bounds;
- turns alternate;
- attacking-third definitions;
- diagonal line-cell behaviour;
- a constructed tackle scenario.

## How to interpret the algorithms
Alpha-beta pruning should return the same minimax value as plain minimax at the same depth/evaluation while potentially expanding fewer nodes. Its benefit depends on move ordering. Random-rollout MCTS is a basic baseline; it is not a full tree-based UCT implementation with selection, expansion and backpropagation.

## Experimental caution
The notebook's quick demonstrations use fewer games for runtime. Its own guidance recommends at least 20 games per pairing before interpreting tournament win rates. The saved notebook does not preserve a complete benchmark table, so this README does not claim a win rate, search speedup or node-count result.
