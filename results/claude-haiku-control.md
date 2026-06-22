# Exam Results: deep-learning-exam.md

**Date:** 2026-06-22 11:46
**Model:** claude:haiku
**Score:** 36/40 (90%)

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
  - Got: Backpropagation (1986) by Rumelhart, Hinton, and Williams
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
- **Q24**: WRONG — How does early stopping relate to L2 regularization?
  - Expected: Early stopping has been shown to be approximately equivalent to L2 regularization, as both constrain the effective capacity of the model by limiting how far weights can move from their initialization.
  - Got: Early stopping and L2 regularization are complementary regularization techniques that both combat overfitting but operate through different mechanisms.
- **Q25**: CORRECT — What is the typical dropout rate for hidden layers?
- **Q26**: CORRECT — What is a VAE's key distinction from a standard autoencoder in its latent space?
- **Q27**: CORRECT — What classical dimensionality reduction technique is a linear autoencoder equivalent to?
- **Q28**: CORRECT — What are the three components of neural architecture search (NAS)?
- **Q29**: WRONG — How much did ENAS reduce the computational cost of NAS compared to the original approach?
  - Expected: c
  - Got: a
- **Q30**: CORRECT — What is the exploration-exploitation tradeoff strategy called where an agent takes random actions with probability epsilon?
- **Q31**: CORRECT — What are the four components of a Markov Decision Process (MDP)?
- **Q32**: CORRECT — Why must the discount factor gamma be less than 1 in infinite-horizon MDPs?
- **Q33**: CORRECT — Is Flash Attention an approximation of standard attention?
- **Q34**: CORRECT — What is negative transfer in the context of transfer learning?
- **Q35**: WRONG — What year was the concept of transfer learning first published?
  - Expected: b
  - Got: a
- **Q36**: CORRECT — What does the CNN convolution operation actually compute mathematically?
- **Q37**: CORRECT — What problem does batch normalization address, and who introduced it?
- **Q38**: CORRECT — What is the derivative of the softplus function?
- **Q39**: CORRECT — What is the risk function in statistical decision theory?
- **Q40**: CORRECT — What loss function is minimized by the posterior mean?

## Wrong Answers (Detail)

### Q10: What was the first deep learning algorithm, and when was it introduced?
- **Expected:** GMDH (Group Method of Data Handling), introduced in 1965 by Alexei Ivakhnenko
- **Got:** Backpropagation (1986) by Rumelhart, Hinton, and Williams
- **Objective:** History of Deep Learning

**Model response:**

```
```json
{
  "answer": "Backpropagation (1986) by Rumelhart, Hinton, and Williams",
  "explanation": "Backpropagation, introduced in 1986 through the landmark paper 'Learning representations by back-propagating errors,' was the foundational algorithm that made training deep neural networks with multiple hidden layers computationally feasible. While earlier neural network concepts like the perceptron existed (1958), they were limited to single-layer systems and suffered from the inability to effectively train hidden layers. Backpropagation solved this by enabling efficient computation of gradients for all layers through the chain rule, thereby unlocking the possibility of training deep architectures. This algorithm became the cornerstone of modern deep learning and remains central to training neural networks today."
}
```
```

### Q24: How does early stopping relate to L2 regularization?
- **Expected:** Early stopping has been shown to be approximately equivalent to L2 regularization, as both constrain the effective capacity of the model by limiting how far weights can move from their initialization.
- **Got:** Early stopping and L2 regularization are complementary regularization techniques that both combat overfitting but operate through different mechanisms.
- **Objective:** Regularization

**Model response:**

```
```json
{
  "answer": "Early stopping and L2 regularization are complementary regularization techniques that both combat overfitting but operate through different mechanisms.",
  "explanation": "L2 regularization penalizes large weights by adding a λ∑w² term to the loss function, directly constraining weight magnitude during training. Early stopping prevents overfitting by halting training when validation performance degrades, implicitly limiting the effective model capacity and the magnitude of weight updates. While L2 regularization works through the loss function and requires tuning the regularization coefficient λ, early stopping is training-duration-based and requires monitoring validation performance. They can be used together and have related effects—both bias the model toward simpler solutions with smaller effective parameter norms—but early stopping has practical advantages including no hyperparameter tuning for the regularization strength and clearer stopping criteria. Research suggests early stopping can sometimes achieve similar regularization effects as L2 without explicit weight penalties."
}
```
```

### Q29: How much did ENAS reduce the computational cost of NAS compared to the original approach?
- a) 10x
- b) 100x
- c) 1000x **<--**
- d) 10000x
- **Expected:** c
- **Got:** a
- **Objective:** Neural Architecture Search

**Model response:**

```
```json
{
  "answer": "a",
  "explanation": "ENAS (Efficient Neural Architecture Search) reduced the computational cost of neural architecture search by approximately 10x compared to the original NAS approach. The key innovation was weight sharing through a supernet architecture and controller-based search, which allowed the system to avoid training each candidate architecture from scratch. The original NAS required thousands of GPU days (e.g., ~5000 GPU days), while ENAS reduced this to around 500-1000 GPU days, achieving roughly an order of magnitude improvement in computational efficiency."
}
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
{
  "answer": "a) 1995",
  "explanation": "Transfer learning as a formal concept in machine learning was first introduced in the mid-1990s, with key early papers including work by Pratt (1993) and subsequent publications in 1995-1998. The seminal paper 'Learning to Learn' by Thrun and Pratt (1998) popularized the term, building on earlier work from the 1995 timeframe. While the concept evolved and became more prominent in deep learning around 2012, the original publication of transfer learning principles occurred in the 1995-1998 period, making 1995 the earliest answer among the options provided."
}
```
```


## By Objective

- **Neural Architecture Search**: 1/2 (50%)
- **Transfer Learning**: 1/2 (50%)
- **Regularization**: 2/3 (66%)
- **History of Deep Learning**: 3/4 (75%)
- **Activation Functions**: 3/3 (100%)
- **Attention Mechanisms**: 3/3 (100%)
- **Transformer Architecture**: 4/4 (100%)
- **LSTM Architecture**: 3/3 (100%)
- **Gradient Descent**: 3/3 (100%)
- **Generative Adversarial Networks**: 3/3 (100%)
- **Dropout**: 1/1 (100%)
- **Autoencoders**: 2/2 (100%)
- **Reinforcement Learning**: 3/3 (100%)
- **Convolutional Neural Networks**: 1/1 (100%)
- **Batch Normalization**: 1/1 (100%)
- **Loss Functions**: 2/2 (100%)
