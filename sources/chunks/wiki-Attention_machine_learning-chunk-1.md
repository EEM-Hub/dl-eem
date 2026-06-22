---
source: sources/wiki-Attention_machine_learning.md
source_url: https://en.wikipedia.org/wiki/Attention_(machine_learning)
chunk: 1/3
---

Machine learning technique 
| Part of a series on |
| --- |
| Machine learninganddata mining |
| ParadigmsSupervised learningUnsupervised learningSemi-supervised learningSelf-supervised learningReinforcement learningMeta-learningOnline learningBatch learningCurriculum learningRule-based learningNeuro-symbolic AINeuromorphic engineeringQuantum machine learning |
| ProblemsClassificationGenerative modelingRegressionClusteringDimensionality reductionDensity estimationAnomaly detectionData cleaningAutoMLAssociation rulesSemantic analysisStructured predictionFeature engineeringFeature learningLearning to rankGrammar inductionOntology learningMultimodal learning |
| Supervised learning(classification•regression)Apprenticeship learningDecision treesEnsemblesBaggingBoostingRandom forestk-NNLinear regressionNaive BayesArtificial neural networksLogistic regressionPerceptronRelevance vector machine (RVM)Support vector machine (SVM) |
| ClusteringBIRCHCUREHierarchicalk-meansFuzzyExpectation–maximization (EM)DBSCANOPTICSMean shift |
| Dimensionality reductionFactor analysisCCAICALDANMFPCAPGDt-SNESDL |
| Structured predictionGraphical modelsBayes netConditional random fieldHidden Markov |
| Anomaly detectionRANSACk-NNLocal outlier factorIsolation forest |
| Neural networksAutoencoderDeep learningFeedforward neural networkRecurrent neural networkLSTMGRUESNreservoir computingBoltzmann machineRestrictedGANDiffusion modelSOMConvolutional neural networkU-NetLeNetAlexNetDeepDreamNeural fieldNeural radiance fieldPhysics-informed neural networksTransformerVisionMambaSpiking neural networkMemtransistorElectrochemical RAM(ECRAM) |
| Reinforcement learningQ-learningPolicy gradientSARSATemporal difference (TD)Multi-agentSelf-play |
| Learning with humansActive learningCrowdsourcingHuman-in-the-loopMechanistic interpretabilityRLHF |
| Model diagnosticsCoefficient of determinationConfusion matrixLearning curveROC curve |
| Mathematical foundationsKernel machinesBias–variance tradeoffComputational learning theoryEmpirical risk minimizationOccam learningPAC learningStatistical learningVC theoryTopological deep learning |
| Journals and conferencesAAAICVPRECCVECML PKDDEMNLPICCVNeurIPSICMLICLRIJCAIMLJMLR |
| Related articlesGlossary of artificial intelligenceList of datasets for machine-learning researchList of datasets in computer vision and image processingOutline of machine learning |
| vte |

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/6/62/Attention_mechanism_overview.svg/250px-Attention_mechanism_overview.svg.png)](./File:Attention_mechanism_overview.svg)Attention mechanism, overview 

In [machine learning](./Machine_learning), **attention** is a method that determines the importance of each component in a sequence relative to the other components in that sequence. In [natural language processing](./Natural_language_processing), importance is represented by "soft" weights assigned to each word in a sentence. More generally, attention encodes [vectors](./Vector_(mathematics_and_physics)) called [token](./Lexical_token) [embeddings](./Word_embedding) across a fixed-width [sequence](./Context_window) that can range from tens to millions of tokens in size.

 

Unlike "hard" weights, which are computed during the backwards training pass, "soft" weights exist only in the forward pass and therefore change with every step of the input. Earlier designs implemented the attention mechanism in a serial [recurrent neural network](./Recurrent_neural_network) (RNN) language translation system, but a more recent design, namely the [transformer](./Transformer_(machine_learning_model)), removed the slower sequential RNN and relied more heavily on the faster parallel attention scheme.

 

Inspired by ideas about [attention in humans](./Attention), the attention mechanism was developed to address the weaknesses of using information from the [hidden layers](./Hidden_layer) of recurrent neural networks. Recurrent neural networks favor information contained in words at the end of a sentence and thus deemed more recent, thereby tending to [attenuate](./Vanishing_gradient_problem) the significance and associated predictive weight assigned to information earlier in the sentence. Attention allows a token equal access to any part of a sentence directly, rather than only through the previous state.

 

## History

 See also: [Timeline of machine learning](./Timeline_of_machine_learning) 
| 1950s–1960s | Psychology and biology of attention.Cocktail party effect[1]— focusing on content by filtering out background noise.Filter model of attention,[2]partial report paradigm, andsaccade control.[3] |
| --- | --- |
| 1980s | Sigma-pi units,[4]higher-order neural networks. |
| 1990s | Fast weight controllersand dynamic links between neurons, anticipating key-value mechanisms in attention.[5][6][7][8] |
| 1998 | Thebilateral filterwas introduced in image processing. It uses pairwise affinity matrices to propagate relevance across elements.[9] |
| 2005 | Non-local means extended affinity-based filtering in image denoising, using Gaussian similarity kernels as fixed attention-like weights.[10] |
| 2014 | seq2seqwith RNN + Attention.[11]Attention was introduced to enhance RNN encoder-decoder translation, particularly for long sentences. See Overview section.Attentional Neural Networks introduced a learned feature selection mechanism using top-down cognitive modulation, showing how attention weights can highlight relevant inputs.[12] |
| 2015 | Attention was extended to vision for image captioning tasks.[13][14] |
| 2016 | Self-attention was integrated into RNN-based models to capture intra-sequence dependencies.[15][16]Self-attention was explored in decomposable attention models for natural language inference[17]and structured self-attentive sentence embeddings.[18] |
| 2017 | TheTransformerarchitecture introduced in the research paperAttention is All You Need[19]formalized scaled dot-product self-attention:A=softmax(QKTdk)V{\displaystyle A={\text{softmax}}\left({\frac {QK^{T}}{\sqrt {d_{k}}}}\right)V}Relation networks[20]and set Transformers[21]applied attention to unordered sets and relational reasoning, generalizing pairwise interaction models. |
| 2018 | Non-local neural networks[22]extended attention to computer vision by capturing long-range dependencies in space and time. Graph attention networks[23]applied attention mechanisms to graph-structured data. |
| 2019–2020 | Efficient Transformers, including Reformer,[24]Linformer,[25]and Performer,[26]introduced scalable approximations of attention for long sequences. |
| 2019+ | Hopfield networkswere reinterpreted as associative memory-based attention systems,[27]andvision transformers(ViTs) achieved competitive results in image classification.[28]Transformers were adopted across scientific domains, includingAlphaFoldfor protein folding,[29]CLIP for vision-language pretraining,[30]and attention-based dense segmentation models like CCNet[31]and DANet.[32] |

 

Additional surveys of the attention mechanism in deep learning are provided by Niu et al.[[33]](./Attention_(machine_learning)#cite_note-:0-33) and Soydaner.[[34]](./Attention_(machine_learning)#cite_note-:1-34)

 

The major breakthrough came with self-attention, where each element in the input sequence attends to all others, enabling the model to capture global dependencies. This idea was central to the [Transformer architecture](./Transformer_architecture), which replaced recurrence with attention mechanisms. As a result, Transformers became the foundation for models like [BERT](./BERT_(language_model)), [T5](./T5_(language_model)) and [generative pre-trained transformers](./Generative_pre-trained_transformer) (GPT).[[19]](./Attention_(machine_learning)#cite_note-allyouneed-19)

 

## Overview

 
|  | This articlemay containoriginal research.Pleaseimprove itbyverifyingthe claims made and addinginline citations. Statements consisting only of original research should be removed.(June 2025)(Learn how and when to remove this message) |
| --- | --- |

 

The modern era of machine attention was revitalized by grafting an attention mechanism (Fig 1.  orange) to an Encoder-Decoder.[*[citation needed](./Wikipedia:Citation_needed)*]

 
| Animated sequence of language translation | Fig 1.  Encoder-decoder with attention.[35]Numerical subscripts (100, 300, 500, 9k, 10k) indicate vector sizes while lettered subscripts i and i − 1 indicate time steps.  Pinkish regions in H matrix and w vector are zero values.  See Legend for details.LegendLabelDescription100Max. sentence length300Embeddingsize (word dimension)500Length of hidden vector9k, 10kDictionary size of input & output languages respectively.x,Y9k and 10k1-hotdictionary vectors.x→ x implemented as alookup tablerather than vector multiplication.Yis the 1-hot maximizer of the linear Decoder layer D; that is, it takes the argmax of D's linear layer output.x300-long word embedding vector.  The vectors are usually pre-calculated from other projects such asGloVeorWord2Vec.h500-long encoder hidden vector.  At each point in time, this vector summarizes all the preceding words before it.  The final h can be viewed as a "sentence" vector, or athought vectoras Hinton calls it.s500-long decoder hidden state vector.E500 neuronrecurrent neural networkencoder.  500 outputs.  Input count is 800–300 from source embedding + 500 from recurrent connections.  The encoder feeds directly into the decoder only to initialize it, but not thereafter; hence, that direct connection is shown very faintly.D2-layer decoder.  The recurrent layer has 500 neurons and the fully-connected linear layer has 10k neurons (the size of the target vocabulary).[36]The linear layer alone has 5 million (500 × 10k) weights – ~10 times more weights than the recurrent layer.score100-long alignment scorew100-long vector attention weight.  These are "soft" weights which changes during the forward pass, in contrast to "hard" neuronal weights that change during the learning phase.AAttention module – this can be a dot product of recurrent states, or the query-key-value fully-connected layers.  The output is a 100-long vector w.H500×100. 100 hidden vectors h concatenated into a matrixc500-long context vector = H * w.  c is a linear combination of h vectors weighted by w. | Label | Description | 100 | Max. sentence length | 300 | Embeddingsize (word dimension) | 500 | Length of hidden vector | 9k, 10k | Dictionary size of input & output languages respectively. | x,Y | 9k and 10k1-hotdictionary vectors.x→ x implemented as alookup tablerather than vector multiplication.Yis the 1-hot maximizer of the linear Decoder layer D; that is, it takes the argmax of D's linear layer output. | x | 300-long word embedding vector.  The vectors are usually pre-calculated from other projects such asGloVeorWord2Vec. | h | 500-long encoder hidden vector.  At each point in time, this vector summarizes all the preceding words before it.  The final h can be viewed as a "sentence" vector, or athought vectoras Hinton calls it. | s | 500-long decoder hidden state vector. | E | 500 neuronrecurrent neural networkencoder.  500 outputs.  Input count is 800–300 from source embedding + 500 from recurrent connections.  The encoder feeds directly into the decoder only to initialize it, but not thereafter; hence, that direct connection is shown very faintly. | D | 2-layer decoder.  The recurrent layer has 500 neurons and the fully-connected linear layer has 10k neurons (the size of the target vocabulary).[36]The linear layer alone has 5 million (500 × 10k) weights – ~10 times more weights than the recurrent layer. | score | 100-long alignment score | w | 100-long vector attention weight.  These are "soft" weights which changes during the forward pass, in contrast to "hard" neuronal weights that change during the learning phase. | A | Attention module – this can be a dot product of recurrent states, or the query-key-value fully-connected layers.  The output is a 100-long vector w. | H | 500×100. 100 hidden vectors h concatenated into a matrix | c | 500-long context vector = H * w.  c is a linear combination of h vectors weighted by w. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Label | Description |
| 100 | Max. sentence length |
| 300 | Embeddingsize (word dimension) |
| 500 | Length of hidden vector |
| 9k, 10k | Dictionary size of input & output languages respectively. |
| x,Y | 9k and 10k1-hotdictionary vectors.x→ x implemented as alookup tablerather than vector multiplication.Yis the 1-hot maximizer of the linear Decoder layer D; that is, it takes the argmax of D's linear layer output. |
| x | 300-long word embedding vector.  The vectors are usually pre-calculated from other projects such asGloVeorWord2Vec. |
| h | 500-long encoder hidden vector.  At each point in time, this vector summarizes all the preceding words before it.  The final h can be viewed as a "sentence" vector, or athought vectoras Hinton calls it. |
| s | 500-long decoder hidden state vector. |
| E | 500 neuronrecurrent neural networkencoder.  500 outputs.  Input count is 800–300 from source embedding + 500 from recurrent connections.  The encoder feeds directly into the decoder only to initialize it, but not thereafter; hence, that direct connection is shown very faintly. |
| D | 2-layer decoder.  The recurrent layer has 500 neurons and the fully-connected linear layer has 10k neurons (the size of the target vocabulary).[36]The linear layer alone has 5 million (500 × 10k) weights – ~10 times more weights than the recurrent layer. |
| score | 100-long alignment score |
| w | 100-long vector attention weight.  These are "soft" weights which changes during the forward pass, in contrast to "hard" neuronal weights that change during the learning phase. |
| A | Attention module – this can be a dot product of recurrent states, or the query-key-value fully-connected layers.  The output is a 100-long vector w. |
| H | 500×100. 100 hidden vectors h concatenated into a matrix |
| c | 500-long context vector = H * w.  c is a linear combination of h vectors weighted by w. |

 

Figure 2 shows the internal step-by-step operation of the attention block (A) in Fig 1.

  [![](//upload.wikimedia.org/wikipedia/commons/thumb/8/81/Attention-qkv.png/960px-Attention-qkv.png)](./File:Attention-qkv.png) Figure 2.  The diagram shows the attention forward pass calculating correlations of the word "that" with other words in "See that girl run."  Given the right weights from training, the network should be able to identify "girl" as a highly correlated word.  Some things to note:

- This example focuses on the attention of a single word "that".  In practice, the attention of each word is calculated in parallel to speed up calculations.  Simply changing the lowercase "x" vector to the uppercase "X" matrix will yield the formula for this.
- Softmax scaling qWkT / √100 prevents a high variance in qWkT that would allow a single word to excessively dominate the softmax resulting in attention to only one word, as a discrete hard max would do.
- Notation: the commonly written row-wise softmax formula above assumes that vectors are rows, which runs contrary to the standard math notation of column vectors. More correctly, we should take the transpose of the context vector and use the column-wise softmax, resulting in the more correct form

         ( X  W  v    )  T   ∗ ∗   [ (  W  k    X  T   ) ∗ ∗   (   x _ _     W  q    )  T     ]  s m          {\displaystyle {\begin{aligned}(XW_{v})^{T}*{[(W_{k}X^{T})*{({\underline {x}}W_{q})^{T}}]_{sm}}\end{aligned}}}  ![{\displaystyle {\begin{aligned}(XW_{v})^{T}*{[(W_{k}X^{T})*{({\underline {x}}W_{q})^{T}}]_{sm}}\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1adff6d5e9decb390b437b6bd3d0b35ad2791406). 

### Interpreting attention weights

 

In translating between languages, alignment is the process of matching words from the source sentence to words of the translated sentence. Networks that perform verbatim translation without regard to word order would show the highest scores along the (dominant) diagonal of the matrix. The off-diagonal dominance shows that the attention mechanism is more nuanced.

 

Consider an example of translating *I love you* to French. On the first pass through the decoder, 94% of the attention weight is on the first English word *I*, so the network offers the word *je*. On the second pass of the decoder, 88% of the attention weight is on the third English word *you*, so it offers *t'*. On the last pass, 95% of the attention weight is on the second English word *love*, so it offers *aime*.

 

In the *I love you* example, the second word *love* is aligned with the third word *aime*. Stacking soft row vectors together for *je*, *t'*, and *aime* yields an [alignment matrix](./Statistical_machine_translation#Word_alignment):

 
|  | I | love | you |
| --- | --- | --- | --- |
| je | 0.94 | 0.02 | 0.04 |
| t' | 0.11 | 0.01 | 0.88 |
| aime | 0.03 | 0.95 | 0.02 |

 

Sometimes, alignment can be multiple-to-multiple. For example, the English phrase *look it up* corresponds to *cherchez-le*. Thus, "soft" attention weights work better than "hard" attention weights (setting one attention weight to 1, and the others to 0), as we would like the model to make a context vector consisting of a weighted sum of the hidden vectors, rather than "the best one", as there may not be a best hidden vector.

 

## Variants

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/d7/Self-attention_in_CNN%2C_RNN%2C_and_self-attention.svg/250px-Self-attention_in_CNN%2C_RNN%2C_and_self-attention.svg.png)](./File:Self-attention_in_CNN,_RNN,_and_self-attention.svg)Comparison of the data flow in CNN, RNN, and self-attention 

Many variants of attention implement soft weights, such as

 
- fast weight programmers, or fast weight controllers (1992).[[5]](./Attention_(machine_learning)#cite_note-transform1992-5) A "slow" [neural network](./Neural_network) outputs the "fast" weights of another neural network through [outer products](./Outer_product). The slow network learns by gradient descent. It was later renamed as "linearized self-attention".[[37]](./Attention_(machine_learning)#cite_note-schlag2021-37)
- Bahdanau-style attention,[[11]](./Attention_(machine_learning)#cite_note-bahdanau-11) also referred to as *additive attention*,
- Luong-style attention,[[38]](./Attention_(machine_learning)#cite_note-xy-dot-38) which is known as *multiplicative attention*,
- Early attention mechanisms similar to modern self-attention were proposed using recurrent neural networks. However, the highly parallelizable self-attention was introduced in 2017 and successfully used in the Transformer model,
- *positional attention* and *factorized positional attention*.[[39]](./Attention_(machine_learning)#cite_note-luo-39)

 

For [convolutional neural networks](./Convolutional_neural_network), attention mechanisms can be distinguished by the dimension on which they operate, namely: spatial attention,[[40]](./Attention_(machine_learning)#cite_note-xzhu1-40) channel attention,[[41]](./Attention_(machine_learning)#cite_note-jhu1-41) or combinations.[[42]](./Attention_(machine_learning)#cite_note-psanghyun1-42)[[43]](./Attention_(machine_learning)#cite_note-mgeorgescu-43)

There are many variants of attention: dot product, query&#x2D;key&#x2D;value,<ref name="allyouneed" /&#x3E; hard, soft, self, cross, Luong,<ref name="xy&#x2D;dot" /&#x3E; and Bahdanau<ref name=Bahdanau /&#x3E; to name a few.
 

These variants recombine the encoder-side inputs to redistribute those effects to each target output. Often, a correlation-style matrix of dot products provides the re-weighting coefficients.  In the figures below, W is the matrix of context attention weights, similar to the formula in Overview section above.

 
| 1. encoder-decoder dot product | 2. encoder-decoder QKV | 3. encoder-only dot product | 4. encoder-only QKV | 5. Pytorch tutorial |
| --- | --- | --- | --- | --- |
| Both encoder & decoder are needed to calculate attention.[38] | Both encoder & decoder are needed to calculate attention.[44] | Decoder isnotused to calculate attention. With only 1 input into corr, W is an auto-correlation of dot products. wij= xixj.[45] | Decoder isnotused to calculate attention.[46] | A fully-connected layer is used to calculate attention instead of dot product correlation.[47] |

 
| Label | Description |
| --- | --- |
| Variables X, H, S, T | Upper case variables represent the entire sentence, and not just the current word. For example, H is a matrix of the encoder hidden state—one word per column. |
| S, T | S, decoder hidden state; T, target word embedding. In thePytorchTutorial variant training phase, T alternates between 2 sources depending on the level ofteacher forcingused. T could be the embedding of the network's output word; i.e. embedding(argmax(FC output)). Alternatively with teacher forcing, T could be the embedding of the known correct word which can occur with a constant forcing probability, say 1/2. |
| X, H | H, encoder hidden state; X, input word embeddings. |
| W | Attention coefficients |
| Qw, Kw, Vw, FC | Weight matrices for query, key, value respectively. FC is a fully-connected weight matrix. |
| ⊕, ⊗ | ⊕, vector concatenation; ⊗, matrix multiplication. |
| corr | Column-wise softmax(matrix of all combinations of dot products). The dot products arexi* xjin variant #3,hi* sjin variant 1, and columni( Kw * H ) * columnj( Qw * S ) in variant 2, and columni( Kw * X ) * columnj( Qw * X ) in variant 4. Variant 5 uses a fully-connected layer to determine the coefficients. If the variant is QKV, then the dot products are normalized by the√dwheredis the height of the QKV matrices. |

 

## Optimizations

 

### Flash attention

 

The size of the attention matrix is proportional to the square of the number of input tokens. Therefore, when the input is long, calculating the attention matrix requires a lot of [GPU](./GPU) memory. Flash attention is an implementation that reduces the memory needs and increases efficiency without sacrificing accuracy. It achieves this by partitioning the attention computation into smaller blocks that fit into the GPU's faster on-chip memory, reducing the need to store large intermediate matrices and thus lowering memory usage while increasing computational efficiency.[[48]](./Attention_(machine_learning)#cite_note-48)

 

### FlexAttention

 

FlexAttention[[49]](./Attention_(machine_learning)#cite_note-49) is an attention kernel developed by [Meta](./Meta_Platforms) that allows users to modify attention scores prior to [softmax](./Softmax) and dynamically chooses the optimal attention algorithm.

 

## Applications

 

Attention is widely used in natural language processing, computer vision, and speech recognition. In NLP, it improves context understanding in tasks like question answering and summarization. In vision, visual attention helps models focus on relevant image regions, enhancing object detection and image captioning.

 

### Attention maps as explanations for vision transformers

 See also: [Saliency map](./Saliency_map) and [Mechanistic interpretability](./Mechanistic_interpretability) 

From the original paper on [vision transformers](./Vision_transformer) (ViT), visualizing attention scores as a heat map (called [saliency maps](./Saliency_map) or attention maps) has become an important and routine way to inspect the decision making process of ViT models.[[50]](./Attention_(machine_learning)#cite_note-50) One can compute the attention maps with respect to any attention head at any layer, while the deeper layers tend to show more semantically meaningful visualization. Attention rollout is a recursive algorithm to combine attention scores across all layers, by computing the dot product of successive attention maps.[[51]](./Attention_(machine_learning)#cite_note-51)

 

Because vision transformers are typically trained in a [self-supervised](./Self-supervised_learning) manner, attention maps are generally not class-sensitive. When a classification head is attached to the ViT backbone, class-discriminative attention maps (CDAM) combines attention maps and gradients with respect to the class `[CLS]` token.[[52]](./Attention_(machine_learning)#cite_note-52) Some class-sensitive [interpretability](./Interpretability_(machine_learning)) methods originally developed for [convolutional neural networks](./Convolutional_neural_network) can be also applied to ViT, such as GradCAM, which [back-propagates](./Backpropagation) the gradients to the outputs of the final attention layer.[[53]](./Attention_(machine_learning)#cite_note-53)

 

Using attention as basis of explanation for the transformers in language and vision is not without debate. While some pioneering papers analyzed and framed attention scores as explanations,[[54]](./Attention_(machine_learning)#cite_note-54)[[55]](./Attention_(machine_learning)#cite_note-55) higher attention scores do not always correlate with greater impact on model performances.[[56]](./Attention_(machine_learning)#cite_note-56)

 


