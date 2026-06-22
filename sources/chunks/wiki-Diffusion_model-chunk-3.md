---
source: sources/wiki-Diffusion_model.md
source_url: https://en.wikipedia.org/wiki/Diffusion_model
chunk: 3/8
---

## Score-based generative model

 

Score-based generative model is another formulation of diffusion modelling. They are also called noise conditional score network (NCSN) or score-matching with Langevin dynamics (SMLD).[[15]](./Diffusion_model#cite_note-15)[[16]](./Diffusion_model#cite_note-:9-16)[[17]](./Diffusion_model#cite_note-:1-17)[[18]](./Diffusion_model#cite_note-18)

 

### Score matching

 

#### The idea of score functions

 

Consider the problem of image generation. Let     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) represent an image, and let     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4) be the probability distribution over all possible images. If we have     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4) itself, then we can say for certain how likely a certain image is. However, this is intractable in general.

 

Most often, we are uninterested in knowing the absolute probability of a certain image. Instead, we are usually only interested in knowing how likely a certain image is compared to its immediate neighbors — e.g. how much more likely is an image of cat compared to some small variants of it? Is it more likely if the image contains two whiskers, or three, or with some Gaussian noise added?

 

Consequently, we are actually quite uninterested in     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4) itself, but rather,      ∇ ∇   x   ln ⁡ ⁡  q ( x )   {\displaystyle \nabla _{x}\ln q(x)}  ![{\displaystyle \nabla _{x}\ln q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4af93047d53da39336a81a2cf0bc6b211cc96ab0). This has two major effects:

 
- One, we no longer need to normalize     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4), but can use any        q ~ ~     ( x ) = C q ( x )   {\displaystyle {\tilde {q}}(x)=Cq(x)}  ![{\displaystyle {\tilde {q}}(x)=Cq(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e0cb9a2697e3bfc69381357d2586568ba1d6f68a), where     C = ∫ ∫     q ~ ~     ( x ) d x > 0   {\displaystyle C=\int {\tilde {q}}(x)dx>0}  ![{\displaystyle C=\int {\tilde {q}}(x)dx>0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ea5a6cdba3dcb7186323c085e2b6dd560c69c3f2) is any unknown constant that is of no concern to us.
- Two, we are comparing     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4) neighbors     q ( x + d x )   {\displaystyle q(x+dx)}  ![{\displaystyle q(x+dx)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/33c48bf4c976a8f0a4a88a3b7313a80e9d64c81e), by        q ( x )   q ( x + d x )    =  e  − −  ⟨ ⟨   ∇ ∇   x   ln ⁡ ⁡  q , d x ⟩ ⟩      {\displaystyle {\frac {q(x)}{q(x+dx)}}=e^{-\langle \nabla _{x}\ln q,dx\rangle }}  ![{\displaystyle {\frac {q(x)}{q(x+dx)}}=e^{-\langle \nabla _{x}\ln q,dx\rangle }}](https://wikimedia.org/api/rest_v1/media/math/render/svg/31f5fb8b5444b9dce7a908f408e90dc514f09091)

 

Let the [score function](./Score_(statistics)) be     s ( x ) :=  ∇ ∇   x   ln ⁡ ⁡  q ( x )   {\displaystyle s(x):=\nabla _{x}\ln q(x)}  ![{\displaystyle s(x):=\nabla _{x}\ln q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6fa4030a859336a3f2d2857b9abfd07562eec8ca); then consider what we can do with     s ( x )   {\displaystyle s(x)}  ![{\displaystyle s(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/10f51eec88706f1a26ac7430dc71d92c15e71a6e).

 

As it turns out,     s ( x )   {\displaystyle s(x)}  ![{\displaystyle s(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/10f51eec88706f1a26ac7430dc71d92c15e71a6e) allows us to sample from     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4) using thermodynamics. Specifically, if we have a potential energy function     U ( x ) = − −  ln ⁡ ⁡  q ( x )   {\displaystyle U(x)=-\ln q(x)}  ![{\displaystyle U(x)=-\ln q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/140e1e71ceda9811aff80285eecf65199ae96899), and a lot of particles in the potential well, then the distribution at thermodynamic equilibrium is the [Boltzmann distribution](./Boltzmann_distribution)      q  U   ( x ) ∝ ∝   e  − −  U ( x )  /   k  B   T   = q ( x  )  1  /   k  B   T     {\displaystyle q_{U}(x)\propto e^{-U(x)/k_{B}T}=q(x)^{1/k_{B}T}}  ![{\displaystyle q_{U}(x)\propto e^{-U(x)/k_{B}T}=q(x)^{1/k_{B}T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4a2fe771133c26a423c282e161b8ad344c7c7d56). At temperature      k  B   T = 1   {\displaystyle k_{B}T=1}  ![{\displaystyle k_{B}T=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/931cb85ae02424c524e0c2dac8be46d34b5fdf62), the Boltzmann distribution is exactly     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4).

 

Therefore, to model     q ( x )   {\displaystyle q(x)}  ![{\displaystyle q(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c38bbafe34a043d284f19231b946a76c0a4b16b4), we may start with a particle sampled at any convenient distribution (such as the standard Gaussian distribution), then simulate the motion of the particle forwards according to the [Langevin equation](./Langevin_equation)     d  x  t   = − −   ∇ ∇    x  t     U (  x  t   ) d t + d  W  t     {\displaystyle dx_{t}=-\nabla _{x_{t}}U(x_{t})dt+dW_{t}}  ![{\displaystyle dx_{t}=-\nabla _{x_{t}}U(x_{t})dt+dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c1af275975d961256369f88132b61dcdf02e06a1)
and the Boltzmann distribution is, [by Fokker-Planck equation, the unique thermodynamic equilibrium](./Fokker–Planck_equation#Boltzmann_distribution_at_the_thermodynamic_equilibrium). So no matter what distribution      x  0     {\displaystyle x_{0}}  ![{\displaystyle x_{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86f21d0e31751534cd6584264ecf864a6aa792cf) has, the distribution of      x  t     {\displaystyle x_{t}}  ![{\displaystyle x_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f279a30bc8eabc788f3fe81c9cfb674e72e858db) converges in distribution to     q   {\displaystyle q}  ![{\displaystyle q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d) as     t → →  ∞ ∞    {\displaystyle t\to \infty }  ![{\displaystyle t\to \infty }](https://wikimedia.org/api/rest_v1/media/math/render/svg/8a34d7a61899d577d950881b4a44888d43f3fa93).

 

#### Learning the score function

 

Given a density     q   {\displaystyle q}  ![{\displaystyle q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d), we wish to learn a score function approximation      f  θ θ    ≈ ≈  ∇ ∇  ln ⁡ ⁡  q   {\displaystyle f_{\theta }\approx \nabla \ln q}  ![{\displaystyle f_{\theta }\approx \nabla \ln q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fbb5d200850fb8dafe9c67473ad0fa5ed03dc8f). This is **score matching***.*[[19]](./Diffusion_model#cite_note-19) Typically, score matching is formalized as minimizing **Fisher divergence** function      E  q   [ ‖ ‖   f  θ θ    ( x ) − −  ∇ ∇  ln ⁡ ⁡  q ( x )  ‖ ‖   2   ]   {\displaystyle E_{q}[\|f_{\theta }(x)-\nabla \ln q(x)\|^{2}]}  ![{\displaystyle E_{q}[\|f_{\theta }(x)-\nabla \ln q(x)\|^{2}]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/629f17805d6fd5182bc671e725d453403e337b40). By expanding the integral, and performing an [integration by parts](./Integration_by_parts),      E  q   [ ‖ ‖   f  θ θ    ( x ) − −  ∇ ∇  ln ⁡ ⁡  q ( x )  ‖ ‖   2   ] =  E  q   [ ‖ ‖   f  θ θ     ‖ ‖   2   + 2 ∇ ∇  ⋅ ⋅   f  θ θ    ] + C   {\displaystyle E_{q}[\|f_{\theta }(x)-\nabla \ln q(x)\|^{2}]=E_{q}[\|f_{\theta }\|^{2}+2\nabla \cdot f_{\theta }]+C}  ![{\displaystyle E_{q}[\|f_{\theta }(x)-\nabla \ln q(x)\|^{2}]=E_{q}[\|f_{\theta }\|^{2}+2\nabla \cdot f_{\theta }]+C}](https://wikimedia.org/api/rest_v1/media/math/render/svg/07719e498d5037e8338a2df0adda804276531b6d)giving us a loss function, also known as the [Hyvärinen scoring rule](./Scoring_rule#Hyvärinen_scoring_rule), that can be minimized by stochastic gradient descent.

 

#### Annealing the score function

 

Suppose we need to model the distribution of images, and we want      x  0   ∼ ∼    N   ( 0 , I )   {\displaystyle x_{0}\sim {\mathcal {N}}(0,I)}  ![{\displaystyle x_{0}\sim {\mathcal {N}}(0,I)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1329458512182d624965869be64daf4e07b0f994), a white-noise image. Now, most white-noise images do not look like real images, so     q (  x  0   ) ≈ ≈  0   {\displaystyle q(x_{0})\approx 0}  ![{\displaystyle q(x_{0})\approx 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d1e460718e2126351aa7193884a2b4dfde99cb5b) for large swaths of      x  0   ∼ ∼    N   ( 0 , I )   {\displaystyle x_{0}\sim {\mathcal {N}}(0,I)}  ![{\displaystyle x_{0}\sim {\mathcal {N}}(0,I)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1329458512182d624965869be64daf4e07b0f994). This presents a problem for learning the score function, because if there are no samples around a certain point, then we can't learn the score function at that point. If we do not know the score function      ∇ ∇    x  t     ln ⁡ ⁡  q (  x  t   )   {\displaystyle \nabla _{x_{t}}\ln q(x_{t})}  ![{\displaystyle \nabla _{x_{t}}\ln q(x_{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb75e80f87ed0112192b6ee0a01995a589213d09) at that point, then we cannot impose the time-evolution equation on a particle:    d  x  t   =  ∇ ∇    x  t     ln ⁡ ⁡  q (  x  t   ) d t + d  W  t     {\displaystyle dx_{t}=\nabla _{x_{t}}\ln q(x_{t})dt+dW_{t}}  ![{\displaystyle dx_{t}=\nabla _{x_{t}}\ln q(x_{t})dt+dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4ab3992c05742efe2bfc2817d90a10eaa5dc11ff)To deal with this problem, we perform [annealing](./Simulated_annealing). If     q   {\displaystyle q}  ![{\displaystyle q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d) is too different from a white-noise distribution, then progressively add noise until it is indistinguishable from one. That is, we perform a forward diffusion, then learn the score function, then use the score function to perform a backward diffusion.

 

### Continuous diffusion processes

 

#### Forward diffusion process

 

Consider again the forward diffusion process, but this time in continuous time:     x  t   =   1 − −   β β   t      x  t − −  1   +    β β   t      z  t     {\displaystyle x_{t}={\sqrt {1-\beta _{t}}}x_{t-1}+{\sqrt {\beta _{t}}}z_{t}}  ![{\displaystyle x_{t}={\sqrt {1-\beta _{t}}}x_{t-1}+{\sqrt {\beta _{t}}}z_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5bfedcf08a29819994ec6abb46ede435512222dd)By taking the      β β   t   → →  β β  ( t ) d t ,   d t    z  t   → →  d  W  t     {\displaystyle \beta _{t}\to \beta (t)dt,{\sqrt {dt}}z_{t}\to dW_{t}}  ![{\displaystyle \beta _{t}\to \beta (t)dt,{\sqrt {dt}}z_{t}\to dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ccccb58046f89db97b4477d7f8f1ead2db7b33fe) limit, we obtain a continuous diffusion process, in the form of a [stochastic differential equation](./Stochastic_differential_equation):    d  x  t   = − −    1 2   β β  ( t )  x  t   d t +   β β  ( t )   d  W  t     {\displaystyle dx_{t}=-{\frac {1}{2}}\beta (t)x_{t}dt+{\sqrt {\beta (t)}}dW_{t}}  ![{\displaystyle dx_{t}=-{\frac {1}{2}}\beta (t)x_{t}dt+{\sqrt {\beta (t)}}dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/11bdd31eb828bcca42d3fb7b2d9ec90126fb62c1)where      W  t     {\displaystyle W_{t}}  ![{\displaystyle W_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/50680c5535c83badfa630dba63b583d2eeaa2977) is a [Wiener process](./Wiener_process) (multidimensional Brownian motion).

 

Now, the equation is exactly a special case of the [overdamped Langevin equation](./Brownian_dynamics)    d  x  t   = − −    D   k  B   T    (  ∇ ∇   x   U ) d t +   2 D   d  W  t     {\displaystyle dx_{t}=-{\frac {D}{k_{B}T}}(\nabla _{x}U)dt+{\sqrt {2D}}dW_{t}}  ![{\displaystyle dx_{t}=-{\frac {D}{k_{B}T}}(\nabla _{x}U)dt+{\sqrt {2D}}dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/506e77f3e2a7001bb35275ddcac420fad74a330e)where     D   {\displaystyle D}  ![{\displaystyle D}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f34a0c600395e5d4345287e21fb26efd386990e6) is diffusion tensor,     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) is temperature, and     U   {\displaystyle U}  ![{\displaystyle U}](https://wikimedia.org/api/rest_v1/media/math/render/svg/458a728f53b9a0274f059cd695e067c430956025) is potential energy field. If we substitute in     D =   1 2   β β  ( t ) I ,  k  B   T = 1 , U =   1 2   ‖ ‖  x  ‖ ‖   2     {\displaystyle D={\frac {1}{2}}\beta (t)I,k_{B}T=1,U={\frac {1}{2}}\|x\|^{2}}  ![{\displaystyle D={\frac {1}{2}}\beta (t)I,k_{B}T=1,U={\frac {1}{2}}\|x\|^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dcac55720db454a155704c7eed1d4a9f34c7d40f), we recover the above equation. This explains why the phrase "Langevin dynamics" is sometimes used in diffusion models.

 

Now the above equation is for the stochastic motion of a single particle. Suppose we have a cloud of particles distributed according to     q   {\displaystyle q}  ![{\displaystyle q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d) at time     t = 0   {\displaystyle t=0}  ![{\displaystyle t=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43469ec032d858feae5aa87029e22eaaf0109e9c), then after a long time, the cloud of particles would settle into the [stable distribution](./Stable_distribution) of       N   ( 0 , I )   {\displaystyle {\mathcal {N}}(0,I)}  ![{\displaystyle {\mathcal {N}}(0,I)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/00d56975d9da87432a3e9bdddf59aec1dd990bcb). Let      ρ ρ   t     {\displaystyle \rho _{t}}  ![{\displaystyle \rho _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d1d393145553a30657afb0fca049fd29eeb260f8) be the density of the cloud of particles at time     t   {\displaystyle t}  ![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560), then we have     ρ ρ   0   = q ;   ρ ρ   T   ≈ ≈    N   ( 0 , I )   {\displaystyle \rho _{0}=q;\quad \rho _{T}\approx {\mathcal {N}}(0,I)}  ![{\displaystyle \rho _{0}=q;\quad \rho _{T}\approx {\mathcal {N}}(0,I)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12606e0f0e5fec62dcca2bc5c913e5e1750405d3)and the goal is to somehow reverse the process, so that we can start at the end and diffuse back to the beginning.

 

By [Fokker-Planck equation](./Fokker–Planck_equation), the density of the cloud evolves according to     ∂ ∂   t   ln ⁡ ⁡   ρ ρ   t   =   1 2   β β  ( t )  (  n + ( x + ∇ ∇  ln ⁡ ⁡   ρ ρ   t   ) ⋅ ⋅  ∇ ∇  ln ⁡ ⁡   ρ ρ   t   + Δ Δ  ln ⁡ ⁡   ρ ρ   t    )    {\displaystyle \partial _{t}\ln \rho _{t}={\frac {1}{2}}\beta (t)\left(n+(x+\nabla \ln \rho _{t})\cdot \nabla \ln \rho _{t}+\Delta \ln \rho _{t}\right)}  ![{\displaystyle \partial _{t}\ln \rho _{t}={\frac {1}{2}}\beta (t)\left(n+(x+\nabla \ln \rho _{t})\cdot \nabla \ln \rho _{t}+\Delta \ln \rho _{t}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb45e063415a40bfe8a9b2830ed92362fcaf8659)where     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) is the dimension of space, and     Δ Δ    {\displaystyle \Delta }  ![{\displaystyle \Delta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/32769037c408874e1890f77554c65f39c523ebe2) is the [Laplace operator](./Laplace_operator). Equivalently,     ∂ ∂   t    ρ ρ   t   =   1 2   β β  ( t ) ( ∇ ∇  ⋅ ⋅  ( x  ρ ρ   t   ) + Δ Δ   ρ ρ   t   )   {\displaystyle \partial _{t}\rho _{t}={\frac {1}{2}}\beta (t)(\nabla \cdot (x\rho _{t})+\Delta \rho _{t})}  ![{\displaystyle \partial _{t}\rho _{t}={\frac {1}{2}}\beta (t)(\nabla \cdot (x\rho _{t})+\Delta \rho _{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/64a1dcc951b25252335dfd511cf23ffb7194cbc9)

 

#### Backward diffusion process

 

If we have solved      ρ ρ   t     {\displaystyle \rho _{t}}  ![{\displaystyle \rho _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d1d393145553a30657afb0fca049fd29eeb260f8) for time     t ∈ ∈  [ 0 , T ]   {\displaystyle t\in [0,T]}  ![{\displaystyle t\in [0,T]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b7ea7b28971838e52f450c48053939e81daa26f), then we can exactly reverse the evolution of the cloud. Suppose we start with another cloud of particles with density      ν ν   0   =  ρ ρ   T     {\displaystyle \nu _{0}=\rho _{T}}  ![{\displaystyle \nu _{0}=\rho _{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dff4707413bae4ce3bf2db3a1b559dfa24f48c15), and let the particles in the cloud evolve according to

 

    d  y  t   =   1 2   β β  ( T − −  t )  y  t   d t + β β  ( T − −  t )      ∇ ∇    y  t     ln ⁡ ⁡   ρ ρ   T − −  t    (  y  t   )   ⏟ ⏟     score function    d t +   β β  ( T − −  t )   d  W  t     {\displaystyle dy_{t}={\frac {1}{2}}\beta (T-t)y_{t}dt+\beta (T-t)\underbrace {\nabla _{y_{t}}\ln \rho _{T-t}\left(y_{t}\right)} _{\text{score function }}dt+{\sqrt {\beta (T-t)}}dW_{t}}  ![{\displaystyle dy_{t}={\frac {1}{2}}\beta (T-t)y_{t}dt+\beta (T-t)\underbrace {\nabla _{y_{t}}\ln \rho _{T-t}\left(y_{t}\right)} _{\text{score function }}dt+{\sqrt {\beta (T-t)}}dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d4e70c112652d959143dd2999d1dbf40d8083d5e)

 

then by plugging into the Fokker-Planck equation, we find that      ∂ ∂   t    ρ ρ   T − −  t   =  ∂ ∂   t    ν ν   t     {\displaystyle \partial _{t}\rho _{T-t}=\partial _{t}\nu _{t}}  ![{\displaystyle \partial _{t}\rho _{T-t}=\partial _{t}\nu _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6ee9c9a6293bf6379a207713aa47e95f5fce8cd2). Thus this cloud of points is the original cloud, evolving backwards.[[20]](./Diffusion_model#cite_note-20)

 

### Noise conditional score network (NCSN)

 

At the continuous limit, 
        α α  ¯ ¯      t   = ( 1 − −   β β   1   ) ⋯ ⋯  ( 1 − −   β β   t   ) =  e   ∑ ∑   i   ln ⁡ ⁡  ( 1 − −   β β   i   )   → →   e  − −   ∫ ∫   0   t   β β  ( t ) d t     {\displaystyle {\bar {\alpha }}_{t}=(1-\beta _{1})\cdots (1-\beta _{t})=e^{\sum _{i}\ln(1-\beta _{i})}\to e^{-\int _{0}^{t}\beta (t)dt}}  ![{\displaystyle {\bar {\alpha }}_{t}=(1-\beta _{1})\cdots (1-\beta _{t})=e^{\sum _{i}\ln(1-\beta _{i})}\to e^{-\int _{0}^{t}\beta (t)dt}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/78d48da3134ceac216f16c31ad32bd6702147d68)
and so 
     x  t    |   x  0   ∼ ∼  N  (   e  − −    1 2    ∫ ∫   0   t   β β  ( t ) d t    x  0   ,  (  1 − −   e  − −   ∫ ∫   0   t   β β  ( t ) d t    )  I  )    {\displaystyle x_{t}|x_{0}\sim N\left(e^{-{\frac {1}{2}}\int _{0}^{t}\beta (t)dt}x_{0},\left(1-e^{-\int _{0}^{t}\beta (t)dt}\right)I\right)}  ![{\displaystyle x_{t}|x_{0}\sim N\left(e^{-{\frac {1}{2}}\int _{0}^{t}\beta (t)dt}x_{0},\left(1-e^{-\int _{0}^{t}\beta (t)dt}\right)I\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/695fb9bfb0b8fac5b69aee9f7643dfff5f4e445b)
In particular, we see that we can directly sample from any point in the continuous diffusion process without going through the intermediate steps, by first sampling      x  0   ∼ ∼  q , z ∼ ∼    N   ( 0 , I )   {\displaystyle x_{0}\sim q,z\sim {\mathcal {N}}(0,I)}  ![{\displaystyle x_{0}\sim q,z\sim {\mathcal {N}}(0,I)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e93eb4336dc328f482f41b27c7fc7fd22ea473b), then get      x  t   =  e  − −    1 2    ∫ ∫   0   t   β β  ( t ) d t    x  0   +  (  1 − −   e  − −   ∫ ∫   0   t   β β  ( t ) d t    )  z   {\displaystyle x_{t}=e^{-{\frac {1}{2}}\int _{0}^{t}\beta (t)dt}x_{0}+\left(1-e^{-\int _{0}^{t}\beta (t)dt}\right)z}  ![{\displaystyle x_{t}=e^{-{\frac {1}{2}}\int _{0}^{t}\beta (t)dt}x_{0}+\left(1-e^{-\int _{0}^{t}\beta (t)dt}\right)z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e49f50c12a4423b33cdca93adb2145b7b7593164). That is, we can quickly sample      x  t   ∼ ∼   ρ ρ   t     {\displaystyle x_{t}\sim \rho _{t}}  ![{\displaystyle x_{t}\sim \rho _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b9b6ffd6c17d45a3c4b8d003a4a54ccbfbf29bff) for any     t ≥ ≥  0   {\displaystyle t\geq 0}  ![{\displaystyle t\geq 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/248525429e9cd266f53ab8c52d17bc206c546060).

 

Now, define a certain probability distribution     γ γ    {\displaystyle \gamma }  ![{\displaystyle \gamma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a) over     [ 0 , ∞ ∞  )   {\displaystyle [0,\infty )}  ![{\displaystyle [0,\infty )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8dc2d914c2df66bc0f7893bfb8da36766650fe47), then the score-matching loss function is defined as the expected Fisher divergence:
    L ( θ θ  ) =  E  t ∼ ∼  γ γ  ,  x  t   ∼ ∼   ρ ρ   t     [ ‖ ‖   f  θ θ    (  x  t   , t )  ‖ ‖   2   + 2 ∇ ∇  ⋅ ⋅   f  θ θ    (  x  t   , t ) ]   {\displaystyle L(\theta )=E_{t\sim \gamma ,x_{t}\sim \rho _{t}}[\|f_{\theta }(x_{t},t)\|^{2}+2\nabla \cdot f_{\theta }(x_{t},t)]}  ![{\displaystyle L(\theta )=E_{t\sim \gamma ,x_{t}\sim \rho _{t}}[\|f_{\theta }(x_{t},t)\|^{2}+2\nabla \cdot f_{\theta }(x_{t},t)]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d8505a3a440a3ddfa923515122f9a4402570df9)
After training,      f  θ θ    (  x  t   , t ) ≈ ≈  ∇ ∇  ln ⁡ ⁡   ρ ρ   t     {\displaystyle f_{\theta }(x_{t},t)\approx \nabla \ln \rho _{t}}  ![{\displaystyle f_{\theta }(x_{t},t)\approx \nabla \ln \rho _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/273582d9e3daa63e8189a4e93d4f660b23330f22), so we can perform the backwards diffusion process by first sampling      x  T   ∼ ∼    N   ( 0 , I )   {\displaystyle x_{T}\sim {\mathcal {N}}(0,I)}  ![{\displaystyle x_{T}\sim {\mathcal {N}}(0,I)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d545e26900fa8a43ce5528e68b746666731cf81e), then integrating the SDE from     t = T   {\displaystyle t=T}  ![{\displaystyle t=T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5c6b2eabe8e275c2da71dbc61ca0ede73a418051) to     t = 0   {\displaystyle t=0}  ![{\displaystyle t=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43469ec032d858feae5aa87029e22eaaf0109e9c):
     x  t − −  d t   =  x  t   +   1 2   β β  ( t )  x  t   d t + β β  ( t )  f  θ θ    (  x  t   , t ) d t +   β β  ( t )   d  W  t     {\displaystyle x_{t-dt}=x_{t}+{\frac {1}{2}}\beta (t)x_{t}dt+\beta (t)f_{\theta }(x_{t},t)dt+{\sqrt {\beta (t)}}dW_{t}}  ![{\displaystyle x_{t-dt}=x_{t}+{\frac {1}{2}}\beta (t)x_{t}dt+\beta (t)f_{\theta }(x_{t},t)dt+{\sqrt {\beta (t)}}dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f07077954ad9a6888e8b5b227e06eb885ef1c805)
This may be done by any SDE integration method, such as [Euler–Maruyama method](./Euler–Maruyama_method).

 

The name "noise conditional score network" is explained thus:

 
- "network", because      f  θ θ      {\displaystyle f_{\theta }}  ![{\displaystyle f_{\theta }}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9874ae06066a2250709085e0fb521eebff2c2fb7) is implemented as a neural network.
- "score", because the output of the network is interpreted as approximating the score function     ∇ ∇  ln ⁡ ⁡   ρ ρ   t     {\displaystyle \nabla \ln \rho _{t}}  ![{\displaystyle \nabla \ln \rho _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f632642155529f92d207ef56dc4f082f616334d).
- "noise conditional", because      ρ ρ   t     {\displaystyle \rho _{t}}  ![{\displaystyle \rho _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d1d393145553a30657afb0fca049fd29eeb260f8) is equal to      ρ ρ   0     {\displaystyle \rho _{0}}  ![{\displaystyle \rho _{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d9c04a9d26b86af8c6205ba2a6287fd655b6b714) blurred by an added Gaussian noise that increases with time, and so the score function depends on the amount of noise added.

 


