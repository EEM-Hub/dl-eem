---
source: sources/wiki-Autoencoder.md
source_url: https://en.wikipedia.org/wiki/Autoencoder
---

## Autoencoders: Architecture, Training, and Variants

Autoencoders are unsupervised neural networks that learn efficient data encodings by training two coupled functions: an encoder that compresses input into a lower-dimensional latent representation, and a decoder that reconstructs the original input from that representation. They are foundational to dimensionality reduction, feature learning, anomaly detection, and generative modeling.

## Key Concepts

- **Encoder-Decoder Architecture**: The encoder maps input space X (dimension m) to code space Z (dimension n), typically with m > n. The decoder maps back from Z to X. Both are usually implemented as multilayer perceptrons (MLPs).
- **Latent Space / Code**: The compressed intermediate representation z = E_φ(x), also called latent variable, latent vector, or latent representation.
- **Undercomplete Autoencoder**: Code dimension n < input dimension m, forcing the network to learn compressed representations rather than the identity function. This is the standard configuration.
- **Overcomplete Autoencoder**: Code dimension n ≥ m. Can learn the identity function (becoming useless), but experimental results show they can still learn useful features when properly regularized.
- **Reconstruction Loss**: Typically L2 (mean squared error) between input and reconstruction: L(θ,φ) = (1/N) Σ ||x_i - D_θ(E_φ(x_i))||². Optimized via gradient descent.
- **Training Objective**: Find parameters θ (decoder) and φ (encoder) that minimize expected reconstruction error over the reference data distribution.

## Variants

- **Variational Autoencoder (VAE)**: Uses variational Bayesian methods. The latent space is a mixture of distributions (not fixed vectors). The encoder outputs distribution parameters (mean and variance), and samples are drawn from this distribution during training. Enables principled generative modeling via p_θ(x) = ∫ p_θ(x,z) dz.
- **Sparse Autoencoder (SAE)**: Encourages most latent activations to be near zero. Two enforcement mechanisms:
  - **k-sparse**: Hard sparsity — only the top-k activations are kept, rest clamped to zero. Backpropagation sets gradients to zero for inactive units (generalized ReLU).
  - **Regularized sparsity**: Soft sparsity — adds a penalty term λ·L_sparse to the loss. The sparsity loss measures divergence between actual activation density ρ_k(x) and desired sparsity ρ̂_k using KL divergence, L1, or L2 distance.
- **Denoising Autoencoder**: Trained to reconstruct clean input from corrupted/noisy versions; learns robust features.
- **Contractive Autoencoder**: Adds a penalty on the Frobenius norm of the encoder's Jacobian, making the representation insensitive to small input variations.

## Commands and Syntax

**Basic autoencoder encoder (one-layer MLP)**:
```
E_φ(x) = σ(Wx + b)
```
where σ is an activation function, W is the weight matrix, b is the bias vector.

**Standard reconstruction loss (L2)**:
```
L(θ,φ) = (1/N) Σᵢ ||xᵢ - D_θ(E_φ(xᵢ))||²
```

**Sparse autoencoder total loss**:
```
min_{θ,φ} L(θ,φ) + λ·L_sparse(θ,φ)
```

**k-sparse function**:
```
f_k(x₁,...,xₙ) = (x₁b₁,...,xₙbₙ)
where bᵢ = 1 if |xᵢ| ranks in the top k, else 0
```

**KL divergence sparsity penalty**:
```
s(ρ, ρ̂) = ρ·log(ρ/ρ̂) + (1-ρ)·log((1-ρ)/(1-ρ̂))
```

## Relationships

- **Dimensionality Reduction**: Autoencoders perform nonlinear dimensionality reduction, generalizing PCA (which is equivalent to a linear autoencoder with L2 loss).
- **Generative Models**: VAEs connect autoencoders to generative modeling alongside GANs and diffusion models. An ideal undercomplete autoencoder's decoder can generate realistic samples by feeding arbitrary latent codes.
- **Sparse Coding / Neuroscience**: Sparse autoencoders are motivated by the sparse coding hypothesis from computational neuroscience.
- **Feature Learning**: Autoencoders learn representations useful as input features for downstream tasks (classification, clustering, anomaly detection).
- **Regularization Techniques**: Sparsity, denoising, and contractive penalties are regularization strategies that prevent trivial solutions and improve learned representations.
- **Variational Bayesian Methods**: VAEs bridge autoencoders and probabilistic inference, connecting to the broader framework of latent variable models.

## Exam-Relevant Points

- The encoder maps X → Z, the decoder maps Z → X; typically dim(Z) < dim(X) for undercomplete autoencoders.
- Autoencoders are **unsupervised** — they learn from unlabeled data by reconstructing their own input.
- An overcomplete autoencoder (dim(Z) ≥ dim(X)) can learn the identity function, making regularization essential.
- VAEs model the latent space as distributions (not point vectors), enabling sampling and generation; they optimize a variational lower bound (ELBO).
- k-sparse autoencoders use hard top-k selection; regularized sparse autoencoders use a soft penalty (KL divergence, L1, or L2).
- Sparse autoencoders may have **more** hidden units than inputs — sparsity, not bottleneck width, prevents trivial solutions.
- The standard loss function is mean squared reconstruction error (L2 loss).
- Denoising autoencoders learn robust features by reconstructing clean inputs from corrupted ones.
- Contractive autoencoders penalize the Jacobian of the encoder, enforcing local invariance.
- Applications include: facial recognition, feature detection, anomaly detection, word embeddings, and synthetic data generation.
