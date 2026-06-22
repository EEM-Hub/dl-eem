# Exam Results: deep-learning-exam.md

**Date:** 2026-06-22 11:21
**Model:** claude:sonnet
**Score:** 37/40 (92%)

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
- **Q10**: WRONG — What was the first deep learning algorithm, and when was it introduced?
  - Expected: GMDH (Group Method of Data Handling), introduced in 1965 by Alexei Ivakhnenko
  - Got: Backpropagation, 1986
- **Q11**: CORRECT — What event in 1969 contributed to the first AI winter?
- **Q12**: CORRECT — What network won the 2012 ImageNet competition and catalyzed the modern deep learning era?
- **Q13**: CORRECT — What are the three gates in an LSTM cell?
- **Q14**: CORRECT — When was the forget gate added to LSTM, and why is it significant?
- **Q15**: CORRECT — Does LSTM solve both the vanishing and exploding gradient problems?
- **Q16**: CORRECT — What is the gradient descent update rule?
- **Q17**: CORRECT — When was gradient descent first described?
- **Q18**: CORRECT — Why are saddle points a bigger concern than local minima in high-dimensional optimization?
- **Q19**: CORRECT — What distinguishes GANs as "implicit" generative models?
- **Q20**: CORRECT — What is the GAN training objective (minimax formulation)?
- **Q21**: CORRECT — What divergence does the optimal GAN discriminator relate to?
- **Q22**: CORRECT — What is the difference between L1 and L2 regularization in terms of weight behavior?
- **Q23**: CORRECT — What is the Bayesian interpretation of L2 regularization?
- **Q24**: CORRECT — How does early stopping relate to L2 regularization?
- **Q25**: CORRECT — What is the typical dropout rate for hidden layers?
- **Q26**: CORRECT — What is a VAE's key distinction from a standard autoencoder in its latent space?
- **Q27**: CORRECT — What classical dimensionality reduction technique is a linear autoencoder equivalent to?
- **Q28**: CORRECT — What are the three components of neural architecture search (NAS)?
- **Q29**: CORRECT — How much did ENAS reduce the computational cost of NAS compared to the original approach?
- **Q30**: CORRECT — What is the exploration-exploitation tradeoff strategy called where an agent takes random actions with probability epsilon?
- **Q31**: CORRECT — What are the four components of a Markov Decision Process (MDP)?
- **Q32**: CORRECT — Why must the discount factor gamma be less than 1 in infinite-horizon MDPs?
- **Q33**: CORRECT — Is Flash Attention an approximation of standard attention?
- **Q34**: CORRECT — What is negative transfer in the context of transfer learning?
- **Q35**: WRONG — What year was the concept of transfer learning first published?
  - Expected: b
  - Got: a
- **Q36**: CORRECT — What does the CNN convolution operation actually compute mathematically?
- **Q37**: WRONG — What problem does batch normalization address, and who introduced it?
  - Expected: Batch normalization was introduced by Ioffe and Szegedy in 2015. It normalizes layer inputs across the minibatch to stabilize and accelerate training, though the original explanation based on internal covariate shift has been challenged.
  - Got: Batch normalization addresses internal covariate shift and was introduced by Sergey Ioffe and Christian Szegedy in 2015.
- **Q38**: CORRECT — What is the derivative of the softplus function?
- **Q39**: CORRECT — What is the risk function in statistical decision theory?
- **Q40**: CORRECT — What loss function is minimized by the posterior mean?

## Wrong Answers (Detail)

### Q10: What was the first deep learning algorithm, and when was it introduced?
- **Expected:** GMDH (Group Method of Data Handling), introduced in 1965 by Alexei Ivakhnenko
- **Got:** Backpropagation, 1986
- **Objective:** History of Deep Learning

**Model response:**

```
```json
{"answer": "Backpropagation, 1986", "explanation": "While the mathematical foundations of backpropagation existed earlier (Linnainmaa's automatic differentiation in 1970), the algorithm that enabled training deep neural networks was popularized by Rumelhart, Hinton, and Williams in their seminal 1986 paper 'Learning representations by back-propagating errors.' This algorithm allows efficient computation of gradients in multi-layer neural networks through the chain rule, making it possible to train networks with multiple hidden layers. Backpropagation remains the fundamental algorithm underlying modern deep learning, enabling the training of deep architectures that were previously impractical."}
```
```

### Q35: What year was the concept of transfer learning first published?
- a) 1995
- b) 1976 **<--**
- c) 2003
- d) 2012
- **Expected:** b
- **Got:** a
- **Objective:** Transfer Learning

**Model response:**

```
```json
{"answer": "a", "explanation": "Transfer learning as a formal concept in machine learning emerged in the mid-1990s, with foundational work by researchers like Lorien Pratt and Sebastian Thrun. Pratt's 1993 paper on discriminability-based transfer and the subsequent 1998 book 'Learning to Learn' edited by Thrun and Pratt established the theoretical framework. While the cognitive science roots of learning transfer date back earlier, and modern deep learning applications became prominent around 2012 with ImageNet pre-training, the explicit formalization of transfer learning in machine learning literature began around 1995."}
```
```

### Q37: What problem does batch normalization address, and who introduced it?
- **Expected:** Batch normalization was introduced by Ioffe and Szegedy in 2015. It normalizes layer inputs across the minibatch to stabilize and accelerate training, though the original explanation based on internal covariate shift has been challenged.
- **Got:** Batch normalization addresses internal covariate shift and was introduced by Sergey Ioffe and Christian Szegedy in 2015.
- **Objective:** Batch Normalization

**Model response:**

```
```json
{"answer": "Batch normalization addresses internal covariate shift and was introduced by Sergey Ioffe and Christian Szegedy in 2015.", "explanation": "Batch normalization was introduced by Sergey Ioffe and Christian Szegedy in their 2015 paper to address the problem of internal covariate shift, where the distribution of layer inputs changes during training as parameters of previous layers update. This phenomenon slows down training and requires careful initialization and lower learning rates. Batch normalization normalizes layer inputs by computing mean and variance statistics over mini-batches, which stabilizes the learning process, enables higher learning rates, reduces sensitivity to initialization, and provides a mild regularization effect. It became a fundamental technique in deep learning, significantly improving training speed and model performance."}
```
```


## By Objective

- **Batch Normalization**: 0/1 (0%) **WEAK AREA**
- **Transfer Learning**: 1/2 (50%)
- **History of Deep Learning**: 3/4 (75%)
- **Activation Functions**: 3/3 (100%)
- **Attention Mechanisms**: 3/3 (100%)
- **Transformer Architecture**: 4/4 (100%)
- **LSTM Architecture**: 3/3 (100%)
- **Gradient Descent**: 3/3 (100%)
- **Generative Adversarial Networks**: 3/3 (100%)
- **Regularization**: 3/3 (100%)
- **Dropout**: 1/1 (100%)
- **Autoencoders**: 2/2 (100%)
- **Neural Architecture Search**: 2/2 (100%)
- **Reinforcement Learning**: 3/3 (100%)
- **Convolutional Neural Networks**: 1/1 (100%)
- **Loss Functions**: 2/2 (100%)
