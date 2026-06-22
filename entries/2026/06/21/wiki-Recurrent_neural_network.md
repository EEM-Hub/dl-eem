---
source: sources/wiki-Recurrent_neural_network.md
source_url: https://en.wikipedia.org/wiki/Recurrent_neural_network
---

I'll create an entry summarizing this RNN documentation.

## Recurrent Neural Networks (RNNs): Architecture and Variants

Recurrent neural networks are a class of artificial neural networks designed for sequential data processing (text, speech, time series). Unlike feedforward networks, RNNs have recurrent connections where a neuron's output at one time step feeds back as input at the next, enabling the network to maintain a hidden state that captures temporal dependencies. While historically dominant for sequence tasks, RNNs have been largely superseded by transformers for many applications, though they remain relevant where computational efficiency or real-time processing is critical.

## Key Concepts

- **Recurrent unit**: The fundamental building block; maintains a **hidden state** (memory) updated at each time step based on current input and previous hidden state
- **Core abstraction**: An RNN is a function f_θ: (x_t, h_t) → (y_t, h_{t+1}), mapping input and hidden state to output and updated hidden state
- **Vanishing gradient problem**: Traditional RNNs cannot learn long-range dependencies because gradients shrink exponentially during backpropagation through time
- **LSTM (Long Short-Term Memory)**: Invented by Hochreiter & Schmidhuber (1995/1997); became the default RNN variant by using gating mechanisms to preserve gradients over long sequences
- **GRU (Gated Recurrent Unit)**: A more computationally efficient alternative to LSTM with fewer parameters
- **Unfolding**: An RNN can be "unfolded" in time to visualize as a deep feedforward network — what looks like layers are actually time steps
- **Fully recurrent neural network (FRNN)**: All neuron outputs connect to all neuron inputs; the most general topology
- **Hopfield network**: An RNN with equal-weight connections across layers; converges to stable states, functions as content-addressable memory with Hebbian learning; rooted in statistical mechanics (Ising model / spin glass)

## Configurations (How RNNs Are Combined)

- **Standard RNN**: Single recurrent unit processing one sequence step at a time
- **Stacked/Deep RNN**: Multiple RNN layers stacked vertically; each layer's output sequence becomes input to the layer above; no limit on depth
- **Bidirectional RNN (BiRNN)**: Two RNNs process the same input in opposite directions; outputs concatenated; allows each token to be processed in context of both past and future. **ELMo** (2018) is a stacked bidirectional LSTM producing word embeddings from character inputs
- **Encoder-Decoder (Seq2Seq)**: Two RNNs in sequence — encoder processes input into hidden vectors, decoder generates output from those vectors; optionally uses attention mechanism; dominated machine translation 2014–2017
- **PixelRNN**: Processes 2D data (images) with RNNs; diagonal BiLSTM processes grids from two corners simultaneously

## Architectures (Individual RNN Designs)

- **Elman network** (1990): Three-layer network with context units that store copies of previous hidden layer values; h_t = σ_h(W_h·x_t + U_h·h_{t-1} + b_h), y_t = σ_y(W_y·h_t + b_y)
- **Jordan network** (1986): Similar to Elman but context units fed from output layer instead of hidden layer; context units have self-recurrent connections
- Both Elman and Jordan networks are called **Simple Recurrent Networks (SRN)**

## Relationships

- **Feedforward networks** → RNNs add recurrence; a fully cross-coupled RNN is equivalent to an infinitely deep feedforward network (Rosenblatt, 1961)
- **LSTM / GRU** → Specific gated architectures that solve the vanishing gradient problem in standard RNNs
- **Attention mechanisms** → Developed within the encoder-decoder RNN framework, then became the basis for transformers
- **Transformers** → Replaced RNNs as dominant sequence architecture by enabling parallelization and better long-range dependency handling
- **CNNs** → Combined with LSTM for tasks like automatic image captioning
- **Statistical mechanics** → Hopfield networks derive from Ising model / Sherrington-Kirkpatrick spin glass model
- **Seq2Seq** → The encoder-decoder RNN configuration; instrumental stepping stone to transformer architecture

## Exam-Relevant Points

- RNNs process sequential data by maintaining hidden state; the key distinction from feedforward networks is the recurrent connection
- The vanishing gradient problem limits standard RNNs; LSTM (1997) and GRU are the solutions
- Configuration vs. architecture distinction: configuration = how multiple RNNs are combined (stacked, bidirectional, encoder-decoder); architecture = internal design of each RNN unit (LSTM, GRU, Elman, etc.)
- Bidirectional RNNs require the full sequence upfront (cannot be used for real-time/streaming); standard RNNs can process one step at a time
- Encoder-decoder (seq2seq) architecture was state-of-the-art for machine translation 2014–2017 and led directly to attention and transformers
- Hopfield networks guarantee convergence but require stationary inputs (not truly sequential processing)
- Elman vs. Jordan: Elman feeds hidden→context; Jordan feeds output→context (with self-recurrence)
- Historical roots: neuroscience (Cajal's recurrent circuits, 1901), statistical mechanics (Ising model, 1920s), and McCulloch-Pitts neurons (1943)
- Modern RNN architectures are mainly based on two foundations: LSTM and BRNN (bidirectional)
- Transformers have largely replaced RNNs, but RNNs remain relevant for real-time processing and computationally constrained environments
