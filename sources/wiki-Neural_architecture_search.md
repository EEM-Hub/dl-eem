---
source: https://en.wikipedia.org/wiki/Neural_architecture_search
fetched: 2026-06-21
---

Machine learning-powered structure design 
| Part of a series on |
| --- |
| Machine learninganddata mining |
| ParadigmsSupervised learningUnsupervised learningSemi-supervised learningSelf-supervised learningReinforcement learningMeta-learningOnline learningBatch learningCurriculum learningRule-based learningNeuro-symbolic AINeuromorphic engineeringQuantum machine learning |
| ProblemsClassificationGenerative modelingRegressionClusteringDimensionality reductionDensity estimationAnomaly detectionData cleaningAutoMLAssociation rulesSemantic analysisStructured predictionFeature engineeringFeature learningLearning to rankGrammar inductionOntology learningMultimodal learning |
| Supervised learning(classification•regression)Apprenticeship learningDecision treesEnsemblesBaggingBoostingRandom forestk-NNLinear regressionNaive BayesArtificial neural networksLogistic regressionPerceptronRelevance vector machine (RVM)Support vector machine (SVM) |
| ClusteringBIRCHCUREHierarchicalk-meansFuzzyExpectation–maximization (EM)DBSCANOPTICSMean shift |
| Dimensionality reductionFactor analysisCCAICALDANMFPCAPGDt-SNESDL |
| Structured predictionGraphical modelsBayes netConditional random fieldHidden Markov |
| Anomaly detectionRANSACk-NNLocal outlier factorIsolation forest |
| Neural networksAutoencoderDeep learningFeedforward neural networkRecurrent neural networkLSTMGRUESNreservoir computingBoltzmann machineRestrictedGANDiffusion modelSOMConvolutional neural networkU-NetLeNetAlexNetDeepDreamNeural fieldNeural radiance fieldPhysics-informed neural networksTransformerVisionMambaSpiking neural networkMemtransistorElectrochemical RAM(ECRAM) |
| Reinforcement learningQ-learningPolicy gradientSARSATemporal difference (TD)Multi-agentSelf-play |
| Learning with humansActive learningCrowdsourcingHuman-in-the-loopMechanistic interpretabilityRLHF |
| Model diagnosticsCoefficient of determinationConfusion matrixLearning curveROC curve |
| Mathematical foundationsKernel machinesBias–variance tradeoffComputational learning theoryEmpirical risk minimizationOccam learningPAC learningStatistical learningVC theoryTopological deep learning |
| Journals and conferencesAAAICVPRECCVECML PKDDEMNLPICCVNeurIPSICMLICLRIJCAIMLJMLR |
| Related articlesGlossary of artificial intelligenceList of datasets for machine-learning researchList of datasets in computer vision and image processingOutline of machine learning |
| vte |

 

**Neural architecture search** (**NAS**)[[1]](./Neural_architecture_search#cite_note-survey-1)[[2]](./Neural_architecture_search#cite_note-survey2-2) is a technique for automating the design of [artificial neural networks](./Artificial_neural_network) (ANN), a widely used model in the field of [machine learning](./Machine_learning). NAS has been used to design networks that are on par with or outperform hand-designed architectures.[[3]](./Neural_architecture_search#cite_note-Zoph_2016-3)[[4]](./Neural_architecture_search#cite_note-Zoph_2017-4) Methods for NAS can be categorized according to the search space, search strategy and performance estimation strategy used:[[1]](./Neural_architecture_search#cite_note-survey-1)

 
- The *search space* defines the type(s) of ANN that can be designed and optimized.
- The *search strategy* defines the approach used to explore the search space.
- The *performance estimation strategy* evaluates the performance of a possible ANN from its design (without constructing and training it).

 

NAS is closely related to [hyperparameter optimization](./Hyperparameter_optimization)[[5]](./Neural_architecture_search#cite_note-5) and [meta-learning](./Meta-learning_(computer_science))[[6]](./Neural_architecture_search#cite_note-6) and is a subfield of [automated machine learning](./Automated_machine_learning) (AutoML).[[7]](./Neural_architecture_search#cite_note-7)

 

## Reinforcement learning

 

[Reinforcement learning](./Reinforcement_learning) (RL) can underpin a NAS search strategy. Barret Zoph and [Quoc Viet Le](./Quoc_Viet_Le)[[3]](./Neural_architecture_search#cite_note-Zoph_2016-3) applied NAS with RL targeting the [CIFAR-10](./CIFAR-10) dataset and achieved a network architecture that rivals the best manually-designed architecture for accuracy, with an error rate of 3.65, 0.09 percent better and 1.05x faster than a related hand-designed model. On the [Penn Treebank](./Treebank) dataset, that model composed a recurrent cell that outperforms [LSTM](./Long_short-term_memory), reaching a test set perplexity of 62.4, or 3.6 perplexity better than the prior leading system. On the PTB character language modeling task it achieved bits per character of 1.214.[[3]](./Neural_architecture_search#cite_note-Zoph_2016-3)

 

Learning a model architecture directly on a large dataset can be a lengthy process. NASNet[[4]](./Neural_architecture_search#cite_note-Zoph_2017-4)[[8]](./Neural_architecture_search#cite_note-8) addressed this issue by transferring a building block designed for a small dataset to a larger dataset. The design was constrained to use two types of [convolutional](./Convolutional_neural_network) cells to return feature maps that serve two main functions when convoluting an input feature map: *normal cells* that return maps of the same extent (height and width) and *reduction cells* in which the returned feature map height and width is reduced by a factor of two. For the reduction cell, the initial operation applied to the cell's inputs uses a stride of two (to reduce the height and width).[[4]](./Neural_architecture_search#cite_note-Zoph_2017-4) The learned aspect of the design included elements such as which lower layer(s) each higher layer took as input, the transformations applied at that layer and to merge multiple outputs at each layer. In the studied example, the best convolutional layer (or "cell") was designed for the CIFAR-10 dataset and then applied to the [ImageNet](./ImageNet) dataset by stacking copies of this cell, each with its own parameters. The approach yielded accuracy of 82.7% top-1 and 96.2% top-5. This exceeded the best human-invented architectures at a cost of 9 billion fewer [FLOPS](./FLOPS)—a reduction of 28%. The system continued to exceed the manually-designed alternative at varying computation levels. The image features learned from image classification can be transferred to other computer vision problems. E.g., for object detection, the learned cells integrated with the Faster-RCNN framework improved performance by 4.0% on the [COCO](./COCO_(dataset)) dataset.[[4]](./Neural_architecture_search#cite_note-Zoph_2017-4)

 

In the so-called Efficient Neural Architecture Search (ENAS), a controller discovers architectures by learning to search for an optimal subgraph within a large graph. The controller is trained with [policy gradient](./Reinforcement_learning) to select a subgraph that maximizes the validation set's expected reward. The model corresponding to the subgraph is trained to minimize a canonical [cross entropy](./Cross_entropy) loss. Multiple child models share parameters, ENAS requires fewer GPU-hours than other approaches and 1000-fold less than "standard" NAS. On CIFAR-10, the ENAS design achieved a test error of 2.89%, comparable to NASNet. On Penn Treebank, the ENAS design reached test perplexity of 55.8.[[9]](./Neural_architecture_search#cite_note-9)

 

## Evolution

 

An alternative approach to NAS is based on [evolutionary algorithms](./Evolutionary_algorithm), which has been employed by several groups.[[10]](./Neural_architecture_search#cite_note-10)[[11]](./Neural_architecture_search#cite_note-11)[[12]](./Neural_architecture_search#cite_note-:0-12)[[13]](./Neural_architecture_search#cite_note-Real_2018-13)[[14]](./Neural_architecture_search#cite_note-14)[[15]](./Neural_architecture_search#cite_note-15)[[16]](./Neural_architecture_search#cite_note-Elsken_2018-16) An Evolutionary Algorithm for Neural Architecture Search generally performs the following procedure.[[17]](./Neural_architecture_search#cite_note-liu2021survey-17) First a pool consisting of different candidate architectures along with their validation scores (fitness) is initialised. At each step the architectures in the candidate pool are mutated (e.g.: 3x3 convolution instead of a 5x5 convolution). Next the new architectures are trained from scratch for a few epochs and their validation scores are obtained. This is followed by replacing the lowest scoring architectures in the candidate pool with the better, newer architectures. This procedure is repeated multiple times and thus the candidate pool is refined over time. Mutations in the context of evolving ANNs are operations such as adding or removing a layer, which include changing the type of a layer (e.g., from convolution to pooling), changing the hyperparameters of a layer, or changing the training hyperparameters. On [CIFAR-10](./CIFAR-10) and [ImageNet](./ImageNet), evolution and RL performed comparably, while both slightly outperformed [random search](./Random_search).[[13]](./Neural_architecture_search#cite_note-Real_2018-13)[[12]](./Neural_architecture_search#cite_note-:0-12)

 

## Bayesian optimization

 

[Bayesian Optimization](./Bayesian_Optimization) (BO), which has proven to be an efficient method for hyperparameter optimization, can also be applied to NAS. In this context, the objective function maps an architecture to its validation error after being trained for a number of epochs. At each iteration, BO uses a surrogate to model this objective function based on previously obtained architectures and their validation errors. One then chooses the next architecture to evaluate by maximizing an acquisition function, such as expected improvement, which provides a balance between exploration and exploitation. Acquisition function maximization and objective function evaluation are often computationally expensive for NAS, and make the application of BO challenging in this context. Recently, BANANAS[[18]](./Neural_architecture_search#cite_note-18) has achieved promising results in this direction by introducing a high-performing instantiation of BO coupled to a neural predictor.

 

## Hill-climbing

 

Another group used a [hill climbing](./Hill_climbing) procedure that applies network morphisms, followed by short cosine-annealing optimization runs. The approach yielded competitive results, requiring resources on the same order of magnitude as training a single network. E.g., on CIFAR-10, the method designed and trained a network with an error rate below 5% in 12 hours on a single GPU.[[19]](./Neural_architecture_search#cite_note-19)

 

## Multi-objective search

 

While most approaches solely focus on finding architecture with maximal predictive performance, for most practical applications other objectives are relevant, such as memory consumption, model size or inference time (i.e., the time required to obtain a prediction). Because of that, researchers created a [multi-objective](./Multi-objective_optimization) search.[[16]](./Neural_architecture_search#cite_note-Elsken_2018-16)[[20]](./Neural_architecture_search#cite_note-Zhou_2018-20)

 

LEMONADE[[16]](./Neural_architecture_search#cite_note-Elsken_2018-16) is an evolutionary algorithm that adopted [Lamarckism](./Lamarckism) to efficiently optimize multiple objectives. In every generation, child networks are generated to improve the [Pareto frontier](./Pareto_efficiency#Pareto_frontier) with respect to the current population of ANNs.

 

Neural Architect[[20]](./Neural_architecture_search#cite_note-Zhou_2018-20) is claimed to be a resource-aware multi-objective RL-based NAS with network embedding and performance prediction. Network embedding encodes an existing network to a trainable embedding vector. Based on the embedding, a controller network generates transformations of the target network. A multi-objective reward function considers network accuracy, computational resource and training time. The reward is predicted by multiple performance simulation networks that are pre-trained or co-trained with the controller network. The controller network is trained via policy gradient. Following a modification, the resulting candidate network is evaluated by both an accuracy network and a training time network. The results are combined by a reward engine that passes its output back to the controller network.

 

## One-shot models

 

RL or evolution-based NAS require thousands of GPU-days of searching/training to achieve state-of-the-art computer vision results as described in the NASNet, mNASNet and MobileNetV3 papers.[[4]](./Neural_architecture_search#cite_note-Zoph_2017-4)[[21]](./Neural_architecture_search#cite_note-mNASNet2-21)[[22]](./Neural_architecture_search#cite_note-MobileNetV3-22)

 

To reduce computational cost, many recent NAS methods rely on the weight-sharing idea.[[23]](./Neural_architecture_search#cite_note-23)[[24]](./Neural_architecture_search#cite_note-24) In this approach, a single overparameterized supernetwork (also known as the one-shot model) is defined. A supernetwork is a very large [Directed Acyclic Graph](./Directed_acyclic_graph) (DAG) whose subgraphs are different candidate neural networks. Thus, in a supernetwork, the weights are shared among a large number of different sub-architectures that have edges in common, each of which is considered as a path within the supernet. The essential idea is to train one supernetwork that spans many options for the final design rather than generating and training thousands of networks independently. In addition to the learned parameters, a set of architecture parameters are learnt to depict preference for one module over another. Such methods reduce the required computational resources to only a few GPU days.

 

More recent works further combine this weight-sharing paradigm, with a continuous relaxation of the search space,[[25]](./Neural_architecture_search#cite_note-25)[[26]](./Neural_architecture_search#cite_note-26)[[27]](./Neural_architecture_search#cite_note-H._Liu,_K._Simonyan_1806-27)[[28]](./Neural_architecture_search#cite_note-28) which enables the use of gradient-based optimization methods. These approaches are generally referred to as differentiable NAS and have proven very efficient in exploring the search space of neural architectures. One of the most popular algorithms amongst the gradient-based methods for NAS is DARTS.[[27]](./Neural_architecture_search#cite_note-H._Liu,_K._Simonyan_1806-27) However, DARTS faces problems such as performance collapse due to an inevitable aggregation of skip connections and poor generalization which were tackled by many future algorithms.[[29]](./Neural_architecture_search#cite_note-29)[[30]](./Neural_architecture_search#cite_note-Arber_Zela_1909-30)[[31]](./Neural_architecture_search#cite_note-Xiangning_Chen_2002-31)[[32]](./Neural_architecture_search#cite_note-32) Methods like [[30]](./Neural_architecture_search#cite_note-Arber_Zela_1909-30)[[31]](./Neural_architecture_search#cite_note-Xiangning_Chen_2002-31) aim at robustifying DARTS and making the validation accuracy landscape smoother by introducing a Hessian norm based regularisation and random smoothing/adversarial attack respectively. The cause of performance degradation is later analyzed from the architecture selection aspect.[[33]](./Neural_architecture_search#cite_note-33)

 

Differentiable NAS has shown to produce competitive results using a fraction of the search-time required by RL-based search methods. For example, FBNet (which is short for Facebook Berkeley Network) demonstrated that supernetwork-based search produces networks that outperform the speed-accuracy tradeoff curve of mNASNet and MobileNetV2 on the ImageNet image-classification dataset. FBNet accomplishes this using over 400x *less* search time than was used for mNASNet.[[34]](./Neural_architecture_search#cite_note-FBNet-34)[[35]](./Neural_architecture_search#cite_note-MobileNetV2-35)[[36]](./Neural_architecture_search#cite_note-36) Further, SqueezeNAS demonstrated that supernetwork-based NAS produces neural networks that outperform the speed-accuracy tradeoff curve of MobileNetV3 on the Cityscapes semantic segmentation dataset, and SqueezeNAS uses over 100x less search time than was used in the MobileNetV3 authors' RL-based search.[[37]](./Neural_architecture_search#cite_note-SqueezeNAS-37)[[38]](./Neural_architecture_search#cite_note-38)

 

## Neural architecture search benchmarks

 

Neural architecture search often requires large computational resources, due to its expensive training and evaluation phases. This further leads to a large carbon footprint required for the evaluation of these methods.  To overcome this limitation, NAS benchmarks[[39]](./Neural_architecture_search#cite_note-39)[[40]](./Neural_architecture_search#cite_note-40)[[41]](./Neural_architecture_search#cite_note-41)[[42]](./Neural_architecture_search#cite_note-42) have been introduced, from which one can either query or predict the final performance of neural architectures in seconds. A NAS benchmark is defined as a dataset with a fixed train-test split, a search space, and a fixed training pipeline (hyperparameters). There are primarily two types of NAS benchmarks: a surrogate NAS benchmark and a tabular NAS benchmark. A surrogate benchmark uses a  surrogate model (e.g.: a neural network) to predict the performance of an architecture from the search space. On the other hand, a tabular benchmark queries the actual performance of an architecture trained up to convergence. Both of these benchmarks are queryable and can be used to efficiently simulate many NAS algorithms using only a CPU to query the benchmark instead of training an architecture from scratch.

 

## See also

 
- [Neural Network Intelligence](./Neural_Network_Intelligence)
- [Automated Machine Learning](./Automated_machine_learning)
- [Hyperparameter Optimization](./Hyperparameter_optimization)

 

## Further reading

 

Survey articles.

 
- Wistuba, Martin; Rawat, Ambrish; Pedapati, Tejaswini (2019-05-04). "A Survey on Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[1905.01392](https://arxiv.org/abs/1905.01392) [[cs.LG](https://arxiv.org/archive/cs.LG)].
- Elsken, Thomas; Metzen, Jan Hendrik; Hutter, Frank (August 8, 2019). ["Neural Architecture Search: A Survey"](http://jmlr.org/papers/v20/18-598.html). *Journal of Machine Learning Research*. **20** (55): 1–21. [arXiv](./ArXiv_(identifier)):[1808.05377](https://arxiv.org/abs/1808.05377).
- Liu, Yuqiao; Sun, Yanan; Xue, Bing; Zhang, Mengjie; Yen, Gary G; Tan, Kay Chen (2021). "A Survey on Evolutionary Neural Architecture Search". *IEEE Transactions on Neural Networks and Learning Systems*. **34** (2): 1–21. [arXiv](./ArXiv_(identifier)):[2008.10937](https://arxiv.org/abs/2008.10937). [doi](./Doi_(identifier)):[10.1109/TNNLS.2021.3100554](https://doi.org/10.1109%2FTNNLS.2021.3100554). [PMID](./PMID_(identifier)) [34357870](https://pubmed.ncbi.nlm.nih.gov/34357870). [S2CID](./S2CID_(identifier)) [221293236](https://api.semanticscholar.org/CorpusID:221293236).
- White, Colin; Safari, Mahmoud; Sukthanker, Rhea; Ru, Binxin; Elsken, Thomas; Zela, Arber; Dey, Debadeepta; Hutter, Frank (2023-01-25). "Neural Architecture Search: Insights from 1000 Papers". [arXiv](./ArXiv_(identifier)):[2301.08727](https://arxiv.org/abs/2301.08727) [[cs.LG](https://arxiv.org/archive/cs.LG)].

 

## References

 
1. [1](./Neural_architecture_search#cite_ref-survey_1-0) [2](./Neural_architecture_search#cite_ref-survey_1-1) Elsken, Thomas; Metzen, Jan Hendrik; Hutter, Frank (August 8, 2019). ["Neural Architecture Search: A Survey"](http://jmlr.org/papers/v20/18-598.html). *Journal of Machine Learning Research*. **20** (55): 1–21. [arXiv](./ArXiv_(identifier)):[1808.05377](https://arxiv.org/abs/1808.05377).
2. [↑](./Neural_architecture_search#cite_ref-survey2_2-0) Wistuba, Martin; Rawat, Ambrish; Pedapati, Tejaswini (2019-05-04). "A Survey on Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[1905.01392](https://arxiv.org/abs/1905.01392) [[cs.LG](https://arxiv.org/archive/cs.LG)].
3. [1](./Neural_architecture_search#cite_ref-Zoph_2016_3-0) [2](./Neural_architecture_search#cite_ref-Zoph_2016_3-1) [3](./Neural_architecture_search#cite_ref-Zoph_2016_3-2) Zoph, Barret; Le, Quoc V. (2016-11-04). "Neural Architecture Search with Reinforcement Learning". [arXiv](./ArXiv_(identifier)):[1611.01578](https://arxiv.org/abs/1611.01578) [[cs.LG](https://arxiv.org/archive/cs.LG)].
4. [1](./Neural_architecture_search#cite_ref-Zoph_2017_4-0) [2](./Neural_architecture_search#cite_ref-Zoph_2017_4-1) [3](./Neural_architecture_search#cite_ref-Zoph_2017_4-2) [4](./Neural_architecture_search#cite_ref-Zoph_2017_4-3) [5](./Neural_architecture_search#cite_ref-Zoph_2017_4-4) Zoph, Barret; Vasudevan, Vijay; Shlens, Jonathon; Le, Quoc V. (2017-07-21). "Learning Transferable Architectures for Scalable Image Recognition". [arXiv](./ArXiv_(identifier)):[1707.07012](https://arxiv.org/abs/1707.07012) [[cs.CV](https://arxiv.org/archive/cs.CV)].
5. [↑](./Neural_architecture_search#cite_ref-5) Matthias Feurer and Frank Hutter. [Hyperparameter optimization](https://link.springer.com/content/pdf/10.1007%2F978-3-030-05318-5_1.pdf). In: *AutoML: Methods, Systems, Challenges*, pages 3–38.
6. [↑](./Neural_architecture_search#cite_ref-6) Vanschoren, Joaquin (2019). ["Meta-Learning"](https://link.springer.com/chapter/10.1007/978-3-030-05318-5_2). *Automated Machine Learning*. The Springer Series on Challenges in Machine Learning. pp. 35–61. [doi](./Doi_(identifier)):[10.1007/978-3-030-05318-5_2](https://doi.org/10.1007%2F978-3-030-05318-5_2). [ISBN](./ISBN_(identifier)) [978-3-030-05317-8](./Special:BookSources/978-3-030-05317-8). [S2CID](./S2CID_(identifier)) [239362577](https://api.semanticscholar.org/CorpusID:239362577).
7. [↑](./Neural_architecture_search#cite_ref-7) Salehin, Imrus; Islam, Md. Shamiul; Saha, Pritom; Noman, S. M.; Tuni, Azra; Hasan, Md. Mehedi; Baten, Md. Abu (2024-01-01). ["AutoML: A systematic review on automated machine learning with neural architecture search"](https://doi.org/10.1016%2Fj.jiixd.2023.10.002). *Journal of Information and Intelligence*. **2** (1): 52–81. [doi](./Doi_(identifier)):[10.1016/j.jiixd.2023.10.002](https://doi.org/10.1016%2Fj.jiixd.2023.10.002). [ISSN](./ISSN_(identifier)) [2949-7159](https://search.worldcat.org/issn/2949-7159).
8. [↑](./Neural_architecture_search#cite_ref-8) Zoph, Barret; Vasudevan, Vijay; Shlens, Jonathon; Le, Quoc V. (November 2, 2017). ["AutoML for large scale image classification and object detection"](https://research.googleblog.com/2017/11/automl-for-large-scale-image.html). *Research Blog*. Retrieved 2018-02-20.
9. [↑](./Neural_architecture_search#cite_ref-9) Pham, Hieu; Guan, Melody Y.; Zoph, Barret; Le, Quoc V.; Dean, Jeff (2018-02-09). "Efficient Neural Architecture Search via Parameter Sharing". [arXiv](./ArXiv_(identifier)):[1802.03268](https://arxiv.org/abs/1802.03268) [[cs.LG](https://arxiv.org/archive/cs.LG)].
10. [↑](./Neural_architecture_search#cite_ref-10) Real, Esteban; Moore, Sherry; Selle, Andrew; Saxena, Saurabh; Suematsu, Yutaka Leon; Tan, Jie; Le, Quoc; Kurakin, Alex (2017-03-03). "Large-Scale Evolution of Image Classifiers". [arXiv](./ArXiv_(identifier)):[1703.01041](https://arxiv.org/abs/1703.01041) [[cs.NE](https://arxiv.org/archive/cs.NE)].
11. [↑](./Neural_architecture_search#cite_ref-11) Suganuma, Masanori; Shirakawa, Shinichi; Nagao, Tomoharu (2017-04-03). "A Genetic Programming Approach to Designing Convolutional Neural Network Architectures". [arXiv](./ArXiv_(identifier)):[1704.00764v2](https://arxiv.org/abs/1704.00764v2) [[cs.NE](https://arxiv.org/archive/cs.NE)].
12. [1](./Neural_architecture_search#cite_ref-:0_12-0) [2](./Neural_architecture_search#cite_ref-:0_12-1) Liu, Hanxiao; Simonyan, Karen; Vinyals, Oriol; Fernando, Chrisantha; Kavukcuoglu, Koray (2017-11-01). "Hierarchical Representations for Efficient Architecture Search". [arXiv](./ArXiv_(identifier)):[1711.00436v2](https://arxiv.org/abs/1711.00436v2) [[cs.LG](https://arxiv.org/archive/cs.LG)].
13. [1](./Neural_architecture_search#cite_ref-Real_2018_13-0) [2](./Neural_architecture_search#cite_ref-Real_2018_13-1) Real, Esteban; Aggarwal, Alok; Huang, Yanping; Le, Quoc V. (2018-02-05). "Regularized Evolution for Image Classifier Architecture Search". [arXiv](./ArXiv_(identifier)):[1802.01548](https://arxiv.org/abs/1802.01548) [[cs.NE](https://arxiv.org/archive/cs.NE)].
14. [↑](./Neural_architecture_search#cite_ref-14) Miikkulainen, Risto; Liang, Jason; Meyerson, Elliot; Rawal, Aditya; Fink, Dan; Francon, Olivier; Raju, Bala; Shahrzad, Hormoz; Navruzyan, Arshak; Duffy, Nigel; Hodjat, Babak (2017-03-04). "Evolving Deep Neural Networks". [arXiv](./ArXiv_(identifier)):[1703.00548](https://arxiv.org/abs/1703.00548) [[cs.NE](https://arxiv.org/archive/cs.NE)].
15. [↑](./Neural_architecture_search#cite_ref-15) Xie, Lingxi; Yuille, Alan (2017). "Genetic CNN". *2017 IEEE International Conference on Computer Vision (ICCV)*. pp. 1388–1397. [arXiv](./ArXiv_(identifier)):[1703.01513](https://arxiv.org/abs/1703.01513). [doi](./Doi_(identifier)):[10.1109/ICCV.2017.154](https://doi.org/10.1109%2FICCV.2017.154). [ISBN](./ISBN_(identifier)) [978-1-5386-1032-9](./Special:BookSources/978-1-5386-1032-9). [S2CID](./S2CID_(identifier)) [206770867](https://api.semanticscholar.org/CorpusID:206770867).
16. [1](./Neural_architecture_search#cite_ref-Elsken_2018_16-0) [2](./Neural_architecture_search#cite_ref-Elsken_2018_16-1) [3](./Neural_architecture_search#cite_ref-Elsken_2018_16-2) Elsken, Thomas; Metzen, Jan Hendrik; Hutter, Frank (2018-04-24). "Efficient Multi-objective Neural Architecture Search via Lamarckian Evolution". [arXiv](./ArXiv_(identifier)):[1804.09081](https://arxiv.org/abs/1804.09081) [[stat.ML](https://arxiv.org/archive/stat.ML)].
17. [↑](./Neural_architecture_search#cite_ref-liu2021survey_17-0) Liu, Yuqiao; Sun, Yanan; Xue, Bing; Zhang, Mengjie; Yen, Gary G; Tan, Kay Chen (2021). "A Survey on Evolutionary Neural Architecture Search". *IEEE Transactions on Neural Networks and Learning Systems*. **34** (2): 1–21. [arXiv](./ArXiv_(identifier)):[2008.10937](https://arxiv.org/abs/2008.10937). [doi](./Doi_(identifier)):[10.1109/TNNLS.2021.3100554](https://doi.org/10.1109%2FTNNLS.2021.3100554). [PMID](./PMID_(identifier)) [34357870](https://pubmed.ncbi.nlm.nih.gov/34357870). [S2CID](./S2CID_(identifier)) [221293236](https://api.semanticscholar.org/CorpusID:221293236).
18. [↑](./Neural_architecture_search#cite_ref-18) White, Colin; Neiswanger, Willie; Savani, Yash (2020-11-02). "BANANAS: Bayesian Optimization with Neural Architectures for Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[1910.11858](https://arxiv.org/abs/1910.11858) [[cs.LG](https://arxiv.org/archive/cs.LG)].
19. [↑](./Neural_architecture_search#cite_ref-19) Thomas, Elsken; Jan Hendrik, Metzen; Frank, Hutter (2017-11-13). "Simple And Efficient Architecture Search for Convolutional Neural Networks". [arXiv](./ArXiv_(identifier)):[1711.04528](https://arxiv.org/abs/1711.04528) [[stat.ML](https://arxiv.org/archive/stat.ML)].
20. [1](./Neural_architecture_search#cite_ref-Zhou_2018_20-0) [2](./Neural_architecture_search#cite_ref-Zhou_2018_20-1) Zhou, Yanqi; Diamos, Gregory. ["Neural Architect: A Multi-objective Neural Architecture Search with Performance Prediction"](https://web.archive.org/web/20190927090457/https://www.sysml.cc/doc/2018/94.pdf) (PDF). Baidu. Archived from [the original](https://www.sysml.cc/doc/2018/94.pdf) (PDF) on 2019-09-27. Retrieved 2019-09-27.
21. [↑](./Neural_architecture_search#cite_ref-mNASNet2_21-0) Tan, Mingxing; Chen, Bo; Pang, Ruoming; Vasudevan, Vijay; Sandler, Mark; Howard, Andrew; Le, Quoc V. (2018). "MnasNet: Platform-Aware Neural Architecture Search for Mobile". [arXiv](./ArXiv_(identifier)):[1807.11626](https://arxiv.org/abs/1807.11626) [[cs.CV](https://arxiv.org/archive/cs.CV)].
22. [↑](./Neural_architecture_search#cite_ref-MobileNetV3_22-0) Howard, Andrew; Sandler, Mark; Chu, Grace; Chen, Liang-Chieh; Chen, Bo; Tan, Mingxing; Wang, Weijun; Zhu, Yukun; Pang, Ruoming; Vasudevan, Vijay; Le, Quoc V.; Adam, Hartwig (2019-05-06). "Searching for MobileNetV3". [arXiv](./ArXiv_(identifier)):[1905.02244](https://arxiv.org/abs/1905.02244) [[cs.CV](https://arxiv.org/archive/cs.CV)].
23. [↑](./Neural_architecture_search#cite_ref-23) Pham, Hieu; Guan, Melody Y.; Zoph, Barret; Le, Quoc V.; Dean, Jeff (2018). "Efficient Neural Architecture Search via Parameter Sharing". [arXiv](./ArXiv_(identifier)):[1802.03268](https://arxiv.org/abs/1802.03268) [[cs.LG](https://arxiv.org/archive/cs.LG)].
24. [↑](./Neural_architecture_search#cite_ref-24) Li, Liam; Talwalkar, Ameet (2019). "Random Search and Reproducibility for Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[1902.07638](https://arxiv.org/abs/1902.07638) [[cs.LG](https://arxiv.org/archive/cs.LG)].
25. [↑](./Neural_architecture_search#cite_ref-25) Cai, Han; Zhu, Ligeng; Han, Song (2018). "ProxylessNAS: Direct Neural Architecture Search on Target Task and Hardware". [arXiv](./ArXiv_(identifier)):[1812.00332](https://arxiv.org/abs/1812.00332) [[cs.LG](https://arxiv.org/archive/cs.LG)].
26. [↑](./Neural_architecture_search#cite_ref-26) Dong, Xuanyi; Yang, Yi (2019). "Searching for a Robust Neural Architecture in Four GPU Hours". [arXiv](./ArXiv_(identifier)):[1910.04465](https://arxiv.org/abs/1910.04465) [[cs.CV](https://arxiv.org/archive/cs.CV)].
27. [1](./Neural_architecture_search#cite_ref-H._Liu,_K._Simonyan_1806_27-0) [2](./Neural_architecture_search#cite_ref-H._Liu,_K._Simonyan_1806_27-1) Liu, Hanxiao; Simonyan, Karen; Yang, Yiming (2018). "DARTS: Differentiable Architecture Search". [arXiv](./ArXiv_(identifier)):[1806.09055](https://arxiv.org/abs/1806.09055) [[cs.LG](https://arxiv.org/archive/cs.LG)].
28. [↑](./Neural_architecture_search#cite_ref-28) Xie, Sirui; Zheng, Hehui; Liu, Chunxiao; Lin, Liang (2018). "SNAS: Stochastic Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[1812.09926](https://arxiv.org/abs/1812.09926) [[cs.LG](https://arxiv.org/archive/cs.LG)].
29. [↑](./Neural_architecture_search#cite_ref-29) Chu, Xiangxiang; Zhou, Tianbao; Zhang, Bo; Li, Jixiang (2019). "Fair DARTS: Eliminating Unfair Advantages in Differentiable Architecture Search". [arXiv](./ArXiv_(identifier)):[1911.12126](https://arxiv.org/abs/1911.12126) [[cs.LG](https://arxiv.org/archive/cs.LG)].
30. [1](./Neural_architecture_search#cite_ref-Arber_Zela_1909_30-0) [2](./Neural_architecture_search#cite_ref-Arber_Zela_1909_30-1) Zela, Arber; Elsken, Thomas; Saikia, Tonmoy; Marrakchi, Yassine; Brox, Thomas; Hutter, Frank (2019). "Understanding and Robustifying Differentiable Architecture Search". [arXiv](./ArXiv_(identifier)):[1909.09656](https://arxiv.org/abs/1909.09656) [[cs.LG](https://arxiv.org/archive/cs.LG)].
31. [1](./Neural_architecture_search#cite_ref-Xiangning_Chen_2002_31-0) [2](./Neural_architecture_search#cite_ref-Xiangning_Chen_2002_31-1) Chen, Xiangning; Hsieh, Cho-Jui (2020). "Stabilizing Differentiable Architecture Search via Perturbation-based Regularization". [arXiv](./ArXiv_(identifier)):[2002.05283](https://arxiv.org/abs/2002.05283) [[cs.LG](https://arxiv.org/archive/cs.LG)].
32. [↑](./Neural_architecture_search#cite_ref-32) Xu, Yuhui; Xie, Lingxi; Zhang, Xiaopeng; Chen, Xin; Qi, Guo-Jun; Tian, Qi; Xiong, Hongkai (2019). "PC-DARTS: Partial Channel Connections for Memory-Efficient Architecture Search". [arXiv](./ArXiv_(identifier)):[1907.05737](https://arxiv.org/abs/1907.05737) [[cs.CV](https://arxiv.org/archive/cs.CV)].
33. [↑](./Neural_architecture_search#cite_ref-33) Wang, Ruochen; Cheng, Minhao; Chen, Xiangning; Tang, Xiaocheng; Hsieh, Cho-Jui (2021). "Rethinking Architecture Selection in Differentiable NAS". [arXiv](./ArXiv_(identifier)):[2108.04392](https://arxiv.org/abs/2108.04392) [[cs.LG](https://arxiv.org/archive/cs.LG)].
34. [↑](./Neural_architecture_search#cite_ref-FBNet_34-0) Wu, Bichen; Dai, Xiaoliang; Zhang, Peizhao; Wang, Yanghan; Sun, Fei; Wu, Yiming; Tian, Yuandong; Vajda, Peter; Jia, Yangqing; Keutzer, Kurt (24 May 2019). "FBNet: Hardware-Aware Efficient ConvNet Design via Differentiable Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[1812.03443](https://arxiv.org/abs/1812.03443) [[cs.CV](https://arxiv.org/archive/cs.CV)].
35. [↑](./Neural_architecture_search#cite_ref-MobileNetV2_35-0) Sandler, Mark; Howard, Andrew; Zhu, Menglong; Zhmoginov, Andrey; Chen, Liang-Chieh (2018). "MobileNetV2: Inverted Residuals and Linear Bottlenecks". [arXiv](./ArXiv_(identifier)):[1801.04381](https://arxiv.org/abs/1801.04381) [[cs.CV](https://arxiv.org/archive/cs.CV)].
36. [↑](./Neural_architecture_search#cite_ref-36) Keutzer, Kurt (2019-05-22). ["Co-Design of DNNs and NN Accelerators"](https://site.ieee.org/scv-cas/files/2019/05/2019-05-22-ieee-co-design-trim.pdf) (PDF). *IEEE*. Retrieved 2019-09-26.
37. [↑](./Neural_architecture_search#cite_ref-SqueezeNAS_37-0) Shaw, Albert; Hunter, Daniel; Iandola, Forrest; Sidhu, Sammy (2019). "SqueezeNAS: Fast neural architecture search for faster semantic segmentation". [arXiv](./ArXiv_(identifier)):[1908.01748](https://arxiv.org/abs/1908.01748) [[cs.CV](https://arxiv.org/archive/cs.CV)].
38. [↑](./Neural_architecture_search#cite_ref-38) Yoshida, Junko (2019-08-25). ["Does Your AI Chip Have Its Own DNN?"](https://www.eetimes.com/document.asp?doc_id=1335063). *EE Times*. Retrieved 2019-09-26.
39. [↑](./Neural_architecture_search#cite_ref-39) Ying, Chris; Klein, Aaron; Real, Esteban; Christiansen, Eric; Murphy, Kevin; Hutter, Frank (2019). "NAS-Bench-101: Towards Reproducible Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[1902.09635](https://arxiv.org/abs/1902.09635) [[cs.LG](https://arxiv.org/archive/cs.LG)].
40. [↑](./Neural_architecture_search#cite_ref-40) Zela, Arber; Siems, Julien; Hutter, Frank (2020). "NAS-Bench-1Shot1: Benchmarking and Dissecting One-shot Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[2001.10422](https://arxiv.org/abs/2001.10422) [[cs.LG](https://arxiv.org/archive/cs.LG)].
41. [↑](./Neural_architecture_search#cite_ref-41) Dong, Xuanyi; Yang, Yi (2020). "NAS-Bench-201: Extending the Scope of Reproducible Neural Architecture Search". [arXiv](./ArXiv_(identifier)):[2001.00326](https://arxiv.org/abs/2001.00326) [[cs.CV](https://arxiv.org/archive/cs.CV)].
42. [↑](./Neural_architecture_search#cite_ref-42) Zela, Arber; Siems, Julien; Zimmer, Lucas; Lukasik, Jovita; Keuper, Margret; Hutter, Frank (2020). "Surrogate NAS Benchmarks: Going Beyond the Limited Search Spaces of Tabular NAS Benchmarks". [arXiv](./ArXiv_(identifier)):[2008.09777](https://arxiv.org/abs/2008.09777) [[cs.LG](https://arxiv.org/archive/cs.LG)].

 
| vteDifferentiable computing |
| --- |
| General | Differentiable programmingInformation geometryStatistical manifoldAutomatic differentiationNeuromorphic computingPattern recognitionRicci calculusComputational learning theoryInductive bias |
| Hardware | IPUTPUVPUMemristorSpiNNaker |
| Software libraries | TensorFlowPyTorchKerasscikit-learnTheanoJAXFlux.jlMindSpore |
| PortalsComputer programmingTechnology |