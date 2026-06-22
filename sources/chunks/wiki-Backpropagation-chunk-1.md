---
source: sources/wiki-Backpropagation.md
source_url: https://en.wikipedia.org/wiki/Backpropagation
chunk: 1/5
---

Optimization algorithm for artificial neural networks This article is about the computer algorithm. For the biological process, see [Neural backpropagation](./Neural_backpropagation). Backpropagation can also refer to the way the result of a playout is propagated up the search tree in [Monte Carlo tree search](./Monte_Carlo_tree_search#Principle_of_operation). 
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

 

In [machine learning](./Machine_learning), **backpropagation** is a [gradient](./Gradient) computation method commonly used for training a [neural network](./Neural_network_(machine_learning)) in computing parameter updates.

 

It is an efficient application of the [chain rule](./Chain_rule) to neural networks. Backpropagation efficiently computes the gradient of the loss with respect to the network weights for a single input–output example. It does this by propagating derivatives backward, one layer at a time, from the output layer to the input layer, thereby avoiding redundant chain-rule calculations.

 

Strictly speaking, the term *backpropagation* refers only to an algorithm for efficiently computing the gradient, not how the gradient is used, but the term is often used loosely to refer to the entire learning algorithm. This includes changing model parameters in the negative direction of the gradient, such as by [stochastic gradient descent](./Stochastic_gradient_descent), or as an intermediate step in a more complicated optimizer, such as [Adaptive Moment Estimation](./Stochastic_gradient_descent#Adam).[[1]](./Backpropagation#cite_note-1)

 

Backpropagation had multiple discoveries and partial discoveries, with a tangled history and terminology (see [§ History](./Backpropagation#History)). Some other names for the technique include "reverse mode of [automatic differentiation](./Automatic_differentiation)" or "[reverse accumulation](./Reverse_accumulation)".[[2]](./Backpropagation#cite_note-DL-reverse-mode-2)

 

## Overview

 

Backpropagation computes the gradient in [weight space](./Parameter_space) of a feedforward neural network, with respect to a [loss function](./Loss_function). Denote:

 
-     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4): input (vector of features)
-     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d): target output
For classification, output will be a vector of class probabilities (e.g.,     ( 0.1 , 0.7 , 0.2 )   {\displaystyle (0.1,0.7,0.2)}  ![{\displaystyle (0.1,0.7,0.2)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fbb2f54392fb76b6dea26425e24447bf2c48cc94), and target output is a specific class, encoded by the [one-hot](./One-hot)/[dummy variable](./Dummy_variable_(statistics)) (e.g.,     ( 0 , 1 , 0 )   {\displaystyle (0,1,0)}  ![{\displaystyle (0,1,0)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3e28bfe8a44d06939011e3ba2159e894c0f22f23)).
-     C   {\displaystyle C}  ![{\displaystyle C}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fc55753007cd3c18576f7933f6f089196732029): [loss function](./Loss_function) or "cost function"[[a]](./Backpropagation#cite_note-3) For classification, this is usually [cross-entropy](./Cross-entropy) (XC, [log loss](./Log_loss)), while for regression it is usually [squared error loss](./Squared_error_loss) (SEL).
-     L   {\displaystyle L}  ![{\displaystyle L}](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8): the number of layers
-      W  l   = (  w  j k   l   )   {\displaystyle W^{l}=(w_{jk}^{l})}  ![{\displaystyle W^{l}=(w_{jk}^{l})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6ef80d37cec97e026476841a0e20f9b35c402bd0): the weights between layer     l − −  1   {\displaystyle l-1}  ![{\displaystyle l-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4e0d448948a353d0b2469b88ca918f34e32c8752) and     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac), where      w  j k   l     {\displaystyle w_{jk}^{l}}  ![{\displaystyle w_{jk}^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8f47c5a00989f34da7a6cde720321223af36a019) is the weight between the     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40)-th node in layer     l − −  1   {\displaystyle l-1}  ![{\displaystyle l-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4e0d448948a353d0b2469b88ca918f34e32c8752) and the     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0)-th node in layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac)[[b]](./Backpropagation#cite_note-4)
-      f  l     {\displaystyle f^{l}}  ![{\displaystyle f^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ee0e6c373d37a6a029890630310cf35ba6acd174): [activation functions](./Activation_function) at layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) For classification the last layer is usually the [logistic function](./Logistic_function) for binary classification, and [softmax](./Softmax_function) (softargmax) for multi-class classification, while for the hidden layers this was traditionally a [sigmoid function](./Sigmoid_function) (logistic function or others) on each node (coordinate), but today is more varied, with [rectifier](./Rectifier_(neural_networks)) ([ramp](./Ramp_function), [ReLU](./ReLU)) being common.
-      a  j   l     {\displaystyle a_{j}^{l}}  ![{\displaystyle a_{j}^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fbb8152a0d8674023edebc1a8760c3ef478831d8): activation of the     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0)-th node in layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac).

 

In the derivation of backpropagation, other intermediate quantities are used by introducing them as needed below. Bias terms are not treated specially since they correspond to a weight with a fixed input of 1. For backpropagation the specific loss function and activation functions do not matter as long as they and their derivatives can be evaluated efficiently. Traditional activation functions include [sigmoid](./Sigmoid_function), [tanh](./Tanh), [ReLU](./Rectifier_(neural_networks)), [Swish](./Swish_function),[[3]](./Backpropagation#cite_note-5) [Mish](./Rectifier_(neural_networks)#Mish),[[4]](./Backpropagation#cite_note-6), and many others.

 

The overall network is a combination of [function composition](./Function_composition) and [matrix multiplication](./Matrix_multiplication):

     g ( x ) :=  f  L   (  W  L    f  L − −  1   (  W  L − −  1   ⋯ ⋯   f  1   (  W  1   x ) ⋯ ⋯  ) )   {\displaystyle g(x):=f^{L}(W^{L}f^{L-1}(W^{L-1}\cdots f^{1}(W^{1}x)\cdots ))}  ![{\displaystyle g(x):=f^{L}(W^{L}f^{L-1}(W^{L-1}\cdots f^{1}(W^{1}x)\cdots ))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/110b3c8ee790c91cf79a882f1515f6f05f8db335) 

For a training set there will be a set of input–output pairs,      {  (  x  i   ,  y  i   )  }    {\displaystyle \left\{(x_{i},y_{i})\right\}}  ![{\displaystyle \left\{(x_{i},y_{i})\right\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/26d74b1e662ee0f0e1604f2e5a63fde1456bb19e). For each input–output pair     (  x  i   ,  y  i   )   {\displaystyle (x_{i},y_{i})}  ![{\displaystyle (x_{i},y_{i})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d6dbb919b91ccacf17ed47898048428a1baf9703) in the training set, the loss of the model on that pair is the cost of the difference between the predicted output     g (  x  i   )   {\displaystyle g(x_{i})}  ![{\displaystyle g(x_{i})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3badcf4ca3e9414821942baee2851b8f9bd27294) and the target output      y  i     {\displaystyle y_{i}}  ![{\displaystyle y_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/67d30d30b6c2dbe4d6f150d699de040937ecc95f):

     C (  y  i   , g (  x  i   ) )   {\displaystyle C(y_{i},g(x_{i}))}  ![{\displaystyle C(y_{i},g(x_{i}))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/57cd91c74155873ce3e1df0fab12d13e7a8f335f) 

Note the distinction: during model evaluation the weights are fixed while the inputs vary (and the target output may be unknown), and the network ends with the output layer (it does not include the loss function). During model training the input–output pair is fixed while the weights vary, and the network ends with the loss function.

 

Backpropagation computes the gradient for a *fixed* input–output pair     (  x  i   ,  y  i   )   {\displaystyle (x_{i},y_{i})}  ![{\displaystyle (x_{i},y_{i})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d6dbb919b91ccacf17ed47898048428a1baf9703), where the weights      w  j k   l     {\displaystyle w_{jk}^{l}}  ![{\displaystyle w_{jk}^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8f47c5a00989f34da7a6cde720321223af36a019) can vary. Each individual component of the gradient,     ∂ ∂  C  /  ∂ ∂   w  j k   l   ,   {\displaystyle \partial C/\partial w_{jk}^{l},}  ![{\displaystyle \partial C/\partial w_{jk}^{l},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/924218a6182ed0f43094ec9f5d8a66c4b9b9026f) can be computed by the chain rule; but doing this separately for each weight is inefficient. Backpropagation efficiently computes the gradient by avoiding duplicate calculations and not computing unnecessary intermediate values, by computing the gradient of each layer – specifically the gradient of the weighted *input* of each layer, denoted by      δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d) – from back to front.

 

Informally, the key point is that since the only way a weight in      W  l     {\displaystyle W^{l}}  ![{\displaystyle W^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/60b87bc8138a82f110491bb1abd0ea6eefe84c22) affects the loss is through its effect on the *next* layer, and it does so *linearly*,      δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d) are the only data you need to compute the gradients of the weights at layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac), and then the gradients of weights of previous layer can be computed by      δ δ   l − −  1     {\displaystyle \delta ^{l-1}}  ![{\displaystyle \delta ^{l-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e4ff3faf90011d3ed813a4ac2fe31904765e2963) and repeated recursively. This avoids inefficiency in two ways. First, it avoids duplication because when computing the gradient at layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac), it is unnecessary to recompute all derivatives on later layers     l + 1 , l + 2 , … …    {\displaystyle l+1,l+2,\ldots }  ![{\displaystyle l+1,l+2,\ldots }](https://wikimedia.org/api/rest_v1/media/math/render/svg/49f721be70a4213a6196f3d14f58eb5844eebb1a) each time. Second, it avoids unnecessary intermediate calculations, because at each stage it directly computes the gradient of the weights with respect to the ultimate output (the loss), rather than unnecessarily computing the derivatives of the values of hidden layers with respect to changes in weights     ∂ ∂   a   j ′     l ′     /  ∂ ∂   w  j k   l     {\displaystyle \partial a_{j'}^{l'}/\partial w_{jk}^{l}}  ![{\displaystyle \partial a_{j'}^{l'}/\partial w_{jk}^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/67e885d69c5968ab173f51222b89d0701b3459d6).

 

Backpropagation can be expressed for simple feedforward networks in terms of [matrix multiplication](./Backpropagation#Matrix_multiplication), or more generally in terms of the [adjoint graph](./Backpropagation#Adjoint_graph).

 

## Matrix multiplication

 

For the basic case of a feedforward network, where nodes in each layer are connected only to nodes in the immediate next layer (without skipping any layers), and there is a loss function that computes a scalar loss for the final output, backpropagation can be understood simply by matrix multiplication.[[c]](./Backpropagation#cite_note-7) Essentially, backpropagation evaluates the expression for the derivative of the cost function as a product of derivatives between each layer *from right to left* – "backwards" – with the gradient of the weights between each layer being a simple modification of the partial products (the "backwards propagated error").

 

Given an input–output pair     ( x , y )   {\displaystyle (x,y)}  ![{\displaystyle (x,y)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/41cf50e4a314ca8e2c30964baa8d26e5be7a9386), the loss is:

     C ( y ,  f  L   (  W  L    f  L − −  1   (  W  L − −  1   ⋯ ⋯   f  2   (  W  2    f  1   (  W  1   x ) ) ⋯ ⋯  ) ) )   {\displaystyle C(y,f^{L}(W^{L}f^{L-1}(W^{L-1}\cdots f^{2}(W^{2}f^{1}(W^{1}x))\cdots )))}  ![{\displaystyle C(y,f^{L}(W^{L}f^{L-1}(W^{L-1}\cdots f^{2}(W^{2}f^{1}(W^{1}x))\cdots )))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3ca8768a6ab49c9e52086741f958221b56b6d03e) 

To compute this, one starts with the input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) and works forward; denote the weighted input of each hidden layer as      z  l     {\displaystyle z^{l}}  ![{\displaystyle z^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3ea4d56d1c5e8fe66b402ea0d1b92368902531dd) and the output of hidden layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) as the activation      a  l     {\displaystyle a^{l}}  ![{\displaystyle a^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/975d9aa9ed78016e94e7438c5af2a6ec8b97a0e9). For backpropagation, the activation      a  l     {\displaystyle a^{l}}  ![{\displaystyle a^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/975d9aa9ed78016e94e7438c5af2a6ec8b97a0e9) as well as the derivatives     (  f  l    ) ′    {\displaystyle (f^{l})'}  ![{\displaystyle (f^{l})'}](https://wikimedia.org/api/rest_v1/media/math/render/svg/75a2f054b20672fb790ed501c4a39873233d4745) (evaluated at      z  l     {\displaystyle z^{l}}  ![{\displaystyle z^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3ea4d56d1c5e8fe66b402ea0d1b92368902531dd)) must be cached for use during the backwards pass.

 

The derivative of the loss in terms of the inputs is given by the chain rule; note that each term is a [total derivative](./Total_derivative), evaluated at the value of the network (at each node) on the input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4):

        d C   d  a  L      ⋅ ⋅     d  a  L     d  z  L      ⋅ ⋅     d  z  L     d  a  L − −  1      ⋅ ⋅     d  a  L − −  1     d  z  L − −  1      ⋅ ⋅     d  z  L − −  1     d  a  L − −  2      ⋅ ⋅  … …  ⋅ ⋅     d  a  1     d  z  1      ⋅ ⋅     ∂ ∂   z  1     ∂ ∂  x    ,   {\displaystyle {\frac {dC}{da^{L}}}\cdot {\frac {da^{L}}{dz^{L}}}\cdot {\frac {dz^{L}}{da^{L-1}}}\cdot {\frac {da^{L-1}}{dz^{L-1}}}\cdot {\frac {dz^{L-1}}{da^{L-2}}}\cdot \ldots \cdot {\frac {da^{1}}{dz^{1}}}\cdot {\frac {\partial z^{1}}{\partial x}},}  ![{\displaystyle {\frac {dC}{da^{L}}}\cdot {\frac {da^{L}}{dz^{L}}}\cdot {\frac {dz^{L}}{da^{L-1}}}\cdot {\frac {da^{L-1}}{dz^{L-1}}}\cdot {\frac {dz^{L-1}}{da^{L-2}}}\cdot \ldots \cdot {\frac {da^{1}}{dz^{1}}}\cdot {\frac {\partial z^{1}}{\partial x}},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b758730620b9e4d0b2018f99c3cc270fa8e3bd31) 

where        d  a  L     d  z  L        {\displaystyle {\frac {da^{L}}{dz^{L}}}}  ![{\displaystyle {\frac {da^{L}}{dz^{L}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e72728161114c81bdf209852a4157264296326fb) is a [diagonal matrix](./Diagonal_matrix).

 

These terms are: the derivative of the loss function;[[d]](./Backpropagation#cite_note-8) the derivatives of the activation functions;[[e]](./Backpropagation#cite_note-9) and the matrices of weights:[[f]](./Backpropagation#cite_note-10)

        d C   d  a  L      ∘ ∘  (  f  L    ) ′  ⋅ ⋅   W  L   ∘ ∘  (  f  L − −  1    ) ′  ⋅ ⋅   W  L − −  1   ∘ ∘  ⋯ ⋯  ∘ ∘  (  f  1    ) ′  ⋅ ⋅   W  1   .   {\displaystyle {\frac {dC}{da^{L}}}\circ (f^{L})'\cdot W^{L}\circ (f^{L-1})'\cdot W^{L-1}\circ \cdots \circ (f^{1})'\cdot W^{1}.}  ![{\displaystyle {\frac {dC}{da^{L}}}\circ (f^{L})'\cdot W^{L}\circ (f^{L-1})'\cdot W^{L-1}\circ \cdots \circ (f^{1})'\cdot W^{1}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f46ed48b7054ef8629f889782c3ffbf953818ca) 

The gradient     ∇ ∇    {\displaystyle \nabla }  ![{\displaystyle \nabla }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a3d0e93b78c50237f9ea83d027e4ebbdaef354b2) is the [transpose](./Transpose) of the derivative of the output in terms of the input, so the matrices are transposed and the order of multiplication is reversed, but the entries are the same:

      ∇ ∇   x   C = (  W  1    )  T   ⋅ ⋅  (  f  1    ) ′  ∘ ∘  … …  ∘ ∘  (  W  L − −  1    )  T   ⋅ ⋅  (  f  L − −  1    ) ′  ∘ ∘  (  W  L    )  T   ⋅ ⋅  (  f  L    ) ′  ∘ ∘   ∇ ∇    a  L     C .   {\displaystyle \nabla _{x}C=(W^{1})^{T}\cdot (f^{1})'\circ \ldots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C.}  ![{\displaystyle \nabla _{x}C=(W^{1})^{T}\cdot (f^{1})'\circ \ldots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6ef269aa176ce5488ce5f6038eebcb9c8fe3c728) 

Backpropagation then consists essentially of evaluating this expression from right to left (equivalently, multiplying the previous expression for the derivative from left to right), computing the gradient at each layer on the way; there is an added step, because the gradient of the weights is not just a subexpression: there's an extra multiplication.

 

Introducing the auxiliary quantity      δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d) for the partial products (multiplying from right to left), interpreted as the "error at level     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac)" and defined as the gradient of the input values at level     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac):

      δ δ   l   := (  f  l    ) ′  ∘ ∘  (  W  l + 1    )  T   ⋅ ⋅  (  f  l + 1    ) ′  ∘ ∘  ⋯ ⋯  ∘ ∘  (  W  L − −  1    )  T   ⋅ ⋅  (  f  L − −  1    ) ′  ∘ ∘  (  W  L    )  T   ⋅ ⋅  (  f  L    ) ′  ∘ ∘   ∇ ∇    a  L     C .   {\displaystyle \delta ^{l}:=(f^{l})'\circ (W^{l+1})^{T}\cdot (f^{l+1})'\circ \cdots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C.}  ![{\displaystyle \delta ^{l}:=(f^{l})'\circ (W^{l+1})^{T}\cdot (f^{l+1})'\circ \cdots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/85f95e97ceff3617728642e31c4090869970cad9) 

Note that      δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d) is a vector, of length equal to the number of nodes in level     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac); each component is interpreted as the "cost attributable to (the value of) that node".

 

The gradient of the weights in layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) is then:

      ∇ ∇    W  l     C =  δ δ   l   (  a  l − −  1    )  T   .   {\displaystyle \nabla _{W^{l}}C=\delta ^{l}(a^{l-1})^{T}.}  ![{\displaystyle \nabla _{W^{l}}C=\delta ^{l}(a^{l-1})^{T}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ef23e829ba87604d15ab01965708906c2baa1e4d) 

The factor of      a  l − −  1     {\displaystyle a^{l-1}}  ![{\displaystyle a^{l-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a66d0e6ecb4f486f7e1b63c6ae0a91448624163) is because the weights      W  l     {\displaystyle W^{l}}  ![{\displaystyle W^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/60b87bc8138a82f110491bb1abd0ea6eefe84c22) between level     l − −  1   {\displaystyle l-1}  ![{\displaystyle l-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4e0d448948a353d0b2469b88ca918f34e32c8752) and     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) affect level     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) proportionally to the inputs (activations): the inputs are fixed, the weights vary.

 

The      δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d) can easily be computed recursively, going from right to left, as:

      δ δ   l − −  1   := (  f  l − −  1    ) ′  ∘ ∘  (  W  l    )  T   ⋅ ⋅   δ δ   l   .   {\displaystyle \delta ^{l-1}:=(f^{l-1})'\circ (W^{l})^{T}\cdot \delta ^{l}.}  ![{\displaystyle \delta ^{l-1}:=(f^{l-1})'\circ (W^{l})^{T}\cdot \delta ^{l}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/16ccb3d3b717f3fa8e1aa72c3a46bbc70945e4cf) 

The gradients of the weights can thus be computed using a few matrix multiplications for each level; this is backpropagation.

 

Compared with naively computing forwards (using the      δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d) for illustration):

          δ δ   1      = (  f  1    ) ′  ∘ ∘  (  W  2    )  T   ⋅ ⋅  (  f  2    ) ′  ∘ ∘  ⋯ ⋯  ∘ ∘  (  W  L − −  1    )  T   ⋅ ⋅  (  f  L − −  1    ) ′  ∘ ∘  (  W  L    )  T   ⋅ ⋅  (  f  L    ) ′  ∘ ∘   ∇ ∇    a  L     C      δ δ   2      = (  f  2    ) ′  ∘ ∘  ⋯ ⋯  ∘ ∘  (  W  L − −  1    )  T   ⋅ ⋅  (  f  L − −  1    ) ′  ∘ ∘  (  W  L    )  T   ⋅ ⋅  (  f  L    ) ′  ∘ ∘   ∇ ∇    a  L     C       ⋮ ⋮       δ δ   L − −  1      = (  f  L − −  1    ) ′  ∘ ∘  (  W  L    )  T   ⋅ ⋅  (  f  L    ) ′  ∘ ∘   ∇ ∇    a  L     C      δ δ   L      = (  f  L    ) ′  ∘ ∘   ∇ ∇    a  L     C ,       {\displaystyle {\begin{aligned}\delta ^{1}&=(f^{1})'\circ (W^{2})^{T}\cdot (f^{2})'\circ \cdots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C\\\delta ^{2}&=(f^{2})'\circ \cdots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C\\&\vdots \\\delta ^{L-1}&=(f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C\\\delta ^{L}&=(f^{L})'\circ \nabla _{a^{L}}C,\end{aligned}}}  ![{\displaystyle {\begin{aligned}\delta ^{1}&=(f^{1})'\circ (W^{2})^{T}\cdot (f^{2})'\circ \cdots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C\\\delta ^{2}&=(f^{2})'\circ \cdots \circ (W^{L-1})^{T}\cdot (f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C\\&\vdots \\\delta ^{L-1}&=(f^{L-1})'\circ (W^{L})^{T}\cdot (f^{L})'\circ \nabla _{a^{L}}C\\\delta ^{L}&=(f^{L})'\circ \nabla _{a^{L}}C,\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65693d61321a41ee6a79f9e24e944f581a33240a) 

There are two key differences with backpropagation:

 
1. Computing      δ δ   l − −  1     {\displaystyle \delta ^{l-1}}  ![{\displaystyle \delta ^{l-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e4ff3faf90011d3ed813a4ac2fe31904765e2963) in terms of      δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d) avoids the obvious duplicate multiplication of layers     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) and beyond.
2. Multiplying starting from      ∇ ∇    a  L     C   {\displaystyle \nabla _{a^{L}}C}  ![{\displaystyle \nabla _{a^{L}}C}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a3491216364a8fe84026d9f114a9477be761c2c) – propagating the error *backwards* – means that each step simply multiplies a vector (     δ δ   l     {\displaystyle \delta ^{l}}  ![{\displaystyle \delta ^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/249b787ef6af0149f7d71b951651c43633e0d56d)) by the matrices of weights     (  W  l    )  T     {\displaystyle (W^{l})^{T}}  ![{\displaystyle (W^{l})^{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/95ded7046a67e4ea5039c86405383ff82c74308e) and derivatives of activations     (  f  l − −  1    ) ′    {\displaystyle (f^{l-1})'}  ![{\displaystyle (f^{l-1})'}](https://wikimedia.org/api/rest_v1/media/math/render/svg/89d6b56875a57b50369e097a55fe50f1be7b9aaf). By contrast, multiplying forwards, starting from the changes at an earlier layer, means that each multiplication multiplies a *matrix* by a *matrix*. This is much more expensive, and corresponds to tracking every possible path of a change in one layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) forward to changes in the layer     l + 2   {\displaystyle l+2}  ![{\displaystyle l+2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f96df20468aecf3a1b6dfedd08982cb6edc489bb) (for multiplying      W  l + 1     {\displaystyle W^{l+1}}  ![{\displaystyle W^{l+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d3f3b2ac57d2c95e81aafd230d2065e8f8cc401) by      W  l + 2     {\displaystyle W^{l+2}}  ![{\displaystyle W^{l+2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74caba7e74227959403a15dfc8041720dae8817d), with additional multiplications for the derivatives of the activations), which unnecessarily computes the intermediate quantities of how weight changes affect the values of hidden nodes.

 


