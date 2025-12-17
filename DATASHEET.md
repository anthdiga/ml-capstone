# Datasheet for the BBO Capstone Project Dataset

## Motivation
This dataset was created to support a black-box optimisation (BBO) challenge in which the objective is to maximise the output of unknown functions under strict query limits. The dataset represents the full query history collected across ten iterations of Bayesian optimisation. It supports analysis of optimisation strategies, surrogate modelling behaviour and exploration–exploitation trade-offs in low-data regimes. The task mirrors real-world optimisation problems where evaluations are expensive, delayed or opaque, such as hyperparameter tuning, engineering design or energy system optimisation.

## Composition
The dataset consists of input–output pairs for eight independent black-box functions.

- **Inputs:** Continuous vectors in the range \([0, 1]\), with dimensionality varying from 2D to 8D depending on the function.
- **Outputs:** A single scalar value per input representing the function evaluation.

By iteration ten, each function contains approximately 17 data points. Data are stored in NumPy `.npy` format (`initial_inputs.npy`, `initial_outputs.npy`), with each row corresponding to one query. There are no missing values, but coverage is sparse, particularly for higher-dimensional functions, and many regions of the search space remain unexplored.

## Collection Process
Queries were generated iteratively over ten weekly rounds using Bayesian Optimisation. For each round:
- A Gaussian Process surrogate model was fitted to the current dataset.
- Candidate points were generated using Sobol sequences.
- Acquisition functions (Upper Confidence Bound or Expected Improvement) guided the selection of the next query.

The strategy evolved from broad exploration in early rounds to more targeted exploitation as structural patterns emerged. The dataset was collected sequentially, with one new query per function per iteration.

## Preprocessing and Intended Uses
Input variables were not scaled, as all values were already constrained to \([0, 1]\). Output values were sometimes standardised internally for GP fitting, but the raw outputs were preserved.

**Intended uses:**
- Studying Bayesian optimisation behaviour in low-data settings.
- Comparing acquisition strategies under uncertainty.
- Educational demonstrations of black-box optimisation.

**Inappropriate uses:**
- Training high-capacity models such as deep neural networks.
- Making claims about global optimality given the limited data.

## Distribution and Maintenance
The dataset is publicly available as part of the project’s GitHub repository and is intended for academic and educational use. The dataset is maintained by the project author and may be updated if additional iterations are completed.
