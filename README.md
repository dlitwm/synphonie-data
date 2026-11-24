# synphonie-data

This repository contains the data accompanying the SYNPHONIE paper. The
pipeline stores its intermediate and final states as SQLite databases. The
directory structure mirrors the way data is passed through the individual
pipeline steps.

## Directory structure

### `input/`

`input/` contains the data used to start the pipeline:

- `source/` contains the source databases. The
  `source/durchfahrer_separiert/` subdirectory contains the corresponding
  variant with through-riders separated.
- `graph_sep.sqlite` and `demand_sep.sqlite` are the graph and demand data
  used by the pipeline.
- The JSON files contain the run configuration, including mode parameters,
  objective parameters, epsilon constraints, scalar values, and transfers.
- `manifest.json` records the input files expected by the pipeline.

### `solutions/`

`solutions/` contains the solutions produced by the pipeline. Solution
databases are kept in nested directories so that intermediate results from
different processing branches and parameterizations remain distinguishable:

- `solution_*.sqlite` are solution states for the rough runs.
- `patch_solution_*/` contains the solutions generated for the corresponding
  patch step. The nested `solution_<patch>_<step>.sqlite` files are the
  successive states passed through that step.
- `eq-no-inf/` contains the results of the equilibrium runs on the rough solutions with equilibrium constraints. 
- Its `infs/` subdirectory contains the related runs
  for the lineplanning step , including the `eq-with-inf/` result branch with the final solutions of the pipeline.
- CSV files contain aggregated or Pareto-frontier data derived from the
  solution databases. `frontier_data.json` and `pareto_frontier.png` provide
  the corresponding frontier data and visualization.
- Warm-start files (`warmstart_*.mst`) contain solver warm-start data.

