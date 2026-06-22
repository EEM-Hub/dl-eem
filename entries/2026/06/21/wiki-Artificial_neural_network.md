---
source: sources/wiki-Artificial_neural_network.md
source_url: https://en.wikipedia.org/wiki/Artificial_neural_network
---

## Neural Networks: Architecture, History, and Core Mechanisms

Neural networks are computational models inspired by biological neural networks, consisting of interconnected artificial neurons organized in layers. They form the foundation of modern deep learning and are used across domains including computer vision, natural language processing, robotics, and generative AI. This page covers the structural components of neural networks, their extensive historical development from the 1940s through modern deep learning, and the key architectural innovations (CNNs, RNNs, LSTMs, Transformers) that drove successive breakthroughs.

## Key Concepts

- **Artificial neuron**: A node that receives signals, computes a non-linear function (activation function) over the weighted sum of inputs, and outputs a real number to connected neurons.
- **Weights**: Parameters on edges between neurons that adjust during training to minimize error; they determine signal strength.
- **Activation function**: The non-linear function applied to the sum of weighted inputs. ReLU (introduced by Fukushima, 1969) is the most common.
- **Layers**: Neurons are grouped into an input layer, one or more hidden layers, and an output layer. A network with at least two hidden layers is called a "deep" neural network.
- **Deep neural networks** learn hierarchical representations — each successive layer captures increasingly abstract features.
- **Backpropagation**: Algorithm for training multi-layer networks by propagating error gradients backward through layers using the chain rule. Modern form published by Linnainmaa (1970); applied to neural networks by Werbos (1982); popularized by Rumelhart et al. (1986).
- **Vanishing gradient problem**: Identified by Hochreiter (1991) — gradients diminish through many layers, preventing deep networks from learning. Addressed by LSTM and residual connections.
- **Training** is compute-intensive, accelerated by GPUs and large datasets.
- **Transfer learning**: Introduced in 1976; reusing learned representations across tasks.
- The simplest feedforward network is equivalent to linear regression (method of least squares, Legendre 1805 / Gauss 1795).

## Commands and Syntax

This page is conceptual rather than procedural. No specific commands or configuration syntax are described. Key mathematical/algorithmic procedures referenced:

- **Stochastic gradient descent (SGD)**: Iterative optimization used to train MLPs; first applied to a deep MLP by Amari (1967).
- **Backpropagation procedure**: Compute output error → propagate gradients backward through layers via chain rule → update weights.
- **Group Method of Data Handling (GMDH)**: Train deep networks layer-by-layer via regression analysis, prune superfluous units using a validation set (Ivakhnenko & Lapa, 1965).
- **Max pooling**: Downsampling operation in CNNs that selects the maximum value in each spatial region (introduced by Fukushima, 1979).

## Relationships

- **Biological neural networks → Artificial neural networks**: Inspiration source; connectionism models information processing without separating memory and processing (unlike von Neumann architecture).
- **Linear regression → Feedforward networks**: The simplest single-layer linear network is equivalent to least squares regression.
- **CNNs → Computer vision**: Convolutional architectures (neocognitron → LeNet → AlexNet → VGG → Inception) drove successive breakthroughs in image recognition.
- **RNNs → Sequential data**: Recurrent architectures handle time-series, speech, and language; evolved from Hopfield networks and Elman/Jordan networks into LSTM/GRU.
- **Transformers → Large Language Models**: Attention mechanisms replaced recurrence for modeling long-range dependencies; foundation of modern LLMs.
- **Statistical mechanics → Neural network theory**: Boltzmann machines, restricted Boltzmann machines, and Helmholtz machines originated from physics-inspired approaches.
- **Perceptrons → AI winter**: Minsky & Papert's 1969 critique of single-layer perceptrons' limitations (e.g., XOR problem) deflated funding; irrelevant to already-existing deep networks (Ivakhnenko, Amari).

## Exam-Relevant Points

- A network needs **at least two hidden layers** to be called "deep."
- **ReLU** was introduced by Fukushima (1969) and is the most common activation function today.
- **Backpropagation** chain of attribution: Leibniz (chain rule, 1673) → Kelley (control theory precursor, 1960) → Rosenblatt (coined "back-propagating errors" but didn't implement, 1962) → Linnainmaa (modern form, 1970) → Werbos (applied to NNs, 1982) → Rumelhart et al. (popularized, 1986).
- **First deep learning algorithm**: GMDH by Ivakhnenko & Lapa (1965, Soviet Union); a 1971 paper trained 8 layers.
- **First deep MLP trained by SGD**: Amari (1967), 5-layer network with 2 modifiable layers.
- **CNN lineage**: Neocognitron (Fukushima, 1979) → TDNN (Waibel, 1987) → LeNet (LeCun, 1989) → AlexNet (Krizhevsky/Sutskever/Hinton, 2012).
- **Vanishing gradient problem** identified by Hochreiter (1991); solved by **LSTM** (Hochreiter & Schmidhuber), with the critical **forget gate** added in 1999.
- **AlexNet** (2012) won ImageNet by a large margin over shallow methods, catalyzing the modern deep learning era.
- McCulloch & Pitts (1943) created the first computational model of neural networks (non-learning).
- **Hebbian learning** ("neurons that fire together wire together") was the basis for early experiments including the perceptron and Hopfield network.
- **Self-supervised pre-training** was introduced by Schmidhuber's "neural history compressor" (1991) — the "P" in GPT/ChatGPT.
- Minsky & Papert's *Perceptrons* (1969) caused the first AI winter for neural networks by showing single-layer perceptrons can't solve XOR.
- **DanNet** (Ciresan et al., 2011) was the first CNN to achieve superhuman visual pattern recognition performance.
