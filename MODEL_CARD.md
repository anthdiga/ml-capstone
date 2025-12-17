# Model Card for the BBO Optimisation Approach

## Overview
- **Model name:** GP-based Bayesian Optimisation  
- **Type:** Sequential black-box optimisation framework  
- **Version:** Iteration 9  
- **Core components:** Gaussian Process surrogate, Matern kernel (ν = 1.5), Sobol candidate sampling, UCB and EI acquisition functions

## Intended Use
This approach is suitable for:
- Optimising unknown, expensive-to-evaluate functions with limited queries.
- Problems where uncertainty quantification is valuable.
- Educational and research settings exploring exploration–exploitation trade-offs.

It is not suitable for:
- Large-scale datasets with thousands of evaluations.
- Real-time optimisation requiring immediate feedback.
- Highly discontinuous or adversarial objective functions.

## Approach Details
Across nine iterations, the optimisation strategy evolved as follows:
- Early rounds prioritised exploration using Sobol sampling and higher exploration parameters to discover basic structure.
- Mid rounds introduced more selective sampling and even using posterior variance (maximum predictive uncertainty) where functions still remained poorly understood.
- Later rounds increasingly focused on exploitation, refining around best-so-far regions while retaining limited exploration to avoid premature convergence.

Different functions required different balances, reflecting varying dimensionality, noise and landscape complexity.

## Performance
Performance was assessed using:
- Best-so-far function value per iteration.
- Relative improvement between successive rounds.
- Stability and consistency of high-performing regions.

Several functions showed clear convergence toward strong local optima, while others remained flat or noisy, highlighting the difficulty of some optimisation landscapes.

## Assumptions and Limitations
Key assumptions include:
- Objective functions are reasonably smooth at the sampling scale.
- Local optima are acceptable proxies for good solutions.
- GP uncertainty estimates remain informative with limited data.

Limitations include sparse coverage in high-dimensional spaces, uncertainty about whether the chosen acquisition function is optimal in every case and reliance on heuristic tuning rather than exhaustive validation.

## Ethical and Transparency Considerations
This approach was designed given the synthetic data, so care should be taken when extending it to real-world applications. Nevertheless, the outcomes should be repeatable for any user who can access the BBO challenge datasets.
