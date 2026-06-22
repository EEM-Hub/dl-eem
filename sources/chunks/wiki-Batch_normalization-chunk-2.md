---
source: sources/wiki-Batch_normalization.md
source_url: https://en.wikipedia.org/wiki/Batch_normalization
chunk: 2/4
---

## Theory

 

Although batch normalization has become popular due to its strong empirical performance, the working mechanism of the method is not yet well-understood. The explanation made in the original paper[[1]](./Batch_normalization#cite_note-:0-1) was that batch norm works by reducing internal covariate shift, but this has been challenged by more recent work. One experiment[[5]](./Batch_normalization#cite_note-:1-5) trained a [VGG-16](./VGGNet) network[[6]](./Batch_normalization#cite_note-VGG-6) under 3 different training regimes: standard (no batch norm), batch norm, and batch norm with noise added to each layer during training. In the third model, the noise has non-zero mean and non-unit variance, i.e. it explicitly introduces covariate shift. Despite this, it showed similar accuracy to the second model, and both performed better than the first, suggesting that covariate shift is not the reason that batch norm improves performance.

 

Using batch normalization causes the items in a batch to no longer be [iid](./Independent_and_identically_distributed_random_variables), which can lead to difficulties in training due to lower quality gradient estimation.[[7]](./Batch_normalization#cite_note-7)

 

### Smoothness

 

One alternative explanation[[5]](./Batch_normalization#cite_note-:1-5) is that the improvement with batch normalization is instead due to producing a smoother parameter space and smoother gradients, as formalized by a smaller [Lipschitz constant](./Lipschitz_continuity). 

 

Consider two identical networks, one contains batch normalization layers and the other does not, the behaviors of these two networks are then compared. Denote the loss functions as        L ^ ^       {\displaystyle {\hat {L}}}  ![{\displaystyle {\hat {L}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c5914e99ad679b0a2d962ea00e6167a20ff0d4ce) and     L   {\displaystyle L}  ![{\displaystyle L}](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8), respectively. Let the input to both networks be     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), and the output be     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d), for which     y = W x   {\displaystyle y=Wx}  ![{\displaystyle y=Wx}](https://wikimedia.org/api/rest_v1/media/math/render/svg/17f279b02105527ae737f6379828d2ca382b69e0), where     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7) is the layer weights. For the second network,     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) additionally goes through a batch normalization layer. Denote the normalized activation as        y ^ ^       {\displaystyle {\hat {y}}}  ![{\displaystyle {\hat {y}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3dc8de3d8ea01304329ef9518fad7a6d196c4c01), which has zero mean and unit variance. Let the transformed activation be     z = γ γ     y ^ ^     + β β    {\displaystyle z=\gamma {\hat {y}}+\beta }  ![{\displaystyle z=\gamma {\hat {y}}+\beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/2cf9bf09cfb9fdb93161e82b93e61d1e1b724b6c), and suppose     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a) and     β β    {\displaystyle \beta }  ![{\displaystyle \beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) are constants. Finally, denote the standard deviation over a mini-batch         y  j   ^ ^     ∈ ∈    R   m     {\displaystyle {\hat {y_{j}}}\in \mathbb {R} ^{m}}  ![{\displaystyle {\hat {y_{j}}}\in \mathbb {R} ^{m}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a8527f733bd4c01bd2aeb0b1cb8eecd026e27649) as      σ σ   j     {\displaystyle \sigma _{j}}  ![{\displaystyle \sigma _{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a234b1f289568934f127c2dd68ba77b6ef3f3569).

 

First, it can be shown that the gradient magnitude of a batch normalized network,      |   |   ▽ ▽    y  i        L ^ ^      |   |    {\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||}  ![{\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47443c58f1c9ffb4509b6688b28030172e35d79e), is bounded, with the bound expressed as

 

     |   |   ▽ ▽    y  i        L ^ ^      |    |   2   ≤ ≤     γ γ   2    σ σ   j   2       (    |   |   ▽ ▽    y  i     L  |    |   2   − −    1 m   ⟨ ⟨  1 ,  ▽ ▽    y  i     L  ⟩ ⟩   2   − −    1 m   ⟨ ⟨   ▽ ▽    y  i     L ,     y ^ ^      j    ⟩ ⟩   2     )     {\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||^{2}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}{\Bigg (}||\triangledown _{y_{i}}L||^{2}-{\frac {1}{m}}\langle 1,\triangledown _{y_{i}}L\rangle ^{2}-{\frac {1}{m}}\langle \triangledown _{y_{i}}L,{\hat {y}}_{j}\rangle ^{2}{\bigg )}}  ![{\displaystyle ||\triangledown _{y_{i}}{\hat {L}}||^{2}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}{\Bigg (}||\triangledown _{y_{i}}L||^{2}-{\frac {1}{m}}\langle 1,\triangledown _{y_{i}}L\rangle ^{2}-{\frac {1}{m}}\langle \triangledown _{y_{i}}L,{\hat {y}}_{j}\rangle ^{2}{\bigg )}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba3c5121143fe7afbff0230f491dba07a1c02c61).

 

Since the gradient magnitude represents the Lipschitzness of the loss, this relationship indicates that a batch normalized network could achieve greater Lipschitzness comparatively. Notice that the bound gets tighter when the gradient      ▽ ▽    y  i        L ^ ^       {\displaystyle \triangledown _{y_{i}}{\hat {L}}}  ![{\displaystyle \triangledown _{y_{i}}{\hat {L}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a386fa35b81502006040e9ea35d424dd997b71cf) correlates with the activation         y  i   ^ ^       {\displaystyle {\hat {y_{i}}}}  ![{\displaystyle {\hat {y_{i}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/84e9f46b496de85491c3227866df492db14c09fb), which is a common phenomena. The scaling of        γ γ   2    σ σ   j   2       {\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}  ![{\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eee6c2b2c2b869c353530cac7ed593c6fadd0ed1) is also significant, since the variance is often large.

 

Secondly, the quadratic form of the loss Hessian with respect to activation in the gradient direction can be bounded as

 

    (  ▽ ▽    y  j        L ^ ^      )  T      ∂ ∂     L ^ ^       ∂ ∂   y  j   ∂ ∂   y  j      (  ▽ ▽    y  j        L ^ ^     ) ≤ ≤     γ γ   2    σ σ   2       (      ∂ ∂     L ^ ^       ∂ ∂   y  j         )    T     (      ∂ ∂  L   ∂ ∂   y  j   ∂ ∂   y  j        )     (      ∂ ∂     L ^ ^       ∂ ∂   y  j        )   − −    γ γ   m  σ σ   2      ⟨ ⟨   ▽ ▽    y  j     L ,     y  j   ^ ^     ⟩ ⟩    |     |      ∂ ∂     L ^ ^       ∂ ∂   y  j        |      |    2     {\displaystyle (\triangledown _{y_{j}}{\hat {L}})^{T}{\frac {\partial {\hat {L}}}{\partial y_{j}\partial y_{j}}}(\triangledown _{y_{j}}{\hat {L}})\leq {\frac {\gamma ^{2}}{\sigma ^{2}}}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}^{T}{\bigg (}{\frac {\partial L}{\partial y_{j}\partial y_{j}}}{\bigg )}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}-{\frac {\gamma }{m\sigma ^{2}}}\langle \triangledown _{y_{j}}L,{\hat {y_{j}}}\rangle {\bigg |}{\bigg |}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg |}{\bigg |}^{2}}  ![{\displaystyle (\triangledown _{y_{j}}{\hat {L}})^{T}{\frac {\partial {\hat {L}}}{\partial y_{j}\partial y_{j}}}(\triangledown _{y_{j}}{\hat {L}})\leq {\frac {\gamma ^{2}}{\sigma ^{2}}}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}^{T}{\bigg (}{\frac {\partial L}{\partial y_{j}\partial y_{j}}}{\bigg )}{\bigg (}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg )}-{\frac {\gamma }{m\sigma ^{2}}}\langle \triangledown _{y_{j}}L,{\hat {y_{j}}}\rangle {\bigg |}{\bigg |}{\frac {\partial {\hat {L}}}{\partial y_{j}}}{\bigg |}{\bigg |}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/598ba229b7a7a25cdeaf500a84d1b8c1fdda5fc8).

 

The scaling of        γ γ   2    σ σ   j   2       {\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}  ![{\displaystyle {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eee6c2b2c2b869c353530cac7ed593c6fadd0ed1) indicates that the loss Hessian is resilient to the mini-batch variance, whereas the second term on the right hand side suggests that it becomes smoother when the [Hessian](./Hessian_matrix) and the inner product are non-negative. If the loss is locally [convex](./Convex_function), then the Hessian is [positive semi-definite](./Positive_semidefinite_matrix), while the inner product is positive if         g  j   ^ ^       {\displaystyle {\hat {g_{j}}}}  ![{\displaystyle {\hat {g_{j}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cbd3bc5d8e75dc374257ba8018dd9f23476ee33c) is in the direction towards the minimum of the loss. It could thus be concluded from this inequality that the gradient generally becomes more predictive with the batch normalization layer.

 

It then follows to translate the bounds related to the loss with respect to the normalized activation to a bound on the loss with respect to the network weights:

 

        g  j   ^ ^     ≤ ≤     γ γ   2    σ σ   j   2     (  g  j   2   − −  m  μ μ    g  j     2   − −   λ λ   2   ⟨ ⟨   ▽ ▽    y  j     L ,     y ^ ^      j    ⟩ ⟩   2   )   {\displaystyle {\hat {g_{j}}}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}(g_{j}^{2}-m\mu _{g_{j}}^{2}-\lambda ^{2}\langle \triangledown _{y_{j}}L,{\hat {y}}_{j}\rangle ^{2})}  ![{\displaystyle {\hat {g_{j}}}\leq {\frac {\gamma ^{2}}{\sigma _{j}^{2}}}(g_{j}^{2}-m\mu _{g_{j}}^{2}-\lambda ^{2}\langle \triangledown _{y_{j}}L,{\hat {y}}_{j}\rangle ^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c94b8189deaf786bb78f83dcb51f2bc422cfffbc), where      g  j   = m a  x   |   |  X  |   |  ≤ ≤  λ λ     |   |   ▽ ▽   W   L  |    |   2     {\displaystyle g_{j}=max_{||X||\leq \lambda }||\triangledown _{W}L||^{2}}  ![{\displaystyle g_{j}=max_{||X||\leq \lambda }||\triangledown _{W}L||^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5f76d93a70a9de73a91da4c44769bc7a720c3bb0) and         g ^ ^      j   = m a  x   |   |  X  |   |  ≤ ≤  λ λ     |   |   ▽ ▽   W      L ^ ^      |    |   2     {\displaystyle {\hat {g}}_{j}=max_{||X||\leq \lambda }||\triangledown _{W}{\hat {L}}||^{2}}  ![{\displaystyle {\hat {g}}_{j}=max_{||X||\leq \lambda }||\triangledown _{W}{\hat {L}}||^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a1c5032bb8d3a7aa61a390c748e95ada0599d670).

 

In addition to the smoother landscape, it is further shown that batch normalization could result in a better initialization with the following inequality:

 

     |   |   W  0   − −      W ^ ^      ∗ ∗     |    |   2   ≤ ≤   |   |   W  0   − −   W  ∗ ∗     |    |   2   − −    1   |   |   W  ∗ ∗     |    |   2      (  |   |   W  ∗ ∗     |    |   2   − −  ⟨ ⟨   W  ∗ ∗    ,  W  0   ⟩ ⟩   )  2     {\displaystyle ||W_{0}-{\hat {W}}^{*}||^{2}\leq ||W_{0}-W^{*}||^{2}-{\frac {1}{||W^{*}||^{2}}}(||W^{*}||^{2}-\langle W^{*},W_{0}\rangle )^{2}}  ![{\displaystyle ||W_{0}-{\hat {W}}^{*}||^{2}\leq ||W_{0}-W^{*}||^{2}-{\frac {1}{||W^{*}||^{2}}}(||W^{*}||^{2}-\langle W^{*},W_{0}\rangle )^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9ac3bd274bf4ea26d42044bf5f0f1fa130174fa6), where      W  ∗ ∗      {\displaystyle W^{*}}  ![{\displaystyle W^{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5292cb3dbf333bb0b51f39fb9f724fa8d4dfcc63) and         W ^ ^      ∗ ∗      {\displaystyle {\hat {W}}^{*}}  ![{\displaystyle {\hat {W}}^{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a9f598335a95fd9cc1d7eb039fd9ca278165a96c) are the local optimal weights for the two networks, respectively.

 

Some scholars argue that the above analysis cannot fully capture the performance of batch normalization, because the proof only concerns the largest eigenvalue, or equivalently, one direction in the landscape at all points. It is suggested that the complete eigenspectrum needs to be taken into account to make a conclusive analysis.[[8]](./Batch_normalization#cite_note-:2-8)[[5]](./Batch_normalization#cite_note-:1-5)

 

### Measure

 

Since it is hypothesized that batch normalization layers could reduce internal covariate shift, an experiment[*[citation needed](./Wikipedia:Citation_needed)*] is set up to measure quantitatively how much covariate shift is reduced. First, the notion of internal covariate shift needs to be defined mathematically. Specifically, to quantify the adjustment that a layer's parameters make in response to updates in previous layers, the correlation between the gradients of the loss before and after all previous layers are updated is measured, since gradients could capture the shifts from the first-order training method. If the shift introduced by the changes in previous layers is small, then the correlation between the gradients would be close to 1.

 

The correlation between the gradients are computed for four models: a standard [VGG network](./VGGNet),[[6]](./Batch_normalization#cite_note-VGG-6) a VGG network with batch normalization layers, a 25-layer deep linear network (DLN) trained with full-batch gradient descent, and a DLN network with batch normalization layers. Interestingly, it is shown that the standard VGG and DLN models both have higher correlations of gradients compared with their counterparts, indicating that the additional batch normalization layers are not reducing internal covariate shift.

 

### Vanishing/exploding gradients

 

Even though batch norm was originally introduced to alleviate [gradient vanishing or explosion problems](./Vanishing_gradient_problem), a deep batch norm network in fact *suffers from gradient explosion* at initialization time, no matter what it uses for nonlinearity. Thus, the optimization landscape is very far from smooth for a randomly initialized, deep batch norm network.
More precisely, if the network has     L   {\displaystyle L}  ![{\displaystyle L}](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8) layers, then the gradient of the first layer weights has norm     > c  λ λ   L     {\displaystyle >c\lambda ^{L}}  ![{\displaystyle >c\lambda ^{L}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cab76f58a7a5dccf0f9ed0c5d78e1db2fb2f7435) for some     λ λ  > 1 , c > 0   {\displaystyle \lambda >1,c>0}  ![{\displaystyle \lambda >1,c>0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/afd304b28687ea62f39b2a8fc2fb7916aa8eb531) depending only on the nonlinearity.
For any fixed nonlinearity,     λ λ    {\displaystyle \lambda }  ![{\displaystyle \lambda }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b43d0ea3c9c025af1be9128e62a18fa74bedda2a) decreases as the batch size increases. For example, for ReLU,     λ λ    {\displaystyle \lambda }  ![{\displaystyle \lambda }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b43d0ea3c9c025af1be9128e62a18fa74bedda2a) decreases to     π π   /  ( π π  − −  1 ) ≈ ≈  1.467   {\displaystyle \pi /(\pi -1)\approx 1.467}  ![{\displaystyle \pi /(\pi -1)\approx 1.467}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e3922a4b656e6d4281f61c029cb1c8b0943cc72) as the batch size tends to infinity.
Practically, this means deep batch norm networks are untrainable.
This is only relieved by skip connections in the fashion of [residual networks](./Residual_neural_network).[[9]](./Batch_normalization#cite_note-:7-9)

 

This gradient explosion on the surface contradicts the *smoothness* property explained in the previous section, but in fact they are consistent. The previous section studies the effect of inserting a single batch norm in a network, while the gradient explosion depends on stacking batch norms typical of modern deep neural networks.

 

### Decoupling

 

Another possible reason for the success of batch normalization is that it [decouples](./Decoupling_(probability)) the length and direction of the weight vectors and thus facilitates better training.

 

By interpreting batch norm as a reparametrization of weight space, it can be shown that the length and the direction of the weights are separated and can thus be trained separately. For a particular neural network unit with input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) and weight vector     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6), denote its output as     f ( w ) =  E  x   [ ϕ ϕ  (  x  T   w ) ]   {\displaystyle f(w)=E_{x}[\phi (x^{T}w)]}  ![{\displaystyle f(w)=E_{x}[\phi (x^{T}w)]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/870188d380627f799e598e056ea71b4c23815741), where     ϕ ϕ    {\displaystyle \phi }  ![{\displaystyle \phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/72b1f30316670aee6270a28334bdf4f5072cdde4) is the activation function, and denote     S = E [ x  x  T   ]   {\displaystyle S=E[xx^{T}]}  ![{\displaystyle S=E[xx^{T}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/71f3a47dfa9441a4050edac91329e66ac747684b). Assume that     E [ x ] = 0   {\displaystyle E[x]=0}  ![{\displaystyle E[x]=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f464a09bd74ae67c6e8094c223aa1edd093699c9), and that the [spectrum](./Spectrum_of_a_matrix) of the matrix     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) is bounded as     0 < μ μ  =  λ λ   m i n   ( S )   {\displaystyle 0<\mu =\lambda _{min}(S)}  ![{\displaystyle 0<\mu =\lambda _{min}(S)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c780462af127d32b872a60841bd24c25da8ea6d9),     L =  λ λ   m a x   ( S ) < ∞ ∞    {\displaystyle L=\lambda _{max}(S)<\infty }  ![{\displaystyle L=\lambda _{max}(S)<\infty }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3c7406de80618dc4081e9c8881339b56595e992), such that     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) is symmetric positive definite. Adding batch normalization to this unit thus results in

 

     f  B N   ( w , γ γ  , β β  ) =  E  x   [ ϕ ϕ  ( B N (  x  T   w ) ) ] =  E  x     [   ϕ ϕ    (   γ γ  (     x  T   w − −   E  x   [  x  T   w ]   v a  r  x   [  x  T   w  ]  1  /  2      ) + β β    )     ]     {\displaystyle f_{BN}(w,\gamma ,\beta )=E_{x}[\phi (BN(x^{T}w))]=E_{x}{\bigg [}\phi {\bigg (}\gamma ({\frac {x^{T}w-E_{x}[x^{T}w]}{var_{x}[x^{T}w]^{1/2}}})+\beta {\bigg )}{\bigg ]}}  ![{\displaystyle f_{BN}(w,\gamma ,\beta )=E_{x}[\phi (BN(x^{T}w))]=E_{x}{\bigg [}\phi {\bigg (}\gamma ({\frac {x^{T}w-E_{x}[x^{T}w]}{var_{x}[x^{T}w]^{1/2}}})+\beta {\bigg )}{\bigg ]}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ef3c8776e25fec4bb27c4e556fafeda7d35686a3), by definition.

 

The variance term can be simplified such that     v a  r  x   [  x  T   w ] =  w  T   S w   {\displaystyle var_{x}[x^{T}w]=w^{T}Sw}  ![{\displaystyle var_{x}[x^{T}w]=w^{T}Sw}](https://wikimedia.org/api/rest_v1/media/math/render/svg/64581f03bf8607566e4f8126ce8822e23ca4454d). Assume that     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) has zero mean and     β β    {\displaystyle \beta }  ![{\displaystyle \beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) can be omitted, then it follows that

 

     f  B N   ( w , γ γ  ) =  E  x     [   ϕ ϕ    (   γ γ      x  T   w   (  w  T   S w  )  1  /  2        )     ]     {\displaystyle f_{BN}(w,\gamma )=E_{x}{\bigg [}\phi {\bigg (}\gamma {\frac {x^{T}w}{(w^{T}Sw)^{1/2}}}{\bigg )}{\bigg ]}}  ![{\displaystyle f_{BN}(w,\gamma )=E_{x}{\bigg [}\phi {\bigg (}\gamma {\frac {x^{T}w}{(w^{T}Sw)^{1/2}}}{\bigg )}{\bigg ]}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8073fc1cb01c6722a53258ee44d8ad020f8b1e6f), where     (  w  T   S w  )   1 2      {\displaystyle (w^{T}Sw)^{\frac {1}{2}}}  ![{\displaystyle (w^{T}Sw)^{\frac {1}{2}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/83a8fad691375fdec2a94f2a066f155172c6045b) is the induced norm of     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2),      |   |  w  |    |   s     {\displaystyle ||w||_{s}}  ![{\displaystyle ||w||_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d0357dc403927cc26418f5ccbe598f35d7b65606).

 

Hence, it could be concluded that      f  B N   ( w , γ γ  ) =  E  x   [ ϕ ϕ  (  x  T      w ~ ~     ) ]   {\displaystyle f_{BN}(w,\gamma )=E_{x}[\phi (x^{T}{\tilde {w}})]}  ![{\displaystyle f_{BN}(w,\gamma )=E_{x}[\phi (x^{T}{\tilde {w}})]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0479b5ef1b32a46c9837a35b2e6746a8a8b36803), where        w ~ ~     = γ γ    w   |   |  w  |    |   s        {\displaystyle {\tilde {w}}=\gamma {\frac {w}{||w||_{s}}}}  ![{\displaystyle {\tilde {w}}=\gamma {\frac {w}{||w||_{s}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fb18955e26cd1b8f38355e59f34f94b4dff6b2e), and     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a) and     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) account for its length and direction separately. This property could then be used to prove the faster convergence of problems with batch normalization.

 


