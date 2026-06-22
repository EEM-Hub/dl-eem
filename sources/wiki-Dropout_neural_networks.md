---
source: https://en.wikipedia.org/wiki/Dropout_(neural_networks)
fetched: 2026-06-21
---

Regularization method for artificial neural networks [![](//upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Dropout_mechanism.png/250px-Dropout_mechanism.png)](./File:Dropout_mechanism.png)On the left is a fully connected neural network with two hidden layers. On the right is the same network after applying dropout. 

**Dropout** is a [regularization](./Regularization_(mathematics)) technique for reducing [overfitting](./Overfitting) in [artificial neural networks](./Artificial_neural_network) by preventing complex co-adaptations on [training data](./Training,_validation,_and_test_sets). The technique consists of randomly setting the inputs and/or outputs of neurons to zero. It is performed during the training process of a neural network, not during inference.[[1]](./Dropout_(neural_networks)#cite_note-MyUser_Jmlr.org_July_26_2015c-1)[[2]](./Dropout_(neural_networks)#cite_note-2)[[3]](./Dropout_(neural_networks)#cite_note-MyUser_Arxiv.org_July_26_2015c-3)

 

A related older technique is *dilution*, which randomly decreases weights towards zero.[[4]](./Dropout_(neural_networks)#cite_note-:1-4)

 

## Dilution

 

Dilution is usually split in *weak dilution* and *strong dilution*. Weak dilution describes the process in which the finite fraction of removed connections is small, and strong dilution refers to when this fraction is large. There is no clear distinction on where the limit between strong and weak dilution is, and often the distinction is dependent on the precedent of a specific use-case and has implications for how to solve for exact solutions.

 

Sometimes dilution is used for adding damping noise to the inputs. In that case, weak dilution refers to adding a small amount of damping noise, while strong dilution refers to adding a greater amount of damping noise. Both can be rewritten as variants of weight dilution.

 

These techniques are also sometimes referred to as random pruning of weights, but this is usually a non-recurring one-way operation. The network is pruned, and then kept if it is an improvement over the previous model. Dilution and dropout both refer to an iterative process. The pruning of weights typically does not imply that the network continues learning, while in dilution/dropout, the network continues to learn after the technique is applied.

 

### Generalized linear network

 

Output from a layer of linear nodes, in an artificial neural net can be described as

 
| yi=∑jwijxj{\displaystyle y_{i}=\sum _{j}w_{ij}x_{j}} |  | 1 |
| --- | --- | --- |

 
-      y  i     {\displaystyle y_{i}}  ![{\displaystyle y_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/67d30d30b6c2dbe4d6f150d699de040937ecc95f) – output from node     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20)
-      w  i j     {\displaystyle w_{ij}}  ![{\displaystyle w_{ij}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3302ff355269436b43bc2fbe180303881c09321) – real weight before dilution, also called the Hebb connection strength
-      x  j     {\displaystyle x_{j}}  ![{\displaystyle x_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5db47cb3d2f9496205a17a6856c91c1d3d363ccd) – input from node     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0)

 

This can be written in [vector notation](./Vector_notation) as

 
| y=Wx{\displaystyle \mathbf {y} =\mathbf {W} \mathbf {x} } |  | 2 |
| --- | --- | --- |

 
-      y    {\displaystyle \mathbf {y} }  ![{\displaystyle \mathbf {y} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/bb25a040b592282dc2a254c3117e792c3c81161f) – output vector
-      W    {\displaystyle \mathbf {W} }  ![{\displaystyle \mathbf {W} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/04749f1e87cca59c094da23c79cc64b085b0df12) – weight matrix
-      x    {\displaystyle \mathbf {x} }  ![{\displaystyle \mathbf {x} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/32adf004df5eb0a8c7fd8c0b6b7405183c5a5ef2) – input vector

 

Equations (1) and (2) are used in the subsequent sections.

 

### Weak dilution

 

During weak dilution, the finite fraction of removed connections (the weights) is small, giving rise to a tiny uncertainty. This edge-case can be solved exactly with [mean field theory](./Mean_field_theory). In weak dilution the impact on the weights can be described as

 
| w^ij={wij,withP(c)0,otherwise{\displaystyle {\hat {w}}_{ij}={\begin{cases}w_{ij},&{\text{with }}P(c)\\0,&{\text{otherwise}}\end{cases}}} |  | 3 |
| --- | --- | --- |

 
-         w ^ ^      i j     {\displaystyle {\hat {w}}_{ij}}  ![{\displaystyle {\hat {w}}_{ij}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/38800c644360409d5c3a1f549c3cd9c4cc65438e) – diluted weight
-      w  i j     {\displaystyle w_{ij}}  ![{\displaystyle w_{ij}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3302ff355269436b43bc2fbe180303881c09321) – real weight before dilution
-     P ( c )   {\displaystyle P(c)}  ![{\displaystyle P(c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8e2f929d4bafddb3fa6b9f3d5accc287de5bc887) – the probability of     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455), the probability of keeping a weight

 

The interpretation of probability     P ( c )   {\displaystyle P(c)}  ![{\displaystyle P(c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8e2f929d4bafddb3fa6b9f3d5accc287de5bc887) can also be changed from keeping a weight into pruning a weight.

 

In vector notation this can be written as

 
| W^=g⁡(W,c){\displaystyle {\hat {\mathbf {W} }}=\operatorname {g} \left(\mathbf {W} ,c\right)} |  | 4 |
| --- | --- | --- |

 

where the function     g ⁡ ⁡  ( ⋅ ⋅  )   {\displaystyle \operatorname {g} (\cdot )}  ![{\displaystyle \operatorname {g} (\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65754ed1ca1a6132f1f1ffdc8d0195816d71f711) imposes the previous dilution.

 

In weak dilution only a small and fixed fraction of the weights are diluted. When the number of terms in the sum goes to infinite (the weights for each node) it is still infinite (the fraction is fixed), thus [mean field theory](./Mean_field_theory) can be applied. In the notation from Hertz et al.[[4]](./Dropout_(neural_networks)#cite_note-:1-4) this would be written as

 
| ⟨hi⟩=c∑jwij⟨Sj⟩{\displaystyle \left\langle h_{i}\right\rangle =c\sum _{j}w_{ij}\left\langle S_{j}\right\rangle } |  | 5 |
| --- | --- | --- |

 
-      ⟨  h  i   ⟩    {\displaystyle \left\langle h_{i}\right\rangle }  ![{\displaystyle \left\langle h_{i}\right\rangle }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d65769963434479bbf76befa1c11d553060dd281) the mean field temperature
-     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) – a scaling factor for the temperature from the probability of keeping the weight
-      w  i j     {\displaystyle w_{ij}}  ![{\displaystyle w_{ij}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3302ff355269436b43bc2fbe180303881c09321) – real weight before dilution, also called the Hebb connection strength
-      ⟨  S  j   ⟩    {\displaystyle \left\langle S_{j}\right\rangle }  ![{\displaystyle \left\langle S_{j}\right\rangle }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7c36fc66e6e093a527bb20d97ab2e63a960472c9) – the mean stable equilibrium states

 

There are some assumptions for this to hold, which are not listed here.[[5]](./Dropout_(neural_networks)#cite_note-5)[[6]](./Dropout_(neural_networks)#cite_note-6)

 

### Strong dilution

 

When the dilution is strong, the finite fraction of removed connections (the weights) is large, giving rise to a huge uncertainty.

 

## Dropout

 

Dropout is a special case of the previous weight equation (**[3](./Dropout_(neural_networks)#math_3)**), where the aforementioned equation is adjusted to remove a whole row in the vector matrix, and not only random weights

 
| w^j={wj,withP(c)0,otherwise{\displaystyle {\hat {\mathbf {w} }}_{j}={\begin{cases}\mathbf {w} _{j},&{\text{with }}P(c)\\\mathbf {0} ,&{\text{otherwise}}\end{cases}}} |  | 6 |
| --- | --- | --- |

 
-     P ( c )   {\displaystyle P(c)}  ![{\displaystyle P(c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8e2f929d4bafddb3fa6b9f3d5accc287de5bc887) – the probability     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) to keep a row in the weight matrix
-       w   j     {\displaystyle \mathbf {w} _{j}}  ![{\displaystyle \mathbf {w} _{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c54e896400d339e82f70e65bdf7865b0f9993624) – real row in the weight matrix before dropout
-          w  ^ ^      j     {\displaystyle {\hat {\mathbf {w} }}_{j}}  ![{\displaystyle {\hat {\mathbf {w} }}_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4596ef571cb41e38a5afa7699166e38780e3eb30) – diluted row in the weight matrix

 

Because dropout removes a whole row from the vector matrix, the previous (unlisted) assumptions for weak dilution and the use of mean field theory are not applicable.

 

The process by which the node is driven to zero, whether by setting the weights to zero, by “removing the node”, or by some other means, does not impact the end result and does not create a new and unique case. If the neural net is processed by a high-performance digital array-multiplicator, then it is likely more effective to drive the value to zero late in the [process graph](./Process_graph). If the net is processed by a constrained processor, perhaps even an analog neuromorphic processor, then it is likely a more power-efficient solution is to drive the value to zero early in the process graph.

 

## Google's patent

 

Although there have been examples of randomly removing connections between [neurons](./Artificial_neuron) in a neural network to improve models,[[4]](./Dropout_(neural_networks)#cite_note-:1-4) this technique was first introduced with the name *dropout* by [Geoffrey Hinton](./Geoffrey_Hinton), et al. in 2012.[[3]](./Dropout_(neural_networks)#cite_note-MyUser_Arxiv.org_July_26_2015c-3) [Google](./Google) currently holds the patent for the dropout technique.[[7]](./Dropout_(neural_networks)#cite_note-pat-7)[[note 1]](./Dropout_(neural_networks)#cite_note-8)

 

## See also

 
- [AlexNet](./AlexNet)
- [Convolutional neural network § Dropout](./Convolutional_neural_network#Dropout)

 

## Notes

 
1. [↑](./Dropout_(neural_networks)#cite_ref-8) The patent is most likely not valid due to previous art. “Dropout” has been described as “dilution” in previous publications. It is described by Hertz, Krogh, and Palmer in *Introduction to the Theory of Neural Computation* (1991) [ISBN](./ISBN_(identifier)) [0-201-51560-1](./Special:BookSources/0-201-51560-1), pp. 45, *Weak Dilution*. The text references Sompolinsky *The Theory of Neural Networks: The Hebb Rules and Beyond* in *Heidelberg Colloquium on Glossy Dynamics* (1987) and Canning and Gardner *Partially Connected Models of Neural Networks* in *Journal of Physics* (1988). It goes on to describe strong dilution. This predates Hinton's paper.

 

## References

  
1. [↑](./Dropout_(neural_networks)#cite_ref-MyUser_Jmlr.org_July_26_2015c_1-0) ["Dropout: A Simple Way to Prevent Neural Networks from Overfitting"](http://jmlr.org/papers/v15/srivastava14a.html). *Jmlr.org*. Retrieved July 26, 2015.
2. [↑](./Dropout_(neural_networks)#cite_ref-2) Warde-Farley, David; Goodfellow, Ian J.; Courville, Aaron; Bengio, Yoshua (2013-12-20). "An empirical analysis of dropout in piecewise linear networks". [arXiv](./ArXiv_(identifier)):[1312.6197](https://arxiv.org/abs/1312.6197) [[stat.ML](https://arxiv.org/archive/stat.ML)].
3. [1](./Dropout_(neural_networks)#cite_ref-MyUser_Arxiv.org_July_26_2015c_3-0) [2](./Dropout_(neural_networks)#cite_ref-MyUser_Arxiv.org_July_26_2015c_3-1) Hinton, Geoffrey E.; Srivastava, Nitish; Krizhevsky, Alex; Sutskever, Ilya; Salakhutdinov, Ruslan R. (2012). "Improving neural networks by preventing co-adaptation of feature detectors". [arXiv](./ArXiv_(identifier)):[1207.0580](https://arxiv.org/abs/1207.0580) [[cs.NE](https://arxiv.org/archive/cs.NE)].
4. [1](./Dropout_(neural_networks)#cite_ref-:1_4-0) [2](./Dropout_(neural_networks)#cite_ref-:1_4-1) [3](./Dropout_(neural_networks)#cite_ref-:1_4-2) Hertz, John; Krogh, Anders; Palmer, Richard (1991). *Introduction to the Theory of Neural Computation*. Redwood City, California: Addison-Wesley Pub. Co. pp. 45–46. [ISBN](./ISBN_(identifier)) [0-201-51560-1](./Special:BookSources/0-201-51560-1).
5. [↑](./Dropout_(neural_networks)#cite_ref-5) Sompolinsky, H. (1987), "The theory of neural networks: The Hebb rule and beyond", *Heidelberg Colloquium on Glassy Dynamics*, Lecture Notes in Physics, vol. 275, Berlin, Heidelberg: Springer Berlin Heidelberg, pp. 485–527, [Bibcode](./Bibcode_(identifier)):[1987LNP...275..485S](https://ui.adsabs.harvard.edu/abs/1987LNP...275..485S), [doi](./Doi_(identifier)):[10.1007/bfb0057531](https://doi.org/10.1007%2Fbfb0057531), [ISBN](./ISBN_(identifier)) [978-3-540-17777-7](./Special:BookSources/978-3-540-17777-7)`{{citation}}`:  CS1 maint: work parameter with ISBN ([link](./Category:CS1_maint:_work_parameter_with_ISBN))
6. [↑](./Dropout_(neural_networks)#cite_ref-6) Canning, A; Gardner, E (1988-08-07). "Partially connected models of neural networks". *Journal of Physics A: Mathematical and General*. **21** (15): 3275–3284. [Bibcode](./Bibcode_(identifier)):[1988JPhA...21.3275C](https://ui.adsabs.harvard.edu/abs/1988JPhA...21.3275C). [doi](./Doi_(identifier)):[10.1088/0305-4470/21/15/016](https://doi.org/10.1088%2F0305-4470%2F21%2F15%2F016). [ISSN](./ISSN_(identifier)) [0305-4470](https://search.worldcat.org/issn/0305-4470).
7. [↑](./Dropout_(neural_networks)#cite_ref-pat_7-0) [US 9406017B2](https://patents.google.com/patent/US9406017B2/en), Hinton, Geoffrey E., "System and method for addressing overfitting in a neural network", published 2016-08-02, issued 2016-08-02