---
source: sources/wiki-Batch_normalization.md
source_url: https://en.wikipedia.org/wiki/Batch_normalization
---

I'll create an entry summarizing this batch normalization documentation.

## Batch Normalization in Neural Networks

Batch normalization (batch norm) is a normalization technique introduced by Ioffe and Szegedy in 2015 that stabilizes and accelerates neural network training by re-centering layer inputs to zero mean and re-scaling them to unit variance within each mini-batch. Despite widespread adoption, the theoretical reasons for its effectiveness remain debated — the original "internal covariate shift" explanation has been challenged in favor of a loss-landscape smoothing hypothesis.

## Key Concepts

- **Internal covariate shift**: The phenomenon where the distribution of inputs to each layer changes during training as preceding layer parameters update, forcing each layer to continuously readjust. Batch norm was originally designed to address this, though newer evidence questions this explanation.
- **Normalization step**: For each mini-batch of size *m*, compute per-dimension mean μ_B and variance σ²_B, then normalize each activation to zero mean and unit variance: x̂ = (x - μ_B) / √(σ²_B + ε).
- **Learnable affine transform**: After normalization, apply y = γx̂ + β, where γ (scale) and β (shift) are learned parameters that restore the network's representational capacity. Without these, normalization would constrain what the layer can represent.
- **Epsilon (ε)**: A small positive constant added to the denominator for numerical stability during division by standard deviation.
- **Per-dimension normalization**: Each feature dimension is normalized independently across the mini-batch, not jointly across dimensions.
- **Training vs. inference difference**: Training uses mini-batch statistics; inference uses population statistics (running averages accumulated during training). This makes inference deterministic and independent of batch composition.
- **Population statistics at inference**: Population mean = E_B[μ_B], population variance = (m/(m-1)) · E_B[σ²_B] — note the Bessel correction factor m/(m-1) for unbiased variance estimation.
- **Inference as linear transform**: At inference time, since all parameters are fixed, batch norm reduces to a simple linear transformation of the activation.
- **Non-iid batch elements**: Batch norm creates statistical dependencies between items in a mini-batch (they share mean/variance), breaking the iid assumption and potentially degrading gradient estimation quality.

## Commands and Syntax

**Batch Norm Forward Pass (Training):**
1. Compute mini-batch mean: μ_B = (1/m) Σ x_i
2. Compute mini-batch variance: σ²_B = (1/m) Σ (x_i - μ_B)²
3. Normalize: x̂_i = (x_i - μ_B) / √(σ²_B + ε)
4. Scale and shift: y_i = γ · x̂_i + β

**Batch Norm Forward Pass (Inference):**
- y = γ · (x - E[x]) / √(Var[x] + ε) + β
- Uses accumulated population statistics instead of mini-batch statistics

**Backpropagation gradients:**
- ∂l/∂x̂ = (∂l/∂y) · γ
- ∂l/∂γ = Σ (∂l/∂y_i) · x̂_i
- ∂l/∂β = Σ (∂l/∂y_i)
- ∂l/∂x_i depends on ∂l/∂x̂, ∂l/∂σ², and ∂l/∂μ (all three terms contribute)

## Relationships

- **Gradient flow**: Batch norm interacts with the vanishing/exploding gradient problem — it allows higher learning rates without gradient instability, but in very deep networks can initially cause gradient explosion, mitigated by **skip connections** in residual networks (ResNets).
- **Regularization**: Acts as an implicit regularizer, reducing the need for **dropout**. The noise introduced by using mini-batch statistics (rather than population statistics) during training provides a regularizing effect.
- **Stochastic optimization**: Designed to work with SGD and its variants — using full-dataset statistics would be impractical, so mini-batch statistics are a practical approximation.
- **Loss landscape smoothing**: Related to **Lipschitz continuity** — batch norm produces a smoother objective function with a smaller Lipschitz constant, making gradient descent more reliable and predictive.
- **Activation functions**: Placed before or after activation functions; the BN output y is what gets passed to subsequent layers.
- **Alternative normalization methods**: Part of a family including Layer Normalization, Instance Normalization, and Group Normalization, which differ in which dimensions statistics are computed over.

## Exam-Relevant Points

- Batch norm normalizes per-dimension across the mini-batch, producing zero mean and unit variance activations (before the affine transform).
- The learnable parameters γ and β are essential — they allow the network to undo the normalization if that is optimal, preserving representational power.
- Training uses mini-batch statistics; inference uses population statistics (running mean/variance). This is a critical train/test behavioral difference.
- Population variance uses Bessel's correction: m/(m-1) multiplier for unbiased estimation.
- The original "internal covariate shift" explanation has been empirically challenged — experiments adding explicit covariate shift noise to batch-normed networks showed no performance degradation, suggesting smoothing of the loss landscape is the actual mechanism.
- Batch norm allows higher learning rates, reduces sensitivity to initialization, and has a regularizing effect (reducing need for dropout).
- The BN transform is fully differentiable, enabling standard backpropagation through all parameters.
- Batch norm introduces dependencies between mini-batch elements (non-iid), which can hurt gradient quality — this is a known limitation.
- At inference time, batch norm collapses to a fixed linear transform since all statistics and parameters are frozen.
- The gradient magnitude bound includes a γ²/σ² scaling factor, meaning batch norm's smoothing effect is stronger when mini-batch variance is large.
