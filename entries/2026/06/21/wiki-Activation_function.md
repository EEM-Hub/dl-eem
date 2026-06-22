---
source: sources/wiki-Activation_function.md
source_url: https://en.wikipedia.org/wiki/Activation_function
---

I'll create the study notes entry now.

## Activation Functions in Neural Networks
An activation function computes a neural network node's output from its weighted inputs. Nonlinear activation functions are essential — they enable even small networks to solve nontrivial problems and are what allow multi-layer networks to be universal function approximators (per the Universal Approximation Theorem). The choice of activation function affects training dynamics, gradient flow, and model expressiveness.

## Key Concepts

- **Nonlinearity requirement**: With a non-linear activation, a two-layer network is a universal function approximator. Identity (linear) activation across all layers collapses the network to a single-layer equivalent.
- **Saturating vs. nonsaturating**: A function is saturating if its gradient approaches 0 as |v| → ∞. Nonsaturating functions (e.g., ReLU) are less prone to the vanishing gradient problem.
- **Range tradeoff**: Finite-range activations (sigmoid, tanh) yield more stable gradient-based training; infinite-range activations (ReLU) yield more efficient training but require smaller learning rates.
- **Continuous differentiability**: Desirable for gradient-based optimization. ReLU is not continuously differentiable (C⁰) but works in practice. Binary step has zero gradient everywhere except at 0, making gradient-based training impossible.
- **Three categories of activation functions**:
  - **Ridge functions**: Act on a linear combination of inputs (Linear, ReLU, Sigmoid, Heaviside)
  - **Radial functions**: Depend on distance from a center vector (Gaussian RBF, Multiquadratic); used in RBF networks
  - **Fold functions**: Aggregate over inputs (mean, max, softmax); used in pooling layers and multiclass output layers

## Key Activation Functions

| Function | Range | Key Property |
|----------|-------|-------------|
| **Sigmoid** σ(x) = 1/(1+e⁻ˣ) | (0,1) | Saturating, C∞, derivative = σ(x)(1−σ(x)); used in Hinton's 2012 speech model |
| **Tanh** | (−1,1) | Saturating, C∞, zero-centered output, derivative = 1−tanh²(x) |
| **ReLU** max(0,x) | [0,∞) | Nonsaturating, C⁰, sparse activation; used in AlexNet (2012), ResNet (2015) |
| **GELU** x·Φ(x) | (−0.17…,∞) | Smooth approximation of ReLU, C∞; used in BERT (2018) |
| **Leaky ReLU** | (−∞,∞) | Fixes "dying ReLU" with small negative slope (0.01x for x<0) |
| **PReLU** | (−∞,∞) | Like Leaky ReLU but negative slope α is a learned parameter |
| **ELU** | (−α,∞) | Smooth for negative inputs: α(eˣ−1); C¹ when α=1 |
| **SELU** | (−λα,∞) | Self-normalizing; fixed λ=1.0507, α=1.67326 |
| **Softplus** ln(1+eˣ) | (0,∞) | Smooth approximation of ReLU, C∞; derivative is the sigmoid |
| **SiLU/Swish** x·σ(x) | [−0.278…,∞) | Self-gated, C∞, non-monotonic |
| **Softmax** | (0,1) per class | Multi-input fold function for multiclass classification; outputs sum to 1 |
| **Maxout** | (−∞,∞) | Takes max over multiple linear pieces; generalizes ReLU |

## Commands and Syntax

```python
# Common activation functions in PyTorch
import torch.nn as nn

nn.ReLU()
nn.Sigmoid()
nn.Tanh()
nn.GELU()
nn.LeakyReLU(negative_slope=0.01)
nn.PReLU(num_parameters=1)
nn.ELU(alpha=1.0)
nn.SELU()
nn.SiLU()       # Swish
nn.Softplus()
nn.Softmax(dim=-1)
```

## Relationships

- **Universal Approximation Theorem**: Nonlinear activation is a prerequisite; proven by Cybenko (1989) for sigmoid
- **Vanishing gradient problem**: Saturating functions (sigmoid, tanh) exacerbate it in deep networks; nonsaturating functions (ReLU family) mitigate it
- **Batch/Layer Normalization**: Often used alongside ReLU-family activations to stabilize training
- **SELU + self-normalizing networks**: SELU activations maintain mean 0 and variance 1 across layers without explicit normalization
- **Softmax + cross-entropy loss**: Standard pairing for multiclass classification output layers
- **Softplus and variational autoencoders**: Strictly positive range makes it suitable for predicting variances
- **RBF networks**: Use radial activation functions (Gaussian RBF) rather than ridge functions
- **Biological neurons**: Sigmoid functions model the bounded firing rate of biological neurons; binary step models fire/no-fire

## Exam-Relevant Points

- A network using only identity (linear) activations across all layers is equivalent to a single-layer model — nonlinearity is required for depth to matter
- **ReLU** is not continuously differentiable (C⁰ continuity) but remains the most widely used activation in practice
- **Sigmoid** derivative: σ(x)(1−σ(x)); **Tanh** derivative: 1−tanh²(x) — know these formulas
- **Softmax** is not a function of a single input — it normalizes across all inputs in the vector; derivative involves the Kronecker delta
- **GELU** = x·Φ(x) where Φ is the standard Gaussian CDF; used in Transformer models (BERT, GPT)
- **Softplus** is a smooth approximation of ReLU; its derivative is the sigmoid function
- **Leaky ReLU** addresses the "dying neuron" problem where ReLU neurons output zero for all inputs
- **SELU** has fixed parameters (λ=1.0507, α=1.67326) derived to achieve self-normalizing property
- Finite-range activations → more stable training; infinite-range → more efficient training but needs smaller learning rate
- **Saturating** functions have gradient → 0 at extremes (sigmoid, tanh); **nonsaturating** functions do not (ReLU) — this distinction is central to understanding vanishing gradients in deep networks
