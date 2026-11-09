# 06 — Computer Vision (CV)

## Dedicated notebook copy

`cifar10-image-classification (torchvision).ipynb`

This is a byte-for-byte copy of the complete neural-network notebook also stored in `03-DL/01-Neural-Networks/`. It gives the CV category an actual notebook file for browsing and running.

**Important scope note:** the original assignment combines neural-network foundations and CIFAR-10 image classification. This copied notebook therefore retains all activation-function, backpropagation, NumPy MLP, gradient-checking and PyTorch sections as well as the CIFAR-10 image task. No cells were extracted, deleted or edited. The canonical notebook remains in the Deep Learning folder.

## Image-classification implementation

- Dataset: CIFAR-10, loaded through `torchvision.datasets.CIFAR10`.
- Image size: 32×32 pixels, RGB.
- Flattened input dimension: 3,072.
- Fully connected MLP: **3072 → 256 → 128 → 10**.
- Notebook training design includes mini-batch training, momentum (0.9), 15 epochs, best-validation checkpointing, training/validation curves, confusion matrix, per-class accuracy and first-layer weight visualisation.
- A 64-image overfit test and a λ=10⁻³ regularisation comparison are also included.

## Results and execution status

The accompanying report marks CIFAR-dependent losses, accuracies, confusion matrix, class-wise accuracy and weight visualisations as pending because CIFAR-10 could not be downloaded during that run. Consequently, this repository does **not** claim a CIFAR-10 accuracy or other unmeasured CV metric.

The notebook downloads CIFAR-10 through `torchvision`; no CSV file is required. A first run may need network access. Run all cells from a fresh kernel to generate the actual metrics before using them in a CV.

## Architecture distinction

This is a fully connected multilayer perceptron (MLP), not a convolutional neural network (CNN). It is accurately described as a CIFAR-10 image-classification / introductory CV exercise using an MLP.

## Canonical source

[Canonical notebook](../03-DL/01-Neural-Networks/neural-networks-and-cifar10.ipynb) · [Deep Learning README](../03-DL/README.md)
