---
source: sources/wiki-Long_short-term_memory.md
source_url: https://en.wikipedia.org/wiki/Long_short-term_memory
---

I've prepared the LSTM study entry but the file write permission hasn't been granted yet. Here's the content I'm trying to write to `entries/2026/06/21/wiki-Long_short-term_memory.md`:

## LSTM (Long Short-Term Memory) Networks

**Summary**: LSTM is a specialized RNN architecture that solves the vanishing gradient problem using a gated memory cell with three gates (forget, input, output) and a cell state that acts as a "constant error carousel" allowing gradients to flow across long sequences.

**Key highlights from the entry**:

- **Three gates** (all sigmoid): forget (discard old info), input (store new info), output (expose cell state)
- **Cell state update**: `c_t = f_t . c_{t-1} + i_t . c_tilde_t` — the core equation
- **Forget gate was added in 2000** (Gers et al.), not in the original 1997 paper
- **Solves vanishing gradients but NOT exploding gradients**
- **Variants covered**: standard LSTM, peephole LSTM (gates access cell state directly), ConvLSTM (convolutions replace matrix multiply)
- **Training**: gradient descent + BPTT; CTC for sequence labeling; neuroevolution/policy gradient for unsupervised
- **Key applications**: speech recognition (Google 2015), machine translation, time series, handwriting recognition

Could you grant write permission so I can save this entry?
