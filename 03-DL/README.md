# 03 — Deep Learning

The deep-learning section is centred on one comprehensive notebook that builds neural-network understanding from mathematical components through NumPy and PyTorch experiments.

## Contents
- [01 — Neural Networks](01-Neural-Networks/README.md)
- `01-Neural-Networks/neural-networks-and-cifar10.ipynb`
- `deep-learning-report.pdf`

## Coverage
1. Activation functions and derivatives: sigmoid, tanh, ReLU, leaky ReLU and softplus.
2. Manual backpropagation through a small network with a tanh hidden layer.
3. Numerically stable softmax and cross-entropy.
4. Data pipelines for the Wine dataset and CIFAR-10.
5. NumPy MLP forward pass on Wine.
6. NumPy backpropagation, finite-difference gradient checking and overfit test.
7. CIFAR-10 MLP image classification.
8. Gradient-flow experiments in ten-hidden-layer PyTorch networks, comparing sigmoid/ReLU and Xavier/He initialisation, plus batch normalisation.
9. Bonus comparison between PyTorch autograd and NumPy backpropagation.

## Verified numerical result
The report records the bonus NumPy/PyTorch gradient comparison:
- Maximum parameter-gradient difference: **2.7756 × 10⁻¹⁷**, passing the stated 10⁻⁹ tolerance.
- Maximum dZ differences: **3.4694 × 10⁻¹⁸**, **3.4694 × 10⁻¹⁸** and **1.3878 × 10⁻¹⁷**.
- Two consecutive backward calls double the accumulated gradient exactly in the reported check (difference from 2× gradient = 0).
- `no_grad` output has `requires_grad=False`; after `detach`, the first-layer gradient is `None`, as expected.

## CIFAR-10 and computer vision scope
The CIFAR-10 section uses flattened 32×32 RGB images (3,072 input values) and an MLP architecture of **3072–256–128–10**. The report marks actual CIFAR-dependent training losses, accuracies, confusion matrix and class-wise results as pending because CIFAR-10 was unavailable during that run. Those values are not claimed here. The model is a fully connected MLP, **not a CNN**.

CIFAR-10 is downloaded by `torchvision.datasets.CIFAR10`; it is not supplied as a CSV. The first run may require network access.

## Reproducibility and scope
Run from a fresh kernel and execute cells in order. The report notes that the supplied assignment PDF contains P1–P9 and does not include a P10 prompt, despite an overview reference to P10. No missing P10 requirements have been inferred.


## CV category copy
A complete byte-for-byte copy of the neural-network notebook is also available in [`06-CV/`](../06-CV/README.md). It retains the full original notebook, not just the CIFAR-10 cells. The canonical notebook remains in this Deep Learning folder.
