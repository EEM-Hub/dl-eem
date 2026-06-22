---
source: sources/wiki-Convolutional_neural_network.md
source_url: https://en.wikipedia.org/wiki/Convolutional_neural_network
---

## Convolutional Neural Networks (CNNs)

CNNs are a class of feedforward neural networks that learn spatial hierarchies of features through convolution operations with learnable filters (kernels). They are the foundational architecture for deep learning-based computer vision and image processing, though increasingly supplemented by transformers in some domains. CNNs exploit local connectivity and weight sharing to dramatically reduce parameters compared to fully connected networks, enabling training on high-dimensional inputs like images.

## Key Concepts

- **Convolution operation**: Slides a small kernel (filter) across the input, computing dot products (Frobenius inner product) to produce feature maps. Despite the name, most CNN implementations actually perform cross-correlation, not true convolution.
- **Weight sharing**: All neurons in a convolutional layer sharing the same filter use identical weights, drastically reducing parameters (e.g., 25 weights for a 5x5 kernel vs. 10,000 for a fully connected neuron on a 100x100 image).
- **Translation equivariance**: Feature maps shift correspondingly when the input shifts, due to the shared-weight sliding kernel architecture. Note: CNNs are equivariant but generally NOT truly translation-invariant due to downsampling operations.
- **Receptive field**: The region of input that influences a given neuron's output. Grows larger in deeper layers as convolutions cascade. Can be manipulated with dilated/atrous convolutions without increasing parameters.
- **Feature hierarchy**: Lower layers extract local features (edges, textures); higher layers extract features from progressively wider context windows, building up to semantic representations.
- **Regularization through architecture**: Shared weights and local connectivity inherently regularize the network, mitigating vanishing/exploding gradient problems seen in fully connected networks.
- **Depthwise separable convolutions**: Decompose standard convolution into depthwise (spatial, per-channel) and pointwise (1x1 cross-channel) convolutions for speed.

## Architecture Components

- **Input tensor shape**: `(batch) x (height) x (width) x (channels)`
- **Convolutional layers**: Apply learned filters to produce feature maps (activation maps). Activation function is commonly ReLU.
- **Pooling layers**: Reduce spatial dimensions by summarizing neuron clusters.
  - **Max pooling**: Takes maximum value in each local region (e.g., 2x2). Most commonly used.
  - **Average pooling**: Takes mean value in each local region.
  - **Global pooling**: Acts on entire feature map, reducing each channel to a single value.
- **Fully connected layers**: Traditional MLP layers that flatten feature maps and perform classification. Connect every neuron to every neuron in the next layer.
- **Deconvolutional (transpose convolution) layers**: Reverse of convolution; used in image generators. Multiply by the transpose of the convolution matrix. Can produce checkerboard artifacts (fix: upscale-then-convolve).
- **Unpooling layers**: Expand spatial dimensions (reverse of pooling).
- **Dilated/atrous convolution**: Expands receptive field without increasing parameters by inserting gaps between kernel elements. Can use multiple dilation ratios in a single layer.

## Relationships

- **Feedforward neural networks**: CNNs are a specialized subtype; standard feedforward nets are fully connected and prone to overfitting on high-dimensional data.
- **Backpropagation**: The standard training algorithm for CNNs; LeCun et al. (1989) first demonstrated learning convolution kernels directly from images via backprop.
- **Transformers**: Increasingly replacing CNNs in some vision tasks (Vision Transformers); CNNs remain dominant for many image processing applications.
- **Neocognitron** (Fukushima, 1980): Architectural predecessor introducing S-layers (convolutional) and C-layers (pooling). Used unsupervised/local learning rather than backprop.
- **ReLU activation**: Introduced by Fukushima (1969) in early vision models; became the standard activation for CNNs and deep networks generally.
- **Biological vision**: Architecture inspired by Hubel and Wiesel's discovery of simple cells (orientation-selective) and complex cells (position-invariant) in the visual cortex.
- **Time Delay Neural Networks (TDNNs)**: 1D CNNs applied along the time axis; first CNN to combine weight sharing with gradient descent training (Waibel, 1987).
- **GPU computing**: CNN breakthroughs in the 2000s depended on GPU acceleration (first GPU CNN implementation: Chellapilla et al., 2006).

## Historical Timeline

- **1969**: Fukushima introduces multilayer vision network with shared weights and ReLU activation (weights not trained)
- **1980**: Fukushima's Neocognitron — first trainable CNN-like architecture with S-layers and C-layers
- **1987**: TDNN (Waibel) — first 1D CNN with weight sharing + backprop training; Homma et al. introduce "convolution" terminology in neural networks
- **1988**: Wei Zhang et al. — shift-invariant neural network trained with backprop for character recognition
- **1989**: LeCun et al. — backprop-trained 2D CNN for handwritten digit recognition
- **1990**: Yamaguchi et al. introduce max pooling in TDNNs
- **1993**: Cresceptron (Weng et al.) — max pooling applied to vision CNNs
- **1995**: LeNet-5 (LeCun) — 7-layer CNN for check digit reading, deployed in NCR banking systems (1996)
- **2004-2006**: GPU acceleration enables practical large-scale CNN training
- **2012**: AlexNet demonstrates CNN dominance on ImageNet

## Exam-Relevant Points

- A 5x5 convolutional kernel requires only **25 learnable weights** per filter, versus **10,000 weights per neuron** for a fully connected layer on a 100x100 image — this parameter reduction is a primary advantage.
- CNNs are **translation-equivariant** (feature maps shift with input) but generally **NOT translation-invariant** due to downsampling/pooling.
- The convolution operation in CNNs is technically **cross-correlation**, not mathematical convolution — the distinction doesn't affect learned results since weights are learned.
- **Depthwise separable convolution** = depthwise (spatial, per-channel) convolution followed by pointwise (1x1) convolution.
- **Deconvolution** (transpose convolution) is multiplication by the **transpose** of the convolution matrix; used in generators and segmentation. Creates **checkerboard artifacts** by default.
- **Neocognitron** (1980) introduced the two fundamental layer types: convolutional (S-layer) and pooling (C-layer).
- **LeNet-5** (1995): 7 layers, 32x32 input, handwritten digit classification — first commercially deployed CNN.
- **Max pooling** was introduced in 1990 (Yamaguchi et al.) for speech recognition, then adopted for vision in 1993 (Weng et al.).
- The TDNN (1987) was the **first CNN to combine weight sharing with backpropagation training**.
- Weight sharing provides implicit **regularization**, helping prevent vanishing/exploding gradients.
- CNN applications span: computer vision, NLP, recommender systems, medical imaging, brain-computer interfaces, financial time series.
