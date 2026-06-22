---
source: sources/wiki-Batch_normalization.md
source_url: https://en.wikipedia.org/wiki/Batch_normalization
chunk: 3/4
---

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

 


