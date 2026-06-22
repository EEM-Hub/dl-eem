---
source: https://en.wikipedia.org/wiki/Batch_normalization
fetched: 2026-06-21
---

Method of improving artificial neural network 

 

 
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

 

In [artificial neural networks](./Artificial_neural_network), **batch normalization** (also known as **batch norm**) is a [normalization](./Normalization_(machine_learning)) technique used to make training faster and more stable by adjusting the inputs to each layer—re-centering them around zero and re-scaling them to a standard size. It was introduced by Sergey Ioffe and Christian Szegedy in 2015.[[1]](./Batch_normalization#cite_note-:0-1)

 

Experts still debate why batch normalization works so well. It was initially thought to tackle *internal covariate shift*, a problem where parameter initialization and changes in the distribution of the inputs of each layer affect the learning rate of the network.[[1]](./Batch_normalization#cite_note-:0-1) However, newer research suggests it doesn’t fix this shift but instead smooths the [objective function](./Intelligent_agent#Objective_function)—a mathematical guide the network follows to improve—enhancing performance.[[2]](./Batch_normalization#cite_note-:13-2) In very deep networks, batch normalization can initially cause a severe [gradient explosion](./Vanishing_gradient_problem)—where updates to the network grow uncontrollably large—but this is managed with shortcuts called skip connections in residual networks.[[3]](./Batch_normalization#cite_note-:73-3) Another theory is that batch normalization adjusts data by handling its size and path separately, speeding up training.[[4]](./Batch_normalization#cite_note-:23-4)

 

## Internal covariate shift

 

Each layer in a neural network has inputs that follow a specific distribution, which shifts during training due to two main factors: the random starting values of the network’s settings ([parameter initialization](./Parameter_initialization)) and the natural variation in the input data. This shifting pattern affecting the inputs to the network’s inner layers is called **internal covariate shift**. While a strict definition isn’t fully agreed upon, experiments show that it involves changes in the means and variances of these inputs during training.

 

Batch normalization was first developed to address internal covariate shift.[[1]](./Batch_normalization#cite_note-:0-1) During training, as the parameters of preceding layers adjust, the distribution of inputs to the current layer changes accordingly, such that the current layer needs to constantly readjust to new distributions. This issue is particularly severe in deep networks, because small changes in shallower hidden layers will be amplified as they propagate within the network, resulting in significant shift in deeper hidden layers. Batch normalization was proposed to reduced these unwanted shifts to speed up training and produce more reliable models.

 

Beyond possibly tackling internal covariate shift, batch normalization offers several additional advantages. It allows the network to use a higher [learning rate](./Learning_rate)—a setting that controls how quickly the network learns—without causing problems like vanishing or exploding gradients, where updates become too small or too large. It also appears to have a regularizing effect, improving the network’s ability to generalize to new data, reducing the need for [dropout](./Dropout_(neural_networks)), a technique used to prevent [overfitting](./Overfitting) (when a model learns the training data too well and fails on new data). Additionally, networks using batch normalization are less sensitive to the choice of starting settings or learning rates, making them more robust and adaptable.

 

## Procedures

 

### Transformation

 

In a neural network, batch normalization is achieved through a normalization step that fixes the means and variances of each layer's inputs. Ideally, the normalization would be conducted over the entire training set, but to use this step jointly with [stochastic optimization](./Stochastic_optimization) methods, it is impractical to use the global information. Thus, normalization is restrained to each mini-batch in the training process.

 

Let us use *B* to denote a mini-batch of size *m* of the entire training set. The empirical [mean](./Mean) and [variance](./Variance) of *B* could thus be denoted as

 

     μ μ   B   =   1 m    ∑ ∑   i = 1   m    x  i     {\displaystyle \mu _{B}={\frac {1}{m}}\sum _{i=1}^{m}x_{i}}  ![{\displaystyle \mu _{B}={\frac {1}{m}}\sum _{i=1}^{m}x_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cd0d3984435337cf2f54a8a37a8b59a2c9be3962) and      σ σ   B   2   =   1 m    ∑ ∑   i = 1   m   (  x  i   − −   μ μ   B    )  2     {\displaystyle \sigma _{B}^{2}={\frac {1}{m}}\sum _{i=1}^{m}(x_{i}-\mu _{B})^{2}}  ![{\displaystyle \sigma _{B}^{2}={\frac {1}{m}}\sum _{i=1}^{m}(x_{i}-\mu _{B})^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ee0c29a63307bef096890d6afa3022f9a1ceb1b1).

 

For a layer of the network with *d-*dimensional input,     x = (  x  ( 1 )   , . . . ,  x  ( d )   )   {\displaystyle x=(x^{(1)},...,x^{(d)})}  ![{\displaystyle x=(x^{(1)},...,x^{(d)})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/78d919bcd4cf8569fc248bad8506dc37c932ad80), each dimension of its input is then normalized (i.e. re-centered and re-scaled) separately,

 

        x ^ ^      i   ( k )   =     x  i   ( k )   − −   μ μ   B   ( k )       (  σ σ   B   ( k )   )   2   + ϵ ϵ       {\displaystyle {\hat {x}}_{i}^{(k)}={\frac {x_{i}^{(k)}-\mu _{B}^{(k)}}{\sqrt {\left(\sigma _{B}^{(k)}\right)^{2}+\epsilon }}}}  ![{\displaystyle {\hat {x}}_{i}^{(k)}={\frac {x_{i}^{(k)}-\mu _{B}^{(k)}}{\sqrt {\left(\sigma _{B}^{(k)}\right)^{2}+\epsilon }}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5bcadd141b0b7eab920a11a6f3a773493d35d744), where     k ∈ ∈  [ 1 , d ]   {\displaystyle k\in [1,d]}  ![{\displaystyle k\in [1,d]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/198a4d2d8ce137b1f4242c3f5cce495d77d7b0fd) and      i ∈ ∈  [ 1 , m ]   {\displaystyle i\in [1,m]}  ![{\displaystyle i\in [1,m]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ab916af4b9efb98e62b719bad44c18601285097b);      μ μ   B   ( k )     {\displaystyle \mu _{B}^{(k)}}  ![{\displaystyle \mu _{B}^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bc97d7418b5f8c2b6396dd94f491ed9a21d8ecb0) and      σ σ   B   ( k )     {\displaystyle \sigma _{B}^{(k)}}  ![{\displaystyle \sigma _{B}^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/977743d2c31d299bbf32990e40a8410bb12b16dd) are the per-dimension mean and standard deviation, respectively.

 

    ϵ ϵ    {\displaystyle \epsilon }  ![{\displaystyle \epsilon }](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3837cad72483d97bcdde49c85d3b7b859fb3fd2) is added in the denominator for numerical stability and is an arbitrarily small positive constant. The resulting normalized activation         x ^ ^      ( k )     {\displaystyle {\hat {x}}^{(k)}}  ![{\displaystyle {\hat {x}}^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e006f6308fa590163ebd3e53744a83575ca56450) have zero mean and unit variance, if     ϵ ϵ    {\displaystyle \epsilon }  ![{\displaystyle \epsilon }](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3837cad72483d97bcdde49c85d3b7b859fb3fd2) is not taken into account. To restore the representation power of the network, a transformation step then follows as

 

     y  i   ( k )   =  γ γ   ( k )       x ^ ^      i   ( k )   +  β β   ( k )     {\displaystyle y_{i}^{(k)}=\gamma ^{(k)}{\hat {x}}_{i}^{(k)}+\beta ^{(k)}}  ![{\displaystyle y_{i}^{(k)}=\gamma ^{(k)}{\hat {x}}_{i}^{(k)}+\beta ^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e890712d3a79c32441a69dba2188cbb4efc41bec),

 

where the parameters      γ γ   ( k )     {\displaystyle \gamma ^{(k)}}  ![{\displaystyle \gamma ^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c4592b76ab91a30f10dec9195b6544c05caf8453) and      β β   ( k )     {\displaystyle \beta ^{(k)}}  ![{\displaystyle \beta ^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c335496d9ec4863fc99f5ac2c836d26e7526ccd7) are subsequently learned in the optimization process.

 

Formally, the operation that implements batch normalization is a transform     B  N   γ γ   ( k )   ,  β β   ( k )     :  x  1... m   ( k )   → →   y  1... m   ( k )     {\displaystyle BN_{\gamma ^{(k)},\beta ^{(k)}}:x_{1...m}^{(k)}\rightarrow y_{1...m}^{(k)}}  ![{\displaystyle BN_{\gamma ^{(k)},\beta ^{(k)}}:x_{1...m}^{(k)}\rightarrow y_{1...m}^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9484456b00b1986f422a5e7bba1bdac2df29b56) called the Batch Normalizing transform. The output of the BN transform      y  ( k )   = B  N   γ γ   ( k )   ,  β β   ( k )     (  x  ( k )   )   {\displaystyle y^{(k)}=BN_{\gamma ^{(k)},\beta ^{(k)}}(x^{(k)})}  ![{\displaystyle y^{(k)}=BN_{\gamma ^{(k)},\beta ^{(k)}}(x^{(k)})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aa553bd532d824a0963c3a0e79e7e2444f0dd87a) is then passed to other network layers, while the normalized output          x ^ ^      i   ( k )     {\displaystyle {\hat {x}}_{i}^{(k)}}  ![{\displaystyle {\hat {x}}_{i}^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8d90e66232261cb252f1eb084812a93691750eff) remains internal to the current layer.

 

### Backpropagation

 

The described BN transform is a [differentiable](./Differentiable_function) operation, and the gradient of the [loss](./Loss_function)     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac)  with respect to the different parameters can be computed directly with the [chain rule](./Chain_rule).

 

Specifically,        ∂ ∂  l   ∂ ∂   y  i   ( k )        {\displaystyle {\frac {\partial l}{\partial y_{i}^{(k)}}}}  ![{\displaystyle {\frac {\partial l}{\partial y_{i}^{(k)}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a3724b90285aa0b2efee4825194ff04d39a5fd29) depends on the choice of [activation function](./Activation_function), and the [gradient](./Gradient) against other parameters could be expressed as a function of        ∂ ∂  l   ∂ ∂   y  i   ( k )        {\displaystyle {\frac {\partial l}{\partial y_{i}^{(k)}}}}  ![{\displaystyle {\frac {\partial l}{\partial y_{i}^{(k)}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a3724b90285aa0b2efee4825194ff04d39a5fd29):

 

       ∂ ∂  l   ∂ ∂      x ^ ^      i   ( k )      =    ∂ ∂  l   ∂ ∂   y  i   ( k )       γ γ   ( k )     {\displaystyle {\frac {\partial l}{\partial {\hat {x}}_{i}^{(k)}}}={\frac {\partial l}{\partial y_{i}^{(k)}}}\gamma ^{(k)}}  ![{\displaystyle {\frac {\partial l}{\partial {\hat {x}}_{i}^{(k)}}}={\frac {\partial l}{\partial y_{i}^{(k)}}}\gamma ^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/32b1beb5cc60115e019d4d9538b9d566ac00dcb4),

 

       ∂ ∂  l   ∂ ∂   γ γ   ( k )      =  ∑ ∑   i = 1   m      ∂ ∂  l   ∂ ∂   y  i   ( k )          x ^ ^      i   ( k )     {\displaystyle {\frac {\partial l}{\partial \gamma ^{(k)}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}{\hat {x}}_{i}^{(k)}}  ![{\displaystyle {\frac {\partial l}{\partial \gamma ^{(k)}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}{\hat {x}}_{i}^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/58b561531b36aa285816ce40e650f5a434128f8b),        ∂ ∂  l   ∂ ∂   β β   ( k )      =  ∑ ∑   i = 1   m      ∂ ∂  l   ∂ ∂   y  i   ( k )        {\displaystyle {\frac {\partial l}{\partial \beta ^{(k)}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}}  ![{\displaystyle {\frac {\partial l}{\partial \beta ^{(k)}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/33a38ea1fbf5cb13f44c41fd90c1e056e400cc7e),
       ∂ ∂  l   ∂ ∂   σ σ   B   ( k  )  2        =  ∑ ∑   i = 1   m      ∂ ∂  l   ∂ ∂   y  i   ( k )      (  x  i   ( k )   − −   μ μ   B   ( k )   )  (  − −     γ γ   ( k )   2   (  σ σ   B   ( k  )  2     + ϵ ϵ   )  − −  3  /  2    )    {\displaystyle {\frac {\partial l}{\partial \sigma _{B}^{(k)^{2}}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}(x_{i}^{(k)}-\mu _{B}^{(k)})\left(-{\frac {\gamma ^{(k)}}{2}}(\sigma _{B}^{(k)^{2}}+\epsilon )^{-3/2}\right)}  ![{\displaystyle {\frac {\partial l}{\partial \sigma _{B}^{(k)^{2}}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}(x_{i}^{(k)}-\mu _{B}^{(k)})\left(-{\frac {\gamma ^{(k)}}{2}}(\sigma _{B}^{(k)^{2}}+\epsilon )^{-3/2}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d7c327087d5fd83d97e4aafb42fbafb069abac12),        ∂ ∂  l   ∂ ∂   μ μ   B   ( k )      =  ∑ ∑   i = 1   m      ∂ ∂  l   ∂ ∂   y  i   ( k )         − −   γ γ   ( k )      σ σ   B   ( k  )  2     + ϵ ϵ     +    ∂ ∂  l   ∂ ∂   σ σ   B   ( k  )  2          1 m    ∑ ∑   i = 1   m   ( − −  2 ) ⋅ ⋅  (  x  i   ( k )   − −   μ μ   B   ( k )   )   {\displaystyle {\frac {\partial l}{\partial \mu _{B}^{(k)}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}{\frac {-\gamma ^{(k)}}{\sqrt {\sigma _{B}^{(k)^{2}}+\epsilon }}}+{\frac {\partial l}{\partial \sigma _{B}^{(k)^{2}}}}{\frac {1}{m}}\sum _{i=1}^{m}(-2)\cdot (x_{i}^{(k)}-\mu _{B}^{(k)})}  ![{\displaystyle {\frac {\partial l}{\partial \mu _{B}^{(k)}}}=\sum _{i=1}^{m}{\frac {\partial l}{\partial y_{i}^{(k)}}}{\frac {-\gamma ^{(k)}}{\sqrt {\sigma _{B}^{(k)^{2}}+\epsilon }}}+{\frac {\partial l}{\partial \sigma _{B}^{(k)^{2}}}}{\frac {1}{m}}\sum _{i=1}^{m}(-2)\cdot (x_{i}^{(k)}-\mu _{B}^{(k)})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b6a39565a8ef5c686e1525bfd66f02c4f48d7b23),

 

and        ∂ ∂  l   ∂ ∂   x  i   ( k )      =    ∂ ∂  l   ∂ ∂      x ^ ^      i   ( k )        1   σ σ   B   ( k  )  2     + ϵ ϵ     +    ∂ ∂  l   ∂ ∂   σ σ   B   ( k  )  2           2 (  x  i   ( k )   − −   μ μ   B   ( k )   )  m   +    ∂ ∂  l   ∂ ∂   μ μ   B   ( k )        1 m     {\displaystyle {\frac {\partial l}{\partial x_{i}^{(k)}}}={\frac {\partial l}{\partial {\hat {x}}_{i}^{(k)}}}{\frac {1}{\sqrt {\sigma _{B}^{(k)^{2}}+\epsilon }}}+{\frac {\partial l}{\partial \sigma _{B}^{(k)^{2}}}}{\frac {2(x_{i}^{(k)}-\mu _{B}^{(k)})}{m}}+{\frac {\partial l}{\partial \mu _{B}^{(k)}}}{\frac {1}{m}}}  ![{\displaystyle {\frac {\partial l}{\partial x_{i}^{(k)}}}={\frac {\partial l}{\partial {\hat {x}}_{i}^{(k)}}}{\frac {1}{\sqrt {\sigma _{B}^{(k)^{2}}+\epsilon }}}+{\frac {\partial l}{\partial \sigma _{B}^{(k)^{2}}}}{\frac {2(x_{i}^{(k)}-\mu _{B}^{(k)})}{m}}+{\frac {\partial l}{\partial \mu _{B}^{(k)}}}{\frac {1}{m}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d95ac93be5adf1d3ba002490414507748ad61fd5).

 

### Inference

 

During the training stage, the normalization steps depend on the mini-batches to ensure efficient and reliable training. However, in the inference stage, this dependence is not useful any more. Instead, the normalization step in this stage is computed with the population statistics such that the output could depend on the input in a deterministic manner. The population mean,     E [  x  ( k )   ]   {\displaystyle E[x^{(k)}]}  ![{\displaystyle E[x^{(k)}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9de884a23a219434520a8f5d2fa6029aa08d9229), and variance,     Var ⁡ ⁡  [  x  ( k )   ]   {\displaystyle \operatorname {Var} [x^{(k)}]}  ![{\displaystyle \operatorname {Var} [x^{(k)}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9626fe6237e75a52277fdfc8f0bde740b22106b2), are computed as:

 

    E [  x  ( k )   ] =  E  B   [  μ μ   B   ( k )   ]   {\displaystyle E[x^{(k)}]=E_{B}[\mu _{B}^{(k)}]}  ![{\displaystyle E[x^{(k)}]=E_{B}[\mu _{B}^{(k)}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/924410b15e63683d9d19aeccadb2d57ca423f151), and     Var ⁡ ⁡  [  x  ( k )   ] =   m  m − −  1     E  B   [   (  σ σ   B   ( k )   )   2   ]   {\displaystyle \operatorname {Var} [x^{(k)}]={\frac {m}{m-1}}E_{B}[\left(\sigma _{B}^{(k)}\right)^{2}]}  ![{\displaystyle \operatorname {Var} [x^{(k)}]={\frac {m}{m-1}}E_{B}[\left(\sigma _{B}^{(k)}\right)^{2}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1717aca2b768b32fe46c3c8f9c66daa25f953dff).

 

The population statistics thus is a complete representation of the mini-batches.

 

The BN transform in the inference step thus becomes

 

     y  ( k )   = B  N   γ γ   ( k )   ,  β β   ( k )     inf   (  x  ( k )   ) =  γ γ   ( k )       x  ( k )   − −  E [  x  ( k )   ]   Var ⁡ ⁡  [  x  ( k )   ] + ϵ ϵ     +  β β   ( k )     {\displaystyle y^{(k)}=BN_{\gamma ^{(k)},\beta ^{(k)}}^{\text{inf}}(x^{(k)})=\gamma ^{(k)}{\frac {x^{(k)}-E[x^{(k)}]}{\sqrt {\operatorname {Var} [x^{(k)}]+\epsilon }}}+\beta ^{(k)}}  ![{\displaystyle y^{(k)}=BN_{\gamma ^{(k)},\beta ^{(k)}}^{\text{inf}}(x^{(k)})=\gamma ^{(k)}{\frac {x^{(k)}-E[x^{(k)}]}{\sqrt {\operatorname {Var} [x^{(k)}]+\epsilon }}}+\beta ^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/032e23f561aa029ae0936e1b55f38a33f4488dcd),

 

where      y  ( k )     {\displaystyle y^{(k)}}  ![{\displaystyle y^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6187d5d10a29c1047e991615c8aaa040219f4741) is passed on to next layers instead of      x  ( k )     {\displaystyle x^{(k)}}  ![{\displaystyle x^{(k)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4c4ad77f04c0f250f01c3b6b5195ac5769d9dacf). Since the parameters are fixed in this transformation, the batch normalization procedure is essentially applying a [linear transform](./Linear_map) to the activation function.

 

## Theory

 

Although batch normalization has become popular due to its strong empirical performance, the working mechanism of the method is not yet well-understood. The explanation made in the original paper[[1]](./Batch_normalization#cite_note-:0-1) was that batch norm works by reducing internal covariate shift, but this has been challenged by more recent work. One experiment[[5]](./Batch_normalization#cite_note-:1-5) trained a [VGG-16](./VGGNet) network[[6]](./Batch_normalization#cite_note-VGG-6) under 3 different training regimes: standard (no batch norm), batch norm, and batch norm with noise added to each layer during training. In the third model, the noise has non-zero mean and non-unit variance, i.e. it explicitly introduces covariate shift. Despite this, it showed similar accuracy to the second model, and both performed better than the first, suggesting that covariate shift is not the reason that batch norm improves performance.

 

Using batch normalization causes the items in a batch to no longer be [iid](./Independent_and_identically_distributed_random_variables), which can lead to difficulties in training due to lower quality gradient estimation.[[7]](./Batch_normalization#cite_note-7)

 

### Smoothness

 

One alternative explanation[[5]](./Batch_normalization#cite_note-:1-5) is that the improvement with batch normalization is instead due to producing a smoother parameter space and smoother gradients, as formalized by a smaller [Lipschitz constant](./Lipschitz_continuity). 

 

Consider two identical networks, one contains batch normalization layers and the other does not, the behaviors of these two networks are then compared. Denote the loss functions as        L ^ ^       {\displaystyle {\hat {L}}}  ![{\displaystyle {\hat {L}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c5914e99ad679b0a2d962ea00e6167a20ff0d4ce) and     L   {\displaystyle L}  ![{\displaystyle L}](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8), respectively. Let the input to both networks be     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), and the output be     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d), for which     y = W x   {\displaystyle y=Wx}  ![{\displaystyle y=Wx}](https://wikimedia.org/api/rest_v1/media/math/render/svg/17f279b02105527ae737f6379828d2ca382b69e0), where     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7) is the layer weights. For the second network,     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) additionally goes through a batch normalization layer. Denote the normalized activation as        y ^ ^       {\displaystyle {\hat {y}}}  ![{\displaystyle {\hat {y}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3dc8de3d8ea01304329ef9518fad7a6d196c4c01), which has zero mean and unit variance. Let the transformed activation be     z = γ γ     y ^ ^     + β β    {\displaystyle z=\gamma {\hat {y}}+\beta }  ![{\displaystyle z=\gamma {\hat {y}}+\beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/2cf9bf09cfb9fdb93161e82b93e61d1e1b724b6c), and suppose     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a) and     β β    {\displaystyle \beta }  ![{\displaystyle \beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) are constants. Finally, denote the standard deviation over a mini-batch         y  j   ^ ^     ∈ ∈    R   m     {\displaystyle {\hat {y_{j}}}\in \mathbb {R} ^{m}}  ![{\displaystyle {\hat {y_{j}}}\in \mathbb {R} ^{m}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8527f733bd4c01bd2aeb0b1cb8eecd026e27649) as      σ σ   j     {\displaystyle \sigma _{j}}  ![{\displaystyle \sigma _{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a234b1f289568934f127c2dd68ba77b6ef3f3569).

 

First, it can be shown that the gradient magnitude of a batch normalized network,      |   |   ▽ ▽    y  i        L ^ ^      |   |    {\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||}  ![{\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47443c58f1c9ffb4509b6688b28030172e35d79e), is bounded, with the bound expressed as

 

     |   |   ▽ ▽    y  i        L ^ ^      |    |   2   ≤ ≤     γ γ   2    σ σ   j   2       (    |   |   ▽ ▽    y  i     L  |    |   2   − −    1 m   ⟨ ⟨  1 ,  ▽ ▽    y  i     L  ⟩ ⟩   2   − −    1 m   ⟨ ⟨   ▽ ▽    y  i     L ,     y ^ ^      j    ⟩ ⟩   2     )     {\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||^{2}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}{\Bigg (}||\triangledown _{y_{i}}L||^{2}-{\frac {1}{m}}\langle 1,\triangledown _{y_{i}}L\rangle ^{2}-{\frac {1}{m}}\langle \triangledown _{y_{i}}L,{\hat {y}}_{j}\rangle ^{2}{\bigg )}}  ![{\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||^{2}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}{\Bigg (}||\triangledown _{y_{i}}L||^{2}-{\frac {1}{m}}\langle 1,\triangledown _{y_{i}}L\rangle ^{2}-{\frac {1}{m}}\langle \triangledown _{y_{i}}L,{\hat {y}}_{j}\rangle ^{2}{\bigg )}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba3c5121143fe7afbff0230f491dba07a1c02c61).

 

Since the gradient magnitude represents the Lipschitzness of the loss, this relationship indicates that a batch normalized network could achieve greater Lipschitzness comparatively. Notice that the bound gets tighter when the gradient      ▽ ▽    y  i        L ^ ^       {\displaystyle \triangledown _{y_{i}}{\hat {L}}}  ![{\displaystyle \triangledown _{y_{i}}{\hat {L}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a386fa35b81502006040e9ea35d424dd997b71cf) correlates with the activation         y  i   ^ ^       {\displaystyle {\hat {y_{i}}}}  ![{\displaystyle {\hat {y_{i}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/84e9f46b496de85491c3227866df492db14c09fb), which is a common phenomena. The scaling of        γ γ   2    σ σ   j   2       {\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}  ![{\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eee6c2b2c2b869c353530cac7ed593c6fadd0ed1) is also significant, since the variance is often large.

 

Secondly, the quadratic form of the loss Hessian with respect to activation in the gradient direction can be bounded as

 

    (  ▽ ▽    y  j        L ^ ^      )  T      ∂ ∂     L ^ ^       ∂ ∂   y  j   ∂ ∂   y  j      (  ▽ ▽    y  j        L ^ ^     ) ≤ ≤     γ γ   2    σ σ   2       (      ∂ ∂     L ^ ^       ∂ ∂   y  j         )    T     (      ∂ ∂  L   ∂ ∂   y  j   ∂ ∂   y  j        )     (      ∂ ∂     L ^ ^       ∂ ∂   y  j        )   − −    γ γ   m  σ σ   2      ⟨ ⟨   ▽ ▽    y  j     L ,     y  j   ^ ^     ⟩ ⟩    |     |      ∂ ∂     L ^ ^       ∂ ∂   y  j        |      |    2     {\displaystyle (\triangledown _{y_{j}}{\hat {L}})^{T}{\frac {\partial {\hat {L}}}{\partial y_{j}\partial y_{j}}}(\triangledown _{y_{j}}{\hat {L}})\leq {\frac {\gamma ^{2}}{\sigma ^{2}}}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}^{T}{\bigg (}{\frac {\partial L}{\partial y_{j}\partial y_{j}}}{\bigg )}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}-{\frac {\gamma }{m\sigma ^{2}}}\langle \triangledown _{y_{j}}L,{\hat {y_{j}}}\rangle {\bigg |}{\bigg |}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg |}{\bigg |}^{2}}  ![{\displaystyle (\triangledown _{y_{j}}{\hat {L}})^{T}{\frac {\partial {\hat {L}}}{\partial y_{j}\partial y_{j}}}(\triangledown _{y_{j}}{\hat {L}})\leq {\frac {\gamma ^{2}}{\sigma ^{2}}}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}^{T}{\bigg (}{\frac {\partial L}{\partial y_{j}\partial y_{j}}}{\bigg )}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}-{\frac {\gamma }{m\sigma ^{2}}}\langle \triangledown _{y_{j}}L,{\hat {y_{j}}}\rangle {\bigg |}{\bigg |}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg |}{\bigg |}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/598ba229b7a7a25cdeaf500a84d1b8c1fdda5fc8).

 

The scaling of        γ γ   2    σ σ   j   2       {\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}  ![{\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eee6c2b2c2b869c353530cac7ed593c6fadd0ed1) indicates that the loss Hessian is resilient to the mini-batch variance, whereas the second term on the right hand side suggests that it becomes smoother when the [Hessian](./Hessian_matrix) and the inner product are non-negative. If the loss is locally [convex](./Convex_function), then the Hessian is [positive semi-definite](./Positive_semidefinite_matrix), while the inner product is positive if         g  j   ^ ^       {\displaystyle {\hat {g_{j}}}}  ![{\displaystyle {\hat {g_{j}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cbd3bc5d8e75dc374257ba8018dd9f23476ee33c) is in the direction towards the minimum of the loss. It could thus be concluded from this inequality that the gradient generally becomes more predictive with the batch normalization layer.

 

It then follows to translate the bounds related to the loss with respect to the normalized activation to a bound on the loss with respect to the network weights:

 

        g  j   ^ ^     ≤ ≤     γ γ   2    σ σ   j   2     (  g  j   2   − −  m  μ μ    g  j     2   − −   λ λ   2   ⟨ ⟨   ▽ ▽    y  j     L ,     y ^ ^      j    ⟩ ⟩   2   )   {\displaystyle {\hat {g_{j}}}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}(g_{j}^{2}-m\mu _{g_{j}}^{2}-\lambda ^{2}\langle \triangledown _{y_{j}}L,{\hat {y}}_{j}\rangle ^{2})}  ![{\displaystyle {\hat {g_{j}}}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}(g_{j}^{2}-m\mu _{g_{j}}^{2}-\lambda ^{2}\langle \triangledown _{y_{j}}L,{\hat {y}}_{j}\rangle ^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c94b8189deaf786bb78f83dcb51f2bc422cfffbc), where      g  j   = m a  x   |   |  X  |   |  ≤ ≤  λ λ     |   |   ▽ ▽   W   L  |    |   2     {\displaystyle g_{j}=max_{||X||\leq \lambda }||\triangledown _{W}L||^{2}}  ![{\displaystyle g_{j}=max_{||X||\leq \lambda }||\triangledown _{W}L||^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5f76d93a70a9de73a91da4c44769bc7a720c3bb0) and         g ^ ^      j   = m a  x   |   |  X  |   |  ≤ ≤  λ λ     |   |   ▽ ▽   W      L ^ ^      |    |   2     {\displaystyle {\hat {g}}_{j}=max_{||X||\leq \lambda }||\triangledown _{W}{\hat {L}}||^{2}}  ![{\displaystyle {\hat {g}}_{j}=max_{||X||\leq \lambda }||\triangledown _{W}{\hat {L}}||^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a1c5032bb8d3a7aa61a390c748e95ada0599d670).

 

In addition to the smoother landscape, it is further shown that batch normalization could result in a better initialization with the following inequality:

 

     |   |   W  0   − −      W ^ ^      ∗ ∗     |    |   2   ≤ ≤   |   |   W  0   − −   W  ∗ ∗     |    |   2   − −    1   |   |   W  ∗ ∗     |    |   2      (  |   |   W  ∗ ∗     |    |   2   − −  ⟨ ⟨   W  ∗ ∗    ,  W  0   ⟩ ⟩   )  2     {\displaystyle ||W_{0}-{\hat {W}}^{*}||^{2}\leq ||W_{0}-W^{*}||^{2}-{\frac {1}{||W^{*}||^{2}}}(||W^{*}||^{2}-\langle W^{*},W_{0}\rangle )^{2}}  ![{\displaystyle ||W_{0}-{\hat {W}}^{*}||^{2}\leq ||W_{0}-W^{*}||^{2}-{\frac {1}{||W^{*}||^{2}}}(||W^{*}||^{2}-\langle W^{*},W_{0}\rangle )^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9ac3bd274bf4ea26d42044bf5f0f1fa130174fa6), where      W  ∗ ∗      {\displaystyle W^{*}}  ![{\displaystyle W^{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5292cb3dbf333bb0b51f39fb9f724fa8d4dfcc63) and         W ^ ^      ∗ ∗      {\displaystyle {\hat {W}}^{*}}  ![{\displaystyle {\hat {W}}^{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a9f598335a95fd9cc1d7eb039fd9ca278165a96c) are the local optimal weights for the two networks, respectively.

 

Some scholars argue that the above analysis cannot fully capture the performance of batch normalization, because the proof only concerns the largest eigenvalue, or equivalently, one direction in the landscape at all points. It is suggested that the complete eigenspectrum needs to be taken into account to make a conclusive analysis.[[8]](./Batch_normalization#cite_note-:2-8)[[5]](./Batch_normalization#cite_note-:1-5)

 

### Measure

 

Since it is hypothesized that batch normalization layers could reduce internal covariate shift, an experiment[*[citation needed](./Wikipedia:Citation_needed)*] is set up to measure quantitatively how much covariate shift is reduced. First, the notion of internal covariate shift needs to be defined mathematically. Specifically, to quantify the adjustment that a layer's parameters make in response to updates in previous layers, the correlation between the gradients of the loss before and after all previous layers are updated is measured, since gradients could capture the shifts from the first-order training method. If the shift introduced by the changes in previous layers is small, then the correlation between the gradients would be close to 1.

 

The correlation between the gradients are computed for four models: a standard [VGG network](./VGGNet),[[6]](./Batch_normalization#cite_note-VGG-6) a VGG network with batch normalization layers, a 25-layer deep linear network (DLN) trained with full-batch gradient descent, and a DLN network with batch normalization layers. Interestingly, it is shown that the standard VGG and DLN models both have higher correlations of gradients compared with their counterparts, indicating that the additional batch normalization layers are not reducing internal covariate shift.

 

### Vanishing/exploding gradients

 

Even though batch norm was originally introduced to alleviate [gradient vanishing or explosion problems](./Vanishing_gradient_problem), a deep batch norm network in fact *suffers from gradient explosion* at initialization time, no matter what it uses for nonlinearity. Thus, the optimization landscape is very far from smooth for a randomly initialized, deep batch norm network.
More precisely, if the network has     L   {\displaystyle L}  ![{\displaystyle L}](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8) layers, then the gradient of the first layer weights has norm     > c  λ λ   L     {\displaystyle >c\lambda ^{L}}  ![{\displaystyle >c\lambda ^{L}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cab76f58a7a5dccf0f9ed0c5d78e1db2fb2f7435) for some     λ λ  > 1 , c > 0   {\displaystyle \lambda >1,c>0}  ![{\displaystyle \lambda >1,c>0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/afd304b28687ea62f39b2a8fc2fb7916aa8eb531) depending only on the nonlinearity.
For any fixed nonlinearity,     λ λ    {\displaystyle \lambda }  ![{\displaystyle \lambda }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b43d0ea3c9c025af1be9128e62a18fa74bedda2a) decreases as the batch size increases. For example, for ReLU,     λ λ    {\displaystyle \lambda }  ![{\displaystyle \lambda }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b43d0ea3c9c025af1be9128e62a18fa74bedda2a) decreases to     π π   /  ( π π  − −  1 ) ≈ ≈  1.467   {\displaystyle \pi /(\pi -1)\approx 1.467}  ![{\displaystyle \pi /(\pi -1)\approx 1.467}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e3922a4b656e6d4281f61c029cb1c8b0943cc72) as the batch size tends to infinity.
Practically, this means deep batch norm networks are untrainable.
This is only relieved by skip connections in the fashion of [residual networks](./Residual_neural_network).[[9]](./Batch_normalization#cite_note-:7-9)

 

This gradient explosion on the surface contradicts the *smoothness* property explained in the previous section, but in fact they are consistent. The previous section studies the effect of inserting a single batch norm in a network, while the gradient explosion depends on stacking batch norms typical of modern deep neural networks.

 

### Decoupling

 

Another possible reason for the success of batch normalization is that it [decouples](./Decoupling_(probability)) the length and direction of the weight vectors and thus facilitates better training.

 

By interpreting batch norm as a reparametrization of weight space, it can be shown that the length and the direction of the weights are separated and can thus be trained separately. For a particular neural network unit with input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) and weight vector     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6), denote its output as     f ( w ) =  E  x   [ ϕ ϕ  (  x  T   w ) ]   {\displaystyle f(w)=E_{x}[\phi (x^{T}w)]}  ![{\displaystyle f(w)=E_{x}[\phi (x^{T}w)]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/870188d380627f799e598e056ea71b4c23815741), where     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4) is the activation function, and denote     S = E [ x  x  T   ]   {\displaystyle S=E[xx^{T}]}  ![{\displaystyle S=E[xx^{T}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/71f3a47dfa9441a4050edac91329e66ac747684b). Assume that     E [ x ] = 0   {\displaystyle E[x]=0}  ![{\displaystyle E[x]=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f464a09bd74ae67c6e8094c223aa1edd093699c9), and that the [spectrum](./Spectrum_of_a_matrix) of the matrix     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) is bounded as     0 < μ μ  =  λ λ   m i n   ( S )   {\displaystyle 0<\mu =\lambda _{min}(S)}  ![{\displaystyle 0<\mu =\lambda _{min}(S)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c780462af127d32b872a60841bd24c25da8ea6d9),     L =  λ λ   m a x   ( S ) < ∞ ∞    {\displaystyle L=\lambda _{max}(S)<\infty }  ![{\displaystyle L=\lambda _{max}(S)<\infty }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3c7406de80618dc4081e9c8881339b56595e992), such that     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) is symmetric positive definite. Adding batch normalization to this unit thus results in

 

     f  B N   ( w , γ γ  , β β  ) =  E  x   [ ϕ ϕ  ( B N (  x  T   w ) ) ] =  E  x     [   ϕ ϕ    (   γ γ  (     x  T   w − −   E  x   [  x  T   w ]   v a  r  x   [  x  T   w  ]  1  /  2      ) + β β    )     ]     {\displaystyle f_{BN}(w,\gamma ,\beta )=E_{x}[\phi (BN(x^{T}w))]=E_{x}{\bigg [}\phi {\bigg (}\gamma ({\frac {x^{T}w-E_{x}[x^{T}w]}{var_{x}[x^{T}w]^{1/2}}})+\beta {\bigg )}{\bigg ]}}  ![{\displaystyle f_{BN}(w,\gamma ,\beta )=E_{x}[\phi (BN(x^{T}w))]=E_{x}{\bigg [}\phi {\bigg (}\gamma ({\frac {x^{T}w-E_{x}[x^{T}w]}{var_{x}[x^{T}w]^{1/2}}})+\beta {\bigg )}{\bigg ]}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ef3c8776e25fec4bb27c4e556fafeda7d35686a3), by definition.

 

The variance term can be simplified such that     v a  r  x   [  x  T   w ] =  w  T   S w   {\displaystyle var_{x}[x^{T}w]=w^{T}Sw}  ![{\displaystyle var_{x}[x^{T}w]=w^{T}Sw}](https://wikimedia.org/api/rest_v1/media/math/render/svg/64581f03bf8607566e4f8126ce8822e23ca4454d). Assume that     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) has zero mean and     β β    {\displaystyle \beta }  ![{\displaystyle \beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) can be omitted, then it follows that

 

     f  B N   ( w , γ γ  ) =  E  x     [   ϕ ϕ    (   γ γ      x  T   w   (  w  T   S w  )  1  /  2        )     ]     {\displaystyle f_{BN}(w,\gamma )=E_{x}{\bigg [}\phi {\bigg (}\gamma {\frac {x^{T}w}{(w^{T}Sw)^{1/2}}}{\bigg )}{\bigg ]}}  ![{\displaystyle f_{BN}(w,\gamma )=E_{x}{\bigg [}\phi {\bigg (}\gamma {\frac {x^{T}w}{(w^{T}Sw)^{1/2}}}{\bigg )}{\bigg ]}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8073fc1cb01c6722a53258ee44d8ad020f8b1e6f), where     (  w  T   S w  )   1 2      {\displaystyle (w^{T}Sw)^{\frac {1}{2}}}  ![{\displaystyle (w^{T}Sw)^{\frac {1}{2}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/83a8fad691375fdec2a94f2a066f155172c6045b) is the induced norm of     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2),      |   |  w  |    |   s     {\displaystyle ||w||_{s}}  ![{\displaystyle ||w||_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d0357dc403927cc26418f5ccbe598f35d7b65606).

 

Hence, it could be concluded that      f  B N   ( w , γ γ  ) =  E  x   [ ϕ ϕ  (  x  T      w ~ ~     ) ]   {\displaystyle f_{BN}(w,\gamma )=E_{x}[\phi (x^{T}{\tilde {w}})]}  ![{\displaystyle f_{BN}(w,\gamma )=E_{x}[\phi (x^{T}{\tilde {w}})]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0479b5ef1b32a46c9837a35b2e6746a8a8b36803), where        w ~ ~     = γ γ    w   |   |  w  |    |   s        {\displaystyle {\tilde {w}}=\gamma {\frac {w}{||w||_{s}}}}  ![{\displaystyle {\tilde {w}}=\gamma {\frac {w}{||w||_{s}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fb18955e26cd1b8f38355e59f34f94b4dff6b2e), and     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a) and     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) account for its length and direction separately. This property could then be used to prove the faster convergence of problems with batch normalization.

 

## Linear convergence

 

### Least-square problem

 

With the reparametrization interpretation, it could then be proved that applying batch normalization to the ordinary least squares problem achieves a linear convergence rate in gradient descent, which is faster than the regular gradient descent with only sub-linear convergence.

 

Denote the objective of minimizing an ordinary least squares problem as

 

     min     w ~ ~     ∈ ∈   R  d      f  O L S   (    w ~ ~     ) =  min     w ~ ~     ∈ ∈   R  d     (  E  x , y   [ ( y − −   x  T      w ~ ~      )  2   ] ) =  min     w ~ ~     ∈ ∈   R  d     ( 2  u  T      w ~ ~     +     w ~ ~      T   S    w ~ ~     )   {\displaystyle \min _{{\tilde {w}}\in R^{d}}f_{OLS}({\tilde {w}})=\min _{{\tilde {w}}\in R^{d}}(E_{x,y}[(y-x^{T}{\tilde {w}})^{2}])=\min _{{\tilde {w}}\in R^{d}}(2u^{T}{\tilde {w}}+{\tilde {w}}^{T}S{\tilde {w}})}  ![{\displaystyle \min _{{\tilde {w}}\in R^{d}}f_{OLS}({\tilde {w}})=\min _{{\tilde {w}}\in R^{d}}(E_{x,y}[(y-x^{T}{\tilde {w}})^{2}])=\min _{{\tilde {w}}\in R^{d}}(2u^{T}{\tilde {w}}+{\tilde {w}}^{T}S{\tilde {w}})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e501150c07350a39f023afeb945d47aa0479d605), where     u = E [ − −  y x ]   {\displaystyle u=E[-yx]}  ![{\displaystyle u=E[-yx]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/946686cd36bcf56c7210946d1a01c17c92c146e1) and     S = E [ x  x  T   ]   {\displaystyle S=E[xx^{T}]}  ![{\displaystyle S=E[xx^{T}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/71f3a47dfa9441a4050edac91329e66ac747684b).

 

Since        w ~ ~     = γ γ    w   |   |  w  |    |   s        {\displaystyle {\tilde {w}}=\gamma {\frac {w}{||w||_{s}}}}  ![{\displaystyle {\tilde {w}}=\gamma {\frac {w}{||w||_{s}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fb18955e26cd1b8f38355e59f34f94b4dff6b2e), the objective thus becomes

 

     min  w ∈ ∈   R  d   ∖ ∖  { 0 } , γ γ  ∈ ∈  R    f  O L S   ( w , γ γ  ) =  min  w ∈ ∈   R  d   ∖ ∖  { 0 } , γ γ  ∈ ∈  R     (   2 γ γ      u  T   w    |   |  w  |    |   S   +  γ γ   2        )     {\displaystyle \min _{w\in R^{d}\backslash \{0\},\gamma \in R}f_{OLS}(w,\gamma )=\min _{w\in R^{d}\backslash \{0\},\gamma \in R}{\bigg (}2\gamma {\frac {u^{T}w}{||w||_{S}+\gamma ^{2}}}{\bigg )}}  ![{\displaystyle \min _{w\in R^{d}\backslash \{0\},\gamma \in R}f_{OLS}(w,\gamma )=\min _{w\in R^{d}\backslash \{0\},\gamma \in R}{\bigg (}2\gamma {\frac {u^{T}w}{||w||_{S}+\gamma ^{2}}}{\bigg )}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e498170da142779b13c9d07efeb1e65d7697b1d5), where 0 is excluded to avoid 0 in the denominator.

 

Since the objective is convex with respect to     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a), its optimal value could be calculated by setting the partial derivative of the objective against     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a) to 0. The objective could be further simplified to be

 

     min  w ∈ ∈   R  d   ∖ ∖  { 0 }   ρ ρ  ( w ) =  min  w ∈ ∈   R  d   ∖ ∖  { 0 }     (   − −      w  T   u  u  T   w    w  T   S w      )     {\displaystyle \min _{w\in R^{d}\backslash \{0\}}\rho (w)=\min _{w\in R^{d}\backslash \{0\}}{\bigg (}-{\frac {w^{T}uu^{T}w}{w^{T}Sw}}{\bigg )}}  ![{\displaystyle \min _{w\in R^{d}\backslash \{0\}}\rho (w)=\min _{w\in R^{d}\backslash \{0\}}{\bigg (}-{\frac {w^{T}uu^{T}w}{w^{T}Sw}}{\bigg )}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba43ce5a4b71d4bf7d68937a82e5877122ec4c12).

 

Note that this objective is a form of the generalized [Rayleigh quotient](./Rayleigh_quotient)

 

       ρ ρ  ~ ~     ( w ) =     w  T   B w    w  T   A w      {\displaystyle {\tilde {\rho }}(w)={\frac {w^{T}Bw}{w^{T}Aw}}}  ![{\displaystyle {\tilde {\rho }}(w)={\frac {w^{T}Bw}{w^{T}Aw}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/68c6543e66c85166484c956afb65e16dd32fed82), where     B ∈ ∈   R  d × ×  d     {\displaystyle B\in R^{d\times d}}  ![{\displaystyle B\in R^{d\times d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a365fbacda143d5138879474fe8b9dd74ce8b2c9) is a symmetric matrix and     A ∈ ∈   R  d × ×  d     {\displaystyle A\in R^{d\times d}}  ![{\displaystyle A\in R^{d\times d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8de279512674b95aa9d64c8dbf34d020710f8ed1) is a symmetric [positive definite](./Positive_definiteness) matrix.

 

It is proven that the gradient descent convergence rate of the generalized Rayleigh quotient is

 

        λ λ   1   − −  ρ ρ  (  w  t + 1   )   ρ ρ  (  w  t + 1   − −   λ λ   2   )    ≤ ≤    (   1 − −      λ λ   1   − −   λ λ   2      λ λ   1   − −   λ λ   m i n         )    2 t       λ λ   1   − −  ρ ρ  (  w  t   )   ρ ρ  (  w  t   ) − −   λ λ   2        {\displaystyle {\frac {\lambda _{1}-\rho (w_{t+1})}{\rho (w_{t+1}-\lambda _{2})}}\leq {\bigg (}1-{\frac {\lambda _{1}-\lambda _{2}}{\lambda _{1}-\lambda _{min}}}{\bigg )}^{2t}{\frac {\lambda _{1}-\rho (w_{t})}{\rho (w_{t})-\lambda _{2}}}}  ![{\displaystyle {\frac {\lambda _{1}-\rho (w_{t+1})}{\rho (w_{t+1}-\lambda _{2})}}\leq {\bigg (}1-{\frac {\lambda _{1}-\lambda _{2}}{\lambda _{1}-\lambda _{min}}}{\bigg )}^{2t}{\frac {\lambda _{1}-\rho (w_{t})}{\rho (w_{t})-\lambda _{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a894c98e578963723b287726f9b223075d38e4b7), where      λ λ   1     {\displaystyle \lambda _{1}}  ![{\displaystyle \lambda _{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/571a423bece8f29bcd1b48572f18dd4f6213dce2) is the largest [eigenvalue](./Eigenvalues_and_eigenvectors) of     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a),      λ λ   2     {\displaystyle \lambda _{2}}  ![{\displaystyle \lambda _{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b668a1bd1e8ab9452ca975b7497546e7c1ba187) is the second largest eigenvalue of     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a), and      λ λ   m i n     {\displaystyle \lambda _{min}}  ![{\displaystyle \lambda _{min}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9ea5700b1cdbc0c935d3d34bc03c778a8641cc79) is the smallest eigenvalue of     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a).[[10]](./Batch_normalization#cite_note-10)

 

In our case,     B = u  u  T     {\displaystyle B=uu^{T}}  ![{\displaystyle B=uu^{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c8158101fea0192702480f5231aba7e185185789) is a rank one matrix, and the convergence result can be simplified accordingly. Specifically, consider gradient descent steps of the form      w  t + 1   =  w  t   − −   η η   t   ▽ ▽  ρ ρ  (  w  t   )   {\displaystyle w_{t+1}=w_{t}-\eta _{t}\triangledown \rho (w_{t})}  ![{\displaystyle w_{t+1}=w_{t}-\eta _{t}\triangledown \rho (w_{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/71855c87dab86bc52e1e722e6b7dc695c7891b66) with step size      η η   t   =     w  t   T   S  w  t     2 L  |  ρ ρ  (  w  t   )  |       {\displaystyle \eta _{t}={\frac {w_{t}^{T}Sw_{t}}{2L|\rho (w_{t})|}}}  ![{\displaystyle \eta _{t}={\frac {w_{t}^{T}Sw_{t}}{2L|\rho (w_{t})|}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4e30e4bf8005a6bfbc82ab34fc4ecef53a3e109d), and starting from     ρ ρ  (  w  0   ) ≠ ≠  0   {\displaystyle \rho (w_{0})\neq 0}  ![{\displaystyle \rho (w_{0})\neq 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e52618bcfa5e5a8170f3f52c9c629aad11a788ea), then

 

    ρ ρ  (  w  t   ) − −  ρ ρ  (  w  ∗ ∗    ) ≤ ≤    (   1 − −    μ μ  L      )    2 t   ( ρ ρ  (  w  0   ) − −  ρ ρ  (  w  ∗ ∗    ) )   {\displaystyle \rho (w_{t})-\rho (w^{*})\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2t}(\rho (w_{0})-\rho (w^{*}))}  ![{\displaystyle \rho (w_{t})-\rho (w^{*})\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2t}(\rho (w_{0})-\rho (w^{*}))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8d977d55687351b9820910c4b55adcce3c3fde06).

 

### Learning halfspace problem

 

The problem of learning halfspaces refers to the training of the [Perceptron](./Perceptron), which is the simplest form of neural network. The optimization problem in this case is

 

     min     w ~ ~     ∈ ∈   R  d      f  L H   (    w ~ ~     ) =  E  y , x   [ ϕ ϕ  (  z  T      w ~ ~     ) ]   {\displaystyle \min _{{\tilde {w}}\in R^{d}}f_{LH}({\tilde {w}})=E_{y,x}[\phi (z^{T}{\tilde {w}})]}  ![{\displaystyle \min _{{\tilde {w}}\in R^{d}}f_{LH}({\tilde {w}})=E_{y,x}[\phi (z^{T}{\tilde {w}})]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cad358cdfcff14d371a6807c76a72f07179b76a0), where     z = − −  y x   {\displaystyle z=-yx}  ![{\displaystyle z=-yx}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f6325883caf5034a3039aa57b80ff90cf19508a) and     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4) is an arbitrary loss function.

 

Suppose that     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4) is infinitely differentiable and has a bounded derivative. Assume that the objective function      f  L H     {\displaystyle f_{LH}}  ![{\displaystyle f_{LH}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94defc1ff6a3119cb74d8743797f2a9b5055b231) is     ζ ζ    {\displaystyle \zeta }  ![{\displaystyle \zeta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5c3916703cae7938143d38865f78f27faadd4ae)-[smooth](./Smoothness), and that a solution      α α   ∗ ∗    = a r g m i  n  α α     |   |  ▽ ▽  f ( α α  w )  |    |   2     {\displaystyle \alpha ^{*}=argmin_{\alpha }||\triangledown f(\alpha w)||^{2}}  ![{\displaystyle \alpha ^{*}=argmin_{\alpha }||\triangledown f(\alpha w)||^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6ba3acfacaaef16df296a3a4d5c07b5e1866dc0a) exists and is bounded such that     − −  ∞ ∞  <  α α   ∗ ∗    < ∞ ∞    {\displaystyle -\infty <\alpha ^{*}<\infty }  ![{\displaystyle -\infty <\alpha ^{*}<\infty }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a7dcae0fdb761140b64f974e10d7515bf30dd776). Also assume     z   {\displaystyle z}  ![{\displaystyle z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf368e72c009decd9b6686ee84a375632e11de98) is a [multivariate normal random variable](./Multivariate_normal_distribution). With the Gaussian assumption, it can be shown that all [critical points](./Critical_point_(network_science)) lie on the same line, for any choice of loss function     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4). Specifically, the gradient of      f  L H     {\displaystyle f_{LH}}  ![{\displaystyle f_{LH}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94defc1ff6a3119cb74d8743797f2a9b5055b231) could be represented as

 

     ▽ ▽     w ~ ~       f  L H   (    w ~ ~     ) =  c  1   (    w ~ ~     ) u +  c  2   (    w ~ ~     ) S    w ~ ~       {\displaystyle \triangledown _{\tilde {w}}f_{LH}({\tilde {w}})=c_{1}({\tilde {w}})u+c_{2}({\tilde {w}})S{\tilde {w}}}  ![{\displaystyle \triangledown _{\tilde {w}}f_{LH}({\tilde {w}})=c_{1}({\tilde {w}})u+c_{2}({\tilde {w}})S{\tilde {w}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c2487deac441b8543d343361909d7d5986233409), where       c  1   (    w ~ ~     ) =  E  z   [  ϕ ϕ   ( 1 )   (  z  T      w ~ ~     ) ] − −   E  z   [  ϕ ϕ   ( 2 )   (  z  T      w ~ ~     ) ] (  u  T      w ~ ~     )   {\displaystyle c_{1}({\tilde {w}})=E_{z}[\phi ^{(1)}(z^{T}{\tilde {w}})]-E_{z}[\phi ^{(2)}(z^{T}{\tilde {w}})](u^{T}{\tilde {w}})}  ![{\displaystyle c_{1}({\tilde {w}})=E_{z}[\phi ^{(1)}(z^{T}{\tilde {w}})]-E_{z}[\phi ^{(2)}(z^{T}{\tilde {w}})](u^{T}{\tilde {w}})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d41acf60dc403751d136a81ba607fbbf80b76ab),      c  2   (    w ~ ~     ) =  E  z   [  ϕ ϕ   ( 2 )   (  z  T      w ~ ~     ) ]   {\displaystyle c_{2}({\tilde {w}})=E_{z}[\phi ^{(2)}(z^{T}{\tilde {w}})]}  ![{\displaystyle c_{2}({\tilde {w}})=E_{z}[\phi ^{(2)}(z^{T}{\tilde {w}})]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e43fecb96d87a856bc20fe7e94d6f6fd172f58c3), and      ϕ ϕ   ( i )     {\displaystyle \phi ^{(i)}}  ![{\displaystyle \phi ^{(i)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7e06943f6204295a43850dac83b582d1c7de9aa1) is the     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20)-th derivative of     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4).

 

By setting the gradient to 0, it thus follows that the bounded critical points         w ~ ~      ∗ ∗      {\displaystyle {\tilde {w}}_{*}}  ![{\displaystyle {\tilde {w}}_{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92c500e6749b54d50218d0658abd54389e8c0c4d) can be expressed as         w ~ ~      ∗ ∗    =  g  ∗ ∗     S  − −  1   u   {\displaystyle {\tilde {w}}_{*}=g_{*}S^{-1}u}  ![{\displaystyle {\tilde {w}}_{*}=g_{*}S^{-1}u}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8010907b60d0727a6709bceaf0cd713e8dc529bb), where      g  ∗ ∗      {\displaystyle g_{*}}  ![{\displaystyle g_{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/158776589fce805bba6b36b91cf383832dfc50cf) depends on         w ~ ~      ∗ ∗      {\displaystyle {\tilde {w}}_{*}}  ![{\displaystyle {\tilde {w}}_{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92c500e6749b54d50218d0658abd54389e8c0c4d) and     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4). Combining this global property with length-direction decoupling, it could thus be proved that this optimization problem converges linearly.

 

First, a variation of [gradient descent](./Gradient_descent) with batch normalization, Gradient Descent in Normalized Parameterization (GDNP), is designed for the objective function      min  w ∈ ∈   R  d   ∖ ∖  { 0 } , γ γ  ∈ ∈  R    f  L H   ( w , γ γ  )   {\displaystyle \min _{w\in R^{d}\backslash \{0\},\gamma \in R}f_{LH}(w,\gamma )}  ![{\displaystyle \min _{w\in R^{d}\backslash \{0\},\gamma \in R}f_{LH}(w,\gamma )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a67794328deeba2944f3a9f90945c93288af54d7), such that the direction and length of the weights are updated separately. Denote the stopping criterion of GDNP as

 

    h (  w  t   ,  γ γ   t   ) =  E  z   [  ϕ ϕ  ′  (  z  T       w ~ ~      t   ) ] (  u  T    w  t   ) − −   E  z   [  ϕ ϕ  ″  (  z  T       w ~ ~      t   ) ] (  u  T    w  t    )  2     {\displaystyle h(w_{t},\gamma _{t})=E_{z}[\phi '(z^{T}{\tilde {w}}_{t})](u^{T}w_{t})-E_{z}[\phi ''(z^{T}{\tilde {w}}_{t})](u^{T}w_{t})^{2}}  ![{\displaystyle h(w_{t},\gamma _{t})=E_{z}[\phi '(z^{T}{\tilde {w}}_{t})](u^{T}w_{t})-E_{z}[\phi ''(z^{T}{\tilde {w}}_{t})](u^{T}w_{t})^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5d9060d18d7abd003631c293bd29c2432de2d7c).

 

Let the step size be

 

     s  t   = s (  w  t   ,  γ γ   t   ) = − −      |   |   w  t    |    |   S   3     L  g  t   h (  w  t   ,  γ γ   t   )      {\displaystyle s_{t}=s(w_{t},\gamma _{t})=-{\frac {||w_{t}||_{S}^{3}}{Lg_{t}h(w_{t},\gamma _{t})}}}  ![{\displaystyle s_{t}=s(w_{t},\gamma _{t})=-{\frac {||w_{t}||_{S}^{3}}{Lg_{t}h(w_{t},\gamma _{t})}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8a8e930d6a9ce8f24fb27a2bdd552b417323fd8).

 

For each step, if     h (  w  t   ,  γ γ   t   ) ≠ ≠  0   {\displaystyle h(w_{t},\gamma _{t})\neq 0}  ![{\displaystyle h(w_{t},\gamma _{t})\neq 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cde3c284d2a4b306d7a5eca3741e12cf716b5a37), then update the direction as

 

     w  t + 1   =  w  t   − −   s  t    ▽ ▽   w   f (  w  t   ,  γ γ   t   )   {\displaystyle w_{t+1}=w_{t}-s_{t}\triangledown _{w}f(w_{t},\gamma _{t})}  ![{\displaystyle w_{t+1}=w_{t}-s_{t}\triangledown _{w}f(w_{t},\gamma _{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/29ca30755c4a189c3f933cd2149a5399252f8604).

 

Then update the length according to

 

     γ γ   t   =  Bisection  (  T  s   , f ,  w  t   )   {\displaystyle \gamma _{t}={\text{Bisection}}(T_{s},f,w_{t})}  ![{\displaystyle \gamma _{t}={\text{Bisection}}(T_{s},f,w_{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aa840ef9457b5a381820c267354c78f2ea4fce05), where      Bisection()    {\displaystyle {\text{Bisection()}}}  ![{\displaystyle {\text{Bisection()}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5122dd7bed813f4ea0fae09b75054ef987d0a05b) is the classical [bisection algorithm](./Bisection_algorithm), and      T  s     {\displaystyle T_{s}}  ![{\displaystyle T_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/942b5ac7697c72b9e3bc1e3b340daf7189fdf61f) is the total iterations ran in the bisection step.

 

Denote the total number of iterations as      T  d     {\displaystyle T_{d}}  ![{\displaystyle T_{d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/70cadcc969636b990957852f205868f9f7178840), then the final output of GDNP is

 

        w ~ ~       T  d     =  γ γ    T  d        w   T  d       |   |   w   T  d      |    |   S        {\displaystyle {\tilde {w}}_{T_{d}}=\gamma _{T_{d}}{\frac {w_{T_{d}}}{||w_{T_{d}}||_{S}}}}  ![{\displaystyle {\tilde {w}}_{T_{d}}=\gamma _{T_{d}}{\frac {w_{T_{d}}}{||w_{T_{d}}||_{S}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e005920866895e02728fea73604305f4837df36).

 

The GDNP algorithm thus slightly modifies the batch normalization step for the ease of mathematical analysis.

 

It can be shown that in GDNP, the partial derivative of      f  L H     {\displaystyle f_{LH}}  ![{\displaystyle f_{LH}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94defc1ff6a3119cb74d8743797f2a9b5055b231) against the length component converges to zero at a linear rate, such that

 

    (  ∂ ∂   γ γ     f  L H   (  w  t   ,  a  t   (  T  s   )    )  2   ≤ ≤      2  − −   T  s     ζ ζ   |   b  t   ( 0 )   − −   a  t   ( 0 )    |    μ μ   2       {\displaystyle (\partial _{\gamma }f_{LH}(w_{t},a_{t}^{(T_{s})})^{2}\leq {\frac {2^{-T_{s}}\zeta |b_{t}^{(0)}-a_{t}^{(0)}|}{\mu ^{2}}}}  ![{\displaystyle (\partial _{\gamma }f_{LH}(w_{t},a_{t}^{(T_{s})})^{2}\leq {\frac {2^{-T_{s}}\zeta |b_{t}^{(0)}-a_{t}^{(0)}|}{\mu ^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dac4b3d5ec56b983050733ec14eaf3bfb6d6349e), where      a  t   ( 0 )     {\displaystyle a_{t}^{(0)}}  ![{\displaystyle a_{t}^{(0)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/655ce27b59661a221a73a4db1c86d535b214cd18) and      b  t   0     {\displaystyle b_{t}^{0}}  ![{\displaystyle b_{t}^{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/80b96c113c5e0ef956ade48ffc16b034b42a1146) are the two starting points of the bisection algorithm on the left and on the right, correspondingly.

 

Further, for each iteration, the norm of the gradient of      f  L H     {\displaystyle f_{LH}}  ![{\displaystyle f_{LH}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94defc1ff6a3119cb74d8743797f2a9b5055b231) with respect to     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) converges linearly, such that

 

     |   |   w  t    |    |   S   2    |   |  ▽ ▽   f  L H   (  w  t   ,  g  t   )  |    |    S  − −  1     2   ≤ ≤    (   1 − −    μ μ  L      )    2 t    Φ Φ   2    γ γ   t   2   ( ρ ρ  (  w  0   ) − −   ρ ρ   ∗ ∗    )   {\displaystyle ||w_{t}||_{S}^{2}||\triangledown f_{LH}(w_{t},g_{t})||_{S^{-1}}^{2}\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2t}\Phi ^{2}\gamma _{t}^{2}(\rho (w_{0})-\rho ^{*})}  ![{\displaystyle ||w_{t}||_{S}^{2}||\triangledown f_{LH}(w_{t},g_{t})||_{S^{-1}}^{2}\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2t}\Phi ^{2}\gamma _{t}^{2}(\rho (w_{0})-\rho ^{*})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2e69aa8c10ac98e3226f97873f811f557bc4eda1).

 

Combining these two inequalities, a bound could thus be obtained for the gradient with respect to         w ~ ~       T  d       {\displaystyle {\tilde {w}}_{T_{d}}}  ![{\displaystyle {\tilde {w}}_{T_{d}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b13d0799f11fb82900a42308223db319bdb3121e):

 

     |   |   ▽ ▽     w ~ ~      f (     w ~ ~       T  d     )  |    |   2   ≤ ≤    (   1 − −    μ μ  L      )    2  T  d      Φ Φ   2   ( ρ ρ  (  w  0   ) − −   ρ ρ   ∗ ∗    ) +     2  − −   T  s     ζ ζ   |   b  t   ( 0 )   − −   a  t   ( 0 )    |    μ μ   2       {\displaystyle ||\triangledown _{\tilde {w}}f({\tilde {w}}_{T_{d}})||^{2}\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2T_{d}}\Phi ^{2}(\rho (w_{0})-\rho ^{*})+{\frac {2^{-T_{s}}\zeta |b_{t}^{(0)}-a_{t}^{(0)}|}{\mu ^{2}}}}  ![{\displaystyle ||\triangledown _{\tilde {w}}f({\tilde {w}}_{T_{d}})||^{2}\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2T_{d}}\Phi ^{2}(\rho (w_{0})-\rho ^{*})+{\frac {2^{-T_{s}}\zeta |b_{t}^{(0)}-a_{t}^{(0)}|}{\mu ^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0489612fd15e3ad03e96d7a1656940429e4e9f05), such that the algorithm is guaranteed to converge linearly.

 

Although the proof stands on the assumption of Gaussian input, it is also shown in experiments that GDNP could accelerate optimization without this constraint.

 

### Neural networks

 

Consider a [multilayer perceptron](./Multilayer_perceptron) (MLP) with one hidden layer and     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) hidden units with mapping from input     x ∈ ∈   R  d     {\displaystyle x\in R^{d}}  ![{\displaystyle x\in R^{d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/23a92052936ccf19989dd3604fc20ffd124440b7) to a scalar output described as

 

     F  x   (    W ~ ~     , Θ Θ  ) =  ∑ ∑   i = 1   m    θ θ   i   ϕ ϕ  (  x  T       w ~ ~      ( i )   )   {\displaystyle F_{x}({\tilde {W}},\Theta )=\sum _{i=1}^{m}\theta _{i}\phi (x^{T}{\tilde {w}}^{(i)})}  ![{\displaystyle F_{x}({\tilde {W}},\Theta )=\sum _{i=1}^{m}\theta _{i}\phi (x^{T}{\tilde {w}}^{(i)})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94913cebd2254503c351cac4f0a0ab4160ee15d8), where         w ~ ~      ( i )     {\displaystyle {\tilde {w}}^{(i)}}  ![{\displaystyle {\tilde {w}}^{(i)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dead04d712f11020730be05360af8f61eccd61fd) and      θ θ   i     {\displaystyle \theta _{i}}  ![{\displaystyle \theta _{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/302b19204ed378e99ff4575341a67eebdbe5a555) are the input and output weights of unit     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) correspondingly, and     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4) is the activation function and is assumed to be a [tanh function](./Hyperbolic_function#Tanh).

 

The input and output weights could then be optimized with

 

     min     W ~ ~     , Θ Θ    (  f  N N   (    W ~ ~     , Θ Θ  ) =  E  y , x   [ l ( − −  y  F  x   (    W ~ ~     , Θ Θ  ) ) ] )   {\displaystyle \min _{{\tilde {W}},\Theta }(f_{NN}({\tilde {W}},\Theta )=E_{y,x}[l(-yF_{x}({\tilde {W}},\Theta ))])}  ![{\displaystyle \min _{{\tilde {W}},\Theta }(f_{NN}({\tilde {W}},\Theta )=E_{y,x}[l(-yF_{x}({\tilde {W}},\Theta ))])}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0fa1741f223166a1d9cb8ba20cb27e6eec9d021b), where     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) is a loss function,        W ~ ~     = {     w ~ ~      ( 1 )   , . . . ,     w ~ ~      ( m )   }   {\displaystyle {\tilde {W}}=\{{\tilde {w}}^{(1)},...,{\tilde {w}}^{(m)}\}}  ![{\displaystyle {\tilde {W}}=\{{\tilde {w}}^{(1)},...,{\tilde {w}}^{(m)}\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8366c97137f31a1f915fed43ab8c3b29676d5822), and     Θ Θ  = {  θ θ   ( 1 )   , . . . ,  θ θ   ( m )   }   {\displaystyle \Theta =\{\theta ^{(1)},...,\theta ^{(m)}\}}  ![{\displaystyle \Theta =\{\theta ^{(1)},...,\theta ^{(m)}\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6a65c783ef8a8eb0acb273071c38d96ad298f055).

 

Consider fixed     Θ Θ    {\displaystyle \Theta }  ![{\displaystyle \Theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/bc927b19f46d005b4720db7a0f96cd5b6f1a0d9b) and optimizing only        W ~ ~       {\displaystyle {\tilde {W}}}  ![{\displaystyle {\tilde {W}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0dae50f239be9486a2273ec98c497e983610fab1), it can be shown that the critical points of      f  N N   (    W ~ ~     )   {\displaystyle f_{NN}({\tilde {W}})}  ![{\displaystyle f_{NN}({\tilde {W}})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/69c185c5fce2d4eadfd6477b3350d07ce1cff644) of a particular hidden unit     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20),         w ^ ^      ( i )     {\displaystyle {\hat {w}}^{(i)}}  ![{\displaystyle {\hat {w}}^{(i)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/60d1b4ae6b98309cc9035090a9fb3ddd61785b22), all align along one line depending on incoming information into the hidden layer, such that

 

        w ^ ^      ( i )   =     c ^ ^      ( i )    S  − −  1   u   {\displaystyle {\hat {w}}^{(i)}={\hat {c}}^{(i)}S^{-1}u}  ![{\displaystyle {\hat {w}}^{(i)}={\hat {c}}^{(i)}S^{-1}u}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c9d8954d7eaad91a6a8c0df63d3e0a36d3d5d5b6), where         c ^ ^      ( i )   ∈ ∈  R   {\displaystyle {\hat {c}}^{(i)}\in R}  ![{\displaystyle {\hat {c}}^{(i)}\in R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3f6e6f405115516bd625706391cec3f299c115c2) is a scalar,     i = 1 , . . . , m   {\displaystyle i=1,...,m}  ![{\displaystyle i=1,...,m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f883868ad60f110c23795233999f65424ce2edc8).

 

This result could be proved by setting the gradient of      f  N N     {\displaystyle f_{NN}}  ![{\displaystyle f_{NN}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/08a9d666847a80de2fc08867864b3df53f83b651) to zero and solving the system of equations.

 

Apply the GDNP algorithm to this optimization problem by alternating optimization over the different hidden units. Specifically, for each hidden unit, run GDNP to find the optimal     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7) and     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a). With the same choice of stopping criterion and stepsize, it follows that

 

     |   |   ▽ ▽       w ~ ~      ( i )     f (     w ~ ~      t   ( i )   )  |    |    S  − −  1     2   ≤ ≤    (   1 − −    μ μ  L      )    2 t   C ( ρ ρ  (  w  0   ) − −   ρ ρ   ∗ ∗    ) +     2  − −   T  s   ( i )     ζ ζ   |   b  t   ( 0 )   − −   a  t   ( 0 )    |    μ μ   2       {\displaystyle ||\triangledown _{{\tilde {w}}^{(i)}}f({\tilde {w}}_{t}^{(i)})||_{S^{-1}}^{2}\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2t}C(\rho (w_{0})-\rho ^{*})+{\frac {2^{-T_{s}^{(i)}}\zeta |b_{t}^{(0)}-a_{t}^{(0)}|}{\mu ^{2}}}}  ![{\displaystyle ||\triangledown _{{\tilde {w}}^{(i)}}f({\tilde {w}}_{t}^{(i)})||_{S^{-1}}^{2}\leq {\bigg (}1-{\frac {\mu }{L}}{\bigg )}^{2t}C(\rho (w_{0})-\rho ^{*})+{\frac {2^{-T_{s}^{(i)}}\zeta |b_{t}^{(0)}-a_{t}^{(0)}|}{\mu ^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/433aac5aef62e7c3e0b249a06d84ef9f14d4829a).

 

Since the parameters of each hidden unit converge linearly, the whole optimization problem has a linear rate of convergence.[[8]](./Batch_normalization#cite_note-:2-8)

 

## References

  
1. [1](./Batch_normalization#cite_ref-:0_1-0) [2](./Batch_normalization#cite_ref-:0_1-1) [3](./Batch_normalization#cite_ref-:0_1-2) [4](./Batch_normalization#cite_ref-:0_1-3) Ioffe, Sergey; Szegedy, Christian (2015). "Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift". [arXiv](./ArXiv_(identifier)):[1502.03167](https://arxiv.org/abs/1502.03167) [[cs.LG](https://arxiv.org/archive/cs.LG)].
2. [↑](./Batch_normalization#cite_ref-:13_2-0) Santurkar, Shibani; Tsipras, Dimitris; Ilyas, Andrew; Madry, Aleksander (29 May 2018). "How Does Batch Normalization Help Optimization?". [arXiv](./ArXiv_(identifier)):[1805.11604](https://arxiv.org/abs/1805.11604) [[stat.ML](https://arxiv.org/archive/stat.ML)].
3. [↑](./Batch_normalization#cite_ref-:73_3-0) Yang, Greg; Pennington, Jeffrey; Rao, Vinay; Sohl-Dickstein, Jascha; Schoenholz, Samuel S. (2019). "A Mean Field Theory of Batch Normalization". [arXiv](./ArXiv_(identifier)):[1902.08129](https://arxiv.org/abs/1902.08129) [[cs.NE](https://arxiv.org/archive/cs.NE)].
4. [↑](./Batch_normalization#cite_ref-:23_4-0) Kohler, Jonas; Daneshmand, Hadi; Lucchi, Aurelien; Zhou, Ming; Neymeyr, Klaus; Hofmann, Thomas (27 May 2018). "Exponential convergence rates for Batch Normalization: The power of length-direction decoupling in non-convex optimization". [arXiv](./ArXiv_(identifier)):[1805.10694](https://arxiv.org/abs/1805.10694) [[stat.ML](https://arxiv.org/archive/stat.ML)].
5. [1](./Batch_normalization#cite_ref-:1_5-0) [2](./Batch_normalization#cite_ref-:1_5-1) [3](./Batch_normalization#cite_ref-:1_5-2) Santurkar, Shibani; Tsipras, Dimitris; Ilyas, Andrew; Madry, Aleksander (29 May 2018). "How Does Batch Normalization Help Optimization?". [arXiv](./ArXiv_(identifier)):[1805.11604](https://arxiv.org/abs/1805.11604) [[stat.ML](https://arxiv.org/archive/stat.ML)].
6. [1](./Batch_normalization#cite_ref-VGG_6-0) [2](./Batch_normalization#cite_ref-VGG_6-1) Simonyan, Karen; Andrew, Zisserman (2014). "Very Deep Convolution Networks for Large Scale Image Recognition". [arXiv](./ArXiv_(identifier)):[1409.1556](https://arxiv.org/abs/1409.1556) [[cs.CV](https://arxiv.org/archive/cs.CV)].
7. [↑](./Batch_normalization#cite_ref-7) Ba, J., Kiros, J.R., & Hinton, G.E. (2016). Layer Normalization. ArXiv, abs/1607.06450.
8. [1](./Batch_normalization#cite_ref-:2_8-0) [2](./Batch_normalization#cite_ref-:2_8-1) Kohler, Jonas; Daneshmand, Hadi; Lucchi, Aurelien; Zhou, Ming; Neymeyr, Klaus; Hofmann, Thomas (27 May 2018). "Exponential convergence rates for Batch Normalization: The power of length-direction decoupling in non-convex optimization". [arXiv](./ArXiv_(identifier)):[1805.10694](https://arxiv.org/abs/1805.10694) [[stat.ML](https://arxiv.org/archive/stat.ML)].
9. [↑](./Batch_normalization#cite_ref-:7_9-0) Yang, Greg; Pennington, Jeffrey; Rao, Vinay; Sohl-Dickstein, Jascha; Schoenholz, Samuel S. (2019). "A Mean Field Theory of Batch Normalization". [arXiv](./ArXiv_(identifier)):[1902.08129](https://arxiv.org/abs/1902.08129) [[cs.NE](https://arxiv.org/archive/cs.NE)].
10. [↑](./Batch_normalization#cite_ref-10) Knyazev, Neymeyr (2003). ["A geometric theory for preconditioned inverse iteration III: A short and sharp convergence estimate for generalized eigenvalue problems"](https://doi.org/10.1016%2FS0024-3795%2801%2900461-X). *Linear Algebra and Its Applications*. **358** (1–3): 95–114. [doi](./Doi_(identifier)):[10.1016/S0024-3795(01)00461-X](https://doi.org/10.1016%2FS0024-3795%2801%2900461-X).

 

## Further reading

 
- Ioffe, Sergey; Szegedy, Christian (2015). "Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift", ICML'15: Proceedings of the 32nd International Conference on International Conference on Machine Learning - Volume 37, July 2015 Pages 448–456
- Simonyan, Karen; Zisserman, Andrew (2014). "Very Deep Convolutional Networks for Large-Scale Image Recognition". [arXiv](./ArXiv_(identifier)):[1409.1556](https://arxiv.org/abs/1409.1556) [[cs.CV](https://arxiv.org/archive/cs.CV)].

 
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