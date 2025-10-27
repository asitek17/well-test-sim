# PINN for Well Test Analysis

## Project Overview
This project explores the application of Physics-Informed Neural Networks (PINNs) to the problem of well test analysis in reservoir engineering. The aim is to evaluate whether PINNs can learn to map spatial permeability fields around a well to recovery pressure curves, integrating physics-based regularization during training.

The study compares PINN-based models with traditional neural networks trained only with data-driven loss, analyzing both their accuracy and their ability to generate physically realistic outputs.

## Contents
- well_test_PINN.ipynb: Main notebook containing the full workflow, model, training loops, and evaluation.

- curve.png: Visualization of a typical pressure recovery curve.

- map.png: Example plot of a spatial permeability map.

- predict.png, predict2.png, predict2_1.png: Plots comparing model predictions with ground truth.

- data/: Directory with training/test datasets (permeability maps, pressure curves).

Other course and auxiliary files (reports, slides, Russian-language materials).

## Dataset Description
The dataset consists of simulated spatial permeability maps (shape: 256x256) and corresponding pressure recovery curves at the well (shape: 361 time steps for each sample). The maps and curves are split into training, validation, and test subsets using a standard split (e.g., 2025/225/250 samples for each, respectively).​

All data is normalized to zero mean and unit variance per pixel.

## Model and PINN Approach
Two models are implemented:

- Vanilla Neural Network: Fully connected MLP that predicts pressure curves from map patches, trained with mean squared error loss and optional monotonicity constraints.

- Physics-Informed Neural Network (PINN): The same MLP, but trained with an additional physical regularization loss derived from domain-specific equations (e.g., mass conservation, volume coefficients as per reservoir theory). The PINN loss includes data loss, monotonicity loss, and physics-based loss terms, each scaled by a tunable coefficient.​

## How to Run
- Install dependencies from the notebook (PyTorch, matplotlib, numpy, scikit-learn).

- Place the dataset in the data/ directory (included).

- Open and run well_test_PINN.ipynb step by step. The notebook will visualize maps, curves, and show evaluation plots.

- Adjust model parameters and loss weights as needed in the notebook configuration section.

- All major hyperparameters, such as batch size, patch size, number of epochs, and regularization weights, can be set interactively within the notebook file.

## Results
The best PINN model achieves a mean $R^2 \approx 0.68$ and $RMSE \approx 0.24$ on the test set (normalized scale).

The project demonstrates that incorporating physical loss terms improves the physical plausibility of predictions, as seen in both qualitative plots and numeric metrics.

Comparative plots of ground truth vs. PINN and vs. vanilla model are saved as .png files for analysis.​

## Acknowledgements
Project developed as a final individual assignment for the "Technologies of Scientific-Informed Machine Learning" course.
