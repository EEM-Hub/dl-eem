---
source: sources/wiki-Autoencoder.md
source_url: https://en.wikipedia.org/wiki/Autoencoder
chunk: 2/4
---

## Variations

 

### Variational autoencoder (VAE)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/4a/VAE_Basic.png/330px-VAE_Basic.png)](./File:VAE_Basic.png)The basic scheme of a variational autoencoder. The model receives     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) as input. The encoder compresses it into the latent space. The decoder receives as input the information sampled from the latent space and produces       x ′     {\displaystyle {x'}}  ![{\displaystyle {x'}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223f94a9c179ffeb6e74e3208a27070a69f3f93) as similar as possible to     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4). Main article: [Variational autoencoder](./Variational_autoencoder) 

[Variational autoencoders](./Variational_autoencoder) (VAEs) belong to the families of [variational Bayesian methods](./Variational_Bayesian_methods). Despite the architectural similarities with basic autoencoders, VAEs are architected with different goals and have a different mathematical formulation. The latent space is, in this case, composed of a mixture of distributions instead of fixed vectors.

 

Given an input dataset     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) characterized by an unknown probability function     P ( x )   {\displaystyle P(x)}  ![{\displaystyle P(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/89833156eff2c51bfb8750db3306a0544ce34e14) and a multivariate latent encoding vector     z   {\displaystyle z}  ![{\displaystyle z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bf368e72c009decd9b6686ee84a375632e11de98), the objective is to model the data as a distribution      p  θ θ    ( x )   {\displaystyle p_{\theta }(x)}  ![{\displaystyle p_{\theta }(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1f0682b1f715edb12932100f59e93d012e4ec886), with     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af) defined as the set of the network parameters so that      p  θ θ    ( x ) =  ∫ ∫   z    p  θ θ    ( x , z ) d z   {\displaystyle p_{\theta }(x)=\int _{z}p_{\theta }(x,z)dz}  ![{\displaystyle p_{\theta }(x)=\int _{z}p_{\theta }(x,z)dz}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a18e1df9f777fee6a6ca3549ba5b1d014f689444).

 

### Sparse autoencoder (SAE)

Inspired by the [sparse coding](./Sparse_coding) hypothesis in neuroscience, *sparse autoencoders* (SAE) are variants of autoencoders, such that the codes      E  ϕ ϕ    ( x )   {\displaystyle E_{\phi }(x)}  ![{\displaystyle E_{\phi }(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d62337867b116b3895877e218f11ed8223e1d793) for messages tend to be *sparse codes*, that is,      E  ϕ ϕ    ( x )   {\displaystyle E_{\phi }(x)}  ![{\displaystyle E_{\phi }(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d62337867b116b3895877e218f11ed8223e1d793) is close to zero in most entries. Sparse autoencoders may include more (rather than fewer) hidden units than inputs, but only a small number of the hidden units are allowed to be active at the same time.[[12]](./Autoencoder#cite_note-domingos-12) Encouraging sparsity improves performance on classification tasks.[[13]](./Autoencoder#cite_note-:1-13) 

[![](//upload.wikimedia.org/wikipedia/commons/thumb/8/83/Autoencoder_sparso.png/250px-Autoencoder_sparso.png)](./File:Autoencoder_sparso.png)Simple schema of a single-layer sparse autoencoder. The hidden nodes in bright yellow are activated, while the light yellow ones are inactive. The activation depends on the input. 

There are two main ways to enforce sparsity. One way is to simply clamp all but the highest-k activations of the latent code to zero. This is the **k-sparse autoencoder**.[[13]](./Autoencoder#cite_note-:1-13)

 

The k-sparse autoencoder inserts the following "k-sparse function" in the latent layer of a standard autoencoder:     f  k   (  x  1   , . . . ,  x  n   ) = (  x  1    b  1   , . . . ,  x  n    b  n   )   {\displaystyle f_{k}(x_{1},...,x_{n})=(x_{1}b_{1},...,x_{n}b_{n})}  ![{\displaystyle f_{k}(x_{1},...,x_{n})=(x_{1}b_{1},...,x_{n}b_{n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e0230c8bdf0bbfd0c70e316b90d47ca6f180f5d6)where      b  i   = 1   {\displaystyle b_{i}=1}  ![{\displaystyle b_{i}=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be70edf0d554ce09ecff0b8c16e5a53a9c606a) if      |   x  i    |    {\displaystyle |x_{i}|}  ![{\displaystyle |x_{i}|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92da0dacc0f9f069128bdd9b4c7de82cf81c2aed) ranks in the top k, and 0 otherwise.

 

Backpropagating through      f  k     {\displaystyle f_{k}}  ![{\displaystyle f_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8a585492f646ca803bc408103a0c705dd67ab8b7) is simple: set gradient to 0 for      b  i   = 0   {\displaystyle b_{i}=0}  ![{\displaystyle b_{i}=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a1fdd6a52e2a95d37ce0fbccbb56dad6b4083a0) entries, and keep gradient for      b  i   = 1   {\displaystyle b_{i}=1}  ![{\displaystyle b_{i}=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e9be70edf0d554ce09ecff0b8c16e5a53a9c606a) entries. This is essentially a generalized [ReLU](./Rectifier_(neural_networks)) function.[[13]](./Autoencoder#cite_note-:1-13)

 

The other way is a [relaxed version](./Relaxation_(approximation)) of the k-sparse autoencoder. Instead of forcing sparsity, we add a **sparsity regularization loss**, then optimize for     min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  ) + λ λ   L  sparse   ( θ θ  , ϕ ϕ  )   {\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{sparse}}(\theta ,\phi )}  ![{\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{sparse}}(\theta ,\phi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e2b184d62f4d8db4863873eab8ed7a9e243f63a5)where     λ λ  > 0   {\displaystyle \lambda >0}  ![{\displaystyle \lambda >0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eea25afc0351140f919cf791c49c1964b8b081de) measures how much sparsity we want to enforce.[[14]](./Autoencoder#cite_note-:6-14)

 

Let the autoencoder architecture have     K   {\displaystyle K}  ![{\displaystyle K}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b76fce82a62ed5461908f0dc8f037de4e3686b0) layers. To define a sparsity regularization loss, we need a "desired" sparsity         ρ ρ  ^ ^      k     {\displaystyle {\hat {\rho }}_{k}}  ![{\displaystyle {\hat {\rho }}_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0f8abe27fcb896ed54b2f4926c7fe9a46dd25983) for each layer, a weight      w  k     {\displaystyle w_{k}}  ![{\displaystyle w_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac808de3e1f01ed40c69d4a350035b19ab28445f) for how much to enforce each sparsity, and a function     s : [ 0 , 1 ] × ×  [ 0 , 1 ] → →  [ 0 , ∞ ∞  ]   {\displaystyle s:[0,1]\times [0,1]\to [0,\infty ]}  ![{\displaystyle s:[0,1]\times [0,1]\to [0,\infty ]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0cd8c20f4b06b6eeddda1f90d5d1b5589ed8e6c3) to measure how much two sparsities differ.

 

For each input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), let the actual sparsity of activation in each layer     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) be     ρ ρ   k   ( x ) =   1 n    ∑ ∑   i = 1   n    a  k , i   ( x )   {\displaystyle \rho _{k}(x)={\frac {1}{n}}\sum _{i=1}^{n}a_{k,i}(x)}  ![{\displaystyle \rho _{k}(x)={\frac {1}{n}}\sum _{i=1}^{n}a_{k,i}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/484a083542fc48db444072c35bf7438b4f5f335f)where      a  k , i   ( x )   {\displaystyle a_{k,i}(x)}  ![{\displaystyle a_{k,i}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d8db682dad885500aaebe6308322fbebe44d482) is the activation in the     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) -th neuron of the     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) -th layer upon input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4).

 

The sparsity loss upon input     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) for one layer is     s (     ρ ρ  ^ ^      k   ,  ρ ρ   k   ( x ) )   {\displaystyle s({\hat {\rho }}_{k},\rho _{k}(x))}  ![{\displaystyle s({\hat {\rho }}_{k},\rho _{k}(x))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3727a598f770abd4f65df3e0abe7ac4929ac9027), and the sparsity regularization loss for the entire autoencoder is the expected weighted sum of sparsity losses:     L  sparse   ( θ θ  , ϕ ϕ  ) =    E    x ∼ ∼   μ μ   X      [   ∑ ∑   k ∈ ∈  1 : K    w  k   s (     ρ ρ  ^ ^      k   ,  ρ ρ   k   ( x ) )  ]    {\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}s({\hat {\rho }}_{k},\rho _{k}(x))\right]}  ![{\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}s({\hat {\rho }}_{k},\rho _{k}(x))\right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6384293aecb3ff69a6e8fee94b87546c533c4510)Typically, the function     s   {\displaystyle s}  ![{\displaystyle s}](https://wikimedia.org/api/rest_v1/media/math/render/svg/01d131dfd7673938b947072a13a9744fe997e632) is either the [Kullback–Leibler (KL) divergence](./Kullback–Leibler_divergence), as[[13]](./Autoencoder#cite_note-:1-13)[[14]](./Autoencoder#cite_note-:6-14)[[15]](./Autoencoder#cite_note-15)[[16]](./Autoencoder#cite_note-16)

     s ( ρ ρ  ,    ρ ρ  ^ ^     ) = K L ( ρ ρ   |   |     ρ ρ  ^ ^     ) = ρ ρ  log ⁡ ⁡    ρ ρ    ρ ρ  ^ ^      + ( 1 − −  ρ ρ  ) log ⁡ ⁡     1 − −  ρ ρ    1 − −     ρ ρ  ^ ^          {\displaystyle s(\rho ,{\hat {\rho }})=KL(\rho ||{\hat {\rho }})=\rho \log {\frac {\rho }{\hat {\rho }}}+(1-\rho )\log {\frac {1-\rho }{1-{\hat {\rho }}}}}  ![{\displaystyle s(\rho ,{\hat {\rho }})=KL(\rho ||{\hat {\rho }})=\rho \log {\frac {\rho }{\hat {\rho }}}+(1-\rho )\log {\frac {1-\rho }{1-{\hat {\rho }}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0460df1d442b4ccfb5d4e55243fe1ab5cb23e624) 

or the L1 loss, as     s ( ρ ρ  ,    ρ ρ  ^ ^     ) =  |  ρ ρ  − −     ρ ρ  ^ ^      |    {\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|}  ![{\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/97093ba0c58ecc04bd3c26a793b254cbd5ca0136), or the L2 loss, as     s ( ρ ρ  ,    ρ ρ  ^ ^     ) =  |  ρ ρ  − −     ρ ρ  ^ ^       |   2     {\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|^{2}}  ![{\displaystyle s(\rho ,{\hat {\rho }})=|\rho -{\hat {\rho }}|^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ee874b463a23a182bbd5c4cee0e25766262effdb).

 

Alternatively, the sparsity regularization loss may be defined without reference to any "desired sparsity", but simply force as much sparsity as possible. In this case, one can define the sparsity regularization loss as      L  sparse   ( θ θ  , ϕ ϕ  ) =    E    x ∼ ∼   μ μ   X      [   ∑ ∑   k ∈ ∈  1 : K    w  k   ‖ ‖   h  k   ‖ ‖   ]    {\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}\|h_{k}\|\right]}  ![{\displaystyle L_{\text{sparse}}(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X}}\left[\sum _{k\in 1:K}w_{k}\|h_{k}\|\right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8464dfd2872b84c2c4299a67fd9fcf1f57797d18)where      h  k     {\displaystyle h_{k}}  ![{\displaystyle h_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/78fe4f83c0bf136a170a0433c961330328b3596f) is the activation vector in the     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40)-th layer of the autoencoder. The norm     ‖ ‖  ⋅ ⋅  ‖ ‖    {\displaystyle \|\cdot \|}  ![{\displaystyle \|\cdot \|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/113f0d8fe6108fc1c5e9802f7c3f634f5480b3d1) is usually the L1 norm (giving the L1 sparse autoencoder) or the L2 norm (giving the L2 sparse autoencoder).

 

### Denoising autoencoder (DAE)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/1/18/Denoising-autoencoder.png/250px-Denoising-autoencoder.png)](./File:Denoising-autoencoder.png)A schema of a denoising autoencoder 

*Denoising autoencoders* (DAE) try to achieve a *good* representation by changing the *reconstruction criterion*.[[2]](./Autoencoder#cite_note-:0-2)[[3]](./Autoencoder#cite_note-:4-3)

 

A DAE, originally called a "robust autoassociative network" by Mark A. Kramer,[[17]](./Autoencoder#cite_note-:13-17) is trained by intentionally corrupting the inputs of a standard autoencoder during training. A noise process is defined by a probability distribution      μ μ   T     {\displaystyle \mu _{T}}  ![{\displaystyle \mu _{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a7c329840dcccf76c639e56c35ef3d56779d1fd5) over functions     T :   X   → →    X     {\displaystyle T:{\mathcal {X}}\to {\mathcal {X}}}  ![{\displaystyle T:{\mathcal {X}}\to {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/16f818c3ae1d1c6ef3b735161eb885fea2e1a645). That is, the function     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) takes a message     x ∈ ∈    X     {\displaystyle x\in {\mathcal {X}}}  ![{\displaystyle x\in {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b3cd596d560b9f3bc71615911c2438cbbf49c15), and corrupts it to a noisy version     T ( x )   {\displaystyle T(x)}  ![{\displaystyle T(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1171c29b4c2b5575f50a4ea9313f90448a2cbe05). The function     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) is selected randomly, with a probability distribution      μ μ   T     {\displaystyle \mu _{T}}  ![{\displaystyle \mu _{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a7c329840dcccf76c639e56c35ef3d56779d1fd5).

 

Given a task     (  μ μ   ref   , d )   {\displaystyle (\mu _{\text{ref}},d)}  ![{\displaystyle (\mu _{\text{ref}},d)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eb846915e028b0a1c631d189a395264d84ac2158), the problem of training a DAE is the optimization problem:     min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  ) =    E    x ∼ ∼   μ μ   X   , T ∼ ∼   μ μ   T     [ d ( x , (  D  θ θ    ∘ ∘   E  ϕ ϕ    ∘ ∘  T ) ( x ) ) ]   {\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X},T\sim \mu _{T}}[d(x,(D_{\theta }\circ E_{\phi }\circ T)(x))]}  ![{\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )=\mathbb {\mathbb {E} } _{x\sim \mu _{X},T\sim \mu _{T}}[d(x,(D_{\theta }\circ E_{\phi }\circ T)(x))]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2bdd1dd52947dc67ec42fba69511b4d28bdd7688)That is, the optimal DAE should take any noisy message and attempt to recover the original message without noise, thus the name "denoising"*.*

 

Usually, the noise process     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) is applied only during training and testing, not during downstream use.

 

The use of DAE depends on two assumptions:

 
- There exist representations to the messages that are relatively stable and robust to the type of noise we are likely to encounter;
- The said representations capture structures in the input distribution that are useful for our purposes.[[3]](./Autoencoder#cite_note-:4-3)

 

Example noise processes include:

 
- additive isotropic [Gaussian noise](./Additive_white_Gaussian_noise),
- masking noise (a fraction of the input is randomly chosen and set to 0)
- [salt-and-pepper noise](./Salt-and-pepper_noise) (a fraction of the input is randomly chosen and randomly set to its minimum or maximum value).[[3]](./Autoencoder#cite_note-:4-3)

 

### Contractive autoencoder (CAE)

 

A *contractive autoencoder* (CAE) adds the contractive regularization loss to the standard autoencoder loss:     min  θ θ  , ϕ ϕ    L ( θ θ  , ϕ ϕ  ) + λ λ   L  cont   ( θ θ  , ϕ ϕ  )   {\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{cont}}(\theta ,\phi )}  ![{\displaystyle \min _{\theta ,\phi }L(\theta ,\phi )+\lambda L_{\text{cont}}(\theta ,\phi )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1d50899e5e474e145e04327418e6094e5661e28f)where     λ λ  > 0   {\displaystyle \lambda >0}  ![{\displaystyle \lambda >0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eea25afc0351140f919cf791c49c1964b8b081de) measures how much contractive-ness we want to enforce. The contractive regularization loss itself is defined as the expected square of [Frobenius norm](./Frobenius_norm) of the [Jacobian matrix](./Jacobian_matrix_and_determinant) of the encoder activations with respect to the input:     L  cont   ( θ θ  , ϕ ϕ  ) =   E   x ∼ ∼   μ μ   r e f     ‖ ‖   ∇ ∇   x    E  ϕ ϕ    ( x )  ‖ ‖   F   2     {\displaystyle L_{\text{cont}}(\theta ,\phi )=\mathbb {E} _{x\sim \mu _{ref}}\|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}  ![{\displaystyle L_{\text{cont}}(\theta ,\phi )=\mathbb {E} _{x\sim \mu _{ref}}\|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b9ecf73ce3d00cc59e0dc569ae167c8c1e439269)To understand what      L  cont     {\displaystyle L_{\text{cont}}}  ![{\displaystyle L_{\text{cont}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/919e6a2bb3a36c6ba639b6e9edd360d17d1b2027) measures, note the fact    ‖ ‖   E  ϕ ϕ    ( x + δ δ  x ) − −   E  ϕ ϕ    ( x )  ‖ ‖   2   ≤ ≤  ‖ ‖   ∇ ∇   x    E  ϕ ϕ    ( x )  ‖ ‖   F   ‖ ‖  δ δ  x  ‖ ‖   2     {\displaystyle \|E_{\phi }(x+\delta x)-E_{\phi }(x)\|_{2}\leq \|\nabla _{x}E_{\phi }(x)\|_{F}\|\delta x\|_{2}}  ![{\displaystyle \|E_{\phi }(x+\delta x)-E_{\phi }(x)\|_{2}\leq \|\nabla _{x}E_{\phi }(x)\|_{F}\|\delta x\|_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/20f744fa9cc9382d66d2f6a6bb05e3e31d9c9229)for any message     x ∈ ∈    X     {\displaystyle x\in {\mathcal {X}}}  ![{\displaystyle x\in {\mathcal {X}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b3cd596d560b9f3bc71615911c2438cbbf49c15), and small variation     δ δ  x   {\displaystyle \delta x}  ![{\displaystyle \delta x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d22318bef6d7358b79bd993321d65d7c1d3db9d4) in it. Thus, if     ‖ ‖   ∇ ∇   x    E  ϕ ϕ    ( x )  ‖ ‖   F   2     {\displaystyle \|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}  ![{\displaystyle \|\nabla _{x}E_{\phi }(x)\|_{F}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b832eef5d8709f1a326dd9eba1609951ebc7ec19) is small, it means that a small neighborhood of the message maps to a small neighborhood of its code. This is a desired property, as it means small variation in the message leads to small, perhaps even zero, variation in its code, like how two pictures may look the same even if they are not exactly the same.

 

The DAE can be understood as an infinitesimal limit of CAE: in the limit of small Gaussian input noise, DAEs make the reconstruction function resist small but finite-sized input perturbations, while CAEs make the extracted features resist infinitesimal input perturbations.

 

### Minimum description length autoencoder (MDL-AE)

 

A *minimum description length autoencoder* (MDL-AE) is an advanced variation of the traditional autoencoder, which leverages principles from information theory, specifically the [Minimum Description Length (MDL) principle](./Minimum_description_length). The MDL principle posits that the best model for a dataset is the one that provides the shortest combined encoding of the model and the data. In the context of [autoencoders](./Autoencoders), this principle is applied to ensure that the learned representation is not only compact but also interpretable and efficient for reconstruction.

 

The MDL-AE seeks to minimize the total description length of the data, which includes the size of the [latent representation](./Latent_representation?action=edit&redlink=1) (code length) and the error in reconstructing the original data. The objective can be expressed as
     L  code   +  L  error     {\displaystyle L_{\text{code}}+L_{\text{error}}}  ![{\displaystyle L_{\text{code}}+L_{\text{error}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/04970ccd9de439b43708851e6d701aa20ae42d50), where      L  code     {\displaystyle L_{\text{code}}}  ![{\displaystyle L_{\text{code}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/724dcb12347fd9f0bbe4582370dd161b2003d4a1) represents the length of the compressed latent representation and      L  error     {\displaystyle L_{\text{error}}}  ![{\displaystyle L_{\text{error}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54fbecfb3bd1d0f30fa1c943dd068fdc662f32b2) denotes the reconstruction error.[[18]](./Autoencoder#cite_note-:5-18)

 

### Concrete autoencoder (CAE)

 

The *concrete autoencoder* is designed for discrete feature selection.[[19]](./Autoencoder#cite_note-19) A concrete autoencoder forces the latent space to consist only of a user-specified number of features. The concrete autoencoder uses a continuous [relaxation](./Relaxation_(approximation)) of the [categorical distribution](./Categorical_distribution) to allow gradients to pass through the feature selector layer, which makes it possible to use standard [backpropagation](./Backpropagation) to learn an optimal subset of input features that minimize reconstruction loss.

 

## Advantages of depth

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/2/28/Autoencoder_structure.png/500px-Autoencoder_structure.png)](./File:Autoencoder_structure.png)Schematic structure of an autoencoder with 3 fully connected hidden layers. The code (z, or h for reference in the text) is the most internal layer. 

Autoencoders are often trained with a single-layer encoder and a single-layer decoder, but using many-layered (deep) encoders and decoders offers many advantages.[[2]](./Autoencoder#cite_note-:0-2)

 
- Depth can exponentially reduce the computational cost of representing some functions.
- Depth can exponentially decrease the amount of training data needed to learn some functions.
- Experimentally, deep autoencoders yield better compression compared to shallow or linear autoencoders.[[10]](./Autoencoder#cite_note-:7-10)
- Depth allows for advantages over traditional methods as one can show that after training single layer linear autoencoders have a latent space whose vectors span the same subspace as the eigenvectors found in [Principal component analysis](./Principal_component_analysis).[[20]](./Autoencoder#cite_note-20)

 

### Training

 

[Geoffrey Hinton](./Geoffrey_Hinton) developed the [deep belief network](./Deep_belief_network) technique for training many-layered deep autoencoders. His method involves treating each neighboring set of two layers as a [restricted Boltzmann machine](./Restricted_Boltzmann_machine) so that pretraining approximates a good solution, then using backpropagation to fine-tune the results.[[10]](./Autoencoder#cite_note-:7-10)

 

Researchers have debated whether joint training (i.e. training the whole architecture together with a single global reconstruction objective to optimize) would be better for deep auto-encoders.[[21]](./Autoencoder#cite_note-:9-21) A 2015 study showed that joint training learns better data models along with more representative features for classification as compared to the layerwise method.[[21]](./Autoencoder#cite_note-:9-21) However, their experiments showed that the success of joint training depends heavily on the regularization strategies adopted.[[21]](./Autoencoder#cite_note-:9-21)[[22]](./Autoencoder#cite_note-22)

 

## History

 

(Oja, 1982)[[23]](./Autoencoder#cite_note-23) noted that [PCA](./Principal_component_analysis) is equivalent to a neural network with one hidden layer with identity activation function. In the language of autoencoding, the input-to-hidden module is the encoder, and the hidden-to-output module is the decoder. Subsequently, in (Baldi and Hornik, 1989)[[24]](./Autoencoder#cite_note-auto-24) and (Kramer, 1991)[[9]](./Autoencoder#cite_note-:12-9) generalized PCA to autoencoders, a technique which they termed "nonlinear PCA".

 

Immediately after the resurgence of neural networks in the 1980s, it was suggested in 1986[[25]](./Autoencoder#cite_note-25) that a neural network be put in "auto-association mode". This was then implemented in (Harrison, 1987)[[26]](./Autoencoder#cite_note-26) and (Elman, Zipser, 1988)[[27]](./Autoencoder#cite_note-27) for speech and in (Cottrell, Munro, Zipser, 1987)[[28]](./Autoencoder#cite_note-28) for images.[[29]](./Autoencoder#cite_note-:14-29) In (Hinton, Salakhutdinov, 2006),[[30]](./Autoencoder#cite_note-:72-30) [deep belief networks](./Deep_belief_network) were developed. These train a pair [restricted Boltzmann machines](./Restricted_Boltzmann_machine) as encoder-decoder pairs, then train another pair on the latent representation of the first pair, and so on.[[31]](./Autoencoder#cite_note-scholar-31)

 

The first applications of AE date to early 1990s.[[2]](./Autoencoder#cite_note-:0-2)[[32]](./Autoencoder#cite_note-32)[[18]](./Autoencoder#cite_note-:5-18) Their most traditional application was [dimensionality reduction](./Dimensionality_reduction) or [feature learning](./Feature_learning), but the concept became widely used for learning [generative models](./Generative_model) of data.[[33]](./Autoencoder#cite_note-VAE-33)[[34]](./Autoencoder#cite_note-gan_faces-34) Some of the most powerful [AIs](./Artificial_intelligence) in the 2010s involved autoencoder modules as a component of larger AI systems, such as VAE in [Stable Diffusion](./Stable_Diffusion), discrete VAE in Transformer-based image generators like [DALL-E 1](./DALL-E), etc.

 

During the early days, when the terminology was uncertain, the autoencoder has also been called identity mapping,[[24]](./Autoencoder#cite_note-auto-24)[[9]](./Autoencoder#cite_note-:12-9) auto-associating,[[35]](./Autoencoder#cite_note-35) [self-supervised](./Self-supervised_learning) [backpropagation](./Backpropagation),[[9]](./Autoencoder#cite_note-:12-9) or Diabolo network.[[36]](./Autoencoder#cite_note-36)[[11]](./Autoencoder#cite_note-bengio-11)

 


