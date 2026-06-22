---
source: sources/wiki-Batch_normalization.md
source_url: https://en.wikipedia.org/wiki/Batch_normalization
chunk: 1/4
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

 


