---
source: https://en.wikipedia.org/wiki/Autoencoder
fetched: 2026-06-21
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

 

## Variations

 

### Variational autoencoder (VAE)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/4a/VAE_Basic.png/330px-VAE_Basic.png)](./File:VAE_Basic.png)The basic scheme of a variational autoencoder. The model receives     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) as input. The encoder compresses it into the latent space. The decoder receives as input the information sampled from the latent space and produces       x ′     {\displaystyle {x'}}  ![{\displaystyle {x'}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223f94a9c179ffeb6e74e3208a27070a69f3f93) as similar as possible to     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4). Main article: [Variational autoencoder](./Variational_autoencoder) 

[Variational autoencoders](./Variational_autoencoder) (VAEs) belong to the families of [variational Bayesian methods](./Variational_Bayesian_methods). Despite the architectural similarities with basic autoencoders, VAEs are architected with different goals and have a different mathematical formulation. The latent space is, in this case, composed of a mixture of distributions instead of fixed vectors.

 

Given an input dataset     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) characterized by an unknown probability function     P ( x )   {\displaystyle P(x)}  ![{\displaystyle P(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/89833156eff2c51bfb8750db3306a0544ce34e14) and a multivariate latent encoding vector     z   {\displaystyle z}  ![{\displaystyle z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf368e72c009decd9b6686ee84a375632e11de98), the objective is to model the data as a distribution      p  θ θ    ( x )   {\displaystyle p_{\theta }(x)}  ![{\displaystyle p_{\theta }(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1f0682b1f715edb12932100f59e93d012e4ec886), with     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af) defined as the set of the network parameters so that      p  θ θ    ( x ) =  ∫ ∫   z    p  θ θ    ( x , z ) d z   {\displaystyle p_{\theta }(x)=\int _{z}p_{\theta }(x,z)dz}  ![{\displaystyle p_{\theta }(x)=\int _{z}p_{\theta }(x,z)dz}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a18e1df9f777fee6a6ca3549ba5b1d014f689444).

 

### Sparse autoencoder (SAE)

Inspired by the [sparse coding](./Sparse_coding) hypothesis in neuroscience, *sparse autoencoders* (SAE) are variants of autoencoders, such that the codes      E  ϕ ϕ    ( x )   {\displaystyle E_{\phi }(x)}  ![{\displaystyle E_{\phi }(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d62337867b116b3895877e218f11ed8223e1d793) for messages tend to be *sparse codes*, that is,      E  ϕ ϕ    ( x )   {\displaystyle E_{\phi }(x)}  ![{\displaystyle E_{\phi }(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d62337867b116b3895877e218f11ed8223e1d793) is close to zero in most entries. Sparse autoencoders may include more (rather than fewer) hidden units than inputs, but only a small number of the hidden units are allowed to be active at the same time.[[12]](./Autoencoder#cite_note-domingos-12) Encouraging sparsity improves performance on classification tasks.[[13]](./Autoencoder#cite_note-:1-13) 

[![](//upload.wikimedia.org/wikipedia/commons/thumb/8/83/Autoencoder_sparso.png/250px-Autoencoder_sparso.png)](./File:Autoencoder_sparso.png)Simple schema of a single-layer sparse autoencoder. The hidden nodes in bright yellow are activated, while the light yellow ones are inactive. The activation depends on the input. 

There are two main ways to enforce sparsity. One way is to simply clamp all but the highest-k activations of the latent code to zero. This is the **k-sparse autoencoder**.[[13]](./Autoencoder#cite_note-:1-13)

 

The k-sparse autoencoder inserts the following "k-sparse function" in the latent layer of a standard autoencoder:     f  k   (  x  1   , . . . ,  x  n   ) = (  x  1    b  1   , . . . ,  x  n    b  n   )   {\displaystyle f_{k}(x_{1},...,x_{n})=(x_{1}b_{1},...,x_{n}b_{n})}  ![{\displaystyle f_{k}(x_{1},...,x_{n})=(x_{1}b_{1},...,x_{n}b_{n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e0230c8bdf0bbfd0c70e316b90d47ca6f180f5d6)where      b  i   = 1   {\displaystyle b_{i}=1}  ![{\displaystyle b_{i}=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be70edf0d554ce09ecff0b8c16e5a53a9c606a) if      |   x  i    |    {\displaystyle |x_{i}|}  ![{\displaystyle |x_{i}|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92da0dacc0f9f069128bdd9b4c7de82cf81c2aed) ranks in the top k, and 0 otherwise.

 

Backpropagating through      f  k     {\displaystyle f_{k}}  ![{\displaystyle f_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8a585492f646ca803bc408103a0c705dd67ab8b7) is simple: set gradient to 0 for      b  i   = 0   {\displaystyle b_{i}=0}  ![{\displaystyle b_{i}=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a1fdd6a52e2a95d37ce0fbccbb56dad6b4083a0) entries, and keep gradient for      b  i   = 1   {\displaystyle b_{i}=1}  ![{\displaystyle b_{i}=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be70edf0d554ce09ecff0b8c16e5a53a9c606a) entries. This is essentially a generalized [ReLU](./Rectifier_(neural_networks)) function.[[13]](./Autoencoder#cite_note-:1-13)

 

The other way is a [relaxed version](./Relaxation_(approximation)) of the k-sparse autoencoder. Instead of forcing sparsity, we add a **sparsity regularization loss**, then optimize for     min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  ) + λ λ   L  sparse   ( θ θ  , ϕ ϕ  )   {\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{sparse}}(\theta ,\phi )}  ![{\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{sparse}}(\theta ,\phi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e2b184d62f4d8db4863873eab8ed7a9e243f63a5)where     λ λ  > 0   {\displaystyle \lambda >0}  ![{\displaystyle \lambda >0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eea25afc0351140f919cf791c49c1964b8b081de) measures how much sparsity we want to enforce.[[14]](./Autoencoder#cite_note-:6-14)

 

Let the autoencoder architecture have     K   {\displaystyle K}  ![{\displaystyle K}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b76fce82a62ed5461908f0dc8f037de4e3686b0) layers. To define a sparsity regularization loss, we need a "desired" sparsity         ρ ρ  ^ ^      k     {\displaystyle {\hat {\rho }}_{k}}  ![{\displaystyle {\hat {\rho }}_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0f8abe27fcb896ed54b2f4926c7fe9a46dd25983) for each layer, a weight      w  k     {\displaystyle w_{k}}  ![{\displaystyle w_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac808de3e1f01ed40c69d4a350035b19ab28445f) for how much to enforce each sparsity, and a function     s : [ 0 , 1 ] × ×  [ 0 , 1 ] → →  [ 0 , ∞ ∞  ]   {\displaystyle s:[0,1]\times [0,1]\to [0,\infty ]}  ![{\displaystyle s:[0,1]\times [0,1]\to [0,\infty ]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0cd8c20f4b06b6eeddda1f90d5d1b5589ed8e6c3) to measure how much two sparsities differ.

 

For each input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), let the actual sparsity of activation in each layer     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) be     ρ ρ   k   ( x ) =   1 n    ∑ ∑   i = 1   n    a  k , i   ( x )   {\displaystyle \rho _{k}(x)={\frac {1}{n}}\sum _{i=1}^{n}a_{k,i}(x)}  ![{\displaystyle \rho _{k}(x)={\frac {1}{n}}\sum _{i=1}^{n}a_{k,i}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/484a083542fc48db444072c35bf7438b4f5f335f)where      a  k , i   ( x )   {\displaystyle a_{k,i}(x)}  ![{\displaystyle a_{k,i}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d8db682dad885500aaebe6308322fbebe44d482) is the activation in the     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) -th neuron of the     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) -th layer upon input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4).

 

The sparsity loss upon input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) for one layer is     s (     ρ ρ  ^ ^      k   ,  ρ ρ   k   ( x ) )   {\displaystyle s({\hat {\rho }}_{k},\rho _{k}(x))}  ![{\displaystyle s({\hat {\rho }}_{k},\rho _{k}(x))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3727a598f770abd4f65df3e0abe7ac4929ac9027), and the sparsity regularization loss for the entire autoencoder is the expected weighted sum of sparsity losses:     L  sparse   ( θ θ  , ϕ ϕ  ) =    E    x ∼ ∼   μ μ   X      [   ∑ ∑   k ∈ ∈  1 : K    w  k   s (     ρ ρ  ^ ^      k   ,  ρ ρ   k   ( x ) )  ]    {\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}s({\hat {\rho }}_{k},\rho _{k}(x))\right]}  ![{\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}s({\hat {\rho }}_{k},\rho _{k}(x))\right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6384293aecb3ff69a6e8fee94b87546c533c4510)Typically, the function     s   {\displaystyle s}  ![{\displaystyle s}](https://wikimedia.org/api/rest_v1/media/math/render/svg/01d131dfd7673938b947072a13a9744fe997e632) is either the [Kullback–Leibler (KL) divergence](./Kullback–Leibler_divergence), as[[13]](./Autoencoder#cite_note-:1-13)[[14]](./Autoencoder#cite_note-:6-14)[[15]](./Autoencoder#cite_note-15)[[16]](./Autoencoder#cite_note-16)

     s ( ρ ρ  ,    ρ ρ  ^ ^     ) = K L ( ρ ρ   |   |     ρ ρ  ^ ^     ) = ρ ρ  log ⁡ ⁡    ρ ρ    ρ ρ  ^ ^      + ( 1 − −  ρ ρ  ) log ⁡ ⁡     1 − −  ρ ρ    1 − −     ρ ρ  ^ ^          {\displaystyle s(\rho ,{\hat {\rho }})=KL(\rho ||{\hat {\rho }})=\rho \log {\frac {\rho }{\hat {\rho }}}+(1-\rho )\log {\frac {1-\rho }{1-{\hat {\rho }}}}}  ![{\displaystyle s(\rho ,{\hat {\rho }})=KL(\rho ||{\hat {\rho }})=\rho \log {\frac {\rho }{\hat {\rho }}}+(1-\rho )\log {\frac {1-\rho }{1-{\hat {\rho }}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0460df1d442b4ccfb5d4e55243fe1ab5cb23e624) 

or the L1 loss, as     s ( ρ ρ  ,    ρ ρ  ^ ^     ) =  |  ρ ρ  − −     ρ ρ  ^ ^      |    {\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|}  ![{\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/97093ba0c58ecc04bd3c26a793b254cbd5ca0136), or the L2 loss, as     s ( ρ ρ  ,    ρ ρ  ^ ^     ) =  |  ρ ρ  − −     ρ ρ  ^ ^       |   2     {\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|^{2}}  ![{\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ee874b463a23a182bbd5c4cee0e25766262effdb).

 

Alternatively, the sparsity regularization loss may be defined without reference to any "desired sparsity", but simply force as much sparsity as possible. In this case, one can define the sparsity regularization loss as      L  sparse   ( θ θ  , ϕ ϕ  ) =    E    x ∼ ∼   μ μ   X      [   ∑ ∑   k ∈ ∈  1 : K    w  k   ‖ ‖   h  k   ‖ ‖   ]    {\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}\|h_{k}\|\right]}  ![{\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}\|h_{k}\|\right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8464dfd2872b84c2c4299a67fd9fcf1f57797d18)where      h  k     {\displaystyle h_{k}}  ![{\displaystyle h_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/78fe4f83c0bf136a170a0433c961330328b3596f) is the activation vector in the     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40)-th layer of the autoencoder. The norm     ‖ ‖  ⋅ ⋅  ‖ ‖    {\displaystyle \|\cdot \|}  ![{\displaystyle \|\cdot \|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/113f0d8fe6108fc1c5e9802f7c3f634f5480b3d1) is usually the L1 norm (giving the L1 sparse autoencoder) or the L2 norm (giving the L2 sparse autoencoder).

 

### Denoising autoencoder (DAE)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/1/18/Denoising-autoencoder.png/250px-Denoising-autoencoder.png)](./File:Denoising-autoencoder.png)A schema of a denoising autoencoder 

*Denoising autoencoders* (DAE) try to achieve a *good* representation by changing the *reconstruction criterion*.[[2]](./Autoencoder#cite_note-:0-2)[[3]](./Autoencoder#cite_note-:4-3)

 

A DAE, originally called a "robust autoassociative network" by Mark A. Kramer,[[17]](./Autoencoder#cite_note-:13-17) is trained by intentionally corrupting the inputs of a standard autoencoder during training. A noise process is defined by a probability distribution      μ μ   T     {\displaystyle \mu _{T}}  ![{\displaystyle \mu _{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a7c329840dcccf76c639e56c35ef3d56779d1fd5) over functions     T :   X   → →    X     {\displaystyle T:{\mathcal {X}}\to {\mathcal {X}}}  ![{\displaystyle T:{\mathcal {X}}\to {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/16f818c3ae1d1c6ef3b735161eb885fea2e1a645). That is, the function     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) takes a message     x ∈ ∈    X     {\displaystyle x\in {\mathcal {X}}}  ![{\displaystyle x\in {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b3cd596d560b9f3bc71615911c2438cbbf49c15), and corrupts it to a noisy version     T ( x )   {\displaystyle T(x)}  ![{\displaystyle T(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1171c29b4c2b5575f50a4ea9313f90448a2cbe05). The function     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) is selected randomly, with a probability distribution      μ μ   T     {\displaystyle \mu _{T}}  ![{\displaystyle \mu _{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a7c329840dcccf76c639e56c35ef3d56779d1fd5).

 

Given a task     (  μ μ   ref   , d )   {\displaystyle (\mu _{\text{ref}},d)}  ![{\displaystyle (\mu _{\text{ref}},d)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eb846915e028b0a1c631d189a395264d84ac2158), the problem of training a DAE is the optimization problem:     min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  ) =    E    x ∼ ∼   μ μ   X   , T ∼ ∼   μ μ   T     [ d ( x , (  D  θ θ    ∘ ∘   E  ϕ ϕ    ∘ ∘  T ) ( x ) ) ]   {\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X},T\sim \mu _{T}}[d(x,(D_{\theta }\circ E_{\phi }\circ T)(x))]}  ![{\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X},T\sim \mu _{T}}[d(x,(D_{\theta }\circ E_{\phi }\circ T)(x))]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2bdd1dd52947dc67ec42fba69511b4d28bdd7688)That is, the optimal DAE should take any noisy message and attempt to recover the original message without noise, thus the name "denoising"*.*

 

Usually, the noise process     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) is applied only during training and testing, not during downstream use.

 

The use of DAE depends on two assumptions:

 
- There exist representations to the messages that are relatively stable and robust to the type of noise we are likely to encounter;
- The said representations capture structures in the input distribution that are useful for our purposes.[[3]](./Autoencoder#cite_note-:4-3)

 

Example noise processes include:

 
- additive isotropic [Gaussian noise](./Additive_white_Gaussian_noise),
- masking noise (a fraction of the input is randomly chosen and set to 0)
- [salt-and-pepper noise](./Salt-and-pepper_noise) (a fraction of the input is randomly chosen and randomly set to its minimum or maximum value).[[3]](./Autoencoder#cite_note-:4-3)

 

### Contractive autoencoder (CAE)

 

A *contractive autoencoder* (CAE) adds the contractive regularization loss to the standard autoencoder loss:     min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  ) + λ λ   L  cont   ( θ θ  , ϕ ϕ  )   {\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{cont}}(\theta ,\phi )}  ![{\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{cont}}(\theta ,\phi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1d50899e5e474e145e04327418e6094e5661e28f)where     λ λ  > 0   {\displaystyle \lambda >0}  ![{\displaystyle \lambda >0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eea25afc0351140f919cf791c49c1964b8b081de) measures how much contractive-ness we want to enforce. The contractive regularization loss itself is defined as the expected square of [Frobenius norm](./Frobenius_norm) of the [Jacobian matrix](./Jacobian_matrix_and_determinant) of the encoder activations with respect to the input:     L  cont   ( θ θ  , ϕ ϕ  ) =   E   x ∼ ∼   μ μ   r e f     ‖ ‖   ∇ ∇   x    E  ϕ ϕ    ( x )  ‖ ‖   F   2     {\displaystyle L_{\text{cont}}(\theta ,\phi )=\mathbb {E} _{x\sim \mu _{ref}}\|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}  ![{\displaystyle L_{\text{cont}}(\theta ,\phi )=\mathbb {E} _{x\sim \mu _{ref}}\|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b9ecf73ce3d00cc59e0dc569ae167c8c1e439269)To understand what      L  cont     {\displaystyle L_{\text{cont}}}  ![{\displaystyle L_{\text{cont}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/919e6a2bb3a36c6ba639b6e9edd360d17d1b2027) measures, note the fact    ‖ ‖   E  ϕ ϕ    ( x + δ δ  x ) − −   E  ϕ ϕ    ( x )  ‖ ‖   2   ≤ ≤  ‖ ‖   ∇ ∇   x    E  ϕ ϕ    ( x )  ‖ ‖   F   ‖ ‖  δ δ  x  ‖ ‖   2     {\displaystyle \|E_{\phi }(x+\delta x)-E_{\phi }(x)\|_{2}\leq \|\nabla _{x}E_{\phi }(x)\|_{F}\|\delta x\|_{2}}  ![{\displaystyle \|E_{\phi }(x+\delta x)-E_{\phi }(x)\|_{2}\leq \|\nabla _{x}E_{\phi }(x)\|_{F}\|\delta x\|_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/20f744fa9cc9382d66d2f6a6bb05e3e31d9c9229)for any message     x ∈ ∈    X     {\displaystyle x\in {\mathcal {X}}}  ![{\displaystyle x\in {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b3cd596d560b9f3bc71615911c2438cbbf49c15), and small variation     δ δ  x   {\displaystyle \delta x}  ![{\displaystyle \delta x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d22318bef6d7358b79bd993321d65d7c1d3db9d4) in it. Thus, if     ‖ ‖   ∇ ∇   x    E  ϕ ϕ    ( x )  ‖ ‖   F   2     {\displaystyle \|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}  ![{\displaystyle \|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b832eef5d8709f1a326dd9eba1609951ebc7ec19) is small, it means that a small neighborhood of the message maps to a small neighborhood of its code. This is a desired property, as it means small variation in the message leads to small, perhaps even zero, variation in its code, like how two pictures may look the same even if they are not exactly the same.

 

The DAE can be understood as an infinitesimal limit of CAE: in the limit of small Gaussian input noise, DAEs make the reconstruction function resist small but finite-sized input perturbations, while CAEs make the extracted features resist infinitesimal input perturbations.

 

### Minimum description length autoencoder (MDL-AE)

 

A *minimum description length autoencoder* (MDL-AE) is an advanced variation of the traditional autoencoder, which leverages principles from information theory, specifically the [Minimum Description Length (MDL) principle](./Minimum_description_length). The MDL principle posits that the best model for a dataset is the one that provides the shortest combined encoding of the model and the data. In the context of [autoencoders](./Autoencoders), this principle is applied to ensure that the learned representation is not only compact but also interpretable and efficient for reconstruction.

 

The MDL-AE seeks to minimize the total description length of the data, which includes the size of the [latent representation](./Latent_representation?action=edit&redlink=1) (code length) and the error in reconstructing the original data. The objective can be expressed as
     L  code   +  L  error     {\displaystyle L_{\text{code}}+L_{\text{error}}}  ![{\displaystyle L_{\text{code}}+L_{\text{error}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/04970ccd9de439b43708851e6d701aa20ae42d50), where      L  code     {\displaystyle L_{\text{code}}}  ![{\displaystyle L_{\text{code}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/724dcb12347fd9f0bbe4582370dd161b2003d4a1) represents the length of the compressed latent representation and      L  error     {\displaystyle L_{\text{error}}}  ![{\displaystyle L_{\text{error}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54fbecfb3bd1d0f30fa1c943dd068fdc662f32b2) denotes the reconstruction error.[[18]](./Autoencoder#cite_note-:5-18)

 

### Concrete autoencoder (CAE)

 

The *concrete autoencoder* is designed for discrete feature selection.[[19]](./Autoencoder#cite_note-19) A concrete autoencoder forces the latent space to consist only of a user-specified number of features. The concrete autoencoder uses a continuous [relaxation](./Relaxation_(approximation)) of the [categorical distribution](./Categorical_distribution) to allow gradients to pass through the feature selector layer, which makes it possible to use standard [backpropagation](./Backpropagation) to learn an optimal subset of input features that minimize reconstruction loss.

 

## Advantages of depth

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/2/28/Autoencoder_structure.png/500px-Autoencoder_structure.png)](./File:Autoencoder_structure.png)Schematic structure of an autoencoder with 3 fully connected hidden layers. The code (z, or h for reference in the text) is the most internal layer. 

Autoencoders are often trained with a single-layer encoder and a single-layer decoder, but using many-layered (deep) encoders and decoders offers many advantages.[[2]](./Autoencoder#cite_note-:0-2)

 
- Depth can exponentially reduce the computational cost of representing some functions.
- Depth can exponentially decrease the amount of training data needed to learn some functions.
- Experimentally, deep autoencoders yield better compression compared to shallow or linear autoencoders.[[10]](./Autoencoder#cite_note-:7-10)
- Depth allows for advantages over traditional methods as one can show that after training single layer linear autoencoders have a latent space whose vectors span the same subspace as the eigenvectors found in [Principal component analysis](./Principal_component_analysis).[[20]](./Autoencoder#cite_note-20)

 

### Training

 

[Geoffrey Hinton](./Geoffrey_Hinton) developed the [deep belief network](./Deep_belief_network) technique for training many-layered deep autoencoders. His method involves treating each neighboring set of two layers as a [restricted Boltzmann machine](./Restricted_Boltzmann_machine) so that pretraining approximates a good solution, then using backpropagation to fine-tune the results.[[10]](./Autoencoder#cite_note-:7-10)

 

Researchers have debated whether joint training (i.e. training the whole architecture together with a single global reconstruction objective to optimize) would be better for deep auto-encoders.[[21]](./Autoencoder#cite_note-:9-21) A 2015 study showed that joint training learns better data models along with more representative features for classification as compared to the layerwise method.[[21]](./Autoencoder#cite_note-:9-21) However, their experiments showed that the success of joint training depends heavily on the regularization strategies adopted.[[21]](./Autoencoder#cite_note-:9-21)[[22]](./Autoencoder#cite_note-22)

 

## History

 

(Oja, 1982)[[23]](./Autoencoder#cite_note-23) noted that [PCA](./Principal_component_analysis) is equivalent to a neural network with one hidden layer with identity activation function. In the language of autoencoding, the input-to-hidden module is the encoder, and the hidden-to-output module is the decoder. Subsequently, in (Baldi and Hornik, 1989)[[24]](./Autoencoder#cite_note-auto-24) and (Kramer, 1991)[[9]](./Autoencoder#cite_note-:12-9) generalized PCA to autoencoders, a technique which they termed "nonlinear PCA".

 

Immediately after the resurgence of neural networks in the 1980s, it was suggested in 1986[[25]](./Autoencoder#cite_note-25) that a neural network be put in "auto-association mode". This was then implemented in (Harrison, 1987)[[26]](./Autoencoder#cite_note-26) and (Elman, Zipser, 1988)[[27]](./Autoencoder#cite_note-27) for speech and in (Cottrell, Munro, Zipser, 1987)[[28]](./Autoencoder#cite_note-28) for images.[[29]](./Autoencoder#cite_note-:14-29) In (Hinton, Salakhutdinov, 2006),[[30]](./Autoencoder#cite_note-:72-30) [deep belief networks](./Deep_belief_network) were developed. These train a pair [restricted Boltzmann machines](./Restricted_Boltzmann_machine) as encoder-decoder pairs, then train another pair on the latent representation of the first pair, and so on.[[31]](./Autoencoder#cite_note-scholar-31)

 

The first applications of AE date to early 1990s.[[2]](./Autoencoder#cite_note-:0-2)[[32]](./Autoencoder#cite_note-32)[[18]](./Autoencoder#cite_note-:5-18) Their most traditional application was [dimensionality reduction](./Dimensionality_reduction) or [feature learning](./Feature_learning), but the concept became widely used for learning [generative models](./Generative_model) of data.[[33]](./Autoencoder#cite_note-VAE-33)[[34]](./Autoencoder#cite_note-gan_faces-34) Some of the most powerful [AIs](./Artificial_intelligence) in the 2010s involved autoencoder modules as a component of larger AI systems, such as VAE in [Stable Diffusion](./Stable_Diffusion), discrete VAE in Transformer-based image generators like [DALL-E 1](./DALL-E), etc.

 

During the early days, when the terminology was uncertain, the autoencoder has also been called identity mapping,[[24]](./Autoencoder#cite_note-auto-24)[[9]](./Autoencoder#cite_note-:12-9) auto-associating,[[35]](./Autoencoder#cite_note-35) [self-supervised](./Self-supervised_learning) [backpropagation](./Backpropagation),[[9]](./Autoencoder#cite_note-:12-9) or Diabolo network.[[36]](./Autoencoder#cite_note-36)[[11]](./Autoencoder#cite_note-bengio-11)

 

## Applications

 

The two main applications of autoencoders are [dimensionality reduction](./Dimensionality_reduction) and [information retrieval](./Information_retrieval) (or [associative memory](./Content-addressable_memory)),[[2]](./Autoencoder#cite_note-:0-2) but modern variations have been applied to other tasks.

 

### Dimensionality reduction

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/0/0b/PCA_vs_Linear_Autoencoder.png/250px-PCA_vs_Linear_Autoencoder.png)](./File:PCA_vs_Linear_Autoencoder.png)Plot of the first two Principal Components (left) and a two-dimension hidden layer of a Linear Autoencoder (Right) applied to the [Fashion MNIST](./Fashion_MNIST) dataset.[[37]](./Autoencoder#cite_note-:10-37) The two models being both linear learn to span the same subspace. The projection of the data points is indeed identical, apart from rotation of the subspace. While PCA selects a specific orientation up to reflections in the general case, the cost function of a simple autoencoder is invariant to rotations of the latent space.

[Dimensionality reduction](./Dimensionality_reduction) was one of the first [deep learning](./Deep_learning) applications.[[2]](./Autoencoder#cite_note-:0-2)

 

For Hinton's 2006 study,[[10]](./Autoencoder#cite_note-:7-10) he pretrained a multi-layer autoencoder with a stack of [RBMs](./Restricted_Boltzmann_machine) and then used their weights to initialize a deep autoencoder with gradually smaller hidden layers until hitting a bottleneck of 30 neurons. The resulting 30 dimensions of the code yielded a smaller reconstruction error compared to the first 30 components of a principal component analysis (PCA), and learned a representation that was qualitatively easier to interpret, clearly separating data clusters.[[2]](./Autoencoder#cite_note-:0-2)[[10]](./Autoencoder#cite_note-:7-10)

 

Reducing dimensions can improve performance on tasks such as classification.[[2]](./Autoencoder#cite_note-:0-2) Indeed, the hallmark of dimensionality reduction is to place semantically related examples near each other.[[38]](./Autoencoder#cite_note-:3-38)

 

#### Principal component analysis

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Reconstruction_autoencoders_vs_PCA.png/250px-Reconstruction_autoencoders_vs_PCA.png)](./File:Reconstruction_autoencoders_vs_PCA.png)Reconstruction of 28x28pixel images by an Autoencoder with a code size of two (two-units hidden layer) and the reconstruction from the first two Principal Components of PCA. Images come from the [Fashion MNIST dataset](./Fashion_MNIST).[[37]](./Autoencoder#cite_note-:10-37) 

If linear activations are used, or only a single sigmoid hidden layer, then the optimal solution to an autoencoder is strongly related to [principal component analysis](./Principal_component_analysis) (PCA).[[29]](./Autoencoder#cite_note-:14-29)[[39]](./Autoencoder#cite_note-39) The weights of an autoencoder with a single hidden layer of size     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) (where     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) is less than the size of the input) span the same vector subspace as the one spanned by the first     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) principal components, and the output of the autoencoder is an orthogonal projection onto this subspace. The autoencoder weights are not equal to the principal components, and are generally not orthogonal, yet the principal components may be recovered from them using the [singular value decomposition](./Singular_value_decomposition).[[40]](./Autoencoder#cite_note-40)

 

However, the potential of autoencoders resides in their non-linearity, allowing the model to learn more powerful generalizations compared to PCA, and to reconstruct the input with significantly lower information loss.[[10]](./Autoencoder#cite_note-:7-10)

 

### Information retrieval

 

[Information retrieval](./Information_retrieval) benefits particularly from [dimensionality reduction](./Dimensionality_reduction) in that search can become more efficient in certain kinds of low dimensional spaces. Autoencoders were indeed applied to semantic hashing, proposed by [Salakhutdinov](./Russ_Salakhutdinov) and Hinton in 2007.[[38]](./Autoencoder#cite_note-:3-38) By training the algorithm to produce a low-dimensional binary code, all database entries could be stored in a [hash table](./Hash_table) mapping binary code vectors to entries. This table would then support information retrieval by returning all entries with the same binary code as the query, or slightly less similar entries by flipping some bits from the query encoding.

 

### Anomaly detection

 

Another application for autoencoders is [anomaly detection](./Anomaly_detection).[[17]](./Autoencoder#cite_note-:13-17)[[41]](./Autoencoder#cite_note-41)[[42]](./Autoencoder#cite_note-42)[[43]](./Autoencoder#cite_note-:8-43)[[44]](./Autoencoder#cite_note-44)[[45]](./Autoencoder#cite_note-45) By learning to replicate the most salient features in the training data under some of the constraints described previously, the model is encouraged to learn to precisely reproduce the most frequently observed characteristics. When facing anomalies, the model should worsen its reconstruction performance. In most cases, only data with normal instances are used to train the autoencoder; in others, the frequency of anomalies is small compared to the observation set so that its contribution to the learned representation could be ignored. After training, the autoencoder will accurately reconstruct "normal" data, while failing to do so with unfamiliar anomalous data.[[43]](./Autoencoder#cite_note-:8-43) Reconstruction error (the error between the original data and its low dimensional reconstruction) is used as an anomaly score to detect anomalies.[[43]](./Autoencoder#cite_note-:8-43)
Typically, this means that on a validation set the empirical distribution of reconstruction errors is recorded and then (e.g.) the empirical 95-percentile      x  p     {\displaystyle x_{p}}  ![{\displaystyle x_{p}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0bec554743fa797409a83ad8d00b4d35e110a50a) is taken as threshold     t :=  x  p     {\displaystyle t:=x_{p}}  ![{\displaystyle t:=x_{p}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6481406e3bed47aebe2848512f5aca6f96085e01) to flag anomalous data points:      loss  ( x ,  reconstruction  ( x ) ) > t  ⟹ ⟹    anomaly    {\displaystyle {\text{loss}}(x,{\text{reconstruction}}(x))>t\implies {\text{anomaly}}}  ![{\displaystyle {\text{loss}}(x,{\text{reconstruction}}(x))>t\implies {\text{anomaly}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a98f4a4d744a1865ae543008661712e48c733326). Since the threshold is an empirical [quantile](./Quantile) estimate, there is an inherent difficulty with "correctly" setting this threshold:
In many cases the distribution of the empirical quantile is asymptotically a normal distribution      empirical p-quantile  ∼ ∼    N    (  μ μ  = p ,  σ σ   2   =    p ( 1 − −  p )   n f (  x  p    )  2       )  ,   {\displaystyle {\text{empirical p-quantile}}\sim {\mathcal {N}}\left(\mu =p,\sigma ^{2}={\frac {p(1-p)}{nf(x_{p})^{2}}}\right),}  ![{\displaystyle {\text{empirical p-quantile}}\sim {\mathcal {N}}\left(\mu =p,\sigma ^{2}={\frac {p(1-p)}{nf(x_{p})^{2}}}\right),}](https://wikimedia.org/api/rest_v1/media/math/render/svg/83a3e1b4f51e83c131a75f457755a72b8140ff62) with     f (  x  p   )   {\displaystyle f(x_{p})}  ![{\displaystyle f(x_{p})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed477b468284792eb8d054af3ebaffe8cae222ac) the probability density at the quantile. This means that the variance grows if an extreme quantile is considered (because     f (  x  p   )   {\displaystyle f(x_{p})}  ![{\displaystyle f(x_{p})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed477b468284792eb8d054af3ebaffe8cae222ac) is small there). This means that there is a, potentially, a big uncertainty in what is the right choice for the threshold since it is *estimated* from a validation set.

 

Recent literature has however shown that certain autoencoding models can, counterintuitively, be very good at reconstructing anomalous examples and consequently not able to reliably perform anomaly detection.[[46]](./Autoencoder#cite_note-46)[[47]](./Autoencoder#cite_note-47) 
Intuitively, this can be understood by considering those one layer auto encoders which are related to PCA - also in this case there can be perfect rein reconstructions for points which are far away from the data region but which lie on a principal component axis.

 

It is best to analyze if the anomalies which are flagged by the auto encoder are true anomalies. In this sense all the metrics in [Evaluation of binary classifiers](./Evaluation_of_binary_classifiers) can be considered. The fundamental challenge which comes with the unsupervised (self-supervised) learning setting is, that labels for rare events do not exist (in which case the labels first have to be gathered and the data set will be imbalanced) or anomaly indicating labels are very rare, introducing larger [confidence intervals](./Confidence_interval) for these performance estimates.

 

### Image processing

 

The characteristics of autoencoders are useful in image processing.

 

One example can be found in lossy [image compression](./Image_compression), where autoencoders outperformed other approaches and proved competitive against [JPEG 2000](./JPEG_2000).[[48]](./Autoencoder#cite_note-48)[[49]](./Autoencoder#cite_note-49)

 

Another useful application of autoencoders in image preprocessing is [image denoising](./Image_denoising).[[50]](./Autoencoder#cite_note-50)[[51]](./Autoencoder#cite_note-51)[[52]](./Autoencoder#cite_note-52)

 

Autoencoders found use in more demanding contexts such as [medical imaging](./Medical_imaging) where they have been used for [image denoising](./Image_denoising)[[53]](./Autoencoder#cite_note-53) as well as [super-resolution](./Super-resolution).[[54]](./Autoencoder#cite_note-54)[[55]](./Autoencoder#cite_note-55) In image-assisted diagnosis, experiments have applied autoencoders for [breast cancer](./Breast_cancer) detection[[56]](./Autoencoder#cite_note-56) and for modelling the relation between the cognitive decline of [Alzheimer's disease](./Alzheimer's_disease) and the latent features of an autoencoder trained with [MRI](./MRI).[[57]](./Autoencoder#cite_note-57)

 

### Drug discovery

 

In 2019 molecules generated with variational autoencoders were validated experimentally in mice.[[58]](./Autoencoder#cite_note-58)[[59]](./Autoencoder#cite_note-59)

 

### Popularity prediction

 

Recently, a stacked autoencoder framework produced promising results in predicting popularity of social media posts,[[60]](./Autoencoder#cite_note-60) which is helpful for online advertising strategies.

 

### Machine translation

 

Autoencoders have been applied to [machine translation](./Machine_translation), which is usually referred to as [neural machine translation](./Neural_machine_translation) (NMT).[[61]](./Autoencoder#cite_note-61)[[62]](./Autoencoder#cite_note-62) Unlike traditional autoencoders, the output does not match the input - it is in another language. In NMT, texts are treated as sequences to be encoded into the learning procedure, while on the decoder side sequences in the target language(s) are generated. [Language](./Language)-specific autoencoders incorporate further [linguistic](./Linguistic) features into the learning procedure, such as Chinese decomposition features.[[63]](./Autoencoder#cite_note-63) Machine translation is rarely still done with autoencoders, due to the availability of more effective [transformer](./Transformer_(machine_learning_model)) networks.

 

### Communication Systems

 

Autoencoders in communication systems are important because they help in encoding data into a more resilient representation for channel impairments, which is crucial for transmitting information while minimizing errors. In Addition, AE-based systems can optimize end-to-end communication performance. This approach can solve the several limitations of designing communication systems such as the inherent difficulty in accurately modeling the complex behavior of real-world channels.[[64]](./Autoencoder#cite_note-64)

 

## See also

 
- [Representation learning](./Representation_learning)
- [Singular value decomposition](./Singular_value_decomposition)
- [Sparse dictionary learning](./Sparse_dictionary_learning)
- [Deep learning](./Deep_learning)

 

## Further reading

 
- Bank, Dor; Koenigstein, Noam; Giryes, Raja (2023). "Autoencoders". *Machine Learning for Data Science Handbook*. Cham: Springer International Publishing. [doi](./Doi_(identifier)):[10.1007/978-3-031-24628-9_16](https://doi.org/10.1007%2F978-3-031-24628-9_16). [ISBN](./ISBN_(identifier)) [978-3-031-24627-2](./Special:BookSources/978-3-031-24627-2).
- Goodfellow, Ian; Bengio, Yoshua; Courville, Aaron (2016). ["14. Autoencoders"](https://www.deeplearningbook.org/contents/autoencoders.html). *Deep learning*. Adaptive computation and machine learning. Cambridge, Mass: The MIT press. [ISBN](./ISBN_(identifier)) [978-0-262-03561-3](./Special:BookSources/978-0-262-03561-3).

 

## References

 
1. [↑](./Autoencoder#cite_ref-1) Bank, Dor; Koenigstein, Noam; Giryes, Raja (2023). ["Autoencoders"](https://link.springer.com/chapter/10.1007/978-3-031-24628-9_16). In Rokach, Lior; Maimon, Oded; Shmueli, Erez (eds.). *Machine learning for data science handbook*. pp. 353–374. [doi](./Doi_(identifier)):[10.1007/978-3-031-24628-9_16](https://doi.org/10.1007%2F978-3-031-24628-9_16). [ISBN](./ISBN_(identifier)) [978-3-031-24627-2](./Special:BookSources/978-3-031-24627-2).
2. [1](./Autoencoder#cite_ref-:0_2-0) [2](./Autoencoder#cite_ref-:0_2-1) [3](./Autoencoder#cite_ref-:0_2-2) [4](./Autoencoder#cite_ref-:0_2-3) [5](./Autoencoder#cite_ref-:0_2-4) [6](./Autoencoder#cite_ref-:0_2-5) [7](./Autoencoder#cite_ref-:0_2-6) [8](./Autoencoder#cite_ref-:0_2-7) [9](./Autoencoder#cite_ref-:0_2-8) Goodfellow, Ian; Bengio, Yoshua; Courville, Aaron (2016). [*Deep Learning*](http://www.deeplearningbook.org). MIT Press. [ISBN](./ISBN_(identifier)) [978-0262035613](./Special:BookSources/978-0262035613).
3. [1](./Autoencoder#cite_ref-:4_3-0) [2](./Autoencoder#cite_ref-:4_3-1) [3](./Autoencoder#cite_ref-:4_3-2) [4](./Autoencoder#cite_ref-:4_3-3) Vincent, Pascal; Larochelle, Hugo (2010). "Stacked Denoising Autoencoders: Learning Useful Representations in a Deep Network with a Local Denoising Criterion". *Journal of Machine Learning Research*. **11**: 3371–3408.
4. [↑](./Autoencoder#cite_ref-:11_4-0) Welling, Max; Kingma, Diederik P. (2019). "An Introduction to Variational Autoencoders". *Foundations and Trends in Machine Learning*. **12** (4): 307–392. [arXiv](./ArXiv_(identifier)):[1906.02691](https://arxiv.org/abs/1906.02691). [Bibcode](./Bibcode_(identifier)):[2019arXiv190602691K](https://ui.adsabs.harvard.edu/abs/2019arXiv190602691K). [doi](./Doi_(identifier)):[10.1561/2200000056](https://doi.org/10.1561%2F2200000056). [S2CID](./S2CID_(identifier)) [174802445](https://api.semanticscholar.org/CorpusID:174802445).
5. [↑](./Autoencoder#cite_ref-5) Hinton GE, Krizhevsky A, Wang SD. [Transforming auto-encoders.](http://www.cs.toronto.edu/~fritz/absps/transauto6.pdf) In International Conference on Artificial Neural Networks 2011 Jun 14 (pp. 44-51). Springer, Berlin, Heidelberg.
6. [1](./Autoencoder#cite_ref-:2_6-0) [2](./Autoencoder#cite_ref-:2_6-1) Géron, Aurélien (2019). *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow*. Canada: O’Reilly Media, Inc. pp. 739–740.
7. [↑](./Autoencoder#cite_ref-7) Liou, Cheng-Yuan; Huang, Jau-Chi; Yang, Wen-Chie (2008). ["Modeling word perception using the Elman network"](http://ntur.lib.ntu.edu.tw//handle/246246/155195). *Neurocomputing*. **71** (16–18): 3150. [doi](./Doi_(identifier)):[10.1016/j.neucom.2008.04.030](https://doi.org/10.1016%2Fj.neucom.2008.04.030).
8. [↑](./Autoencoder#cite_ref-8) Liou, Cheng-Yuan; Cheng, Wei-Chen; Liou, Jiun-Wei; Liou, Daw-Ran (2014). "Autoencoder for words". *Neurocomputing*. **139**: 84–96. [doi](./Doi_(identifier)):[10.1016/j.neucom.2013.09.055](https://doi.org/10.1016%2Fj.neucom.2013.09.055).
9. [1](./Autoencoder#cite_ref-:12_9-0) [2](./Autoencoder#cite_ref-:12_9-1) [3](./Autoencoder#cite_ref-:12_9-2) [4](./Autoencoder#cite_ref-:12_9-3) Kramer, Mark A. (1991). ["Nonlinear principal component analysis using autoassociative neural networks"](https://www.researchgate.net/profile/Abir_Alobaid/post/To_learn_a_probability_density_function_by_using_neural_network_can_we_first_estimate_density_using_nonparametric_methods_then_train_the_network/attachment/59d6450279197b80779a031e/AS:451263696510979@1484601057779/download/NL+PCA+by+using+ANN.pdf) (PDF). *AIChE Journal*. **37** (2): 233–243. [Bibcode](./Bibcode_(identifier)):[1991AIChE..37..233K](https://ui.adsabs.harvard.edu/abs/1991AIChE..37..233K). [doi](./Doi_(identifier)):[10.1002/aic.690370209](https://doi.org/10.1002%2Faic.690370209).
10. [1](./Autoencoder#cite_ref-:7_10-0) [2](./Autoencoder#cite_ref-:7_10-1) [3](./Autoencoder#cite_ref-:7_10-2) [4](./Autoencoder#cite_ref-:7_10-3) [5](./Autoencoder#cite_ref-:7_10-4) [6](./Autoencoder#cite_ref-:7_10-5) Hinton, G. E.; Salakhutdinov, R.R. (2006-07-28). "Reducing the Dimensionality of Data with Neural Networks". *Science*. **313** (5786): 504–507. [Bibcode](./Bibcode_(identifier)):[2006Sci...313..504H](https://ui.adsabs.harvard.edu/abs/2006Sci...313..504H). [doi](./Doi_(identifier)):[10.1126/science.1127647](https://doi.org/10.1126%2Fscience.1127647). [PMID](./PMID_(identifier)) [16873662](https://pubmed.ncbi.nlm.nih.gov/16873662). [S2CID](./S2CID_(identifier)) [1658773](https://api.semanticscholar.org/CorpusID:1658773).
11. [1](./Autoencoder#cite_ref-bengio_11-0) [2](./Autoencoder#cite_ref-bengio_11-1) Bengio, Y. (2009). ["Learning Deep Architectures for AI"](http://www.iro.umontreal.ca/~lisa/pointeurs/TR1312.pdf) (PDF). *Foundations and Trends in Machine Learning*. **2** (8): 1795–7. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.701.9550](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.701.9550). [doi](./Doi_(identifier)):[10.1561/2200000006](https://doi.org/10.1561%2F2200000006). [PMID](./PMID_(identifier)) [23946944](https://pubmed.ncbi.nlm.nih.gov/23946944). [S2CID](./S2CID_(identifier)) [207178999](https://api.semanticscholar.org/CorpusID:207178999).
12. [↑](./Autoencoder#cite_ref-domingos_12-0) [Domingos, Pedro](./Pedro_Domingos) (2015). "4". [*The Master Algorithm: How the Quest for the Ultimate Learning Machine Will Remake Our World*](./The_Master_Algorithm). Basic Books. "Deeper into the Brain" subsection. [ISBN](./ISBN_(identifier)) [978-046506192-1](./Special:BookSources/978-046506192-1).
13. [1](./Autoencoder#cite_ref-:1_13-0) [2](./Autoencoder#cite_ref-:1_13-1) [3](./Autoencoder#cite_ref-:1_13-2) [4](./Autoencoder#cite_ref-:1_13-3) Makhzani, Alireza; Frey, Brendan (2013). "K-Sparse Autoencoders". [arXiv](./ArXiv_(identifier)):[1312.5663](https://arxiv.org/abs/1312.5663) [[cs.LG](https://arxiv.org/archive/cs.LG)].
14. [1](./Autoencoder#cite_ref-:6_14-0) [2](./Autoencoder#cite_ref-:6_14-1) Ng, A. (2011). [Sparse autoencoder](https://web.stanford.edu/class/cs294a/sparseAutoencoder_2011new.pdf). *CS294A Lecture notes*, *72*(2011), 1-19.
15. [↑](./Autoencoder#cite_ref-15) Nair, Vinod; Hinton, Geoffrey E. (2009). ["3D Object Recognition with Deep Belief Nets"](http://dl.acm.org/citation.cfm?id=2984093.2984244). *Proceedings of the 22nd International Conference on Neural Information Processing Systems*. NIPS'09. USA: Curran Associates Inc.: 1339–1347. [ISBN](./ISBN_(identifier)) [9781615679119](./Special:BookSources/9781615679119).
16. [↑](./Autoencoder#cite_ref-16) Zeng, Nianyin; Zhang, Hong; Song, Baoye; Liu, Weibo; Li, Yurong; Dobaie, Abdullah M. (2018-01-17). "Facial expression recognition via learning deep sparse autoencoders". *Neurocomputing*. **273**: 643–649. [doi](./Doi_(identifier)):[10.1016/j.neucom.2017.08.043](https://doi.org/10.1016%2Fj.neucom.2017.08.043). [ISSN](./ISSN_(identifier)) [0925-2312](https://search.worldcat.org/issn/0925-2312).
17. [1](./Autoencoder#cite_ref-:13_17-0) [2](./Autoencoder#cite_ref-:13_17-1) Kramer, M. A. (1992-04-01). ["Autoassociative neural networks"](https://dx.doi.org/10.1016/0098-1354%2892%2980051-A). *Computers & Chemical Engineering*. Neutral network applications in chemical engineering. **16** (4): 313–328. [doi](./Doi_(identifier)):[10.1016/0098-1354(92)80051-A](https://doi.org/10.1016%2F0098-1354%2892%2980051-A). [ISSN](./ISSN_(identifier)) [0098-1354](https://search.worldcat.org/issn/0098-1354).
18. [1](./Autoencoder#cite_ref-:5_18-0) [2](./Autoencoder#cite_ref-:5_18-1) Hinton, Geoffrey E; Zemel, Richard (1993). ["Autoencoders, Minimum Description Length and Helmholtz Free Energy"](https://proceedings.neurips.cc/paper/1993/hash/9e3cfc48eccf81a0d57663e129aef3cb-Abstract.html). *Advances in Neural Information Processing Systems*. **6**. Morgan-Kaufmann.
19. [↑](./Autoencoder#cite_ref-19) Abid, Abubakar; Balin, Muhammad Fatih; Zou, James (2019-01-27). "Concrete Autoencoders for Differentiable Feature Selection and Reconstruction". [arXiv](./ArXiv_(identifier)):[1901.09346](https://arxiv.org/abs/1901.09346) [[cs.LG](https://arxiv.org/archive/cs.LG)].
20. [↑](./Autoencoder#cite_ref-20) Plaut, Elad (2018-12-28), *From Principal Subspaces to Principal Components with Linear Autoencoders*, [arXiv](./ArXiv_(identifier)):[1804.10253](https://arxiv.org/abs/1804.10253)
21. [1](./Autoencoder#cite_ref-:9_21-0) [2](./Autoencoder#cite_ref-:9_21-1) [3](./Autoencoder#cite_ref-:9_21-2) Zhou, Yingbo; Arpit, Devansh; Nwogu, Ifeoma; Govindaraju, Venu (2014). "Is Joint Training Better for Deep Auto-Encoders?". [arXiv](./ArXiv_(identifier)):[1405.1380](https://arxiv.org/abs/1405.1380) [[stat.ML](https://arxiv.org/archive/stat.ML)].
22. [↑](./Autoencoder#cite_ref-22) R. Salakhutdinov and G. E. Hinton, “Deep Boltzmann machines,” in AISTATS, 2009, pp. 448–455.
23. [↑](./Autoencoder#cite_ref-23) Oja, Erkki (1982-11-01). ["Simplified neuron model as a principal component analyzer"](https://link.springer.com/article/10.1007/BF00275687). *Journal of Mathematical Biology*. **15** (3): 267–273. [doi](./Doi_(identifier)):[10.1007/BF00275687](https://doi.org/10.1007%2FBF00275687). [ISSN](./ISSN_(identifier)) [1432-1416](https://search.worldcat.org/issn/1432-1416). [PMID](./PMID_(identifier)) [7153672](https://pubmed.ncbi.nlm.nih.gov/7153672).
24. [1](./Autoencoder#cite_ref-auto_24-0) [2](./Autoencoder#cite_ref-auto_24-1) Baldi, Pierre; Hornik, Kurt (1989-01-01). ["Neural networks and principal component analysis: Learning from examples without local minima"](https://www.sciencedirect.com/science/article/abs/pii/0893608089900142). *Neural Networks*. **2** (1): 53–58. [doi](./Doi_(identifier)):[10.1016/0893-6080(89)90014-2](https://doi.org/10.1016%2F0893-6080%2889%2990014-2). [ISSN](./ISSN_(identifier)) [0893-6080](https://search.worldcat.org/issn/0893-6080).
25. [↑](./Autoencoder#cite_ref-25) Rumelhart, David E.; McClelland, James L.; AU (1986). "2. A General Framework for Parallel Distributed Processing". [*Parallel Distributed Processing: Explorations in the Microstructure of Cognition: Foundations*](https://direct.mit.edu/books/book/4424/Parallel-Distributed-ProcessingExplorations-in-the). The MIT Press. [doi](./Doi_(identifier)):[10.7551/mitpress/5236.001.0001](https://doi.org/10.7551%2Fmitpress%2F5236.001.0001). [ISBN](./ISBN_(identifier)) [978-0-262-29140-8](./Special:BookSources/978-0-262-29140-8).
26. [↑](./Autoencoder#cite_ref-26) Harrison TD (1987) A Connectionist framework for continuous speech recognition. Cambridge University Ph. D. dissertation
27. [↑](./Autoencoder#cite_ref-27) Elman, Jeffrey L.; Zipser, David (1988-04-01). ["Learning the hidden structure of speech"](https://pubs.aip.org/jasa/article/83/4/1615/826094/Learning-the-hidden-structure-of-speechLearning). *The Journal of the Acoustical Society of America*. **83** (4): 1615–1626. [Bibcode](./Bibcode_(identifier)):[1988ASAJ...83.1615E](https://ui.adsabs.harvard.edu/abs/1988ASAJ...83.1615E). [doi](./Doi_(identifier)):[10.1121/1.395916](https://doi.org/10.1121%2F1.395916). [ISSN](./ISSN_(identifier)) [0001-4966](https://search.worldcat.org/issn/0001-4966). [PMID](./PMID_(identifier)) [3372872](https://pubmed.ncbi.nlm.nih.gov/3372872).
28. [↑](./Autoencoder#cite_ref-28) Cottrell, Garrison W.; Munro, Paul; Zipser, David (1987). ["Learning Internal Representation From Gray-Scale Images: An Example of Extensional Programming"](https://escholarship.org/uc/item/2zs7w6z8). *Proceedings of the Annual Meeting of the Cognitive Science Society*. **9**.
29. [1](./Autoencoder#cite_ref-:14_29-0) [2](./Autoencoder#cite_ref-:14_29-1) Bourlard, H.; Kamp, Y. (1988). ["Auto-association by multilayer perceptrons and singular value decomposition"](http://infoscience.epfl.ch/record/82601). *Biological Cybernetics*. **59** (4–5): 291–294. [doi](./Doi_(identifier)):[10.1007/BF00332918](https://doi.org/10.1007%2FBF00332918). [PMID](./PMID_(identifier)) [3196773](https://pubmed.ncbi.nlm.nih.gov/3196773). [S2CID](./S2CID_(identifier)) [206775335](https://api.semanticscholar.org/CorpusID:206775335).
30. [↑](./Autoencoder#cite_ref-:72_30-0) Hinton, G. E.; Salakhutdinov, R.R. (2006-07-28). "Reducing the Dimensionality of Data with Neural Networks". *Science*. **313** (5786): 504–507. [Bibcode](./Bibcode_(identifier)):[2006Sci...313..504H](https://ui.adsabs.harvard.edu/abs/2006Sci...313..504H). [doi](./Doi_(identifier)):[10.1126/science.1127647](https://doi.org/10.1126%2Fscience.1127647). [PMID](./PMID_(identifier)) [16873662](https://pubmed.ncbi.nlm.nih.gov/16873662). [S2CID](./S2CID_(identifier)) [1658773](https://api.semanticscholar.org/CorpusID:1658773).
31. [↑](./Autoencoder#cite_ref-scholar_31-0) Hinton G (2009). ["Deep belief networks"](https://doi.org/10.4249%2Fscholarpedia.5947). *Scholarpedia*. **4** (5): 5947. [Bibcode](./Bibcode_(identifier)):[2009SchpJ...4.5947H](https://ui.adsabs.harvard.edu/abs/2009SchpJ...4.5947H). [doi](./Doi_(identifier)):[10.4249/scholarpedia.5947](https://doi.org/10.4249%2Fscholarpedia.5947).
32. [↑](./Autoencoder#cite_ref-32) Schmidhuber, Jürgen (January 2015). "Deep learning in neural networks: An overview". *Neural Networks*. **61**: 85–117. [arXiv](./ArXiv_(identifier)):[1404.7828](https://arxiv.org/abs/1404.7828). [doi](./Doi_(identifier)):[10.1016/j.neunet.2014.09.003](https://doi.org/10.1016%2Fj.neunet.2014.09.003). [PMID](./PMID_(identifier)) [25462637](https://pubmed.ncbi.nlm.nih.gov/25462637). [S2CID](./S2CID_(identifier)) [11715509](https://api.semanticscholar.org/CorpusID:11715509).
33. [↑](./Autoencoder#cite_ref-VAE_33-0) Diederik P Kingma; Welling, Max (2013). "Auto-Encoding Variational Bayes". [arXiv](./ArXiv_(identifier)):[1312.6114](https://arxiv.org/abs/1312.6114) [[stat.ML](https://arxiv.org/archive/stat.ML)].
34. [↑](./Autoencoder#cite_ref-gan_faces_34-0) Generating Faces with Torch, Boesen A., Larsen L. and Sonderby S.K., 2015 [torch.ch/blog/2015/11/13/gan.html](http://torch.ch/blog/2015/11/13/gan.html)
35. [↑](./Autoencoder#cite_ref-35) Ackley, D; Hinton, G; Sejnowski, T (March 1985). ["A learning algorithm for boltzmann machines"](http://doi.wiley.com/10.1016/S0364-0213(85)80012-4). *Cognitive Science*. **9** (1): 147–169. [doi](./Doi_(identifier)):[10.1016/S0364-0213(85)80012-4](https://doi.org/10.1016%2FS0364-0213%2885%2980012-4).
36. [↑](./Autoencoder#cite_ref-36) Schwenk, Holger; Bengio, Yoshua (1997). ["Training Methods for Adaptive Boosting of Neural Networks"](https://proceedings.neurips.cc/paper/1997/hash/9cb67ffb59554ab1dabb65bcb370ddd9-Abstract.html). *Advances in Neural Information Processing Systems*. **10**. MIT Press.
37. [1](./Autoencoder#cite_ref-:10_37-0) [2](./Autoencoder#cite_ref-:10_37-1) ["Fashion MNIST"](https://github.com/zalandoresearch/fashion-mnist). *[GitHub](./GitHub)*. 2019-07-12.
38. [1](./Autoencoder#cite_ref-:3_38-0) [2](./Autoencoder#cite_ref-:3_38-1) Salakhutdinov, Ruslan; Hinton, Geoffrey (2009-07-01). ["Semantic hashing"](https://doi.org/10.1016%2Fj.ijar.2008.11.006). *International Journal of Approximate Reasoning*. Special Section on Graphical Models and Information Retrieval. **50** (7): 969–978. [doi](./Doi_(identifier)):[10.1016/j.ijar.2008.11.006](https://doi.org/10.1016%2Fj.ijar.2008.11.006). [ISSN](./ISSN_(identifier)) [0888-613X](https://search.worldcat.org/issn/0888-613X).
39. [↑](./Autoencoder#cite_ref-39) Chicco, Davide; Sadowski, Peter; Baldi, Pierre (2014). "Deep autoencoder neural networks for gene ontology annotation predictions". [*Proceedings of the 5th ACM Conference on Bioinformatics, Computational Biology, and Health Informatics - BCB '14*](http://dl.acm.org/citation.cfm?id=2649442). p. 533. [doi](./Doi_(identifier)):[10.1145/2649387.2649442](https://doi.org/10.1145%2F2649387.2649442). [hdl](./Hdl_(identifier)):[11311/964622](https://hdl.handle.net/11311%2F964622). [ISBN](./ISBN_(identifier)) [9781450328944](./Special:BookSources/9781450328944). [S2CID](./S2CID_(identifier)) [207217210](https://api.semanticscholar.org/CorpusID:207217210).
40. [↑](./Autoencoder#cite_ref-40) Plaut, E (2018). "From Principal Subspaces to Principal Components with Linear Autoencoders". [arXiv](./ArXiv_(identifier)):[1804.10253](https://arxiv.org/abs/1804.10253) [[stat.ML](https://arxiv.org/archive/stat.ML)].
41. [↑](./Autoencoder#cite_ref-41) Morales-Forero, A.; Bassetto, S. (December 2019). "Case Study: A Semi-Supervised Methodology for Anomaly Detection and Diagnosis". *2019 IEEE International Conference on Industrial Engineering and Engineering Management (IEEM)*. Macao, Macao: IEEE. pp. 1031–1037. [doi](./Doi_(identifier)):[10.1109/IEEM44572.2019.8978509](https://doi.org/10.1109%2FIEEM44572.2019.8978509). [ISBN](./ISBN_(identifier)) [978-1-7281-3804-6](./Special:BookSources/978-1-7281-3804-6). [S2CID](./S2CID_(identifier)) [211027131](https://api.semanticscholar.org/CorpusID:211027131).
42. [↑](./Autoencoder#cite_ref-42) Sakurada, Mayu; Yairi, Takehisa (December 2014). ["Anomaly Detection Using Autoencoders with Nonlinear Dimensionality Reduction"](http://dl.acm.org/citation.cfm?doid=2689746.2689747). *Proceedings of the MLSDA 2014 2nd Workshop on Machine Learning for Sensory Data Analysis*. Gold Coast, Australia QLD, Australia: ACM Press. pp. 4–11. [doi](./Doi_(identifier)):[10.1145/2689746.2689747](https://doi.org/10.1145%2F2689746.2689747). [ISBN](./ISBN_(identifier)) [978-1-4503-3159-3](./Special:BookSources/978-1-4503-3159-3). [S2CID](./S2CID_(identifier)) [14613395](https://api.semanticscholar.org/CorpusID:14613395).
43. [1](./Autoencoder#cite_ref-:8_43-0) [2](./Autoencoder#cite_ref-:8_43-1) [3](./Autoencoder#cite_ref-:8_43-2) An, J., & Cho, S. (2015). [Variational Autoencoder based Anomaly Detection using Reconstruction Probability](http://dm.snu.ac.kr/static/docs/TR/SNUDM-TR-2015-03.pdf). *Special Lecture on IE*, *2*, 1-18.
44. [↑](./Autoencoder#cite_ref-44) Zhou, Chong; Paffenroth, Randy C. (2017-08-04). ["Anomaly Detection with Robust Deep Autoencoders"](https://dl.acm.org/doi/10.1145/3097983.3098052). *Proceedings of the 23rd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*. ACM. pp. 665–674. [doi](./Doi_(identifier)):[10.1145/3097983.3098052](https://doi.org/10.1145%2F3097983.3098052). [ISBN](./ISBN_(identifier)) [978-1-4503-4887-4](./Special:BookSources/978-1-4503-4887-4). [S2CID](./S2CID_(identifier)) [207557733](https://api.semanticscholar.org/CorpusID:207557733).
45. [↑](./Autoencoder#cite_ref-45) Ribeiro, Manassés; Lazzaretti, André Eugênio; Lopes, Heitor Silvério (2018). "A study of deep convolutional auto-encoders for anomaly detection in videos". *Pattern Recognition Letters*. **105**: 13–22. [Bibcode](./Bibcode_(identifier)):[2018PaReL.105...13R](https://ui.adsabs.harvard.edu/abs/2018PaReL.105...13R). [doi](./Doi_(identifier)):[10.1016/j.patrec.2017.07.016](https://doi.org/10.1016%2Fj.patrec.2017.07.016).
46. [↑](./Autoencoder#cite_ref-46) Nalisnick, Eric; Matsukawa, Akihiro; Teh, Yee Whye; Gorur, Dilan; Lakshminarayanan, Balaji (2019-02-24). "Do Deep Generative Models Know What They Don't Know?". [arXiv](./ArXiv_(identifier)):[1810.09136](https://arxiv.org/abs/1810.09136) [[stat.ML](https://arxiv.org/archive/stat.ML)].
47. [↑](./Autoencoder#cite_ref-47) Xiao, Zhisheng; Yan, Qing; Amit, Yali (2020). ["Likelihood Regret: An Out-of-Distribution Detection Score For Variational Auto-encoder"](https://proceedings.neurips.cc/paper/2020/hash/eddea82ad2755b24c4e168c5fc2ebd40-Abstract.html). *Advances in Neural Information Processing Systems*. **33**. [arXiv](./ArXiv_(identifier)):[2003.02977](https://arxiv.org/abs/2003.02977).
48. [↑](./Autoencoder#cite_ref-48) Theis, Lucas; Shi, Wenzhe; Cunningham, Andrew; Huszár, Ferenc (2017). "Lossy Image Compression with Compressive Autoencoders". [arXiv](./ArXiv_(identifier)):[1703.00395](https://arxiv.org/abs/1703.00395) [[stat.ML](https://arxiv.org/archive/stat.ML)].
49. [↑](./Autoencoder#cite_ref-49) Balle, J; Laparra, V; Simoncelli, EP (April 2017). "End-to-end optimized image compression". *International Conference on Learning Representations*. [arXiv](./ArXiv_(identifier)):[1611.01704](https://arxiv.org/abs/1611.01704).
50. [↑](./Autoencoder#cite_ref-50) Cho, K. (2013, February). Simple sparsification improves sparse denoising autoencoders in denoising highly corrupted images. In *International Conference on Machine Learning* (pp. 432-440).
51. [↑](./Autoencoder#cite_ref-51) Cho, Kyunghyun (2013). "Boltzmann Machines and Denoising Autoencoders for Image Denoising". [arXiv](./ArXiv_(identifier)):[1301.3468](https://arxiv.org/abs/1301.3468) [[stat.ML](https://arxiv.org/archive/stat.ML)].
52. [↑](./Autoencoder#cite_ref-52) Buades, A.; Coll, B.; Morel, J. M. (2005). ["A Review of Image Denoising Algorithms, with a New One"](https://hal.archives-ouvertes.fr/hal-00271141). *Multiscale Modeling & Simulation*. **4** (2): 490–530. [doi](./Doi_(identifier)):[10.1137/040616024](https://doi.org/10.1137%2F040616024). [S2CID](./S2CID_(identifier)) [218466166](https://api.semanticscholar.org/CorpusID:218466166).
53. [↑](./Autoencoder#cite_ref-53) Gondara, Lovedeep (December 2016). "Medical Image Denoising Using Convolutional Denoising Autoencoders". *2016 IEEE 16th International Conference on Data Mining Workshops (ICDMW)*. Barcelona, Spain: IEEE. pp. 241–246. [arXiv](./ArXiv_(identifier)):[1608.04667](https://arxiv.org/abs/1608.04667). [Bibcode](./Bibcode_(identifier)):[2016arXiv160804667G](https://ui.adsabs.harvard.edu/abs/2016arXiv160804667G). [doi](./Doi_(identifier)):[10.1109/ICDMW.2016.0041](https://doi.org/10.1109%2FICDMW.2016.0041). [ISBN](./ISBN_(identifier)) [9781509059102](./Special:BookSources/9781509059102). [S2CID](./S2CID_(identifier)) [14354973](https://api.semanticscholar.org/CorpusID:14354973).
54. [↑](./Autoencoder#cite_ref-54) Zeng, Kun; Yu, Jun; Wang, Ruxin; Li, Cuihua; Tao, Dacheng (January 2017). "Coupled Deep Autoencoder for Single Image Super-Resolution". *IEEE Transactions on Cybernetics*. **47** (1): 27–37. [Bibcode](./Bibcode_(identifier)):[2017ITCyb..47...27Z](https://ui.adsabs.harvard.edu/abs/2017ITCyb..47...27Z). [doi](./Doi_(identifier)):[10.1109/TCYB.2015.2501373](https://doi.org/10.1109%2FTCYB.2015.2501373). [ISSN](./ISSN_(identifier)) [2168-2267](https://search.worldcat.org/issn/2168-2267). [PMID](./PMID_(identifier)) [26625442](https://pubmed.ncbi.nlm.nih.gov/26625442). [S2CID](./S2CID_(identifier)) [20787612](https://api.semanticscholar.org/CorpusID:20787612).
55. [↑](./Autoencoder#cite_ref-55) Tzu-Hsi, Song; Sanchez, Victor; Hesham, EIDaly; Nasir M., Rajpoot (2017). "Hybrid deep autoencoder with Curvature Gaussian for detection of various types of cells in bone marrow trephine biopsy images". *2017 IEEE 14th International Symposium on Biomedical Imaging (ISBI 2017)*. pp. 1040–1043. [doi](./Doi_(identifier)):[10.1109/ISBI.2017.7950694](https://doi.org/10.1109%2FISBI.2017.7950694). [ISBN](./ISBN_(identifier)) [978-1-5090-1172-8](./Special:BookSources/978-1-5090-1172-8). [S2CID](./S2CID_(identifier)) [7433130](https://api.semanticscholar.org/CorpusID:7433130).
56. [↑](./Autoencoder#cite_ref-56) Xu, Jun; Xiang, Lei; Liu, Qingshan; Gilmore, Hannah; Wu, Jianzhong; Tang, Jinghai; Madabhushi, Anant (January 2016). ["Stacked Sparse Autoencoder (SSAE) for Nuclei Detection on Breast Cancer Histopathology Images"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4729702). *IEEE Transactions on Medical Imaging*. **35** (1): 119–130. [Bibcode](./Bibcode_(identifier)):[2016ITMI...35..119X](https://ui.adsabs.harvard.edu/abs/2016ITMI...35..119X). [doi](./Doi_(identifier)):[10.1109/TMI.2015.2458702](https://doi.org/10.1109%2FTMI.2015.2458702). [PMC](./PMC_(identifier)) [4729702](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4729702). [PMID](./PMID_(identifier)) [26208307](https://pubmed.ncbi.nlm.nih.gov/26208307).
57. [↑](./Autoencoder#cite_ref-57) Martinez-Murcia, Francisco J.; Ortiz, Andres; Gorriz, Juan M.; Ramirez, Javier; Castillo-Barnes, Diego (2020). ["Studying the Manifold Structure of Alzheimer's Disease: A Deep Learning Approach Using Convolutional Autoencoders"](https://doi.org/10.1109%2FJBHI.2019.2914970). *IEEE Journal of Biomedical and Health Informatics*. **24** (1): 17–26. [Bibcode](./Bibcode_(identifier)):[2020IJBHI..24...17M](https://ui.adsabs.harvard.edu/abs/2020IJBHI..24...17M). [doi](./Doi_(identifier)):[10.1109/JBHI.2019.2914970](https://doi.org/10.1109%2FJBHI.2019.2914970). [hdl](./Hdl_(identifier)):[10630/28806](https://hdl.handle.net/10630%2F28806). [PMID](./PMID_(identifier)) [31217131](https://pubmed.ncbi.nlm.nih.gov/31217131). [S2CID](./S2CID_(identifier)) [195187846](https://api.semanticscholar.org/CorpusID:195187846).
58. [↑](./Autoencoder#cite_ref-58) Zhavoronkov, Alex (2019). "Deep learning enables rapid identification of potent DDR1 kinase inhibitors". *Nature Biotechnology*. **37** (9): 1038–1040. [doi](./Doi_(identifier)):[10.1038/s41587-019-0224-x](https://doi.org/10.1038%2Fs41587-019-0224-x). [PMID](./PMID_(identifier)) [31477924](https://pubmed.ncbi.nlm.nih.gov/31477924). [S2CID](./S2CID_(identifier)) [201716327](https://api.semanticscholar.org/CorpusID:201716327).
59. [↑](./Autoencoder#cite_ref-59) Gregory, Barber. ["A Molecule Designed By AI Exhibits 'Druglike' Qualities"](https://www.wired.com/story/molecule-designed-ai-exhibits-druglike-qualities/). *Wired*.
60. [↑](./Autoencoder#cite_ref-60) De, Shaunak; Maity, Abhishek; Goel, Vritti; Shitole, Sanjay; Bhattacharya, Avik (2017). "Predicting the popularity of instagram posts for a lifestyle magazine using deep learning". *2017 2nd IEEE International Conference on Communication Systems, Computing and IT Applications (CSCITA)*. pp. 174–177. [doi](./Doi_(identifier)):[10.1109/CSCITA.2017.8066548](https://doi.org/10.1109%2FCSCITA.2017.8066548). [ISBN](./ISBN_(identifier)) [978-1-5090-4381-1](./Special:BookSources/978-1-5090-4381-1). [S2CID](./S2CID_(identifier)) [35350962](https://api.semanticscholar.org/CorpusID:35350962).
61. [↑](./Autoencoder#cite_ref-61) Cho, Kyunghyun; Bart van Merrienboer; Bahdanau, Dzmitry; Bengio, Yoshua (2014). "On the Properties of Neural Machine Translation: Encoder-Decoder Approaches". [arXiv](./ArXiv_(identifier)):[1409.1259](https://arxiv.org/abs/1409.1259) [[cs.CL](https://arxiv.org/archive/cs.CL)].
62. [↑](./Autoencoder#cite_ref-62) Sutskever, Ilya; Vinyals, Oriol; Le, Quoc V. (2014). "Sequence to Sequence Learning with Neural Networks". [arXiv](./ArXiv_(identifier)):[1409.3215](https://arxiv.org/abs/1409.3215) [[cs.CL](https://arxiv.org/archive/cs.CL)].
63. [↑](./Autoencoder#cite_ref-63) Han, Lifeng; Kuang, Shaohui (2018). "Incorporating Chinese Radicals into Neural Machine Translation: Deeper Than Character Level". [arXiv](./ArXiv_(identifier)):[1805.01565](https://arxiv.org/abs/1805.01565) [[cs.CL](https://arxiv.org/archive/cs.CL)].
64. [↑](./Autoencoder#cite_ref-64) Alnaseri, Omar; Alzubaidi, Laith; Himeur, Yassine; Timmermann, Jens (2024). "A Review on Deep Learning Autoencoder in the Design of Next-Generation Communication Systems". [arXiv](./ArXiv_(identifier)):[2412.13843](https://arxiv.org/abs/2412.13843) [[eess.SP](https://arxiv.org/archive/eess.SP)].

 
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

 
| vteNoise(physics and telecommunications) |
| --- |
| General | Acoustic quietingDistortionNoise cancellationNoise controlNoise measurementNoise powerNoise reductionNoise temperaturePhase distortion |
| Noise in... | AudioBuildingsElectronicsEnvironmentGovernment regulationHuman healthImagesRadioRoomsShipsSound maskingTransportationVideo |
| Class of noise | Additive white Gaussian noise(AWGN)Atmospheric noiseBackground noiseBrownian noiseBurst noiseCosmic noiseFlicker noiseGaussian noiseGrey noiseInfrasoundJitterJohnson–Nyquist noise(thermal noise)Pink noiseQuantization noiseShot noiseWhite noiseCoherent noiseValue noiseGradient noiseWorley noise |
| Engineeringterms | Channel noise levelCircuit noise levelEffective input noise temperatureEquivalent noise resistanceEquivalent pulse code modulation noiseImpulse noise (audio)Noise figureNoise floorNoise shapingNoise spectral densityNoise, vibration, and harshness(NVH)Phase noisePseudorandom noiseStatistical noise |
| Ratios | Carrier-to-noise ratio(C/N)Carrier-to-receiver noise density(C/kT)dBrnCEb/N0(energy per bit to noise density)Es/N0(energy per symbol to noise density)Modulation error ratio(MER)Signal, noise and distortion(SINAD)Signal-to-interference ratio(S/I)Signal-to-noise ratio(S/N,SNR)Signal-to-noise ratio (imaging)Signal-to-interference-plus-noise ratio(SINR)Signal-to-quantization-noise ratio(SQNR)Contrast-to-noise ratio(CNR) |
| Related topics | List of noise topicsAcousticsColors of noiseInterference (communication)Noise generatorSpectrum analyzerThermal radiation |
| Denoisemethods | GeneralLow-pass filterMedian filterTotal variation denoisingWavelet denoising2D (Image)Gaussian blurAnisotropic diffusionBilateral filterNon-local meansBlock-matching and 3D filtering(BM3D)Shrinkage FieldsDenoising autoencoder(DAE)Deep Image Prior | General | Low-pass filterMedian filterTotal variation denoisingWavelet denoising | 2D (Image) | Gaussian blurAnisotropic diffusionBilateral filterNon-local meansBlock-matching and 3D filtering(BM3D)Shrinkage FieldsDenoising autoencoder(DAE)Deep Image Prior |
| General | Low-pass filterMedian filterTotal variation denoisingWavelet denoising |
| 2D (Image) | Gaussian blurAnisotropic diffusionBilateral filterNon-local meansBlock-matching and 3D filtering(BM3D)Shrinkage FieldsDenoising autoencoder(DAE)Deep Image Prior |