---
source: sources/wiki-Artificial_neural_network.md
source_url: https://en.wikipedia.org/wiki/Artificial_neural_network
chunk: 3/7
---

## Elements

 
|  | This sectionmay beconfusing or unclearto readers.Please helpclarify the section. There might be a discussion about this onthe talk page.(April 2017)(Learn how and when to remove this message) |
| --- | --- |

Further information: [Mathematics of artificial neural networks](./Mathematics_of_artificial_neural_networks) [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/44/Neuron3.png/250px-Neuron3.png)](./File:Neuron3.png)Neuron and myelinated axon, with signal flow from inputs at dendrites to outputs at axon terminals 

NNs began as an attempt to replicate the architecture of the brain in the digital realm. NNs immediately showed promise for handling non-linear relationships, but encountered obstacles. Models soon reoriented to applying mathematical insights to improve empirical results, at the expense of biological fidelity. 

 

### Neuron

 [![Artificial neuron structure](//upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Artificial_neuron_structure.svg/330px-Artificial_neuron_structure.svg.png)](./File:Artificial_neuron_structure.svg)Structure of an artificial neuron 

NNs are composed of [digital neurons](./Artificial_neurons), conceptually derived from biological [neurons](./Neuron). Each neuron has one or more numerical inputs and produces a single numerical output.[[111]](./Neural_network_(machine_learning)#cite_note-Abbod20072-111) An input (e.g., an image) is typically parceled across the set of input neurons (each getting a piece of the image). Each neuron's inputs, [weighted](./Weight_function) by the weights of the connections from each of those inputs are summed. A bias term is added to this sum.[[112]](./Neural_network_(machine_learning)#cite_note-DAWSON19982-112)) The result is then passed through a nonlinear [activation function](./Activation_function) to produce the neuron's output. Small enough outputs may be zeroed out (ignored).[[113]](./Neural_network_(machine_learning)#cite_note-:52-113)[[114]](./Neural_network_(machine_learning)#cite_note-114)[[115]](./Neural_network_(machine_learning)#cite_note-115)

 

### Network

 

NNs connect neurons to each other, using the output of some neurons as the input of others, akin to biological [axon](./Axoneme)-[synapse](./Synapse)-[dendrite](./Matrix_(protocol)) connections.[[116]](./Neural_network_(machine_learning)#cite_note-Winston2-116) The network forms a [directed](./Directed_graph), [weighted graph](./Weighted_graph). The weights apply to both the graph's the nodes and edges.[[117]](./Neural_network_(machine_learning)#cite_note-Zell1994ch5.22-117)

 

Nodes are arranged in layers, with the bottom layers directly addressing raw data, while the top layers reveal the final results. Intermediate layers gradually increase the level of abstraction, so what began as for example, pixels in an image, gradually resolves into things such as object boundaries, and then into real-world objects such as letters and faces.[[117]](./Neural_network_(machine_learning)#cite_note-Zell1994ch5.22-117)[[113]](./Neural_network_(machine_learning)#cite_note-:52-113) Single layer and unlayered networks are also used.[*[citation needed](./Wikipedia:Citation_needed)*]

[![](//upload.wikimedia.org/wikipedia/commons/thumb/1/15/Neural_Network.svg/250px-Neural_Network.svg.png)](./File:Neural_Network.svg)Structure of a feedforward neural network with four layers 

Multiple connection patterns have been used. Traditionally, they are *fully connected*, with every neuron in one layer connecting to every neuron in the next layer.[[118]](./Neural_network_(machine_learning)#cite_note-118) However, in [convolutional neural networks](./Convolutional_neural_network), some layers are *convolutional,* meaning each neuron in one layer is connected to a subset of neurons in the previous layer, such as those representing one section of an image.[[119]](./Neural_network_(machine_learning)#cite_note-flexible2-119)[[120]](./Neural_network_(machine_learning)#cite_note-120)[*[clarification needed](./Wikipedia:Please_clarify)*]

 

In most neural networks,[*[citation needed](./Wikipedia:Citation_needed)*] the outputs of the neurons in one layer are connected only to neurons in the immediately  following layer ([directed acyclic graph](./Directed_acyclic_graph)), meaning information only flows forward from one layer to the next. These are known as [feedforward networks](./Feedforward_neural_network).[[121]](./Neural_network_(machine_learning)#cite_note-Zell1994p732-121) In contrast, networks that allow connections between neurons in the same or previous layers are known as [recurrent networks](./Recurrent_neural_network).[[122]](./Neural_network_(machine_learning)#cite_note-122)

 

## Learning

 
|  | This section includes alist of references,related reading, orexternal links,but its sources remain unclear because it lacksinline citations.Please helpimprovethis section byintroducingmore precise citations.(August 2019)(Learn how and when to remove this message) |
| --- | --- |

See also: [Mathematical optimization](./Mathematical_optimization), [Estimation theory](./Estimation_theory), and [Machine learning](./Machine_learning) 

Training/learning involves adjusting the weights of the network to improve the accuracy of the result. NNs typically require vast numbers of sample inputs (far more than biological brains) to achieve a given level of function. This is done by minimizing the observed errors among sample observations. Training takes place before a network is deployed, and (unlike brains) does not continue thereafter. Instead, the network may be retrained from scratch as more sample data becomes available.

 

[Empirical risk minimization](./Empirical_risk_minimization) adjusts node and link weights to minimize the difference (empirical risk), between the predicted output and the known values in the training samples.[[123]](./Neural_network_(machine_learning)#cite_note-:23-123) A defined [loss function](./Loss_functions_for_classification) measures the degree of error.[[92]](./Neural_network_(machine_learning)#cite_note-:42-92) [Backpropagation](./Backpropagation) spreads the error (adjusts the weights) from the output nodes across the network to the input nodes.[[123]](./Neural_network_(machine_learning)#cite_note-:23-123) The intent is to allow the network to process data that is not included in the training samples.

 

As long as the value of the loss function (its cost) continues to decline, the network is continuing to improve. The function typically produces a [statistic](./Statistic) whose value is only approximate. When the cost is low, the difference between the output (*e.g.* almost certainly a cat) and the correct answer (a cat) is small. Most learning models can be viewed as a straightforward application of [optimization](./Mathematical_optimization) theory and [statistical estimation](./Statistical_estimation).[[117]](./Neural_network_(machine_learning)#cite_note-Zell1994ch5.22-117)[[124]](./Neural_network_(machine_learning)#cite_note-124)

 

Learning typically ends when additional observations do not usefully reduce the cost. The cost typically approaches, but does not reach, 0. If no feasible amount of sample data yields a low cost, training is labeled a failure.

 

### Loss function

 
|  | This sectionneeds expansionwith: Talk more about how loss functions are described, what types exist for different problems. You can help byadding missing information.(March 2026) |
| --- | --- |

 

While it is possible to assess a loss function [ad hoc](./Ad_hoc), typically it must exhibit desirable properties such as [convexity](./Convex_function), [differentiability](./Differentiable_function), and [robustness](./Robustness_(computer_science)).[[125]](./Neural_network_(machine_learning)#cite_note-125) In a probabilistic model, the model's [posterior probability](./Posterior_probability) can be used as an inverse cost (higher values are better).[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Backpropagation

 Main article: [Backpropagation](./Backpropagation) 

Backpropagation is a method used to adjust the connection weights to compensate for errors found during learning. The error amount is essentially divided among the connections. Technically, backpropagation calculates the [gradient](./Gradient) (the derivative) of the [loss function](./Loss_function) associated with a given state with respect to the weights. The weight updates can be done via [stochastic gradient descent](./Stochastic_gradient_descent) or other methods, such as *[extreme learning machines](./Extreme_learning_machine)*,[[126]](./Neural_network_(machine_learning)#cite_note-126) "no-prop" networks,[[127]](./Neural_network_(machine_learning)#cite_note-127) training without backtracking,[[128]](./Neural_network_(machine_learning)#cite_note-128) "weightless" networks,[[129]](./Neural_network_(machine_learning)#cite_note-RBMTRAIN2-129) and [non-connectionist neural networks](./Holographic_associative_memory).[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Hyperparameters

 Main article: [Hyperparameter (machine learning)](./Hyperparameter_(machine_learning)) 

A [hyperparameter](./Hyperparameter_(machine_learning)) is a [parameter](./Parameter) defining any configurable part of the network and learning process whose value is set prior to training.[[130]](./Neural_network_(machine_learning)#cite_note-130) Examples of hyperparameters include [learning rate](./Learning_rate), sample batch size, number of nodes and layers, etc .[[131]](./Neural_network_(machine_learning)#cite_note-131) The performance of a neural network is strongly influenced by hyperparameter choices, and thus may be adjusted during training (typically between training runs), a process called hyperparameter tuning or hyperparameter optimization.[[132]](./Neural_network_(machine_learning)#cite_note-132)

 

#### Learning rate

 Main article: [Learning rate](./Learning_rate) 

The learning rate defines the size of the corrective steps that the model takes to adjust for errors in each observation.[[133]](./Neural_network_(machine_learning)#cite_note-133) A high learning rate shortens training time, but with lower ultimate accuracy, while a lower learning rate takes longer, but with the potential for greater accuracy. Optimizations such as [quickprop](./Quickprop) are primarily aimed at accelerating learning. In order to avoid [oscillations](./Oscillation) such as connection weights that cycle between high and low values, and to improve the rate of convergence, refinements use an [adaptive learning rate](./Adaptive_learning_rate) that increases or decreases as appropriate.[[134]](./Neural_network_(machine_learning)#cite_note-134) The concept of momentum allows the balance between the gradient and the previous change to be weighted such that the weight adjustment depends to some degree on the previous change. A momentum close to 0 emphasizes the gradient, while a value close to 1 emphasizes the last change.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Learning paradigms

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(May 2026)(Learn how and when to remove this message) |
| --- | --- |

 

Machine learning has involved a variety of approaches to training models, including [supervised learning](./Supervised_learning),[[135]](./Neural_network_(machine_learning)#cite_note-135) [unsupervised learning](./Unsupervised_learning),[[136]](./Neural_network_(machine_learning)#cite_note-136) [reinforcement learning](./Reinforcement_learning),[[137]](./Neural_network_(machine_learning)#cite_note-137) and [self-supervised learning](./Self-supervised_learning).

 

#### Supervised learning

 

[Supervised learning](./Supervised_learning) pairs inputs and desired outputs. The learning task is to produce the desired output for each input. In this case, the cost is related to eliminating incorrect outputs.[[138]](./Neural_network_(machine_learning)#cite_note-138) A commonly used cost is the [mean-squared error](./Mean-squared_error), which tries to minimize the average squared error between the network's output and the desired output. Tasks suited for supervised learning include [pattern recognition](./Pattern_recognition) (classification) and [regression](./Regression_analysis) (function approximation). Supervised learning is applicable to sequential data (e.g., for handwriting, speech and [gesture recognition](./Gesture_recognition)). This can be thought of as learning with a "teacher", in the form of a function that provides continuous feedback.

 

#### Unsupervised learning

 

In [unsupervised learning](./Unsupervised_learning), input data is given along with the cost function for the data      x    {\displaystyle \textstyle x}  ![{\displaystyle \textstyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1bd1c9e87a24e459706fa8e63b9e5d94db4540b4) and the output, without an "answer sheet". The cost function is dependent on the task (the model domain) and reflects *[a priori](./A_priori_and_a_posteriori)* assumptions (implicit model properties, its parameters and the observed variables). For example, the model      f ( x ) = a    {\displaystyle \textstyle f(x)=a}  ![{\displaystyle \textstyle f(x)=a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a0e4cc2a7c5c4f65d59b669d64c7759623c648c5) treats      a    {\displaystyle \textstyle a}  ![{\displaystyle \textstyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7abc4e8a2ef67ff9b7ad050afa4cf286c3ec0cd3) is a constant and the cost      C = E [ ( x − −  f ( x )  )  2   ]    {\displaystyle \textstyle C=E[(x-f(x))^{2}]}  ![{\displaystyle \textstyle C=E[(x-f(x))^{2}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2929ecb1606fdfeaddc55477d9671e11c034e21c). Minimizing this cost produces a value of      a    {\displaystyle \textstyle a}  ![{\displaystyle \textstyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7abc4e8a2ef67ff9b7ad050afa4cf286c3ec0cd3) that is equal to the mean of the data. The cost function can be much more complicated. Its form depends on the application: for example, in [compression](./Data_compression) it could be related to the [mutual information](./Mutual_information) between      x    {\displaystyle \textstyle x}  ![{\displaystyle \textstyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1bd1c9e87a24e459706fa8e63b9e5d94db4540b4) and      f ( x )    {\displaystyle \textstyle f(x)}  ![{\displaystyle \textstyle f(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e0fa998ae55408f7f94d08ee08a04fcf92330878), whereas in statistical modeling, it could be related to the [posterior probability](./Posterior_probability) (in both examples, those quantities are maximized). Unsupervised learning is typically applied to [estimation](./Approximation) problems; applications include [clustering](./Data_clustering), the estimation of [statistical distributions](./Statistical_distributions), [compression](./Data_compression), and [filtering](./Bayesian_spam_filtering).

 

#### Self-supervised learning

 These paragraphs are an excerpt from [Self-supervised learning](./Self-supervised_learning).[[edit](https://en.wikipedia.org/w/index.php?title=Self-supervised_learning&action=edit)] 

[Self-supervised learning](./Self-supervised_learning) (SSL) is a paradigm in [machine learning](./Machine_learning) where a model is trained on a task using the data itself to generate supervisory signals, rather than relying on externally-provided labels. In the context of neural networks, self-supervised learning aims to leverage inherent structures or relationships within the input data to create meaningful training signals. SSL tasks are designed so that solving them requires capturing essential [features](./Feature_(machine_learning)) or relationships in the data. The input data is typically augmented or transformed in a way that creates pairs of related samples, where one sample serves as the input, and the other is used to formulate the supervisory signal. This augmentation can involve introducing noise, cropping, rotation, or other transformations. Self-supervised learning more closely imitates the way humans learn to classify objects.[[139]](./Neural_network_(machine_learning)#cite_note-Self-supervised_learning_auto3-139)

 

During SSL, the model learns in two steps. First, the task is solved based on an auxiliary or pretext classification task using pseudo-labels, which help to initialize the model [parameters](./Parameter#Artificial_intelligence).[[140]](./Neural_network_(machine_learning)#cite_note-140)[[141]](./Neural_network_(machine_learning)#cite_note-Self-supervised_learning_auto1-141) Next, the actual task is performed with [supervised](./Supervised_learning) or [unsupervised learning](./Unsupervised_learning).[[142]](./Neural_network_(machine_learning)#cite_note-142)[[143]](./Neural_network_(machine_learning)#cite_note-143)[[144]](./Neural_network_(machine_learning)#cite_note-144)

 

Self-supervised learning has produced promising results in recent years, and has found practical application in fields such as [audio processing](./Audio_signal_processing), and is being used by [Facebook](./Facebook) and others for [speech recognition](./Speech_recognition).[[145]](./Neural_network_(machine_learning)#cite_note-Self-supervised_learning_auto-145)

   

#### Reinforcement learning

 Main article: [Reinforcement learning](./Reinforcement_learning) See also: [Stochastic control](./Stochastic_control) 

In applications such as playing video games, an actor takes a string of actions, receiving a generally unpredictable response from the environment (the game) after each one. The goal is to win the game (get the highest score). The cost is the inverse of the score. In reinforcement learning, the aim is to weight the network to increase the score. After each action the game generates an observation and an [instantaneous](./Instant) cost, according to its rules. The rules and the long-term cost  can only be estimated. At any juncture, the agent decides whether to explore new actions to uncover their costs or to exploit prior learning to proceed more quickly.

 

Formally, the environment is modeled as a [Markov decision process](./Markov_decision_process) (MDP) with states        s  1   , . . . ,  s  n    ∈ ∈  S    {\displaystyle \textstyle {s_{1},...,s_{n}}\in S}  ![{\displaystyle \textstyle {s_{1},...,s_{n}}\in S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/594ab196af08f0326623318ae24ea08359f03c2f) and actions        a  1   , . . . ,  a  m    ∈ ∈  A    {\displaystyle \textstyle {a_{1},...,a_{m}}\in A}  ![{\displaystyle \textstyle {a_{1},...,a_{m}}\in A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c1a2b52db3ad57568da895b2171c90ae6e0de377). Because the state transitions (policies) are not known, [probability distributions](./Probability_distributions) are used instead: the instantaneous cost distribution      P (  c  t    |   s  t   )    {\displaystyle \textstyle P(c_{t}|s_{t})}  ![{\displaystyle \textstyle P(c_{t}|s_{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d64a75ad0caf0be43f971b53a2c16b637bf8bb20), the observation distribution      P (  x  t    |   s  t   )    {\displaystyle \textstyle P(x_{t}|s_{t})}  ![{\displaystyle \textstyle P(x_{t}|s_{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/591cc95a2eb71b92b0fc200675bc8037094a37f0) and the transition distribution      P (  s  t + 1    |   s  t   ,  a  t   )    {\displaystyle \textstyle P(s_{t+1}|s_{t},a_{t})}  ![{\displaystyle \textstyle P(s_{t+1}|s_{t},a_{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0200f5e1c5ad6c6114027fd0f660399c8b584d71), while a policy is defined as the conditional distribution over actions given the observations. Taken together, the two define a [Markov chain](./Markov_chain) (MC). The aim is to discover the lowest-cost MC.

 

NNs serve as the learning component.[[146]](./Neural_network_(machine_learning)#cite_note-146)[[147]](./Neural_network_(machine_learning)#cite_note-147) [Dynamic programming](./Dynamic_programming) coupled with NNs (giving [neurodynamic](./Neural_oscillation) programming)[[148]](./Neural_network_(machine_learning)#cite_note-148) has been applied to problems such as [vehicle routing](./Vehicle_routing),[[149]](./Neural_network_(machine_learning)#cite_note-149) video games, [natural resource management](./Natural_resource_management)[[150]](./Neural_network_(machine_learning)#cite_note-150)[[151]](./Neural_network_(machine_learning)#cite_note-151) and [medicine](./Medicine)[[152]](./Neural_network_(machine_learning)#cite_note-152) because of NNs' ability to mitigate cost even when reducing the [discretization](./Discretization) grid density for numerically approximating control tasks.

 

#### Self-learning

 

Self-learning was introduced in 1982 along with a *crossbar adaptive array* (CAA) NN that could teach itself.[[153]](./Neural_network_(machine_learning)#cite_note-153) It is a system with only one input, situation s, and only one output, action (or behavior) a. It has neither external advice input nor external reinforcement from the environment. The CAA computes, in a crossbar fashion, both decisions about actions and emotions (feelings) about encountered situations. The system is driven by the interaction between cognition and emotion.[[154]](./Neural_network_(machine_learning)#cite_note-154) Given the memory matrix, W =||w(a,s)||, the crossbar self-learning algorithm in each iteration performs the following computation:

 
```
 In situation s perform action a;
 Receive consequence situation s';
 Compute emotion of being in consequence situation v(s');
 Update crossbar memory w'(a,s) = w(a,s) + v(s').
```
 

The backpropagated value (secondary reinforcement) is the emotion toward the consequence situation. The CAA exists in two environments, its behavioral environment, and its genetic environment, from which it receives initial emotions (only once) about to be encountered situations in the behavioral environment. Having received the genome vector (species vector) from the genetic environment, the CAA will learn a goal-seeking behavior, in the behavioral environment that contains both desirable and undesirable situations.[[155]](./Neural_network_(machine_learning)#cite_note-155)

 

#### Neuroevolution

 Main article: [Neuroevolution](./Neuroevolution) 

Neuroevolution can create NN topologies and weights using [evolutionary computation](./Evolutionary_computation). It is competitive with gradient descent approaches.[[156]](./Neural_network_(machine_learning)#cite_note-156)[[157]](./Neural_network_(machine_learning)#cite_note-157) Neuroevolution may be less prone to get caught in "dead ends".[[158]](./Neural_network_(machine_learning)#cite_note-158)

 

### Stochastic neural network

 

**Stochastic neural networks** originating from [Sherrington–Kirkpatrick models](./Spin_glass#Sherrington–Kirkpatrick_model) are a type of neural network built by introducing random variations into the network, either by giving neurons [stochastic](./Stochastic_process) transfer functions,[[159]](./Neural_network_(machine_learning)#cite_note-Ackley19852-159) or by giving them stochastic weights. This makes them useful tools for [optimization](./Optimization_(mathematics)) problems, since the random fluctuations help the network escape from [local minima](./Maxima_and_minima).[[160]](./Neural_network_(machine_learning)#cite_note-160) Stochastic neural networks trained using a [Bayesian](./Bayes'_theorem) approach are known as Bayesian neural networks.[[161]](./Neural_network_(machine_learning)#cite_note-161)

 

### Topological deep learning

 

[Topological deep learning](./Topological_deep_learning), introduced in 2017,[[162]](./Neural_network_(machine_learning)#cite_note-162) integrates topology with deep neural networks to address high-order data. Initially rooted in [algebraic topology](./Algebraic_topology), TDL evolved into a versatile framework incorporating tools from mathematical disciplines such as [differential topology](./Differential_topology) and [geometric topology](./Geometric_topology). 

 

### Other

 

In a [Bayesian](./Bayesian_probability) framework, a distribution over the set of allowed models is chosen to minimize cost. [Evolutionary methods](./Evolutionary_methods),[[163]](./Neural_network_(machine_learning)#cite_note-163) [gene expression programming](./Gene_expression_programming),[[164]](./Neural_network_(machine_learning)#cite_note-164) [simulated annealing](./Simulated_annealing),[[165]](./Neural_network_(machine_learning)#cite_note-165) [expectation–maximization](./Expectation–maximization_algorithm), [non-parametric methods](./Non-parametric_methods) and [particle swarm optimization](./Particle_swarm_optimization)[[166]](./Neural_network_(machine_learning)#cite_note-166) are other learning algorithms. Convergent recursion is a learning algorithm for [cerebellar model articulation controller](./Cerebellar_model_articulation_controller) (CMAC) neural networks.[[167]](./Neural_network_(machine_learning)#cite_note-Qin12-167)[[168]](./Neural_network_(machine_learning)#cite_note-Qin22-168)

 

#### Modes

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(May 2026)(Learn how and when to remove this message) |
| --- | --- |

 

Learning can be either stochastic or batch. Stochastic learning creates a weight adjustment for each sample. In batch learning, weights are adjusted based on a batch of inputs, accumulating errors over the batch. Stochastic learning introduces "noise" into the process, using the local gradient calculated from one data point; this reduces the chance of the network getting stuck in local minima. However, batch learning typically yields a faster, more stable descent to a local minimum, since each update is performed in the direction of the batch's average error. A common compromise is to use "mini-batches", small batches with samples in each batch selected stochastically from the entire data set.

 

## Types

 This section is an excerpt from [Types of artificial neural networks](./Types_of_artificial_neural_networks).[[edit](https://en.wikipedia.org/w/index.php?title=Types_of_artificial_neural_networks&action=edit)] 

[Types of neural networks](./Types_of_artificial_neural_networks) (NN) include a family of techniques. The simplest types have static components, including number of units, number of layers, unit weights and [topology](./Topology). Dynamic NNs evolve via learning. Some types allow/require learning to be "supervised" by the operator, while others operate independently. Some types operate purely in hardware, while others are purely software and run on general purpose computers.

 

The main types are:

 
- [Transformers](./Transformer_(deep_learning)): these use [attention](./Attention_(machine_learning)) to analyze every token in the input stream against every other token in the stream. That technique has enabled neural networks to reach the general public via chatbots, code generators and many other forms.
- [Convolutional neural networks](./Convolutional_neural_networks) (CNN): a FNN that uses kernels and regularization to evade problems in prior generations of NNs. They are typically used to analyze visual and other two-dimensional data.[[169]](./Neural_network_(machine_learning)#cite_note-169)[[170]](./Neural_network_(machine_learning)#cite_note-Types_of_artificial_neural_networks_lecun2016slides2-170)
- [Generative adversarial networks](./Generative_adversarial_network) set networks (of varying structure) against each other, each trying to push the other(s) to produce better results such as winning a game[[171]](./Neural_network_(machine_learning)#cite_note-Types_of_artificial_neural_networks_preprint2-171) or to deceive the opponent about the authenticity of an input.[[172]](./Neural_network_(machine_learning)#cite_note-Types_of_artificial_neural_networks_GANnips2-172) 

  

## Network design

 

The choice of model depends on the data and the application. Models that work well with textual data are typically not the best choice for image data, etc. An important element is which training/learning the model uses.[[173]](./Neural_network_(machine_learning)#cite_note-173)

 

[Neural architecture search](./Neural_architecture_search) (NAS) uses machine learning to automate NN design. NAS has yielded networks that compare well with hand-designed systems. The basic algorithm is to propose a candidate model, evaluate it against a dataset, and use the results as feedback to teach the NAS network.[[174]](./Neural_network_(machine_learning)#cite_note-174) Efforts include [AutoML](./Automated_machine_learning) and AutoKeras.[[175]](./Neural_network_(machine_learning)#cite_note-175) [scikit-learn library](./Scikit-learn) provides functions to help with building a deep network from scratch. 

 

Hyperparameters are design choices (they are not learned).[[176]](./Neural_network_(machine_learning)#cite_note-abs1502.021272-176)

 


