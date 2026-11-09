# 03.1 — Neural Networks and CIFAR-10

## Main notebook
`neural-networks-and-cifar10.ipynb`

A progressive implementation notebook covering neural-network mathematics, a NumPy multilayer perceptron, PyTorch automatic differentiation and a CIFAR-10 image-classification pipeline.

## Experiment-by-experiment guide

| Part | Implementation | What it demonstrates |
|---|---|---|
| P1 | Activation functions and derivatives | Nonlinearities and their gradients |
| P2 | Manual backpropagation | Chain-rule propagation through a tanh hidden layer |
| P3 | Stable softmax and cross-entropy | Numerically stable multiclass probabilities and loss gradients |
| P4 | Wine and CIFAR-10 data pipelines | Dataset loading and preparation |
| P5 | NumPy MLP forward pass on Wine | Layer-wise affine transforms, activations and logits |
| P6 | NumPy backpropagation | Parameter gradients, finite-difference checks and overfit test |
| P7 | CIFAR-10 NumPy MLP | Mini-batch training with momentum and regularisation comparison |
| P8 | Deep PyTorch networks | Gradient magnitudes and activation statistics across ten hidden layers |
| P9 | Autograd versus NumPy | Independent gradient implementation cross-check |
| P10 | No task statement supplied | No result claimed |

## P9 numerical verification
The report records:
- maximum parameter-gradient difference = **2.7756e−17**;
- maximum intermediate dZ differences = **3.4694e−18**, **3.4694e−18**, **1.3878e−17**;
- gradient accumulation check after two backward calls: exact doubling (difference = 0);
- `no_grad` and `detach` behaviour checks passed.

These tiny differences indicate numerical agreement between the two gradient implementations for the stated small Wine batch and setup.

## CIFAR-10 image task
- Input: flattened 32×32×3 image, 3,072 input features.
- Network: 3,072 → 256 → 128 → 10.
- Training design in the notebook: mini-batches, momentum 0.9, 15 epochs, best-validation checkpoint, training/validation curves, confusion matrix and per-class accuracy.
- A 64-image overfit test and λ=10⁻³ comparison are included in the notebook/report plan.

**Status:** the report explicitly says CIFAR-dependent outputs (losses, accuracies, confusion matrix, per-class ranking, weight visualisations and regularisation comparison) were pending because the dataset could not be downloaded in that run. Do not cite a CIFAR accuracy until the notebook is run successfully and the result is recorded.

## Dependencies
The Wine dataset is loaded through the relevant library data interface. CIFAR-10 is fetched through `torchvision`; no CSV is required. The notebook also uses NumPy, PyTorch, Matplotlib and scikit-learn components as imported in its cells.
