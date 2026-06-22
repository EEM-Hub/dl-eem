---
source: sources/wiki-Recurrent_neural_network.md
source_url: https://en.wikipedia.org/wiki/Recurrent_neural_network
chunk: 2/5
---

## Architectures

 

### Fully recurrent

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/44/Hopfield-net-vector.svg/250px-Hopfield-net-vector.svg.png)](./File:Hopfield-net-vector.svg)A fully connected RNN with 4 neurons 

**Fully recurrent neural networks** (FRNN) connect the outputs of all neurons to the inputs of all neurons. In other words, it is a [fully connected network](./Fully_connected_network). This is the most general neural network topology, because all other topologies can be represented by setting some connection weights to zero to simulate the lack of connections between those neurons.

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/0/02/RNN_architecture.png/250px-RNN_architecture.png)](./File:RNN_architecture.png)A simple Elman network where      σ σ   h   = tanh ,  σ σ   y   =  Identity    {\displaystyle \sigma _{h}=\tanh ,\sigma _{y}={\text{Identity}}}  ![{\displaystyle \sigma _{h}=\tanh ,\sigma _{y}={\text{Identity}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/02121b05b248e1d48a45e75052bc4e5144c8bde7) 

### Hopfield

 Main article: [Hopfield network](./Hopfield_network) 

The **Hopfield network** is an RNN in which all connections across layers are equally sized. It requires [stationary](./Stationary_process) inputs and is thus not a general RNN, as it does not process sequences of patterns. However, it guarantees that it will converge. If the connections are trained using [Hebbian learning](./Hebbian_learning), then the Hopfield network can perform as [robust](./Robustness_(computer_science)) [content-addressable memory](./Content-addressable_memory), resistant to connection alteration.

 

### Elman networks and Jordan networks

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Elman_srnn.png/250px-Elman_srnn.png)](./File:Elman_srnn.png)The Elman network 

An **[Elman](./Jeff_Elman) network** is a three-layer network (arranged horizontally as *x*, *y*, and *z* in the illustration) with the addition of a set of context units (*u* in the illustration). The middle (hidden) layer is connected to these context units fixed with a weight of one.[[51]](./Recurrent_neural_network#cite_note-bmm615-51) At each time step, the input is fed forward and a [learning rule](./Learning_rule) is applied. The fixed back-connections save a copy of the previous values of the hidden units in the context units (since they propagate over the connections before the learning rule is applied). Thus the network can maintain a sort of state, allowing it to perform tasks such as sequence-prediction that are beyond the power of a standard [multilayer perceptron](./Multilayer_perceptron).

 

**[Jordan](./Michael_I._Jordan) networks** are similar to Elman networks. The context units are fed from the output layer instead of the hidden layer. The context units in a Jordan network are also called the state layer. They have a recurrent connection to themselves.[[51]](./Recurrent_neural_network#cite_note-bmm615-51)

 

Elman and Jordan networks are also known as "Simple recurrent networks" (SRN).

 Elman network[[52]](./Recurrent_neural_network#cite_note-52)          h  t      =  σ σ   h   (  W  h    x  t   +  U  h    h  t − −  1   +  b  h   )      y  t      =  σ σ   y   (  W  y    h  t   +  b  y   )       {\displaystyle {\begin{aligned}h_{t}&=\sigma _{h}(W_{h}x_{t}+U_{h}h_{t-1}+b_{h})\\y_{t}&=\sigma _{y}(W_{y}h_{t}+b_{y})\end{aligned}}}  ![{\displaystyle {\begin{aligned}h_{t}&=\sigma _{h}(W_{h}x_{t}+U_{h}h_{t-1}+b_{h})\\y_{t}&=\sigma _{y}(W_{y}h_{t}+b_{y})\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/983c33bfddb6c6d8b1bfdf9accf50bb5634e2f5a) Jordan network[[53]](./Recurrent_neural_network#cite_note-53)          h  t      =  σ σ   h   (  W  h    x  t   +  U  h    s  t   +  b  h   )      y  t      =  σ σ   y   (  W  y    h  t   +  b  y   )      s  t      =  σ σ   s   (  W  s , s    s  t − −  1   +  W  s , y    y  t − −  1   +  b  s   )       {\displaystyle {\begin{aligned}h_{t}&=\sigma _{h}(W_{h}x_{t}+U_{h}s_{t}+b_{h})\\y_{t}&=\sigma _{y}(W_{y}h_{t}+b_{y})\\s_{t}&=\sigma _{s}(W_{s,s}s_{t-1}+W_{s,y}y_{t-1}+b_{s})\end{aligned}}}  ![{\displaystyle {\begin{aligned}h_{t}&=\sigma _{h}(W_{h}x_{t}+U_{h}s_{t}+b_{h})\\y_{t}&=\sigma _{y}(W_{y}h_{t}+b_{y})\\s_{t}&=\sigma _{s}(W_{s,s}s_{t-1}+W_{s,y}y_{t-1}+b_{s})\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/da448ff637dcc68dbd497e10f7623c76c265b983) 

Variables and functions

 
-      x  t     {\displaystyle x_{t}}  ![{\displaystyle x_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f279a30bc8eabc788f3fe81c9cfb674e72e858db): input vector
-      h  t     {\displaystyle h_{t}}  ![{\displaystyle h_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e8dbf3d8bfe322f68ff6400385578f8d78e1ba7c): hidden layer vector
-      s  t     {\displaystyle s_{t}}  ![{\displaystyle s_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92a402d151a0173378ee252a634c77898ebe4b06): "state" vector,
-      y  t     {\displaystyle y_{t}}  ![{\displaystyle y_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0fe9554452b93508c9d2479414a45981ecc75a2d): output vector
-     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7),     U   {\displaystyle U}  ![{\displaystyle U}](https://wikimedia.org/api/rest_v1/media/math/render/svg/458a728f53b9a0274f059cd695e067c430956025) and     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3): parameter matrices and vector
-     σ σ    {\displaystyle \sigma }  ![{\displaystyle \sigma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/59f59b7c3e6fdb1d0365a494b81fb9a696138c36): [Activation functions](./Activation_function)

 

### Long short-term memory

 Main article: [Long short-term memory](./Long_short-term_memory) [![](//upload.wikimedia.org/wikipedia/commons/thumb/6/63/Long_Short-Term_Memory.svg/250px-Long_Short-Term_Memory.svg.png)](./File:Long_Short-Term_Memory.svg)Long short-term memory unit 

**Long short-term memory** (LSTM) is the most widely used RNN architecture. It was designed to solve the [vanishing gradient problem](./Vanishing_gradient_problem). LSTM is normally augmented by recurrent gates called "forget gates".[[54]](./Recurrent_neural_network#cite_note-gers2002-54) LSTM prevents backpropagated errors from vanishing or exploding.[[55]](./Recurrent_neural_network#cite_note-hochreiter1991-55) Instead, errors can flow backward through unlimited numbers of virtual layers unfolded in space. That is, LSTM can learn tasks that require memories of events that happened thousands or even millions of discrete time steps earlier. Problem-specific LSTM-like topologies can be evolved.[[56]](./Recurrent_neural_network#cite_note-bayer2009-56) LSTM works even given long delays between significant events and can handle signals that mix low and high-frequency components.

 

Many applications use stacks of LSTMs,[[57]](./Recurrent_neural_network#cite_note-fernandez2007-57) for which it is called "deep LSTM". LSTM can learn to recognize [context-sensitive languages](./Context-sensitive_languages) unlike previous models based on [hidden Markov models](./Hidden_Markov_model) (HMM) and similar concepts.[[58]](./Recurrent_neural_network#cite_note-peepholeLSTM-58)

 

### Gated recurrent unit

 Main article: [Gated recurrent unit](./Gated_recurrent_unit) [![](//upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Gated_Recurrent_Unit.svg/250px-Gated_Recurrent_Unit.svg.png)](./File:Gated_Recurrent_Unit.svg)Gated recurrent unit 

**Gated recurrent unit** (GRU), introduced in 2014, was designed as a simplification of LSTM. They are used in the full form and several further simplified variants.[[59]](./Recurrent_neural_network#cite_note-59)[[60]](./Recurrent_neural_network#cite_note-60) They have fewer parameters than LSTM, as they lack an output gate.[[61]](./Recurrent_neural_network#cite_note-MyUser_Wildml.com_May_18_2016c-61)

 

Their performance on polyphonic music modeling and speech signal modeling was found to be similar to that of long short-term memory.[[62]](./Recurrent_neural_network#cite_note-MyUser_Arxiv.org_May_18_2016c2-62) There does not appear to be particular performance difference between LSTM and GRU.[[62]](./Recurrent_neural_network#cite_note-MyUser_Arxiv.org_May_18_2016c2-62)[[63]](./Recurrent_neural_network#cite_note-gruber_jockisch-63)

 

#### Bidirectional associative memory

 Main article: [Bidirectional associative memory](./Bidirectional_associative_memory) 

Introduced by [Bart Kosko](./Bart_Kosko),[[64]](./Recurrent_neural_network#cite_note-64) a bidirectional associative memory (BAM) network is a variant of a Hopfield network that stores associative data as a vector. The bidirectionality comes from passing information through a matrix and its [transpose](./Transpose). Typically, [bipolar encoding](./Bipolar_encoding) is preferred to binary encoding of the associative pairs. Recently, stochastic BAM models using [Markov](./Markov_chain) stepping are optimized for increased network stability and relevance to real-world applications.[[65]](./Recurrent_neural_network#cite_note-65)

 

A BAM network has two layers, either of which can be driven as an input to recall an association and produce an output on the other layer.[[66]](./Recurrent_neural_network#cite_note-66)

 

### Echo state

 Main article: [Echo state network](./Echo_state_network) 

[**Echo state networks**](./Echo_state_network) (ESN) have a sparsely connected random hidden layer. The weights of output neurons are the only part of the network that can change (be trained). ESNs are good at reproducing certain [time series](./Time_series).[[67]](./Recurrent_neural_network#cite_note-67) A variant for [spiking neurons](./Spiking_neural_network) is known as a [liquid state machine](./Liquid_state_machine).[[68]](./Recurrent_neural_network#cite_note-68)

 

### Recursive

 Main article: [Recursive neural network](./Recursive_neural_network) 

A **[recursive neural network](./Recursive_neural_network)**[[69]](./Recurrent_neural_network#cite_note-69) is created by applying the same set of weights [recursively](./Recursion) over a differentiable graph-like structure by traversing the structure in [topological order](./Topological_sort). Such networks are typically also trained by the reverse mode of [automatic differentiation](./Automatic_differentiation).[[70]](./Recurrent_neural_network#cite_note-lin1970-70)[[71]](./Recurrent_neural_network#cite_note-grie2008-71) They can process [distributed representations](./Distributed_representation) of structure, such as [logical terms](./Mathematical_logic). A special case of recursive neural networks is the RNN whose structure corresponds to a linear chain. Recursive neural networks have been applied to [natural language processing](./Natural_language_processing).[[72]](./Recurrent_neural_network#cite_note-72) The *recursive neural tensor network* uses a [tensor](./Tensor)-based composition function for all nodes in the tree.[[73]](./Recurrent_neural_network#cite_note-73)

 

### Neural Turing machines

 Main articles: [Neural Turing machine](./Neural_Turing_machine) and [Differentiable neural computer](./Differentiable_neural_computer) 

**Neural Turing machines** (NTMs) are a method of extending recurrent neural networks by coupling them to external [memory](./Memory) resources with which they interact. The combined system is analogous to a [Turing machine](./Turing_machine) or [Von Neumann architecture](./Von_Neumann_architecture) but is [differentiable](./Differentiable_neural_computer) end-to-end, allowing it to be efficiently trained with [gradient descent](./Gradient_descent).[[74]](./Recurrent_neural_network#cite_note-74)

 

**Differentiable neural computers** (DNCs) are an extension of neural Turing machines, allowing for the usage of fuzzy amounts of each memory address and a record of chronology.[[75]](./Recurrent_neural_network#cite_note-DNCnature2016-75)

 

**Neural network pushdown automata** (NNPDA) are similar to NTMs, but tapes are replaced by analog stacks that are differentiable and trained. In this way, they are similar in complexity to recognizers of [context free grammars](./Context_free_grammar) (CFGs).[[76]](./Recurrent_neural_network#cite_note-76)

 

Recurrent neural networks are [Turing complete](./Turing_complete) and can run arbitrary programs to process arbitrary sequences of inputs.[[77]](./Recurrent_neural_network#cite_note-77)

 

## Training

 

### Teacher forcing

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/72/Seq2seq_RNN_encoder-decoder_with_attention_mechanism%2C_training_and_inferring.png/250px-Seq2seq_RNN_encoder-decoder_with_attention_mechanism%2C_training_and_inferring.png)](./File:Seq2seq_RNN_encoder-decoder_with_attention_mechanism,_training_and_inferring.png)Encoder-decoder RNN without attention mechanism. Teacher forcing is shown in red.

An RNN can be trained into a conditionally [generative model](./Generative_model) of sequences, aka **autoregression**.

 

Concretely, let us consider the problem of machine translation, that is, given a sequence     (  x  1   ,  x  2   , … …  ,  x  n   )   {\displaystyle (x_{1},x_{2},\dots ,x_{n})}  ![{\displaystyle (x_{1},x_{2},\dots ,x_{n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7c0e6a4f6008f01547bb5cc1e8b01207272939e9) of English words, the model is to produce a sequence     (  y  1   , … …  ,  y  m   )   {\displaystyle (y_{1},\dots ,y_{m})}  ![{\displaystyle (y_{1},\dots ,y_{m})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1f788b82def8d7a3933ae95cc81463bde894ae57) of French words. It is to be solved by a [seq2seq](./Seq2seq) model.

 

Now, during training, the encoder half of the model would first ingest     (  x  1   ,  x  2   , … …  ,  x  n   )   {\displaystyle (x_{1},x_{2},\dots ,x_{n})}  ![{\displaystyle (x_{1},x_{2},\dots ,x_{n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7c0e6a4f6008f01547bb5cc1e8b01207272939e9), then the decoder half would start generating a sequence     (     y ^ ^      1   ,     y ^ ^      2   , … …  ,     y ^ ^      l   )   {\displaystyle ({\hat {y}}_{1},{\hat {y}}_{2},\dots ,{\hat {y}}_{l})}  ![{\displaystyle ({\hat {y}}_{1},{\hat {y}}_{2},\dots ,{\hat {y}}_{l})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1c690f99611b8115d603410038d1c900eb099b69). The problem is that if the model makes a mistake early on, say at         y ^ ^      2     {\displaystyle {\hat {y}}_{2}}  ![{\displaystyle {\hat {y}}_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d678e9549266e3dfc09066e1145e3f7a13fd7d2), then subsequent tokens are likely to also be mistakes. This makes it inefficient for the model to obtain a learning signal, since the model would mostly learn to shift         y ^ ^      2     {\displaystyle {\hat {y}}_{2}}  ![{\displaystyle {\hat {y}}_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2d678e9549266e3dfc09066e1145e3f7a13fd7d2) towards      y  2     {\displaystyle y_{2}}  ![{\displaystyle y_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7377c7399e662562cd420fa5c7ce49cfba574998), but not the others.

 

**Teacher forcing** makes it so that the decoder uses the correct output sequence for generating the next entry in the sequence. So for example, it would see     (  y  1   , … …  ,  y  k   )   {\displaystyle (y_{1},\dots ,y_{k})}  ![{\displaystyle (y_{1},\dots ,y_{k})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06fbc6292b20008e7ee5b70877d89c445b81f6d5) in order to generate         y ^ ^      k + 1     {\displaystyle {\hat {y}}_{k+1}}  ![{\displaystyle {\hat {y}}_{k+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a1af03c401fbfdd242dd870b01707b2d946b0d68).

 

### Gradient descent

 Main articles: [Gradient descent](./Gradient_descent) and [Vanishing gradient problem](./Vanishing_gradient_problem) 

Gradient descent is a [first-order](./Category:First_order_methods) [iterative](./Iterative_algorithm) [optimization](./Mathematical_optimization) [algorithm](./Algorithm) for finding the minimum of a function. In neural networks, it can be used to minimize the error term by changing each weight in proportion to the derivative of the error with respect to that weight, provided the non-linear [activation functions](./Activation_function) are [differentiable](./Differentiable_function).

 

The standard method for training RNN by gradient descent is the "[backpropagation through time](./Backpropagation_through_time)" (BPTT) algorithm, which is a special case of the general algorithm of [backpropagation](./Backpropagation). A more computationally expensive online variant is called "Real-Time Recurrent Learning" or RTRL,[[78]](./Recurrent_neural_network#cite_note-78)[[79]](./Recurrent_neural_network#cite_note-79) which is an instance of [automatic differentiation](./Automatic_differentiation) in the forward accumulation mode with stacked tangent vectors. Unlike BPTT, this algorithm is [local](./Local_algorithm) in time but not local in space.

 

In this context, local in space means that a unit's weight vector can be updated using only information stored in the connected units and the unit itself such that update complexity of a single unit is linear in the dimensionality of the weight vector. Local in time means that the updates take place continually (on-line) and depend only on the most recent time step rather than on multiple time steps within a given time horizon as in BPTT. Biological neural networks appear to be local with respect to both time and space.[[80]](./Recurrent_neural_network#cite_note-80)[[81]](./Recurrent_neural_network#cite_note-PríncipeEuliano2000-81)

 

For recursively computing the partial derivatives, RTRL has a time-complexity of O(number of hidden x number of weights) per time step for computing the [Jacobian matrices](./Jacobian_matrix), while BPTT only takes O(number of weights) per time step, at the cost of storing all forward activations within the given time horizon.[[82]](./Recurrent_neural_network#cite_note-Ollivier2015-82) An online hybrid between BPTT and RTRL with intermediate complexity exists,[[83]](./Recurrent_neural_network#cite_note-83)[[84]](./Recurrent_neural_network#cite_note-84) along with variants for continuous time.[[85]](./Recurrent_neural_network#cite_note-85)

 

A major problem with gradient descent for standard RNN architectures is that [error gradients vanish](./Vanishing_gradient_problem) exponentially quickly with the size of the time lag between important events.[[55]](./Recurrent_neural_network#cite_note-hochreiter1991-55)[[86]](./Recurrent_neural_network#cite_note-HOCH2001-86) LSTM combined with a BPTT/RTRL hybrid learning method attempts to overcome these problems.[[36]](./Recurrent_neural_network#cite_note-lstm-36) This problem is also solved in the independently recurrent neural network (IndRNN)[[87]](./Recurrent_neural_network#cite_note-auto-87) by reducing the context of a neuron to its own past state and the cross-neuron information can then be explored in the following layers. Memories of different ranges including long-term memory can be learned without the gradient vanishing and exploding problems.

 

The [online algorithm](./Online_algorithm) called **causal recursive backpropagation** (CRBP), implements and combines BPTT and RTRL paradigms for locally recurrent networks.[[88]](./Recurrent_neural_network#cite_note-88) It works with the most general locally recurrent networks. The CRBP algorithm can minimize the global error term. This fact improves the stability of the algorithm, providing a unifying view of gradient calculation techniques for recurrent networks with local feedback.

 

One approach to gradient information computation in RNNs with arbitrary architectures is based on signal-flow graphs diagrammatic derivation.[[89]](./Recurrent_neural_network#cite_note-89) It uses the BPTT batch algorithm, based on Lee's theorem for network sensitivity calculations.[[90]](./Recurrent_neural_network#cite_note-ReferenceA-90) It was proposed by Wan and Beaufays, while its fast online version was proposed by Campolucci, Uncini and Piazza.[[90]](./Recurrent_neural_network#cite_note-ReferenceA-90)

 

### Connectionist temporal classification

 

The [connectionist temporal classification](./Connectionist_temporal_classification) (CTC)[[91]](./Recurrent_neural_network#cite_note-graves2006-91) is a specialized loss function for training RNNs for sequence modeling problems where the timing is variable.[[92]](./Recurrent_neural_network#cite_note-92)

 

### Global optimization methods

 

Training the weights in a neural network can be modeled as a non-linear [global optimization](./Global_optimization) problem. A target function can be formed to evaluate the fitness or error of a particular weight vector as follows: First, the weights in the network are set according to the weight vector. Next, the network is evaluated against the training sequence. Typically, the sum-squared difference between the predictions and the target values specified in the training sequence is used to represent the error of the current weight vector. Arbitrary global optimization techniques may then be used to minimize this target function.

 

The most common global optimization method for training RNNs is [genetic algorithms](./Genetic_algorithm), especially in unstructured networks.[[93]](./Recurrent_neural_network#cite_note-93)[[94]](./Recurrent_neural_network#cite_note-94)[[95]](./Recurrent_neural_network#cite_note-95)

 

Initially, the genetic algorithm is encoded with the neural network weights in a predefined manner where one gene in the [chromosome](./Chromosome_(genetic_algorithm)) represents one weight link. The whole network is represented as a single chromosome. The fitness function is evaluated as follows:

 
- Each weight encoded in the chromosome is assigned to the respective weight link of the network.
- The training set is presented to the network which propagates the input signals forward.
- The mean-squared error is returned to the fitness function.
- This function drives the genetic selection process.

 

Many chromosomes make up the population; therefore, many different neural networks are evolved until a stopping criterion is satisfied. A common stopping scheme can be: 

 
- When the neural network has learned a certain percentage of the training data.
- When the minimum value of the mean-squared-error is satisfied.
- When the maximum number of training generations has been reached.

 

The fitness function evaluates the stopping criterion as it receives the mean-squared error reciprocal from each network during training. Therefore, the goal of the genetic algorithm is to maximize the fitness function, reducing the mean-squared error.

 

Other global (and/or evolutionary) optimization techniques may be used to seek a good set of weights, such as [simulated annealing](./Simulated_annealing) or [particle swarm optimization](./Particle_swarm_optimization).

 


