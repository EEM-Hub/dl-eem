---
source: sources/wiki-Gradient_descent.md
source_url: https://en.wikipedia.org/wiki/Gradient_descent
---

Here's the structured study entry for **Gradient Descent**:

---

## Gradient Descent: The Core Optimization Algorithm for Deep Learning

Gradient descent is a first-order iterative optimization algorithm for finding local minima of differentiable multivariate functions. It works by repeatedly stepping in the direction of the negative gradient (steepest descent). Attributed to Cauchy (1847) and independently proposed by Hadamard (1907), gradient descent — and its stochastic variant SGD — is the foundational algorithm for training deep neural networks. The update rule is x_{n+1} = x_n - eta_n * grad(f(x_n)), where eta_n is the learning rate (step size).

## Key Concepts

- **Update rule**: x_{n+1} = x_n - eta * nabla f(x_n). Subtract the gradient scaled by the learning rate to move toward lower function values.
- **Learning rate (eta)**: Controls step size. Too small = slow convergence. Too large = overshoot and divergence. Can vary per iteration.
- **Monotonic decrease guarantee**: For sufficiently small eta, f(x_{n+1}) <= f(x_n) — the function value never increases.
- **Convergence conditions**: Guaranteed convergence to a local minimum when f is convex and nabla f is Lipschitz continuous.
- **Convex functions**: When f is convex, all local minima are global minima, so gradient descent finds the global optimum.
- **Gradient direction**: The negative gradient is orthogonal to contour lines (level sets) of the function — it always points in the direction of steepest local decrease.
- **Gradient ascent**: Stepping in the positive gradient direction instead maximizes the function.
- **Saddle points**: Gradient descent can get stuck at saddle points (not just local minima), which is a significant concern in high-dimensional optimization.
- **Stochastic gradient descent (SGD)**: The primary extension of gradient descent; the most basic algorithm for training deep networks today.

## Learning Rate Selection Methods

- **Barzilai-Borwein method**: Adaptive step size computed from consecutive gradient differences: eta_n = |delta_x^T * delta_g| / ||delta_g||^2.
- **Wolfe conditions**: Sufficient decrease + curvature conditions that a step size must satisfy; found via line search.
- **Backtracking line search**: Economical method for choosing learning rates with good theoretical guarantees and practical results.
- **Lipschitz constant bound**: If nabla f is L-Lipschitz, use L to bound gradient variation and derive optimal step size.
- **Hessian-based estimation**: Use the second derivative (Hessian) to estimate how quickly the gradient changes and choose step size accordingly.

## Descent Direction Strategies

- **Steepest descent**: p_n = nabla f(x_n), the default choice — direction of maximum local decrease.
- **General descent direction**: Any direction p_n with positive inner product with -nabla f(x_n) (i.e., cos(theta) > 0) guarantees decrease for small enough eta.
- **Non-gradient directions**: A smaller slope can be compensated by being sustained over a longer distance — sometimes deviating from steepest descent is beneficial.
- **Trade-off principle**: Guaranteed decrease depends on the balance between (1) alignment of descent direction with negative gradient and (2) how quickly the gradient changes along that direction.

## Linear Systems Application

- **Quadratic minimization**: Gradient descent solves Ax = b by minimizing f(x) = x^T A x - 2x^T b when A is symmetric positive-definite.
- **Gradient of quadratic**: nabla f(x) = 2(Ax - b), making each step straightforward.
- **Least squares**: For general A, minimizes f(x) = ||Ax - b||^2 using normal equations (gradient = 2A^T(Ax - b)).

## Commands and Syntax

```python
# Basic gradient descent pseudocode
x = x_0  # initial guess
for n in range(max_iterations):
    grad = compute_gradient(f, x)
    x = x - eta * grad  # update step

# With adaptive learning rate (Barzilai-Borwein)
delta_x = x_n - x_prev
delta_g = grad_n - grad_prev
eta = abs(delta_x.T @ delta_g) / (np.linalg.norm(delta_g) ** 2)
```

## Relationships

- **Stochastic gradient descent (SGD)**: Uses a random subset of data to approximate the gradient; the workhorse of deep learning training.
- **Backpropagation**: The algorithm for computing gradients in neural networks, which gradient descent then uses for weight updates.
- **Loss/cost functions**: Gradient descent minimizes these; the choice of loss function shapes the optimization landscape.
- **Learning rate schedules**: Techniques like cosine annealing, warm-up, and step decay modify eta over training.
- **Momentum methods**: Extensions (Nesterov momentum, Adam, RMSProp) that accelerate convergence by accumulating gradient history.
- **Second-order methods**: Newton's method, L-BFGS use Hessian information for better convergence but at higher computational cost.
- **Convex optimization**: Gradient descent theory is well-understood for convex problems; non-convex (deep learning) convergence is more nuanced.
- **Batch normalization, dropout**: Regularization techniques that alter the loss landscape and interact with gradient-based optimization.

## Exam-Relevant Points

- The update rule is x_{n+1} = x_n - eta * nabla f(x_n); know this formula cold.
- The learning rate (eta) is the single most important hyperparameter — too large causes divergence, too small causes slow convergence.
- Gradient descent guarantees convergence to a global minimum **only** when the function is convex.
- The negative gradient is orthogonal to level sets (contour lines) of the function.
- For convex functions, local minima = global minima; for non-convex functions (neural networks), gradient descent may converge to local minima or saddle points.
- Lipschitz continuity of the gradient is the standard smoothness assumption for convergence proofs.
- Barzilai-Borwein and Wolfe conditions are two standard approaches to adaptive step size selection.
- SGD is the extension of gradient descent that makes deep network training practical by using mini-batch gradient approximations.
- Cauchy (1847) originated gradient descent; Curry (1944) first studied convergence for non-linear problems.
- Line search (exact or backtracking) is the classical approach to finding a good step size at each iteration.

---

I wasn't able to write this to `entries/2026/06/21/wiki-Gradient_descent.md` due to permission restrictions. The full entry content is above — you can approve the write or save it manually.
