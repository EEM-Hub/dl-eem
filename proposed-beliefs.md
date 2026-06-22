# Proposed Beliefs

Review each entry: change `[ACCEPT]` to `[ACCEPT]` to keep, or vice versa.
Then run: `expert-build accept-beliefs`

---

**Generated:** 2026-06-21
**Source:** 20 entries from entries/
**Model:** claude

### [ACCEPT] nonlinear-activation-enables-universal-approximation
A two-layer neural network with a nonlinear activation function is a universal function approximator (Cybenko 1989 for sigmoid)
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] linear-activation-collapses-to-single-layer
A multi-layer network using only identity (linear) activation functions across all layers is equivalent to a single-layer model
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] saturating-activation-gradient-approaches-zero
A saturating activation function has gradient approaching 0 as |v| approaches infinity (e.g., sigmoid, tanh); nonsaturating functions like ReLU do not
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] relu-not-continuously-differentiable
ReLU (max(0,x)) has C⁰ continuity (not continuously differentiable) but is the most widely used activation function in practice
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] sigmoid-derivative-formula
The sigmoid derivative is σ(x)(1−σ(x)); the tanh derivative is 1−tanh²(x)
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] gelu-definition-gaussian-cdf
GELU is defined as x·Φ(x) where Φ is the standard Gaussian CDF; used in BERT (2018) and GPT
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] softplus-derivative-is-sigmoid
Softplus (ln(1+eˣ)) is a smooth approximation of ReLU and its derivative is the sigmoid function
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] selu-fixed-parameters-self-normalizing
SELU has fixed parameters λ=1.0507 and α=1.67326 derived to maintain mean 0 and variance 1 across layers without explicit normalization
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] three-categories-activation-functions
Activation functions fall into three categories: ridge functions (act on linear combination of inputs, e.g. ReLU, sigmoid), radial functions (depend on distance from center, e.g. Gaussian RBF), and fold functions (aggregate over inputs, e.g. softmax, max)
- Source: entries/2026/06/21/wiki-Activation_function.md
- Source URL: https://en.wikipedia.org/wiki/Activation_function

### [ACCEPT] deep-network-requires-two-hidden-layers
A neural network with at least two hidden layers is called a 'deep' neural network
- Source: entries/2026/06/21/wiki-Artificial_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Artificial_neural_network

### [ACCEPT] backprop-history-chain
Backpropagation attribution chain: Leibniz (chain rule, 1673) → Kelley (control theory, 1960) → Linnainmaa (modern form, 1970) → Werbos (applied to NNs, 1982) → Rumelhart et al. (popularized, 1986)
- Source: entries/2026/06/21/wiki-Artificial_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Artificial_neural_network

### [ACCEPT] first-deep-learning-algorithm-gmdh-1965
The first deep learning algorithm was GMDH by Ivakhnenko & Lapa (1965); a 1971 paper trained 8 layers deep
- Source: entries/2026/06/21/wiki-Artificial_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Artificial_neural_network

### [ACCEPT] cnn-lineage-neocognitron-to-alexnet
CNN lineage: Neocognitron (Fukushima 1979) → TDNN (Waibel 1987) → LeNet (LeCun 1989) → AlexNet (Krizhevsky/Sutskever/Hinton 2012)
- Source: entries/2026/06/21/wiki-Artificial_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Artificial_neural_network

### [ACCEPT] vanishing-gradient-identified-hochreiter-1991
The vanishing gradient problem was identified by Hochreiter (1991) and addressed by LSTM, with the critical forget gate added in 1999
- Source: entries/2026/06/21/wiki-Artificial_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Artificial_neural_network

### [ACCEPT] alexnet-2012-catalyzed-deep-learning-era
AlexNet (2012) won ImageNet by a large margin over shallow methods, catalyzing the modern deep learning era
- Source: entries/2026/06/21/wiki-Artificial_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Artificial_neural_network

### [ACCEPT] minsky-papert-perceptrons-1969-ai-winter
Minsky & Papert's Perceptrons (1969) showed single-layer perceptrons cannot solve XOR, causing the first AI winter for neural networks
- Source: entries/2026/06/21/wiki-Artificial_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Artificial_neural_network

### [ACCEPT] scaled-dot-product-attention-formula
Scaled dot-product attention: Attention(Q,K,V) = softmax(QK^T / sqrt(d_k)) V, where scaling by sqrt(d_k) prevents softmax saturation
- Source: entries/2026/06/21/wiki-Attention_machine_learning.md
- Source URL: https://en.wikipedia.org/wiki/Attention_(machine_learning)

### [ACCEPT] attention-matrix-quadratic-complexity
The attention matrix has O(n²) complexity in sequence length, which is the primary scalability bottleneck of Transformers
- Source: entries/2026/06/21/wiki-Attention_machine_learning.md
- Source URL: https://en.wikipedia.org/wiki/Attention_(machine_learning)

### [ACCEPT] self-attention-introduced-transformer-2017
Self-attention was introduced in the 2017 Transformer paper ('Attention Is All You Need'); earlier attention (Bahdanau 2014) was cross-attention between encoder and decoder
- Source: entries/2026/06/21/wiki-Attention_machine_learning.md
- Source URL: https://en.wikipedia.org/wiki/Attention_(machine_learning)

### [ACCEPT] flash-attention-exact-not-approximation
Flash Attention reduces attention memory from O(n²) to O(n) by tiling computation into GPU SRAM-sized blocks; it is exact, not an approximation
- Source: entries/2026/06/21/wiki-Attention_machine_learning.md
- Source URL: https://en.wikipedia.org/wiki/Attention_(machine_learning)

### [ACCEPT] bahdanau-additive-vs-luong-multiplicative-attention
Bahdanau (additive) attention uses a learned feedforward network for alignment scores; Luong (multiplicative) attention uses dot products
- Source: entries/2026/06/21/wiki-Attention_machine_learning.md
- Source URL: https://en.wikipedia.org/wiki/Attention_(machine_learning)

### [ACCEPT] attention-output-convex-hull-of-values
Each attention output row is a convex combination of the value vectors, so the output is confined to the convex hull of V's rows
- Source: entries/2026/06/21/wiki-Attention_machine_learning.md
- Source URL: https://en.wikipedia.org/wiki/Attention_(machine_learning)

### [ACCEPT] attention-maps-not-reliable-explanations
Attention maps do not reliably explain model decisions — higher attention scores do not always correlate with greater impact on output
- Source: entries/2026/06/21/wiki-Attention_machine_learning.md
- Source URL: https://en.wikipedia.org/wiki/Attention_(machine_learning)

### [ACCEPT] autoencoder-unsupervised-encoder-decoder
Autoencoders are unsupervised neural networks with an encoder (X→Z) and decoder (Z→X); standard (undercomplete) configuration has dim(Z) < dim(X)
- Source: entries/2026/06/21/wiki-Autoencoder.md
- Source URL: https://en.wikipedia.org/wiki/Autoencoder

### [ACCEPT] vae-latent-distributions-not-point-vectors
Variational autoencoders model the latent space as distributions (outputting mean and variance parameters), not point vectors, enabling sampling and generation via a variational lower bound (ELBO)
- Source: entries/2026/06/21/wiki-Autoencoder.md
- Source URL: https://en.wikipedia.org/wiki/Autoencoder

### [ACCEPT] sparse-autoencoder-k-sparse-vs-regularized
Sparse autoencoders use either hard sparsity (k-sparse: keep only top-k activations) or soft sparsity (penalty term using KL divergence, L1, or L2)
- Source: entries/2026/06/21/wiki-Autoencoder.md
- Source URL: https://en.wikipedia.org/wiki/Autoencoder

### [ACCEPT] linear-autoencoder-equivalent-to-pca
A linear autoencoder with L2 loss is equivalent to PCA; autoencoders generalize PCA to nonlinear dimensionality reduction
- Source: entries/2026/06/21/wiki-Autoencoder.md
- Source URL: https://en.wikipedia.org/wiki/Autoencoder

### [ACCEPT] denoising-autoencoder-reconstructs-from-corrupted
Denoising autoencoders learn robust features by training to reconstruct clean input from corrupted/noisy versions
- Source: entries/2026/06/21/wiki-Autoencoder.md
- Source URL: https://en.wikipedia.org/wiki/Autoencoder

### [ACCEPT] contractive-autoencoder-jacobian-penalty
Contractive autoencoders add a penalty on the Frobenius norm of the encoder's Jacobian, enforcing local invariance to small input perturbations
- Source: entries/2026/06/21/wiki-Autoencoder.md
- Source URL: https://en.wikipedia.org/wiki/Autoencoder

### [ACCEPT] rnn-maintains-hidden-state-across-timesteps
Recurrent neural networks maintain a hidden state that is updated at each time step based on current input and previous hidden state, enabling temporal dependency capture.
- Source: entries/2026/06/21/wiki-Recurrent_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Recurrent_neural_network

### [ACCEPT] rnn-vanishing-gradient-limits-long-range
Traditional RNNs cannot learn long-range dependencies because gradients shrink exponentially during backpropagation through time (the vanishing gradient problem).
- Source: entries/2026/06/21/wiki-Recurrent_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Recurrent_neural_network

### [ACCEPT] lstm-invented-1997-hochreiter-schmidhuber
LSTM (Long Short-Term Memory) was invented by Hochreiter & Schmidhuber (1995/1997) and uses gating mechanisms to preserve gradients over long sequences, solving the vanishing gradient problem.
- Source: entries/2026/06/21/wiki-Recurrent_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Recurrent_neural_network

### [ACCEPT] bidirectional-rnn-requires-full-sequence
Bidirectional RNNs require the full input sequence upfront and cannot be used for real-time or streaming processing, unlike standard unidirectional RNNs.
- Source: entries/2026/06/21/wiki-Recurrent_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Recurrent_neural_network

### [ACCEPT] seq2seq-encoder-decoder-dominated-mt-2014-2017
The encoder-decoder (seq2seq) RNN architecture was state-of-the-art for machine translation from 2014 to 2017 and led directly to attention mechanisms and transformers.
- Source: entries/2026/06/21/wiki-Recurrent_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Recurrent_neural_network

### [ACCEPT] elman-vs-jordan-context-units
Elman networks feed hidden layer values to context units, while Jordan networks feed output layer values to context units with self-recurrent connections; both are called Simple Recurrent Networks (SRN).
- Source: entries/2026/06/21/wiki-Recurrent_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Recurrent_neural_network

### [ACCEPT] hopfield-network-content-addressable-memory
Hopfield networks are RNNs with equal-weight connections that converge to stable states, functioning as content-addressable memory using Hebbian learning, rooted in the Ising model from statistical mechanics.
- Source: entries/2026/06/21/wiki-Recurrent_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Recurrent_neural_network

### [ACCEPT] l1-regularization-induces-sparsity
L1 (LASSO) regularization penalizes absolute weight values and drives weights exactly to zero, inducing sparsity; it is the convex relaxation of the NP-hard L0 regularization problem.
- Source: entries/2026/06/21/wiki-Regularization_mathematics.md
- Source URL: https://en.wikipedia.org/wiki/Regularization_(mathematics)

### [ACCEPT] l2-regularization-small-nonzero-weights
L2 (Ridge/Tikhonov) regularization penalizes squared magnitude of weights, producing small but non-zero weights; its closed-form solution is w = (X^T X + λnI)^{-1}(X^T Y).
- Source: entries/2026/06/21/wiki-Regularization_mathematics.md
- Source URL: https://en.wikipedia.org/wiki/Regularization_(mathematics)

### [ACCEPT] elastic-net-combines-l1-l2
Elastic net regularization combines L1 and L2 penalties with mixing parameter α ∈ [0,1], resolving L1's non-uniqueness problem while preserving sparsity.
- Source: entries/2026/06/21/wiki-Regularization_mathematics.md
- Source URL: https://en.wikipedia.org/wiki/Regularization_(mathematics)

### [ACCEPT] early-stopping-equivalent-to-l2-regularization
Early stopping in gradient descent is mathematically related to L2 regularization — limiting iterations T controls effective model complexity analogously to 1/λ.
- Source: entries/2026/06/21/wiki-Regularization_mathematics.md
- Source URL: https://en.wikipedia.org/wiki/Regularization_(mathematics)

### [ACCEPT] bayesian-interpretation-l2-gaussian-l1-laplace
L2 regularization corresponds to a Gaussian prior on weights and L1 corresponds to a Laplace prior; the regularized solution approximates the MAP (maximum a posteriori) estimate.
- Source: entries/2026/06/21/wiki-Regularization_mathematics.md
- Source URL: https://en.wikipedia.org/wiki/Regularization_(mathematics)

### [ACCEPT] dropout-rate-typically-0.5-hidden-layers
Dropout rate is typically 0.5 for hidden layers; it simulates training an exponential number of sub-networks and approximates ensemble methods.
- Source: entries/2026/06/21/wiki-Regularization_mathematics.md
- Source URL: https://en.wikipedia.org/wiki/Regularization_(mathematics)

### [ACCEPT] early-stopping-requires-three-datasets
Early stopping requires three separate datasets: training (fit model), validation (monitor for stopping criterion), and test (final evaluation) — the test set must never be used for stopping decisions.
- Source: entries/2026/06/21/wiki-Regularization_mathematics.md
- Source URL: https://en.wikipedia.org/wiki/Regularization_(mathematics)

### [ACCEPT] rl-three-ml-paradigms
Reinforcement learning is one of three machine learning paradigms alongside supervised learning (labeled data) and unsupervised learning (unlabeled data); RL learns through interaction with an environment.
- Source: entries/2026/06/21/wiki-Reinforcement_learning.md
- Source URL: https://en.wikipedia.org/wiki/Reinforcement_learning

### [ACCEPT] mdp-four-components
A Markov decision process (MDP) is defined by four components: state space S, action space A, transition probabilities P_a(s,s'), and reward function R_a(s,s').
- Source: entries/2026/06/21/wiki-Reinforcement_learning.md
- Source URL: https://en.wikipedia.org/wiki/Reinforcement_learning

### [ACCEPT] knowing-q-star-sufficient-optimal-action
Knowing the optimal action-value function Q*(s,a) alone is sufficient to act optimally — the agent simply chooses argmax_a Q*(s,a) at each state without needing an environment model.
- Source: entries/2026/06/21/wiki-Reinforcement_learning.md
- Source URL: https://en.wikipedia.org/wiki/Reinforcement_learning

### [ACCEPT] rl-discount-factor-gamma-less-than-one
The RL discount factor γ must satisfy 0 ≤ γ < 1 to ensure convergence of infinite-horizon discounted returns G = Σ γ^t R_{t+1}.
- Source: entries/2026/06/21/wiki-Reinforcement_learning.md
- Source URL: https://en.wikipedia.org/wiki/Reinforcement_learning

### [ACCEPT] rl-optimal-policy-deterministic-stationary
In RL, optimal policies can always be found among deterministic stationary policies — there is no loss of generality from restricting the search to policies that depend only on current state.
- Source: entries/2026/06/21/wiki-Reinforcement_learning.md
- Source URL: https://en.wikipedia.org/wiki/Reinforcement_learning

### [ACCEPT] epsilon-greedy-exploration
ε-greedy exploration selects the best-known action with probability (1-ε) and a random action with probability ε, providing the simplest practical method for balancing exploration and exploitation.
- Source: entries/2026/06/21/wiki-Reinforcement_learning.md
- Source URL: https://en.wikipedia.org/wiki/Reinforcement_learning

### [ACCEPT] transfer-learning-first-paper-1976
The first neural network transfer learning paper was by Bozinovski and Fulgosi in 1976.
- Source: entries/2026/06/21/wiki-Transfer_learning.md
- Source URL: https://en.wikipedia.org/wiki/Transfer_learning

### [ACCEPT] transfer-learning-domain-feature-space-plus-distribution
In transfer learning, a domain is formally defined as a feature space X plus a marginal probability distribution P(X); a task is defined as a label space Y plus a predictive function f: X → Y.
- Source: entries/2026/06/21/wiki-Transfer_learning.md
- Source URL: https://en.wikipedia.org/wiki/Transfer_learning

### [ACCEPT] negative-transfer-possible
Negative transfer occurs when source knowledge hurts target task performance; experimentally demonstrated as early as 1981 with letter recognition datasets.
- Source: entries/2026/06/21/wiki-Transfer_learning.md
- Source URL: https://en.wikipedia.org/wiki/Transfer_learning

### [ACCEPT] pretraining-can-hurt-accuracy-zoph-2020
Zoph et al. (2020) demonstrated that pre-training can reduce accuracy in some settings, advocating self-training as an alternative to transfer learning via pre-training.
- Source: entries/2026/06/21/wiki-Transfer_learning.md
- Source URL: https://en.wikipedia.org/wiki/Transfer_learning

### [ACCEPT] transformer-attention-is-all-you-need-2017
The transformer architecture was introduced in the 2017 paper 'Attention Is All You Need' by Google researchers, with the original model having approximately 100M parameters.
- Source: entries/2026/06/21/wiki-Transformer_deep_learning_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

### [ACCEPT] self-attention-permutation-invariant
Self-attention is permutation-invariant — it has no inherent notion of token order, so transformers must inject positional information via positional encodings or learned positional embeddings.
- Source: entries/2026/06/21/wiki-Transformer_deep_learning_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

### [ACCEPT] transformer-quadratic-context-window
Transformer computation scales quadratically with context window size (due to self-attention over all token pairs), compared to linear scaling for RNNs which process sequentially.
- Source: entries/2026/06/21/wiki-Transformer_deep_learning_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

### [ACCEPT] bert-encoder-only-gpt-decoder-only-t5-encoder-decoder
BERT uses encoder-only architecture (masked language modeling), GPT uses decoder-only (autoregressive generation), and T5 uses encoder-decoder (prefixLM) — the three main transformer variants.
- Source: entries/2026/06/21/wiki-Transformer_deep_learning_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

### [ACCEPT] pre-ln-vs-post-ln-transformer
Pre-layer-normalization (applying LayerNorm before attention/FFN) stabilizes transformer training and eliminates the need for learning rate warmup; the original 2017 paper used post-LN, but pre-LN is now standard.
- Source: entries/2026/06/21/wiki-Transformer_deep_learning_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

### [ACCEPT] masked-lm-vs-masked-attention-different-concepts
'Masked' in masked language modeling (randomly hiding tokens for prediction) is not the same as 'masked' in masked/causal attention (preventing visibility of future tokens during autoregressive generation).
- Source: entries/2026/06/21/wiki-Transformer_deep_learning_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

### [ACCEPT] transformer-pretrain-finetune-paradigm
The standard transformer training paradigm is self-supervised pretraining on large unlabeled corpora followed by supervised fine-tuning on task-specific labeled data.
- Source: entries/2026/06/21/wiki-Transformer_deep_learning_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)

### [ACCEPT] gan-introduced-goodfellow-2014
Generative adversarial networks (GANs) were introduced by Ian Goodfellow et al. in June 2014
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-two-player-zero-sum-game
GANs are formulated as a two-player zero-sum game where the generator minimizes and the discriminator maximizes the same objective function L(G, D)
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-implicit-generative-model
GANs are implicit generative models that do not explicitly model the likelihood function, unlike VAEs and flow-based models
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-minimax-objective
The GAN minimax objective is min_G max_D L(G,D) = E_{x~μ_ref}[ln D(x)] + E_{z~μ_Z}[ln(1 - D(G(z)))]
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-optimal-discriminator-js-divergence
The optimal GAN discriminator's objective equals 2·D_JS(μ_ref; μ_G) − 2ln2, meaning generator training effectively minimizes the Jensen-Shannon divergence between generated and real distributions
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-optimal-discriminator-deterministic
The optimal GAN discriminator strategy is always deterministic, proven via Jensen's inequality
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-asymptotically-consistent
GANs are asymptotically consistent because neural networks are universal approximators
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-reparameterization-concurrent-vae
The reparameterization trick (μ_G = μ_Z ∘ G⁻¹) was developed concurrently by Kingma & Welling (VAE) and Rezende et al.
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gan-generator-deconv-discriminator-conv
For image generation GANs, the generator is typically a deconvolutional neural network and the discriminator is typically a convolutional neural network
- Source: entries/2026/06/21/wiki-Generative_adversarial_network.md
- Source URL: https://en.wikipedia.org/wiki/Generative_adversarial_network

### [ACCEPT] gradient-descent-update-rule
The gradient descent update rule is x_{n+1} = x_n - η·∇f(x_n), where η is the learning rate (step size)
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] gradient-descent-cauchy-1847
Gradient descent was originated by Cauchy in 1847 and independently proposed by Hadamard in 1907
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] gradient-descent-convex-global-minimum
Gradient descent guarantees convergence to a global minimum only when the objective function is convex (where all local minima are global minima)
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] gradient-descent-negative-gradient-orthogonal-level-sets
The negative gradient is orthogonal to level sets (contour lines) of the function, always pointing in the direction of steepest local decrease
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] gradient-descent-saddle-point-problem
Gradient descent can get stuck at saddle points (not just local minima), which is a significant concern in high-dimensional optimization
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] gradient-descent-lipschitz-convergence
Lipschitz continuity of the gradient is the standard smoothness assumption for gradient descent convergence proofs
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] gradient-descent-monotonic-decrease
For sufficiently small learning rate η, gradient descent guarantees monotonic decrease: f(x_{n+1}) ≤ f(x_n)
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] barzilai-borwein-adaptive-step-size
The Barzilai-Borwein method computes adaptive step sizes from consecutive gradient differences: η_n = |δx^T·δg| / ||δg||²
- Source: entries/2026/06/21/wiki-Gradient_descent.md
- Source URL: https://en.wikipedia.org/wiki/Gradient_descent

### [ACCEPT] lstm-three-gates-architecture
LSTM networks use three sigmoid gates: forget gate (discard old info), input gate (store new info), and output gate (expose cell state)
- Source: entries/2026/06/21/wiki-Long_short-term_memory.md
- Source URL: https://en.wikipedia.org/wiki/Long_short-term_memory

### [ACCEPT] lstm-cell-state-update-equation
The LSTM cell state update equation is c_t = f_t ⊙ c_{t-1} + i_t ⊙ c̃_t, combining gated previous state with gated candidate values
- Source: entries/2026/06/21/wiki-Long_short-term_memory.md
- Source URL: https://en.wikipedia.org/wiki/Long_short-term_memory

### [ACCEPT] lstm-forget-gate-added-2000
The LSTM forget gate was added by Gers et al. in 2000, not present in the original 1997 LSTM paper by Hochreiter & Schmidhuber
- Source: entries/2026/06/21/wiki-Long_short-term_memory.md
- Source URL: https://en.wikipedia.org/wiki/Long_short-term_memory

### [ACCEPT] lstm-solves-vanishing-not-exploding-gradients
LSTM solves the vanishing gradient problem but does NOT solve the exploding gradient problem
- Source: entries/2026/06/21/wiki-Long_short-term_memory.md
- Source URL: https://en.wikipedia.org/wiki/Long_short-term_memory

### [ACCEPT] lstm-peephole-variant
Peephole LSTM is a variant where gates can directly access the cell state, unlike standard LSTM where gates only see the hidden state
- Source: entries/2026/06/21/wiki-Long_short-term_memory.md
- Source URL: https://en.wikipedia.org/wiki/Long_short-term_memory

### [ACCEPT] squared-loss-minimizer-is-mean
The minimizer of squared (quadratic) loss is the mean; the minimizer of absolute loss is the median
- Source: entries/2026/06/21/wiki-Loss_function.md
- Source URL: https://en.wikipedia.org/wiki/Loss_function

### [ACCEPT] risk-function-is-expected-loss
The risk function R(θ, δ) = E_θ[L(θ, δ(X))] is the expected value of the loss function, bridging single-observation loss to a statistical estimation criterion
- Source: entries/2026/06/21/wiki-Loss_function.md
- Source URL: https://en.wikipedia.org/wiki/Loss_function

### [ACCEPT] mse-minimized-by-posterior-mean
Mean squared error (MSE) is the risk function under quadratic loss and is minimized by the posterior mean estimator
- Source: entries/2026/06/21/wiki-Loss_function.md
- Source URL: https://en.wikipedia.org/wiki/Loss_function

### [ACCEPT] minimax-decision-rule-definition
The minimax decision rule argmin_δ max_{θ∈Θ} R(θ, δ) chooses the decision rule with the lowest worst-case risk across all parameter values
- Source: entries/2026/06/21/wiki-Loss_function.md
- Source URL: https://en.wikipedia.org/wiki/Loss_function

### [ACCEPT] quadratic-loss-sensitive-to-outliers
Quadratic (squared error) loss is sensitive to outliers because squaring amplifies large errors; Huber loss and log-cosh are robust alternatives
- Source: entries/2026/06/21/wiki-Loss_function.md
- Source URL: https://en.wikipedia.org/wiki/Loss_function

### [ACCEPT] zero-one-loss-equals-hamming-distortion
The 0-1 loss function (0 for correct, 1 for incorrect classification) is equivalent to Hamming distortion in information theory
- Source: entries/2026/06/21/wiki-Loss_function.md
- Source URL: https://en.wikipedia.org/wiki/Loss_function

### [ACCEPT] nas-three-components
Neural Architecture Search (NAS) is defined by three components: search space, search strategy, and performance estimation strategy
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] nas-subfield-of-automl
NAS is a subfield of Automated Machine Learning (AutoML), closely related to hyperparameter optimization and meta-learning
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] nasnet-cell-transfer-paradigm
NASNet introduced the cell transfer paradigm: learn architecture cells on small datasets (CIFAR-10), then stack with separate parameters for large datasets (ImageNet), achieving 82.7% top-1 ImageNet accuracy with 28% fewer FLOPS than hand-designed architectures
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] enas-1000x-cost-reduction
Efficient NAS (ENAS) reduces NAS compute cost by 1000x compared to standard NAS through parameter sharing across child models
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] darts-differentiable-nas-skip-collapse
DARTS uses continuous relaxation of discrete search space for gradient-based NAS but suffers from performance collapse due to skip-connection aggregation, addressed by Hessian-norm regularization
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] evolutionary-vs-rl-nas-comparable
On CIFAR-10 and ImageNet, evolutionary NAS and RL-based NAS performed comparably, both slightly outperforming random search
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] nas-supernet-weight-sharing-few-gpu-days
One-shot supernet models use weight sharing to reduce NAS search cost from thousands of GPU-days to a few GPU-days by training a single overparameterized supernetwork whose subgraphs represent candidate architectures
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] nas-normal-vs-reduction-cells
In NAS cell-based search spaces, normal cells return feature maps of the same spatial dimensions while reduction cells halve height and width using stride 2
- Source: entries/2026/06/21/wiki-Neural_architecture_search.md
- Source URL: https://en.wikipedia.org/wiki/Neural_architecture_search

### [ACCEPT] batchnorm-normalizes-per-dimension-across-minibatch
Batch normalization computes mean and variance per feature dimension independently across the mini-batch, not jointly across dimensions.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] batchnorm-learnable-gamma-beta-restore-capacity
After normalization, batch norm applies learnable parameters gamma (scale) and beta (shift) via y = gamma * x_hat + beta, which can undo the normalization entirely if optimal, preserving the network's representational capacity.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] batchnorm-training-vs-inference-statistics
During training, batch normalization uses mini-batch statistics (mean and variance); during inference, it uses population statistics accumulated as running averages during training, making inference deterministic.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] batchnorm-population-variance-bessel-correction
Batch normalization computes population variance with Bessel's correction: multiplying by m/(m-1) for unbiased variance estimation from mini-batch statistics.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] batchnorm-ics-explanation-challenged
The original 'internal covariate shift' explanation for batch normalization's effectiveness has been empirically challenged; experiments adding explicit covariate shift noise to batch-normed networks showed no performance degradation, suggesting loss landscape smoothing is the actual mechanism.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] batchnorm-inference-collapses-to-linear-transform
At inference time, batch normalization collapses to a fixed linear transformation since all statistics and parameters are frozen.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] batchnorm-introduces-minibatch-dependencies
Batch normalization introduces statistical dependencies between elements in a mini-batch (they share mean/variance), breaking the iid assumption and potentially degrading gradient estimation quality.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] batchnorm-ioffe-szegedy-2015
Batch normalization was introduced by Ioffe and Szegedy in 2015.
- Source: entries/2026/06/21/wiki-Batch_normalization.md
- Source URL: https://en.wikipedia.org/wiki/Batch_normalization

### [ACCEPT] cnn-weight-sharing-parameter-reduction
A 5x5 convolutional kernel requires only 25 learnable weights per filter, versus 10,000 weights per neuron for a fully connected layer on a 100x100 image.
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] cnn-translation-equivariant-not-invariant
CNNs are translation-equivariant (feature maps shift correspondingly when input shifts) but generally NOT truly translation-invariant due to downsampling/pooling operations.
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] cnn-convolution-is-actually-cross-correlation
Most CNN implementations perform cross-correlation rather than true mathematical convolution; the distinction does not affect learned results since weights are learned.
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] depthwise-separable-convolution-decomposition
Depthwise separable convolution decomposes standard convolution into a depthwise convolution (spatial, per-channel) followed by a pointwise 1x1 convolution (cross-channel).
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] transpose-convolution-checkerboard-artifacts
Transpose convolution (deconvolution) multiplies by the transpose of the convolution matrix and can produce checkerboard artifacts, fixable by using upscale-then-convolve instead.
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] neocognitron-introduced-conv-and-pooling-layers-1980
Fukushima's Neocognitron (1980) introduced the two fundamental CNN layer types: convolutional (S-layer) and pooling (C-layer), using unsupervised/local learning rather than backpropagation.
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] lenet5-first-commercial-cnn-1995
LeNet-5 (1995, LeCun) was a 7-layer CNN for handwritten digit classification and the first commercially deployed CNN, used in NCR banking systems starting 1996.
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] tdnn-first-cnn-weight-sharing-plus-backprop-1987
The Time Delay Neural Network (TDNN, Waibel 1987) was the first CNN to combine weight sharing with backpropagation training.
- Source: entries/2026/06/21/wiki-Convolutional_neural_network.md
- Source URL: https://en.wikipedia.org/wiki/Convolutional_neural_network

### [ACCEPT] deep-learning-cap-depth-greater-than-2
In deep learning, 'deep' refers to the depth of the Credit Assignment Path (CAP); CAP depth > 2 is generally considered deep, though no universal threshold exists.
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] universal-approximation-depth-2-sufficient
The Universal Approximation Theorem states that a network with CAP depth of 2 can emulate any function, but deeper models extract better features in practice.
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] relu-network-width-greater-than-input-dimension
A deep ReLU network is a universal approximator only if its width is strictly greater than the input dimension (Lu et al.).
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] lstm-1995-forget-gate-1999
LSTM was published in 1995 by Hochreiter and Schmidhuber to address the vanishing gradient problem; the forget gate was added in 1999, completing the modern LSTM architecture.
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] backpropagation-history-linnainmaa-1970
The modern form of backpropagation was formulated by Linnainmaa in 1970, applied to neural networks by Werbos in 1982, and popularized by Rumelhart et al. in 1986.
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] gmdh-first-deep-learning-algorithm-1965
The Group Method of Data Handling (GMDH, Ivakhnenko and Lapa, 1965) was the first working deep learning algorithm, predating backpropagation-based methods.
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] relu-introduced-fukushima-1969
The ReLU activation function was introduced by Fukushima in 1969, much earlier than its widespread popularization in deep learning.
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] deep-belief-networks-layer-by-layer-rbm-2006
Deep belief networks (Hinton et al., 2006) consist of stacked restricted Boltzmann machines trained layer-by-layer, optionally fine-tuned with backpropagation.
- Source: entries/2026/06/21/wiki-Deep_learning.md
- Source URL: https://en.wikipedia.org/wiki/Deep_learning

### [ACCEPT] diffusion-forward-process-no-learnable-params
The forward diffusion process requires no learnable parameters — it is a fixed Markov chain defined by the noise schedule {beta_t}.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] diffusion-one-step-sampling-reparameterization
Any intermediate noisy sample x_t can be computed in one step from x_0 via x_t = sqrt(alpha_bar_t) * x_0 + sqrt(1 - alpha_bar_t) * epsilon, without iterating through all previous steps, enabling efficient training.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] ddpm-simplified-loss-better-than-elbo
DDPM's simplified loss (L_simple) uses uniform-weighted MSE between predicted and actual noise, ignoring time-dependent ELBO weighting; despite being a looser bound, it produces better sample quality empirically.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] diffusion-model-parameterization-equivalence
Diffusion models can be parameterized to predict noise (epsilon), clean data (x_0), or velocity (v) — these are mathematically equivalent but have different training dynamics.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] diffusion-introduced-2015-practical-ddpm-2020
Diffusion models were introduced in 2015 (Sohl-Dickstein et al.) using non-equilibrium thermodynamics but became practical with DDPM in 2020 (Ho et al.).
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] classifier-free-guidance-requires-conditioning-dropout
Classifier-free guidance requires training the diffusion model with random dropout of the conditioning signal (e.g., text prompt dropped some fraction of the time), then using the difference between conditional and unconditional predictions at inference.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] ddpm-sampling-requires-t-forward-passes
DDPM sampling requires T forward passes through the network (one per timestep), making it much slower than GANs; accelerated samplers like DDIM and DPM-Solver reduce this to 10-50 steps.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] latent-diffusion-operates-in-compressed-space
Latent diffusion models run diffusion in the latent space of a pretrained autoencoder (e.g., 8x spatial downsampling) rather than pixel space, with a separate autoencoder handling pixel-space reconstruction, dramatically reducing computational cost.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] noise-prediction-proportional-to-negative-score
The noise prediction network epsilon_theta is proportional to the negative score function: epsilon_theta(x_t, t) ≈ -sigma_t * nabla_{x_t} log p_t(x_t), connecting DDPM and score-based generative models.
- Source: entries/2026/06/21/wiki-Diffusion_model.md
- Source URL: https://en.wikipedia.org/wiki/Diffusion_model

### [ACCEPT] dropout-training-only-not-inference
Dropout is applied only during training; at inference, all neurons are active with weights scaled by the keep probability P(c).
- Source: entries/2026/06/21/wiki-Dropout_neural_networks.md
- Source URL: https://en.wikipedia.org/wiki/Dropout_(neural_networks)

### [ACCEPT] dropout-zeros-neurons-dilution-zeros-weights
Dropout zeros entire neurons (whole rows of the weight matrix), while dilution zeros individual weights — these are distinct operations with different mathematical properties.
- Source: entries/2026/06/21/wiki-Dropout_neural_networks.md
- Source URL: https://en.wikipedia.org/wiki/Dropout_(neural_networks)

### [ACCEPT] dropout-prevents-co-adaptation-forces-redundancy
Dropout prevents co-adaptation of feature detectors by ensuring neurons cannot rely on specific other neurons being present, forcing redundant distributed representations.
- Source: entries/2026/06/21/wiki-Dropout_neural_networks.md
- Source URL: https://en.wikipedia.org/wiki/Dropout_(neural_networks)

### [ACCEPT] dropout-named-hinton-2012-concept-dates-1987
Dropout was named by Geoffrey Hinton et al. in 2012, but the underlying concept (called 'dilution') dates back to at least Sompolinsky (1987) and Canning & Gardner (1988).
- Source: entries/2026/06/21/wiki-Dropout_neural_networks.md
- Source URL: https://en.wikipedia.org/wiki/Dropout_(neural_networks)

### [ACCEPT] dropout-typical-keep-probability-values
Typical dropout keep probability P(c) is 0.5 for hidden layers and higher (e.g., 0.8) for input layers.
- Source: entries/2026/06/21/wiki-Dropout_neural_networks.md
- Source URL: https://en.wikipedia.org/wiki/Dropout_(neural_networks)

