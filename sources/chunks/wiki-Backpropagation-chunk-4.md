---
source: sources/wiki-Backpropagation.md
source_url: https://en.wikipedia.org/wiki/Backpropagation
chunk: 4/5
---

## Loss function

 Further information: [Loss function](./Loss_function) 

The loss function is a function that maps values of one or more variables onto a [real number](./Real_number) intuitively representing some "cost" associated with those values. For backpropagation, the loss function calculates the difference between the network output and its expected output, after a training example has propagated through the network.

 

### Assumptions

 

The mathematical expression of the loss function must fulfill two conditions in order for it to be possibly used in backpropagation.[[9]](./Backpropagation#cite_note-18) The first is that it can be written as an average     E =   1 n    ∑ ∑   x    E  x     {\textstyle E={\frac {1}{n}}\sum _{x}E_{x}}  ![{\textstyle E={\frac {1}{n}}\sum _{x}E_{x}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/10d86f4c725f4158341b538f99eacc618e640b78) over error functions      E  x     {\textstyle E_{x}}  ![{\textstyle E_{x}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fa289d8c2030c92095fe10836f648984bd80d10b), for     n   {\textstyle n}  ![{\textstyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc6e1f880981346a604257ebcacdef24c0aca2d6) individual training examples,     x   {\textstyle x}  ![{\textstyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d951e0f3b54b6a3d73bb9a0a005749046cbce781). The reason for this assumption is that the backpropagation algorithm calculates the gradient of the error function for a single training example, which needs to be generalized to the overall error function. The second assumption is that it can be written as a function of the outputs from the neural network.

 

### Example loss function

 

Let     y ,  y ′    {\displaystyle y,y'}  ![{\displaystyle y,y'}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b7de53e950ff33763c8d524e32280498ec480f86) be vectors in       R   n     {\displaystyle \mathbb {R} ^{n}}  ![{\displaystyle \mathbb {R} ^{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c510b63578322050121fe966f2e5770bea43308d).

 

Select an error function     E ( y ,  y ′  )   {\displaystyle E(y,y')}  ![{\displaystyle E(y,y')}](https://wikimedia.org/api/rest_v1/media/math/render/svg/15c4c7f9edb4d4a5ca9844bfb82f947363d0d40f) measuring the difference between two outputs. The standard choice is the square of the [Euclidean distance](./Euclidean_distance) between the vectors     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) and      y ′    {\displaystyle y'}  ![{\displaystyle y'}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3a535de94a2183d7130731eab8a83531d7c35c6b):    E ( y ,  y ′  ) =    1 2    ‖ ‖  y − −   y ′   ‖ ‖   2     {\displaystyle E(y,y')={\tfrac {1}{2}}\lVert y-y'\rVert ^{2}}  ![{\displaystyle E(y,y')={\tfrac {1}{2}}\lVert y-y'\rVert ^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/11ae60805a3914707a33ece46b0d46700262e028)The error function over     n   {\textstyle n}  ![{\textstyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc6e1f880981346a604257ebcacdef24c0aca2d6) training examples can then be written as an average of losses over individual examples:    E =   1  2 n     ∑ ∑   x   ‖ ‖  ( y ( x ) − −   y ′  ( x ) )  ‖ ‖   2     {\displaystyle E={\frac {1}{2n}}\sum _{x}\lVert (y(x)-y'(x))\rVert ^{2}}  ![{\displaystyle E={\frac {1}{2n}}\sum _{x}\lVert (y(x)-y'(x))\rVert ^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/774b3a3904cbcc2ea2768491f4df2cf1c041563c)

 

## Limitations

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/1/1e/Extrema_example.svg/250px-Extrema_example.svg.png)](./File:Extrema_example.svg)Gradient descent may find a local minimum instead of the global minimum. 
- Gradient descent with backpropagation is not guaranteed to find the [global minimum](./Maxima_and_minima) of the error function, but only a local minimum; also, it has trouble crossing [plateaus](./Plateau_(mathematics)) in the error function landscape. This issue, caused by the [non-convexity](./Convex_optimization) of error functions in neural networks, was long thought to be a major drawback, but [Yann LeCun](./Yann_LeCun) *et al.* argue that in many practical problems, it is not.[[10]](./Backpropagation#cite_note-19)
- Backpropagation learning does not require normalization of input vectors; however, normalization could improve performance.[[11]](./Backpropagation#cite_note-20)
- Backpropagation requires the derivatives of activation functions to be known at network design time.

 

## History

 See also: [History of perceptron](./Perceptron#History) 

### Precursors

 

Backpropagation had been derived repeatedly, as it is essentially an efficient application of the [chain rule](./Chain_rule) (first written down by [Gottfried Wilhelm Leibniz](./Gottfried_Wilhelm_Leibniz) in 1676)[[12]](./Backpropagation#cite_note-leibniz1676-21)[[13]](./Backpropagation#cite_note-22) to neural networks.

 

The terminology "back-propagating error correction" was introduced in 1962 by [Frank Rosenblatt](./Frank_Rosenblatt), but he did not know how to implement this.[[14]](./Backpropagation#cite_note-23) In any case, he only studied neurons whose outputs were discrete levels, which only had zero derivatives, making backpropagation impossible.

 

Precursors to backpropagation appeared in [optimal control theory](./Optimal_control) since 1950s. [Yann LeCun](./Yann_LeCun) et al credits 1950s work by [Pontryagin](./Lev_Pontryagin) and others in optimal control theory, especially the [adjoint state method](./Adjoint_state_method), for being a continuous-time version of backpropagation.[[15]](./Backpropagation#cite_note-24) [Hecht-Nielsen](./Robert_Hecht-Nielsen)[[16]](./Backpropagation#cite_note-25) credits the [Robbins–Monro algorithm](./Stochastic_approximation) (1951)[[17]](./Backpropagation#cite_note-robbins1951-26) and [Arthur Bryson](./Arthur_E._Bryson) and [Yu-Chi Ho](./Yu-Chi_Ho)'s *Applied Optimal Control* (1969) as presages of backpropagation. Other precursors were [Henry J. Kelley](./Henry_J._Kelley) 1960,[[18]](./Backpropagation#cite_note-kelley1960-27) and [Arthur E. Bryson](./Arthur_E._Bryson) (1961).[[19]](./Backpropagation#cite_note-bryson1961-28) In 1962, [Stuart Dreyfus](./Stuart_Dreyfus) published a simpler derivation based only on the [chain rule](./Chain_rule).[[20]](./Backpropagation#cite_note-29)[[21]](./Backpropagation#cite_note-dreyfus1990-30)[[22]](./Backpropagation#cite_note-31) In 1973, he adapted [parameters](./Parameter) of controllers in proportion to error gradients.[[23]](./Backpropagation#cite_note-dreyfus1973-32) Unlike modern backpropagation, these precursors used standard Jacobian matrix calculations from one stage to the previous one, neither addressing direct links across several stages nor potential additional efficiency gains due to network sparsity.[[24]](./Backpropagation#cite_note-DLhistory-33)

 

The [ADALINE](./ADALINE) (1960) learning algorithm was gradient descent with a squared error loss for a single layer. The first [multilayer perceptron](./Multilayer_perceptron) (MLP) with more than one layer trained by [stochastic gradient descent](./Stochastic_gradient_descent)[[17]](./Backpropagation#cite_note-robbins1951-26) was published in 1967 by [Shun'ichi Amari](./Shun'ichi_Amari).[[25]](./Backpropagation#cite_note-Amari1967-34) The MLP had 5 layers, with 2 learnable layers, and it learned to classify patterns not linearly separable.[[24]](./Backpropagation#cite_note-DLhistory-33)

 

### Modern backpropagation

 

Modern backpropagation was first published by [Seppo Linnainmaa](./Seppo_Linnainmaa) as "reverse mode of [automatic differentiation](./Automatic_differentiation)" (1970)[[26]](./Backpropagation#cite_note-lin1970-35) for discrete connected networks of nested [differentiable](./Differentiable_function) functions.[[27]](./Backpropagation#cite_note-lin1976-36)[[28]](./Backpropagation#cite_note-grie2012-37)[[29]](./Backpropagation#cite_note-grie2008-38)

 

In 1982, [Paul Werbos](./Paul_Werbos) applied backpropagation to MLPs in the way that has become standard.[[30]](./Backpropagation#cite_note-werbos1982-39)[[31]](./Backpropagation#cite_note-werbos1974-40) Werbos described how he developed backpropagation in an interview. In 1971, during his PhD work, he developed backpropagation to mathematicize [Freud](./Sigmund_Freud)'s "flow of psychic energy". He faced repeated difficulty in publishing the work, only managing in 1981.[[32]](./Backpropagation#cite_note-:1-41) He also claimed that "the first practical application of back-propagation was for estimating a dynamic model to predict nationalism and social communications in 1974" by him.[[33]](./Backpropagation#cite_note-42)

 

Around 1982,[[32]](./Backpropagation#cite_note-:1-41): 376  [David E. Rumelhart](./David_E._Rumelhart) independently developed[[34]](./Backpropagation#cite_note-43): 252  backpropagation and taught the algorithm to others in his research circle. He did not cite previous work as he was unaware of them. He published the algorithm first in a 1985 paper, then in a 1986 *[Nature](./Nature_(journal))* paper an experimental analysis of the technique.[[35]](./Backpropagation#cite_note-learning-representations-44) These papers became highly cited, contributed to the popularization of backpropagation, and coincided with the resurging research interest in neural networks during the 1980s.[[5]](./Backpropagation#cite_note-RumelhartHintonWilliams1986a-11)[[36]](./Backpropagation#cite_note-RumelhartHintonWilliams1986b-45)[[37]](./Backpropagation#cite_note-46)

 

In 1985, the method was also described by David Parker.[[38]](./Backpropagation#cite_note-47)[[39]](./Backpropagation#cite_note-:0-48) [Yann LeCun](./Yann_LeCun) proposed an alternative form of backpropagation for neural networks in his PhD thesis in 1987.[[40]](./Backpropagation#cite_note-49)

 

Gradient descent took a considerable amount of time to reach acceptance. Some early objections were: there were no guarantees that gradient descent could reach a global minimum, only local minimum; neurons were "known" by physiologists as making discrete signals (0/1), not continuous ones, and with discrete signals, there is no gradient to take. See the interview with [Geoffrey Hinton](./Geoffrey_Hinton),[[32]](./Backpropagation#cite_note-:1-41) who was awarded the 2024 [Nobel Prize in Physics](./Nobel_Prize_in_Physics) for his contributions to the field.[[41]](./Backpropagation#cite_note-50)

 

### Early successes

 

Contributing to the acceptance were several applications in training neural networks via backpropagation, sometimes achieving popularity outside the research circles.

 

In 1987, [NETtalk](./NETtalk_(artificial_neural_network)) learned to convert English text into pronunciation. Sejnowski tried training it with both backpropagation and Boltzmann machine, but found the backpropagation significantly faster, so he used it for the final NETtalk.[[32]](./Backpropagation#cite_note-:1-41): 324  The NETtalk program became a popular success, appearing on the [*Today* show](./Today_(American_TV_program)).[[42]](./Backpropagation#cite_note-:02-51)

 

In 1989, Dean A. Pomerleau published ALVINN, a neural network trained to [drive autonomously](./Vehicular_automation) using backpropagation.[[43]](./Backpropagation#cite_note-52)

 

The [LeNet](./LeNet) was published in 1989 to recognize handwritten zip codes.

 

In 1992, [TD-Gammon](./TD-Gammon) achieved top human level play in backgammon. It was a reinforcement learning agent with a neural network with two layers, trained by backpropagation.[[44]](./Backpropagation#cite_note-53)

 

In 1993, Eric Wan won an international pattern recognition contest through backpropagation.[[45]](./Backpropagation#cite_note-schmidhuber2015-54)[[46]](./Backpropagation#cite_note-55)

 

### After backpropagation

 

During the 2000s it fell out of favour[*[citation needed](./Wikipedia:Citation_needed)*], but returned in the 2010s, benefiting from cheap, powerful [GPU](./GPU)-based computing systems. This has been especially so in [speech recognition](./Speech_recognition), [machine vision](./Machine_vision), [natural language processing](./Natural_language_processing), and language structure learning research (in which it has been used to explain a variety of phenomena related to first[[47]](./Backpropagation#cite_note-56) and second language learning.[[48]](./Backpropagation#cite_note-57))[[49]](./Backpropagation#cite_note-58)

 

Error backpropagation has been suggested to explain human brain [event-related potential](./Event-related_potential) (ERP) components like the [N400](./N400_(neuroscience)) and [P600](./P600_(neuroscience)).[[50]](./Backpropagation#cite_note-59)

 

In 2023, a backpropagation algorithm was implemented on a [photonic processor](./Photonic_processor) by a team at [Stanford University](./Stanford_University).[[51]](./Backpropagation#cite_note-60)

 

## See also

 
- [Artificial neural network](./Artificial_neural_network)
- [Neural circuit](./Neural_circuit)
- [Catastrophic interference](./Catastrophic_interference)
- [Ensemble learning](./Ensemble_learning)
- [AdaBoost](./AdaBoost)
- [Overfitting](./Overfitting)
- [Neural backpropagation](./Neural_backpropagation)
- [Backpropagation through time](./Backpropagation_through_time)
- [Backpropagation through structure](./Backpropagation_through_structure)
- [Three-factor learning](./Three-factor_learning)

 

## Notes

  
1. [↑](./Backpropagation#cite_ref-3) Use     C   {\displaystyle C}  ![{\displaystyle C}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fc55753007cd3c18576f7933f6f089196732029) for the loss function to allow     L   {\displaystyle L}  ![{\displaystyle L}](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8) to be used for the number of layers
2. [↑](./Backpropagation#cite_ref-4) This follows [Nielsen (2015)](./Backpropagation#CITEREFNielsen2015), and means (left) multiplication by the matrix      W  l     {\displaystyle W^{l}}  ![{\displaystyle W^{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/60b87bc8138a82f110491bb1abd0ea6eefe84c22) corresponds to converting output values of layer     l − −  1   {\displaystyle l-1}  ![{\displaystyle l-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4e0d448948a353d0b2469b88ca918f34e32c8752) to input values of layer     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac): columns correspond to input coordinates, rows correspond to output coordinates.
3. [↑](./Backpropagation#cite_ref-7) This section largely follows and summarizes [Nielsen (2015)](./Backpropagation#CITEREFNielsen2015).
4. [↑](./Backpropagation#cite_ref-8) The derivative of the loss function is a [covector](./Covector), since the loss function is a [scalar-valued function](./Scalar-valued_function) of several variables.
5. [↑](./Backpropagation#cite_ref-9) The activation function is applied to each node separately, so the derivative is just the diagonal matrix of the derivative on each node. This is often represented as the [Hadamard product](./Hadamard_product_(matrices)) with the vector of derivatives, denoted by     (  f  l    ) ′  ⊙ ⊙    {\displaystyle (f^{l})'\odot }  ![{\displaystyle (f^{l})'\odot }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ee57033dfe04a65842e5260c85240f9295cb464c), which is mathematically identical but better matches the internal representation of the derivatives as a vector, rather than a diagonal matrix.
6. [↑](./Backpropagation#cite_ref-10) Since matrix multiplication is linear, the derivative of multiplying by a matrix is just the matrix:     ( W x  ) ′  = W   {\displaystyle (Wx)'=W}  ![{\displaystyle (Wx)'=W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0beeadf03249427d72b4c95732f23143fdfd6c30).
7. [↑](./Backpropagation#cite_ref-12) One may notice that multi-layer neural networks use non-linear activation functions, so an example with linear neurons seems obscure. However, even though the error surface of multi-layer networks are much more complicated, locally they can be approximated by a paraboloid. Therefore, linear neurons are used for simplicity and easier understanding.
8. [↑](./Backpropagation#cite_ref-13) There can be multiple output neurons, in which case the error is the squared norm of the difference vector.
9. [↑](./Backpropagation#cite_ref-14) This order follows (Rumelhart, Hinton & Williams, 1986a):[[5]](./Backpropagation#cite_note-RumelhartHintonWilliams1986a-11) "    Δ Δ   w  i   j   {\displaystyle \Delta w_{i}j}  ![{\displaystyle \Delta w_{i}j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06827536202e269493d147fd8987b9918f7a4aab) is the change to be made to the weight from the     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20)th to the
    j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0)th unit"

 


