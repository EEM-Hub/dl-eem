---
source: sources/wiki-Transfer_learning.md
source_url: https://en.wikipedia.org/wiki/Transfer_learning
---

## Transfer Learning in Deep Learning

Transfer learning (TL) is a machine learning technique where knowledge learned from one task (the **source**) is reused to improve performance on a different but related task (the **target**). For example, a model trained to recognize cars can transfer learned features to help recognize trucks. First explored in neural networks by Bozinovski and Fulgosi (1976), it became a major practical paradigm after Andrew Ng predicted at NIPS 2016 that transfer learning would be the next driver of ML commercial success after supervised learning.

## Key Concepts

- **Source domain (D_S) and target domain (D_T)**: Transfer learning applies when domains or tasks differ — either the feature spaces, marginal distributions, label spaces, or predictive functions are different between source and target.
- **Domain**: Defined as a feature space X and a marginal probability distribution P(X).
- **Task**: Defined as a label space Y and a predictive function f: X → Y, learned from training pairs {x_i, y_i}.
- **Positive transfer**: When source knowledge improves target performance (e.g., shared low-level visual features across image tasks).
- **Negative transfer**: When source knowledge *hurts* target performance — demonstrated as early as 1981 experiments with letter recognition datasets.
- **Pre-training can hurt**: Zoph et al. (2020) showed that pre-training can reduce accuracy in some settings, advocating self-training as an alternative.
- Transfer learning is related to **cost-sensitive machine learning** and **multi-objective optimization** because it involves training with multiple objective functions.
- End-users of pre-trained models can modify fully-connected layer structure to improve performance on their target task.

## Commands and Syntax

No specific CLI commands. Transfer learning is implemented via framework APIs. The general procedure is:

1. **Train or obtain a pre-trained model** on a large source dataset (e.g., ImageNet for vision, large text corpus for NLP).
2. **Freeze early layers** that capture general features (edges, textures, basic language patterns).
3. **Replace/retrain later layers** (especially fully-connected classification heads) for the target task.
4. **Fine-tune** with a lower learning rate on the target dataset, optionally unfreezing deeper layers progressively.

## Relationships

- **Domain adaptation**: A sub-problem of transfer learning focused specifically on bridging distribution differences between source and target domains.
- **Multi-task learning**: Related but distinct — MTL trains on multiple tasks simultaneously; TL uses a pre-trained model sequentially.
- **Zero-shot learning**: Extreme case where no target-task training examples are available; relies entirely on transferred knowledge.
- **Feature learning / representation learning**: Transfer learning exploits learned representations — early layers learn transferable features, later layers learn task-specific ones.
- **Self-supervised learning**: Often used as the pre-training phase for transfer learning (e.g., BERT, GPT pre-training on unlabeled data before fine-tuning).
- **Fine-tuning**: The most common mechanism by which transfer learning is implemented in practice (especially with large pre-trained models like transformers).

## Exam-Relevant Points

- Transfer learning is formally defined by source/target **domains** (feature space + marginal distribution) and **tasks** (label space + predictive function). Transfer applies when either domain or task differs.
- First neural network transfer learning paper: **Bozinovski and Fulgosi, 1976**.
- Both **positive and negative transfer** are possible — negative transfer was experimentally demonstrated as early as 1981.
- Key survey papers: Pan & Yang (2009/2010), Zhuang et al. (2019).
- **Pre-training is not always beneficial**: Zoph et al. (2020) showed pre-training can hurt accuracy; self-training may be preferable.
- Transfer learning has been successfully applied across domains: image classification, text classification, medical imaging, spam filtering, EEG/EMG signal classification, game playing, and cancer subtype discovery.
- Cross-domain transfer between **EMG and EEG signals** works bidirectionally due to similar physical natures of the signals (Bird et al., 2020).
- Algorithms exist for transfer learning in **Markov logic networks** and **Bayesian networks**, not just neural networks.
- Andrew Ng (NIPS 2016): predicted transfer learning as the next major driver of ML commercial success after supervised learning.
