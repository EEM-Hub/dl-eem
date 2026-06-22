---
source: sources/wiki-Neural_architecture_search.md
source_url: https://en.wikipedia.org/wiki/Neural_architecture_search
---

I'll create an entry for this topic.

## Neural Architecture Search (NAS)

Neural Architecture Search (NAS) automates the design of artificial neural network architectures, replacing manual architecture engineering with algorithmic search. It is a subfield of Automated Machine Learning (AutoML), closely related to hyperparameter optimization and meta-learning. NAS methods are defined by three components: the search space (what architectures are possible), the search strategy (how to explore them), and the performance estimation strategy (how to evaluate candidates without full training).

## Key Concepts

- **Three pillars of NAS**: search space, search strategy, and performance estimation strategy
- **Search space** defines the types of ANN that can be designed and optimized
- **Search strategy** defines the approach for exploring the search space (RL, evolution, Bayesian optimization, gradient-based, hill climbing)
- **Performance estimation strategy** evaluates a candidate ANN from its design without fully constructing and training it
- **NASNet cell transfer**: learn architecture cells on small datasets (CIFAR-10), then stack them with separate parameters for large datasets (ImageNet) — achieved 82.7% top-1 accuracy on ImageNet with 28% fewer FLOPS than hand-designed architectures
- **Normal cells** return feature maps of the same spatial dimensions; **reduction cells** halve height and width (stride of 2)
- **ENAS (Efficient NAS)**: controller learns to select optimal subgraphs within a large computational graph; child models share parameters, reducing cost 1000x vs standard NAS
- **Evolutionary NAS**: maintains a candidate pool, mutates architectures (change layer types, add/remove layers, modify hyperparameters), replaces lowest-scoring candidates with better offspring
- **On CIFAR-10 and ImageNet, evolutionary and RL-based NAS performed comparably**, both slightly outperforming random search
- **Weight-sharing / one-shot models (supernets)**: train a single overparameterized supernetwork (a large DAG) whose subgraphs represent candidate architectures; shared weights reduce search cost to a few GPU days
- **Differentiable NAS (DARTS)**: continuous relaxation of the discrete search space enables gradient-based optimization; orders of magnitude faster than RL-based search
- **DARTS failure mode**: performance collapse from aggregation of skip connections; addressed by Hessian-norm regularization and random smoothing
- **FBNet**: supernetwork-based search outperformed mNASNet and MobileNetV2 on ImageNet using 400x less search time
- **Multi-objective NAS**: optimizes not just accuracy but also memory, model size, and inference time simultaneously
- **LEMONADE**: evolutionary multi-objective NAS using Lamarckian inheritance to improve the Pareto frontier
- **BANANAS**: Bayesian optimization with a neural predictor for NAS — uses a surrogate model to approximate the objective function (architecture -> validation error)
- **NAS benchmarks**: tabular (query actual pre-computed performance) and surrogate (predict performance via a model) — eliminate need for GPU training during search algorithm development

## Commands and Syntax

No specific CLI commands or code APIs are described in this source. NAS is presented at the algorithmic/conceptual level. Key implementation references:

- **NASNet**: search on CIFAR-10, transfer cells to ImageNet by stacking
- **ENAS**: controller trained with policy gradient; child models share parameters
- **DARTS**: continuous relaxation + gradient descent over architecture parameters
- **Hill climbing approach**: network morphisms + short cosine-annealing runs; achieved <5% error on CIFAR-10 in 12 hours on a single GPU

## Relationships

- **Parent field**: AutoML (Automated Machine Learning)
- **Sibling techniques**: hyperparameter optimization, meta-learning
- **Search strategies draw from**: reinforcement learning (policy gradient), evolutionary algorithms, Bayesian optimization, gradient-based optimization, hill climbing
- **Architectures discovered by NAS**: NASNet, MnasNet, MobileNetV3, FBNet, SqueezeNAS
- **Evaluation datasets**: CIFAR-10, ImageNet, Penn Treebank, COCO, Cityscapes
- **Downstream integration**: NAS-discovered cells can be plugged into existing frameworks (e.g., Faster R-CNN for object detection)
- **Connects to network efficiency**: multi-objective NAS directly addresses deployment constraints (latency, memory, model size)
- **Supernet / weight-sharing** connects to knowledge distillation and parameter-efficient methods

## Exam-Relevant Points

- NAS is defined by three components: search space, search strategy, and performance estimation strategy
- NAS is a subfield of AutoML, related to hyperparameter optimization and meta-learning
- RL-based NAS (Zoph & Le, 2016) was the seminal work; achieved competitive results on CIFAR-10 (3.65% error) and Penn Treebank (62.4 perplexity)
- NASNet introduced the cell transfer paradigm: design on small data, stack on large data
- Normal cells preserve spatial dimensions; reduction cells halve them (stride 2)
- ENAS reduces compute by 1000x through parameter sharing across child models
- Evolutionary NAS and RL-based NAS perform comparably; both slightly beat random search
- One-shot models / supernets use weight sharing to reduce search cost from thousands of GPU-days to a few GPU-days
- DARTS is the most prominent differentiable NAS method; suffers from skip-connection collapse
- FBNet achieved 400x search speedup over mNASNet; SqueezeNAS achieved 100x over MobileNetV3 search
- Multi-objective NAS optimizes accuracy alongside inference time, memory, and model size (Pareto frontier)
- NAS benchmarks (tabular and surrogate) enable CPU-only evaluation of search algorithms, reducing compute and carbon footprint
- Bayesian optimization for NAS uses a surrogate model and acquisition function (e.g., expected improvement) to balance exploration vs exploitation
