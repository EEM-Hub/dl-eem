---
source: sources/wiki-Autoencoder.md
source_url: https://en.wikipedia.org/wiki/Autoencoder
chunk: 1/4
---

Neural network that learns efficient data encoding in an unsupervised manner Not to be confused with [Autocoder](./Autocoder) or [Autocode](./Autocode). 

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/3/37/Autoencoder_schema.png/330px-Autoencoder_schema.png)](./File:Autoencoder_schema.png)A schema of an *autoencoder*. An autoencoder has two main parts: an *encoder* that maps the message to a code, and a *decoder* that reconstructs the message from the code. 
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

 

An **autoencoder** is a type of [artificial neural network](./Artificial_neural_network) used to learn [efficient codings](./Feature_learning) of unlabeled data ([unsupervised learning](./Unsupervised_learning)). An autoencoder learns two functions: an encoding function that transforms the input data, and a decoding function that recreates the input data from the encoded representation. The autoencoder learns an efficient representation (encoding) for a set of data, typically for [dimensionality reduction](./Dimensionality_reduction), to generate lower-dimensional embeddings for subsequent use by other [machine learning](./Machine_learning) algorithms.[[1]](./Autoencoder#cite_note-1)

 

Variants exist which aim to make the learned representations assume useful properties.[[2]](./Autoencoder#cite_note-:0-2) Examples are regularized autoencoders (*sparse*, *denoising* and *contractive* autoencoders), which are effective in learning representations for subsequent [classification](./Statistical_classification) tasks,[[3]](./Autoencoder#cite_note-:4-3) and [*variational* autoencoders](./Variational_autoencoder), which can be used as [generative models](./Generative_model).[[4]](./Autoencoder#cite_note-:11-4) Autoencoders are applied to many problems, including [facial recognition](./Facial_recognition_system),[[5]](./Autoencoder#cite_note-5) [feature detection](./Feature_(computer_vision)),[[6]](./Autoencoder#cite_note-:2-6) [anomaly detection](./Anomaly_detection), and [learning the meaning of words](./Word_embedding).[[7]](./Autoencoder#cite_note-7)[[8]](./Autoencoder#cite_note-8) In terms of [data synthesis](./Synthetic_data), autoencoders can also be used to randomly generate new data that is similar to the input (training) data.[[6]](./Autoencoder#cite_note-:2-6)

  

## Mathematical principles

 

### Definition

An autoencoder is defined by the following components: 

Two sets: the space of encoded messages       Z     {\displaystyle {\mathcal {Z}}}  ![{\displaystyle {\mathcal {Z}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be1e2c3c82e7b8055fe26eb4cf2caac6f8ec73); the space of decoded messages       X     {\displaystyle {\mathcal {X}}}  ![{\displaystyle {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c7e5461c5286852df4ef652fca7e4b0b63030e9). Typically       X     {\displaystyle {\mathcal {X}}}  ![{\displaystyle {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c7e5461c5286852df4ef652fca7e4b0b63030e9) and       Z     {\displaystyle {\mathcal {Z}}}  ![{\displaystyle {\mathcal {Z}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be1e2c3c82e7b8055fe26eb4cf2caac6f8ec73) are [Euclidean spaces](./Euclidean_space), that is,       X   =   R   m   ,   Z   =   R   n     {\displaystyle {\mathcal {X}}=\mathbb {R} ^{m},{\mathcal {Z}}=\mathbb {R} ^{n}}  ![{\displaystyle {\mathcal {X}}=\mathbb {R} ^{m},{\mathcal {Z}}=\mathbb {R} ^{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0019b12cb0c515f608bdec62ff3e31248ce282f0) with     m > n .   {\displaystyle m>n.}  ![{\displaystyle m>n.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/982733f442459689d943182858c50d3942aaa764) 

Two [parametrized](./Parameterization) families of functions: the encoder family      E  ϕ ϕ    :   X   → →    Z     {\displaystyle E_{\phi }:{\mathcal {X}}\rightarrow {\mathcal {Z}}}  ![{\displaystyle E_{\phi }:{\mathcal {X}}\rightarrow {\mathcal {Z}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1ca207ad612d4f68f449647ef438f20fc6f1dfd8), parametrized by     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4); the decoder family      D  θ θ    :   Z   → →    X     {\displaystyle D_{\theta }:{\mathcal {Z}}\rightarrow {\mathcal {X}}}  ![{\displaystyle D_{\theta }:{\mathcal {Z}}\rightarrow {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f67a834ca4cd55d93088f2ca566739c100500f75), parametrized by     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af).

For any     x ∈ ∈    X     {\displaystyle x\in {\mathcal {X}}}  ![{\displaystyle x\in {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b3cd596d560b9f3bc71615911c2438cbbf49c15), we usually write     z =  E  ϕ ϕ    ( x )   {\displaystyle z=E_{\phi }(x)}  ![{\displaystyle z=E_{\phi }(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/002c12f50476471d3e541bdd77f7a522cbd80444), and refer to it as the code, the [latent variable](./Latent_variable), latent representation, latent vector, etc. Conversely, for any     z ∈ ∈    Z     {\displaystyle z\in {\mathcal {Z}}}  ![{\displaystyle z\in {\mathcal {Z}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3fd7a639b0e1c2ba8d6825ca79b144c906980979), we usually write      x ′  =  D  θ θ    ( z )   {\displaystyle x'=D_{\theta }(z)}  ![{\displaystyle x'=D_{\theta }(z)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2959b5a51a87eac650c51768411b6a310c197b67), and refer to it as the (decoded) message.

 

Usually, both the encoder and the decoder are defined as [multilayer perceptrons](./Multilayer_perceptron) (MLPs). For example, a one-layer-MLP encoder      E  ϕ ϕ      {\displaystyle E_{\phi }}  ![{\displaystyle E_{\phi }}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c08f0cada78242b00f566df96531e52fc6277fb6) is:

      E  ϕ ϕ    (  x  ) = σ σ  ( W x + b )   {\displaystyle E_{\phi }(\mathbf {x} )=\sigma (Wx+b)}  ![{\displaystyle E_{\phi }(\mathbf {x} )=\sigma (Wx+b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8ce6546eb990e3b456b461f905fcf795affbddd9) 

where     σ σ    {\displaystyle \sigma }  ![{\displaystyle \sigma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/59f59b7c3e6fdb1d0365a494b81fb9a696138c36) is an element-wise [activation function](./Activation_function),     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7) is a "weight" matrix, and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) is a "bias" vector.

 

### Training an autoencoder

 

An autoencoder, by itself, is simply a tuple of two functions. To judge its *quality*, we need a *task*. A task is defined by a reference probability distribution      μ μ   r e f     {\displaystyle \mu _{ref}}  ![{\displaystyle \mu _{ref}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/15d15b590538ca3450d814c51e7707812a8c26b4) over       X     {\displaystyle {\mathcal {X}}}  ![{\displaystyle {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c7e5461c5286852df4ef652fca7e4b0b63030e9), and a "reconstruction quality" function     d :   X   × ×    X   → →  [ 0 , ∞ ∞  ]   {\displaystyle d:{\mathcal {X}}\times {\mathcal {X}}\to [0,\infty ]}  ![{\displaystyle d:{\mathcal {X}}\times {\mathcal {X}}\to [0,\infty ]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e69538969fb3dc0706fb3368e6312ccb95cf2d6e), such that     d ( x ,  x ′  )   {\displaystyle d(x,x')}  ![{\displaystyle d(x,x')}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c46ecfdcff1eb6b830f767255959144e33e680a3) measures how much      x ′    {\displaystyle x'}  ![{\displaystyle x'}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0ac74959896052e160a5953102e4bc3850fe93b2) differs from     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4).

 

With those, we can define the loss function for the autoencoder as    L ( θ θ  , ϕ ϕ  ) :=    E    x ∼ ∼   μ μ   r e f     [ d ( x ,  D  θ θ    (  E  ϕ ϕ    ( x ) ) ) ]   {\displaystyle L(\theta ,\phi ):=\mathbb {\mathbb {E} } _{x\sim \mu _{ref}}[d(x,D_{\theta }(E_{\phi }(x)))]}  ![{\displaystyle L(\theta ,\phi ):=\mathbb {\mathbb {E} } _{x\sim \mu _{ref}}[d(x,D_{\theta }(E_{\phi }(x)))]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b67d5c0347ed7cd5dab78196fe3501a843f97d34)The *optimal* autoencoder for the given task     (  μ μ   r e f   , d )   {\displaystyle (\mu _{ref},d)}  ![{\displaystyle (\mu _{ref},d)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4077502606b9dc074830c1abca71cc750b87fed4) is then     arg ⁡ ⁡   min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  )   {\displaystyle \arg \min _{\theta ,\phi }L(\theta ,\phi )}  ![{\displaystyle \arg \min _{\theta ,\phi }L(\theta ,\phi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/be5f1d9e9e86289264951861390a1649e7c99952). The search for the optimal autoencoder can be accomplished by any mathematical optimization technique, but usually by [gradient descent](./Gradient_descent). This search process is referred to as "training the autoencoder".

 

In most situations, the reference distribution is just the [empirical distribution](./Empirical_measure) given by a dataset     {  x  1   , . . . ,  x  N   } ⊂ ⊂    X     {\displaystyle \{x_{1},...,x_{N}\}\subset {\mathcal {X}}}  ![{\displaystyle \{x_{1},...,x_{N}\}\subset {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f6afdb997fd084fba75fed0afa6e9b1658c11821), so that     μ μ   r e f   =   1 N    ∑ ∑   i = 1   N    δ δ    x  i       {\displaystyle \mu _{ref}={\frac {1}{N}}\sum _{i=1}^{N}\delta _{x_{i}}}  ![{\displaystyle \mu _{ref}={\frac {1}{N}}\sum _{i=1}^{N}\delta _{x_{i}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d63652bf750ae452bed32819120001ee060b105f)

 

where      δ δ    x  i       {\displaystyle \delta _{x_{i}}}  ![{\displaystyle \delta _{x_{i}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/472764bb2606d7dfd874da3b4dce1075678a15d1) is the [Dirac measure](./Dirac_measure), the quality function is just      L  2     {\displaystyle L^{2}}  ![{\displaystyle L^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba162c66ca85776c83557af5088cc6f8584d1912) loss:     d ( x ,  x ′  ) = ‖ ‖  x − −   x ′   ‖ ‖   2   2     {\displaystyle d(x,x')=\|x-x'\|_{2}^{2}}  ![{\displaystyle d(x,x')=\|x-x'\|_{2}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/76cf47d547a92f5e5bc7938b525ce8d3fa8d7a55), and     ‖ ‖  ⋅ ⋅   ‖ ‖   2     {\displaystyle \|\cdot \|_{2}}  ![{\displaystyle \|\cdot \|_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b3a8e44a2eb980f856968a6357e3d0a7c22c905f) is the [Euclidean norm](./Norm_(mathematics)#Euclidean_norm). Then the problem of searching for the optimal autoencoder is just a [least-squares](./Least_squares) optimization:     min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  ) ,   where   L ( θ θ  , ϕ ϕ  ) =   1 N    ∑ ∑   i = 1   N   ‖ ‖   x  i   − −   D  θ θ    (  E  ϕ ϕ    (  x  i   ) )  ‖ ‖   2   2     {\displaystyle \min _{\theta ,\phi }L(\theta ,\phi ),\qquad {\text{where }}L(\theta ,\phi )={\frac {1}{N}}\sum _{i=1}^{N}\|x_{i}-D_{\theta }(E_{\phi }(x_{i}))\|_{2}^{2}}  ![{\displaystyle \min _{\theta ,\phi }L(\theta ,\phi ),\qquad {\text{where }}L(\theta ,\phi )={\frac {1}{N}}\sum _{i=1}^{N}\|x_{i}-D_{\theta }(E_{\phi }(x_{i}))\|_{2}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3cb4a557857908505588af248b8abfc682e3cb5)

 

### Interpretation

 

An autoencoder has two main parts: an encoder that maps the message to a code, and a decoder that reconstructs the message from the code. An optimal autoencoder would perform as close to perfect reconstruction as possible, with "close to perfect" defined by the reconstruction quality function     d   {\displaystyle d}  ![{\displaystyle d}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e85ff03cbe0c7341af6b982e47e9f90d235c66ab).

 

The simplest way to perform the copying task perfectly would be to duplicate the signal. To suppress this behavior, the code space       Z     {\displaystyle {\mathcal {Z}}}  ![{\displaystyle {\mathcal {Z}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be1e2c3c82e7b8055fe26eb4cf2caac6f8ec73) usually has fewer dimensions than the message space       X     {\displaystyle {\mathcal {X}}}  ![{\displaystyle {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c7e5461c5286852df4ef652fca7e4b0b63030e9).

 

Such an autoencoder is called *undercomplete*. It can be interpreted as [compressing](./Data_compression) the message, or [reducing its dimensionality](./Dimensionality_reduction).[[9]](./Autoencoder#cite_note-:12-9)[[10]](./Autoencoder#cite_note-:7-10)

 

At the limit of an ideal undercomplete autoencoder, every possible code     z   {\displaystyle z}  ![{\displaystyle z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf368e72c009decd9b6686ee84a375632e11de98) in the code space is used to encode a message     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) that really appears in the distribution      μ μ   r e f     {\displaystyle \mu _{ref}}  ![{\displaystyle \mu _{ref}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/15d15b590538ca3450d814c51e7707812a8c26b4), and the decoder is also perfect:      D  θ θ    (  E  ϕ ϕ    ( x ) ) = x   {\displaystyle D_{\theta }(E_{\phi }(x))=x}  ![{\displaystyle D_{\theta }(E_{\phi }(x))=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e539ece922d70a8af7087f56daa66c223f0f926f). This ideal autoencoder can then be used to generate messages indistinguishable from real messages, by feeding its decoder arbitrary code     z   {\displaystyle z}  ![{\displaystyle z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf368e72c009decd9b6686ee84a375632e11de98) and obtaining      D  θ θ    ( z )   {\displaystyle D_{\theta }(z)}  ![{\displaystyle D_{\theta }(z)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0f3eb8bf3238f6523cbceb2e714035f08aad6b84), which is a message that really appears in the distribution      μ μ   r e f     {\displaystyle \mu _{ref}}  ![{\displaystyle \mu _{ref}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/15d15b590538ca3450d814c51e7707812a8c26b4).

 

If the code space       Z     {\displaystyle {\mathcal {Z}}}  ![{\displaystyle {\mathcal {Z}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be1e2c3c82e7b8055fe26eb4cf2caac6f8ec73) has dimension larger than (*overcomplete*), or equal to, the message space       X     {\displaystyle {\mathcal {X}}}  ![{\displaystyle {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c7e5461c5286852df4ef652fca7e4b0b63030e9), or the hidden units are given enough capacity, an autoencoder can learn the [identity function](./Identity_function) and become useless. However, experimental results found that overcomplete autoencoders might still [learn useful features](./Feature_learning).[[11]](./Autoencoder#cite_note-bengio-11)

 

In the ideal setting, the code dimension and the model capacity could be set on the basis of the complexity of the data distribution to be modeled. A standard way to do so is to add modifications to the basic autoencoder, to be detailed below.[[2]](./Autoencoder#cite_note-:0-2)

 


