---
source: sources/wiki-Regularization_mathematics.md
source_url: https://en.wikipedia.org/wiki/Regularization_(mathematics)
chunk: 2/3
---

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

 


