# Datasheet for the BBO Capstone Project Dataset

## Motivation
This dataset was created to support a black-box optimisation (BBO) challenge in which the objective is to maximise the output of unknown functions under strict query limits. The dataset represents the full query history collected across nine iterations of Bayesian optimisation. It supports analysis of optimisation strategies, surrogate modelling behaviour and exploration–exploitation trade-offs in low-data regimes. The task mirrors real-world optimisation problems where evaluations are expensive, delayed or opaque, such as hyperparameter tuning, engineering design or energy system optimisation.

## Composition
The dataset consists of eight function-specific datasets corresponding to the eight black-box optimisation tasks. In all cases, input features are scaled to the range \([0,1]\). Each row represents a single query, corresponding to a point in a \([0,1]^k\) space, where \(k\) is the dimensionality of the function. The final column in each dataset contains the scalar output value, and the remaining columns contain the input features.

All datasets are complete and contain no missing values. As of the current iteration, the datasets have the following shapes:

- **Function 1:** (19, 3)  
- **Function 2:** (19, 3)  
- **Function 3:** (24, 4)  
- **Function 4:** (39, 5)  
- **Function 5:** (29, 5)  
- **Function 6:** (29, 6)  
- **Function 7:** (39, 7)  
- **Function 8:** (49, 9)  

In each case, the last column corresponds to the function output, while all preceding columns correspond to input features. Due to increasing dimensionality, coverage becomes progressively sparser for higher-index functions.


## Collection Process
Queries were generated iteratively over nine weekly rounds using Bayesian Optimisation. For each round:
- A Gaussian Process surrogate model was fitted to the current dataset.
- Candidate points were generated using Sobol sequences.
- Acquisition functions (Upper Confidence Bound or Expected Improvement) guided the selection of the next query.

The strategy evolved from broad exploration in early rounds to more targeted exploitation as structural patterns emerged. The dataset was collected sequentially, with one new query per function per iteration.

## Preprocessing and Intended Uses
Input variables were not scaled, as all values were already constrained to \([0, 1]\). Output values were standardised internally for GP fitting, but the raw outputs were preserved.

**Intended uses:**
- Studying Bayesian optimisation behaviour in low-data settings.
- Comparing acquisition strategies under uncertainty.
- Educational demonstrations of black-box optimisation.

**Inappropriate uses:**
- Training high-capacity models such as deep neural networks.
- Making claims about global optimality given the limited data.

## Distribution and Maintenance
The dataset is publicly available as part of the project’s GitHub repository and is intended for academic and educational use. The dataset is maintained by the project author and may be updated if additional iterations are completed.
