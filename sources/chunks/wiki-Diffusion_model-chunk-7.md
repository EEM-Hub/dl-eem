---
source: sources/wiki-Diffusion_model.md
source_url: https://en.wikipedia.org/wiki/Diffusion_model
chunk: 7/8
---

## Choice of architecture

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/4/45/Diffusion_Architecture.png/330px-Diffusion_Architecture.png)](./File:Diffusion_Architecture.png)Architecture of Stable Diffusion [![](//upload.wikimedia.org/wikipedia/commons/thumb/9/99/X-Y_plot_of_algorithmically-generated_AI_art_of_European-style_castle_in_Japan_demonstrating_DDIM_diffusion_steps.png/330px-X-Y_plot_of_algorithmically-generated_AI_art_of_European-style_castle_in_Japan_demonstrating_DDIM_diffusion_steps.png)](./File:X-Y_plot_of_algorithmically-generated_AI_art_of_European-style_castle_in_Japan_demonstrating_DDIM_diffusion_steps.png)The denoising process used by Stable Diffusion 

### Diffusion model

 

For generating images by DDPM, we need a neural network that takes a time     t   {\displaystyle t}  ![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) and a noisy image      x  t     {\displaystyle x_{t}}  ![{\displaystyle x_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f279a30bc8eabc788f3fe81c9cfb674e72e858db), and predicts a noise      ϵ ϵ   θ θ    (  x  t   , t )   {\displaystyle \epsilon _{\theta }(x_{t},t)}  ![{\displaystyle \epsilon _{\theta }(x_{t},t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac1d100b70d76dbb0e1429000edc61529a2c1724) from it. Since predicting the noise is the same as predicting the denoised image, then subtracting it from      x  t     {\displaystyle x_{t}}  ![{\displaystyle x_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f279a30bc8eabc788f3fe81c9cfb674e72e858db), denoising architectures tend to work well. For example, the [U-Net](./U-Net), which was found to be good for denoising images, is often used for denoising diffusion models that generate images.[[45]](./Diffusion_model#cite_note-:3-45)

 

For DDPM, the underlying architecture ("backbone") does not have to be a U-Net. It just has to predict the noise somehow. For example, the diffusion transformer (DiT) uses a [Transformer](./Transformer_(deep_learning_architecture)) to predict the mean and diagonal covariance of the noise, given the textual conditioning and the partially denoised image. It is the same as standard U-Net-based denoising diffusion model, with a Transformer replacing the U-Net.[[46]](./Diffusion_model#cite_note-46) [Mixture of experts](./Mixture_of_experts)-Transformer can also be applied.[[47]](./Diffusion_model#cite_note-47)

 

DDPM can be used to model general data distributions, not just natural-looking images. For example, Human Motion Diffusion[[48]](./Diffusion_model#cite_note-:4-48) models human motion trajectory by DDPM. Each human motion trajectory is a sequence of poses, represented by either joint rotations or positions. It uses a [Transformer](./Transformer_(deep_learning_architecture)) network to generate a less noisy trajectory out of a noisy one.

 

### Conditioning

 

The base diffusion model can only generate unconditionally from the whole distribution. For example, a diffusion model learned on [ImageNet](./ImageNet) would generate images that look like a random image from ImageNet. To generate images from just one category, one would need to impose the condition, and then sample from the conditional distribution. Whatever condition one wants to impose, one needs to first convert the conditioning into a vector of floating point numbers, then feed it into the underlying diffusion model neural network. However, one has freedom in choosing how to convert the conditioning into a vector.

 

Stable Diffusion, for example, imposes conditioning in the form of [cross-attention mechanism](./Attention_(machine_learning)), where the query is an intermediate representation of the image in the U-Net, and both key and value are the conditioning vectors. The conditioning can be selectively applied to only parts of an image, and new kinds of conditionings can be finetuned upon the base model, as used in ControlNet.[[49]](./Diffusion_model#cite_note-49)

 

As a particularly simple example, consider [image inpainting](./Inpainting). The conditions are        x ~ ~       {\displaystyle {\tilde {x}}}  ![{\displaystyle {\tilde {x}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4f5c5435030c952a58a756e691ea64f60c1bd240), the reference image, and     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc), the inpainting [mask](./Mask_(computing)#Image_masks). The conditioning is imposed at each step of the backward diffusion process, by first sampling         x ~ ~      t   ∼ ∼  N  (        α α  ¯ ¯      t        x ~ ~     ,  σ σ   t   2   I  )    {\displaystyle {\tilde {x}}_{t}\sim N\left({\sqrt {{\bar {\alpha }}_{t}}}{\tilde {x}},\sigma _{t}^{2}I\right)}  ![{\displaystyle {\tilde {x}}_{t}\sim N\left({\sqrt {{\bar {\alpha }}_{t}}}{\tilde {x}},\sigma _{t}^{2}I\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3126b84dfe0b37ed0f66cc575e89e0aaa6f6aa35), a noisy version of        x ~ ~       {\displaystyle {\tilde {x}}}  ![{\displaystyle {\tilde {x}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4f5c5435030c952a58a756e691ea64f60c1bd240), then replacing      x  t     {\displaystyle x_{t}}  ![{\displaystyle x_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f279a30bc8eabc788f3fe81c9cfb674e72e858db) with     ( 1 − −  m ) ⊙ ⊙   x  t   + m ⊙ ⊙      x ~ ~      t     {\displaystyle (1-m)\odot x_{t}+m\odot {\tilde {x}}_{t}}  ![{\displaystyle (1-m)\odot x_{t}+m\odot {\tilde {x}}_{t}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a17035f75725ed4e664f673ae052fe0b631304e3), where     ⊙ ⊙    {\displaystyle \odot }  ![{\displaystyle \odot }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e89e009eb8a8839c82aa5c76c15e9f2d67006276) means [elementwise multiplication](./Hadamard_product_(matrices)).[[50]](./Diffusion_model#cite_note-50) Another application of cross-attention mechanism is prompt-to-prompt image editing.[[51]](./Diffusion_model#cite_note-51)

 

Conditioning is not limited to just generating images from a specific category, or according to a specific caption (as in text-to-image). For example,[[48]](./Diffusion_model#cite_note-:4-48) demonstrated generating human motion, conditioned on an audio clip of human walking (allowing syncing motion to a soundtrack), or video of human running, or a text description of human motion, etc. For how conditional diffusion models are mathematically formulated, see a methodological summary in.[[52]](./Diffusion_model#cite_note-52)

 

### Upscaling

 

As generating an image takes a long time, one can try to generate a small image by a base diffusion model, then upscale it by other models. Upscaling can be done by [GAN](./Generative_adversarial_network),[[53]](./Diffusion_model#cite_note-53) [Transformer](./Transformer_(machine_learning_model)),[[54]](./Diffusion_model#cite_note-54) or signal processing methods like [Lanczos resampling](./Lanczos_resampling).

 

Diffusion models themselves can be used to perform upscaling. Cascading diffusion model stacks multiple diffusion models one after another, in the style of [Progressive GAN](./StyleGAN#Progressive_GAN). The lowest level is a standard diffusion model that generate 32x32 image, then the image would be upscaled by a diffusion model specifically trained for upscaling, and the process repeats.[[45]](./Diffusion_model#cite_note-:3-45)

 

In more detail, the diffusion upscaler is trained as follows:[[45]](./Diffusion_model#cite_note-:3-45)

 
- Sample     (  x  0   ,  z  0   , c )   {\displaystyle (x_{0},z_{0},c)}  ![{\displaystyle (x_{0},z_{0},c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7f376bb518a818d0c9dd8f64f1178637ff3a3fc0), where      x  0     {\displaystyle x_{0}}  ![{\displaystyle x_{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86f21d0e31751534cd6584264ecf864a6aa792cf) is the high-resolution image,      z  0     {\displaystyle z_{0}}  ![{\displaystyle z_{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9e72d1d86e86355892b39b8eb32b964834e113bf) is the same image but scaled down to a low-resolution, and     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) is the conditioning, which can be the caption of the image, the class of the image, etc.
- Sample two white noises      ϵ ϵ   x   ,  ϵ ϵ   z     {\displaystyle \epsilon _{x},\epsilon _{z}}  ![{\displaystyle \epsilon _{x},\epsilon _{z}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c1d35063cb7e4fa9dfe889e89e83d1d245217ef2), two time-steps      t  x   ,  t  z     {\displaystyle t_{x},t_{z}}  ![{\displaystyle t_{x},t_{z}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2831b1f81c27023b4d3d4af480e88b0e35ae8368). Compute the noisy versions of the high-resolution and low-resolution images:       {     x   t  x       =       α α  ¯ ¯       t  x        x  0   +  σ σ    t  x      ϵ ϵ   x        z   t  z       =       α α  ¯ ¯       t  z        z  0   +  σ σ    t  z      ϵ ϵ   z           {\displaystyle {\begin{cases}x_{t_{x}}&={\sqrt {{\bar {\alpha }}_{t_{x}}}}x_{0}+\sigma _{t_{x}}\epsilon _{x}\\z_{t_{z}}&={\sqrt {{\bar {\alpha }}_{t_{z}}}}z_{0}+\sigma _{t_{z}}\epsilon _{z}\end{cases}}}  ![{\displaystyle {\begin{cases}x_{t_{x}}&={\sqrt {{\bar {\alpha }}_{t_{x}}}}x_{0}+\sigma _{t_{x}}\epsilon _{x}\\z_{t_{z}}&={\sqrt {{\bar {\alpha }}_{t_{z}}}}z_{0}+\sigma _{t_{z}}\epsilon _{z}\end{cases}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3188c91ee8a2cea17c6bac011639e8c662b5ffba).
- Train the denoising network to predict      ϵ ϵ   x     {\displaystyle \epsilon _{x}}  ![{\displaystyle \epsilon _{x}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/41af29de2b1d4b9ac93f30b80ff3d21e3a10e32f) given      x   t  x     ,  z   t  z     ,  t  x   ,  t  z   , c   {\displaystyle x_{t_{x}},z_{t_{z}},t_{x},t_{z},c}  ![{\displaystyle x_{t_{x}},z_{t_{z}},t_{x},t_{z},c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/378c504ecda7c62d9d36d1393ce7eb80bc302338). That is, apply gradient descent on     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af) on the L2 loss     ‖ ‖   ϵ ϵ   θ θ    (  x   t  x     ,  z   t  z     ,  t  x   ,  t  z   , c ) − −   ϵ ϵ   x    ‖ ‖   2   2     {\displaystyle \|\epsilon _{\theta }(x_{t_{x}},z_{t_{z}},t_{x},t_{z},c)-\epsilon _{x}\|_{2}^{2}}  ![{\displaystyle \|\epsilon _{\theta }(x_{t_{x}},z_{t_{z}},t_{x},t_{z},c)-\epsilon _{x}\|_{2}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fe24a761f2ef9e6fc11e1de1e63c31c990c575d7).

 

## Examples

 

This section collects some notable diffusion models, and briefly describes their architecture.

 

### OpenAI

 Main articles: [DALL-E](./DALL-E) and [Sora (text-to-video model)](./Sora_(text-to-video_model)) 

The DALL-E series by OpenAI are text-conditional diffusion models of images.

 

The first version of DALL-E (2021) is not actually a diffusion model. Instead, it uses a Transformer architecture that autoregressively generates a sequence of tokens, which is then converted to an image by the decoder of a discrete VAE. Released with DALL-E was the CLIP classifier, which was used by DALL-E to rank generated images according to how close the image fits the text.

 

GLIDE (2022–03)[[55]](./Diffusion_model#cite_note-55) is a 3.5-billion diffusion model, and a small version was released publicly.[[5]](./Diffusion_model#cite_note-dalle2-5) Soon after, DALL-E 2 was released (2022–04).[[56]](./Diffusion_model#cite_note-56) DALL-E 2 is a 3.5-billion cascaded diffusion model that generates images from text by "inverting the CLIP image encoder", the technique which they termed "unCLIP".

 

The unCLIP method contains 4 models: a CLIP image encoder, a CLIP text encoder, an image decoder, and a "prior" model (which can be a diffusion model, or an autoregressive model). During training, the prior model is trained to convert CLIP image encodings to CLIP text encodings. The image decoder is trained to convert CLIP image encodings back to images. During inference, a text is converted by the CLIP text encoder to a vector, then it is converted by the prior model to an image encoding, then it is converted by the image decoder to an image.

 

[Sora](./Sora_(text-to-video_model)) (2024–02) is a diffusion Transformer model (DiT).

 

### Lightricks

 Main article: [LTX (AI Model)](./LTX_(AI_Model)) 

LTX is a family of [open source](./Open_source) [artificial intelligence](./Artificial_intelligence) video [foundation models](./Foundation_model) developed by [Lightricks](./Lightricks), first released in November 2024.[[57]](./Diffusion_model#cite_note-57) The latest models, LTX-2, create videos based on user [prompts](./Prompt_engineering), conditioned on text, images, video or audio - and capable of generating audio and visual in a unified way.[[58]](./Diffusion_model#cite_note-58)[[59]](./Diffusion_model#cite_note-59) They were preceded by LTX Video, which was released in 2024 as the company's first text-to-video model.

 

### Stability AI

 Main article: [Stable Diffusion](./Stable_Diffusion) 

[Stable Diffusion](./Stable_Diffusion) (2022–08), released by Stability AI, consists of a denoising latent diffusion model (860 million parameters), a VAE, and a text encoder. The denoising network is a U-Net, with cross-attention blocks to allow for conditional image generation.[[60]](./Diffusion_model#cite_note-:02-60)[[23]](./Diffusion_model#cite_note-:2-23)

 

Stable Diffusion 3 (2024–03)[[61]](./Diffusion_model#cite_note-:6-61) changed the latent diffusion model from the UNet to a Transformer model, and so it is a DiT. It uses rectified flow.

 

Stable Video 4D (2024–07)[[62]](./Diffusion_model#cite_note-62) is a latent diffusion model for videos of 3D objects.

 

### Google

 

Imagen (2022)[[63]](./Diffusion_model#cite_note-63)[[64]](./Diffusion_model#cite_note-64) uses a [T5-XXL language model](./T5_(language_model)) to encode the input text into an embedding vector. It is a cascaded diffusion model with three sub-models. The first step denoises a white noise to a 64×64 image, conditional on the embedding vector of the text. This model has 2B parameters. The second step upscales the image by 64×64→256×256, conditional on embedding. This model has 650M parameters. The third step is similar, upscaling by 256×256→1024×1024. This model has 400M parameters. The three denoising networks are all U-Nets.

 

Muse (2023–01)[[65]](./Diffusion_model#cite_note-65) is not a diffusion model, but an encoder-only Transformer that is trained to predict masked image tokens from unmasked image tokens.

 

Imagen 2 (2023–12) is also diffusion-based. It can generate images based on a prompt that mixes images and text. No further information available.[[66]](./Diffusion_model#cite_note-66) Imagen 3 (2024–05) is too. No further information available.[[67]](./Diffusion_model#cite_note-67)

 

Veo (2024) generates videos by latent diffusion. The diffusion is conditioned on a vector that encodes both a text prompt and an image prompt.[[68]](./Diffusion_model#cite_note-68)

 

### Meta

 

Make-A-Video (2022) is a text-to-video diffusion model.[[69]](./Diffusion_model#cite_note-69)[[70]](./Diffusion_model#cite_note-70)

 

CM3leon (2023) is not a diffusion model, but an autoregressive causally masked Transformer, with mostly the same architecture as [LLaMa](./Llama_(language_model))-2.[[71]](./Diffusion_model#cite_note-71)[[72]](./Diffusion_model#cite_note-72)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/a/af/Transfusion_%282024%29_Fig_1%2C_architectural_diagram.png/330px-Transfusion_%282024%29_Fig_1%2C_architectural_diagram.png)](./File:Transfusion_(2024)_Fig_1,_architectural_diagram.png)Transfusion architectural diagram 

Transfusion (2024) is a Transformer that combines autoregressive text generation and denoising diffusion. Specifically, it generates text autoregressively (with causal masking), and generates images by denoising multiple times over image tokens (with all-to-all attention).[[73]](./Diffusion_model#cite_note-73)

 

Movie Gen (2024) is a series of Diffusion Transformers operating on latent space and by flow matching.[[74]](./Diffusion_model#cite_note-74)

 

## See also

 
- [Diffusion process](./Diffusion_process)
- [Markov chain](./Markov_chain)
- [Variational inference](./Variational_inference)
- [Variational autoencoder](./Variational_autoencoder)

 

## Further reading

 
- Review papers

- Yang, Ling (2024-09-06), [*YangLing0818/Diffusion-Models-Papers-Survey-Taxonomy*](https://github.com/YangLing0818/Diffusion-Models-Papers-Survey-Taxonomy), retrieved 2024-09-06
- Yang, Ling; Zhang, Zhilong; Song, Yang; Hong, Shenda; Xu, Runsheng; Zhao, Yue; Zhang, Wentao; Cui, Bin; Yang, Ming-Hsuan (2023-11-09). ["Diffusion Models: A Comprehensive Survey of Methods and Applications"](https://dl.acm.org/doi/abs/10.1145/3626235). *ACM Comput. Surv*. **56** (4): 105:1–105:39. [arXiv](./ArXiv_(identifier)):[2209.00796](https://arxiv.org/abs/2209.00796). [doi](./Doi_(identifier)):[10.1145/3626235](https://doi.org/10.1145%2F3626235). [ISSN](./ISSN_(identifier)) [0360-0300](https://search.worldcat.org/issn/0360-0300).
- Austin, Jacob; Johnson, Daniel D.; Ho, Jonathan; Tarlow, Daniel; Rianne van den Berg (2021). "Structured Denoising Diffusion Models in Discrete State-Spaces". [arXiv](./ArXiv_(identifier)):[2107.03006](https://arxiv.org/abs/2107.03006) [[cs.LG](https://arxiv.org/archive/cs.LG)].
- Croitoru, Florinel-Alin; Hondru, Vlad; Ionescu, Radu Tudor; Shah, Mubarak (2023-09-01). "Diffusion Models in Vision: A Survey". *IEEE Transactions on Pattern Analysis and Machine Intelligence*. **45** (9): 10850–10869. [arXiv](./ArXiv_(identifier)):[2209.04747](https://arxiv.org/abs/2209.04747). [Bibcode](./Bibcode_(identifier)):[2023ITPAM..4510850C](https://ui.adsabs.harvard.edu/abs/2023ITPAM..4510850C). [doi](./Doi_(identifier)):[10.1109/TPAMI.2023.3261988](https://doi.org/10.1109%2FTPAMI.2023.3261988). [ISSN](./ISSN_(identifier)) [0162-8828](https://search.worldcat.org/issn/0162-8828). [PMID](./PMID_(identifier)) [37030794](https://pubmed.ncbi.nlm.nih.gov/37030794).

- Mathematical details omitted in the article.

- ["Power of Diffusion Models"](https://astralord.github.io/posts/power-of-diffusion-models/). *AstraBlog*. 2022-09-25. Retrieved 2023-09-25.
- Luo, Calvin (2022-08-25). "Understanding Diffusion Models: A Unified Perspective". [arXiv](./ArXiv_(identifier)):[2208.11970](https://arxiv.org/abs/2208.11970) [[cs.LG](https://arxiv.org/archive/cs.LG)].
- Weng, Lilian (2021-07-11). ["What are Diffusion Models?"](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/). *lilianweng.github.io*. Retrieved 2023-09-25.

- Tutorials

- Nakkiran, Preetum; Bradley, Arwen; Zhou, Hattie; Advani, Madhu (2024). "Step-by-Step Diffusion: An Elementary Tutorial". [arXiv](./ArXiv_(identifier)):[2406.08929](https://arxiv.org/abs/2406.08929) [[cs.LG](https://arxiv.org/archive/cs.LG)].
- ["Guidance: a cheat code for diffusion models"](https://benanne.github.io/2022/05/26/guidance.html). 26 May 2022. Overview of classifier guidance and classifier-free guidance, light on mathematical details.
- Catherine Higham, Desmond J. Higham, and Peter Grindrod: "Diffusion Models for Generative Artificial Intelligence: An Introduction for Applied Mathematicians", SIAM Review, Vol.67, No.3 (2025).

 


