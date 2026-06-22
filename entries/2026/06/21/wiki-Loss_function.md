---
source: sources/wiki-Loss_function.md
source_url: https://en.wikipedia.org/wiki/Loss_function
---

## Loss Functions in Optimization and Decision Theory

A loss function (also called cost function or error function) maps an event or variable values onto a real number representing the "cost" associated with that event. Optimization problems seek to minimize a loss function. When the objective is instead to maximize, the function is called a reward, profit, utility, or fitness function. Loss functions are foundational across statistics, economics, classification, actuarial science, optimal control, and financial risk management.

## Key Concepts

- **Loss function vs. objective function**: A loss function is minimized; an objective function is either a loss (minimized) or its negation — a reward/utility/fitness function (maximized)
- **Quadratic (squared error) loss**: `L(x) = C(t - x)²` — symmetric, mathematically tractable due to variance properties, but sensitive to outliers
- **Absolute loss**: `L(a) = |a|` — more robust to outliers than squared loss, but not differentiable at zero
- **0-1 loss**: Returns 0 for correct classification, 1 for incorrect — used in classification and equivalent to Hamming distortion in information theory
- **Huber loss, log-cosh, SMAE**: Alternatives to quadratic loss that are more robust when data contains large outliers
- **Regret**: Loss defined as the difference between the best possible decision (with hindsight) and the actual decision taken — advocated by Savage for non-Bayesian methods like minimax
- **Risk function**: The expected value of the loss function — `R(θ, δ) = E_θ[L(θ, δ(X))]` — connects loss to statistical estimation
- **Bayes risk**: Expected loss computed using the prior distribution over parameters; minimizing posterior risk for each observation yields the Bayes decision rule
- **Mean squared error (MSE)**: The risk function under quadratic loss — minimized by the posterior mean
- **Mean integrated squared error (MISE)**: Risk function for density estimation under L² norm loss

## Commands and Syntax

Key mathematical formulations:

- **Quadratic loss**: `λ(x) = C(t - x)²`
- **0-1 loss**: `L(ŷ, y) = 0 if y = ŷ, 1 if y ≠ ŷ`
- **Frequentist risk**: `R(θ, δ) = ∫_X L(θ, δ(x)) dP_θ(x)`
- **Bayes risk**: `ρ(π*, a) = ∫_Θ ∫_X L(θ, a(x)) dP(x|θ) dπ*(θ)`
- **Minimax rule**: `argmin_δ max_{θ∈Θ} R(θ, δ)` — choose the decision rule with the lowest worst-case loss

## Relationships

- **Mathematical optimization**: Loss functions define the objective that optimization algorithms minimize
- **Least squares / linear regression**: Built on the quadratic loss function; underpins t-tests, regression models, and experimental design
- **Parameter estimation**: Loss quantifies the discrepancy between estimated and true values
- **Bayesian vs. frequentist inference**: Both use expected loss but compute it differently — frequentist conditions on θ, Bayesian integrates over the prior
- **Linear-quadratic regulator (LQR)**: Uses quadratic loss in optimal control, yielding linear first-order conditions
- **Empirical risk minimization**: Framework for choosing models by minimizing average loss over training data
- **Utility theory / von Neumann-Morgenstern**: In economics, loss is the negative of utility; risk-neutral agents use expected monetary value, risk-averse agents use expected utility
- **Scoring rules**: Related framework for evaluating probabilistic predictions
- **Hinge loss**: Used in SVMs — a classification-specific loss function

## Exam-Relevant Points

- **Squared loss minimizer is the mean; absolute loss minimizer is the median** — a classic result connecting loss function choice to the optimal location estimator
- **Quadratic loss is sensitive to outliers** because squaring amplifies large errors; Huber loss and log-cosh are robust alternatives
- **0-1 loss** is the standard loss for classification problems and equals Hamming distortion in information theory
- **Risk function = expected loss** — the bridge between a single-observation loss and a statistical criterion
- **Minimax decision rule** minimizes the maximum possible risk across all parameter values — a worst-case approach
- **Bayes decision rule** minimizes posterior risk and yields a uniformly optimal action given the observed data
- **MSE = risk under quadratic loss** — minimized by the posterior mean estimator
- **Loss functions should be globally continuous and differentiable** for most optimization algorithms to work well — absolute loss violates differentiability at zero
- **Real-world losses are often asymmetric and discontinuous** (Deming/Taleb argument) — e.g., missing a flight by 1 minute vs. arriving 1 minute early have vastly different costs
- **Choice of loss function determines the optimal estimator** — not arbitrary; constrained by the problem's actual cost structure
