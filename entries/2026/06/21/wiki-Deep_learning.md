---
source: sources/wiki-Deep_learning.md
source_url: https://en.wikipedia.org/wiki/Deep_learning
---

## Deep Learning: Foundations, Architectures, and History

Deep learning is a subfield of machine learning that uses multilayered neural networks — typically three to hundreds or thousands of layers — to learn hierarchical representations of data. Rather than relying on hand-crafted feature engineering, deep learning models automatically discover useful features at progressively higher levels of abstraction. The field draws loose inspiration from biological neuroscience but is not intended to model actual brain function.

## Key Concepts

- **"Deep" definition**: Refers to the number of layers (depth of the credit assignment path / CAP). CAP depth > 2 is generally considered "deep." No universal threshold exists.
- **Credit Assignment Path (CAP)**: The chain of transformations from input to output. For feedforward networks, CAP depth = hidden layers + 1. For RNNs, CAP depth is potentially unlimited.
- **Universal Approximation Theorem**: A network with CAP depth of 2 can emulate any function, but deeper models extract better features in practice.
- **Width constraint (Lu et al.)**: A deep ReLU network is a universal approximator only if its width is strictly greater than the input dimension.
- **Automatic feature learning**: Deep learning replaces hand-crafted feature engineering with learned representations — raw input is transformed layer-by-layer into increasingly abstract representations (e.g., pixels → edges → parts → objects).
- **Probabilistic interpretation**: Treats activation nonlinearities as cumulative distribution functions; led to the introduction of dropout as a regularizer.
- **Training paradigms**: Supervised, semi-supervised, and unsupervised learning are all applicable. Unsupervised deep learning is especially valuable because unlabeled data is far more abundant.
- **Greedy layer-by-layer training**: An alternative to end-to-end backpropagation; each layer is trained independently then stacked.

## Core Architectures

- **Fully connected networks (FCN)**: Every neuron connected to all neurons in adjacent layers.
- **Convolutional Neural Networks (CNN)**: Use convolutional layers and downsampling; originated with Fukushima's Neocognitron (1979), formalized by LeCun's LeNet (1989).
- **Recurrent Neural Networks (RNN)**: Have cycles in connectivity; process sequences. Key variants: Jordan network (1986), Elman network (1990).
- **Long Short-Term Memory (LSTM)**: Addresses vanishing gradient problem; published 1995 by Hochreiter & Schmidhuber; modern form with forget gate added in 1999.
- **Deep Belief Networks (DBN)**: Stacked restricted Boltzmann machines, trained layer-by-layer, optionally fine-tuned with backpropagation (Hinton et al., 2006).
- **Generative Adversarial Networks (GAN)**: Two networks in a zero-sum game — a generator and a discriminator. Concept from Schmidhuber (1991), formalized as GANs in 2014.
- **Transformers**: Modern dominant architecture for sequence tasks.
- **Neural Radiance Fields (NeRF)**: For 3D scene representation.

## Key Historical Milestones

| Year | Milestone |
|------|-----------|
| 1965 | Group Method of Data Handling (GMDH) — first working deep learning algorithm (Ivakhnenko & Lapa) |
| 1967 | First deep MLP trained by stochastic gradient descent (Amari) |
| 1969 | ReLU activation function introduced (Fukushima) |
| 1970 | Modern backpropagation formulated (Linnainmaa) |
| 1979 | Neocognitron — first CNN architecture (Fukushima) |
| 1986 | Term "deep learning" introduced to ML (Dechter); backpropagation popularized (Rumelhart et al.) |
| 1989 | LeNet for handwritten ZIP code recognition (LeCun) |
| 1991 | Vanishing gradient problem identified (Hochreiter); adversarial neural networks (Schmidhuber) |
| 1995 | LSTM published (Hochreiter & Schmidhuber) |
| 1999 | LSTM forget gate — becomes standard RNN architecture |
| 2006 | Deep belief networks (Hinton, Salakhutdinov et al.) |
| 2009 | LSTM wins first pattern recognition contest (handwriting) |

## Relationships

- **Machine learning parent field**: Deep learning is a subset of ML, which is a subset of AI.
- **Feature engineering**: Deep learning automates what was previously manual feature engineering in classical ML.
- **Backpropagation**: The dominant training method; an application of the chain rule to differentiable computational graphs. Roots in control theory (Kelley, 1960).
- **Statistical mechanics**: Boltzmann machines, restricted Boltzmann machines, and the Helmholtz machine were inspired by physics.
- **Computer vision**: CNNs are the foundational architecture; progression from Neocognitron → LeNet → modern deep CNNs.
- **NLP and speech**: RNNs and LSTMs dominated sequence tasks before transformers; connectionist temporal classification (CTC) was a key enabler for speech recognition.
- **Generative modeling**: Deep belief networks, GANs, and variational approaches connect deep learning to probabilistic generative models.
- **Vanishing gradient problem**: Central challenge linking RNNs, deep feedforward networks, and the motivation for LSTM, residual connections, and ReLU.

## Exam-Relevant Points

- "Deep" means multiple layers (CAP > 2); there is no universally agreed threshold separating shallow from deep.
- CAP depth 2 is sufficient for universal approximation, but deeper networks learn better features.
- For ReLU deep networks: universal approximation requires width **strictly greater than** the input dimension (Lu et al.).
- ReLU was introduced by Fukushima in **1969** — much earlier than its popularization.
- Backpropagation's modern form: Linnainmaa (1970), applied to neural networks by Werbos (1982), popularized by Rumelhart et al. (1986).
- LSTM (1995) solves vanishing gradient; the **forget gate** (1999) completed the modern LSTM architecture.
- Deep belief networks (2006) use layer-by-layer pre-training of restricted Boltzmann machines.
- The first working deep learning algorithm was GMDH (1965), not backpropagation-based methods.
- Dropout as regularization arose from the probabilistic interpretation of neural networks.
- Deep learning can be supervised, semi-supervised, or unsupervised — unsupervised is especially important because unlabeled data is more abundant.
- First major industrial deployment: Nuance Verifier for speaker recognition (late 1990s, SRI International).
- By early 2000s, CNNs already processed 10-20% of all US checks (LeCun).
