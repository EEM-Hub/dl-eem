---
source: sources/wiki-Generative_adversarial_network.md
source_url: https://en.wikipedia.org/wiki/Generative_adversarial_network
---

## Generative Adversarial Networks (GANs)

GANs are a class of deep learning frameworks where two neural networks — a generator and a discriminator — compete in a zero-sum game. Introduced by Ian Goodfellow et al. in 2014, the generator learns to produce synthetic data that matches the statistics of a training set, while the discriminator learns to distinguish real from generated samples. GANs are implicit generative models: they do not explicitly model the likelihood function.

## Key Concepts

- **Two-player zero-sum game**: The generator minimizes and the discriminator maximizes the same objective function L(G, D).
- **Generator**: Maps from a latent space (typically Gaussian or uniform noise z) through a function G to produce synthetic samples. Implemented as a pushforward measure μ_G = μ_Z ∘ G⁻¹. Often a deconvolutional neural network for images.
- **Discriminator**: Evaluates whether a sample is real or generated, outputting a value in [0,1]. Often a convolutional neural network for images. The optimal discriminator is always deterministic (proven via Jensen's inequality).
- **Implicit generative model**: GANs do not model the likelihood explicitly, unlike flow-based models or VAEs. Training is "indirect" — the generator is not trained to minimize distance to specific data points, but to fool the discriminator.
- **Latent space**: The generator is seeded with randomized input from a predefined distribution (e.g., multivariate normal).
- **Training**: Independent backpropagation applied to both networks alternately. The generator improves at producing realistic samples; the discriminator improves at detection.
- **Reparameterization trick**: Decomposing μ_G into μ_Z ∘ G⁻¹ avoids intractable probabilistic computations that plagued earlier generative models. Developed concurrently by Kingma & Welling (VAE) and Rezende et al.
- **Jensen-Shannon divergence**: The optimal discriminator's objective equals 2·D_JS(μ_ref; μ_G) − 2ln2, meaning training the generator effectively minimizes the JS divergence between generated and real distributions.
- **Optimal discriminator formula**: D*(x) = dμ_ref / d(μ_ref + μ_G) — the Radon-Nikodym derivative of the reference measure with respect to the mixture.
- **Asymptotic consistency**: Since neural networks are universal approximators, GANs are asymptotically consistent.

## Commands and Syntax

**GAN objective function (minimax formulation):**
```
min_G max_D L(G, D) = E_{x~μ_ref}[ln D(x)] + E_{z~μ_Z}[ln(1 - D(G(z)))]
```

**Training procedure:**
1. Sample a batch from the real data distribution μ_ref
2. Sample noise z from latent distribution μ_Z (e.g., standard normal)
3. Generate fake samples via G(z)
4. Train discriminator D to maximize L (classify real as 1, fake as 0)
5. Train generator G to minimize L (fool D into classifying G(z) as real)
6. Repeat with independent backpropagation for each network

## Relationships

- **vs. Variational Autoencoders (VAEs)**: Both use reparameterization; VAEs explicitly model likelihood, GANs do not. VAE universality unproven as of 2017.
- **vs. Flow-based models**: Flow models provide explicit density and invertible mappings; GANs lack both.
- **vs. Autoregressive models (WaveNet, PixelRNN)**: GANs generate complete samples in one pass; autoregressive models require sequential generation.
- **vs. Boltzmann machines / ICA**: GANs have no restrictions on network function type.
- **Game theory**: GAN training is formulated as a minimax game; equilibrium analysis involves Nash equilibrium, minimax theorem, and move-order considerations.
- **Applicable across learning paradigms**: Originally unsupervised, but proven useful for semi-supervised, fully supervised, and reinforcement learning.
- **Evolutionary biology analogy**: GANs mirror mimicry and evolutionary arms races.

## Exam-Relevant Points

- GANs were introduced by **Ian Goodfellow et al. in June 2014**.
- The GAN game is a **zero-sum game** — generator minimizes, discriminator maximizes the same objective.
- The generator maps from a **latent space** to the data space; the discriminator maps from data space to [0,1].
- The optimal discriminator computes a quantity related to the **Jensen-Shannon divergence** between real and generated distributions.
- GANs are **implicit generative models** — they do not explicitly model the likelihood function.
- The optimal discriminator strategy is always **deterministic** (proved via Jensen's inequality).
- For image generation: generator is typically **deconvolutional**, discriminator is typically **convolutional**.
- The **minimax theorem** applies only when strategy sets are finitely spanned; since GAN strategy sets are infinite, equilibrium analysis requires distinguishing between generator-first, discriminator-first, and Nash equilibria.
- For the original GAN game, all three equilibrium types **exist and are equal**, but this does not hold for all GAN variants.
- GANs are **asymptotically consistent** because neural networks are universal approximators.
- The reparameterization trick (μ_G = μ_Z ∘ G⁻¹) was developed concurrently with the **variational autoencoder** by Kingma & Welling.
