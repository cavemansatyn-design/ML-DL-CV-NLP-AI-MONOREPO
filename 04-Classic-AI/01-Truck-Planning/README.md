# 04.1 — Truck Loading and Delivery Planning

## Notebook
`truck-planning.ipynb`

A finite offline planning problem: packages arrive in a known sequence, each package has a destination, and trucks have a fixed capacity. The model assigns packages to truck loads and evaluates delivery time together with the number of trucks.

## Model formulation
- State-space representation of package assignment/loading decisions.
- Integer destinations and a fixed truck capacity.
- Explicit unloading-order assumption: front-to-back unloading follows increasing destination order.
- Delivery time combines waiting time until dispatch and destination travel distance (one time unit per destination).
- Objective is a weighted combination of truck count and mean package delivery time; the truck-count weight is exposed as a parameter.

## Algorithms and experiments
- Greedy planning baseline.
- Breadth-first search (BFS).
- A* search with an optimistic lower bound based on minimum additional trucks and unavoidable destination travel.
- Generated small instances with a fixed seed.
- Plan validation checks that a plan exists and that package assignments obey capacity/validity rules.
- Cross-instance algorithm comparison.
- Sensitivity analysis over the truck-count weight.

## Interpretation
A larger truck-count weight favours consolidating packages, even if packages wait longer. A smaller weight favours faster delivery and may justify dispatching more trucks. The A* heuristic helps order exploration but does not make the full search inexpensive.

## Assumptions and limitations
The model assumes all packages are known before planning, one truck capacity, equal travel-time units per destination, and no congestion or variable loading times. A live system would need online dispatch decisions under uncertain future arrivals.

## Numerical results
The saved notebook does not preserve a complete numeric comparison table in its output cells. Run the generated-instance and sensitivity sections to obtain current expanded-state counts, costs and runtime measurements. No benchmark values are asserted here without those outputs.
