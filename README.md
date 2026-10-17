# Dynamic Home Health Care Routing and Scheduling with Synchronized Visits

This repository contains the computational notebooks and experimental results associated with the study **“Dynamic Home Health Care Routing and Scheduling with Synchronized Visits: Complete-Information versus Rolling-Horizon Planning.”**

The study considers daily caregiver routing and scheduling when patient requests may be known in advance or revealed dynamically during operations. Some visits require two qualified caregivers to begin service simultaneously. The objective balances response delay, caregiver travel, and priority-weighted uncovered demand.

## Solution approaches

The repository implements and evaluates three approaches:

- **Mixed-integer linear programming (MILP):** implemented with Gurobi and used as the benchmark when a feasible solution is available within the time limit.
- **Genetic algorithm (GA):** a tailored metaheuristic for complete-information planning, including synchronization-aware chromosome representation and schedule decoding.
- **Rolling horizon (RH):** a reactive framework that periodically updates caregiver locations and availability, preserves completed and committed visits, and reoptimizes the residual problem as requests are revealed.

## Repository structure

```text
home-healthcare-scheduling/
├── README.md
├── LICENSE
├── requirements.txt
├── notebooks/
│   ├── Gurobi.ipynb
│   ├── genetic_algorithm.ipynb
│   └── rolling_horizon.ipynb
├── results/
│   ├── Instances_and_Results.xlsx
│   └── Sensitivity_Analysis_Tracker.xlsx
├── figures/
│   ├── Objective_Components_Figure.ipynb
│   └── Sensitivity_Analysis_Figures.ipynb
```

### Notebooks

- `genetic_algorithm.ipynb`: Generates problem instances, constructs and decodes GA chromosomes, evaluates schedule feasibility, runs the GA, and reports objective components and uncovered requests.
- `rolling_horizon.ipynb`: Implements the MILP-based rolling-horizon procedure, including caregiver-state updates, committed visits, residual optimization, and schedule reporting.

### Result workbooks

- `Instances_and_Results.xlsx`: Consolidated Gurobi, GA, and rolling-horizon results, including instance characteristics, repeated GA runs, decomposed objective values, and computation times.
- `Sensitivity_Analysis_Tracker.xlsx`: Results used to analyze the synchronization ratio and rolling-horizon update interval.

## Experimental design

The computational study includes instances with 20, 40, 60, and 80 patients. The proportion of dynamically arriving requests takes values of 10%, 25%, 50%, 75%, and 90%. Five independently generated instances are evaluated for each problem-size and dynamic-demand combination. The baseline synchronization ratio is 10%.

Each patient has one service requirement during the planning horizon. Service durations are 20, 30, 45, or 60 minutes, depending on the service type. A synchronized request requires two distinct qualified caregivers to begin service at the same time.

The objective contains three components:

1. response delay for dynamically arriving requests;
2. caregiver travel time; and
3. a priority-weighted penalty for uncovered requests.

## Requirements

The experiments were conducted using:

- Python 3.10.11
- Gurobi Optimizer 13.0.1
- Jupyter

Install the Python dependencies with:

```bash
pip install -r requirements.txt
```

Gurobi requires a separate license. Academic licenses are available through the [Gurobi Academic Program](https://www.gurobi.com/academia/academic-program-and-licenses/).

## Running the notebooks

1. Clone or download the repository.
2. Install the dependencies from `requirements.txt`.
3. Confirm that the Gurobi license is active.
4. Open Jupyter Lab:

```bash
jupyter lab
```

5. Open the desired notebook from the `notebooks` directory and run its cells in order.

The random seeds used to generate instances and execute stochastic runs are specified in the notebooks and result workbooks. Because the GA is stochastic, repeated runs can produce slightly different solutions unless the same seeds and software environment are used.

## Computational environment

The reported experiments were conducted on a computer with a Snapdragon X Plus 8-core processor running at 3.30 GHz, using up to eight threads. Gurobi runs were subject to a six-hour time limit. Reported computation times are wall-clock times.

## Data availability

All instances are synthetically generated. The notebooks provide the instance-generation procedure, and the result workbooks contain the outputs used in the computational analysis.

## Citation

The associated manuscript is currently under review. Citation information will be added after publication.

If you use this repository before publication, please cite the repository URL and access date.

## License

This project is distributed under the MIT License. See `LICENSE` for details.

## Contact

Questions, reproducibility issues, and suggestions may be submitted through the repository's GitHub Issues page.
