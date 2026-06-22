# Exam Results: deep-learning-exam.md

**Date:** 2026-06-22 11:54
**Model:** claude:haiku
**Score:** 35/40 (87%)

## Per-Question Results

- **Q1**: CORRECT — What property of activation functions enables neural networks to approximate arbitrary functions?
- **Q2**: CORRECT — What happens when all layers of a deep network use linear activation functions?
- **Q3**: CORRECT — What is the formula for scaled dot-product attention?
- **Q4**: CORRECT — What is the computational complexity of the self-attention matrix with respect to sequence length n?
- **Q5**: CORRECT — Who introduced the Transformer architecture, and in what year?
- **Q6**: CORRECT — Why is self-attention permutation invariant, and what mechanism is used to address this?
- **Q7**: CORRECT — Which Transformer variant uses only the encoder stack?
- **Q8**: CORRECT — What is the key difference between Pre-LN and Post-LN Transformer architectures?
- **Q9**: CORRECT — What year was backpropagation's mathematical foundation (automatic differentiation) first described, and by whom?
- **Q10**: CORRECT — What was the first deep learning algorithm, and when was it introduced?
- **Q11**: CORRECT — What event in 1969 contributed to the first AI winter?
- **Q12**: CORRECT — What network won the 2012 ImageNet competition and catalyzed the modern deep learning era?
- **Q13**: CORRECT — What are the three gates in an LSTM cell?
- **Q14**: CORRECT — When was the forget gate added to LSTM, and why is it significant?
- **Q15**: CORRECT — Does LSTM solve both the vanishing and exploding gradient problems?
- **Q16**: CORRECT — What is the gradient descent update rule?
- **Q17**: CORRECT — When was gradient descent first described?
- **Q18**: CORRECT — Why are saddle points a bigger concern than local minima in high-dimensional optimization?
- **Q19**: WRONG — What distinguishes GANs as "implicit" generative models?
  - Expected: GANs are implicit generative models because the generator defines a sampling procedure to produce data but never explicitly computes or defines a probability density function over the data space.
  - Got: Let me search the belief database for relevant information about GANs and implicit models.

{"tool":
- **Q20**: CORRECT — What is the GAN training objective (minimax formulation)?
- **Q21**: CORRECT — What divergence does the optimal GAN discriminator relate to?
- **Q22**: WRONG — What is the difference between L1 and L2 regularization in terms of weight behavior?
  - Expected: L1 regularization induces sparsity by driving some weights exactly to zero, while L2 regularization produces small but nonzero weights across all parameters.
  - Got: Based on the belief database search, I have found clear information about the difference between L1
- **Q23**: CORRECT — What is the Bayesian interpretation of L2 regularization?
- **Q24**: CORRECT — How does early stopping relate to L2 regularization?
- **Q25**: WRONG — What is the typical dropout rate for hidden layers?
  - Expected: c
  - Got: b
- **Q26**: CORRECT — What is a VAE's key distinction from a standard autoencoder in its latent space?
- **Q27**: CORRECT — What classical dimensionality reduction technique is a linear autoencoder equivalent to?
- **Q28**: CORRECT — What are the three components of neural architecture search (NAS)?
- **Q29**: CORRECT — How much did ENAS reduce the computational cost of NAS compared to the original approach?
- **Q30**: CORRECT — What is the exploration-exploitation tradeoff strategy called where an agent takes random actions with probability epsilon?
- **Q31**: CORRECT — What are the four components of a Markov Decision Process (MDP)?
- **Q32**: CORRECT — Why must the discount factor gamma be less than 1 in infinite-horizon MDPs?
- **Q33**: CORRECT — Is Flash Attention an approximation of standard attention?
- **Q34**: WRONG — What is negative transfer in the context of transfer learning?
  - Expected: Negative transfer occurs when knowledge transferred from a source domain actually hurts performance on the target task, rather than helping it. This can happen when the source and target domains are too dissimilar.
  - Got: Let me try using the tools directly to search the belief database:

I'll search for information abou
- **Q35**: CORRECT — What year was the concept of transfer learning first published?
- **Q36**: CORRECT — What does the CNN convolution operation actually compute mathematically?
- **Q37**: CORRECT — What problem does batch normalization address, and who introduced it?
- **Q38**: CORRECT — What is the derivative of the softplus function?
- **Q39**: CORRECT — What is the risk function in statistical decision theory?
- **Q40**: WRONG — What loss function is minimized by the posterior mean?
  - Expected: c
  - Got: Let me try searching the belief database directly:

{"tool": "search_beliefs", "query": "posterior m

## Wrong Answers (Detail)

### Q19: What distinguishes GANs as "implicit" generative models?
- **Expected:** GANs are implicit generative models because the generator defines a sampling procedure to produce data but never explicitly computes or defines a probability density function over the data space.
- **Got:** Let me search the belief database for relevant information about GANs and implicit models.

{"tool":
- **Objective:** Generative Adversarial Networks

**Model response:**

```

```

### Q22: What is the difference between L1 and L2 regularization in terms of weight behavior?
- **Expected:** L1 regularization induces sparsity by driving some weights exactly to zero, while L2 regularization produces small but nonzero weights across all parameters.
- **Got:** Based on the belief database search, I have found clear information about the difference between L1
- **Objective:** Regularization

**Model response:**

```

```

### Q25: What is the typical dropout rate for hidden layers?
- a) 0.1
- b) 0.3
- c) 0.5 **<--**
- d) 0.8
- **Expected:** c
- **Got:** b
- **Objective:** Dropout

**Model response:**

```
The belief database confirms that the typical dropout rate for hidden layers is 0.5 (equivalently, a keep probability of 0.5). This is the canonical value used in practice. The reasoning is that dropout works by zeroing entire neurons, and hidden layer neurons tolerate this aggressive 50% dropout because their distributed representations provide redundancy against individual neuron removal. Input layers use higher keep probability (0.8) because dropping input neurons destroys entire raw feature channels, making them less recoverable.
```

### Q34: What is negative transfer in the context of transfer learning?
- **Expected:** Negative transfer occurs when knowledge transferred from a source domain actually hurts performance on the target task, rather than helping it. This can happen when the source and target domains are too dissimilar.
- **Got:** Let me try using the tools directly to search the belief database:

I'll search for information abou
- **Objective:** Transfer Learning

**Model response:**

```

```

### Q40: What loss function is minimized by the posterior mean?
- a) Cross-entropy loss
- b) Mean absolute error
- c) Mean squared error **<--**
- d) Hinge loss
- **Expected:** c
- **Got:** Let me try searching the belief database directly:

{"tool": "search_beliefs", "query": "posterior m
- **Objective:** Loss Functions

**Model response:**

```

```


## By Objective

- **Dropout**: 0/1 (0%) **WEAK AREA**
- **Transfer Learning**: 1/2 (50%)
- **Loss Functions**: 1/2 (50%)
- **Generative Adversarial Networks**: 2/3 (66%)
- **Regularization**: 2/3 (66%)
- **Activation Functions**: 3/3 (100%)
- **Attention Mechanisms**: 3/3 (100%)
- **Transformer Architecture**: 4/4 (100%)
- **History of Deep Learning**: 4/4 (100%)
- **LSTM Architecture**: 3/3 (100%)
- **Gradient Descent**: 3/3 (100%)
- **Autoencoders**: 2/2 (100%)
- **Neural Architecture Search**: 2/2 (100%)
- **Reinforcement Learning**: 3/3 (100%)
- **Convolutional Neural Networks**: 1/1 (100%)
- **Batch Normalization**: 1/1 (100%)
