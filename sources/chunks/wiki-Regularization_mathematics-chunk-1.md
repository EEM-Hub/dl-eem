---
source: sources/wiki-Regularization_mathematics.md
source_url: https://en.wikipedia.org/wiki/Regularization_(mathematics)
chunk: 1/3
---

Technique to make a model more generalizable and transferable [![](//upload.wikimedia.org/wikipedia/commons/thumb/0/02/Regularization.svg/250px-Regularization.svg.png)](./File:Regularization.svg)The green and blue functions both incur zero loss on the given data points. A learned model can be induced to prefer the green function, which may generalize better to more points drawn from the underlying unknown distribution, by adjusting     λ λ    {\displaystyle \lambda }  ![{\displaystyle \lambda }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b43d0ea3c9c025af1be9128e62a18fa74bedda2a), the weight of the regularization term. 

In [mathematics](./Mathematics), [statistics](./Statistics), [finance](./Mathematical_finance),[[1]](./Regularization_(mathematics)#cite_note-1) and [computer science](./Computer_science), particularly in [machine learning](./Machine_learning) and [inverse problems](./Inverse_problem), **regularization** is a process that converts the [answer to a problem](./Problem_solving) to a simpler one. It is often used in solving [ill-posed problems](./Ill-posed_problems) or to prevent [overfitting](./Overfitting).[[2]](./Regularization_(mathematics)#cite_note-2) There is a strong connection between regularization methods and Bayesian approaches for solving such ill-posed problems [[3]](./Regularization_(mathematics)#cite_note-3).

 

Although regularization procedures can be divided in many ways, the following delineation is particularly helpful:

 
- **Explicit regularization** is regularization whenever one explicitly adds a term to the optimization problem.  These terms could be [priors](./Prior_probability), penalties, or constraints. Explicit regularization is commonly employed with ill-posed optimization problems. The regularization term, or penalty, imposes a cost on the optimization function to make the optimal solution unique.
- **Implicit regularization** is all other forms of regularization.  This includes, for example, early stopping, using a robust loss function, and discarding outliers. Implicit regularization is essentially ubiquitous in modern machine learning approaches, including [stochastic gradient descent](./Stochastic_gradient_descent) for training [deep neural networks](./Deep_neural_networks), and [ensemble methods](./Ensemble_methods) (such as [random forests](./Random_forest) and [gradient boosted trees](./Gradient_boosted_trees)).

 

In explicit regularization, independent of the problem or model, there is always a data term, that corresponds to a likelihood of the measurement, and a regularization term that corresponds to a prior. By combining both using [Bayesian statistics](./Bayesian_statistics), one can compute a posterior, that includes both information sources and therefore stabilizes the estimation process. By trading off both objectives, one chooses to be more aligned to the data or to enforce regularization (to prevent overfitting). There is a whole research branch dealing with all possible regularizations. In practice, one usually tries a specific regularization and then figures out the probability density that corresponds to that regularization to justify the choice. It can also be physically motivated by common sense or intuition.

 

In [machine learning](./Supervised_learning), the data term corresponds to the training data and the regularization is either the choice of the model or modifications to the algorithm. It is always intended to reduce the [generalization error](./Generalization_error), i.e. the error score with the trained model on the evaluation set (testing data) and not the training data.[[4]](./Regularization_(mathematics)#cite_note-4)

 

One of the earliest uses of regularization is [Tikhonov regularization](./Tikhonov_regularization) (ridge regression), related to the method of least squares.

 

## Regularization in machine learning

 

In [machine learning](./Machine_learning), a key challenge is enabling models to accurately predict outcomes on unseen data, not just on familiar training data. Regularization is crucial for addressing [overfitting](./Overfitting)—where a model memorizes training data details but cannot generalize to new data. The goal of regularization is to encourage models to learn the broader patterns within the data rather than memorizing it. Techniques like [early stopping](./Early_stopping), L1 and [L2 regularization](./L2_regularization), and [dropout](./Dropout_(neural_networks)) are designed to prevent overfitting and underfitting, thereby enhancing the model's ability to adapt to and perform well with new data, thus improving model generalization.[[5]](./Regularization_(mathematics)#cite_note-:1-5)

 

### Early stopping

 

Stops training when validation performance deteriorates, preventing overfitting by halting before the model memorizes training data.[[5]](./Regularization_(mathematics)#cite_note-:1-5)

 

### L1 and L2 regularization

 

Adds penalty terms to the cost function to discourage complex models:

 
- **L1 regularization** (also called [LASSO](./Lasso_(statistics))) leads to sparse models by adding a penalty based on the absolute value of coefficients.
- **L2 regularization** (also called [ridge regression](./Ridge_regression)) encourages smaller, more evenly distributed weights by adding a penalty based on the square of the coefficients.[[5]](./Regularization_(mathematics)#cite_note-:1-5)

 

### Dropout

 

In the context of neural networks, the Dropout technique repeatedly ignores random subsets of neurons during training, which simulates the training of multiple neural network architectures at once to improve generalization.[[5]](./Regularization_(mathematics)#cite_note-:1-5)

 

## Classification

 

Empirical learning of classifiers (from a finite data set) is always an [underdetermined](./Underdetermination) problem, because it attempts to infer a function of any     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) given only examples      x  1   ,  x  2   , … …  ,  x  n     {\displaystyle x_{1},x_{2},\dots ,x_{n}}  ![{\displaystyle x_{1},x_{2},\dots ,x_{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/75c2d357bc1b965979bf171b5ba3bac0f68961c2).

 

A regularization term (or regularizer)     R ( f )   {\displaystyle R(f)}  ![{\displaystyle R(f)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb57f1b3ae288e52318d733f1c69d3e3637318b8) is added to a [loss function](./Loss_functions_for_classification):
     min  f    ∑ ∑   i = 1   n   V ( f (  x  i   ) ,  y  i   ) + λ λ  R ( f )   {\displaystyle \min _{f}\sum _{i=1}^{n}V(f(x_{i}),y_{i})+\lambda R(f)}  ![{\displaystyle \min _{f}\sum _{i=1}^{n}V(f(x_{i}),y_{i})+\lambda R(f)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d55221bf8c9b730ff7c4eddddb9473af47bb1d1c)
where     V   {\displaystyle V}  ![{\displaystyle V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/af0f6064540e84211d0ffe4dac72098adfa52845) is an underlying loss function that describes the cost of predicting     f ( x )   {\displaystyle f(x)}  ![{\displaystyle f(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/202945cce41ecebb6f643f31d119c514bec7a074) when the label is     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d), such as the [square loss](./Loss_functions_for_classification#Square_loss) or [hinge loss](./Hinge_loss); and     λ λ    {\displaystyle \lambda }  ![{\displaystyle \lambda }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b43d0ea3c9c025af1be9128e62a18fa74bedda2a) is a parameter which controls the importance of the regularization term.     R ( f )   {\displaystyle R(f)}  ![{\displaystyle R(f)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb57f1b3ae288e52318d733f1c69d3e3637318b8) is typically chosen to impose a penalty on the complexity of     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61). Concrete notions of complexity used include restrictions for [smoothness](./Smooth_function) and bounds on the [vector space norm](./Normed_vector_space).[[6]](./Regularization_(mathematics)#cite_note-:0-6)[*[page needed](./Wikipedia:Citing_sources)*]

 

A theoretical justification for regularization is that it attempts to impose [Occam's razor](./Occam's_razor) on the solution (as depicted in the figure above, where the green function, the simpler one, may be preferred). From a [Bayesian](./Bayesian_inference) point of view, many regularization techniques correspond to imposing certain [prior](./Prior_probability) distributions on model parameters.[[7]](./Regularization_(mathematics)#cite_note-7)

 

Regularization can serve multiple purposes, including learning simpler models, inducing models to be sparse and introducing group structure[*[clarification needed](./Wikipedia:Please_clarify)*] into the learning problem.

 

The same idea arose in many fields of [science](./Science). A simple form of regularization applied to [integral equations](./Integral_equation) ([Tikhonov regularization](./Tikhonov_regularization))  is essentially a trade-off between fitting the data and reducing a norm of the solution. More recently, non-linear regularization methods, including [total variation regularization](./Total_variation_regularization), have become popular.

 

### Generalization

 Main article: [Generalization error](./Generalization_error) 

Regularization can be motivated as a technique to improve the generalizability of a learned model.

 

The goal of this learning problem is to find a function that fits or predicts the outcome (label) that minimizes the expected error over all possible inputs and labels. The expected error of a function      f  n     {\displaystyle f_{n}}  ![{\displaystyle f_{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b2702450f0458a5e01a698e248af552a7fab2b50) is:
    I [  f  n   ] =  ∫ ∫   X × ×  Y   V (  f  n   ( x ) , y ) ρ ρ  ( x , y )  d x  d y   {\displaystyle I[f_{n}]=\int _{X\times Y}V(f_{n}(x),y)\rho (x,y)\,dx\,dy}  ![{\displaystyle I[f_{n}]=\int _{X\times Y}V(f_{n}(x),y)\rho (x,y)\,dx\,dy}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed5b23928275fa76b21e57ae0e15ca2b145951fc)
where     X   {\displaystyle X}  ![{\displaystyle X}](https://wikimedia.org/api/rest_v1/media/math/render/svg/68baa052181f707c662844a465bfeeb135e82bab) and     Y   {\displaystyle Y}  ![{\displaystyle Y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/961d67d6b454b4df2301ac571808a3538b3a6d3f) are the domains of input data     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) and their labels     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) respectively.

 

Typically in learning problems, only a subset of input data and labels are available, measured with some noise. Therefore, the expected error is unmeasurable, and the best surrogate available is the empirical error over the     N   {\displaystyle N}  ![{\displaystyle N}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5e3890c981ae85503089652feb48b191b57aae3) available samples:
     I  S   [  f  n   ] =   1 n    ∑ ∑   i = 1   N   V (  f  n   (     x ^ ^      i   ) ,     y ^ ^      i   )   {\displaystyle I_{S}[f_{n}]={\frac {1}{n}}\sum _{i=1}^{N}V(f_{n}({\hat {x}}_{i}),{\hat {y}}_{i})}  ![{\displaystyle I_{S}[f_{n}]={\frac {1}{n}}\sum _{i=1}^{N}V(f_{n}({\hat {x}}_{i}),{\hat {y}}_{i})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a58098b9d07627cd142659a29510d7e9d7b02510)
Without bounds on the complexity of the function space (formally, the [reproducing kernel Hilbert space](./Reproducing_kernel_Hilbert_space)) available, a model will be learned that incurs zero loss on the surrogate empirical error. If measurements (e.g. of      x  i     {\displaystyle x_{i}}  ![{\displaystyle x_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e87000dd6142b81d041896a30fe58f0c3acb2158)) were made with noise, this model may suffer from [overfitting](./Overfitting) and display poor expected error. Regularization introduces a penalty for exploring certain regions of the function space used to build the model, which can improve generalization.

 

## Tikhonov regularization (ridge regression)

 Main article: [Tikhonov regularization](./Tikhonov_regularization) 

These techniques are named for [Andrey Nikolayevich Tikhonov](./Andrey_Nikolayevich_Tikhonov), who applied regularization to [integral equations](./Integral_equation) and made important contributions in many other areas.

 

When learning a linear function     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61), characterized by an unknown [vector](./Vector_space)     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) such that     f ( x ) = w ⋅ ⋅  x   {\displaystyle f(x)=w\cdot x}  ![{\displaystyle f(x)=w\cdot x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d5ff2299b2423508dcbb92773fd4d18b6d43dd6), one can add the      L  2     {\displaystyle L_{2}}  ![{\displaystyle L_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c6a952cfe42c86b7741f55a817da0e251793a358)-norm of the vector     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) to the loss expression in order to prefer solutions with smaller norms. Tikhonov regularization is one of the most common forms. It is also known as ridge regression. It is expressed as:
     min  w    ∑ ∑   i = 1   n   V (     x ^ ^      i   ⋅ ⋅  w ,     y ^ ^      i   ) + λ λ    ‖ w ‖   2   2   ,   {\displaystyle \min _{w}\sum _{i=1}^{n}V({\hat {x}}_{i}\cdot w,{\hat {y}}_{i})+\lambda \left\|w\right\|_{2}^{2},}  ![{\displaystyle \min _{w}\sum _{i=1}^{n}V({\hat {x}}_{i}\cdot w,{\hat {y}}_{i})+\lambda \left\|w\right\|_{2}^{2},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94620eaa70c51ec7ea59fcf8f43720f7e99e37c0)
where     (     x ^ ^      i   ,     y ^ ^      i   ) ,  1 ≤ ≤  i ≤ ≤  n ,   {\displaystyle ({\hat {x}}_{i},{\hat {y}}_{i}),\,1\leq i\leq n,}  ![{\displaystyle ({\hat {x}}_{i},{\hat {y}}_{i}),\,1\leq i\leq n,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1161d93f48a6b936ca488173be50af4a33171d01) would represent samples used for training.

 

In the case of a general function, the norm of the function in its [reproducing kernel Hilbert space](./Reproducing_kernel_Hilbert_space) is:
     min  f    ∑ ∑   i = 1   n   V ( f (     x ^ ^      i   ) ,     y ^ ^      i   ) + λ λ    ‖ f ‖    H    2     {\displaystyle \min _{f}\sum _{i=1}^{n}V(f({\hat {x}}_{i}),{\hat {y}}_{i})+\lambda \left\|f\right\|_{\mathcal {H}}^{2}}  ![{\displaystyle \min _{f}\sum _{i=1}^{n}V(f({\hat {x}}_{i}),{\hat {y}}_{i})+\lambda \left\|f\right\|_{\mathcal {H}}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf6c09c88a01ceec0946115884bfb1085ddd8e40)

 

As the      L  2     {\displaystyle L_{2}}  ![{\displaystyle L_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c6a952cfe42c86b7741f55a817da0e251793a358) norm is [differentiable](./Differentiable_function#Differentiability_in_higher_dimensions), learning can be advanced by [gradient descent](./Gradient_descent).

 

### Tikhonov-regularized least squares

 

The learning problem with the [least squares](./Least_squares) loss function and Tikhonov regularization can be solved analytically. Written in matrix form, the optimal     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) is the one for which the gradient of the loss function with respect to     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) is 0.
     min  w     1 n     (     X ^ ^     w − −  Y  )    T     (     X ^ ^     w − −  Y  )  + λ λ    ‖ w ‖   2   2     {\displaystyle \min _{w}{\frac {1}{n}}\left({\hat {X}}w-Y\right)^{\mathsf {T}}\left({\hat {X}}w-Y\right)+\lambda \left\|w\right\|_{2}^{2}}  ![{\displaystyle \min _{w}{\frac {1}{n}}\left({\hat {X}}w-Y\right)^{\mathsf {T}}\left({\hat {X}}w-Y\right)+\lambda \left\|w\right\|_{2}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7bc20d46882e103abee5b293ab075926d021c843)      ∇ ∇   w   =   2 n       X ^ ^       T     (     X ^ ^     w − −  Y  )  + 2 λ λ  w   {\displaystyle \nabla _{w}={\frac {2}{n}}{\hat {X}}^{\mathsf {T}}\left({\hat {X}}w-Y\right)+2\lambda w}  ![{\displaystyle \nabla _{w}={\frac {2}{n}}{\hat {X}}^{\mathsf {T}}\left({\hat {X}}w-Y\right)+2\lambda w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/caa68ca05fc0bddf68952e716cacde280747152a)     0 =     X ^ ^       T     (     X ^ ^     w − −  Y  )  + n λ λ  w   {\displaystyle 0={\hat {X}}^{\mathsf {T}}\left({\hat {X}}w-Y\right)+n\lambda w}  ![{\displaystyle 0={\hat {X}}^{\mathsf {T}}\left({\hat {X}}w-Y\right)+n\lambda w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/df92f3efe07bf2547ff4635321d18369f2eabdcb)    w =   (      X ^ ^       T       X ^ ^     + λ λ  n I  )   − −  1    (      X ^ ^       T    Y  )    {\displaystyle w=\left({\hat {X}}^{\mathsf {T}}{\hat {X}}+\lambda nI\right)^{-1}\left({\hat {X}}^{\mathsf {T}}Y\right)}  ![{\displaystyle w=\left({\hat {X}}^{\mathsf {T}}{\hat {X}}+\lambda nI\right)^{-1}\left({\hat {X}}^{\mathsf {T}}Y\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/751490b804e1af09fa8ee4cd01f1ff93c2cf1101)
where the third statement is a [first-order condition](./First-order_condition).

 

By construction of the optimization problem, other values of     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) give larger values for the loss function. This can be verified by examining the [second derivative](./Second_derivative)      ∇ ∇   w w     {\displaystyle \nabla _{ww}}  ![{\displaystyle \nabla _{ww}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9df074aaacb814a1dc62001766847b1c0457c358).

 

During training, this algorithm takes     O (  d  3   + n  d  2   )   {\displaystyle O(d^{3}+nd^{2})}  ![{\displaystyle O(d^{3}+nd^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb07ee3b6722d3b0e2537d36e2a75669325c49c8) [time](./Time_complexity). The terms correspond to the matrix inversion and calculating      X   T    X   {\displaystyle X^{\mathsf {T}}X}  ![{\displaystyle X^{\mathsf {T}}X}](https://wikimedia.org/api/rest_v1/media/math/render/svg/75a4cb7b8bf2de8f4b677bee7ac95cd1fd3ef35f), respectively. Testing takes     O ( n d )   {\displaystyle O(nd)}  ![{\displaystyle O(nd)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d627081a425c8784d1e2f4da283e073fd960e881) time.

 

## Early stopping

 Main article: [Early stopping](./Early_stopping) 

Early stopping can be viewed as regularization in time. Intuitively, a training procedure such as gradient descent tends to learn more and more complex functions with increasing iterations. By regularizing for time, model complexity can be controlled, improving generalization.

 

Early stopping is implemented using one data set for training, one statistically independent data set for validation and another for testing. The model is trained until performance on the validation set no longer improves and then applied to the test set.

 

### Theoretical motivation in least squares

 

Consider the finite approximation of [Neumann series](./Neumann_series) for an invertible matrix A where      ‖  I − −  A  ‖  < 1   {\displaystyle \left\|I-A\right\|<1}  ![{\displaystyle \left\|I-A\right\|<1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ab22351caf868979f543b253b84af3bc91006765):
     ∑ ∑   i = 0   T − −  1     (  I − −  A  )   i   ≈ ≈   A  − −  1     {\displaystyle \sum _{i=0}^{T-1}\left(I-A\right)^{i}\approx A^{-1}}  ![{\displaystyle \sum _{i=0}^{T-1}\left(I-A\right)^{i}\approx A^{-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/19e1cb5e5c56c4a950048e048d48ebb043ea3398)

 

This can be used to approximate the analytical solution of unregularized least squares, if γ is introduced to ensure the norm is less than one.
     w  T   =   γ γ  n    ∑ ∑   i = 0   T − −  1     (  I − −    γ γ  n       X ^ ^       T       X ^ ^      )   i       X ^ ^       T       Y ^ ^       {\displaystyle w_{T}={\frac {\gamma }{n}}\sum _{i=0}^{T-1}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}}  ![{\displaystyle w_{T}={\frac {\gamma }{n}}\sum _{i=0}^{T-1}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0eb1c16a5a30e1e372378b087aee9f8124c38b84)

 

The exact solution to the unregularized least squares learning problem minimizes the empirical error, but may fail. By limiting T, the only free parameter in the algorithm above, the problem is regularized for time, which may improve its generalization.

 

The algorithm above is equivalent to restricting the number of gradient descent iterations for the empirical risk
     I  s   [ w ] =   1  2 n      ‖     X ^ ^     w − −     Y ^ ^      ‖     R   n     2     {\displaystyle I_{s}[w]={\frac {1}{2n}}\left\|{\hat {X}}w-{\hat {Y}}\right\|_{\mathbb {R} ^{n}}^{2}}  ![{\displaystyle I_{s}[w]={\frac {1}{2n}}\left\|{\hat {X}}w-{\hat {Y}}\right\|_{\mathbb {R} ^{n}}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9026461a341e26206c118e94aaa72f0ef54c8c8)
with the gradient descent update:
         w  0      = 0      w  t + 1      =  (  I − −    γ γ  n       X ^ ^       T       X ^ ^      )   w  t   +   γ γ  n       X ^ ^       T       Y ^ ^           {\displaystyle {\begin{aligned}w_{0}&=0\\[1ex]w_{t+1}&=\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)w_{t}+{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\end{aligned}}}  ![{\displaystyle {\begin{aligned}w_{0}&=0\\[1ex]w_{t+1}&=\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)w_{t}+{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/faa62ed56683605d9076bd2e16e2e6a78e2c0ac8)

 

The base case is trivial. The inductive case is proved as follows:
         w  T      =  (  I − −    γ γ  n       X ^ ^       T       X ^ ^      )    γ γ  n    ∑ ∑   i = 0   T − −  2     (  I − −    γ γ  n       X ^ ^       T       X ^ ^      )   i       X ^ ^       T       Y ^ ^     +   γ γ  n       X ^ ^       T       Y ^ ^           =   γ γ  n    ∑ ∑   i = 1   T − −  1     (  I − −    γ γ  n       X ^ ^       T       X ^ ^      )   i       X ^ ^       T       Y ^ ^     +   γ γ  n       X ^ ^       T       Y ^ ^           =   γ γ  n    ∑ ∑   i = 0   T − −  1     (  I − −    γ γ  n       X ^ ^       T       X ^ ^      )   i       X ^ ^       T       Y ^ ^           {\displaystyle {\begin{aligned}w_{T}&=\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right){\frac {\gamma }{n}}\sum _{i=0}^{T-2}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}+{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\\[1ex]&={\frac {\gamma }{n}}\sum _{i=1}^{T-1}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}+{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\\[1ex]&={\frac {\gamma }{n}}\sum _{i=0}^{T-1}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\end{aligned}}}  ![{\displaystyle {\begin{aligned}w_{T}&=\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right){\frac {\gamma }{n}}\sum _{i=0}^{T-2}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}+{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\\[1ex]&={\frac {\gamma }{n}}\sum _{i=1}^{T-1}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}+{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\\[1ex]&={\frac {\gamma }{n}}\sum _{i=0}^{T-1}\left(I-{\frac {\gamma }{n}}{\hat {X}}^{\mathsf {T}}{\hat {X}}\right)^{i}{\hat {X}}^{\mathsf {T}}{\hat {Y}}\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a9db8fc95e0e48598fa460210d8fb4103167135c)

 


