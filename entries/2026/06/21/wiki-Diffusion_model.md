---
source: sources/wiki-Diffusion_model.md
source_url: https://en.wikipedia.org/wiki/Diffusion_model
---

I'll create an entry summarizing this diffusion models documentation.

## Diffusion Models: Generative Modeling via Iterative Denoising

Diffusion models are a class of latent variable generative models that learn to generate new data by modeling a diffusion process. The core idea: gradually corrupt data with noise (forward process) until it becomes pure Gaussian noise, then train a neural network to reverse this corruption (backward process). At generation time, start from random noise and iteratively denoise to produce realistic samples. Originally introduced in 2015 using non-equilibrium thermodynamics, they became practical with the DDPM paper in 2020 and now power commercial systems like Stable Diffusion and DALL-E.

## Key Concepts

- **Forward diffusion process**: A Markov chain that progressively adds Gaussian noise to data over T steps, controlled by a variance schedule beta_1, ..., beta_T in (0,1). The coefficients sqrt(1 - beta_t) and sqrt(beta_t) preserve unit variance across steps.
- **Reverse/backward diffusion process**: A learned neural network parameterized by theta that approximates the reverse of the forward process, predicting the mean mu_theta(x_t, t) and covariance Sigma_theta(x_t, t) at each step.
- **Noise schedule**: The sequence of beta_t values. Common choices include linear, cosine, and sigmoid schedules. The cumulative product alpha_bar_t = alpha_1 * ... * alpha_t determines signal-to-noise ratio at step t.
- **Reparameterization trick**: Because x_t | x_0 is Gaussian with mean sqrt(alpha_bar_t) * x_0 and variance sigma_t^2 * I, any intermediate noisy sample can be computed in one step directly from x_0 without iterating through all previous steps. This is critical for efficient training.
- **DDPM (Denoising Diffusion Probabilistic Model)**: The 2020 formulation (Ho et al.) that made diffusion models practical. Trains with variational inference, simplifying the loss to an MSE between predicted and actual noise (epsilon-prediction).
- **Score-based formulation**: Equivalent formulation where the model learns the score function (gradient of log probability density) rather than directly predicting noise. Connected to SDEs.
- **ELBO (Evidence Lower Bound)**: The training objective derived via variational inference. Decomposes into a reconstruction term, a prior matching term, and a sum of KL divergences between forward and reverse transition distributions.
- **Simplified loss (L_simple)**: Ho et al. showed that training with a simple noise-prediction MSE loss (ignoring weighting terms) works better in practice than the full variational bound.
- **Non-equilibrium thermodynamics motivation**: The data distribution is "out of equilibrium"; the forward process diffuses it toward the equilibrium Gaussian N(0, I), analogous to particles diffusing in a potential well V(x) = ||x||^2 / 2.
- **Backbone architectures**: The denoising network is typically a U-Net or Transformer. The model takes noisy input x_t and timestep t, and predicts the noise, the clean data x_0, or the score.
- **Latent diffusion models (LDM)**: Run diffusion in the latent space of a pretrained autoencoder rather than pixel space, dramatically reducing computational cost (used by Stable Diffusion).
- **Classifier-free guidance (CFG)**: A technique to improve conditional generation quality by interpolating between conditional and unconditional score estimates, controlled by a guidance scale parameter.

## Commands and Syntax

**Forward process sampling (one-step reparameterization)**:
```
x_t = sqrt(alpha_bar_t) * x_0 + sigma_t * epsilon
where epsilon ~ N(0, I)
```

**Reverse process sampling (DDPM)**:
```
x_{t-1} = mu_theta(x_t, t) + sigma_t * z
where z ~ N(0, I) for t > 1, z = 0 for t = 1
```

**Simplified training loss**:
```
L_simple = E_{t, x_0, epsilon} [ || epsilon - epsilon_theta(x_t, t) ||^2 ]
where x_t = sqrt(alpha_bar_t) * x_0 + sqrt(1 - alpha_bar_t) * epsilon
```

**Key notation**:
```
alpha_t     = 1 - beta_t
alpha_bar_t = product(alpha_1, ..., alpha_t)
sigma_t     = sqrt(1 - alpha_bar_t)
```

**Posterior mean (when x_0 is known)**:
```
mu_tilde_t(x_t, x_0) = [sqrt(alpha_t)(1 - alpha_bar_{t-1}) * x_t 
                       + sqrt(alpha_bar_{t-1})(1 - alpha_t) * x_0] / sigma_t^2
```

## Relationships

- **Variational autoencoders (VAEs)**: Diffusion models can be viewed as a hierarchical VAE with T latent layers, fixed encoder (forward process), and learned decoder (reverse process). The ELBO derivation follows the same logic.
- **Score matching / Langevin dynamics**: The score-based generative modeling framework (Song & Ermon) learns the score function nabla_x log p(x) and uses Langevin dynamics for sampling. Song et al. unified DDPM and score-based models under the SDE framework.
- **Stochastic differential equations (SDEs)**: The continuous-time limit of diffusion models is an SDE. The forward SDE has a corresponding reverse-time SDE that depends on the score function. This unification enables flexible samplers (probability flow ODE, various SDE solvers).
- **Normalizing flows**: Both are invertible generative models, but diffusion models relax the requirement for exact invertibility by using learned approximate inverses.
- **GANs**: Diffusion models offer more stable training and better mode coverage than GANs, at the cost of slower sampling (many iterative steps vs. single forward pass).
- **U-Net architecture**: The standard backbone for pixel-space diffusion models, using skip connections between encoder and decoder at matching resolutions.
- **Transformers**: Increasingly used as diffusion backbones (DiT - Diffusion Transformers), especially for large-scale models.
- **Non-equilibrium thermodynamics**: The theoretical foundation. Forward diffusion is analogous to physical diffusion toward thermal equilibrium; reverse diffusion requires learning the "thermodynamic force" that created the non-equilibrium state.
- **Text-to-image models**: Commercial diffusion systems (DALL-E, Stable Diffusion, Midjourney) combine diffusion models with text encoders (CLIP, T5) via cross-attention for text-conditioned generation.
- **Discrete diffusion models**: An extension that applies the diffusion framework to discrete data (text, categorical variables) using discrete corruption processes instead of Gaussian noise.

## Exam-Relevant Points

- The forward process requires **no learnable parameters** -- it is a fixed Markov chain defined by the noise schedule {beta_t}.
- The key insight enabling efficient training is that x_t can be sampled directly from x_0 in **one step** via x_t = sqrt(alpha_bar_t) * x_0 + sqrt(1 - alpha_bar_t) * epsilon, without computing intermediate steps.
- The **simplified loss** (L_simple) ignores the time-dependent weighting from the ELBO and uses uniform weighting across timesteps. Despite being a looser bound, it produces better sample quality empirically.
- The model can be parameterized to predict **noise (epsilon)**, **clean data (x_0)**, or **velocity (v)** -- these are mathematically equivalent but have different training dynamics.
- The posterior q(x_{t-1} | x_t, x_0) is **tractable** and Gaussian, which is what makes the KL divergence terms in the ELBO computable in closed form.
- Diffusion models were introduced in **2015** (Sohl-Dickstein et al.) but became practical with **DDPM in 2020** (Ho et al.).
- The variance of the reverse process can be **fixed** (set to beta_t or sigma_tilde_t^2) or **learned**. DDPM fixes it; later work (Improved DDPM, Nichol & Dhariwal 2021) learns it.
- The forward process converges to N(0, I) as T approaches infinity, provided alpha_bar_T approaches 0, meaning the signal is completely destroyed.
- **Classifier-free guidance** requires training the model with random dropout of the conditioning signal (e.g., text prompt dropped some fraction of the time), then using the difference between conditional and unconditional predictions at inference time.
- DDPM sampling requires **T forward passes** through the network (one per timestep), making it much slower than GANs. Accelerated samplers (DDIM, DPM-Solver) reduce this to 10-50 steps.
- The connection to **score matching**: the noise prediction network epsilon_theta is proportional to the negative score: epsilon_theta(x_t, t) is approximately equal to -sigma_t * nabla_{x_t} log p_t(x_t).
- **Latent diffusion** reduces computation by operating in a compressed latent space (e.g., 8x spatial downsampling), with a separate autoencoder handling pixel-space reconstruction.
