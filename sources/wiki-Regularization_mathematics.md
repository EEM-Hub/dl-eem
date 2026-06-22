---
source: https://en.wikipedia.org/wiki/Regularization_(mathematics)
fetched: 2026-06-21
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

 

## Regularizers for sparsity

 

Assume that a dictionary      ϕ ϕ   j     {\displaystyle \phi _{j}}  ![{\displaystyle \phi _{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e4cbf9f77e99bf49bdc5b3afa8b6b77d15b9be6b) with dimension     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) is given such that a function in the function space can be expressed as:
    f ( x ) =  ∑ ∑   j = 1   p    ϕ ϕ   j   ( x )  w  j     {\displaystyle f(x)=\sum _{j=1}^{p}\phi _{j}(x)w_{j}}  ![{\displaystyle f(x)=\sum _{j=1}^{p}\phi _{j}(x)w_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/252ae1db10e047c163e16d13dc51d0cf5edea9b8)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/b/b8/Sparsityl1.png/250px-Sparsityl1.png)](./File:Sparsityl1.png)A comparison between the L1 ball and the L2 ball in two dimensions gives an intuition on how L1 regularization achieves sparsity. 

Enforcing a sparsity constraint on     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) can lead to simpler and more interpretable models. This is useful in many real-life applications such as [computational biology](./Computational_biology). An example is developing a simple predictive test for a disease in order to minimize the cost of performing medical tests while maximizing predictive power.

 

A sensible sparsity constraint is the [     L  0     {\displaystyle L_{0}}  ![{\displaystyle L_{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/db742b8c210fc611329a4c2dcc3af4b4e1a110cb) norm](./Norm_(mathematics))     ‖ ‖  w  ‖ ‖   0     {\displaystyle \|w\|_{0}}  ![{\displaystyle \|w\|_{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c88dffe8814e949d43dd9c949e26b1ebab06642), defined as the number of non-zero elements in     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6). Solving a      L  0     {\displaystyle L_{0}}  ![{\displaystyle L_{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/db742b8c210fc611329a4c2dcc3af4b4e1a110cb) regularized learning problem, however, has been demonstrated to be [NP-hard](./NP-hardness).[[8]](./Regularization_(mathematics)#cite_note-8)

 

The [     L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013) norm](./Taxicab_geometry) (see also [Norms](./Norm_(mathematics))) can be used to approximate the optimal [     L  0     {\displaystyle L_{0}}  ![{\displaystyle L_{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/db742b8c210fc611329a4c2dcc3af4b4e1a110cb)](./Norm_(mathematics)) norm via convex relaxation. It can be shown that the [     L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013)](./Norm_(mathematics)) norm induces sparsity. In the case of least squares, this problem is known as [LASSO](./Lasso_(statistics)) in statistics and [basis pursuit](./Basis_pursuit) in signal processing.
     min  w ∈ ∈    R   p       1 n     ‖     X ^ ^     w − −     Y ^ ^      ‖   2   + λ λ    ‖ w ‖   1     {\displaystyle \min _{w\in \mathbb {R} ^{p}}{\frac {1}{n}}\left\|{\hat {X}}w-{\hat {Y}}\right\|^{2}+\lambda \left\|w\right\|_{1}}  ![{\displaystyle \min _{w\in \mathbb {R} ^{p}}{\frac {1}{n}}\left\|{\hat {X}}w-{\hat {Y}}\right\|^{2}+\lambda \left\|w\right\|_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/881363e7ce3cd9f55e427783027faeb58c92b0ac)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Sparsityen.png/250px-Sparsityen.png)](./File:Sparsityen.png)Elastic net regularization 

[     L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013)](./Norm_(mathematics)) regularization can occasionally produce non-unique solutions. A simple example is provided in the figure when the space of possible solutions lies on a 45 degree line. This can be problematic for certain applications, and is overcome by combining [     L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013)](./Norm_(mathematics)) with [     L  2     {\displaystyle L_{2}}  ![{\displaystyle L_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c6a952cfe42c86b7741f55a817da0e251793a358)](./Norm_(mathematics)) regularization in [elastic net regularization](./Elastic_net_regularization), which takes the following form:
     min  w ∈ ∈    R   p       1 n     ‖     X ^ ^     w − −     Y ^ ^      ‖   2   + λ λ   (  α α    ‖ w ‖   1   + ( 1 − −  α α  )   ‖ w ‖   2   2    )  , α α  ∈ ∈  [ 0 , 1 ]   {\displaystyle \min _{w\in \mathbb {R} ^{p}}{\frac {1}{n}}\left\|{\hat {X}}w-{\hat {Y}}\right\|^{2}+\lambda \left(\alpha \left\|w\right\|_{1}+(1-\alpha )\left\|w\right\|_{2}^{2}\right),\alpha \in [0,1]}  ![{\displaystyle \min _{w\in \mathbb {R} ^{p}}{\frac {1}{n}}\left\|{\hat {X}}w-{\hat {Y}}\right\|^{2}+\lambda \left(\alpha \left\|w\right\|_{1}+(1-\alpha )\left\|w\right\|_{2}^{2}\right),\alpha \in [0,1]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/114822b99a2e7ac7104e507bd6873f1337b44807)

 

Elastic net regularization tends to have a grouping effect, where correlated input features are assigned equal weights.

 

Elastic net regularization is commonly used in practice and is implemented in many machine learning libraries.

 

### Proximal methods

 Main article: [Proximal gradient method](./Proximal_gradient_method)

While the [     L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013)](./Norm_(mathematics)) norm does not result in an NP-hard problem, the [     L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013)](./Norm_(mathematics)) norm is convex but is not strictly differentiable due to the kink at x = 0. [Subgradient methods](./Subgradient_method) which rely on the [subderivative](./Subderivative) can be used to solve [     L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013)](./Norm_(mathematics)) regularized learning problems. However, faster convergence can be achieved through proximal methods.

 

For a problem      min  w ∈ ∈  H   F ( w ) + R ( w )   {\displaystyle \min _{w\in H}F(w)+R(w)}  ![{\displaystyle \min _{w\in H}F(w)+R(w)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a5487b2c176722605917b8965873a8382bd1186) such that     F   {\displaystyle F}  ![{\displaystyle F}](https://wikimedia.org/api/rest_v1/media/math/render/svg/545fd099af8541605f7ee55f08225526be88ce57) is convex, continuous, differentiable, with Lipschitz continuous gradient (such as the least squares loss function), and     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) is convex, continuous, and proper, then the proximal method to solve the problem is as follows. First define the [proximal operator](./Proximal_operator)      prox  R   ⁡ ⁡  ( v ) =   argmin   w ∈ ∈    R   D     ⁡ ⁡   {  R ( w ) +   1 2     ‖  w − −  v  ‖   2    }  ,   {\displaystyle \operatorname {prox} _{R}(v)=\mathop {\operatorname {argmin} } _{w\in \mathbb {R} ^{D}}\left\{R(w)+{\frac {1}{2}}\left\|w-v\right\|^{2}\right\},}  ![{\displaystyle \operatorname {prox} _{R}(v)=\mathop {\operatorname {argmin} } _{w\in \mathbb {R} ^{D}}\left\{R(w)+{\frac {1}{2}}\left\|w-v\right\|^{2}\right\},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5ad71c25084098075b68125c5e9198ce0f68fb7d)
and then iterate
     w  k + 1   =   prox   γ γ  , R   ⁡ ⁡   (   w  k   − −  γ γ  ∇ ∇  F (  w  k   )  )    {\displaystyle w_{k+1}=\mathop {\operatorname {prox} } _{\gamma ,R}\left(w_{k}-\gamma \nabla F(w_{k})\right)}  ![{\displaystyle w_{k+1}=\mathop {\operatorname {prox} } _{\gamma ,R}\left(w_{k}-\gamma \nabla F(w_{k})\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a92f3cae619dba225955ea410992a919899bb376)

 

The proximal method iteratively performs gradient descent and then projects the result back into the space permitted by     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33).

 

When     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) is the [*L*1](./Norm_(mathematics)) regularizer, the proximal operator is equivalent to the soft-thresholding operator,
     S  λ λ    ( v ) f ( n ) =   {     v  i   − −  λ λ  ,    if    v  i   > λ λ      0 ,    if    v  i   ∈ ∈  [ − −  λ λ  , λ λ  ]      v  i   + λ λ  ,    if    v  i   < − −  λ λ          {\displaystyle S_{\lambda }(v)f(n)={\begin{cases}v_{i}-\lambda ,&{\text{if }}v_{i}>\lambda \\0,&{\text{if }}v_{i}\in [-\lambda ,\lambda ]\\v_{i}+\lambda ,&{\text{if }}v_{i}<-\lambda \end{cases}}}  ![{\displaystyle S_{\lambda }(v)f(n)={\begin{cases}v_{i}-\lambda ,&{\text{if }}v_{i}>\lambda \\0,&{\text{if }}v_{i}\in [-\lambda ,\lambda ]\\v_{i}+\lambda ,&{\text{if }}v_{i}<-\lambda \end{cases}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c66ce8f0dd246cee2c7dc8e38051a7f4526bb41f)

 

This allows for efficient computation.

 

### Group sparsity without overlaps

 

Groups of features can be regularized by a sparsity constraint, which can be useful for expressing certain prior knowledge into an optimization problem.

 

In the case of a linear model with non-overlapping known groups, a regularizer can be defined:
    R ( w ) =  ∑ ∑   g = 1   G     ‖  w  g   ‖   2   ,   {\displaystyle R(w)=\sum _{g=1}^{G}\left\|w_{g}\right\|_{2},}  ![{\displaystyle R(w)=\sum _{g=1}^{G}\left\|w_{g}\right\|_{2},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d52d671d356f362f9338d2bdd3e57f39b5387541) where     ‖ ‖   w  g    ‖ ‖   2   =    ∑ ∑   j = 1    |   G  g    |      (  w  g   j   )   2       {\displaystyle \|w_{g}\|_{2}={\sqrt {\sum _{j=1}^{|G_{g}|}\left(w_{g}^{j}\right)^{2}}}}  ![{\displaystyle \|w_{g}\|_{2}={\sqrt {\sum _{j=1}^{|G_{g}|}\left(w_{g}^{j}\right)^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dc43475d5da834e6d577e02a4e1d4e0e6b0d4a05)

 

This can be viewed as inducing a regularizer over the      L  2     {\displaystyle L_{2}}  ![{\displaystyle L_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c6a952cfe42c86b7741f55a817da0e251793a358) norm over members of each group followed by an      L  1     {\displaystyle L_{1}}  ![{\displaystyle L_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e79dc1b001f8b923df475ed14de023cbc456013) norm over groups.

 

This can be solved by the proximal method, where the proximal operator is a block-wise soft-thresholding function:

 

     prox  λ λ  , R , g   ⁡ ⁡  (  w  g   ) =   {     (  1 − −     λ λ    ‖  w  g   ‖   2       )   w  g   ,    if     ‖  w  g   ‖   2   > λ λ      0 ,    if   ‖ ‖   w  g    ‖ ‖   2   ≤ ≤  λ λ          {\displaystyle \operatorname {prox} \limits _{\lambda ,R,g}(w_{g})={\begin{cases}\left(1-{\dfrac {\lambda }{\left\|w_{g}\right\|_{2}}}\right)w_{g},&{\text{if }}\left\|w_{g}\right\|_{2}>\lambda \\[1ex]0,&{\text{if }}\|w_{g}\|_{2}\leq \lambda \end{cases}}}  ![{\displaystyle \operatorname {prox} \limits _{\lambda ,R,g}(w_{g})={\begin{cases}\left(1-{\dfrac {\lambda }{\left\|w_{g}\right\|_{2}}}\right)w_{g},&{\text{if }}\left\|w_{g}\right\|_{2}>\lambda \\[1ex]0,&{\text{if }}\|w_{g}\|_{2}\leq \lambda \end{cases}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ef394215d5b0d59b5a26afee3b81cfcbf68363cd)

 

### Group sparsity with overlaps

 

The algorithm described for group sparsity without overlaps can be applied to the case where groups do overlap, in certain situations. This will likely result in some groups with all zero elements, and other groups with some non-zero and some zero elements.

 

If it is desired to preserve the group structure, a new regularizer can be defined:
    R ( w ) = inf  {   ∑ ∑   g = 1   G   ‖ ‖   w  g    ‖ ‖   2   : w =  ∑ ∑   g = 1   G       w ¯ ¯      g    }    {\displaystyle R(w)=\inf \left\{\sum _{g=1}^{G}\|w_{g}\|_{2}:w=\sum _{g=1}^{G}{\bar {w}}_{g}\right\}}  ![{\displaystyle R(w)=\inf \left\{\sum _{g=1}^{G}\|w_{g}\|_{2}:w=\sum _{g=1}^{G}{\bar {w}}_{g}\right\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5c6ddbe625e5d5655ca37290438269f3ace773d5)

 

For each      w  g     {\displaystyle w_{g}}  ![{\displaystyle w_{g}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3e28da8e516d060d7d6cef2ef308b1000a89c806),         w ¯ ¯      g     {\displaystyle {\bar {w}}_{g}}  ![{\displaystyle {\bar {w}}_{g}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/07167fb8c0903147514bf7a72f2e736eca4cd12e) is defined as the vector such that the restriction of         w ¯ ¯      g     {\displaystyle {\bar {w}}_{g}}  ![{\displaystyle {\bar {w}}_{g}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/07167fb8c0903147514bf7a72f2e736eca4cd12e) to the group     g   {\displaystyle g}  ![{\displaystyle g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3556280e66fe2c0d0140df20935a6f057381d77) equals      w  g     {\displaystyle w_{g}}  ![{\displaystyle w_{g}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3e28da8e516d060d7d6cef2ef308b1000a89c806) and all other entries of         w ¯ ¯      g     {\displaystyle {\bar {w}}_{g}}  ![{\displaystyle {\bar {w}}_{g}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/07167fb8c0903147514bf7a72f2e736eca4cd12e) are zero. The regularizer finds the optimal disintegration of     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) into parts. It can be viewed as duplicating all elements that exist in multiple groups. Learning problems with this regularizer can also be solved with the proximal method with a complication. The proximal operator cannot be computed in closed form, but can be effectively solved iteratively, inducing an inner iteration within the proximal method iteration.

 

## Regularizers for semi-supervised learning

 Main article: [Semi-supervised learning](./Semi-supervised_learning) 

When labels are more expensive to gather than input examples, semi-supervised learning can be useful. Regularizers have been designed to guide learning algorithms to learn models that respect the structure of unsupervised training samples. If a symmetric weight matrix     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7) is given, a regularizer can be defined:
    R ( f ) =  ∑ ∑   i , j    w  i j     (  f (  x  i   ) − −  f (  x  j   )  )   2     {\displaystyle R(f)=\sum _{i,j}w_{ij}\left(f(x_{i})-f(x_{j})\right)^{2}}  ![{\displaystyle R(f)=\sum _{i,j}w_{ij}\left(f(x_{i})-f(x_{j})\right)^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c9a7ea0ce9f893eafce65a40452c60229423456e)

 

If      W  i j     {\displaystyle W_{ij}}  ![{\displaystyle W_{ij}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/29c09e9d719bb634d8ca5a6172b0562b945bf325) encodes the result of some distance metric for points      x  i     {\displaystyle x_{i}}  ![{\displaystyle x_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e87000dd6142b81d041896a30fe58f0c3acb2158) and      x  j     {\displaystyle x_{j}}  ![{\displaystyle x_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5db47cb3d2f9496205a17a6856c91c1d3d363ccd), it is desirable that     f (  x  i   ) ≈ ≈  f (  x  j   )   {\displaystyle f(x_{i})\approx f(x_{j})}  ![{\displaystyle f(x_{i})\approx f(x_{j})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b4e02bfc3366dd21618d120571b12271ad361c84). This regularizer captures this intuition, and is equivalent to:
    R ( f ) =     f ¯ ¯       T    L    f ¯ ¯       {\displaystyle R(f)={\bar {f}}^{\mathsf {T}}L{\bar {f}}}  ![{\displaystyle R(f)={\bar {f}}^{\mathsf {T}}L{\bar {f}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2ba0d74fdf16e5f3cdc6443c8a5c13ded456df67) where     L = D − −  W   {\displaystyle L=D-W}  ![{\displaystyle L=D-W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/14ee07ee510ca6515e6668dca08cf5a0de2c2544) is the [Laplacian matrix](./Laplacian_matrix) of the graph induced by     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7).

 

The optimization problem      min  f ∈ ∈    R   m     R ( f ) , m = u + l   {\displaystyle \min _{f\in \mathbb {R} ^{m}}R(f),m=u+l}  ![{\displaystyle \min _{f\in \mathbb {R} ^{m}}R(f),m=u+l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a64f689da30e245b8bad2f51ba3a4bf191efab4e) can be solved analytically if the constraint     f (  x  i   ) =  y  i     {\displaystyle f(x_{i})=y_{i}}  ![{\displaystyle f(x_{i})=y_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/20ade1442f5d991818460d0ecdd4f7b053cbd91c) is applied for all supervised samples. The labeled part of the vector     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) is therefore obvious. The unlabeled part of     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) is solved for by:
     min   f  u   ∈ ∈    R   u      f   T    L f =  min   f  u   ∈ ∈    R   u      {   f  u    T     L  u u    f  u   +  f  l    T     L  l u    f  u   +  f  u    T     L  u l    f  l    }    {\displaystyle \min _{f_{u}\in \mathbb {R} ^{u}}f^{\mathsf {T}}Lf=\min _{f_{u}\in \mathbb {R} ^{u}}\left\{f_{u}^{\mathsf {T}}L_{uu}f_{u}+f_{l}^{\mathsf {T}}L_{lu}f_{u}+f_{u}^{\mathsf {T}}L_{ul}f_{l}\right\}}  ![{\displaystyle \min _{f_{u}\in \mathbb {R} ^{u}}f^{\mathsf {T}}Lf=\min _{f_{u}\in \mathbb {R} ^{u}}\left\{f_{u}^{\mathsf {T}}L_{uu}f_{u}+f_{l}^{\mathsf {T}}L_{lu}f_{u}+f_{u}^{\mathsf {T}}L_{ul}f_{l}\right\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1cad974824a9925ed9c67f34c9ebc9df68a2248f)      ∇ ∇    f  u     = 2  L  u u    f  u   + 2  L  u l   Y   {\displaystyle \nabla _{f_{u}}=2L_{uu}f_{u}+2L_{ul}Y}  ![{\displaystyle \nabla _{f_{u}}=2L_{uu}f_{u}+2L_{ul}Y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/63adc3e09a6fef7ef3112d2cf032111d090b6b18)      f  u   =  L  u u   † †     (   L  u l   Y  )    {\displaystyle f_{u}=L_{uu}^{\dagger }\left(L_{ul}Y\right)}  ![{\displaystyle f_{u}=L_{uu}^{\dagger }\left(L_{ul}Y\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fc3b2a939bca89b01fc44eb2f352f663defb2d52)
The pseudo-inverse can be taken because      L  u l     {\displaystyle L_{ul}}  ![{\displaystyle L_{ul}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/de9f0f868a225b3d179c9d7687a693c7488cb787) has the same range as      L  u u     {\displaystyle L_{uu}}  ![{\displaystyle L_{uu}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b8c142b8f58dbd2bd5dc50136f33cf446df5c19).

 

## Regularizers for multitask learning

 Main article: [Multi-task learning](./Multi-task_learning)

In the case of multitask learning,     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) problems are considered simultaneously, each related in some way. The goal is to learn     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) functions, ideally borrowing strength from the relatedness of tasks, that have predictive power. This is equivalent to learning the matrix     W : T × ×  D   {\displaystyle W:T\times D}  ![{\displaystyle W:T\times D}](https://wikimedia.org/api/rest_v1/media/math/render/svg/edf8322cb32156be2fe4daec37105dbe1a1cb1d3) .

 

### Sparse regularizer on columns

 

    R ( w ) =  ∑ ∑   i = 1   D     ‖ W ‖   2 , 1     {\displaystyle R(w)=\sum _{i=1}^{D}\left\|W\right\|_{2,1}}  ![{\displaystyle R(w)=\sum _{i=1}^{D}\left\|W\right\|_{2,1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43d6568dcb2d8fcb4d605ac566fe7cb10b4e3a67)

 

This regularizer defines an L2 norm on each column and an L1 norm over all columns. It can be solved by proximal methods.

 

### Nuclear norm regularization

 

    R ( w ) =   ‖  σ σ  ( W )  ‖   1     {\displaystyle R(w)=\left\|\sigma (W)\right\|_{1}}  ![{\displaystyle R(w)=\left\|\sigma (W)\right\|_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cdd498f57dd6bf6d5c31b8fc5b227e66f71c6196) where     σ σ  ( W )   {\displaystyle \sigma (W)}  ![{\displaystyle \sigma (W)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f89efda565839c985b5320de98bd98b88c1cfd90) is the [eigenvalues](./Eigenvalues_and_eigenvectors) in the [singular value decomposition](./Singular_value_decomposition) of     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7).

 

### Mean-constrained regularization

 

    R (  f  1   ⋯ ⋯   f  T   ) =  ∑ ∑   t = 1   T     ‖   f  t   − −    1 T    ∑ ∑   s = 1   T    f  s    ‖    H  k     2     {\displaystyle R(f_{1}\cdots f_{T})=\sum _{t=1}^{T}\left\|f_{t}-{\frac {1}{T}}\sum _{s=1}^{T}f_{s}\right\|_{H_{k}}^{2}}  ![{\displaystyle R(f_{1}\cdots f_{T})=\sum _{t=1}^{T}\left\|f_{t}-{\frac {1}{T}}\sum _{s=1}^{T}f_{s}\right\|_{H_{k}}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4681ac499974cbdb666145ff3f14911acc8ff1e6)

 

This regularizer constrains the functions learned for each task to be similar to the overall average of the functions across all tasks. This is useful for expressing prior information that each task is expected to share with each other task. An example is predicting blood iron levels measured at different times of the day, where each task represents an individual.

 

### Clustered mean-constrained regularization

 

    R (  f  1   ⋯ ⋯   f  T   ) =  ∑ ∑   r = 1   C    ∑ ∑   t ∈ ∈  I ( r )     ‖   f  t   − −    1  I ( r )     ∑ ∑   s ∈ ∈  I ( r )    f  s    ‖    H  k     2     {\displaystyle R(f_{1}\cdots f_{T})=\sum _{r=1}^{C}\sum _{t\in I(r)}\left\|f_{t}-{\frac {1}{I(r)}}\sum _{s\in I(r)}f_{s}\right\|_{H_{k}}^{2}}  ![{\displaystyle R(f_{1}\cdots f_{T})=\sum _{r=1}^{C}\sum _{t\in I(r)}\left\|f_{t}-{\frac {1}{I(r)}}\sum _{s\in I(r)}f_{s}\right\|_{H_{k}}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d6bab94e0fff842586619d95058486db18612fe4) where     I ( r )   {\displaystyle I(r)}  ![{\displaystyle I(r)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43eabce3279a8b35ce65904e1bc775fb78e931f5) is a cluster of tasks.

 

This regularizer is similar to the mean-constrained regularizer, but instead enforces similarity between tasks within the same cluster. This can capture more complex prior information. This technique has been used to predict [Netflix](./Netflix) recommendations. A cluster would correspond to a group of people who share similar preferences.

 

### Graph-based similarity

 

More generally than above, similarity between tasks can be defined by a function. The regularizer encourages the model to learn similar functions for similar tasks.
    R (  f  1   ⋯ ⋯   f  T   ) =  ∑ ∑   t , s = 1 , t ≠ ≠  s    T      ‖   f  t   − −   f  s    ‖   2    M  t s     {\displaystyle R(f_{1}\cdots f_{T})=\sum _{t,s=1,t\neq s}^{\mathsf {T}}\left\|f_{t}-f_{s}\right\|^{2}M_{ts}}  ![{\displaystyle R(f_{1}\cdots f_{T})=\sum _{t,s=1,t\neq s}^{\mathsf {T}}\left\|f_{t}-f_{s}\right\|^{2}M_{ts}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3459e10d61e621b82c76faf683fb48709fddd9c3) for a given symmetric [similarity matrix](./Similarity_matrix)     M   {\displaystyle M}  ![{\displaystyle M}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f82cade9898ced02fdd08712e5f0c0151758a0dd).

 

## Other uses of regularization in statistics and machine learning

 

[Bayesian learning](./Bayesian_model_comparison) methods make use of a [prior probability](./Prior_probability) that (usually) gives lower probability to more complex models. Well-known model selection techniques include the [Akaike information criterion](./Akaike_information_criterion) (AIC), [minimum description length](./Minimum_description_length) (MDL), and the [Bayesian information criterion](./Bayesian_information_criterion) (BIC). Alternative methods of controlling overfitting not involving regularization include [cross-validation](./Cross-validation_(statistics)).

 

Examples of applications of different methods of regularization to the [linear model](./Linear_model) are:

 
| Model | Fit measure | Entropy measure[6][9] |
| --- | --- | --- |
| AIC/BIC | ‖Y−Xβ‖2{\displaystyle \left\|Y-X\beta \right\|_{2}} | ‖β‖0{\displaystyle \left\|\beta \right\|_{0}} |
| Lasso[10] | ‖Y−Xβ‖2{\displaystyle \left\|Y-X\beta \right\|_{2}} | ‖β‖1{\displaystyle \left\|\beta \right\|_{1}} |
| Ridge regression[11] | ‖Y−Xβ‖2{\displaystyle \left\|Y-X\beta \right\|_{2}} | ‖β‖2{\displaystyle \left\|\beta \right\|_{2}} |
| Basis pursuit denoising | ‖Y−Xβ‖2{\displaystyle \left\|Y-X\beta \right\|_{2}} | λ‖β‖1{\displaystyle \lambda \left\|\beta \right\|_{1}} |
| Rudin–Osher–Fatemi model (TV) | ‖Y−Xβ‖2{\displaystyle \left\|Y-X\beta \right\|_{2}} | λ‖∇β‖1{\displaystyle \lambda \left\|\nabla \beta \right\|_{1}} |
| Potts model | ‖Y−Xβ‖2{\displaystyle \left\|Y-X\beta \right\|_{2}} | λ‖∇β‖0{\displaystyle \lambda \left\|\nabla \beta \right\|_{0}} |
| RLAD[12] | ‖Y−Xβ‖1{\displaystyle \left\|Y-X\beta \right\|_{1}} | ‖β‖1{\displaystyle \left\|\beta \right\|_{1}} |
| Dantzig Selector[13] | ‖XT(Y−Xβ)‖∞{\displaystyle \left\|X^{\mathsf {T}}(Y-X\beta )\right\|_{\infty }} | ‖β‖1{\displaystyle \left\|\beta \right\|_{1}} |
| SLOPE[14] | ‖Y−Xβ‖2{\displaystyle \left\|Y-X\beta \right\|_{2}} | ∑i=1pλi|β|(i){\displaystyle \sum _{i=1}^{p}\lambda _{i}\left|\beta \right|_{(i)}} |

 

## See also

 
- [Bayesian interpretation of regularization](./Bayesian_interpretation_of_regularization)
- [Bias–variance tradeoff](./Bias–variance_tradeoff)
- [Matrix regularization](./Matrix_regularization)
- [Regularization by spectral filtering](./Regularization_by_spectral_filtering)
- [Regularized least squares](./Regularized_least_squares)
- [Lagrange multiplier](./Lagrange_multiplier)
- [Variance reduction](./Variance_reduction)
- [L-curve](./L-curve)

 

## Notes

  
1. [↑](./Regularization_(mathematics)#cite_ref-1) Kratsios, Anastasis (2020). ["Deep Arbitrage-Free Learning in a Generalized HJM Framework via Arbitrage-Regularization Data"](https://doi.org/10.3390%2Frisks8020040). *Risks*. **8** (2): [](https://www.mdpi.com/2227-9091/8/2/40). [arXiv](./ArXiv_(identifier)):[1710.05114](https://arxiv.org/abs/1710.05114). [doi](./Doi_(identifier)):[10.3390/risks8020040](https://doi.org/10.3390%2Frisks8020040). [hdl](./Hdl_(identifier)):[20.500.11850/456375](https://hdl.handle.net/20.500.11850%2F456375). Term structure models can be regularized to remove arbitrage opportunities [*[sic](./Sic)?*].
2. [↑](./Regularization_(mathematics)#cite_ref-2) Bühlmann, Peter; Van De Geer, Sara (2011). [*Statistics for High-Dimensional Data*](https://archive.org/details/statisticsforhig00bhlm). Springer Series in Statistics. p. [9](https://archive.org/details/statisticsforhig00bhlm/page/n27). [doi](./Doi_(identifier)):[10.1007/978-3-642-20192-9](https://doi.org/10.1007%2F978-3-642-20192-9). [ISBN](./ISBN_(identifier)) [978-3-642-20191-2](./Special:BookSources/978-3-642-20191-2). If p > n, the ordinary least squares estimator is not unique and will heavily overfit the data. Thus, a form of complexity regularization will be necessary.
3. [↑](./Regularization_(mathematics)#cite_ref-3) Huang, Yunfei.; et al. (2019). ["Traction force microscopy with optimized regularization and automated Bayesian parameter selection for comparing cells"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6345967). *Scientific Reports*. **9** (1) 539: 537. [arXiv](./ArXiv_(identifier)):[1810.05848](https://arxiv.org/abs/1810.05848). [Bibcode](./Bibcode_(identifier)):[2019NatSR...9..539H](https://ui.adsabs.harvard.edu/abs/2019NatSR...9..539H). [doi](./Doi_(identifier)):[10.1038/s41598-018-36896-x](https://doi.org/10.1038%2Fs41598-018-36896-x). [PMC](./PMC_(identifier)) [6345967](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6345967). [PMID](./PMID_(identifier)) [30679578](https://pubmed.ncbi.nlm.nih.gov/30679578).
4. [↑](./Regularization_(mathematics)#cite_ref-4) Goodfellow, Ian; Bengio, Yoshua; Courville, Aaron. [*Deep Learning Book*](https://www.deeplearningbook.org/contents/ml.html). Retrieved 2021-01-29.
5. [1](./Regularization_(mathematics)#cite_ref-:1_5-0) [2](./Regularization_(mathematics)#cite_ref-:1_5-1) [3](./Regularization_(mathematics)#cite_ref-:1_5-2) [4](./Regularization_(mathematics)#cite_ref-:1_5-3) Guo, Jingru. ["AI Notes: Regularizing neural networks"](https://deeplearning.ai/ai-notes/regularization/). *[deeplearning.ai](./Deeplearning.ai?action=edit&redlink=1)*. Retrieved 2024-02-04.
6. [1](./Regularization_(mathematics)#cite_ref-:0_6-0) [2](./Regularization_(mathematics)#cite_ref-:0_6-1) Bishop, Christopher M. (2007). *Pattern recognition and machine learning* (Corr. printing. ed.). New York: Springer. [ISBN](./ISBN_(identifier)) [978-0-387-31073-2](./Special:BookSources/978-0-387-31073-2).
7. [↑](./Regularization_(mathematics)#cite_ref-7) For the connection between [maximum a posteriori estimation](./Maximum_a_posteriori_estimation) and [ridge regression](./Ridge_regression), see Weinberger, Kilian (July 11, 2018). ["Linear / Ridge Regression"](https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote08.html#map-estimate). *CS4780 Machine Learning Lecture 13*. Cornell.
8. [↑](./Regularization_(mathematics)#cite_ref-8) Natarajan, B. (1995-04-01). ["Sparse Approximate Solutions to Linear Systems"](http://epubs.siam.org/doi/abs/10.1137/S0097539792240406). *SIAM Journal on Computing*. **24** (2): 227–234. [doi](./Doi_(identifier)):[10.1137/S0097539792240406](https://doi.org/10.1137%2FS0097539792240406). [ISSN](./ISSN_(identifier)) [0097-5397](https://search.worldcat.org/issn/0097-5397). [S2CID](./S2CID_(identifier)) [2072045](https://api.semanticscholar.org/CorpusID:2072045).
9. [↑](./Regularization_(mathematics)#cite_ref-9) Duda, Richard O. (2004). *Pattern classification + computer manual : hardcover set* (2 ed.). New York [u.a.]: Wiley. [ISBN](./ISBN_(identifier)) [978-0-471-70350-1](./Special:BookSources/978-0-471-70350-1).
10. [↑](./Regularization_(mathematics)#cite_ref-10) Tibshirani, Robert (1996). ["Regression Shrinkage and Selection via the Lasso"](https://web.archive.org/web/20081031180255/http://www-stat.stanford.edu/~tibs/ftp/lasso.ps). *[Journal of the Royal Statistical Society, Series B](./Journal_of_the_Royal_Statistical_Society,_Series_B)*. **58** (1): 267–288. [doi](./Doi_(identifier)):[10.1111/j.2517-6161.1996.tb02080.x](https://doi.org/10.1111%2Fj.2517-6161.1996.tb02080.x). [MR](./MR_(identifier)) [1379242](https://mathscinet.ams.org/mathscinet-getitem?mr=1379242). Archived from [the original](http://www-stat.stanford.edu/~tibs/ftp/lasso.ps) ([PostScript](./PostScript)) on 2008-10-31. Retrieved 2009-03-19.
11. [↑](./Regularization_(mathematics)#cite_ref-ridge_11-0) Arthur E. Hoerl; Robert W. Kennard (1970). "Ridge regression: Biased estimation for nonorthogonal problems". *Technometrics*. **12** (1): 55–67. [doi](./Doi_(identifier)):[10.2307/1267351](https://doi.org/10.2307%2F1267351). [JSTOR](./JSTOR_(identifier)) [1267351](https://www.jstor.org/stable/1267351).
12. [↑](./Regularization_(mathematics)#cite_ref-12) Li Wang; Michael D. Gordon; Ji Zhu (2006). "Regularized Least Absolute Deviations Regression and an Efficient Algorithm for Parameter Tuning". *Sixth International Conference on Data Mining*. pp. 690–700. [doi](./Doi_(identifier)):[10.1109/ICDM.2006.134](https://doi.org/10.1109%2FICDM.2006.134). [ISBN](./ISBN_(identifier)) [978-0-7695-2701-7](./Special:BookSources/978-0-7695-2701-7).
13. [↑](./Regularization_(mathematics)#cite_ref-13) [Candes, Emmanuel](./Emmanuel_Candès); [Tao, Terence](./Terence_Tao) (2007). "The Dantzig selector: Statistical estimation when *p* is much larger than *n*". *Annals of Statistics*. **35** (6): 2313–2351. [arXiv](./ArXiv_(identifier)):[math/0506081](https://arxiv.org/abs/math/0506081). [doi](./Doi_(identifier)):[10.1214/009053606000001523](https://doi.org/10.1214%2F009053606000001523). [MR](./MR_(identifier)) [2382644](https://mathscinet.ams.org/mathscinet-getitem?mr=2382644). [S2CID](./S2CID_(identifier)) [88524200](https://api.semanticscholar.org/CorpusID:88524200).
14. [↑](./Regularization_(mathematics)#cite_ref-14)  [Małgorzata Bogdan](./Małgorzata_Bogdan); Ewout van den Berg; Weijie Su; Emmanuel J. Candes (2013). "Statistical estimation and testing via the ordered L1 norm". [arXiv](./ArXiv_(identifier)):[1310.1969](https://arxiv.org/abs/1310.1969) [[stat.ME](https://arxiv.org/archive/stat.ME)].

 

## References

 
- Neumaier, A. (1998). ["Solving ill-conditioned and singular linear systems: A tutorial on regularization"](https://web.archive.org/web/20070630163742/https://www.mat.univie.ac.at/~neum/ms/regtutorial.pdf) (PDF). *SIAM Review*. **40** (3): 636–666. [Bibcode](./Bibcode_(identifier)):[1998SIAMR..40..636N](https://ui.adsabs.harvard.edu/abs/1998SIAMR..40..636N). [doi](./Doi_(identifier)):[10.1137/S0036144597321909](https://doi.org/10.1137%2FS0036144597321909). Archived from [the original](https://www.mat.univie.ac.at/~neum/ms/regtutorial.pdf) (PDF) on 2007-06-30.
- Kukačka, Jan; Golkov, Vladimir; Cremers, Daniel (2017). "Regularization for Deep Learning: A Taxonomy". [arXiv](./ArXiv_(identifier)):[1710.10686](https://arxiv.org/abs/1710.10686) [[cs.LG](https://arxiv.org/archive/cs.LG)].

 
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