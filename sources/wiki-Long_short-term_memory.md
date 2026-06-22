---
source: https://en.wikipedia.org/wiki/Long_short-term_memory
fetched: 2026-06-21
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

 

## Applications

 

Applications of LSTM include:

  
- [Robot control](./Robot_control)[[13]](./Long_short-term_memory#cite_note-mayer2006-13)
- [Time series prediction](./Time_series_prediction)[[7]](./Long_short-term_memory#cite_note-wierstra2005-7)
- [Speech recognition](./Speech_recognition)[[26]](./Long_short-term_memory#cite_note-graves2005-26)[[27]](./Long_short-term_memory#cite_note-fernandez2007icann-27)[[28]](./Long_short-term_memory#cite_note-graves2013-28)
- Rhythm learning[[22]](./Long_short-term_memory#cite_note-peephole2002-22)
- Hydrological rainfall–runoff modeling[[29]](./Long_short-term_memory#cite_note-29)
- Music composition[[30]](./Long_short-term_memory#cite_note-eck2002-30)
- [Energy forecasting](./Energy_forecasting)[[18]](./Long_short-term_memory#cite_note-AMVT-18)
- Grammar learning[[31]](./Long_short-term_memory#cite_note-gers2002-31)[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[32]](./Long_short-term_memory#cite_note-perez2003-32)
- [Handwriting recognition](./Handwriting_recognition)[[33]](./Long_short-term_memory#cite_note-graves2009nips-33)[[34]](./Long_short-term_memory#cite_note-34)
- Human action recognition[[35]](./Long_short-term_memory#cite_note-baccouche2011-35)
- [Sign language translation](./Sign_language)[[36]](./Long_short-term_memory#cite_note-huang2018-36)
- Protein homology detection[[37]](./Long_short-term_memory#cite_note-hochreiter2007-37)
- Predicting subcellular localization of proteins[[38]](./Long_short-term_memory#cite_note-thireou2007-38)
- Time series [anomaly detection](./Anomaly_detection)[[39]](./Long_short-term_memory#cite_note-malhotra2015-39)
- Several prediction tasks in the area of [business process management](./Business_process_management)[[40]](./Long_short-term_memory#cite_note-tax2017-40)
- Prediction in medical care pathways[[41]](./Long_short-term_memory#cite_note-choi2016-41)
- [Semantic parsing](./Semantic_parsing)[[42]](./Long_short-term_memory#cite_note-jia2016-42)
- [Object co-segmentation](./Object_co-segmentation)[[43]](./Long_short-term_memory#cite_note-Wang_Duan_Zhang_Niu_p=1657-43)[[44]](./Long_short-term_memory#cite_note-Duan_Wang_Zhai_Zheng_2018_p.-44)
- Airport passenger management[[45]](./Long_short-term_memory#cite_note-orsini2019-45)
- Short-term [traffic forecast](./Traffic_forecast)[[46]](./Long_short-term_memory#cite_note-liu2017-46)
- [Drug design](./Drug_design)[[47]](./Long_short-term_memory#cite_note-pmid29095571-47)
- [Financial forecasting](./Financial_forecasting)[[48]](./Long_short-term_memory#cite_note-saiful2020-48)
- Activity classification in video[[49]](./Long_short-term_memory#cite_note-49)

 

**2015:** Google started using an LSTM trained by CTC for speech recognition on [Google Voice](./Google_Voice).[[50]](./Long_short-term_memory#cite_note-Beau15-50)[[51]](./Long_short-term_memory#cite_note-GoogleVoiceSearch-51) According to the official blog post, the new model cut transcription errors by 49%.[[52]](./Long_short-term_memory#cite_note-googleblog2015-52)

 

**2016:** Google started using an LSTM to suggest messages in the Allo conversation app.[[53]](./Long_short-term_memory#cite_note-GoogleAllo-53) In the same year, Google released the [Google Neural Machine Translation](./Google_Neural_Machine_Translation) system for Google Translate which used LSTMs to reduce translation errors by 60%.[[10]](./Long_short-term_memory#cite_note-GoogleTranslate-10)[[54]](./Long_short-term_memory#cite_note-WiredGoogleTranslate-54)[[55]](./Long_short-term_memory#cite_note-googleblog2016-55)

 

Apple announced in its [Worldwide Developers Conference](./Worldwide_Developers_Conference) that it would start using the LSTM for quicktype[[56]](./Long_short-term_memory#cite_note-AppleQuicktype-56)[[57]](./Long_short-term_memory#cite_note-AppleQuicktype2-57)[[58]](./Long_short-term_memory#cite_note-58) in the iPhone and for Siri.[[59]](./Long_short-term_memory#cite_note-AppleSiri-59)[[60]](./Long_short-term_memory#cite_note-capes2017-60)

 

Amazon released [Polly](./Amazon_Polly), which generates the voices behind Alexa, using a bidirectional LSTM for the text-to-speech technology.[[61]](./Long_short-term_memory#cite_note-AmazonAlexa-61)

 

**2017:**  Facebook performed some 4.5 billion automatic translations every day using long short-term memory networks.[[11]](./Long_short-term_memory#cite_note-FacebookTranslate-11)

 

Microsoft reported reaching 94.9% recognition accuracy on the [Switchboard corpus](./Switchboard_corpus?action=edit&redlink=1), incorporating a vocabulary of 165,000 words. The approach used "dialog session-based long-short-term memory".[[62]](./Long_short-term_memory#cite_note-62)

 

**2018:** [OpenAI](./OpenAI) used LSTM trained by policy gradients to beat humans in the complex video game of Dota 2,[[15]](./Long_short-term_memory#cite_note-OpenAIfive-15) and to control a human-like robot hand that manipulates physical objects with unprecedented dexterity.[[14]](./Long_short-term_memory#cite_note-OpenAIhand-14)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2019:** [DeepMind](./DeepMind) used LSTM trained by policy gradients to excel at the complex video game of [Starcraft II](./Starcraft_II).[[16]](./Long_short-term_memory#cite_note-alphastar-16)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

## History

 

### Development

 

Aspects of LSTM were anticipated by "focused back-propagation",[[64]](./Long_short-term_memory#cite_note-mozer1989-64) cited by the LSTM paper.[[1]](./Long_short-term_memory#cite_note-lstm1997-1)

 

Sepp Hochreiter's 1991 German diploma thesis analyzed the [vanishing gradient problem](./Vanishing_gradient_problem) and developed principles of the method.[[2]](./Long_short-term_memory#cite_note-hochreiter1991-2) His supervisor, [Jürgen Schmidhuber](./Jürgen_Schmidhuber), considered the thesis highly significant.[[65]](./Long_short-term_memory#cite_note-DLhistory-65)

 

An early version of LSTM was published in 1995 in a technical report by [Sepp Hochreiter](./Sepp_Hochreiter) and [Jürgen Schmidhuber](./Jürgen_Schmidhuber),[[66]](./Long_short-term_memory#cite_note-66) then published in the [NIPS](./Conference_on_Neural_Information_Processing_Systems) 1996 conference.[[3]](./Long_short-term_memory#cite_note-hochreiter1996-3)

 

The most commonly used reference point for LSTM was published in 1997 in the journal [Neural Computation](./Neural_Computation_(journal)).[[1]](./Long_short-term_memory#cite_note-lstm1997-1) By introducing Constant Error Carousel (CEC) units, LSTM deals with the [vanishing gradient problem](./Vanishing_gradient_problem). The initial version of LSTM block included cells, input and output gates.[[67]](./Long_short-term_memory#cite_note-ASearchSpaceOdyssey-67)

 

[Felix Gers](./Felix_Gers), Jürgen Schmidhuber, and Fred Cummins introduced the forget gate (also called "keep gate") into the LSTM architecture in 1999,[[68]](./Long_short-term_memory#cite_note-lstm1999-68) enabling the LSTM to reset its own state.[[67]](./Long_short-term_memory#cite_note-ASearchSpaceOdyssey-67) This is the most commonly used version of LSTM nowadays. They added peephole connections in 2000.[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[22]](./Long_short-term_memory#cite_note-peephole2002-22) Additionally, the output activation function was omitted.[[67]](./Long_short-term_memory#cite_note-ASearchSpaceOdyssey-67)

 

### Development of variants

 

In 2005 Graves and Schmidhuber[[26]](./Long_short-term_memory#cite_note-graves2005-26) published LSTM with full [backpropagation through time](./Backpropagation_through_time) and bidirectional LSTM.

 

In 2006 Graves, Fernandez, Gomez, and Schmidhuber[[5]](./Long_short-term_memory#cite_note-graves2006-5) introduced a new error function for LSTM: [Connectionist Temporal Classification](./Connectionist_Temporal_Classification) (CTC) for simultaneous alignment and recognition of sequences.

 

In 2014 Kyunghyun Cho an others[[69]](./Long_short-term_memory#cite_note-cho2014-69) published a simplified variant of the forget gate LSTM[[68]](./Long_short-term_memory#cite_note-lstm1999-68) called [Gated recurrent unit](./Gated_recurrent_unit) (GRU).

 

In 2015 Srivastava, Greff, and Schmidhuber used LSTM principles[[68]](./Long_short-term_memory#cite_note-lstm1999-68) to create the [Highway network](./Highway_network), a [feedforward neural network](./Feedforward_neural_network) with hundreds of layers, much deeper than previous networks.[[70]](./Long_short-term_memory#cite_note-highway2015-70)[[71]](./Long_short-term_memory#cite_note-highway2015neurips-71)[[72]](./Long_short-term_memory#cite_note-mostcited2021-72) Concurrently, the [ResNet](./Residual_neural_network) architecture was developed. It is equivalent to an open-gated or gateless highway network.[[73]](./Long_short-term_memory#cite_note-resnet2015-73)

 

A modern upgrade of LSTM called [xLSTM](./XLSTM?action=edit&redlink=1) is published by a team led by [Sepp Hochreiter](./Sepp_Hochreiter).[[74]](./Long_short-term_memory#cite_note-74)[[75]](./Long_short-term_memory#cite_note-75) One of the 2 blocks (mLSTM) of the architecture are parallelizable like the [Transformer](./Transformer_(deep_learning_architecture)) architecture, the other ones (sLSTM) allow state tracking.

 

### Applications

 

**2001:** Gers and Schmidhuber trained LSTM to learn languages unlearnable by traditional models such as Hidden Markov Models.[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

Hochreiter et al. used LSTM for [meta-learning](./Meta-learning_(computer_science)) (i.e. learning a learning algorithm).[[76]](./Long_short-term_memory#cite_note-76)

 

**2004:** First successful application of LSTM to speech [Alex Graves](./Alex_Graves_(computer_scientist)) et al.[[77]](./Long_short-term_memory#cite_note-graves2004-77)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2005:** Daan Wierstra, Faustino Gomez, and Schmidhuber trained LSTM by [neuroevolution](./Neuroevolution) without a teacher.[[7]](./Long_short-term_memory#cite_note-wierstra2005-7)

 

Mayer et al. trained LSTM to control [robots](./Robot).[[13]](./Long_short-term_memory#cite_note-mayer2006-13)

 

**2007:** Wierstra, Foerster, Peters, and Schmidhuber trained LSTM by policy gradients for [reinforcement learning](./Reinforcement_learning) without a teacher.[[78]](./Long_short-term_memory#cite_note-wierstra2007-78)

 

Hochreiter, Heuesel, and Obermayr applied LSTM to protein homology detection the field of [biology](./Biology).[[37]](./Long_short-term_memory#cite_note-hochreiter2007-37)

 

**2009:** Justin Bayer et al. introduced [neural architecture search](./Neural_architecture_search) for LSTM.[[79]](./Long_short-term_memory#cite_note-bayer2009-79)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2009:** An LSTM trained by CTC won the [ICDAR](./ICDAR) connected handwriting recognition competition. Three such models were submitted by a team led by [Alex Graves](./Alex_Graves_(computer_scientist)).[[80]](./Long_short-term_memory#cite_note-graves2009-80) One was the most accurate model in the competition and another was the fastest.[[81]](./Long_short-term_memory#cite_note-maergner2009-81) This was the first time an RNN won international competitions.[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2013:** Alex Graves, Abdel-rahman Mohamed, and Geoffrey Hinton used LSTM networks as a major component of a network that achieved a record 17.7% [phoneme](./Phoneme) error rate on the classic [TIMIT](./TIMIT) natural speech dataset.[[28]](./Long_short-term_memory#cite_note-graves2013-28)

 

**2017:** Researchers from [Michigan State University](./Michigan_State_University), [IBM Research](./IBM_Research), and [Cornell University](./Cornell_University) published a study in the Knowledge Discovery and Data Mining (KDD) conference.[[82]](./Long_short-term_memory#cite_note-82) Their [time-aware LSTM](./Time-aware_LSTM) (T-LSTM) performs better on certain data sets than standard LSTM.

 

**2020:** Kaplan and McCandlish et al. explored the [ scaling law](./Neural_scaling_law) of LSTM architecture in language modeling and compared it with [ Transformers](./Transformer_(deep_learning)), showing that Transformers scale better than LSTM on text data. [[83]](./Long_short-term_memory#cite_note-83)

 

## See also

  Please respect alphabetical order   
- [Attention (machine learning)](./Attention_(machine_learning))
- [Deep learning](./Deep_learning)
- [Differentiable neural computer](./Differentiable_neural_computer)
- [Gated recurrent unit](./Gated_recurrent_unit)
- [Highway network](./Highway_network)
- [Long-term potentiation](./Long-term_potentiation)
- [Prefrontal cortex basal ganglia working memory](./Prefrontal_cortex_basal_ganglia_working_memory)
- [Recurrent neural network](./Recurrent_neural_network)
- [Seq2seq](./Seq2seq)
- [Transformer (machine learning model)](./Transformer_(machine_learning_model))
- [Time series](./Time_series)

  

## References

  
1. [1](./Long_short-term_memory#cite_ref-lstm1997_1-0) [2](./Long_short-term_memory#cite_ref-lstm1997_1-1) [3](./Long_short-term_memory#cite_ref-lstm1997_1-2) [4](./Long_short-term_memory#cite_ref-lstm1997_1-3) [5](./Long_short-term_memory#cite_ref-lstm1997_1-4) [Sepp Hochreiter](./Sepp_Hochreiter); [Jürgen Schmidhuber](./Jürgen_Schmidhuber) (1997). ["Long short-term memory"](https://www.researchgate.net/publication/13853244). *[Neural Computation](./Neural_Computation_(journal))*. **9** (8): 1735–1780. [doi](./Doi_(identifier)):[10.1162/neco.1997.9.8.1735](https://doi.org/10.1162%2Fneco.1997.9.8.1735). [PMID](./PMID_(identifier)) [9377276](https://pubmed.ncbi.nlm.nih.gov/9377276). [S2CID](./S2CID_(identifier)) [1915014](https://api.semanticscholar.org/CorpusID:1915014).
2. [1](./Long_short-term_memory#cite_ref-hochreiter1991_2-0) [2](./Long_short-term_memory#cite_ref-hochreiter1991_2-1) [3](./Long_short-term_memory#cite_ref-hochreiter1991_2-2) Hochreiter, Sepp (1991). [*Untersuchungen zu dynamischen neuronalen Netzen*](http://www.bioinf.jku.at/publications/older/3804.pdf) (PDF) (diploma thesis). [Technical University of Munich](./Technical_University_of_Munich), Institute of Computer Science.
3. [1](./Long_short-term_memory#cite_ref-hochreiter1996_3-0) [2](./Long_short-term_memory#cite_ref-hochreiter1996_3-1) Hochreiter, Sepp; Schmidhuber, Jürgen (1996-12-03). ["LSTM can solve hard long time lag problems"](https://dl.acm.org/doi/10.5555/2998981.2999048). *Proceedings of the 9th International Conference on Neural Information Processing Systems*. NIPS'96. Cambridge, MA, USA: MIT Press: 473–479.
4. [1](./Long_short-term_memory#cite_ref-lstm2000_4-0) [2](./Long_short-term_memory#cite_ref-lstm2000_4-1) [3](./Long_short-term_memory#cite_ref-lstm2000_4-2) Felix A. Gers; Jürgen Schmidhuber; Fred Cummins (2000). "Learning to Forget: Continual Prediction with LSTM". *[Neural Computation](./Neural_Computation_(journal))*. **12** (10): 2451–2471. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.55.5709](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.55.5709). [doi](./Doi_(identifier)):[10.1162/089976600300015015](https://doi.org/10.1162%2F089976600300015015). [PMID](./PMID_(identifier)) [11032042](https://pubmed.ncbi.nlm.nih.gov/11032042). [S2CID](./S2CID_(identifier)) [11598600](https://api.semanticscholar.org/CorpusID:11598600).
5. [1](./Long_short-term_memory#cite_ref-graves2006_5-0) [2](./Long_short-term_memory#cite_ref-graves2006_5-1) [3](./Long_short-term_memory#cite_ref-graves2006_5-2) Graves, Alex; Fernández, Santiago; Gomez, Faustino; Schmidhuber, Jürgen (2006). "Connectionist temporal classification: Labelling unsegmented sequence data with recurrent neural networks". *In Proceedings of the International Conference on Machine Learning, ICML 2006*: 369–376. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.75.6306](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.75.6306).
6. [↑](./Long_short-term_memory#cite_ref-6) Karim, Fazle; Majumdar, Somshubra; Darabi, Houshang; Chen, Shun (2018). ["LSTM Fully Convolutional Networks for Time Series Classification"](https://doi.org/10.1109%2FACCESS.2017.2779939). *IEEE Access*. **6**: 1662–1669. [arXiv](./ArXiv_(identifier)):[1709.05206](https://arxiv.org/abs/1709.05206). [Bibcode](./Bibcode_(identifier)):[2018IEEEA...6.1662K](https://ui.adsabs.harvard.edu/abs/2018IEEEA...6.1662K). [doi](./Doi_(identifier)):[10.1109/ACCESS.2017.2779939](https://doi.org/10.1109%2FACCESS.2017.2779939). [ISSN](./ISSN_(identifier)) [2169-3536](https://search.worldcat.org/issn/2169-3536).
7. [1](./Long_short-term_memory#cite_ref-wierstra2005_7-0) [2](./Long_short-term_memory#cite_ref-wierstra2005_7-1) [3](./Long_short-term_memory#cite_ref-wierstra2005_7-2) [4](./Long_short-term_memory#cite_ref-wierstra2005_7-3) Wierstra, Daan; Schmidhuber, J.; Gomez, F. J. (2005). ["Evolino: Hybrid Neuroevolution/Optimal Linear Search for Sequence Learning"](https://www.academia.edu/5830256). *Proceedings of the 19th International Joint Conference on Artificial Intelligence (IJCAI), Edinburgh*: 853–858.
8. [↑](./Long_short-term_memory#cite_ref-sak2014_8-0) Sak, Hasim; Senior, Andrew; Beaufays, Francoise (2014). ["Long Short-Term Memory recurrent neural network architectures for large scale acoustic modeling"](https://web.archive.org/web/20180424203806/https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43905.pdf) (PDF). Archived from [the original](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43905.pdf) (PDF) on 2018-04-24.
9. [↑](./Long_short-term_memory#cite_ref-liwu2015_9-0) Li, Xiangang; Wu, Xihong (2014-10-15). "Constructing Long Short-Term Memory based Deep Recurrent Neural Networks for Large Vocabulary Speech Recognition". [arXiv](./ArXiv_(identifier)):[1410.4281](https://arxiv.org/abs/1410.4281) [[cs.CL](https://arxiv.org/archive/cs.CL)].
10. [1](./Long_short-term_memory#cite_ref-GoogleTranslate_10-0) [2](./Long_short-term_memory#cite_ref-GoogleTranslate_10-1) Wu, Yonghui; Schuster, Mike; Chen, Zhifeng; Le, Quoc V.; Norouzi, Mohammad; Macherey, Wolfgang; Krikun, Maxim; Cao, Yuan; Gao, Qin (2016-09-26). "Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation". [arXiv](./ArXiv_(identifier)):[1609.08144](https://arxiv.org/abs/1609.08144) [[cs.CL](https://arxiv.org/archive/cs.CL)].
11. [1](./Long_short-term_memory#cite_ref-FacebookTranslate_11-0) [2](./Long_short-term_memory#cite_ref-FacebookTranslate_11-1) Ong, Thuy (4 August 2017). ["Facebook's translations are now powered completely by AI"](https://www.theverge.com/2017/8/4/16093872/facebook-ai-translations-artificial-intelligence). *www.allthingsdistributed.com*. Retrieved 2019-02-15.
12. [↑](./Long_short-term_memory#cite_ref-12) Sahidullah, Md; Patino, Jose; Cornell, Samuele; Yin, Ruiking; Sivasankaran, Sunit; Bredin, Herve; Korshunov, Pavel; Brutti, Alessio; Serizel, Romain; Vincent, Emmanuel; Evans, Nicholas; Marcel, Sebastien; Squartini, Stefano; Barras, Claude (2019-11-06). "The Speed Submission to DIHARD II: Contributions & Lessons Learned". [arXiv](./ArXiv_(identifier)):[1911.02388](https://arxiv.org/abs/1911.02388) [[eess.AS](https://arxiv.org/archive/eess.AS)].
13. [1](./Long_short-term_memory#cite_ref-mayer2006_13-0) [2](./Long_short-term_memory#cite_ref-mayer2006_13-1) [3](./Long_short-term_memory#cite_ref-mayer2006_13-2) Mayer, H.; Gomez, F.; Wierstra, D.; Nagy, I.; Knoll, A.; Schmidhuber, J. (October 2006). "A System for Robotic Heart Surgery that Learns to Tie Knots Using Recurrent Neural Networks". *2006 IEEE/RSJ International Conference on Intelligent Robots and Systems*. pp. 543–548. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.218.3399](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.218.3399). [doi](./Doi_(identifier)):[10.1109/IROS.2006.282190](https://doi.org/10.1109%2FIROS.2006.282190). [ISBN](./ISBN_(identifier)) [978-1-4244-0258-8](./Special:BookSources/978-1-4244-0258-8). [S2CID](./S2CID_(identifier)) [12284900](https://api.semanticscholar.org/CorpusID:12284900).
14. [1](./Long_short-term_memory#cite_ref-OpenAIhand_14-0) [2](./Long_short-term_memory#cite_ref-OpenAIhand_14-1) ["Learning Dexterity"](https://openai.com/research/learning-dexterity/). *OpenAI*. July 30, 2018. Retrieved 2023-06-28.
15. [1](./Long_short-term_memory#cite_ref-OpenAIfive_15-0) [2](./Long_short-term_memory#cite_ref-OpenAIfive_15-1) Rodriguez, Jesus (July 2, 2018). ["The Science Behind OpenAI Five that just Produced One of the Greatest Breakthrough in the History of AI"](https://web.archive.org/web/20191226222000/https://towardsdatascience.com/the-science-behind-openai-five-that-just-produced-one-of-the-greatest-breakthrough-in-the-history-b045bcdc2b69?gi=24b20ef8ca3f). *Towards Data Science*. Archived from [the original](https://towardsdatascience.com/the-science-behind-openai-five-that-just-produced-one-of-the-greatest-breakthrough-in-the-history-b045bcdc2b69) on 2019-12-26. Retrieved 2019-01-15.
16. [1](./Long_short-term_memory#cite_ref-alphastar_16-0) [2](./Long_short-term_memory#cite_ref-alphastar_16-1) Stanford, Stacy (January 25, 2019). ["DeepMind's AI, AlphaStar Showcases Significant Progress Towards AGI"](https://medium.com/mlmemoirs/deepminds-ai-alphastar-showcases-significant-progress-towards-agi-93810c94fbe9). *Medium ML Memoirs*. Retrieved 2019-01-15.
17. [↑](./Long_short-term_memory#cite_ref-decade2022_17-0) Schmidhuber, Jürgen (2021). ["The 2010s: Our Decade of Deep Learning / Outlook on the 2020s"](https://people.idsia.ch/~juergen/2010s-our-decade-of-deep-learning.html). *AI Blog*. IDSIA, Switzerland. Retrieved 2022-04-30.
18. [1](./Long_short-term_memory#cite_ref-AMVT_18-0) [2](./Long_short-term_memory#cite_ref-AMVT_18-1) Maity, Abhishek; Tukarul, Viraj (23 January 2026). "Forecasting Energy Consumption using Recurrent Neural Networks: A Comparative Analysis". [arXiv](./ArXiv_(identifier)):[2601.17110](https://arxiv.org/abs/2601.17110) [[cs.CY](https://arxiv.org/archive/cs.CY)].
19. [↑](./Long_short-term_memory#cite_ref-calin2020_19-0) Calin, Ovidiu (14 February 2020). *Deep Learning Architectures*. Cham, Switzerland: Springer Nature. p. 555. [ISBN](./ISBN_(identifier)) [978-3-030-36720-6](./Special:BookSources/978-3-030-36720-6).
20. [↑](./Long_short-term_memory#cite_ref-LakretzKruszewskiDesbordes2019_20-0) Lakretz, Yair; Kruszewski, German; Desbordes, Theo; Hupkes, Dieuwke; Dehaene, Stanislas; Baroni, Marco (2019), ["The emergence of number and syntax units in"](https://aclanthology.org/N19-1002/), [*The emergence of number and syntax units*](https://pure.uva.nl/ws/files/49723040/N19_1002.pdf) (PDF), Association for Computational Linguistics, pp. 11–20, [doi](./Doi_(identifier)):[10.18653/v1/N19-1002](https://doi.org/10.18653%2Fv1%2FN19-1002), [hdl](./Hdl_(identifier)):[11245.1/16cb6800-e10d-4166-8e0b-fed61ca6ebb4](https://hdl.handle.net/11245.1%2F16cb6800-e10d-4166-8e0b-fed61ca6ebb4), [S2CID](./S2CID_(identifier)) [81978369](https://api.semanticscholar.org/CorpusID:81978369)
21. [1](./Long_short-term_memory#cite_ref-peepholeLSTM_21-0) [2](./Long_short-term_memory#cite_ref-peepholeLSTM_21-1) [3](./Long_short-term_memory#cite_ref-peepholeLSTM_21-2) [4](./Long_short-term_memory#cite_ref-peepholeLSTM_21-3) [5](./Long_short-term_memory#cite_ref-peepholeLSTM_21-4) [6](./Long_short-term_memory#cite_ref-peepholeLSTM_21-5) Gers, F. A.; Schmidhuber, J. (2001). ["LSTM Recurrent Networks Learn Simple Context Free and Context Sensitive Languages"](https://web.archive.org/web/20170706014426/ftp://ftp.idsia.ch/pub/juergen/L-IEEE.pdf) (PDF). *IEEE Transactions on Neural Networks*. **12** (6): 1333–1340. [Bibcode](./Bibcode_(identifier)):[2001ITNN...12.1333G](https://ui.adsabs.harvard.edu/abs/2001ITNN...12.1333G). [doi](./Doi_(identifier)):[10.1109/72.963769](https://doi.org/10.1109%2F72.963769). [PMID](./PMID_(identifier)) [18249962](https://pubmed.ncbi.nlm.nih.gov/18249962). [S2CID](./S2CID_(identifier)) [10192330](https://api.semanticscholar.org/CorpusID:10192330). Archived from [the original](ftp://ftp.idsia.ch/pub/juergen/L-IEEE.pdf) (PDF) on 2017-07-06.
22. [1](./Long_short-term_memory#cite_ref-peephole2002_22-0) [2](./Long_short-term_memory#cite_ref-peephole2002_22-1) [3](./Long_short-term_memory#cite_ref-peephole2002_22-2) [4](./Long_short-term_memory#cite_ref-peephole2002_22-3) Gers, F.; Schraudolph, N.; Schmidhuber, J. (2002). ["Learning precise timing with LSTM recurrent networks"](http://www.jmlr.org/papers/volume3/gers02a/gers02a.pdf) (PDF). *Journal of Machine Learning Research*. **3**: 115–143.
23. [↑](./Long_short-term_memory#cite_ref-shi2015_23-0) Xingjian Shi; Zhourong Chen; Hao Wang; Dit-Yan Yeung; Wai-kin Wong; Wang-chun Woo (2015). "Convolutional LSTM Network: A Machine Learning Approach for Precipitation Nowcasting". *Proceedings of the 28th International Conference on Neural Information Processing Systems*: 802–810. [arXiv](./ArXiv_(identifier)):[1506.04214](https://arxiv.org/abs/1506.04214). [Bibcode](./Bibcode_(identifier)):[2015arXiv150604214S](https://ui.adsabs.harvard.edu/abs/2015arXiv150604214S).
24. [↑](./Long_short-term_memory#cite_ref-gradf_24-0) Hochreiter, S.; Bengio, Y.; Frasconi, P.; Schmidhuber, J. (2001). ["Gradient Flow in Recurrent Nets: the Difficulty of Learning Long-Term Dependencies (PDF Download Available)"](https://www.researchgate.net/publication/2839938). In Kremer and, S. C.; Kolen, J. F. (eds.). *A Field Guide to Dynamical Recurrent Neural Networks*. IEEE Press.
25. [↑](./Long_short-term_memory#cite_ref-fernandez2007ijcai_25-0) Fernández, Santiago; Graves, Alex; Schmidhuber, Jürgen (2007). "Sequence labelling in structured domains with hierarchical recurrent neural networks". *Proc. 20th Int. Joint Conf. On Artificial Intelligence, Ijcai 2007*: 774–779. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.79.1887](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.79.1887).
26. [1](./Long_short-term_memory#cite_ref-graves2005_26-0) [2](./Long_short-term_memory#cite_ref-graves2005_26-1) Graves, A.; Schmidhuber, J. (2005). "Framewise phoneme classification with bidirectional LSTM and other neural network architectures". *Neural Networks*. **18** (5–6): 602–610. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.331.5800](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.331.5800). [doi](./Doi_(identifier)):[10.1016/j.neunet.2005.06.042](https://doi.org/10.1016%2Fj.neunet.2005.06.042). [PMID](./PMID_(identifier)) [16112549](https://pubmed.ncbi.nlm.nih.gov/16112549). [S2CID](./S2CID_(identifier)) [1856462](https://api.semanticscholar.org/CorpusID:1856462).
27. [↑](./Long_short-term_memory#cite_ref-fernandez2007icann_27-0) Fernández, S.; Graves, A.; Schmidhuber, J. (9 September 2007). ["An Application of Recurrent Neural Networks to Discriminative Keyword Spotting"](http://dl.acm.org/citation.cfm?id=1778066.1778092). *Proceedings of the 17th International Conference on Artificial Neural Networks*. ICANN'07. Berlin, Heidelberg: Springer-Verlag: 220–229. [ISBN](./ISBN_(identifier)) [978-3540746935](./Special:BookSources/978-3540746935). Retrieved 28 December 2023.
28. [1](./Long_short-term_memory#cite_ref-graves2013_28-0) [2](./Long_short-term_memory#cite_ref-graves2013_28-1) Graves, Alex; Mohamed, Abdel-rahman; Hinton, Geoffrey (2013). "Speech recognition with deep recurrent neural networks". *2013 IEEE International Conference on Acoustics, Speech and Signal Processing*. pp. 6645–6649. [arXiv](./ArXiv_(identifier)):[1303.5778](https://arxiv.org/abs/1303.5778). [doi](./Doi_(identifier)):[10.1109/ICASSP.2013.6638947](https://doi.org/10.1109%2FICASSP.2013.6638947). [ISBN](./ISBN_(identifier)) [978-1-4799-0356-6](./Special:BookSources/978-1-4799-0356-6). [S2CID](./S2CID_(identifier)) [206741496](https://api.semanticscholar.org/CorpusID:206741496).
29. [↑](./Long_short-term_memory#cite_ref-29) Kratzert, Frederik; Klotz, Daniel; Shalev, Guy; Klambauer, Günter; Hochreiter, Sepp; Nearing, Grey (2019-12-17). ["Towards learning universal, regional, and local hydrological behaviors via machine learning applied to large-sample datasets"](https://hess.copernicus.org/articles/23/5089/2019/). *Hydrology and Earth System Sciences*. **23** (12): 5089–5110. [arXiv](./ArXiv_(identifier)):[1907.08456](https://arxiv.org/abs/1907.08456). [Bibcode](./Bibcode_(identifier)):[2019HESS...23.5089K](https://ui.adsabs.harvard.edu/abs/2019HESS...23.5089K). [doi](./Doi_(identifier)):[10.5194/hess-23-5089-2019](https://doi.org/10.5194%2Fhess-23-5089-2019). [ISSN](./ISSN_(identifier)) [1027-5606](https://search.worldcat.org/issn/1027-5606).
30. [↑](./Long_short-term_memory#cite_ref-eck2002_30-0) Eck, Douglas; Schmidhuber, Jürgen (2002-08-28). "Learning the Long-Term Structure of the Blues". *Artificial Neural Networks — ICANN 2002*. Lecture Notes in Computer Science. Vol. 2415. Springer, Berlin, Heidelberg. pp. 284–289. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.116.3620](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.116.3620). [doi](./Doi_(identifier)):[10.1007/3-540-46084-5_47](https://doi.org/10.1007%2F3-540-46084-5_47). [ISBN](./ISBN_(identifier)) [978-3540460848](./Special:BookSources/978-3540460848).
31. [↑](./Long_short-term_memory#cite_ref-gers2002_31-0) Schmidhuber, J.; Gers, F.; Eck, D.; Schmidhuber, J.; Gers, F. (2002). "Learning nonregular languages: A comparison of simple recurrent networks and LSTM". *Neural Computation*. **14** (9): 2039–2041. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.11.7369](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.11.7369). [doi](./Doi_(identifier)):[10.1162/089976602320263980](https://doi.org/10.1162%2F089976602320263980). [PMID](./PMID_(identifier)) [12184841](https://pubmed.ncbi.nlm.nih.gov/12184841). [S2CID](./S2CID_(identifier)) [30459046](https://api.semanticscholar.org/CorpusID:30459046).
32. [↑](./Long_short-term_memory#cite_ref-perez2003_32-0) Perez-Ortiz, J. A.; Gers, F. A.; Eck, D.; Schmidhuber, J. (2003). "Kalman filters improve LSTM network performance in problems unsolvable by traditional recurrent nets". *Neural Networks*. **16** (2): 241–250. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.381.1992](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.381.1992). [doi](./Doi_(identifier)):[10.1016/s0893-6080(02)00219-8](https://doi.org/10.1016%2Fs0893-6080%2802%2900219-8). [PMID](./PMID_(identifier)) [12628609](https://pubmed.ncbi.nlm.nih.gov/12628609).
33. [↑](./Long_short-term_memory#cite_ref-graves2009nips_33-0) A. Graves, J. Schmidhuber. Offline Handwriting Recognition with Multidimensional Recurrent Neural Networks. Advances in Neural Information Processing Systems 22, NIPS'22, pp 545–552, Vancouver, MIT Press, 2009.
34. [↑](./Long_short-term_memory#cite_ref-34) Graves, A.; Fernández, S.; Liwicki, M.; Bunke, H.; Schmidhuber, J. (3 December 2007). ["Unconstrained Online Handwriting Recognition with Recurrent Neural Networks"](http://dl.acm.org/citation.cfm?id=2981562.2981635). *Proceedings of the 20th International Conference on Neural Information Processing Systems*. NIPS'07. USA: Curran Associates Inc.: 577–584. [ISBN](./ISBN_(identifier)) [9781605603520](./Special:BookSources/9781605603520). Retrieved 28 December 2023.
35. [↑](./Long_short-term_memory#cite_ref-baccouche2011_35-0) Baccouche, M.; Mamalet, F.; Wolf, C.; Garcia, C.; Baskurt, A. (2011). "Sequential Deep Learning for Human Action Recognition". In Salah, A. A.; Lepri, B. (eds.). *2nd International Workshop on Human Behavior Understanding (HBU)*. Lecture Notes in Computer Science. Vol. 7065. Amsterdam, Netherlands: Springer. pp. 29–39. [doi](./Doi_(identifier)):[10.1007/978-3-642-25446-8_4](https://doi.org/10.1007%2F978-3-642-25446-8_4). [ISBN](./ISBN_(identifier)) [978-3-642-25445-1](./Special:BookSources/978-3-642-25445-1).
36. [↑](./Long_short-term_memory#cite_ref-huang2018_36-0) Huang, Jie; Zhou, Wengang; Zhang, Qilin; Li, Houqiang; Li, Weiping (2018-01-30). "Video-based Sign Language Recognition without Temporal Segmentation". [arXiv](./ArXiv_(identifier)):[1801.10111](https://arxiv.org/abs/1801.10111) [[cs.CV](https://arxiv.org/archive/cs.CV)].
37. [1](./Long_short-term_memory#cite_ref-hochreiter2007_37-0) [2](./Long_short-term_memory#cite_ref-hochreiter2007_37-1) Hochreiter, S.; Heusel, M.; Obermayer, K. (2007). ["Fast model-based protein homology detection without alignment"](https://doi.org/10.1093%2Fbioinformatics%2Fbtm247). *Bioinformatics*. **23** (14): 1728–1736. [doi](./Doi_(identifier)):[10.1093/bioinformatics/btm247](https://doi.org/10.1093%2Fbioinformatics%2Fbtm247). [PMID](./PMID_(identifier)) [17488755](https://pubmed.ncbi.nlm.nih.gov/17488755).
38. [↑](./Long_short-term_memory#cite_ref-thireou2007_38-0) Thireou, T.; Reczko, M. (2007). "Bidirectional Long Short-Term Memory Networks for predicting the subcellular localization of eukaryotic proteins". *IEEE/ACM Transactions on Computational Biology and Bioinformatics*. **4** (3): 441–446. [Bibcode](./Bibcode_(identifier)):[2007ITCBB...4..441T](https://ui.adsabs.harvard.edu/abs/2007ITCBB...4..441T). [doi](./Doi_(identifier)):[10.1109/tcbb.2007.1015](https://doi.org/10.1109%2Ftcbb.2007.1015). [PMID](./PMID_(identifier)) [17666763](https://pubmed.ncbi.nlm.nih.gov/17666763). [S2CID](./S2CID_(identifier)) [11787259](https://api.semanticscholar.org/CorpusID:11787259).
39. [↑](./Long_short-term_memory#cite_ref-malhotra2015_39-0) Malhotra, Pankaj; Vig, Lovekesh; Shroff, Gautam; Agarwal, Puneet (April 2015). ["Long Short Term Memory Networks for Anomaly Detection in Time Series"](https://web.archive.org/web/20201030224634/https://www.elen.ucl.ac.be/Proceedings/esann/esannpdf/es2015-56.pdf) (PDF). *European Symposium on Artificial Neural Networks, Computational Intelligence and Machine Learning — ESANN 2015*. Archived from [the original](https://www.elen.ucl.ac.be/Proceedings/esann/esannpdf/es2015-56.pdf) (PDF) on 2020-10-30. Retrieved 2018-02-21.
40. [↑](./Long_short-term_memory#cite_ref-tax2017_40-0) Tax, N.; Verenich, I.; La Rosa, M.; Dumas, M. (2017). "Predictive Business Process Monitoring with LSTM Neural Networks". *Advanced Information Systems Engineering*. Lecture Notes in Computer Science. Vol. 10253. pp. 477–492. [arXiv](./ArXiv_(identifier)):[1612.02130](https://arxiv.org/abs/1612.02130). [doi](./Doi_(identifier)):[10.1007/978-3-319-59536-8_30](https://doi.org/10.1007%2F978-3-319-59536-8_30). [ISBN](./ISBN_(identifier)) [978-3-319-59535-1](./Special:BookSources/978-3-319-59535-1). [S2CID](./S2CID_(identifier)) [2192354](https://api.semanticscholar.org/CorpusID:2192354).
41. [↑](./Long_short-term_memory#cite_ref-choi2016_41-0) Choi, E.; Bahadori, M.T.; Schuetz, E.; Stewart, W.; Sun, J. (2016). ["Doctor AI: Predicting Clinical Events via Recurrent Neural Networks"](http://proceedings.mlr.press/v56/Choi16.html). *JMLR Workshop and Conference Proceedings*. **56**: 301–318. [arXiv](./ArXiv_(identifier)):[1511.05942](https://arxiv.org/abs/1511.05942). [Bibcode](./Bibcode_(identifier)):[2015arXiv151105942C](https://ui.adsabs.harvard.edu/abs/2015arXiv151105942C). [PMC](./PMC_(identifier)) [5341604](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5341604). [PMID](./PMID_(identifier)) [28286600](https://pubmed.ncbi.nlm.nih.gov/28286600).
42. [↑](./Long_short-term_memory#cite_ref-jia2016_42-0) Jia, Robin; [Liang, Percy](./Percy_Liang) (2016). "Data Recombination for Neural Semantic Parsing". [arXiv](./ArXiv_(identifier)):[1606.03622](https://arxiv.org/abs/1606.03622) [[cs.CL](https://arxiv.org/archive/cs.CL)].
43. [↑](./Long_short-term_memory#cite_ref-Wang_Duan_Zhang_Niu_p=1657_43-0) Wang, Le; Duan, Xuhuan; Zhang, Qilin; Niu, Zhenxing; Hua, Gang; Zheng, Nanning (2018-05-22). ["Segment-Tube: Spatio-Temporal Action Localization in Untrimmed Videos with Per-Frame Segmentation"](https://qilin-zhang.github.io/_pages/pdfs/Segment-Tube_Spatio-Temporal_Action_Localization_in_Untrimmed_Videos_with_Per-Frame_Segmentation.pdf) (PDF). *Sensors*. **18** (5): 1657. [Bibcode](./Bibcode_(identifier)):[2018Senso..18.1657W](https://ui.adsabs.harvard.edu/abs/2018Senso..18.1657W). [doi](./Doi_(identifier)):[10.3390/s18051657](https://doi.org/10.3390%2Fs18051657). [ISSN](./ISSN_(identifier)) [1424-8220](https://search.worldcat.org/issn/1424-8220). [PMC](./PMC_(identifier)) [5982167](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5982167). [PMID](./PMID_(identifier)) [29789447](https://pubmed.ncbi.nlm.nih.gov/29789447).
44. [↑](./Long_short-term_memory#cite_ref-Duan_Wang_Zhai_Zheng_2018_p._44-0) Duan, Xuhuan; Wang, Le; Zhai, Changbo; Zheng, Nanning; Zhang, Qilin; Niu, Zhenxing; Hua, Gang (2018). "Joint Spatio-Temporal Action Localization in Untrimmed Videos with Per-Frame Segmentation". *2018 25th IEEE International Conference on Image Processing (ICIP)*. 25th IEEE International Conference on Image Processing (ICIP). pp. 918–922. [doi](./Doi_(identifier)):[10.1109/icip.2018.8451692](https://doi.org/10.1109%2Ficip.2018.8451692). [ISBN](./ISBN_(identifier)) [978-1-4799-7061-2](./Special:BookSources/978-1-4799-7061-2).
45. [↑](./Long_short-term_memory#cite_ref-orsini2019_45-0) Orsini, F.; Gastaldi, M.; Mantecchini, L.; Rossi, R. (2019). *Neural networks trained with WiFi traces to predict airport passenger behavior*. 6th International Conference on Models and Technologies for Intelligent Transportation Systems. Krakow: IEEE. [arXiv](./ArXiv_(identifier)):[1910.14026](https://arxiv.org/abs/1910.14026). [doi](./Doi_(identifier)):[10.1109/MTITS.2019.8883365](https://doi.org/10.1109%2FMTITS.2019.8883365). 8883365.
46. [↑](./Long_short-term_memory#cite_ref-liu2017_46-0) Zhao, Z.; Chen, W.; Wu, X.; Chen, P.C.Y.; Liu, J. (2017). "LSTM network: A deep learning approach for Short-term traffic forecast". *IET Intelligent Transport Systems*. **11** (2): 68–75. [doi](./Doi_(identifier)):[10.1049/iet-its.2016.0208](https://doi.org/10.1049%2Fiet-its.2016.0208). [S2CID](./S2CID_(identifier)) [114567527](https://api.semanticscholar.org/CorpusID:114567527).
47. [↑](./Long_short-term_memory#cite_ref-pmid29095571_47-0) Gupta A, Müller AT, Huisman BJH, Fuchs JA, Schneider P, Schneider G (2018). ["Generative Recurrent Networks for De Novo Drug Design"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5836943). *Mol Inform*. **37** (1–2) 1700111. [doi](./Doi_(identifier)):[10.1002/minf.201700111](https://doi.org/10.1002%2Fminf.201700111). [PMC](./PMC_(identifier)) [5836943](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5836943). [PMID](./PMID_(identifier)) [29095571](https://pubmed.ncbi.nlm.nih.gov/29095571).`{{cite journal}}`:  CS1 maint: multiple names: authors list ([link](./Category:CS1_maint:_multiple_names:_authors_list))
48. [↑](./Long_short-term_memory#cite_ref-saiful2020_48-0) Saiful Islam, Md.; Hossain, Emam (2020-10-26). ["Foreign Exchange Currency Rate Prediction using a GRU-LSTM Hybrid Network"](https://doi.org/10.1016%2Fj.socl.2020.100009). *Soft Computing Letters*. **3** 100009. [doi](./Doi_(identifier)):[10.1016/j.socl.2020.100009](https://doi.org/10.1016%2Fj.socl.2020.100009). [ISSN](./ISSN_(identifier)) [2666-2221](https://search.worldcat.org/issn/2666-2221).
49. [↑](./Long_short-term_memory#cite_ref-49) Martin, Abbey; Hill, Andrew J.; Seiler, Konstantin M.; Balamurali, Mehala (2024-05-27). ["Automatic excavator action recognition and localisation for untrimmed video using hybrid LSTM-Transformer networks"](https://www.tandfonline.com/doi/full/10.1080/17480930.2023.2290364). *International Journal of Mining, Reclamation and Environment*. **38** (5): 353–372. [Bibcode](./Bibcode_(identifier)):[2024IJMRE..38..353M](https://ui.adsabs.harvard.edu/abs/2024IJMRE..38..353M). [doi](./Doi_(identifier)):[10.1080/17480930.2023.2290364](https://doi.org/10.1080%2F17480930.2023.2290364). [ISSN](./ISSN_(identifier)) [1748-0930](https://search.worldcat.org/issn/1748-0930).
50. [↑](./Long_short-term_memory#cite_ref-Beau15_50-0) Beaufays, Françoise (August 11, 2015). ["The neural networks behind Google Voice transcription"](http://googleresearch.blogspot.co.at/2015/08/the-neural-networks-behind-google-voice.html). *Research Blog*. Retrieved 2017-06-27.
51. [↑](./Long_short-term_memory#cite_ref-GoogleVoiceSearch_51-0) Sak, Haşim; Senior, Andrew; Rao, Kanishka; Beaufays, Françoise; Schalkwyk, Johan (September 24, 2015). ["Google voice search: faster and more accurate"](http://googleresearch.blogspot.co.uk/2015/09/google-voice-search-faster-and-more.html). *Research Blog*. Retrieved 2017-06-27.
52. [↑](./Long_short-term_memory#cite_ref-googleblog2015_52-0) ["Neon prescription... or rather, New transcription for Google Voice"](https://googleblog.blogspot.com/2015/07/neon-prescription-or-rather-new.html). *Official Google Blog*. 23 July 2015. Retrieved 2020-04-25.
53. [↑](./Long_short-term_memory#cite_ref-GoogleAllo_53-0) Khaitan, Pranav (May 18, 2016). ["Chat Smarter with Allo"](http://googleresearch.blogspot.co.at/2016/05/chat-smarter-with-allo.html). *Research Blog*. Retrieved 2017-06-27.
54. [↑](./Long_short-term_memory#cite_ref-WiredGoogleTranslate_54-0) Metz, Cade (September 27, 2016). ["An Infusion of AI Makes Google Translate More Powerful Than Ever | WIRED"](https://www.wired.com/2016/09/google-claims-ai-breakthrough-machine-translation/). *Wired*. Retrieved 2017-06-27.
55. [↑](./Long_short-term_memory#cite_ref-googleblog2016_55-0) ["A Neural Network for Machine Translation, at Production Scale"](http://ai.googleblog.com/2016/09/a-neural-network-for-machine.html). *Google AI Blog*. 27 September 2016. Retrieved 2020-04-25.
56. [↑](./Long_short-term_memory#cite_ref-AppleQuicktype_56-0) Efrati, Amir (June 13, 2016). ["Apple's Machines Can Learn Too"](https://www.theinformation.com/apples-machines-can-learn-too). *The Information*. Retrieved 2017-06-27.
57. [↑](./Long_short-term_memory#cite_ref-AppleQuicktype2_57-0) Ranger, Steve (June 14, 2016). ["iPhone, AI and big data: Here's how Apple plans to protect your privacy"](https://www.zdnet.com/article/ai-big-data-and-the-iphone-heres-how-apple-plans-to-protect-your-privacy/). *ZDNet*. Retrieved 2017-06-27.
58. [↑](./Long_short-term_memory#cite_ref-58) ["Can Global Semantic Context Improve Neural Language Models? – Apple"](https://machinelearning.apple.com/2018/09/27/can-global-semantic-context-improve-neural-language-models.html). *Apple Machine Learning Journal*. Retrieved 2020-04-30.
59. [↑](./Long_short-term_memory#cite_ref-AppleSiri_59-0) Smith, Chris (2016-06-13). ["iOS 10: Siri now works in third-party apps, comes with extra AI features"](http://bgr.com/2016/06/13/ios-10-siri-third-party-apps/). *BGR*. Retrieved 2017-06-27.
60. [↑](./Long_short-term_memory#cite_ref-capes2017_60-0) Capes, Tim; Coles, Paul; Conkie, Alistair; Golipour, Ladan; Hadjitarkhani, Abie; Hu, Qiong; Huddleston, Nancy; Hunt, Melvyn; Li, Jiangchuan; Neeracher, Matthias; Prahallad, Kishore (2017-08-20). ["Siri On-Device Deep Learning-Guided Unit Selection Text-to-Speech System"](http://www.isca-speech.org/archive/Interspeech_2017/abstracts/1798.html). *Interspeech 2017*. ISCA: 4011–4015. [doi](./Doi_(identifier)):[10.21437/Interspeech.2017-1798](https://doi.org/10.21437%2FInterspeech.2017-1798).
61. [↑](./Long_short-term_memory#cite_ref-AmazonAlexa_61-0) Vogels, Werner (30 November 2016). ["Bringing the Magic of Amazon AI and Alexa to Apps on AWS. – All Things Distributed"](http://www.allthingsdistributed.com/2016/11/amazon-ai-and-alexa-for-all-aws-apps.html). *www.allthingsdistributed.com*. Retrieved 2017-06-27.
62. [↑](./Long_short-term_memory#cite_ref-62) Xiong, W.; Wu, L.; Alleva, F.; Droppo, J.; Huang, X.; Stolcke, A. (April 2018). "The Microsoft 2017 Conversational Speech Recognition System". *2018 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)*. IEEE. pp. 5934–5938. [arXiv](./ArXiv_(identifier)):[1708.06073](https://arxiv.org/abs/1708.06073). [doi](./Doi_(identifier)):[10.1109/ICASSP.2018.8461870](https://doi.org/10.1109%2FICASSP.2018.8461870). [ISBN](./ISBN_(identifier)) [978-1-5386-4658-8](./Special:BookSources/978-1-5386-4658-8).
63. [1](./Long_short-term_memory#cite_ref-miraculous2021_63-0) [2](./Long_short-term_memory#cite_ref-miraculous2021_63-1) [3](./Long_short-term_memory#cite_ref-miraculous2021_63-2) [4](./Long_short-term_memory#cite_ref-miraculous2021_63-3) [5](./Long_short-term_memory#cite_ref-miraculous2021_63-4) [6](./Long_short-term_memory#cite_ref-miraculous2021_63-5) Schmidhuber, Juergen (10 May 2021). "Deep Learning: Our Miraculous Year 1990-1991". [arXiv](./ArXiv_(identifier)):[2005.05744](https://arxiv.org/abs/2005.05744) [[cs.NE](https://arxiv.org/archive/cs.NE)].
64. [↑](./Long_short-term_memory#cite_ref-mozer1989_64-0) Mozer, Mike (1989). "A Focused Backpropagation Algorithm for Temporal Pattern Recognition". *Complex Systems*.
65. [↑](./Long_short-term_memory#cite_ref-DLhistory_65-0) [Schmidhuber, Juergen](./Juergen_Schmidhuber) (2022). "Annotated History of Modern AI and Deep Learning". [arXiv](./ArXiv_(identifier)):[2212.11279](https://arxiv.org/abs/2212.11279) [[cs.NE](https://arxiv.org/archive/cs.NE)].
66. [↑](./Long_short-term_memory#cite_ref-66) [Sepp Hochreiter](./Sepp_Hochreiter); [Jürgen Schmidhuber](./Jürgen_Schmidhuber) (21 August 1995), [*Long Short Term Memory*](ftp://ftp.idsia.ch/pub/juergen/fki-207-95.ps.gz), [Wikidata](./WDQ_(identifier)) [Q98967430](https://www.wikidata.org/wiki/Q98967430)[*[dead link](./Wikipedia:Link_rot)*]
67. [1](./Long_short-term_memory#cite_ref-ASearchSpaceOdyssey_67-0) [2](./Long_short-term_memory#cite_ref-ASearchSpaceOdyssey_67-1) [3](./Long_short-term_memory#cite_ref-ASearchSpaceOdyssey_67-2) Klaus Greff; Rupesh Kumar Srivastava; Jan Koutník; Bas R. Steunebrink; Jürgen Schmidhuber (2015). "LSTM: A Search Space Odyssey". *IEEE Transactions on Neural Networks and Learning Systems*. **28** (10): 2222–2232. [arXiv](./ArXiv_(identifier)):[1503.04069](https://arxiv.org/abs/1503.04069). [Bibcode](./Bibcode_(identifier)):[2015arXiv150304069G](https://ui.adsabs.harvard.edu/abs/2015arXiv150304069G). [doi](./Doi_(identifier)):[10.1109/TNNLS.2016.2582924](https://doi.org/10.1109%2FTNNLS.2016.2582924). [PMID](./PMID_(identifier)) [27411231](https://pubmed.ncbi.nlm.nih.gov/27411231). [S2CID](./S2CID_(identifier)) [3356463](https://api.semanticscholar.org/CorpusID:3356463).
68. [1](./Long_short-term_memory#cite_ref-lstm1999_68-0) [2](./Long_short-term_memory#cite_ref-lstm1999_68-1) [3](./Long_short-term_memory#cite_ref-lstm1999_68-2) Gers, Felix; Schmidhuber, Jürgen; Cummins, Fred (1999). "Learning to forget: Continual prediction with LSTM". *9th International Conference on Artificial Neural Networks: ICANN '99*. Vol. 1999. pp. 850–855. [doi](./Doi_(identifier)):[10.1049/cp:19991218](https://doi.org/10.1049%2Fcp%3A19991218). [ISBN](./ISBN_(identifier)) [0-85296-721-7](./Special:BookSources/0-85296-721-7).
69. [↑](./Long_short-term_memory#cite_ref-cho2014_69-0) Cho, Kyunghyun; van Merrienboer, Bart; Gulcehre, Caglar; Bahdanau, Dzmitry; Bougares, Fethi; Schwenk, Holger; Bengio, Yoshua (2014). "Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation". [arXiv](./ArXiv_(identifier)):[1406.1078](https://arxiv.org/abs/1406.1078) [[cs.CL](https://arxiv.org/archive/cs.CL)].
70. [↑](./Long_short-term_memory#cite_ref-highway2015_70-0) Srivastava, Rupesh Kumar; Greff, Klaus; Schmidhuber, Jürgen (2 May 2015). "Highway Networks". [arXiv](./ArXiv_(identifier)):[1505.00387](https://arxiv.org/abs/1505.00387) [[cs.LG](https://arxiv.org/archive/cs.LG)].
71. [↑](./Long_short-term_memory#cite_ref-highway2015neurips_71-0) Srivastava, Rupesh K; Greff, Klaus; Schmidhuber, Juergen (December 2015).  Written at Montreal, Canada. [*Training Very Deep Networks*](https://dl.acm.org/doi/10.5555/2969442.2969505). NIPS'15: Proceedings of the 29th International Conference on Neural Information Processing Systems. Vol. 2. Cambridge, MA, United States: MIT Press. pp. 2377–2385.
72. [↑](./Long_short-term_memory#cite_ref-mostcited2021_72-0) Schmidhuber, Jürgen (2021). ["The most cited neural networks all build on work done in my labs"](https://people.idsia.ch/~juergen/most-cited-neural-nets.html). *AI Blog*. IDSIA, Switzerland. Retrieved 2022-04-30.
73. [↑](./Long_short-term_memory#cite_ref-resnet2015_73-0) He, Kaiming; Zhang, Xiangyu; Ren, Shaoqing; Sun, Jian (2016). "Deep Residual Learning for Image Recognition". *2016 IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*. IEEE. pp. 770–778. [arXiv](./ArXiv_(identifier)):[1512.03385](https://arxiv.org/abs/1512.03385). [doi](./Doi_(identifier)):[10.1109/CVPR.2016.90](https://doi.org/10.1109%2FCVPR.2016.90). [ISBN](./ISBN_(identifier)) [978-1-4673-8851-1](./Special:BookSources/978-1-4673-8851-1).
74. [↑](./Long_short-term_memory#cite_ref-74) Beck, Maximilian; Pöppel, Korbinian; Spanring, Markus; Auer, Andreas; Prudnikova, Oleksandra; Kopp, Michael; Klambauer, Günter; Brandstetter, Johannes; Hochreiter, Sepp (2024-05-07). "xLSTM: Extended Long Short-Term Memory". [arXiv](./ArXiv_(identifier)):[2405.04517](https://arxiv.org/abs/2405.04517) [[cs.LG](https://arxiv.org/archive/cs.LG)].
75. [↑](./Long_short-term_memory#cite_ref-75) [*NX-AI/xlstm*](https://github.com/NX-AI/xlstm), NXAI, 2024-06-04, retrieved 2024-06-04
76. [↑](./Long_short-term_memory#cite_ref-76) Hochreiter, S.; Younger, A. S.; Conwell, P. R. (2001). "Learning to Learn Using Gradient Descent". [*Artificial Neural Networks — ICANN 2001*](http://www.bioinf.jku.at/publications/older/1504.pdf) (PDF). Lecture Notes in Computer Science. Vol. 2130. pp. 87–94. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.5.323](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.5.323). [doi](./Doi_(identifier)):[10.1007/3-540-44668-0_13](https://doi.org/10.1007%2F3-540-44668-0_13). [ISBN](./ISBN_(identifier)) [978-3-540-42486-4](./Special:BookSources/978-3-540-42486-4). [ISSN](./ISSN_(identifier)) [0302-9743](https://search.worldcat.org/issn/0302-9743). [S2CID](./S2CID_(identifier)) [52872549](https://api.semanticscholar.org/CorpusID:52872549).
77. [↑](./Long_short-term_memory#cite_ref-graves2004_77-0) Graves, Alex; Beringer, Nicole; Eck, Douglas; Schmidhuber, Juergen (2004). *Biologically Plausible Speech Recognition with LSTM Neural Nets*. Workshop on Biologically Inspired Approaches to Advanced Information Technology, Bio-ADIT 2004, Lausanne, Switzerland. pp. 175–184.
78. [↑](./Long_short-term_memory#cite_ref-wierstra2007_78-0) Wierstra, Daan; Foerster, Alexander; Peters, Jan; Schmidhuber, Juergen (2005). ["Solving Deep Memory POMDPs with Recurrent Policy Gradients"](https://people.idsia.ch/~juergen/lstm-policy-gradient-2010.html). *International Conference on Artificial Neural Networks ICANN'07*.
79. [↑](./Long_short-term_memory#cite_ref-bayer2009_79-0) Bayer, Justin; Wierstra, Daan; Togelius, Julian; Schmidhuber, Juergen (2009). "Evolving memory cell structures for sequence learning". *International Conference on Artificial Neural Networks ICANN'09, Cyprus*.
80. [↑](./Long_short-term_memory#cite_ref-graves2009_80-0) Graves, A.; Liwicki, M.; Fernández, S.; Bertolami, R.; Bunke, H.; Schmidhuber, J. (May 2009). "A Novel Connectionist System for Unconstrained Handwriting Recognition". *IEEE Transactions on Pattern Analysis and Machine Intelligence*. **31** (5): 855–868. [Bibcode](./Bibcode_(identifier)):[2009ITPAM..31..855G](https://ui.adsabs.harvard.edu/abs/2009ITPAM..31..855G). [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.139.4502](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.139.4502). [doi](./Doi_(identifier)):[10.1109/tpami.2008.137](https://doi.org/10.1109%2Ftpami.2008.137). [ISSN](./ISSN_(identifier)) [0162-8828](https://search.worldcat.org/issn/0162-8828). [PMID](./PMID_(identifier)) [19299860](https://pubmed.ncbi.nlm.nih.gov/19299860). [S2CID](./S2CID_(identifier)) [14635907](https://api.semanticscholar.org/CorpusID:14635907).
81. [↑](./Long_short-term_memory#cite_ref-maergner2009_81-0) Märgner, Volker; Abed, Haikal El (July 2009). "ICDAR 2009 Arabic Handwriting Recognition Competition". *2009 10th International Conference on Document Analysis and Recognition*. pp. 1383–1387. [doi](./Doi_(identifier)):[10.1109/ICDAR.2009.256](https://doi.org/10.1109%2FICDAR.2009.256). [ISBN](./ISBN_(identifier)) [978-1-4244-4500-4](./Special:BookSources/978-1-4244-4500-4). [S2CID](./S2CID_(identifier)) [52851337](https://api.semanticscholar.org/CorpusID:52851337).
82. [↑](./Long_short-term_memory#cite_ref-82) Baytas, Inci M.; Xiao, Cao; Zhang, Xi; Wang, Fei; Jain, Anil K.; Zhou, Jiayu (2017-08-04). ["Patient Subtyping via Time-Aware LSTM Networks"](https://dl.acm.org/doi/pdf/10.1145/3097983.3097997). *Proceedings of the 23rd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*. New York, NY, USA: Association for Computing Machinery. pp. 65–74. [doi](./Doi_(identifier)):[10.1145/3097983.3097997](https://doi.org/10.1145%2F3097983.3097997). [ISBN](./ISBN_(identifier)) [978-1-4503-4887-4](./Special:BookSources/978-1-4503-4887-4).
83. [↑](./Long_short-term_memory#cite_ref-83) Kaplan, Jared; McCandlish, Sam; Henighan, Tom; Brown, Tom B.; Chess, Benjamin; Child, Rewon; Gray, Scott; Radford, Alec; Wu, Jeffrey; Amodei, Dario (2020). "Scaling Laws for Neural Language Models". [arXiv](./ArXiv_(identifier)):[2001.08361](https://arxiv.org/abs/2001.08361) [[cs.LG](https://arxiv.org/archive/cs.LG)].

 

## Further reading

 
- Sherstinsky, Alex (2018). "Fundamentals of Recurrent Neural Network (RNN) and Long Short-Term Memory (LSTM) Network". [arXiv](./ArXiv_(identifier)):[1808.03314](https://arxiv.org/abs/1808.03314) [[cs.LG](https://arxiv.org/archive/cs.LG)].
- Monner, Derek D.; Reggia, James A. (2010). ["A generalized LSTM-like training algorithm for second-order recurrent neural networks"](http://www.cs.umd.edu/~dmonner/papers/nn2012.pdf) (PDF). *Neural Networks*. **25** (1): 70–83. [doi](./Doi_(identifier)):[10.1016/j.neunet.2011.07.003](https://doi.org/10.1016%2Fj.neunet.2011.07.003). [PMC](./PMC_(identifier)) [3217173](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3217173). [PMID](./PMID_(identifier)) [21803542](https://pubmed.ncbi.nlm.nih.gov/21803542). High-performing extension of LSTM that has been simplified to a single node type and can train arbitrary architectures
- Gers, Felix A.; Schraudolph, Nicol N.; Schmidhuber, Jürgen (Aug 2002). ["Learning precise timing with LSTM recurrent networks"](http://www.jmlr.org/papers/volume3/gers02a/gers02a.pdf) (PDF). *Journal of Machine Learning Research*. **3**: 115–143.
- Gers, Felix (2001). ["Long Short-Term Memory in Recurrent Neural Networks"](http://www.felixgers.de/papers/phd.pdf) (PDF). *PhD thesis*.
- Abidogun, Olusola Adeniyi (2005). [*Data Mining, Fraud Detection and Mobile Telecommunications: Call Pattern Analysis with Unsupervised Neural Networks*](http://etd.uwc.ac.za/xmlui/handle/11394/249). *Master's Thesis* (Thesis). University of the Western Cape. [hdl](./Hdl_(identifier)):[11394/249](https://hdl.handle.net/11394%2F249). [Archived](https://web.archive.org/web/20120522234026/http://etd.uwc.ac.za/usrfiles/modules/etd/docs/etd_init_3937_1174040706.pdf) (PDF) from the original on May 22, 2012. 
- [original](http://etd.uwc.ac.za/bitstream/handle/11394/249/Abidogun_MSC_2005.pdf) with two chapters devoted to explaining recurrent neural networks, especially LSTM.

 

## External links

 
- [Recurrent Neural Networks](http://www.idsia.ch/~juergen/rnn.html) with over 30 LSTM papers by [Jürgen Schmidhuber](./Jürgen_Schmidhuber)'s group at [IDSIA](./IDSIA)
- Zhang, Aston; Lipton, Zachary; Li, Mu; Smola, Alexander J. (2024). ["10.1. Long Short-Term Memory (LSTM)"](https://d2l.ai/chapter_recurrent-modern/lstm.html). *Dive into deep learning*. Cambridge New York Port Melbourne New Delhi Singapore: Cambridge University Press. [ISBN](./ISBN_(identifier)) [978-1-009-38943-3](./Special:BookSources/978-1-009-38943-3).

 
| vteArtificial intelligence(AI) |
| --- |
| HistorytimelineGlossaryCompaniesProjectsList of open-source AI software |
| Concepts | Automated reasoningParameterHyperparameterLoss functionsRegressionBias–variance tradeoffDouble descentOverfittingClusteringGradient descentSGDQuasi-Newton methodConjugate gradient methodBackpropagationAttentionConvolutionNormalizationBatchnormActivationSoftmaxSigmoidRectifierGatingWeight initializationRegularizationDatasetsAugmentationPrompt engineeringReinforcement learningQ-learningSARSAImitationPolicy gradientDiffusionLatent diffusion modelAutoregressionAdversaryRAGUncanny valleyRLHFSelf-supervised learningReflectionRecursive self-improvementHallucinationWord embeddingVibe codingSymbolic AINeuro-symbolic AI |
| Applications | Automated theorem provingMachine learningIn-context learningArtificial neural networkDeep learningLanguage modelLargeNMTReasoningModel Context ProtocolIntelligent agentAI agentArtificial human companionHumanity's Last ExamLethal autonomous weapons (LAWs)Generative AIWeak AIHypotheticalArtificial general intelligence (AGI)Artificial superintelligence (ASI)Agent2Agent protocol |
| Implementations | Audio–visualAlexNetWaveNetHuman image synthesisHWROCRComputer visionSpeech synthesis15.aiElevenLabsSpeech recognitionWhisperFacial recognitionAlphaFoldText-to-image modelsAuroraDALL-EFireflyFluxGPT ImageIdeogramImagenMidjourneyRecraftStable DiffusionText-to-video modelsDream MachineRunway GenHailuo AIKlingSoraSeedanceVeoMusic generationRiffusionSunoUdioWorld modelsGenieOasisTextList of large language modelsProject DebaterIBM WatsonIBM WatsonxDecisionalAlphaGoAlphaZeroOpenAI FiveSelf-driving carMuZeroAction selectionAutoGPTRobot controlReasoning systemsDeductive classifiersExpert systemsInference enginesKnowledge-based systemsLogic programsProcedural reasoning systemsSemantic reasonersRule-based systemsCognitive architecturesACT-RSoarCLARIONLIDAOpenCogKnowledge basesConceptNetWikidataDBpediaYAGO | Audio–visual | AlexNetWaveNetHuman image synthesisHWROCRComputer visionSpeech synthesis15.aiElevenLabsSpeech recognitionWhisperFacial recognitionAlphaFoldText-to-image modelsAuroraDALL-EFireflyFluxGPT ImageIdeogramImagenMidjourneyRecraftStable DiffusionText-to-video modelsDream MachineRunway GenHailuo AIKlingSoraSeedanceVeoMusic generationRiffusionSunoUdioWorld modelsGenieOasis | Text | List of large language modelsProject DebaterIBM WatsonIBM Watsonx | Decisional | AlphaGoAlphaZeroOpenAI FiveSelf-driving carMuZeroAction selectionAutoGPTRobot control | Reasoning systems | Deductive classifiersExpert systemsInference enginesKnowledge-based systemsLogic programsProcedural reasoning systemsSemantic reasonersRule-based systems | Cognitive architectures | ACT-RSoarCLARIONLIDAOpenCog | Knowledge bases | ConceptNetWikidataDBpediaYAGO |
| Audio–visual | AlexNetWaveNetHuman image synthesisHWROCRComputer visionSpeech synthesis15.aiElevenLabsSpeech recognitionWhisperFacial recognitionAlphaFoldText-to-image modelsAuroraDALL-EFireflyFluxGPT ImageIdeogramImagenMidjourneyRecraftStable DiffusionText-to-video modelsDream MachineRunway GenHailuo AIKlingSoraSeedanceVeoMusic generationRiffusionSunoUdioWorld modelsGenieOasis |
| Text | List of large language modelsProject DebaterIBM WatsonIBM Watsonx |
| Decisional | AlphaGoAlphaZeroOpenAI FiveSelf-driving carMuZeroAction selectionAutoGPTRobot control |
| Reasoning systems | Deductive classifiersExpert systemsInference enginesKnowledge-based systemsLogic programsProcedural reasoning systemsSemantic reasonersRule-based systems |
| Cognitive architectures | ACT-RSoarCLARIONLIDAOpenCog |
| Knowledge bases | ConceptNetWikidataDBpediaYAGO |
| People | Alan TuringWarren Sturgis McCullochWalter PittsJohn von NeumannChristopher D. ManningClaude ShannonShun'ichi AmariKunihiko FukushimaTakeo KanadeMarvin MinskyJohn McCarthyNathaniel RochesterAllen NewellCliff ShawHerbert A. SimonOliver SelfridgeFrank RosenblattBernard WidrowJoseph WeizenbaumSeymour PapertSeppo LinnainmaaPaul WerbosGeoffrey HintonJohn HopfieldJürgen SchmidhuberYann LeCunYoshua BengioLotfi A. ZadehStephen GrossbergAlex GravesJames GoodnightAndrew NgFei-Fei LiAlex KrizhevskyIlya SutskeverOriol VinyalsQuoc V. LeIan GoodfellowDemis HassabisDavid SilverAndrej KarpathyAshish VaswaniNoam ShazeerAidan GomezJohn SchulmanMustafa SuleymanJan LeikeDaniel KokotajloFrançois Chollet |
| Neural network architectures | Neural Turing machineDifferentiable neural computerTransformerVision transformer (ViT)Recurrent neural network (RNN)Long short-term memory (LSTM)Gated recurrent unit (GRU)Echo state networkMultilayer perceptron (MLP)Convolutional neural network (CNN)Residual neural network (RNN)Highway networkMambaAutoencoderVariational autoencoder (VAE)Generative adversarial network (GAN)Graph neural network (GNN) |
| Political | AI Cold WarAI safety(Alignment)AI takeoverElectionsEthics of AIEUAI ActNationalismPrecautionary principleRegulation of AIUSVirtual politicianPropaganda |
| Social and economic | AI boomAI bubbleAI data centerAI effectAI literacyAI slopAI veganismAI winterAnthropomorphismArms raceCompetitionEnvironmental impactExplainable AIGenerative engine optimizationIn architectureIn educationIn fictionIn healthcareChatbot psychosisIn marketingIn video gamesIn visual artMilitary applicationsAI warfareWorkplace impact |
| Category |