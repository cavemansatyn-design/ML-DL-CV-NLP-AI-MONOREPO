# 04 — Classic AI

These projects use explicit state representations, search, planning, game-tree reasoning and symbolic transformations. They are not supervised or deep-learning models.

## 04.1 — Truck planning
[Open project README](01-Truck-Planning/README.md) · `01-Truck-Planning/truck-planning.ipynb`

A finite offline package-loading and delivery-planning model. It compares greedy, BFS and A* search, validates plans against capacity/loading constraints and studies the objective's truck-count weight.

## 04.2 — Robo-Football
[Open project README](02-Robo-Football/README.md) · `02-Robo-Football/robo-football.ipynb`

A 6×5 turn-based grid game with legal-action rules, heuristic evaluation, minimax, alpha-beta pruning, Monte Carlo rollouts, tournaments and search profiling.

## 04.3 — ARC-AGI-1 reasoning
[Open project README](03-ARC-Reasoning/README.md) · `03-ARC-Reasoning/arc-agi-solver (ARC JSON required).ipynb`

An interpretable symbolic baseline using grid matrices, connected components, candidate transformations and demonstration-based rule selection. Official evaluation requires ARC task JSON files, which are not included.

## Metrics policy
The saved classical-AI notebooks contain implementations and test logic, but do not retain a complete, reproducible numeric benchmark table in their stored outputs. Their READMEs therefore describe implemented tests and algorithms without inventing win rates, node counts, planning costs or ARC accuracy. Run the experiment cells to generate current measurements.
