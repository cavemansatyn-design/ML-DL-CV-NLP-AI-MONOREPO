# 04.3 — ARC-AGI-1 Classical Reasoning Solver

## Notebook
`arc-agi-solver (ARC JSON required).ipynb`

A compact, interpretable, non-neural baseline for ARC-AGI-1-style grid tasks. The notebook represents grids as matrices of colour integers, extracts connected objects, proposes a fixed set of candidate transformations and ranks candidates by agreement with demonstration input/output pairs.

## Pipeline
1. Load an ARC task JSON file.
2. Convert input/output grids into array representations.
3. Extract connected components/objects.
4. Generate candidate transformations.
5. Score each candidate against demonstration pairs.
6. Rank candidate rules and apply them to test inputs.
7. Optionally evaluate a folder of task JSON files where labelled test outputs are available.

## Candidate transformations
The candidate library includes identity, 90°/180°/270° rotations, horizontal and vertical reflection, transpose and crop-to-content.

## Local tests
The notebook constructs a small toy task and checks:
- connected-component size for a simple two-cell object;
- a 90-degree rotation result;
- demonstration-based candidate ranking and prediction output.

These are unit-style checks on constructed examples, not a benchmark on the official ARC evaluation set.

## Data dependency
Place official ARC task `.json` files in the folder configured by the notebook before using folder evaluation. No ARC JSON dataset is bundled in this repository. The notebook does not require a CSV.

## Limitations
The solver searches only a small fixed set of global transformations. It is not expected to solve tasks requiring object counting, conditional logic, multi-object relations, drawing, symmetry completion, identity-dependent colour mapping or compositions of multiple operations. Its explicit priors include background colour 0 and four-neighbour connectivity. No official ARC accuracy is claimed without a supplied task set and measured evaluation.
