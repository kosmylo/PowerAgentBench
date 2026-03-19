# PowerAgentBench

A benchmark suite for evaluating AI agents on power system operational tasks.

## Repository Structure

```
PowerAgentBench/
├── cases/                          # Network case data in multiple formats
│   └── case39/
│       ├── pypsa/case39.nc         # PyPSA netCDF format
│       ├── matpower/case39.m       # MATPOWER .m format
│       └── pandapower/case39.json  # PandaPower JSON format
├── benchmarks/                     # Benchmark definitions and configs
│   └── steady/
│       └── level_1/
│           ├── README.md           # Full benchmark specification
│           ├── actionspace.json    # Action contract and operating limits
│           ├── actioncost.json     # Per-step action costs
│           ├── baseline_summary.json
│           └── solution_template.json
├── scripts/                        # Runnable entry points
│   ├── build_case.py               # Rebuild the stressed scenario
│   ├── convert_case.py             # Export to MATPOWER and PandaPower
│   └── evaluate_solution.py        # Score a solution
└── poweragentbench/                # Shared library code
    └── benchmark_utils.py          # Case construction and scoring
```

## Quick Start

```bash
pip install -e .

# Rebuild the benchmark case from source
python scripts/build_case.py

# Export to MATPOWER and PandaPower formats
python scripts/convert_case.py

# Evaluate a solution
python scripts/evaluate_solution.py --solution benchmarks/steady/level_1/solution_template.json
```

## Case Formats

The IEEE 39-bus stressed scenario is provided in three formats so that agents and solvers are not tied to a single tool:

- **PyPSA** (`cases/case39/pypsa/case39.nc`): the primary format used by the evaluator.
- **PandaPower** (`cases/case39/pandapower/case39.json`): for use with PandaPower-based tools.
- **MATPOWER** (`cases/case39/matpower/case39.m`): for use with MATPOWER or MATPOWER-compatible solvers.

## Benchmarks

See `benchmarks/steady/level_1/README.md` for the full specification of the first benchmark task.
