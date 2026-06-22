---
source: sources/wiki-Diffusion_model.md
source_url: https://en.wikipedia.org/wiki/Diffusion_model
chunk: 4/8
---

## Their equivalence

 

DDPM and score-based generative models are equivalent.[[16]](./Diffusion_model#cite_note-:9-16)[[1]](./Diffusion_model#cite_note-song-1)[[21]](./Diffusion_model#cite_note-21) This means that a network trained using DDPM can be used as a NCSN, and vice versa.

 

We know that      x  t    |   x  0   ∼ ∼  N  (        α α  ¯ ¯      t      x  0   ,  σ σ   t   2   I  )    {\displaystyle x_{t}|x_{0}\sim N\left({\sqrt {{\bar {\alpha }}_{t}}}x_{0},\sigma _{t}^{2}I\right)}  ![{\displaystyle x_{t}|x_{0}\sim N\left({\sqrt {{\bar {\alpha }}_{t}}}x_{0},\sigma _{t}^{2}I\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0aafa5f6c97510632e03f5a981573fed0d509363), so by [Tweedie's formula](./Maurice_Tweedie#Tweedie's_formula), we have
     ∇ ∇    x  t     ln ⁡ ⁡  q (  x  t   ) =   1  σ σ   t   2     ( − −   x  t   +       α α  ¯ ¯      t      E  q   [  x  0    |   x  t   ] )   {\displaystyle \nabla _{x_{t}}\ln q(x_{t})={\frac {1}{\sigma _{t}^{2}}}(-x_{t}+{\sqrt {{\bar {\alpha }}_{t}}}E_{q}[x_{0}|x_{t}])}  ![{\displaystyle \nabla _{x_{t}}\ln q(x_{t})={\frac {1}{\sigma _{t}^{2}}}(-x_{t}+{\sqrt {{\bar {\alpha }}_{t}}}E_{q}[x_{0}|x_{t}])}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e501cf3cc429e6e8fa34ce80701750d5f43c3400)
As described previously, the DDPM loss function is      ∑ ∑   t    L  s i m p l e , t     {\displaystyle \sum _{t}L_{simple,t}}  ![{\displaystyle \sum _{t}L_{simple,t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/445e82c1c7fdb7da14ca516e78e44bf346f093b2) with
     L  s i m p l e , t   =  E   x  0   ∼ ∼  q ; z ∼ ∼    N   ( 0 , I )    [   ‖   ϵ ϵ   θ θ    (  x  t   , t ) − −  z  ‖   2   ]    {\displaystyle L_{simple,t}=E_{x_{0}\sim q;z\sim {\mathcal {N}}(0,I)}\left[\left\|\epsilon _{\theta }(x_{t},t)-z\right\|^{2}\right]}  ![{\displaystyle L_{simple,t}=E_{x_{0}\sim q;z\sim {\mathcal {N}}(0,I)}\left[\left\|\epsilon _{\theta }(x_{t},t)-z\right\|^{2}\right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/935e47818aeafab5cc11a12a4dd25361dade64bc)
where      x  t   =       α α  ¯ ¯      t      x  0   +  σ σ   t   z   {\displaystyle x_{t}={\sqrt {{\bar {\alpha }}_{t}}}x_{0}+\sigma _{t}z}  ![{\displaystyle x_{t}={\sqrt {{\bar {\alpha }}_{t}}}x_{0}+\sigma _{t}z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/46b439306dae327b2ae72767693896f7505a02e9). By a change of variables,
     L  s i m p l e , t   =  E   x  0   ,  x  t   ∼ ∼  q    [   ‖   ϵ ϵ   θ θ    (  x  t   , t ) − −      x  t   − −        α α  ¯ ¯      t      x  0     σ σ   t      ‖   2   ]  =  E   x  t   ∼ ∼  q ,  x  0   ∼ ∼  q ( ⋅ ⋅   |   x  t   )    [   ‖   ϵ ϵ   θ θ    (  x  t   , t ) − −      x  t   − −        α α  ¯ ¯      t      x  0     σ σ   t      ‖   2   ]    {\displaystyle L_{simple,t}=E_{x_{0},x_{t}\sim q}\left[\left\|\epsilon _{\theta }(x_{t},t)-{\frac {x_{t}-{\sqrt {{\bar {\alpha }}_{t}}}x_{0}}{\sigma _{t}}}\right\|^{2}\right]=E_{x_{t}\sim q,x_{0}\sim q(\cdot |x_{t})}\left[\left\|\epsilon _{\theta }(x_{t},t)-{\frac {x_{t}-{\sqrt {{\bar {\alpha }}_{t}}}x_{0}}{\sigma _{t}}}\right\|^{2}\right]}  ![{\displaystyle L_{simple,t}=E_{x_{0},x_{t}\sim q}\left[\left\|\epsilon _{\theta }(x_{t},t)-{\frac {x_{t}-{\sqrt {{\bar {\alpha }}_{t}}}x_{0}}{\sigma _{t}}}\right\|^{2}\right]=E_{x_{t}\sim q,x_{0}\sim q(\cdot |x_{t})}\left[\left\|\epsilon _{\theta }(x_{t},t)-{\frac {x_{t}-{\sqrt {{\bar {\alpha }}_{t}}}x_{0}}{\sigma _{t}}}\right\|^{2}\right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/42e46edbe79966d43c6ead0b38b9b12c12a1a2ed)
and the term inside becomes a least squares regression, so if the network actually reaches the global minimum of loss, then we have      ϵ ϵ   θ θ    (  x  t   , t ) =     x  t   − −        α α  ¯ ¯      t      E  q   [  x  0    |   x  t   ]   σ σ   t     = − −   σ σ   t    ∇ ∇    x  t     ln ⁡ ⁡  q (  x  t   )   {\displaystyle \epsilon _{\theta }(x_{t},t)={\frac {x_{t}-{\sqrt {{\bar {\alpha }}_{t}}}E_{q}[x_{0}|x_{t}]}{\sigma _{t}}}=-\sigma _{t}\nabla _{x_{t}}\ln q(x_{t})}  ![{\displaystyle \epsilon _{\theta }(x_{t},t)={\frac {x_{t}-{\sqrt {{\bar {\alpha }}_{t}}}E_{q}[x_{0}|x_{t}]}{\sigma _{t}}}=-\sigma _{t}\nabla _{x_{t}}\ln q(x_{t})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fe275f9f8a6ce998920e403651cc41b36d7b3020)

 

Thus, given a good score-based network, its predicted score is a good prediction of the noise (after scaling by      σ σ   t     {\displaystyle \sigma _{t}}  ![{\displaystyle \sigma _{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b5dd6db0238ac32f34c6feb604748e253e842356)), and thus can be used for denoising.

 

Conversely, the continuous limit      x  t − −  1   =  x  t − −  d t   ,  β β   t   = β β  ( t ) d t ,  z  t     d t   = d  W  t     {\displaystyle x_{t-1}=x_{t-dt},\beta _{t}=\beta (t)dt,z_{t}{\sqrt {dt}}=dW_{t}}  ![{\displaystyle x_{t-1}=x_{t-dt},\beta _{t}=\beta (t)dt,z_{t}{\sqrt {dt}}=dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4bca13017ed81d77be7e91ba3594898eaad8eea2) of the backward equation
     x  t − −  1   =    x  t     α α   t      − −     β β   t     σ σ   t      α α   t         ϵ ϵ   θ θ    (  x  t   , t ) +    β β   t      z  t   ;   z  t   ∼ ∼    N   ( 0 , I )   {\displaystyle x_{t-1}={\frac {x_{t}}{\sqrt {\alpha _{t}}}}-{\frac {\beta _{t}}{\sigma _{t}{\sqrt {\alpha _{t}}}}}\epsilon _{\theta }(x_{t},t)+{\sqrt {\beta _{t}}}z_{t};\quad z_{t}\sim {\mathcal {N}}(0,I)}  ![{\displaystyle x_{t-1}={\frac {x_{t}}{\sqrt {\alpha _{t}}}}-{\frac {\beta _{t}}{\sigma _{t}{\sqrt {\alpha _{t}}}}}\epsilon _{\theta }(x_{t},t)+{\sqrt {\beta _{t}}}z_{t};\quad z_{t}\sim {\mathcal {N}}(0,I)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/da578e0f283c65143e518ace956bcd6d53da6383)
gives us precisely the same equation as score-based diffusion:
     x  t − −  d t   =  x  t   ( 1 + β β  ( t ) d t  /  2 ) + β β  ( t )  ∇ ∇    x  t     ln ⁡ ⁡  q (  x  t   ) d t +   β β  ( t )   d  W  t     {\displaystyle x_{t-dt}=x_{t}(1+\beta (t)dt/2)+\beta (t)\nabla _{x_{t}}\ln q(x_{t})dt+{\sqrt {\beta (t)}}dW_{t}}  ![{\displaystyle x_{t-dt}=x_{t}(1+\beta (t)dt/2)+\beta (t)\nabla _{x_{t}}\ln q(x_{t})dt+{\sqrt {\beta (t)}}dW_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/483586f87a35977a732696a497df97d4044048a4)Thus, at infinitesimal steps of DDPM, a denoising network performs score-based diffusion.

 


