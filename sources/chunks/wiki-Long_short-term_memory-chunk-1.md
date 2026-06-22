---
source: sources/wiki-Long_short-term_memory.md
source_url: https://en.wikipedia.org/wiki/Long_short-term_memory
chunk: 1/4
---

Recurrent neural network architecture "LSTM" redirects here. For other uses, see [LSTM (disambiguation)](./LSTM_(disambiguation)). 
|  | This articlemay be too technical for most readers to understand.Pleasehelp improve ittomake it understandable to non-experts, without removing the technical details.(March 2022)(Learn how and when to remove this message) |
| --- | --- |

 
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

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/7d/NN_LSTM-Cell_v2.svg/330px-NN_LSTM-Cell_v2.svg.png)](./File:NN_LSTM-Cell_v2.svg)The long short-term memory (LSTM) cell can process data sequentially and keep its hidden state through time. 

**Long short-term memory** (**LSTM**)[[1]](./Long_short-term_memory#cite_note-lstm1997-1) is a type of [recurrent neural network](./Recurrent_neural_network) (RNN) aimed at mitigating the [vanishing gradient problem](./Vanishing_gradient_problem)[[2]](./Long_short-term_memory#cite_note-hochreiter1991-2) commonly encountered by traditional RNNs. Its relative insensitivity to gap length is its advantage over other RNNs, [hidden Markov models](./Hidden_Markov_models), and other sequence learning methods. It aims to provide a short-term memory for RNN that can last thousands of timesteps (thus "*long* short-term memory").[[1]](./Long_short-term_memory#cite_note-lstm1997-1) The name is made in analogy with [long-term memory](./Long-term_memory) and [short-term memory](./Short-term_memory) and their relationship, studied by cognitive psychologists since the early 20th century.

 

An LSTM unit is typically composed of a cell and three [gates](./Gating_mechanism): an input gate, an output gate,[[3]](./Long_short-term_memory#cite_note-hochreiter1996-3) and a forget gate.[[4]](./Long_short-term_memory#cite_note-lstm2000-4) The cell remembers values over arbitrary time intervals, and the gates regulate the flow of information into and out of the cell. Forget gates decide what information to discard from the previous state, by mapping the previous state and the current input to a value between 0 and 1. A (rounded) value of 1 signifies retention of the information, and a value of 0 represents discarding. Input gates decide which pieces of new information to store in the current cell state, using the same system as forget gates. Output gates control which pieces of information in the current cell state to output, by assigning a value from 0 to 1 to the information, considering the previous and current states. Selectively outputting relevant information from the current state allows the LSTM network to maintain useful, long-term dependencies to make predictions, both in current and future time-steps.

 

LSTM has wide applications in [classification](./Classification_in_machine_learning),[[5]](./Long_short-term_memory#cite_note-graves2006-5)[[6]](./Long_short-term_memory#cite_note-6) [data processing](./Data_processing), [time series](./Time_series) analysis tasks,[[7]](./Long_short-term_memory#cite_note-wierstra2005-7) [speech recognition](./Speech_recognition),[[8]](./Long_short-term_memory#cite_note-sak2014-8)[[9]](./Long_short-term_memory#cite_note-liwu2015-9) [machine translation](./Machine_translation),[[10]](./Long_short-term_memory#cite_note-GoogleTranslate-10)[[11]](./Long_short-term_memory#cite_note-FacebookTranslate-11) speech activity detection,[[12]](./Long_short-term_memory#cite_note-12) [robot control](./Robot_control),[[13]](./Long_short-term_memory#cite_note-mayer2006-13)[[14]](./Long_short-term_memory#cite_note-OpenAIhand-14) [video games](./Video_game),[[15]](./Long_short-term_memory#cite_note-OpenAIfive-15)[[16]](./Long_short-term_memory#cite_note-alphastar-16) [healthcare](./Healthcare),[[17]](./Long_short-term_memory#cite_note-decade2022-17) [energy forecasting](./Energy_forecasting).[[18]](./Long_short-term_memory#cite_note-AMVT-18)

 

## Motivation

 

In theory, classic [RNNs](./Recurrent_neural_network) can keep track of arbitrary long-term dependencies in the input sequences. The problem with classic RNNs is computational (or practical) in nature: when training a classic RNN using [back-propagation](./Back-propagation), the long-term gradients which are back-propagated can ["vanish"](./Vanishing_gradient_problem), meaning they can tend to zero due to very small numbers creeping into the computations, causing the model to effectively stop learning. RNNs using LSTM units partially solve the [vanishing gradient problem](./Vanishing_gradient_problem), because LSTM units allow gradients to also flow with little to no attenuation. However, LSTM networks can still suffer from the exploding gradient problem.[[19]](./Long_short-term_memory#cite_note-calin2020-19)

 

The intuition behind the LSTM architecture is to create an additional module in a neural network that learns when to remember and when to forget pertinent information.[[4]](./Long_short-term_memory#cite_note-lstm2000-4) In other words, the network effectively learns which information might be needed later on in a sequence and when that information is no longer needed. For instance, in the context of [natural language processing](./Natural_language_processing), the network can learn grammatical dependencies.[[20]](./Long_short-term_memory#cite_note-LakretzKruszewskiDesbordes2019-20) An LSTM might process the sentence "Dave, as a result of his controversial claims, is now a pariah" by remembering the (statistically likely) grammatical gender and number of the subject *Dave*. Note that this information is pertinent for the pronoun *his* and note that this information is no longer important after the verb *is*.

 

## Variants

 

In the equations below, the lowercase variables represent vectors. Matrices      W  q     {\displaystyle W_{q}}  ![{\displaystyle W_{q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d16355ad959593cf720b24fffe62d99af53d15d9) and      U  q     {\displaystyle U_{q}}  ![{\displaystyle U_{q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/05e27486afb11613504d6d6b9f6bd72e322607c8) contain, respectively, the weights of the input and recurrent connections, where the subscript        q     {\displaystyle _{q}}  ![{\displaystyle _{q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e333a711146f91533eb5a030accc0e90948e4f92) can either be the input gate     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20), output gate     o   {\displaystyle o}  ![{\displaystyle o}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0c1031f61947aa3d1cf3a70ec3e4904df2c3675d), the forget gate     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) or the memory cell     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455), depending on the activation being calculated. In this section, we are thus using a "vector notation". So, for example,      c  t   ∈ ∈    R   h     {\displaystyle c_{t}\in \mathbb {R} ^{h}}  ![{\displaystyle c_{t}\in \mathbb {R} ^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65d6f2af820422ed59a0f14af91eee7498ebc4a2) is not just one unit of one LSTM cell, but contains     h   {\displaystyle h}  ![{\displaystyle h}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b26be3e694314bc90c3215047e4a2010c6ee184a) LSTM cell's units.

 

### LSTM with a forget gate (crucial)

 

The compact forms of the equations for the forward pass of an LSTM cell with a forget gate are:[[1]](./Long_short-term_memory#cite_note-lstm1997-1)[[4]](./Long_short-term_memory#cite_note-lstm2000-4)

          f  t      =  σ σ   g   (  W  f    x  t   +  U  f    h  t − −  1   +  b  f   )      i  t      =  σ σ   g   (  W  i    x  t   +  U  i    h  t − −  1   +  b  i   )      o  t      =  σ σ   g   (  W  o    x  t   +  U  o    h  t − −  1   +  b  o   )         c ~ ~      t      =  σ σ   c   (  W  c    x  t   +  U  c    h  t − −  1   +  b  c   )      c  t      =  f  t   ⊙ ⊙   c  t − −  1   +  i  t   ⊙ ⊙      c ~ ~      t        h  t      =  o  t   ⊙ ⊙   σ σ   h   (  c  t   )       {\displaystyle {\begin{aligned}f_{t}&=\sigma _{g}(W_{f}x_{t}+U_{f}h_{t-1}+b_{f})\\i_{t}&=\sigma _{g}(W_{i}x_{t}+U_{i}h_{t-1}+b_{i})\\o_{t}&=\sigma _{g}(W_{o}x_{t}+U_{o}h_{t-1}+b_{o})\\{\tilde {c}}_{t}&=\sigma _{c}(W_{c}x_{t}+U_{c}h_{t-1}+b_{c})\\c_{t}&=f_{t}\odot c_{t-1}+i_{t}\odot {\tilde {c}}_{t}\\h_{t}&=o_{t}\odot \sigma _{h}(c_{t})\end{aligned}}}  ![{\displaystyle {\begin{aligned}f_{t}&=\sigma _{g}(W_{f}x_{t}+U_{f}h_{t-1}+b_{f})\\i_{t}&=\sigma _{g}(W_{i}x_{t}+U_{i}h_{t-1}+b_{i})\\o_{t}&=\sigma _{g}(W_{o}x_{t}+U_{o}h_{t-1}+b_{o})\\{\tilde {c}}_{t}&=\sigma _{c}(W_{c}x_{t}+U_{c}h_{t-1}+b_{c})\\c_{t}&=f_{t}\odot c_{t-1}+i_{t}\odot {\tilde {c}}_{t}\\h_{t}&=o_{t}\odot \sigma _{h}(c_{t})\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dc89390b3136ccbbc223a1ed110c6d2b4856069c) 

where the initial values are      c  0   = 0   {\displaystyle c_{0}=0}  ![{\displaystyle c_{0}=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/29af3d4e887815bb3b9b9eab4f7540a376fccd73) and      h  0   = 0   {\displaystyle h_{0}=0}  ![{\displaystyle h_{0}=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/14a294b6cf9cbde4c37efd966913a63d316e615c) and the operator     ⊙ ⊙    {\displaystyle \odot }  ![{\displaystyle \odot }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e89e009eb8a8839c82aa5c76c15e9f2d67006276) denotes the [Hadamard product](./Hadamard_product_(matrices)) (element-wise product). The subscript     t   {\displaystyle t}  ![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) indexes the time step.

 

#### Variables

 

Letting the superscripts     d   {\displaystyle d}  ![{\displaystyle d}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e85ff03cbe0c7341af6b982e47e9f90d235c66ab) and     h   {\displaystyle h}  ![{\displaystyle h}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b26be3e694314bc90c3215047e4a2010c6ee184a) refer to the number of input features and number of hidden units, respectively:

 
-      x  t   ∈ ∈    R   d     {\displaystyle x_{t}\in \mathbb {R} ^{d}}  ![{\displaystyle x_{t}\in \mathbb {R} ^{d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d528d57c5517e90795e0a6d6760463564236fee7): input vector to the LSTM unit
-      f  t   ∈ ∈    ( 0 , 1 )   h     {\displaystyle f_{t}\in {(0,1)}^{h}}  ![{\displaystyle f_{t}\in {(0,1)}^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6801986d2383af655b5ba1ca1c48b535b4f60bbf): forget gate's activation vector
-      i  t   ∈ ∈    ( 0 , 1 )   h     {\displaystyle i_{t}\in {(0,1)}^{h}}  ![{\displaystyle i_{t}\in {(0,1)}^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e8cb1a28fcd328d06438c80be6308b6a3ccdc5d7): input/update gate's activation vector
-      o  t   ∈ ∈    ( 0 , 1 )   h     {\displaystyle o_{t}\in {(0,1)}^{h}}  ![{\displaystyle o_{t}\in {(0,1)}^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f3961562e04e80ad79e482894135770237ce7a59): output gate's activation vector
-      h  t   ∈ ∈    ( − −  1 , 1 )   h     {\displaystyle h_{t}\in {(-1,1)}^{h}}  ![{\displaystyle h_{t}\in {(-1,1)}^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ca986de16d69ffdecaa766c76306d30c406f57fa): hidden state vector also known as output vector of the LSTM unit
-         c ~ ~      t   ∈ ∈    ( − −  1 , 1 )   h     {\displaystyle {\tilde {c}}_{t}\in {(-1,1)}^{h}}  ![{\displaystyle {\tilde {c}}_{t}\in {(-1,1)}^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/df821ed31ee4133fc9a3a272008dfcb43279c204): cell input activation vector
-      c  t   ∈ ∈    R   h     {\displaystyle c_{t}\in \mathbb {R} ^{h}}  ![{\displaystyle c_{t}\in \mathbb {R} ^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65d6f2af820422ed59a0f14af91eee7498ebc4a2): cell state vector
-     W ∈ ∈    R   h × ×  d     {\displaystyle W\in \mathbb {R} ^{h\times d}}  ![{\displaystyle W\in \mathbb {R} ^{h\times d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/925afdb42f13f1d912db87ecda65135eb9fe6352),     U ∈ ∈    R   h × ×  h     {\displaystyle U\in \mathbb {R} ^{h\times h}}  ![{\displaystyle U\in \mathbb {R} ^{h\times h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0ff9bb53a5409a1e51f6130b3dfbcdad63324880) and     b ∈ ∈    R   h     {\displaystyle b\in \mathbb {R} ^{h}}  ![{\displaystyle b\in \mathbb {R} ^{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/289515b23d7df7e2e09f2ee38951abf345e60080): weight matrices and bias vector parameters which need to be learned during training

 

#### [Activation functions](./Activation_function)

 
-      σ σ   g     {\displaystyle \sigma _{g}}  ![{\displaystyle \sigma _{g}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/086f92de077f853afd7f5d22fb3d305cbf5e0ac3): [sigmoid function](./Sigmoid_function).
-      σ σ   c     {\displaystyle \sigma _{c}}  ![{\displaystyle \sigma _{c}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b436b43abda74fce1a6859e03d34c914c6a240f4): [hyperbolic tangent](./Hyperbolic_tangent) function.
-      σ σ   h     {\displaystyle \sigma _{h}}  ![{\displaystyle \sigma _{h}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8a7f19495f5a65d26570b54b7ca332956d27b27b): hyperbolic tangent function or, as the peephole LSTM paper[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[22]](./Long_short-term_memory#cite_note-peephole2002-22) suggests,      σ σ   h   ( x ) = x   {\displaystyle \sigma _{h}(x)=x}  ![{\displaystyle \sigma _{h}(x)=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/98d34299f4e04f10f7c22e1219bf182712c3e0fc).

 

### Peephole LSTM

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/5/53/Peephole_Long_Short-Term_Memory.svg/330px-Peephole_Long_Short-Term_Memory.svg.png)](./File:Peephole_Long_Short-Term_Memory.svg)A peephole LSTM unit with input (i.e.     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20)), output (i.e.     o   {\displaystyle o}  ![{\displaystyle o}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0c1031f61947aa3d1cf3a70ec3e4904df2c3675d)), and forget (i.e.     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61)) gates 

The figure on the right is a graphical representation of an LSTM unit with peephole connections (i.e. a peephole LSTM).[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[22]](./Long_short-term_memory#cite_note-peephole2002-22) Peephole connections allow the gates to access the constant error carousel (CEC), whose activation is the cell state.[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)      h  t − −  1     {\displaystyle h_{t-1}}  ![{\displaystyle h_{t-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cf56fc7e1114417475762546403f3d66460975d0) is not used,      c  t − −  1     {\displaystyle c_{t-1}}  ![{\displaystyle c_{t-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b5dbc0177993c2ebd927aee23d88bd263770532) is used instead in most places.

          f  t      =  σ σ   g   (  W  f    x  t   +  U  f    c  t − −  1   +  b  f   )      i  t      =  σ σ   g   (  W  i    x  t   +  U  i    c  t − −  1   +  b  i   )      o  t      =  σ σ   g   (  W  o    x  t   +  U  o    c  t − −  1   +  b  o   )      c  t      =  f  t   ⊙ ⊙   c  t − −  1   +  i  t   ⊙ ⊙   σ σ   c   (  W  c    x  t   +  b  c   )      h  t      =  o  t   ⊙ ⊙   σ σ   h   (  c  t   )       {\displaystyle {\begin{aligned}f_{t}&=\sigma _{g}(W_{f}x_{t}+U_{f}c_{t-1}+b_{f})\\i_{t}&=\sigma _{g}(W_{i}x_{t}+U_{i}c_{t-1}+b_{i})\\o_{t}&=\sigma _{g}(W_{o}x_{t}+U_{o}c_{t-1}+b_{o})\\c_{t}&=f_{t}\odot c_{t-1}+i_{t}\odot \sigma _{c}(W_{c}x_{t}+b_{c})\\h_{t}&=o_{t}\odot \sigma _{h}(c_{t})\end{aligned}}}  ![{\displaystyle {\begin{aligned}f_{t}&=\sigma _{g}(W_{f}x_{t}+U_{f}c_{t-1}+b_{f})\\i_{t}&=\sigma _{g}(W_{i}x_{t}+U_{i}c_{t-1}+b_{i})\\o_{t}&=\sigma _{g}(W_{o}x_{t}+U_{o}c_{t-1}+b_{o})\\c_{t}&=f_{t}\odot c_{t-1}+i_{t}\odot \sigma _{c}(W_{c}x_{t}+b_{c})\\h_{t}&=o_{t}\odot \sigma _{h}(c_{t})\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fc535506b930c709edeefd4d6f24e45d0f2249ae) 

Each of the gates can be thought as a "standard" neuron in a feed-forward (or multi-layer) neural network: that is, they compute an activation (using an activation function) of a weighted sum.      i  t   ,  o  t     {\displaystyle i_{t},o_{t}}  ![{\displaystyle i_{t},o_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cf0b0dee7b12fd921a114101ff11c83e1606a1f8) and      f  t     {\displaystyle f_{t}}  ![{\displaystyle f_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/874c306411e808e8191e8aeb95e3440e1c68d6e9) represent the activations of respectively the input, output and forget gates, at time step     t   {\displaystyle t}  ![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560).

 

The 3 exit arrows from the memory cell     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) to the 3 gates     i , o   {\displaystyle i,o}  ![{\displaystyle i,o}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4697b39f565cd54942b9f81d5de46dcdd1174528) and     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) represent the *peephole* connections. These peephole connections actually denote the contributions of the activation of the memory cell     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) at time step     t − −  1   {\displaystyle t-1}  ![{\displaystyle t-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a215d9553945bb84b3b5a79cc796fb7d6e0629f0), i.e. the contribution of      c  t − −  1     {\displaystyle c_{t-1}}  ![{\displaystyle c_{t-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b5dbc0177993c2ebd927aee23d88bd263770532) (and not      c  t     {\displaystyle c_{t}}  ![{\displaystyle c_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/93578e37f3234419a34df79845836bc0ec5ef76c), as the picture may suggest). In other words, the gates     i , o   {\displaystyle i,o}  ![{\displaystyle i,o}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4697b39f565cd54942b9f81d5de46dcdd1174528) and     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) calculate their activations at time step     t   {\displaystyle t}  ![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) (i.e., respectively,      i  t   ,  o  t     {\displaystyle i_{t},o_{t}}  ![{\displaystyle i_{t},o_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cf0b0dee7b12fd921a114101ff11c83e1606a1f8) and      f  t     {\displaystyle f_{t}}  ![{\displaystyle f_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/874c306411e808e8191e8aeb95e3440e1c68d6e9)) also considering the activation of the memory cell     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) at time step     t − −  1   {\displaystyle t-1}  ![{\displaystyle t-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a215d9553945bb84b3b5a79cc796fb7d6e0629f0), i.e.      c  t − −  1     {\displaystyle c_{t-1}}  ![{\displaystyle c_{t-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b5dbc0177993c2ebd927aee23d88bd263770532).

 

The single left-to-right arrow exiting the memory cell is *not* a peephole connection and denotes      c  t     {\displaystyle c_{t}}  ![{\displaystyle c_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/93578e37f3234419a34df79845836bc0ec5ef76c).

 

The little circles containing a     × ×    {\displaystyle \times }  ![{\displaystyle \times }](https://wikimedia.org/api/rest_v1/media/math/render/svg/0ffafff1ad26cbe49045f19a67ce532116a32703) symbol represent an element-wise multiplication between its inputs. The big circles containing an *S*-like curve represent the application of a differentiable function (like the sigmoid function) to a weighted sum.

 

### Peephole convolutional LSTM

 

Peephole [convolutional](./Convolutional_neural_network) LSTM.[[23]](./Long_short-term_memory#cite_note-shi2015-23) The     ∗ ∗    {\displaystyle *}  ![{\displaystyle *}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8e9972f426d9e07855984f73ee195a21dbc21755) denotes the [convolution](./Convolution) operator.

          f  t      =  σ σ   g   (  W  f   ∗ ∗   x  t   +  U  f   ∗ ∗   h  t − −  1   +  V  f   ⊙ ⊙   c  t − −  1   +  b  f   )      i  t      =  σ σ   g   (  W  i   ∗ ∗   x  t   +  U  i   ∗ ∗   h  t − −  1   +  V  i   ⊙ ⊙   c  t − −  1   +  b  i   )      c  t      =  f  t   ⊙ ⊙   c  t − −  1   +  i  t   ⊙ ⊙   σ σ   c   (  W  c   ∗ ∗   x  t   +  U  c   ∗ ∗   h  t − −  1   +  b  c   )      o  t      =  σ σ   g   (  W  o   ∗ ∗   x  t   +  U  o   ∗ ∗   h  t − −  1   +  V  o   ⊙ ⊙   c  t   +  b  o   )      h  t      =  o  t   ⊙ ⊙   σ σ   h   (  c  t   )       {\displaystyle {\begin{aligned}f_{t}&=\sigma _{g}(W_{f}*x_{t}+U_{f}*h_{t-1}+V_{f}\odot c_{t-1}+b_{f})\\i_{t}&=\sigma _{g}(W_{i}*x_{t}+U_{i}*h_{t-1}+V_{i}\odot c_{t-1}+b_{i})\\c_{t}&=f_{t}\odot c_{t-1}+i_{t}\odot \sigma _{c}(W_{c}*x_{t}+U_{c}*h_{t-1}+b_{c})\\o_{t}&=\sigma _{g}(W_{o}*x_{t}+U_{o}*h_{t-1}+V_{o}\odot c_{t}+b_{o})\\h_{t}&=o_{t}\odot \sigma _{h}(c_{t})\end{aligned}}}  ![{\displaystyle {\begin{aligned}f_{t}&=\sigma _{g}(W_{f}*x_{t}+U_{f}*h_{t-1}+V_{f}\odot c_{t-1}+b_{f})\\i_{t}&=\sigma _{g}(W_{i}*x_{t}+U_{i}*h_{t-1}+V_{i}\odot c_{t-1}+b_{i})\\c_{t}&=f_{t}\odot c_{t-1}+i_{t}\odot \sigma _{c}(W_{c}*x_{t}+U_{c}*h_{t-1}+b_{c})\\o_{t}&=\sigma _{g}(W_{o}*x_{t}+U_{o}*h_{t-1}+V_{o}\odot c_{t}+b_{o})\\h_{t}&=o_{t}\odot \sigma _{h}(c_{t})\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/84eefaa4a824754340378effe198b298b11cb5f5) 

## Training

 

An RNN using LSTM units can be trained in a supervised fashion on a set of training sequences, using an optimization algorithm like [gradient descent](./Gradient_descent) combined with [backpropagation through time](./Backpropagation_through_time) to compute the gradients needed during the optimization process, in order to change each weight of the LSTM network in proportion to the derivative of the error (at the output layer of the LSTM network) with respect to corresponding weight.

 

A problem with using [gradient descent](./Gradient_descent) for standard RNNs is that error gradients [vanish](./Vanishing_gradient_problem) exponentially quickly with the size of the time lag between important events. This is due to      lim  n → →  ∞ ∞     W  n   = 0   {\displaystyle \lim _{n\to \infty }W^{n}=0}  ![{\displaystyle \lim _{n\to \infty }W^{n}=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4f21d24f36ac54c2e3826fe618891ce17b19e12d) if the [spectral radius](./Spectral_radius) of     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7) is smaller than 1.[[2]](./Long_short-term_memory#cite_note-hochreiter1991-2)[[24]](./Long_short-term_memory#cite_note-gradf-24)

 

However, with LSTM units, when error values are back-propagated from the output layer, the error remains in the LSTM unit's cell. This "error carousel" continuously feeds error back to each of the LSTM unit's gates, until they learn to cut off the value.

 

### CTC score function

 

Many applications use stacks of LSTM RNNs[[25]](./Long_short-term_memory#cite_note-fernandez2007ijcai-25) and train them by [connectionist temporal classification (CTC)](./Connectionist_temporal_classification_(CTC))[[5]](./Long_short-term_memory#cite_note-graves2006-5) to find an RNN weight matrix that maximizes the probability of the label sequences in a training set, given the corresponding input sequences. CTC achieves both alignment and recognition.

 

### Alternatives

 

Sometimes, it can be advantageous to train (parts of) an LSTM by [neuroevolution](./Neuroevolution)[[7]](./Long_short-term_memory#cite_note-wierstra2005-7) or by policy gradient methods, especially when there is no "teacher" (that is, training labels).

 


