---
source: https://en.wikipedia.org/wiki/Activation_function
fetched: 2026-06-21
---

Artificial neural network node function For the formalism used to approximate the influence of an extracellular electrical field on neurons, see [activating function](./Activating_function). For a linear system's transfer function, see [transfer function](./Transfer_function). 
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

 

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/8/88/Logistic-curve.svg/250px-Logistic-curve.svg.png)](./File:Logistic-curve.svg)Logistic activation function 

In [artificial neural networks](./Artificial_neural_networks), the **activation function** of a node is a function that calculates the output of the node based on its individual inputs and their weights. Nontrivial problems can be solved using only a few nodes if the activation function is *nonlinear*.[[1]](./Activation_function#cite_note-1)

 

Modern activation functions include the logistic ([sigmoid](./Sigmoid_function)) function used in the 2012 [speech recognition](./Speech_recognition) model developed by [Hinton](./Geoffrey_Hinton) et al;[[2]](./Activation_function#cite_note-2) the [ReLU](./Rectified_linear_unit) used in the 2012 [AlexNet](./AlexNet) computer vision model[[3]](./Activation_function#cite_note-3)[[4]](./Activation_function#cite_note-4) and in the 2015 [ResNet](./Residual_neural_network) model; and the smooth version of the ReLU, the [GELU](./ReLU#Gaussian-error_linear_unit_(GELU)), which was used in the 2018 [BERT](./BERT_(language_model)) model.[[5]](./Activation_function#cite_note-ReferenceA-5)

 

## Comparison of activation functions

 

Aside from their empirical performance, activation functions also have different mathematical properties:

 NonlinearWhen the activation function is non-linear, then a two-layer neural network can be proven to be a universal function approximator.[[6]](./Activation_function#cite_note-6) This is known as the [Universal Approximation Theorem](./Universal_approximation_theorem). The identity activation function does not satisfy this property. When multiple layers use the identity activation function, the entire network is equivalent to a single-layer model. RangeWhen the range of the activation function is finite, gradient-based training methods tend to be more stable, because pattern presentations significantly affect only limited weights. When the range is infinite, training is generally more efficient because pattern presentations significantly affect most of the weights. In the latter case, smaller [learning rates](./Learning_rate) are typically necessary.[*[citation needed](./Wikipedia:Citation_needed)*] Continuously differentiableThis property is desirable for enabling gradient-based optimization methods ([ReLU](./Rectifier_(neural_networks)) is not continuously differentiable and has some issues with gradient-based optimization, but it is still possible). The binary step activation function is not differentiable at 0, and it differentiates to 0 for all other values, so gradient-based methods can make no progress with it.[[7]](./Activation_function#cite_note-7) 

These properties do not decisively influence performance, nor are they the only mathematical properties that may be useful. For instance, the strictly positive range of the [softplus](./Softplus) makes it suitable for predicting variances in [variational autoencoders](./Autoencoder#Variational_autoencoder_(VAE)).

 

## Mathematical details

 

The most common activation functions can be divided into three categories: [ridge functions](./Ridge_function), [radial functions](./Radial_function) and [fold functions](./Fold_function).

 

An activation function     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) is **saturating** if      lim   |  v  |  → →  ∞ ∞     |  ∇ ∇  f ( v )  |  = 0   {\displaystyle \lim _{|v|\to \infty }|\nabla f(v)|=0}  ![{\displaystyle \lim _{|v|\to \infty }|\nabla f(v)|=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/021f17d830f9788b09661f13eba64efdb08f7f81). It is **nonsaturating** if      lim   |  v  |  → →  ∞ ∞     |  ∇ ∇  f ( v )  |  ≠ ≠  0   {\displaystyle \lim _{|v|\to \infty }|\nabla f(v)|\neq 0}  ![{\displaystyle \lim _{|v|\to \infty }|\nabla f(v)|\neq 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d1155f5745278662978a46abb282732cdc018c4). Non-saturating activation functions, such as [ReLU](./Rectified_linear_unit), may be better than saturating activation functions, because they are less likely to suffer from the [vanishing gradient problem](./Vanishing_gradient_problem).[[8]](./Activation_function#cite_note-8)

 

### Ridge activation functions

 Main article: [Ridge function](./Ridge_function) 

Ridge functions are multivariate functions acting on a linear combination of the input variables. Often used examples include:[*[clarification needed](./Wikipedia:Please_clarify)*]

 
- [Linear](./Linear) activation:     ϕ ϕ  (  v  ) = a +   v  ′   b    {\displaystyle \phi (\mathbf {v} )=a+\mathbf {v} '\mathbf {b} }  ![{\displaystyle \phi (\mathbf {v} )=a+\mathbf {v} '\mathbf {b} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed31c6adef34fb6edec1f2d8ce728129fad0fcb4),
- [ReLU](./Rectified_linear_unit) activation:     ϕ ϕ  (  v  ) = max ( 0 , a +   v  ′   b  )   {\displaystyle \phi (\mathbf {v} )=\max(0,a+\mathbf {v} '\mathbf {b} )}  ![{\displaystyle \phi (\mathbf {v} )=\max(0,a+\mathbf {v} '\mathbf {b} )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fa1a705a1fc6718e11db7829c71dc4140b7284b6),
- [Heaviside](./Heaviside_function) activation:     ϕ ϕ  (  v  ) =  1  a +   v  ′   b  > 0     {\displaystyle \phi (\mathbf {v} )=1_{a+\mathbf {v} '\mathbf {b} >0}}  ![{\displaystyle \phi (\mathbf {v} )=1_{a+\mathbf {v} '\mathbf {b} >0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b000741d74e6e32f416e12d8d7ea7ace33c88caf),
- [Logistic](./Logistic_function) activation:     ϕ ϕ  (  v  ) = ( 1 + exp ⁡ ⁡  ( − −  a − −    v  ′   b  )  )  − −  1     {\displaystyle \phi (\mathbf {v} )=(1+\exp(-a-\mathbf {v} '\mathbf {b} ))^{-1}}  ![{\displaystyle \phi (\mathbf {v} )=(1+\exp(-a-\mathbf {v} '\mathbf {b} ))^{-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1799f7243c7c1970bab912ffed951598a545e65d).

 

In [biologically inspired neural networks](./Neural_network_(biology)), the activation function is usually an abstraction representing the rate of [action potential](./Action_potential) firing in the cell.[[9]](./Activation_function#cite_note-9) In its simplest form, this function is [binary](./Binary_function)—that is, either the neuron is firing or not.[[10]](./Activation_function#cite_note-10)

 

Neurons also cannot fire faster than a certain rate. This biological limitation motivates the use of sigmoid activation functions, whose output range is confined to a finite interval.

 

The function looks like     ϕ ϕ  (  v  ) = U ( a +   v  ′   b  )   {\displaystyle \phi (\mathbf {v} )=U(a+\mathbf {v} '\mathbf {b} )}  ![{\displaystyle \phi (\mathbf {v} )=U(a+\mathbf {v} '\mathbf {b} )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb75cd94baebd2dda406680a3050f3783423edea), where     U   {\displaystyle U}  ![{\displaystyle U}](https://wikimedia.org/api/rest_v1/media/math/render/svg/458a728f53b9a0274f059cd695e067c430956025) is the [Heaviside step function](./Heaviside_step_function). 

 

If a line has a positive [slope](./Slope), on the other hand, it may reflect the increase in firing rate that occurs as input current increases. Such a function would be of the form     ϕ ϕ  (  v  ) = a +   v  ′   b    {\displaystyle \phi (\mathbf {v} )=a+\mathbf {v} '\mathbf {b} }  ![{\displaystyle \phi (\mathbf {v} )=a+\mathbf {v} '\mathbf {b} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed31c6adef34fb6edec1f2d8ce728129fad0fcb4).

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/42/ReLU_and_GELU.svg/250px-ReLU_and_GELU.svg.png)](./File:ReLU_and_GELU.svg)Rectified linear unit and Gaussian error linear unit activation functions 

### Radial activation functions

 Main article: [Radial function](./Radial_function) 

A special class of activation functions known as [radial basis functions](./Radial_basis_function) (RBFs) are used in [RBF networks](./Radial_basis_function_network). These activation functions can take many forms, but they are usually found as one of the following functions:

 
- [Gaussian](./Gaussian_function):      ϕ ϕ  (  v  ) = exp ⁡ ⁡   (  − −     ‖ ‖   v  − −   c   ‖ ‖   2     2  σ σ   2       )    {\displaystyle \,\phi (\mathbf {v} )=\exp \left(-{\frac {\|\mathbf {v} -\mathbf {c} \|^{2}}{2\sigma ^{2}}}\right)}  ![{\displaystyle \,\phi (\mathbf {v} )=\exp \left(-{\frac {\|\mathbf {v} -\mathbf {c} \|^{2}}{2\sigma ^{2}}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/35c95662dac6d6832a8416c5bfdb289f27eb9a0e)
- Multiquadratics:      ϕ ϕ  (  v  ) =   ‖ ‖   v  − −   c   ‖ ‖   2   +  a  2       {\displaystyle \,\phi (\mathbf {v} )={\sqrt {\|\mathbf {v} -\mathbf {c} \|^{2}+a^{2}}}}  ![{\displaystyle \,\phi (\mathbf {v} )={\sqrt {\|\mathbf {v} -\mathbf {c} \|^{2}+a^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e3dd7c063c480f51a789fc219deacf9ff05239ff)
- Inverse multiquadratics:      ϕ ϕ  (  v  ) =   (  ‖ ‖   v  − −   c   ‖ ‖   2   +  a  2    )   − −    1 2       {\displaystyle \,\phi (\mathbf {v} )=\left(\|\mathbf {v} -\mathbf {c} \|^{2}+a^{2}\right)^{-{\frac {1}{2}}}}  ![{\displaystyle \,\phi (\mathbf {v} )=\left(\|\mathbf {v} -\mathbf {c} \|^{2}+a^{2}\right)^{-{\frac {1}{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/851f303abbe017788c38b1ade9b5223bdee10764)
- [Polyharmonic splines](./Polyharmonic_spline)

 

where      c    {\displaystyle \mathbf {c} }  ![{\displaystyle \mathbf {c} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/8798d172f59e21f2ce193a3118d4063d19353ded) is the vector representing the function *center* and     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc) and     σ σ    {\displaystyle \sigma }  ![{\displaystyle \sigma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/59f59b7c3e6fdb1d0365a494b81fb9a696138c36) are parameters affecting the spread of the radius.

 

### Other examples

 

Periodic functions can serve as activation functions. Usually the [sinusoid](./Sine_wave) is used, as any periodic function is decomposable into sinusoids by the [Fourier transform](./Fourier_transform).[[11]](./Activation_function#cite_note-11)

 

Quadratic activation maps     x ↦ ↦   x  2     {\displaystyle x\mapsto x^{2}}  ![{\displaystyle x\mapsto x^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/40b49de3850ec5b2be3acb8db45514958c5e80ae).[[12]](./Activation_function#cite_note-12)[[13]](./Activation_function#cite_note-13)

 

### Folding activation functions

 Main article: [Fold function](./Fold_function) 

Folding activation functions are extensively used in the [pooling layers](./Pooling_layer) in [convolutional neural networks](./Convolutional_neural_network), and in output layers of [multiclass classification](./Multiclass_classification) networks. These activations perform [aggregation](./Aggregate_function) over the inputs, such as taking the [mean](./Mean), [minimum](./Minimum) or [maximum](./Maximum). In multiclass classification the [softmax](./Softmax_function) activation is often used.

 

### Table of activation functions

 

The following table compares the properties of several activation functions that are functions of one [fold](./Fold_(higher-order_function)) x from the previous layer or layers:

 
| Name | Plot | Function,g(x){\displaystyle g(x)} | Derivativeofg{\displaystyle g},g′(x){\displaystyle g'(x)} | Range | Order of continuity |
| --- | --- | --- | --- | --- | --- |
| Identity |  | x{\displaystyle x} | 1{\displaystyle 1} | (−∞,∞){\displaystyle (-\infty ,\infty )} | C∞{\displaystyle C^{\infty }} |
| Binary step |  | {0ifx<01ifx≥0{\displaystyle {\begin{cases}0&{\text{if }}x<0\\1&{\text{if }}x\geq 0\end{cases}}} | 0{\displaystyle 0} | {0,1}{\displaystyle \{0,1\}} | C−1{\displaystyle C^{-1}} |
| Logistic, sigmoid, or softstep |  | σ(x)≐11+e−x{\displaystyle \sigma (x)\doteq {\frac {1}{1+e^{-x}}}} | g(x)(1−g(x)){\displaystyle g(x)(1-g(x))} | (0,1){\displaystyle (0,1)} | C∞{\displaystyle C^{\infty }} |
| Hyperbolic tangent (tanh) |  | tanh⁡(x)≐ex−e−xex+e−x{\displaystyle \tanh(x)\doteq {\frac {e^{x}-e^{-x}}{e^{x}+e^{-x}}}} | 1−g(x)2{\displaystyle 1-g(x)^{2}} | (−1,1){\displaystyle (-1,1)} | C∞{\displaystyle C^{\infty }} |
| Soboleva modified hyperbolic tangent (smht) |  | smht⁡(x)≐eax−e−bxecx+e−dx{\displaystyle \operatorname {smht} (x)\doteq {\frac {e^{ax}-e^{-bx}}{e^{cx}+e^{-dx}}}} |  | (−1,1){\displaystyle (-1,1)} | C∞{\displaystyle C^{\infty }} |
| Softsign |  | x1+|x|{\displaystyle {\frac {x}{1+|x|}}} | 1(1+|x|)2{\displaystyle {\frac {1}{(1+|x|)^{2}}}} | (−1,1){\displaystyle (-1,1)} | C1{\displaystyle C^{1}} |
| Rectified linear unit(ReLU)[14] |  | (x)+≐{0ifx≤0xifx>0=max(0,x)=x1x>0{\displaystyle {\begin{aligned}(x)^{+}\doteq {}&{\begin{cases}0&{\text{if }}x\leq 0\\x&{\text{if }}x>0\end{cases}}\\={}&\max(0,x)=x{\textbf {1}}_{x>0}\end{aligned}}} | {0ifx<01ifx>0{\displaystyle {\begin{cases}0&{\text{if }}x<0\\1&{\text{if }}x>0\end{cases}}} | [0,∞){\displaystyle [0,\infty )} | C0{\displaystyle C^{0}} |
| Gaussian Error Linear Unit (GELU)[5] |  | 12x(1+erf(x2))=xΦ(x){\displaystyle {\begin{aligned}&{\frac {1}{2}}x\left(1+{\text{erf}}\left({\frac {x}{\sqrt {2}}}\right)\right)\\{}={}&x\Phi (x)\end{aligned}}}whereerf{\displaystyle \mathrm {erf} }is thegaussian error function. | Φ(x)+12xϕ(x){\displaystyle \Phi (x)+{\frac {1}{2}}x\phi (x)}whereϕ(x)=12πe−12x2{\displaystyle \phi (x)={\frac {1}{\sqrt {2\pi }}}e^{-{\frac {1}{2}}x^{2}}}is the probability density function of standard gaussian distribution. | (−0.17…,∞){\displaystyle (-0.17\ldots ,\infty )} | C∞{\displaystyle C^{\infty }} |
| Softplus[15] |  | ln⁡(1+ex){\displaystyle \ln \left(1+e^{x}\right)} | 11+e−x{\displaystyle {\frac {1}{1+e^{-x}}}} | (0,∞){\displaystyle (0,\infty )} | C∞{\displaystyle C^{\infty }} |
| Exponential linear unit (ELU)[16] |  | {α(ex−1)ifx≤0xifx>0{\displaystyle {\begin{cases}\alpha \left(e^{x}-1\right)&{\text{if }}x\leq 0\\x&{\text{if }}x>0\end{cases}}}with parameterα{\displaystyle \alpha } | {αexifx<01ifx>0{\displaystyle {\begin{cases}\alpha e^{x}&{\text{if }}x<0\\1&{\text{if }}x>0\end{cases}}} | (−α,∞){\displaystyle (-\alpha ,\infty )} | {C1ifα=1C0otherwise{\displaystyle {\begin{cases}C^{1}&{\text{if }}\alpha =1\\C^{0}&{\text{otherwise}}\end{cases}}} |
| Scaled exponential linear unit (SELU)[17] |  | λ{α(ex−1)ifx<0xifx≥0{\displaystyle \lambda {\begin{cases}\alpha (e^{x}-1)&{\text{if }}x<0\\x&{\text{if }}x\geq 0\end{cases}}}with parametersλ=1.0507{\displaystyle \lambda =1.0507}andα=1.67326{\displaystyle \alpha =1.67326} | λ{αexifx<01ifx≥0{\displaystyle \lambda {\begin{cases}\alpha e^{x}&{\text{if }}x<0\\1&{\text{if }}x\geq 0\end{cases}}} | (−λα,∞){\displaystyle (-\lambda \alpha ,\infty )} | C0{\displaystyle C^{0}} |
| Leaky rectified linear unit (Leaky ReLU)[18] |  | {0.01xifx≤0xifx>0{\displaystyle {\begin{cases}0.01x&{\text{if }}x\leq 0\\x&{\text{if }}x>0\end{cases}}} | {0.01ifx<01ifx>0{\displaystyle {\begin{cases}0.01&{\text{if }}x<0\\1&{\text{if }}x>0\end{cases}}} | (−∞,∞){\displaystyle (-\infty ,\infty )} | C0{\displaystyle C^{0}} |
| Parametric rectified linear unit (PReLU)[19] |  | {αxifx<0xifx≥0{\displaystyle {\begin{cases}\alpha x&{\text{if }}x<0\\x&{\text{if }}x\geq 0\end{cases}}}with parameterα{\displaystyle \alpha } | {αifx<01ifx≥0{\displaystyle {\begin{cases}\alpha &{\text{if }}x<0\\1&{\text{if }}x\geq 0\end{cases}}} | (−∞,∞){\displaystyle (-\infty ,\infty )} | C0{\displaystyle C^{0}} |
| Rectified Parametric Sigmoid Units (flexible, 5 parameters) |  | α(2x1{x⩾λ}−gλ,σ,μ,β(x))+(1−α)gλ,σ,μ,β(x){\displaystyle \alpha (2x{1}_{\{x\geqslant \lambda \}}-g_{\lambda ,\sigma ,\mu ,\beta }(x))+(1-\alpha )g_{\lambda ,\sigma ,\mu ,\beta }(x)}wheregλ,σ,μ,β(x)=(x−λ)1{x⩾λ}1+e−sgn⁡(x−μ)(|x−μ|σ)β{\displaystyle g_{\lambda ,\sigma ,\mu ,\beta }(x)={\frac {(x-\lambda ){1}_{\{x\geqslant \lambda \}}}{1+e^{-\operatorname {sgn}(x-\mu )\left({\frac {\vert x-\mu \vert }{\sigma }}\right)^{\beta }}}}}[20] | −{\displaystyle -} | (−∞,+∞){\displaystyle (-\infty ,+\infty )} | C0{\displaystyle C^{0}} |
| Sigmoid linear unit(SiLU,[5]Sigmoid shrinkage,[21]SiL,[22]orSwish-‍1[23]) |  | x1+e−x{\displaystyle {\frac {x}{1+e^{-x}}}} | 1+e−x+xe−x(1+e−x)2{\displaystyle {\frac {1+e^{-x}+xe^{-x}}{\left(1+e^{-x}\right)^{2}}}} | [−0.278…,∞){\displaystyle [-0.278\ldots ,\infty )} | C∞{\displaystyle C^{\infty }} |
| Exponential Linear Sigmoid SquasHing (ELiSH)[24] |  | {ex−11+e−xifx<0x1+e−xifx≥0{\displaystyle {\begin{cases}{\frac {e^{x}-1}{1+e^{-x}}}&{\text{if }}x<0\\{\frac {x}{1+e^{-x}}}&{\text{if }}x\geq 0\end{cases}}} | {2e2x+e3x−exe2x+2ex+1ifx<0xex+e2x+exe2x+2ex+1ifx≥0{\displaystyle {\begin{cases}{\frac {2e^{2x}+e^{3x}-e^{x}}{e^{2x}+2e^{x}+1}}&{\text{if }}x<0\\{\frac {xe^{x}+e^{2x}+e^{x}}{e^{2x}+2e^{x}+1}}&{\text{if }}x\geq 0\end{cases}}} | [−0.881…,∞){\displaystyle [-0.881\ldots ,\infty )} | C1{\displaystyle C^{1}} |
| Gaussian |  | e−x2{\displaystyle e^{-x^{2}}} | −2xe−x2{\displaystyle -2xe^{-x^{2}}} | (0,1]{\displaystyle (0,1]} | C∞{\displaystyle C^{\infty }} |
| Sinusoid |  | sin⁡x{\displaystyle \sin x} | cos⁡x{\displaystyle \cos x} | [−1,1]{\displaystyle [-1,1]} | C∞{\displaystyle C^{\infty }} |

 

The following table lists activation functions that are not functions of a single [fold](./Fold_(higher-order_function)) x from the previous layer or layers:

 
| Name | Equation,gi(x→){\displaystyle g_{i}\left({\vec {x}}\right)} | Derivatives,∂gi(x→)∂xj{\displaystyle {\frac {\partial g_{i}\left({\vec {x}}\right)}{\partial x_{j}}}} | Range | Order of continuity |
| --- | --- | --- | --- | --- |
| Softmax | exi∑j=1Jexj{\displaystyle {\frac {e^{x_{i}}}{\sum _{j=1}^{J}e^{x_{j}}}}}fori= 1, …,J | gi(x→)(δij−gj(x→)){\displaystyle g_{i}\left({\vec {x}}\right)\left(\delta _{ij}-g_{j}\left({\vec {x}}\right)\right)} | (0,1){\displaystyle (0,1)} | C∞{\displaystyle C^{\infty }} |
| Maxout[25] | maxixi{\displaystyle \max _{i}x_{i}} | {1ifj=argmaxixi0ifj≠argmaxixi{\displaystyle {\begin{cases}1&{\text{if }}j={\underset {i}{\operatorname {argmax} }}\,x_{i}\\0&{\text{if }}j\neq {\underset {i}{\operatorname {argmax} }}\,x_{i}\end{cases}}} | (−∞,∞){\displaystyle (-\infty ,\infty )} | C0{\displaystyle C^{0}} |

 **[^](./Activation_function#ref_kronecker_delta)** Here,      δ δ   i j     {\displaystyle \delta _{ij}}  ![{\displaystyle \delta _{ij}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fa75d04c11480d976e1396951e02cbb3c4f71568) is the [Kronecker delta](./Kronecker_delta). **[^](./Activation_function#ref_j)** For instance,     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0) could be iterating through the number of kernels of the previous neural network layer while     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) iterates through the number of kernels of the current layer. 

### Quantum activation functions

 Main article: [Quantum function](./Quantum_function) 

In [quantum neural networks](./Quantum_neural_networks) programmed on gate-model [quantum computers](./Quantum_computers), based on quantum perceptrons instead of variational quantum circuits, the non-linearity of the activation function can be implemented with no need of measuring the output of each [perceptron](./Perceptron) at each layer. The quantum properties loaded within the circuit such as [superposition](./Quantum_superposition) can be preserved by creating the [Taylor series](./Taylor_series) of the argument computed by the perceptron itself, with suitable quantum circuits computing the powers up to a wanted approximation degree. Because of the flexibility of such quantum circuits, they can be designed in order to approximate any arbitrary classical activation function.[[26]](./Activation_function#cite_note-26)

 

## See also

 
- [Logistic function](./Logistic_function)
- [Rectifier (neural networks)](./Rectifier_(neural_networks))
- [Stability (learning theory)](./Stability_(learning_theory))
- [Softmax function](./Softmax_function)

 

## References

 
1. [↑](./Activation_function#cite_ref-1) Hinkelmann, Knut. ["Neural Networks, p. 7"](https://web.archive.org/web/20181006235506/http://didattica.cs.unicam.it/lib/exe/fetch.php?media=didattica:magistrale:kebi:ay_1718:ke-11_neural_networks.pdf) (PDF). *University of Applied Sciences Northwestern Switzerland*. Archived from [the original](http://didattica.cs.unicam.it/lib/exe/fetch.php?media=didattica:magistrale:kebi:ay_1718:ke-11_neural_networks.pdf) (PDF) on 6 October 2018. Retrieved 6 October 2018.
2. [↑](./Activation_function#cite_ref-2) Hinton, Geoffrey; Deng, Li; Deng, Li; Yu, Dong; Dahl, George; Mohamed, Abdel-rahman; Jaitly, Navdeep; Senior, Andrew; Vanhoucke, Vincent; Nguyen, Patrick; [Sainath, Tara](./Tara_Sainath); Kingsbury, Brian (2012). "Deep Neural Networks for Acoustic Modeling in Speech Recognition". *IEEE Signal Processing Magazine*. **29** (6): 82–97. [doi](./Doi_(identifier)):[10.1109/MSP.2012.2205597](https://doi.org/10.1109%2FMSP.2012.2205597). [S2CID](./S2CID_(identifier)) [206485943](https://api.semanticscholar.org/CorpusID:206485943).
3. [↑](./Activation_function#cite_ref-3) Krizhevsky, Alex; Sutskever, Ilya; Hinton, Geoffrey E. (24 May 2017). ["ImageNet classification with deep convolutional neural networks"](https://dl.acm.org/doi/10.1145/3065386). *Communications of the ACM*. **60** (6): 84–90. [doi](./Doi_(identifier)):[10.1145/3065386](https://doi.org/10.1145%2F3065386). [ISSN](./ISSN_(identifier)) [0001-0782](https://search.worldcat.org/issn/0001-0782).
4. [↑](./Activation_function#cite_ref-4) King Abdulaziz University; Al-johania, Norah; Elrefaei, Lamiaa; Benha University (30 June 2019). ["Dorsal Hand Vein Recognition by Convolutional Neural Networks: Feature Learning and Transfer Learning Approaches"](http://www.inass.org/2019/2019063019.pdf) (PDF). *International Journal of Intelligent Engineering and Systems*. **12** (3): 178–191. [doi](./Doi_(identifier)):[10.22266/ijies2019.0630.19](https://doi.org/10.22266%2Fijies2019.0630.19).
5. [1](./Activation_function#cite_ref-ReferenceA_5-0) [2](./Activation_function#cite_ref-ReferenceA_5-1) [3](./Activation_function#cite_ref-ReferenceA_5-2) Hendrycks, Dan; Gimpel, Kevin (2016). "Gaussian Error Linear Units (GELUs)". [arXiv](./ArXiv_(identifier)):[1606.08415](https://arxiv.org/abs/1606.08415) [[cs.LG](https://arxiv.org/archive/cs.LG)].
6. [↑](./Activation_function#cite_ref-6) [Cybenko, G.](./George_Cybenko) (December 1989). ["Approximation by superpositions of a sigmoidal function"](https://hal.archives-ouvertes.fr/hal-03753170/file/Cybenko1989.pdf) (PDF). *Mathematics of Control, Signals, and Systems*. **2** (4): 303–314. [Bibcode](./Bibcode_(identifier)):[1989MCSS....2..303C](https://ui.adsabs.harvard.edu/abs/1989MCSS....2..303C). [doi](./Doi_(identifier)):[10.1007/BF02551274](https://doi.org/10.1007%2FBF02551274). [ISSN](./ISSN_(identifier)) [0932-4194](https://search.worldcat.org/issn/0932-4194). [S2CID](./S2CID_(identifier)) [3958369](https://api.semanticscholar.org/CorpusID:3958369).
7. [↑](./Activation_function#cite_ref-7) Snyman, Jan (3 March 2005). [*Practical Mathematical Optimization: An Introduction to Basic Optimization Theory and Classical and New Gradient-Based Algorithms*](https://books.google.com/books?id=0tFmf_UKl7oC). Springer Science & Business Media. [ISBN](./ISBN_(identifier)) [978-0-387-24348-1](./Special:BookSources/978-0-387-24348-1).
8. [↑](./Activation_function#cite_ref-8) Krizhevsky, Alex; Sutskever, Ilya; Hinton, Geoffrey E. (24 May 2017). ["ImageNet classification with deep convolutional neural networks"](https://doi.org/10.1145%2F3065386). *Communications of the ACM*. **60** (6): 84–90. [doi](./Doi_(identifier)):[10.1145/3065386](https://doi.org/10.1145%2F3065386). [ISSN](./ISSN_(identifier)) [0001-0782](https://search.worldcat.org/issn/0001-0782). [S2CID](./S2CID_(identifier)) [195908774](https://api.semanticscholar.org/CorpusID:195908774).
9. [↑](./Activation_function#cite_ref-9) Hodgkin, A. L.; Huxley, A. F. (28 August 1952). ["A quantitative description of membrane current and its application to conduction and excitation in nerve"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1392413). *The Journal of Physiology*. **117** (4): 500–544. [doi](./Doi_(identifier)):[10.1113/jphysiol.1952.sp004764](https://doi.org/10.1113%2Fjphysiol.1952.sp004764). [PMC](./PMC_(identifier)) [1392413](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1392413). [PMID](./PMID_(identifier)) [12991237](https://pubmed.ncbi.nlm.nih.gov/12991237).
10. [↑](./Activation_function#cite_ref-10) Gerstein, G. L. (1964). "Representation of firing activity by nerve cell ensembles". *IEEE Transactions on Biomedical Engineering*. **11**: 61–65. [doi](./Doi_(identifier)):[10.1109/TBME.1964.4502244](https://doi.org/10.1109%2FTBME.1964.4502244).
11. [↑](./Activation_function#cite_ref-11) Sitzmann, Vincent; Martel, Julien; Bergman, Alexander; Lindell, David; Wetzstein, Gordon (2020). ["Implicit Neural Representations with Periodic Activation Functions"](https://proceedings.neurips.cc/paper/2020/hash/53c04118df112c13a8c34b38343b9c10-Abstract.html). *Advances in Neural Information Processing Systems*. **33**. Curran Associates, Inc.: 7462–7473. [arXiv](./ArXiv_(identifier)):[2006.09661](https://arxiv.org/abs/2006.09661).
12. [↑](./Activation_function#cite_ref-12) Flake, Gary William (1998), Orr, Genevieve B.; Müller, Klaus-Robert (eds.), ["Square Unit Augmented Radially Extended Multilayer Perceptrons"](https://link.springer.com/chapter/10.1007/3-540-49430-8_8), *Neural Networks: Tricks of the Trade*, Lecture Notes in Computer Science, vol. 1524, Berlin, Heidelberg: Springer, pp. 145–163, [doi](./Doi_(identifier)):[10.1007/3-540-49430-8_8](https://doi.org/10.1007%2F3-540-49430-8_8), [ISBN](./ISBN_(identifier)) [978-3-540-49430-0](./Special:BookSources/978-3-540-49430-0), retrieved 5 October 2024`{{citation}}`:  CS1 maint: work parameter with ISBN ([link](./Category:CS1_maint:_work_parameter_with_ISBN))
13. [↑](./Activation_function#cite_ref-13) Du, Simon; Lee, Jason (3 July 2018). ["On the Power of Over-parametrization in Neural Networks with Quadratic Activation"](https://proceedings.mlr.press/v80/du18a.html). *Proceedings of the 35th International Conference on Machine Learning*. PMLR: 1329–1338. [arXiv](./ArXiv_(identifier)):[1803.01206](https://arxiv.org/abs/1803.01206).
14. [↑](./Activation_function#cite_ref-14) Nair, Vinod; Hinton, Geoffrey E. (2010), ["Rectified Linear Units Improve Restricted Boltzmann Machines"](http://dl.acm.org/citation.cfm?id=3104322.3104425), *27th International Conference on International Conference on Machine Learning*, ICML'10, USA: Omnipress, pp. 807–814, [ISBN](./ISBN_(identifier)) [9781605589077](./Special:BookSources/9781605589077)
15. [↑](./Activation_function#cite_ref-15) Glorot, Xavier; Bordes, Antoine; Bengio, Yoshua (2011). ["Deep sparse rectifier neural networks"](http://proceedings.mlr.press/v15/glorot11a/glorot11a.pdf) (PDF). *International Conference on Artificial Intelligence and Statistics*.
16. [↑](./Activation_function#cite_ref-16) Clevert, Djork-Arné; Unterthiner, Thomas; Hochreiter, Sepp (23 November 2015). "Fast and Accurate Deep Network Learning by Exponential Linear Units (ELUs)". [arXiv](./ArXiv_(identifier)):[1511.07289](https://arxiv.org/abs/1511.07289) [[cs.LG](https://arxiv.org/archive/cs.LG)].
17. [↑](./Activation_function#cite_ref-17) Klambauer, Günter; Unterthiner, Thomas; Mayr, Andreas; Hochreiter, Sepp (8 June 2017). "Self-Normalizing Neural Networks". *Advances in Neural Information Processing Systems*. **30** (2017). [arXiv](./ArXiv_(identifier)):[1706.02515](https://arxiv.org/abs/1706.02515).
18. [↑](./Activation_function#cite_ref-18) Maas, Andrew L.; Hannun, Awni Y.; Ng, Andrew Y. (June 2013). "Rectifier nonlinearities improve neural network acoustic models". *Proc. ICML*. **30** (1). [S2CID](./S2CID_(identifier)) [16489696](https://api.semanticscholar.org/CorpusID:16489696).
19. [↑](./Activation_function#cite_ref-19) He, Kaiming; Zhang, Xiangyu; Ren, Shaoqing; Sun, Jian (6 February 2015). "Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification". [arXiv](./ArXiv_(identifier)):[1502.01852](https://arxiv.org/abs/1502.01852) [[cs.CV](https://arxiv.org/archive/cs.CV)].
20. [↑](./Activation_function#cite_ref-refrepsu1_20-0)  Atto, Abdourrahmane M.; Galichet, Sylvie; Pastor, Dominique; Méger, Nicolas (2023), ["On joint parameterizations of linear and nonlinear functionals in neural networks"](https://doi.org/10.1016/j.neunet.2022.12.019), *Elsevier Pattern Recognition*, vol. 160, pp. 12–21, [arXiv](./ArXiv_(identifier)):[2101.09948](https://arxiv.org/abs/2101.09948), [doi](./Doi_(identifier)):[10.1016/j.neunet.2022.12.019](https://doi.org/10.1016%2Fj.neunet.2022.12.019), [PMID](./PMID_(identifier)) [36592526](https://pubmed.ncbi.nlm.nih.gov/36592526)
21. [↑](./Activation_function#cite_ref-refssbs1_21-0)  Atto, Abdourrahmane M.; Pastor, Dominique; Mercier, Grégoire (2008), ["Smooth sigmoid wavelet shrinkage for non-parametric estimation"](https://hal.archives-ouvertes.fr/hal-02136546/file/ICASSP_ATTO_2008.pdf) (PDF), *[2008 IEEE International Conference on Acoustics, Speech and Signal Processing](./2008_IEEE_International_Conference_on_Acoustics,_Speech_and_Signal_Processing?action=edit&redlink=1)*, pp. 3265–3268, [doi](./Doi_(identifier)):[10.1109/ICASSP.2008.4518347](https://doi.org/10.1109%2FICASSP.2008.4518347), [ISBN](./ISBN_(identifier)) [978-1-4244-1483-3](./Special:BookSources/978-1-4244-1483-3), [S2CID](./S2CID_(identifier)) [9959057](https://api.semanticscholar.org/CorpusID:9959057)
22. [↑](./Activation_function#cite_ref-22) Elfwing, Stefan; Uchibe, Eiji; Doya, Kenji (2018). "Sigmoid-Weighted Linear Units for Neural Network Function Approximation in Reinforcement Learning". *Neural Networks*. **107**: 3–11. [arXiv](./ArXiv_(identifier)):[1702.03118](https://arxiv.org/abs/1702.03118). [doi](./Doi_(identifier)):[10.1016/j.neunet.2017.12.012](https://doi.org/10.1016%2Fj.neunet.2017.12.012). [PMID](./PMID_(identifier)) [29395652](https://pubmed.ncbi.nlm.nih.gov/29395652). [S2CID](./S2CID_(identifier)) [6940861](https://api.semanticscholar.org/CorpusID:6940861).
23. [↑](./Activation_function#cite_ref-23) Ramachandran, Prajit; Zoph, Barret; Le, Quoc V (2017). "Searching for Activation Functions". [arXiv](./ArXiv_(identifier)):[1710.05941](https://arxiv.org/abs/1710.05941) [[cs.NE](https://arxiv.org/archive/cs.NE)].
24. [↑](./Activation_function#cite_ref-24) Basirat, Mina; Roth, Peter M. (2 August 2018), *The Quest for the Golden Activation Function*, [arXiv](./ArXiv_(identifier)):[1808.00783](https://arxiv.org/abs/1808.00783)
25. [↑](./Activation_function#cite_ref-25) Goodfellow, Ian J.; Warde-Farley, David; Mirza, Mehdi; Courville, Aaron; Bengio, Yoshua (2013). "Maxout Networks". *JMLR Workshop and Conference Proceedings*. **28** (3): 1319–1327. [arXiv](./ArXiv_(identifier)):[1302.4389](https://arxiv.org/abs/1302.4389).
26. [↑](./Activation_function#cite_ref-26) Maronese, Marco; Destri, Claudio; Prati, Enrico (2022). "Quantum activation functions for quantum neural networks". *Quantum Information Processing*. **21** (4): 128. [arXiv](./ArXiv_(identifier)):[2201.03700](https://arxiv.org/abs/2201.03700). [Bibcode](./Bibcode_(identifier)):[2022QuIP...21..128M](https://ui.adsabs.harvard.edu/abs/2022QuIP...21..128M). [doi](./Doi_(identifier)):[10.1007/s11128-022-03466-0](https://doi.org/10.1007%2Fs11128-022-03466-0). [ISSN](./ISSN_(identifier)) [1570-0755](https://search.worldcat.org/issn/1570-0755).

 

## Further reading

 
- Kunc, Vladimír; Kléma, Jiří (14 February 2024), *Three Decades of Activations: A Comprehensive Survey of 400 Activation Functions for Neural Networks*, [arXiv](./ArXiv_(identifier)):[2402.09092](https://arxiv.org/abs/2402.09092)
- Nwankpa, Chigozie; Ijomah, Winifred; Gachagan, Anthony; Marshall, Stephen (8 November 2018). "Activation Functions: Comparison of trends in Practice and Research for Deep Learning". [arXiv](./ArXiv_(identifier)):[1811.03378](https://arxiv.org/abs/1811.03378) [[cs.LG](https://arxiv.org/archive/cs.LG)].
- Dubey, Shiv Ram; Singh, Satish Kumar; Chaudhuri, Bidyut Baran (2022). ["Activation functions in deep learning: A comprehensive survey and benchmark"](https://doi.org/10.1016%2Fj.neucom.2022.06.111). *Neurocomputing*. **503**. Elsevier BV: 92–108. [arXiv](./ArXiv_(identifier)):[2109.14545](https://arxiv.org/abs/2109.14545). [doi](./Doi_(identifier)):[10.1016/j.neucom.2022.06.111](https://doi.org/10.1016%2Fj.neucom.2022.06.111). [ISSN](./ISSN_(identifier)) [0925-2312](https://search.worldcat.org/issn/0925-2312).

 
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