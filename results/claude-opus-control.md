# Exam Results: deep-learning-exam.md

**Date:** 2026-06-22 10:49
**Model:** claude:opus
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
  - Got: Backpropagation (1986)
- **Q11**: WRONG — What event in 1969 contributed to the first AI winter?
  - Expected: Minsky and Papert published "Perceptrons," which highlighted the limitations of single-layer perceptrons and discouraged neural network research.
  - Got: The Mansfield Amendment
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
- **Q37**: CORRECT — What problem does batch normalization address, and who introduced it?
- **Q38**: CORRECT — What is the derivative of the softplus function?
- **Q39**: CORRECT — What is the risk function in statistical decision theory?
- **Q40**: CORRECT — What loss function is minimized by the posterior mean?

## Wrong Answers (Detail)

### Q10: What was the first deep learning algorithm, and when was it introduced?
- **Expected:** GMDH (Group Method of Data Handling), introduced in 1965 by Alexei Ivakhnenko
- **Got:** Backpropagation (1986)
- **Objective:** History of Deep Learning

**Model response:**

```
```json
{"answer": "Backpropagation (1986)", "explanation": "While neural network concepts date back to the 1940s (McCulloch-Pitts neuron) and the perceptron was introduced in 1958, the algorithm most commonly credited as launching deep learning is the backpropagation algorithm as popularized by Rumelhart, Hinton, and Williams in their seminal 1986 paper 'Learning representations by back-propagation of errors' published in Nature. Backpropagation provided an efficient method for computing gradients in multi-layer neural networks, enabling the training of networks with hidden layers — the core requirement for 'deep' learning. Earlier related work existed (Werbos described backpropagation in his 1974 PhD thesis, and Linnainmaa formalized reverse-mode automatic differentiation in 1970), but the 1986 paper demonstrated its practical effectiveness for learning internal representations and is widely regarded as the foundational moment for deep learning as a field."}
```
```

### Q11: What event in 1969 contributed to the first AI winter?
- **Expected:** Minsky and Papert published "Perceptrons," which highlighted the limitations of single-layer perceptrons and discouraged neural network research.
- **Got:** The Mansfield Amendment
- **Objective:** History of Deep Learning

**Model response:**

```
{"answer": "The Mansfield Amendment", "explanation": "The Mansfield Amendment of 1969 required the Defense Advanced Research Projects Agency (DARPA, then ARPA) to fund only research with direct military applicability, rather than basic 'blue sky' research. Since ARPA had been the primary funder of AI research in the United States, this legislation significantly curtailed funding for exploratory AI projects that lacked clear near-term military applications. Combined with the influential 1966 ALPAC report (which cut machine translation funding) and the 1969 book 'Perceptrons' by Minsky and Papert — which formally demonstrated the limitations of single-layer perceptrons and was widely interpreted as discrediting neural network research — these events collectively triggered the first AI winter. The Mansfield Amendment was particularly impactful because it shifted the funding landscape, forcing AI researchers to justify practical military relevance for their work at a time when AI's theoretical promises far outstripped its deliverable capabilities."}
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
{"answer": "a", "explanation": "The concept of transfer learning in machine learning is most commonly traced back to a 1995 NIPS workshop titled 'Learning to Learn,' organized by Sebastian Thrun and Lorien Pratt. This workshop and the subsequent 1998 book 'Learning to Learn' formalized the idea that knowledge gained from one task could be transferred to improve learning on a related task. While earlier related ideas existed in psychology and some preliminary computational work appeared before 1995, the 1995 workshop is widely recognized as the seminal moment when transfer learning was formally introduced as a research topic in the machine learning community."}
```


## By Objective

- **History of Deep Learning**: 2/4 (50%)
- **Transfer Learning**: 1/2 (50%)
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
- **Batch Normalization**: 1/1 (100%)
- **Loss Functions**: 2/2 (100%)
