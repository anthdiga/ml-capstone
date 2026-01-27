# Bayesian Black-Box Optimisation for Efficient Function Search

## Overview

This project explores how a computer can intelligently search for the best solution when the underlying problem is unknown. Instead of guessing randomly, the system learns from previous results and decides where to search next. Over multiple rounds, it balances trying new areas with refining promising ones. This approach is useful in real-world problems such as tuning machine learning models, engineering design, and scientific experiments where testing is expensive or slow. By using data-driven decision-making, the project demonstrates how optimisation can become faster, more efficient, and more reliable.


## Data

The dataset consists of query histories and corresponding function outputs collected during the optimisation process. Eight synthetic black-box functions were provided by the course platform. Each function accepts continuous inputs scaled between 0 and 1 and returns a single scalar output representing performance.

The dimensionality increases across tasks, ranging from 2D to 8D. Each dataset contains all submitted query points and their observed outputs. No missing values are present.

Data was generated through iterative interaction with the BBO capstone evaluation portal and stored locally as NumPy arrays (`.npy` files). Since these datasets are course-generated, they are not publicly hosted and are described directly in this repository.


## Model

The primary model used in this project is a Gaussian Process (GP) surrogate model combined with Bayesian Optimisation. Gaussian Processes were chosen because they perform well with small datasets and provide uncertainty estimates alongside predictions. This uncertainty information is critical for deciding where to sample next.

A Matérn kernel (ν = 1.5) was used to handle irregular and noisy response surfaces. In addition, a WhiteKernel component was added to model observation noise. The surrogate model was updated after each iteration using newly observed data points.

This modelling approach allows the system to approximate unknown functions while actively improving its predictions through sequential learning.


## Hyperparameter Optimisation

Several hyperparameters were tuned during the optimisation process to improve performance and stability:

- **Exploration parameters (β for UCB, ξ for EI)**  
  These controlled the balance between exploration and exploitation. Higher values encouraged broader searching early on, while lower values focused on refining promising regions in later rounds.

- **Kernel parameters**  
  Kernel length scales were optimised automatically by the GP during training to adapt to the structure of each function.

- **Noise level (WhiteKernel)**  
  Adjusted for functions that exhibited higher variance or measurement noise.

- **Sobol sampling resolution**  
  The candidate points were concentrated around promising regions that emerged.

Hyperparameters were adjusted manually based on observed performance trends and surrogate behaviour rather than using automated grid or random search, reflecting realistic constraints of limited evaluation budgets.


## Results

Across multiple optimisation rounds, performance improved steadily for most functions. Lower-dimensional and unimodal functions converged quickly toward strong solutions, while higher-dimensional and noisy functions required longer exploration phases. Example visualisations and convergence plots are included in the `notebooks` folder.

Key observations include:

- Early exploration improved surrogate model stability  
- Adaptive acquisition strategies helped avoid stagnation  
- Targeted exploitation accelerated convergence in later rounds  
- Sobol sampling provided better space coverage than random sampling  

Overall, the project demonstrates that Bayesian Optimisation can efficiently locate strong candidate solutions even with limited data and unknown function structure.
