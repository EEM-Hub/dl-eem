---
source: sources/wiki-Attention_machine_learning.md
source_url: https://en.wikipedia.org/wiki/Attention_(machine_learning)
---

## Attention Mechanisms in Deep Learning

Attention is a method that determines the relative importance of each component in a sequence by assigning learned "soft" weights. Originally developed to address the limitations of recurrent neural networks (which favor recent information due to vanishing gradients), attention allows any token to directly access any other token in a sequence. The mechanism was transformative when formalized as self-attention in the 2017 Transformer architecture, which replaced sequential recurrence with parallelizable attention and became the foundation for BERT, GPT, and modern large language models.

## Key Concepts

- **Soft vs. hard weights**: "Hard" weights are learned during backpropagation and are fixed at inference; "soft" attention weights are computed dynamically during the forward pass and change with every input.
- **Query-Key-Value (QKV)**: The core abstraction — queries (what to look for), keys (what to match against), and values (what to retrieve). Attention computes a weighted sum of values based on query-key similarity.
- **Scaled dot-product attention**: `Attention(Q,K,V) = softmax(QK^T / sqrt(d_k)) V` — scaling by `sqrt(d_k)` prevents dot products from growing large and collapsing softmax into a hard max on a single token.
- **Self-attention**: Each element in the input attends to all other elements in the same sequence, capturing global dependencies without recurrence.
- **Cross-attention**: Queries come from the decoder, keys and values from the encoder — used in encoder-decoder architectures like machine translation.
- **Context vector**: The weighted sum `c = H * w`, where H is the matrix of encoder hidden states and w is the attention weight vector. This is the attention module's output.
- **Alignment matrix**: Stacking soft attention weight vectors reveals which source tokens align to which target tokens (e.g., in translation).
- **Permutation equivariance**: QKV attention is equivariant to permutations of queries and invariant to permutations of key-value pairs — the output does not depend on the ordering of keys/values.
- **Attention output is confined to the convex hull** of the value vectors — each output row is a convex combination of V's rows.

## Commands and Syntax

**Scaled dot-product attention formula:**
```
Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) * V
```
Where:
- `Q ∈ R^(m × d_k)` — m query vectors of dimension d_k
- `K ∈ R^(n × d_k)` — n key vectors of dimension d_k
- `V ∈ R^(n × d_v)` — n value vectors of dimension d_v
- Output ∈ `R^(m × d_v)`
- Softmax is applied row-wise

**Column-vector correct form** (when vectors are columns, not rows):
```
(X W_v)^T * [softmax((W_k X^T) * (x W_q)^T)]
```

## Relationships

- **Transformer architecture**: Attention is the core mechanism; the Transformer replaced RNN recurrence entirely with multi-head self-attention ("Attention Is All You Need", 2017).
- **RNN / Seq2Seq**: Attention was originally grafted onto RNN encoder-decoders (Bahdanau 2014) to solve long-sentence translation degradation.
- **Vanishing gradient problem**: Attention was developed specifically to circumvent the information attenuation in deep recurrent networks.
- **Word embeddings (GloVe, Word2Vec)**: Input embeddings are typically pre-computed and fed into the attention mechanism.
- **Vision Transformers (ViT)**: Self-attention applied to image patches; attention maps serve as saliency/interpretability visualizations.
- **Flash Attention**: An implementation optimization that tiles the attention computation into blocks fitting GPU SRAM, reducing O(n^2) memory to O(n) without approximation.
- **Efficient Transformers (Reformer, Linformer, Performer)**: Approximate attention with sub-quadratic complexity for long sequences.
- **Graph Attention Networks (GAT)**: Extend attention to non-sequential, graph-structured data.
- **Hopfield networks**: Reinterpreted as associative memory systems equivalent to attention.

## Exam-Relevant Points

- The attention matrix size is **O(n^2)** in sequence length — this is the primary scalability bottleneck and the motivation for Flash Attention and efficient variants.
- **Bahdanau (additive) attention** uses a learned feedforward network to compute alignment scores; **Luong (multiplicative) attention** uses dot products.
- The `sqrt(d_k)` scaling factor prevents dot products from having high variance, which would cause softmax to saturate and attend to only one token.
- Self-attention was introduced in 2017 with the Transformer; earlier attention (2014) was cross-attention between encoder and decoder.
- **Flash Attention** achieves memory reduction by partitioning computation into tiles that fit in GPU on-chip SRAM — it is exact, not an approximation.
- Attention maps do **not** reliably explain model decisions — higher attention scores do not always correlate with greater impact on output.
- Five major attention variants: (1) encoder-decoder dot product, (2) encoder-decoder QKV, (3) encoder-only dot product (autocorrelation), (4) encoder-only QKV (self-attention), (5) fully-connected layer attention.
- Fast weight controllers (Schmidhuber, 1992) anticipated modern self-attention and were later renamed "linearized self-attention."
- For CNNs, attention operates on three dimensions: **spatial**, **channel**, or **combined**.
- Attention rollout computes a composite attention map across all layers by taking the dot product of successive per-layer attention matrices.
