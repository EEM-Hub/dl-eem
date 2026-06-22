---
source: sources/wiki-Transformer_deep_learning_architecture.md
source_url: https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)
---

I'll create the study notes entry now.

## Transformer Architecture (Deep Learning)

The transformer is a family of neural network architectures introduced in the 2017 paper "Attention Is All You Need" by Google researchers. It replaces recurrent processing with parallel multi-head self-attention, enabling efficient training on GPUs and forming the foundation of modern large language models (LLMs), vision models, and multimodal systems.

## Key Concepts

- **Core mechanism**: Multi-head self-attention allows each token to attend to all other (unmasked) tokens in parallel, amplifying important signals and diminishing less relevant ones
- **Tokenization pipeline**: Text → preprocessor (pretokenization) → tokenizer (maps to vocabulary V) → integer IDs → embedding vectors
- **Positional information**: Self-attention is permutation-invariant, so transformers must inject positional information via positional encodings or learned positional embeddings
- **Three architecture variants**:
  - **Encoder-only** (e.g., BERT): optimized for representation learning / understanding tasks
  - **Decoder-only** (e.g., GPT series): optimized for autoregressive generation
  - **Encoder-decoder** (original transformer): optimized for sequence-to-sequence tasks like translation
- **Advantage over RNNs**: No recurrent units means all tokens processed in parallel; eliminates vanishing gradient problem of sequential processing
- **Trade-off**: Computation is quadratic in context window size (vs. linear for RNNs)
- **Primary components**: Tokenizer, embedding layer, transformer layers (alternating attention + feedforward), un-embedding layer
- **Pre-LN vs Post-LN**: Pre-layer-normalization (applying LayerNorm before attention/FFN) stabilizes training and removes the need for learning rate warmup; now more common than original post-LN

## Three Language Modeling Tasks

- **Masked** (e.g., BERT): Random tokens masked; model predicts masked tokens from context. Loss = negative sum of log-probabilities of masked tokens
- **Autoregressive** (e.g., GPT): Predict next token sequentially; entire sequence initially masked, tokens revealed one at a time
- **PrefixLM** (e.g., T5): Sequence split into prefix (context) and target; model autoregressively predicts the target portion

## Commands and Syntax

No CLI commands per se, but key architectural formulas and conventions:

- **Vector convention**: All vectors are row vectors; linear layer = multiply by weight matrix on the right: `xW`
- **Loss function** (all three tasks): `Loss = -Σ ln(P(t | context))` summed over predicted tokens
- **Learning rate warmup** (original transformer): Linear scale from 0 to max over first ~2% of training steps, then decay
- **Vocabulary size |V|**: Key hyperparameter — smaller = more character-level tokens per word; larger = whole-word tokens

## Relationships

- **Predecessors**: Elman networks (1990) → LSTM (1997) → Seq2seq with attention (2014-2016) → Transformer (2017)
- **LSTM**: Solved vanishing gradient with gating but remained sequential; transformer replaced it for most tasks
- **Seq2seq**: Encoder-decoder framework originated with RNNs; transformer kept the architecture but removed recurrence
- **Attention mechanism**: Evolved from additive attention in RNN search (Bahdanau 2014) → decomposable self-attention on feedforward networks (2016) → multi-head attention in transformer
- **Downstream models**: BERT (encoder-only, 2018), GPT series (decoder-only, 2018+), T5 (encoder-decoder), Vision Transformer (ViT), Whisper (audio), DALL-E/Stable Diffusion/Sora (image/video generation)
- **Training paradigm**: Self-supervised pretraining on large unlabeled corpus → supervised fine-tuning on task-specific data
- **Convolutional neural networks**: Vision transformers stimulated new CNN developments in return
- **Mamba / SSMs**: Emerging alternatives addressing quadratic complexity

## Exam-Relevant Points

- The original transformer paper is "Attention Is All You Need" (2017), published by Google researchers; the model was ~100M parameters
- Self-attention is **permutation-invariant** — positional encodings are required to preserve token order
- Transformer computation scales **quadratically** with context window size; RNNs scale linearly but cannot parallelize
- **Pre-LN** (layer norm before attention/FFN) is now standard and eliminates the need for learning rate warmup; the original paper used **post-LN**
- BERT = encoder-only (masked language modeling); GPT = decoder-only (autoregressive); T5 = encoder-decoder (prefixLM)
- "Masked" in masked language modeling (randomly hiding tokens for prediction) is **not the same** as "masked" in masked attention (causal attention preventing future token visibility)
- Google Neural Machine Translation (2016) used 8-layer bidirectional LSTM before being partially replaced by transformer encoder in 2020
- The pretrain-finetune paradigm: pretrain with self-supervised learning on unlabeled data (e.g., The Pile), then fine-tune with supervised learning on labeled task data
- Key predecessor milestones: LSTM (1997), Seq2seq (2014), Bahdanau attention (2014), decomposable attention on feedforward nets (2016)
- Transformers are applied beyond NLP: computer vision (ViT), speech (Whisper), robotics, reinforcement learning, multimodal learning, image/video generation
