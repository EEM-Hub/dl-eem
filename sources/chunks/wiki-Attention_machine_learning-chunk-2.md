---
source: sources/wiki-Attention_machine_learning.md
source_url: https://en.wikipedia.org/wiki/Attention_(machine_learning)
chunk: 2/3
---

## Mathematical representation

 

### Standard scaled dot-product attention

 

For matrices:     Q ∈ ∈    R   m × ×   d  k     , K ∈ ∈    R   n × ×   d  k       {\displaystyle Q\in \mathbb {R} ^{m\times d_{k}},K\in \mathbb {R} ^{n\times d_{k}}}  ![{\displaystyle Q\in \mathbb {R} ^{m\times d_{k}},K\in \mathbb {R} ^{n\times d_{k}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/32465b005ab325fcae5d7dc472b578d060b8ff99) and     V ∈ ∈    R   n × ×   d  v       {\displaystyle V\in \mathbb {R} ^{n\times d_{v}}}  ![{\displaystyle V\in \mathbb {R} ^{n\times d_{v}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/202925a11ae6c1678f0975f8902dfc398a8626e3), the scaled dot-product, or QKV attention, is defined as:
     Attention  ( Q , K , V ) =  softmax   (    Q  K  T      d  k      )  V ∈ ∈    R   m × ×   d  v       {\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}\left({\frac {QK^{T}}{\sqrt {d_{k}}}}\right)V\in \mathbb {R} ^{m\times d_{v}}}  ![{\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}\left({\frac {QK^{T}}{\sqrt {d_{k}}}}\right)V\in \mathbb {R} ^{m\times d_{v}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/db3106d8746fa638cda2e3440cd2438c7e682bde)
where         T     {\displaystyle {}^{T}}  ![{\displaystyle {}^{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8f5df5b5ecb120f5e7f4837d839c7c3181a08346) denotes [transpose](./Matrix_transpose) and the [softmax function](./Softmax_function) is applied independently to every row of its argument. The matrix     Q   {\displaystyle Q}  ![{\displaystyle Q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8752c7023b4b3286800fe3238271bbca681219ed) contains     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) queries, while matrices     K , V   {\displaystyle K,V}  ![{\displaystyle K,V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c1059d12adb442403ba8c33fd0379064bb9754bb) jointly contain an *unordered* set of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) key-value pairs. Value vectors in matrix     V   {\displaystyle V}  ![{\displaystyle V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/af0f6064540e84211d0ffe4dac72098adfa52845) are weighted using the weights resulting from the softmax operation, so that the rows of the     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc)-by-     d  v     {\displaystyle d_{v}}  ![{\displaystyle d_{v}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4034edfd613443b0938cb4da1899ab1ce102da2a) output matrix are confined to the [convex hull](./Convex_hull) of the points in       R    d  v       {\displaystyle \mathbb {R} ^{d_{v}}}  ![{\displaystyle \mathbb {R} ^{d_{v}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f17b1fab835e9a966e7a1f9c75875f98d3de3970) given by the rows of     V   {\displaystyle V}  ![{\displaystyle V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/af0f6064540e84211d0ffe4dac72098adfa52845).

 

To understand the permutation invariance and permutation equivariance properties of QKV attention,[[57]](./Attention_(machine_learning)#cite_note-SetTransformer-57) let     A ∈ ∈    R   m × ×  m     {\displaystyle A\in \mathbb {R} ^{m\times m}}  ![{\displaystyle A\in \mathbb {R} ^{m\times m}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/900e5c7a9590bf32dbf6130f6f7579df9027d80c) and     B ∈ ∈    R   n × ×  n     {\displaystyle B\in \mathbb {R} ^{n\times n}}  ![{\displaystyle B\in \mathbb {R} ^{n\times n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3a6da48b3b39c68ecfdbddb3367c0bb9c6c5dab8) be [permutation matrices](./Permutation_matrix); and     D ∈ ∈    R   m × ×  n     {\displaystyle D\in \mathbb {R} ^{m\times n}}  ![{\displaystyle D\in \mathbb {R} ^{m\times n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4078865760ea47300ba9eb9958cbc326e836c6da) an arbitrary matrix. The softmax function is permutation equivariant in the sense that:
     softmax  ( A D B ) = A   softmax  ( D ) B   {\displaystyle {\text{softmax}}(ADB)=A\,{\text{softmax}}(D)B}  ![{\displaystyle {\text{softmax}}(ADB)=A\,{\text{softmax}}(D)B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/03aacfdd979d855aff47c20abf94d6d4f5271a20)
By noting that the transpose of a permutation matrix is also its inverse, it follows that:
     Attention  ( A Q , B K , B V ) = A   Attention  ( Q , K , V )   {\displaystyle {\text{Attention}}(AQ,BK,BV)=A\,{\text{Attention}}(Q,K,V)}  ![{\displaystyle {\text{Attention}}(AQ,BK,BV)=A\,{\text{Attention}}(Q,K,V)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8cdee6b028b70be2e05e00a58783c9f9c646e24e)
which shows that QKV attention is [equivariant](./Equivariance) with respect to re-ordering the queries (rows of     Q   {\displaystyle Q}  ![{\displaystyle Q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8752c7023b4b3286800fe3238271bbca681219ed)); and [invariant](./Invariant_(mathematics)) to re-ordering of the key-value pairs in     K , V   {\displaystyle K,V}  ![{\displaystyle K,V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c1059d12adb442403ba8c33fd0379064bb9754bb). These properties are inherited when applying linear transforms to the inputs and outputs of QKV attention blocks. For example, a simple self-attention function defined as:
    X ↦ ↦   Attention  ( X  T  q   , X  T  k   , X  T  v   )   {\displaystyle X\mapsto {\text{Attention}}(XT_{q},XT_{k},XT_{v})}  ![{\displaystyle X\mapsto {\text{Attention}}(XT_{q},XT_{k},XT_{v})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d70ba131ae5fab0bf4ed87a19c9e32fdb306d1e7)  
is permutation equivariant with respect to re-ordering the rows of the input matrix     X   {\displaystyle X}  ![{\displaystyle X}](https://wikimedia.org/api/rest_v1/media/math/render/svg/68baa052181f707c662844a465bfeeb135e82bab) in a non-trivial way, because every row of the output is a function of all the rows of the input. Similar properties hold for *multi-head attention*, which is defined below.

 

### Masked attention

 

When QKV attention is used as a building block for an autoregressive decoder, and when at training time all input and output matrices have     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) rows, a masked attention variant is used:
     Attention  ( Q , K , V ) =  softmax   (     Q  K  T      d  k      + M  )  V   {\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}\left({\frac {QK^{T}}{\sqrt {d_{k}}}}+M\right)V}  ![{\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}\left({\frac {QK^{T}}{\sqrt {d_{k}}}}+M\right)V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f2344362e74c257757b96397c5e7d2acb2f27f07)
where the mask,     M ∈ ∈    R   n × ×  n     {\displaystyle M\in \mathbb {R} ^{n\times n}}  ![{\displaystyle M\in \mathbb {R} ^{n\times n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba045fb18350a8830da60df84aa1bc0f699a2dd8) is a [strictly upper triangular matrix](./Triangular_matrix), with zeros on and below the diagonal and     − −  ∞ ∞    {\displaystyle -\infty }  ![{\displaystyle -\infty }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ca2608c4b5fd3bffc73585f8c67e379b4e99b6f1) in every element above the diagonal. The softmax output, also in       R   n × ×  n     {\displaystyle \mathbb {R} ^{n\times n}}  ![{\displaystyle \mathbb {R} ^{n\times n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7095e87521f2c247d021fa7101072f11beba0a70) is then *lower triangular*, with zeros in all elements above the diagonal. The masking ensures that for all     1 ≤ ≤  i < j ≤ ≤  n   {\displaystyle 1\leq i<j\leq n}  ![{\displaystyle 1\leq i<j\leq n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/05aa5c14ef41693716e76cecdd716851f4f5d304), row     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) of the attention output is independent of row     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0) of any of the three input matrices. The permutation invariance and equivariance properties of standard QKV attention do not hold for the masked variant.

 

### Multi-head attention

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Encoder_cross-attention%2C_multiheaded_version.png/250px-Encoder_cross-attention%2C_multiheaded_version.png)](./File:Encoder_cross-attention,_multiheaded_version.png)Decoder multiheaded cross-attention 

Multi-head attention
     MultiHead  ( Q , K , V ) =  Concat  (   head   1   , . . . ,   head   h   )  W  O     {\displaystyle {\text{MultiHead}}(Q,K,V)={\text{Concat}}({\text{head}}_{1},...,{\text{head}}_{h})W^{O}}  ![{\displaystyle {\text{MultiHead}}(Q,K,V)={\text{Concat}}({\text{head}}_{1},...,{\text{head}}_{h})W^{O}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/008a9557a33d71fa3d16abe664eb4fc257d5a6db)
where each head is computed with QKV attention as:
      head   i   =  Attention  ( Q  W  i   Q   , K  W  i   K   , V  W  i   V   )   {\displaystyle {\text{head}}_{i}={\text{Attention}}(QW_{i}^{Q},KW_{i}^{K},VW_{i}^{V})}  ![{\displaystyle {\text{head}}_{i}={\text{Attention}}(QW_{i}^{Q},KW_{i}^{K},VW_{i}^{V})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fba64142fc62f2da5f4ed116d6cc19772a89bba)
and      W  i   Q   ,  W  i   K   ,  W  i   V     {\displaystyle W_{i}^{Q},W_{i}^{K},W_{i}^{V}}  ![{\displaystyle W_{i}^{Q},W_{i}^{K},W_{i}^{V}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3087f1739ddc134719d701163d3a75af985498b1), and      W  O     {\displaystyle W^{O}}  ![{\displaystyle W^{O}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7f0f376fd1863b3a195a6bf34b56ff43ec5d695f) are parameter matrices.

 

The permutation properties of (standard, unmasked) QKV attention apply here also. For permutation matrices,     A , B   {\displaystyle A,B}  ![{\displaystyle A,B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/96c3298ea9aa77c226be56a7d8515baaa517b90b):
     MultiHead  ( A Q , B K , B V ) = A   MultiHead  ( Q , K , V )   {\displaystyle {\text{MultiHead}}(AQ,BK,BV)=A\,{\text{MultiHead}}(Q,K,V)}  ![{\displaystyle {\text{MultiHead}}(AQ,BK,BV)=A\,{\text{MultiHead}}(Q,K,V)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3b87f0747c0651491cc17e9b81eb7c3256dc782)
from which we also see that multi-head self-attention:
    X ↦ ↦   MultiHead  ( X  T  q   , X  T  k   , X  T  v   )   {\displaystyle X\mapsto {\text{MultiHead}}(XT_{q},XT_{k},XT_{v})}  ![{\displaystyle X\mapsto {\text{MultiHead}}(XT_{q},XT_{k},XT_{v})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0630d9f93e5736f659a56b908fa8234198c3672c)  
is equivariant with respect to re-ordering of the rows of input matrix     X   {\displaystyle X}  ![{\displaystyle X}](https://wikimedia.org/api/rest_v1/media/math/render/svg/68baa052181f707c662844a465bfeeb135e82bab).

 

### Bahdanau (additive) attention

 

     Attention  ( Q , K , V ) =  softmax  ( tanh ⁡ ⁡  (  W  Q   Q +  W  K   K ) ) V   {\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}(\tanh(W_{Q}Q+W_{K}K))V}  ![{\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}(\tanh(W_{Q}Q+W_{K}K))V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/40d34445e83f991acd397ab8979f2f194f5c530e)
where      W  Q     {\displaystyle W_{Q}}  ![{\displaystyle W_{Q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/27233f4471dd458034969c094d1ac13bff1e38d1) and      W  K     {\displaystyle W_{K}}  ![{\displaystyle W_{K}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1476608b04371ce36cdf6625d8b9ba8a96c615b9) are learnable weight matrices.[[11]](./Attention_(machine_learning)#cite_note-bahdanau-11)

 

### Luong attention (general)

 

     Attention  ( Q , K , V ) =  softmax  ( Q W  K  T   ) V   {\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}(QWK^{T})V}  ![{\displaystyle {\text{Attention}}(Q,K,V)={\text{softmax}}(QWK^{T})V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5e929a24c593127608cadcb84997c67fdb434741)
where     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7) is a learnable weight matrix.[[38]](./Attention_(machine_learning)#cite_note-xy-dot-38)

 

### Self-attention

 

Self-attention is essentially the same as cross-attention, except that query, key, and value vectors all come from the same model. Both encoder and decoder can use self-attention, but with subtle differences.

 

For encoder self-attention, we can start with a simple encoder without self-attention, such as an "embedding layer", which simply converts each input word into a vector by a fixed [lookup table](./Lookup_table). This gives a sequence of hidden vectors      h  0   ,  h  1   , … …    {\displaystyle h_{0},h_{1},\dots }  ![{\displaystyle h_{0},h_{1},\dots }](https://wikimedia.org/api/rest_v1/media/math/render/svg/1c31f089081e2b1d4e3022a7c2e090cb393f74b5). These can then be applied to a dot-product attention mechanism, to obtain         h  0  ′     =  A t t e n t i o n  (  h  0    W  Q   , H  W  K   , H  W  V   )      h  1  ′     =  A t t e n t i o n  (  h  1    W  Q   , H  W  K   , H  W  V   )         ⋮ ⋮        {\displaystyle {\begin{aligned}h_{0}'&=\mathrm {Attention} (h_{0}W^{Q},HW^{K},HW^{V})\\h_{1}'&=\mathrm {Attention} (h_{1}W^{Q},HW^{K},HW^{V})\\&\;\,\vdots \end{aligned}}}  ![{\displaystyle {\begin{aligned}h_{0}'&=\mathrm {Attention} (h_{0}W^{Q},HW^{K},HW^{V})\\h_{1}'&=\mathrm {Attention} (h_{1}W^{Q},HW^{K},HW^{V})\\&\;\,\vdots \end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2c8313b988269a80d9ff4a821dd650a069eb5ed7)or more succinctly,      H ′  =  A t t e n t i o n  ( H  W  Q   , H  W  K   , H  W  V   )   {\displaystyle H'=\mathrm {Attention} (HW^{Q},HW^{K},HW^{V})}  ![{\displaystyle H'=\mathrm {Attention} (HW^{Q},HW^{K},HW^{V})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f4c3a1f071c91152b75f73e4dce95c0ceb90394c). This can be applied repeatedly, to obtain a multilayered encoder. This is the "encoder self-attention", sometimes called the "all-to-all attention", as the vector at every position can attend to every other.

 

### Masking

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/72/Decoder_self-attention_with_causal_masking%2C_detailed_diagram.png/250px-Decoder_self-attention_with_causal_masking%2C_detailed_diagram.png)](./File:Decoder_self-attention_with_causal_masking,_detailed_diagram.png)Decoder self-attention with causal masking, detailed diagram

For decoder self-attention, all-to-all attention is inappropriate, because during the autoregressive decoding process, the decoder cannot attend to future outputs that has yet to be decoded. This can be solved by forcing the attention weights      w  i j   = 0   {\displaystyle w_{ij}=0}  ![{\displaystyle w_{ij}=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/22675f237ad99282d4a6cd7e9742aeeeb1e049fb) for all     i < j   {\displaystyle i<j}  ![{\displaystyle i<j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e60ff2d1b23e30fb2979e8c1536da03493f943cf), called "causal masking". This attention mechanism is the "causally masked self-attention".

 

## See also

 
- [Recurrent neural network](./Recurrent_neural_network)
- [seq2seq](./Seq2seq)
- [Transformer (deep learning architecture)](./Transformer_(deep_learning_architecture))
- [Attention](./Attention)
- [Dynamic neural network](./Dynamic_neural_network)

 


