# Deep Learning Exam

## Q1: What property of activation functions enables neural networks to approximate arbitrary functions?
- a) Differentiability
- b) Nonlinearity
- c) Monotonicity
- d) Boundedness
Answer: b
Objective: Activation Functions

## Q2: What happens when all layers of a deep network use linear activation functions?
- a) The network becomes more expressive
- b) Training becomes unstable
- c) The network collapses to a single-layer equivalent
- d) Gradient descent fails to converge
Answer: c
Objective: Activation Functions

## Q3: What is the formula for scaled dot-product attention?
Answer: softmax(QK^T / sqrt(d_k))V
Objective: Attention Mechanisms

## Q4: What is the computational complexity of the self-attention matrix with respect to sequence length n?
- a) O(n)
- b) O(n log n)
- c) O(n^2)
- d) O(n^3)
Answer: c
Objective: Attention Mechanisms

## Q5: Who introduced the Transformer architecture, and in what year?
Answer: Vaswani et al. introduced the Transformer in 2017 in "Attention Is All You Need"
Objective: Transformer Architecture

## Q6: Why is self-attention permutation invariant, and what mechanism is used to address this?
Answer: Self-attention treats input as a set with no inherent ordering, so positional encodings are added to inject sequence order information.
Objective: Transformer Architecture

## Q7: Which Transformer variant uses only the encoder stack?
- a) GPT
- b) BERT
- c) T5
- d) LLaMA
Answer: b
Objective: Transformer Architecture

## Q8: What is the key difference between Pre-LN and Post-LN Transformer architectures?
Answer: In Pre-LN, layer normalization is applied before the attention/FFN sublayer, while in Post-LN it is applied after. Pre-LN is more stable for training deep Transformers.
Objective: Transformer Architecture

## Q9: What year was backpropagation's mathematical foundation (automatic differentiation) first described, and by whom?
- a) Rumelhart, 1986
- b) Linnainmaa, 1970
- c) Werbos, 1974
- d) LeCun, 1989
Answer: b
Objective: History of Deep Learning

## Q10: What was the first deep learning algorithm, and when was it introduced?
Answer: GMDH (Group Method of Data Handling), introduced in 1965 by Alexei Ivakhnenko
Objective: History of Deep Learning

## Q11: What event in 1969 contributed to the first AI winter?
Answer: Minsky and Papert published "Perceptrons," which highlighted the limitations of single-layer perceptrons and discouraged neural network research.
Objective: History of Deep Learning

## Q12: What network won the 2012 ImageNet competition and catalyzed the modern deep learning era?
- a) VGGNet
- b) GoogLeNet
- c) AlexNet
- d) ResNet
Answer: c
Objective: History of Deep Learning

## Q13: What are the three gates in an LSTM cell?
- a) Input, output, reset
- b) Input, forget, output
- c) Read, write, erase
- d) Update, reset, output
Answer: b
Objective: LSTM Architecture

## Q14: When was the forget gate added to LSTM, and why is it significant?
Answer: The forget gate was added in 2000 by Gers et al. It allows the cell to reset its state, which was essential for learning to process continuous input streams and improved performance on many tasks.
Objective: LSTM Architecture

## Q15: Does LSTM solve both the vanishing and exploding gradient problems?
Answer: LSTM solves the vanishing gradient problem through its cell state mechanism, but does not directly solve the exploding gradient problem. Gradient clipping is typically used separately for exploding gradients.
Objective: LSTM Architecture

## Q16: What is the gradient descent update rule?
Answer: theta_{t+1} = theta_t - alpha * gradient of f(theta_t), where alpha is the learning rate
Objective: Gradient Descent

## Q17: When was gradient descent first described?
- a) 1950
- b) 1847
- c) 1936
- d) 1900
Answer: b
Objective: Gradient Descent

## Q18: Why are saddle points a bigger concern than local minima in high-dimensional optimization?
Answer: In high-dimensional spaces, saddle points are exponentially more common than local minima. At a saddle point, the gradient is zero but the point is a minimum in some dimensions and a maximum in others, causing gradient descent to slow down or stall.
Objective: Gradient Descent

## Q19: What distinguishes GANs as "implicit" generative models?
Answer: GANs are implicit generative models because the generator defines a sampling procedure to produce data but never explicitly computes or defines a probability density function over the data space.
Objective: Generative Adversarial Networks

## Q20: What is the GAN training objective (minimax formulation)?
Answer: min_G max_D E[log D(x)] + E[log(1 - D(G(z)))]
Objective: Generative Adversarial Networks

## Q21: What divergence does the optimal GAN discriminator relate to?
- a) KL divergence
- b) Wasserstein distance
- c) Jensen-Shannon divergence
- d) Total variation distance
Answer: c
Objective: Generative Adversarial Networks

## Q22: What is the difference between L1 and L2 regularization in terms of weight behavior?
Answer: L1 regularization induces sparsity by driving some weights exactly to zero, while L2 regularization produces small but nonzero weights across all parameters.
Objective: Regularization

## Q23: What is the Bayesian interpretation of L2 regularization?
- a) Laplace prior on weights
- b) Gaussian prior on weights
- c) Uniform prior on weights
- d) Cauchy prior on weights
Answer: b
Objective: Regularization

## Q24: How does early stopping relate to L2 regularization?
Answer: Early stopping has been shown to be approximately equivalent to L2 regularization, as both constrain the effective capacity of the model by limiting how far weights can move from their initialization.
Objective: Regularization

## Q25: What is the typical dropout rate for hidden layers?
- a) 0.1
- b) 0.3
- c) 0.5
- d) 0.8
Answer: c
Objective: Dropout

## Q26: What is a VAE's key distinction from a standard autoencoder in its latent space?
Answer: A VAE encodes inputs as probability distributions (typically Gaussian) in the latent space rather than deterministic point vectors, enabling generation of new samples by sampling from the learned latent distribution.
Objective: Autoencoders

## Q27: What classical dimensionality reduction technique is a linear autoencoder equivalent to?
- a) t-SNE
- b) PCA
- c) LDA
- d) ICA
Answer: b
Objective: Autoencoders

## Q28: What are the three components of neural architecture search (NAS)?
Answer: Search space (what architectures can be represented), search strategy (how to explore the space), and performance estimation strategy (how to evaluate candidate architectures).
Objective: Neural Architecture Search

## Q29: How much did ENAS reduce the computational cost of NAS compared to the original approach?
- a) 10x
- b) 100x
- c) 1000x
- d) 10000x
Answer: c
Objective: Neural Architecture Search

## Q30: What is the exploration-exploitation tradeoff strategy called where an agent takes random actions with probability epsilon?
- a) Softmax exploration
- b) UCB exploration
- c) Epsilon-greedy exploration
- d) Thompson sampling
Answer: c
Objective: Reinforcement Learning

## Q31: What are the four components of a Markov Decision Process (MDP)?
Answer: States, actions, transition probabilities (dynamics), and a reward function.
Objective: Reinforcement Learning

## Q32: Why must the discount factor gamma be less than 1 in infinite-horizon MDPs?
Answer: To ensure the sum of future rewards converges to a finite value. Without discounting (gamma >= 1), the cumulative reward could be infinite, making comparisons between policies undefined.
Objective: Reinforcement Learning

## Q33: Is Flash Attention an approximation of standard attention?
- a) Yes, it trades accuracy for speed
- b) No, it computes exact attention with better memory access patterns
- c) Yes, it uses sparse attention patterns
- d) No, it uses a different attention formula entirely
Answer: b
Objective: Attention Mechanisms

## Q34: What is negative transfer in the context of transfer learning?
Answer: Negative transfer occurs when knowledge transferred from a source domain actually hurts performance on the target task, rather than helping it. This can happen when the source and target domains are too dissimilar.
Objective: Transfer Learning

## Q35: What year was the concept of transfer learning first published?
- a) 1995
- b) 1976
- c) 2003
- d) 2012
Answer: b
Objective: Transfer Learning

## Q36: What does the CNN convolution operation actually compute mathematically?
- a) Convolution
- b) Cross-correlation
- c) Dot product
- d) Outer product
Answer: b
Objective: Convolutional Neural Networks

## Q37: What problem does batch normalization address, and who introduced it?
Answer: Batch normalization was introduced by Ioffe and Szegedy in 2015. It normalizes layer inputs across the minibatch to stabilize and accelerate training, though the original explanation based on internal covariate shift has been challenged.
Objective: Batch Normalization

## Q38: What is the derivative of the softplus function?
- a) ReLU
- b) Sigmoid
- c) Tanh
- d) GELU
Answer: b
Objective: Activation Functions

## Q39: What is the risk function in statistical decision theory?
Answer: The risk function is the expected value of the loss function, computed as the expectation of the loss over the data distribution.
Objective: Loss Functions

## Q40: What loss function is minimized by the posterior mean?
- a) Cross-entropy loss
- b) Mean absolute error
- c) Mean squared error
- d) Hinge loss
Answer: c
Objective: Loss Functions
