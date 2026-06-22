---
source: sources/wiki-Dropout_neural_networks.md
source_url: https://en.wikipedia.org/wiki/Dropout_(neural_networks)
---

## Dropout Regularization in Neural Networks

Dropout is a regularization technique that reduces overfitting in neural networks by randomly setting neuron inputs/outputs to zero during training (not inference). It prevents complex co-adaptations among neurons on training data. The technique was named "dropout" by Geoffrey Hinton et al. in 2012, though the underlying idea (called "dilution") dates back to at least 1987.

## Key Concepts

- **Dropout** randomly zeroes entire rows of the weight matrix (effectively removing whole neurons), distinguished from **dilution** which randomly zeroes individual weights
- **Dilution** comes in two forms:
  - **Weak dilution**: small fraction of connections removed; solvable exactly with mean field theory
  - **Strong dilution**: large fraction removed; creates large uncertainty, mean field theory does not apply
- **P(c)** is the probability of *keeping* a weight/neuron (not dropping it)
- Dropout is applied only during **training**, never during inference
- The mechanism prevents **co-adaptation of feature detectors** — neurons cannot rely on specific other neurons being present, forcing redundant representations
- Whether zeroing happens at weights, node outputs, or elsewhere in the computation graph does not change the mathematical result — only implementation efficiency differs
- Dilution/dropout are **iterative** processes where the network continues learning, unlike **pruning** which is a one-time removal

## Commands and Syntax

No CLI commands. In frameworks:

```python
# PyTorch
nn.Dropout(p=0.5)       # p = probability of DROPPING (1 - P(c))

# TensorFlow/Keras
tf.keras.layers.Dropout(rate=0.5)  # rate = drop probability
```

Mathematical formulation:
- Linear layer output: `y_i = Σ_j w_ij * x_j` (vector form: **y** = **Wx**)
- Weak dilution: `ŵ_ij = w_ij with P(c), else 0` (individual weights)
- Dropout: `ŵ_j = w_j with P(c), else 0` (entire rows/neurons)

## Relationships

- **Regularization**: Dropout is one of several regularization methods (alongside L1/L2 weight decay, early stopping, data augmentation)
- **AlexNet**: One of the first major architectures to use dropout successfully
- **CNNs**: Dropout is commonly applied in fully connected layers of convolutional networks
- **Ensemble interpretation**: Dropout can be viewed as training an exponential number of sub-networks simultaneously and averaging their predictions at inference
- **Batch Normalization**: Partially overlaps with dropout's regularization effect; some architectures use one or the other but not both
- **Mean field theory**: Provides the theoretical framework for analyzing weak dilution, but does not apply to full dropout

## Exam-Relevant Points

- Dropout is applied **during training only** — at inference, all neurons are active (with weights scaled by P(c))
- Dropout zeros **entire neurons** (whole rows of weight matrix); dilution zeros **individual weights**
- The keep probability P(c) is the key hyperparameter (commonly 0.5 for hidden layers, higher like 0.8 for input layers)
- Historical priority: the concept predates Hinton's 2012 paper — Hertz, Krogh, and Palmer described "dilution" in 1991, referencing Sompolinsky (1987) and Canning & Gardner (1988)
- Google holds the patent (US 9406017B2), though its validity is questionable due to prior art
- Weak dilution assumptions allow mean field theory solutions; dropout violates those assumptions by removing entire rows
- Dropout forces **redundant distributed representations**, preventing any single neuron from becoming a critical feature detector
