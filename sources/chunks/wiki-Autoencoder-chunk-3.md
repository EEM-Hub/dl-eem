---
source: sources/wiki-Autoencoder.md
source_url: https://en.wikipedia.org/wiki/Autoencoder
chunk: 3/4
---

## Applications

 

The two main applications of autoencoders are [dimensionality reduction](./Dimensionality_reduction) and [information retrieval](./Information_retrieval) (or [associative memory](./Content-addressable_memory)),[[2]](./Autoencoder#cite_note-:0-2) but modern variations have been applied to other tasks.

 

### Dimensionality reduction

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/0/0b/PCA_vs_Linear_Autoencoder.png/250px-PCA_vs_Linear_Autoencoder.png)](./File:PCA_vs_Linear_Autoencoder.png)Plot of the first two Principal Components (left) and a two-dimension hidden layer of a Linear Autoencoder (Right) applied to the [Fashion MNIST](./Fashion_MNIST) dataset.[[37]](./Autoencoder#cite_note-:10-37) The two models being both linear learn to span the same subspace. The projection of the data points is indeed identical, apart from rotation of the subspace. While PCA selects a specific orientation up to reflections in the general case, the cost function of a simple autoencoder is invariant to rotations of the latent space.

[Dimensionality reduction](./Dimensionality_reduction) was one of the first [deep learning](./Deep_learning) applications.[[2]](./Autoencoder#cite_note-:0-2)

 

For Hinton's 2006 study,[[10]](./Autoencoder#cite_note-:7-10) he pretrained a multi-layer autoencoder with a stack of [RBMs](./Restricted_Boltzmann_machine) and then used their weights to initialize a deep autoencoder with gradually smaller hidden layers until hitting a bottleneck of 30 neurons. The resulting 30 dimensions of the code yielded a smaller reconstruction error compared to the first 30 components of a principal component analysis (PCA), and learned a representation that was qualitatively easier to interpret, clearly separating data clusters.[[2]](./Autoencoder#cite_note-:0-2)[[10]](./Autoencoder#cite_note-:7-10)

 

Reducing dimensions can improve performance on tasks such as classification.[[2]](./Autoencoder#cite_note-:0-2) Indeed, the hallmark of dimensionality reduction is to place semantically related examples near each other.[[38]](./Autoencoder#cite_note-:3-38)

 

#### Principal component analysis

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Reconstruction_autoencoders_vs_PCA.png/250px-Reconstruction_autoencoders_vs_PCA.png)](./File:Reconstruction_autoencoders_vs_PCA.png)Reconstruction of 28x28pixel images by an Autoencoder with a code size of two (two-units hidden layer) and the reconstruction from the first two Principal Components of PCA. Images come from the [Fashion MNIST dataset](./Fashion_MNIST).[[37]](./Autoencoder#cite_note-:10-37) 

If linear activations are used, or only a single sigmoid hidden layer, then the optimal solution to an autoencoder is strongly related to [principal component analysis](./Principal_component_analysis) (PCA).[[29]](./Autoencoder#cite_note-:14-29)[[39]](./Autoencoder#cite_note-39) The weights of an autoencoder with a single hidden layer of size     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) (where     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) is less than the size of the input) span the same vector subspace as the one spanned by the first     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) principal components, and the output of the autoencoder is an orthogonal projection onto this subspace. The autoencoder weights are not equal to the principal components, and are generally not orthogonal, yet the principal components may be recovered from them using the [singular value decomposition](./Singular_value_decomposition).[[40]](./Autoencoder#cite_note-40)

 

However, the potential of autoencoders resides in their non-linearity, allowing the model to learn more powerful generalizations compared to PCA, and to reconstruct the input with significantly lower information loss.[[10]](./Autoencoder#cite_note-:7-10)

 

### Information retrieval

 

[Information retrieval](./Information_retrieval) benefits particularly from [dimensionality reduction](./Dimensionality_reduction) in that search can become more efficient in certain kinds of low dimensional spaces. Autoencoders were indeed applied to semantic hashing, proposed by [Salakhutdinov](./Russ_Salakhutdinov) and Hinton in 2007.[[38]](./Autoencoder#cite_note-:3-38) By training the algorithm to produce a low-dimensional binary code, all database entries could be stored in a [hash table](./Hash_table) mapping binary code vectors to entries. This table would then support information retrieval by returning all entries with the same binary code as the query, or slightly less similar entries by flipping some bits from the query encoding.

 

### Anomaly detection

 

Another application for autoencoders is [anomaly detection](./Anomaly_detection).[[17]](./Autoencoder#cite_note-:13-17)[[41]](./Autoencoder#cite_note-41)[[42]](./Autoencoder#cite_note-42)[[43]](./Autoencoder#cite_note-:8-43)[[44]](./Autoencoder#cite_note-44)[[45]](./Autoencoder#cite_note-45) By learning to replicate the most salient features in the training data under some of the constraints described previously, the model is encouraged to learn to precisely reproduce the most frequently observed characteristics. When facing anomalies, the model should worsen its reconstruction performance. In most cases, only data with normal instances are used to train the autoencoder; in others, the frequency of anomalies is small compared to the observation set so that its contribution to the learned representation could be ignored. After training, the autoencoder will accurately reconstruct "normal" data, while failing to do so with unfamiliar anomalous data.[[43]](./Autoencoder#cite_note-:8-43) Reconstruction error (the error between the original data and its low dimensional reconstruction) is used as an anomaly score to detect anomalies.[[43]](./Autoencoder#cite_note-:8-43)
Typically, this means that on a validation set the empirical distribution of reconstruction errors is recorded and then (e.g.) the empirical 95-percentile      x  p     {\displaystyle x_{p}}  ![{\displaystyle x_{p}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0bec554743fa797409a83ad8d00b4d35e110a50a) is taken as threshold     t :=  x  p     {\displaystyle t:=x_{p}}  ![{\displaystyle t:=x_{p}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6481406e3bed47aebe2848512f5aca6f96085e01) to flag anomalous data points:      loss  ( x ,  reconstruction  ( x ) ) > t  ⟹ ⟹    anomaly    {\displaystyle {\text{loss}}(x,{\text{reconstruction}}(x))>t\implies {\text{anomaly}}}  ![{\displaystyle {\text{loss}}(x,{\text{reconstruction}}(x))>t\implies {\text{anomaly}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a98f4a4d744a1865ae543008661712e48c733326). Since the threshold is an empirical [quantile](./Quantile) estimate, there is an inherent difficulty with "correctly" setting this threshold:
In many cases the distribution of the empirical quantile is asymptotically a normal distribution      empirical p-quantile  ∼ ∼    N    (  μ μ  = p ,  σ σ   2   =    p ( 1 − −  p )   n f (  x  p    )  2       )  ,   {\displaystyle {\text{empirical p-quantile}}\sim {\mathcal {N}}\left(\mu =p,\sigma ^{2}={\frac {p(1-p)}{nf(x_{p})^{2}}}\right),}  ![{\displaystyle {\text{empirical p-quantile}}\sim {\mathcal {N}}\left(\mu =p,\sigma ^{2}={\frac {p(1-p)}{nf(x_{p})^{2}}}\right),}](https://wikimedia.org/api/rest_v1/media/math/render/svg/83a3e1b4f51e83c131a75f457755a72b8140ff62) with     f (  x  p   )   {\displaystyle f(x_{p})}  ![{\displaystyle f(x_{p})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed477b468284792eb8d054af3ebaffe8cae222ac) the probability density at the quantile. This means that the variance grows if an extreme quantile is considered (because     f (  x  p   )   {\displaystyle f(x_{p})}  ![{\displaystyle f(x_{p})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed477b468284792eb8d054af3ebaffe8cae222ac) is small there). This means that there is a, potentially, a big uncertainty in what is the right choice for the threshold since it is *estimated* from a validation set.

 

Recent literature has however shown that certain autoencoding models can, counterintuitively, be very good at reconstructing anomalous examples and consequently not able to reliably perform anomaly detection.[[46]](./Autoencoder#cite_note-46)[[47]](./Autoencoder#cite_note-47) 
Intuitively, this can be understood by considering those one layer auto encoders which are related to PCA - also in this case there can be perfect rein reconstructions for points which are far away from the data region but which lie on a principal component axis.

 

It is best to analyze if the anomalies which are flagged by the auto encoder are true anomalies. In this sense all the metrics in [Evaluation of binary classifiers](./Evaluation_of_binary_classifiers) can be considered. The fundamental challenge which comes with the unsupervised (self-supervised) learning setting is, that labels for rare events do not exist (in which case the labels first have to be gathered and the data set will be imbalanced) or anomaly indicating labels are very rare, introducing larger [confidence intervals](./Confidence_interval) for these performance estimates.

 

### Image processing

 

The characteristics of autoencoders are useful in image processing.

 

One example can be found in lossy [image compression](./Image_compression), where autoencoders outperformed other approaches and proved competitive against [JPEG 2000](./JPEG_2000).[[48]](./Autoencoder#cite_note-48)[[49]](./Autoencoder#cite_note-49)

 

Another useful application of autoencoders in image preprocessing is [image denoising](./Image_denoising).[[50]](./Autoencoder#cite_note-50)[[51]](./Autoencoder#cite_note-51)[[52]](./Autoencoder#cite_note-52)

 

Autoencoders found use in more demanding contexts such as [medical imaging](./Medical_imaging) where they have been used for [image denoising](./Image_denoising)[[53]](./Autoencoder#cite_note-53) as well as [super-resolution](./Super-resolution).[[54]](./Autoencoder#cite_note-54)[[55]](./Autoencoder#cite_note-55) In image-assisted diagnosis, experiments have applied autoencoders for [breast cancer](./Breast_cancer) detection[[56]](./Autoencoder#cite_note-56) and for modelling the relation between the cognitive decline of [Alzheimer's disease](./Alzheimer's_disease) and the latent features of an autoencoder trained with [MRI](./MRI).[[57]](./Autoencoder#cite_note-57)

 

### Drug discovery

 

In 2019 molecules generated with variational autoencoders were validated experimentally in mice.[[58]](./Autoencoder#cite_note-58)[[59]](./Autoencoder#cite_note-59)

 

### Popularity prediction

 

Recently, a stacked autoencoder framework produced promising results in predicting popularity of social media posts,[[60]](./Autoencoder#cite_note-60) which is helpful for online advertising strategies.

 

### Machine translation

 

Autoencoders have been applied to [machine translation](./Machine_translation), which is usually referred to as [neural machine translation](./Neural_machine_translation) (NMT).[[61]](./Autoencoder#cite_note-61)[[62]](./Autoencoder#cite_note-62) Unlike traditional autoencoders, the output does not match the input - it is in another language. In NMT, texts are treated as sequences to be encoded into the learning procedure, while on the decoder side sequences in the target language(s) are generated. [Language](./Language)-specific autoencoders incorporate further [linguistic](./Linguistic) features into the learning procedure, such as Chinese decomposition features.[[63]](./Autoencoder#cite_note-63) Machine translation is rarely still done with autoencoders, due to the availability of more effective [transformer](./Transformer_(machine_learning_model)) networks.

 

### Communication Systems

 

Autoencoders in communication systems are important because they help in encoding data into a more resilient representation for channel impairments, which is crucial for transmitting information while minimizing errors. In Addition, AE-based systems can optimize end-to-end communication performance. This approach can solve the several limitations of designing communication systems such as the inherent difficulty in accurately modeling the complex behavior of real-world channels.[[64]](./Autoencoder#cite_note-64)

 

## See also

 
- [Representation learning](./Representation_learning)
- [Singular value decomposition](./Singular_value_decomposition)
- [Sparse dictionary learning](./Sparse_dictionary_learning)
- [Deep learning](./Deep_learning)

 

## Further reading

 
- Bank, Dor; Koenigstein, Noam; Giryes, Raja (2023). "Autoencoders". *Machine Learning for Data Science Handbook*. Cham: Springer International Publishing. [doi](./Doi_(identifier)):[10.1007/978-3-031-24628-9_16](https://doi.org/10.1007%2F978-3-031-24628-9_16). [ISBN](./ISBN_(identifier)) [978-3-031-24627-2](./Special:BookSources/978-3-031-24627-2).
- Goodfellow, Ian; Bengio, Yoshua; Courville, Aaron (2016). ["14. Autoencoders"](https://www.deeplearningbook.org/contents/autoencoders.html). *Deep learning*. Adaptive computation and machine learning. Cambridge, Mass: The MIT press. [ISBN](./ISBN_(identifier)) [978-0-262-03561-3](./Special:BookSources/978-0-262-03561-3).

 


