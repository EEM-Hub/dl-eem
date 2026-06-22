---
source: sources/wiki-Regularization_mathematics.md
source_url: https://en.wikipedia.org/wiki/Regularization_(mathematics)
---

## Regularization Techniques in Deep Learning

Regularization is a family of techniques that constrain or modify the learning process to prevent overfitting and improve generalization to unseen data. It works by discouraging overly complex models, either by explicitly adding penalty terms to the loss function or by implicitly constraining the learning procedure. The fundamental tradeoff is between fitting the training data closely and keeping the model simple enough to generalize — controlled by the hyperparameter λ.

## Key Concepts

- **Regularization** converts an ill-posed or underdetermined problem into a well-posed one by adding constraints or penalties that favor simpler solutions (Occam's razor principle)
- **Explicit regularization** adds a term directly to the optimization objective (priors, penalties, constraints) — e.g., L1, L2 penalties
- **Implicit regularization** arises from algorithmic choices rather than explicit penalty terms — e.g., early stopping, SGD noise, ensemble methods, robust loss functions
- **The regularized objective** has two components: a **data term** (loss on training data, corresponds to likelihood) and a **regularization term** (penalty on model complexity, corresponds to prior)
- **λ (lambda)** controls the tradeoff between data fidelity and regularization strength — higher λ means stronger regularization, simpler models
- **Bayesian interpretation**: regularization terms correspond to prior distributions on model parameters; combining data term + regularization = computing a posterior
- **Generalization error** is the error on unseen data — regularization aims to minimize this, not training error
- **Empirical error** (training loss) is a surrogate for the unmeasurable expected error; without regularization, models can achieve zero empirical error but overfit
- **L0 norm** (count of non-zero weights) is the ideal sparsity constraint but is NP-hard to optimize

## Commands and Syntax

**General regularized loss function:**
```
min_f  Σ V(f(x_i), y_i) + λ R(f)
```
where V is the loss function, R(f) is the regularization term, λ controls regularization strength.

**L2 / Tikhonov / Ridge Regression:**
```
min_w  Σ V(x̂_i · w, ŷ_i) + λ ||w||₂²
```
- Penalizes squared magnitude of weights
- Differentiable → amenable to gradient descent
- Closed-form solution: `w = (X^T X + λnI)^{-1} (X^T Y)`
- Training complexity: O(d³ + nd²); Testing: O(nd)

**L1 / LASSO:**
```
min_w  (1/n) ||X̂w - Ŷ||² + λ ||w||₁
```
- Penalizes absolute value of weights
- Induces sparsity (drives weights exactly to zero)
- Convex relaxation of the NP-hard L0 problem
- Can produce non-unique solutions when solution space aligns with L1 ball geometry

**Elastic Net (L1 + L2 combined):**
```
min_w  (1/n) ||X̂w - Ŷ||² + λ(α||w||₁ + (1-α)||w||₂²),  α ∈ [0,1]
```
- Overcomes L1's non-uniqueness problem
- α controls the mix between L1 (sparsity) and L2 (smoothness)

**Early stopping as gradient descent truncation:**
```
w₀ = 0
w_{t+1} = (I - (γ/n) X̂ᵀX̂) w_t + (γ/n) X̂ᵀŶ
```
- Limit iterations T to regularize; equivalent to Neumann series approximation of the unregularized solution

## Relationships

- **Overfitting**: Regularization is the primary defense against overfitting; all techniques aim to reduce the gap between training and test performance
- **Bias-variance tradeoff**: Regularization increases bias (by constraining the model) but reduces variance (by preventing fitting to noise) — λ controls this tradeoff
- **Bayesian inference**: L2 regularization corresponds to a Gaussian prior on weights; L1 corresponds to a Laplace prior; the regularized solution approximates the MAP estimate
- **Dropout**: Connects to ensemble methods — randomly dropping neurons during training approximates training an ensemble of sub-networks
- **SGD and implicit regularization**: Stochastic gradient descent's noise acts as an implicit regularizer, favoring flatter minima that generalize better
- **Early stopping and L2**: Early stopping in gradient descent is mathematically related to L2 regularization — both constrain the effective model complexity, with T (iterations) playing a role analogous to 1/λ
- **Feature selection**: L1 regularization connects to feature selection by zeroing out irrelevant feature weights; useful in high-dimensional settings (computational biology, genomics)
- **Reproducing Kernel Hilbert Spaces (RKHS)**: Tikhonov regularization generalizes to non-linear models via the RKHS norm

## Exam-Relevant Points

- **L1 produces sparse models** (weights driven to exactly zero); **L2 produces small but non-zero weights** — know the geometric intuition (L1 ball has corners at axes where sparsity occurs)
- **L0 regularization is NP-hard**; L1 is its convex relaxation
- **Ridge regression closed-form**: w = (XᵀX + λnI)⁻¹(XᵀY) — adding λnI to XᵀX ensures invertibility even when features outnumber samples
- **Early stopping = regularization in time**: limiting gradient descent iterations prevents convergence to the empirical risk minimizer, controlling complexity
- **Dropout rate** is typically 0.5 for hidden layers; it simulates training an exponential number of sub-networks
- **Elastic net** combines L1 and L2, controlled by α ∈ [0,1]; resolves L1's non-uniqueness while preserving sparsity
- **Higher λ → simpler model, more regularization, potentially more bias**; lower λ → closer to unregularized solution, risk of overfitting
- **Tikhonov regularization** training time is O(d³ + nd²), dominated by matrix inversion
- **Three datasets for early stopping**: training (fit model), validation (monitor for stopping), test (final evaluation) — never use test set for stopping decisions
- **Regularization ≠ just preventing overfitting**: also stabilizes ill-posed problems, induces sparsity for interpretability, and enables learning when p >> n (more features than samples)
