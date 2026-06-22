---
source: sources/wiki-Convolutional_neural_network.md
source_url: https://en.wikipedia.org/wiki/Convolutional_neural_network
chunk: 3/7
---

## Building blocks

A CNN architecture is formed by a stack of distinct layers that transform the input volume into an output volume (e.g. holding the class scores) through a differentiable function. A few distinct types of layers are commonly used. These are further discussed below.

[![](//upload.wikimedia.org/wikipedia/commons/thumb/6/68/Conv_layer.png/250px-Conv_layer.png)](./File:Conv_layer.png)Neurons of a convolutional layer (blue), connected to their receptive field (red) 

### Convolutional layer

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/b/bd/Convolutional_neural_network%2C_convolution_worked_example.png/250px-Convolutional_neural_network%2C_convolution_worked_example.png)](./File:Convolutional_neural_network,_convolution_worked_example.png)A worked example of performing a convolution. The convolution has stride 1, zero-padding, with kernel size 3-by-3. The convolution kernel is a [discrete Laplacian operator](./Discrete_Laplace_operator). 

The convolutional layer is the core building block of a CNN. The layer's parameters consist of a set of learnable filters (or [kernels](./Kernel_(image_processing))), which have a small receptive field, but extend through the full depth of the input volume. During the forward pass, each filter is [convolved](./Convolution) across the width and height of the input volume, computing the [dot product](./Dot_product) between the filter entries and the input, producing a 2-dimensional [activation map](./Activation_function) of that filter. As a result, the network learns filters that activate when it detects some specific type of [feature](./Feature_(machine_learning)) at some spatial position in the input.[[74]](./Convolutional_neural_network#cite_note-Géron_Hands-on_ML_2019-74)[[nb 1]](./Convolutional_neural_network#cite_note-75)

 

Stacking the activation maps for all filters along the depth dimension forms the full output volume of the convolution layer. Every entry in the output volume can thus also be interpreted as an output of a neuron that looks at a small region in the input. Each entry in an activation map use the same set of parameters that define the filter.

 

[Self-supervised learning](./Self-supervised_learning) has been adapted for use in convolutional layers by using sparse patches with a high-mask ratio and a global response normalization layer.[*[citation needed](./Wikipedia:Citation_needed)*]

 

#### Local connectivity

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/6/63/Typical_cnn.png/500px-Typical_cnn.png)](./File:Typical_cnn.png)Typical CNN architecture 

When dealing with high-dimensional inputs such as images, it is impractical to connect neurons to all neurons in the previous volume because such a network architecture does not take the spatial structure of the data into account. Convolutional networks exploit spatially local correlation by enforcing a [sparse local connectivity](./Sparse_network) pattern between neurons of adjacent layers: each neuron is connected to only a small region of the input volume.

 

The extent of this connectivity is a [hyperparameter](./Hyperparameter_optimization) called the [receptive field](./Receptive_field) of the neuron. The connections are [local in space](./Spatial_locality) (along width and height), but always extend along the entire depth of the input volume. Such an architecture ensures that the learned filters produce the strongest response to a spatially local input pattern.[[75]](./Convolutional_neural_network#cite_note-76)

 

#### Spatial arrangement

 

Three [hyperparameters](./Hyperparameter_(machine_learning)) control the size of the output volume of the convolutional layer: the depth, [stride](./Stride_of_an_array), and padding size:

 
- The *depth* of the output volume controls the number of neurons in a layer that connect to the same region of the input volume. These neurons learn to activate for different features in the input. For example, if the first convolutional layer takes the raw image as input, then different neurons along the depth dimension may activate in the presence of various oriented edges, or blobs of color.
- *Stride* controls how depth columns around the width and height are allocated. If the stride is 1, then we move the filters one pixel at a time. This leads to heavily [overlapping](./Intersection_(set_theory)) receptive fields between the columns, and to large output volumes. For any integer     S > 0 ,   {\textstyle S>0,}  ![{\textstyle S>0,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d1fb1c59de56b22cfdf94e6c2a03f4b0dfc7c4d2) a stride *S* means that the filter is translated *S* units at a time per output. In practice,     S ≥ ≥  3   {\textstyle S\geq 3}  ![{\textstyle S\geq 3}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1b1cc974b8af65e3a94aa730c0f360dd7059604d) is rare. A greater stride means smaller overlap of receptive fields and smaller spatial dimensions of the output volume.[[76]](./Convolutional_neural_network#cite_note-77)
- Sometimes, it is convenient to pad the input with zeros (or other values, such as the average of the region) on the border of the input volume. The size of this padding is a third hyperparameter. Padding provides control of the output volume's spatial size. In particular, sometimes it is desirable to exactly preserve the spatial size of the input volume, this is commonly referred to as "same" padding.

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/7f/Convolutional_neural_network%2C_boundary_conditions.png/330px-Convolutional_neural_network%2C_boundary_conditions.png)](./File:Convolutional_neural_network,_boundary_conditions.png)Three example padding conditions. Replication condition means that the pixel outside is padded with the closest pixel inside. The reflection padding is where the pixel outside is padded with the pixel inside, reflected across the boundary of the image. The circular padding is where the pixel outside wraps around to the other side of the image. 

The spatial size of the output volume is a function of the input volume size     W   {\displaystyle W}  ![{\displaystyle W}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54a9c4c547f4d6111f81946cad242b18298d70b7), the kernel field size     K   {\displaystyle K}  ![{\displaystyle K}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b76fce82a62ed5461908f0dc8f037de4e3686b0) of the convolutional layer neurons, the stride     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2), and the amount of zero padding     P   {\displaystyle P}  ![{\displaystyle P}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b4dc73bf40314945ff376bd363916a738548d40a) on the border. The number of neurons that "fit" in a given volume is then:

        W − −  K + 2 P  S   + 1.   {\displaystyle {\frac {W-K+2P}{S}}+1.}  ![{\displaystyle {\frac {W-K+2P}{S}}+1.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a5325dc0b1b8695f19ec8fe3485d0da19040c622) 

If this number is not an [integer](./Integer), then the strides are incorrect and the neurons cannot be tiled to fit across the input volume in a [symmetric](./Symmetry) way. In general, setting zero padding to be     P = ( K − −  1 )  /  2   {\textstyle P=(K-1)/2}  ![{\textstyle P=(K-1)/2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b1c80a44e8d2e568cb4adfc6f6c8bf554f210e6) when the stride is     S = 1   {\displaystyle S=1}  ![{\displaystyle S=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5e2b58c1aaaf2718fb801e97bf21d1f72726372) ensures that the input volume and output volume will have the same size spatially. However, it is not always completely necessary to use all of the neurons of the previous layer. For example, a neural network designer may decide to use just a portion of padding.

 

#### Parameter sharing

 

A parameter sharing scheme is used in convolutional layers to control the number of free parameters. It relies on the assumption that if a patch feature is useful to compute at some spatial position, then it should also be useful to compute at other positions. Denoting a single 2-dimensional slice of depth as a *depth slice*, the neurons in each depth slice are constrained to use the same weights and bias.

 

Since all neurons in a single depth slice share the same parameters, the forward pass in each depth slice of the convolutional layer can be computed as a [convolution](./Convolution) of the neuron's weights with the input volume.[[nb 2]](./Convolutional_neural_network#cite_note-78) Therefore, it is common to refer to the sets of weights as a filter (or a [kernel](./Kernel_(image_processing))), which is convolved with the input. The result of this convolution is an [activation map](./Activation_function), and the set of activation maps for each different filter are stacked together along the depth dimension to produce the output volume. Parameter sharing contributes to the [translation invariance](./Translational_symmetry) of the CNN architecture.[[16]](./Convolutional_neural_network#cite_note-:6-16)

 

Sometimes, the parameter sharing assumption may not make sense. This is especially the case when the input images to a CNN have some specific centered structure; for which we expect completely different features to be learned on different spatial locations. One practical example is when the inputs are faces that have been centered in the image: we might expect different eye-specific or hair-specific features to be learned in different parts of the image. In that case it is common to relax the parameter sharing scheme, and instead simply call the layer a "locally connected layer". In this layer, the convolutional kernels' parameters are not shared. Instead, the network learns independent weights and biases for each spatial location. This allows each location to have its own feature-learning ability, making it better suited to handle images with distinct central structures or irregular features.

 

### Pooling layer

 Main article: [Pooling layer](./Pooling_layer) [![](//upload.wikimedia.org/wikipedia/commons/thumb/b/bb/Convolutional_neural_network%2C_maxpooling.png/330px-Convolutional_neural_network%2C_maxpooling.png)](./File:Convolutional_neural_network,_maxpooling.png)Worked example of 2x2 maxpooling with stride 2 [![](//upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Max_pooling.png/330px-Max_pooling.png)](./File:Max_pooling.png)Max pooling with a 2x2 filter and stride = 2 

Another important concept of CNNs is pooling, which is used as a form of non-linear [down-sampling](./Downsampling_(signal_processing)). Pooling provides downsampling because it reduces the spatial dimensions (height and width) of the input feature maps while retaining the most important information. There are several non-linear functions to implement pooling, where *max pooling* and *average pooling* are the most common. Pooling aggregates information from small regions of the input creating [partitions](./Partition_of_a_set) of the input feature map, typically using a fixed-size window (like 2x2) and applying a stride (often 2) to move the window across the input.[[77]](./Convolutional_neural_network#cite_note-79) Note that without using a stride greater than 1, pooling would not perform downsampling, as it would simply move the pooling window across the input one step at a time, without reducing the size of the feature map. In other words, the stride is what actually causes the downsampling by determining how much the pooling window moves over the input.

 

Intuitively, the exact location of a feature is less important than its rough location relative to other features. This is the idea behind the use of pooling in convolutional neural networks. The pooling layer serves to progressively reduce the spatial size of the representation, to reduce the number of parameters, [memory footprint](./Memory_footprint) and amount of computation in the network, and hence to also control [overfitting](./Overfitting). This is known as down-sampling. It is common to periodically insert a pooling layer between successive convolutional layers (each one typically followed by an activation function, such as a [ReLU layer](./Convolutional_neural_network#ReLU_layer)) in a CNN architecture.[[74]](./Convolutional_neural_network#cite_note-Géron_Hands-on_ML_2019-74): 460–461  While pooling layers contribute to local translation invariance, they do not provide global translation invariance in a CNN, unless a form of global pooling is used.[[16]](./Convolutional_neural_network#cite_note-:6-16)[[73]](./Convolutional_neural_network#cite_note-:5-73) The pooling layer commonly operates independently on every depth, or slice, of the input and resizes it spatially. A very common form of max pooling is a layer with filters of size 2×2, applied with a stride of 2, which subsamples every depth slice in the input by 2 along both width and height, discarding 75% of the activations:     f  X , Y   ( S ) =  max  a , b = 0   1    S  2 X + a , 2 Y + b   .   {\displaystyle f_{X,Y}(S)=\max _{a,b=0}^{1}S_{2X+a,2Y+b}.}  ![{\displaystyle f_{X,Y}(S)=\max _{a,b=0}^{1}S_{2X+a,2Y+b}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb35d034c37054cf3920f0dc52236a636dd8f902)
In this case, every [max operation](./Maximum) is over 4 numbers. The depth dimension remains unchanged (this is true for other forms of pooling as well).

 

In addition to max pooling, pooling units can use other functions, such as [average](./Average) pooling or [ℓ2-norm](./Euclidean_norm) pooling. Average pooling was often used historically but has recently fallen out of favor compared to max pooling, which generally performs better in practice.[[78]](./Convolutional_neural_network#cite_note-Scherer-ICANN-2010-80)

 

Due to the effects of fast spatial reduction of the size of the representation,[*[which?](./Wikipedia:Avoid_weasel_words)*] there is a recent trend towards using smaller filters[[79]](./Convolutional_neural_network#cite_note-81) or discarding pooling layers altogether.[[80]](./Convolutional_neural_network#cite_note-82)

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/dc/RoI_pooling_animated.gif/500px-RoI_pooling_animated.gif)](./File:RoI_pooling_animated.gif)RoI pooling to size 2x2. In this example region proposal (an input parameter) has size 7x5. 

#### Channel max pooling

 

A channel max pooling (CMP) operation layer conducts the MP operation along the channel side among the corresponding positions of the consecutive feature maps for the purpose of redundant information elimination. The CMP makes the significant features gather together within fewer channels, which is important for fine-grained image classification that needs more discriminating features. Meanwhile, another advantage of the CMP operation is to make the channel number of feature maps smaller before it connects to the first fully connected (FC) layer. Similar to the MP operation, we denote the input feature maps and output feature maps of a CMP layer as F ∈ R(C×M×N) and C ∈ R(c×M×N), respectively, where C and c are the channel numbers of the input and output feature maps, M and N are the widths and the height of the feature maps, respectively. Note that the CMP operation only changes the channel number of the feature maps. The width and the height of the feature maps are not changed, which is different from the MP operation.[[81]](./Convolutional_neural_network#cite_note-Ma_Chang_Xie_Ding_2019_pp._3224–3233-83)

 

See [[82]](./Convolutional_neural_network#cite_note-84)[[83]](./Convolutional_neural_network#cite_note-85) for reviews for pooling methods.

 

### ReLU layer

 

ReLU is the abbreviation of [rectified linear unit](./Rectifier_(neural_networks)). It was proposed by [Alston Householder](./Alston_Scott_Householder) in 1941,[[84]](./Convolutional_neural_network#cite_note-86) and used in CNN by [Kunihiko Fukushima](./Kunihiko_Fukushima) in 1969.[[39]](./Convolutional_neural_network#cite_note-Fukushima1969-39) ReLU applies the non-saturating [activation function](./Activation_function)     f ( x ) = max ( 0 , x )   {\textstyle f(x)=\max(0,x)}  ![{\textstyle f(x)=\max(0,x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e2559111e4c3500df55d16f958f853e19e90804a).[[69]](./Convolutional_neural_network#cite_note-:02-69) It effectively removes negative values from an activation map by setting them to zero.[[85]](./Convolutional_neural_network#cite_note-Romanuke4-87) It introduces [nonlinearity](./Nonlinearity_(disambiguation)) to the [decision function](./Decision_boundary) and in the overall network without affecting the receptive fields of the convolution layers.
In 2011, Xavier Glorot, Antoine Bordes and [Yoshua Bengio](./Yoshua_Bengio) found that ReLU enables better training of deeper networks,[[86]](./Convolutional_neural_network#cite_note-glorot2011-88) compared to widely used activation functions prior to 2011.

 

Other functions can also be used to increase nonlinearity, for example the saturating [hyperbolic tangent](./Hyperbolic_tangent)     f ( x ) = tanh ⁡ ⁡  ( x )   {\displaystyle f(x)=\tanh(x)}  ![{\displaystyle f(x)=\tanh(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1a319ec32dbb0c625fa4802baf9252d1f00854e2),     f ( x ) =  |  tanh ⁡ ⁡  ( x )  |    {\displaystyle f(x)=|\tanh(x)|}  ![{\displaystyle f(x)=|\tanh(x)|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d1eb71e39ce9687851b7ec55bb8f54f42df2a828), and the [sigmoid function](./Sigmoid_function)     σ σ  ( x ) = ( 1 +  e  − −  x    )  − −  1     {\textstyle \sigma (x)=(1+e^{-x})^{-1}}  ![{\textstyle \sigma (x)=(1+e^{-x})^{-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3805da830a1a77523aefcdae0d2164d954849066). ReLU is often preferred to other functions because it trains the neural network several times faster without a significant penalty to [generalization](./Generalization_(learning)) accuracy.[[87]](./Convolutional_neural_network#cite_note-89)

 

### Fully connected layer

 

After several convolutional and max pooling layers, the final classification is done via fully connected layers. Neurons in a fully connected layer have connections to all activations in the previous layer, as seen in regular (non-convolutional) [artificial neural networks](./Artificial_neural_network). Their activations can thus be computed as an [affine transformation](./Affine_transformation), with [matrix multiplication](./Matrix_multiplication) followed by a bias offset ([vector addition](./Vector_addition) of a learned or fixed bias term).

 

### Loss layer

 Main articles: [Loss function](./Loss_function) and [Loss functions for classification](./Loss_functions_for_classification) 

The "loss layer", or "[loss function](./Loss_function)", exemplifies how [training](./Training) penalizes the deviation between the predicted output of the network, and the [true](./Ground_truth) data labels (during supervised learning). Various [loss functions](./Loss_function) can be used, depending on the specific task.

 

The [Softmax](./Softmax_function) loss function is used for predicting a single class of *K* mutually exclusive classes.[[nb 3]](./Convolutional_neural_network#cite_note-90) [Sigmoid](./Sigmoid_function) [cross-entropy](./Cross_entropy) loss is used for predicting *K* independent probability values in     [ 0 , 1 ]   {\displaystyle [0,1]}  ![{\displaystyle [0,1]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/738f7d23bb2d9642bab520020873cccbef49768d). [Euclidean](./Euclidean_distance) loss is used for [regressing](./Regression_(machine_learning)) to [real-valued](./Real_number) labels     ( − −  ∞ ∞  , ∞ ∞  )   {\displaystyle (-\infty ,\infty )}  ![{\displaystyle (-\infty ,\infty )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0c8c11c44279888c9e395eeb5f45d121348ae10a).

 

## Hyperparameters

 
|  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.(June 2017)(Learn how and when to remove this message) |
| --- | --- |

 

Hyperparameters are various settings that are used to control the learning process. CNNs use more [hyperparameters](./Hyperparameter_(machine_learning)) than a standard multilayer perceptron (MLP).

 

### Padding

 

Padding is the addition of (typically) 0-valued pixels on the borders of an image. This is done so that the border pixels are not undervalued (lost) from the output because they would ordinarily participate in only a single receptive field instance. The padding applied is typically one less than the corresponding kernel dimension. For example, a convolutional layer using 3x3 kernels would receive a 2-pixel pad, that is 1 pixel on each side of the image.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Stride

 

The stride is the number of pixels that the analysis window moves on each iteration. A stride of 2 means that each kernel is offset by 2 pixels from its predecessor.

 

### Number of filters

 

Since feature map size decreases with depth, layers near the input layer tend to have fewer filters while higher layers can have more. To equalize computation at each layer, the product of feature values *va* with pixel position is kept roughly constant across layers. Preserving more information about the input would require keeping the total number of activations (number of feature maps times number of pixel positions) non-decreasing from one layer to the next.

 

The number of feature maps directly controls the capacity and depends on the number of available examples and task complexity.

 

### Filter (or kernel) size

 

Common filter sizes found in the literature vary greatly, and are usually chosen based on the data set. Typical filter sizes range from 1x1 to 7x7. As two famous examples, [AlexNet](./AlexNet) used 3x3, 5x5, and 11x11. [Inceptionv3](./Inceptionv3) used 1x1, 3x3, and 5x5.

 

The challenge is to find the right level of granularity so as to create abstractions at the proper scale, given a particular data set, and without [overfitting](./Overfitting).

 

### Pooling type and size

 

[Max pooling](./Max_pooling) is typically used, often with a 2x2 dimension. This implies that the input is drastically [downsampled](./Downsampling_(signal_processing)), reducing processing cost.

 

Greater pooling [reduces the dimension](./Dimensionality_reduction) of the signal, and may result in unacceptable [information loss](./Data_loss). Often, non-overlapping pooling windows perform best.[[78]](./Convolutional_neural_network#cite_note-Scherer-ICANN-2010-80)

 

### Dilation

 

Dilation involves ignoring pixels within a kernel. This reduces processing memory potentially without significant signal loss. A dilation of 2 on a 3x3 kernel expands the kernel to 5x5, while still processing 9 (evenly spaced) pixels. Specifically, the processed pixels after the dilation are the cells (1,1), (1,3), (1,5), (3,1), (3,3), (3,5), (5,1), (5,3), (5,5), where (i,j) denotes the cell of the i-th row and j-th column in the expanded 5x5 kernel. Accordingly, dilation of 4 expands the kernel to 7x7.[*[citation needed](./Wikipedia:Citation_needed)*]

 

## Translation equivariance and aliasing

 

It is commonly assumed that CNNs are invariant to shifts of the input. Convolution or pooling layers within a CNN that do not have a stride greater than one are indeed [equivariant](./Equivariant_map) to translations of the input.[[73]](./Convolutional_neural_network#cite_note-:5-73) However, layers with a stride greater than one ignore the [Nyquist–Shannon sampling theorem](./Nyquist–Shannon_sampling_theorem) and might lead to [aliasing](./Aliasing) of the input signal[[73]](./Convolutional_neural_network#cite_note-:5-73) While, in principle, CNNs are capable of implementing anti-aliasing filters, it has been observed that this does not happen in practice,[[88]](./Convolutional_neural_network#cite_note-91) and therefore yield models that are not equivariant to translations.

 

Furthermore, if a CNN makes use of fully connected layers, translation equivariance does not imply translation invariance, as the fully connected layers are not invariant to shifts of the input.[[89]](./Convolutional_neural_network#cite_note-92)[[16]](./Convolutional_neural_network#cite_note-:6-16) One solution for complete translation invariance is avoiding any down-sampling throughout the network and applying global average pooling at the last layer.[[73]](./Convolutional_neural_network#cite_note-:5-73) Additionally, several other partial solutions have been proposed, such as [anti-aliasing](./Anti-aliasing_filter) before downsampling operations,[[90]](./Convolutional_neural_network#cite_note-93) spatial transformer networks,[[91]](./Convolutional_neural_network#cite_note-94) [data augmentation](./Data_augmentation), subsampling combined with pooling,[[16]](./Convolutional_neural_network#cite_note-:6-16) and [capsule neural networks](./Capsule_neural_network).[[92]](./Convolutional_neural_network#cite_note-95)

 

## Evaluation

 

The accuracy of the final model is typically estimated on a sub-part of the dataset set apart at the start, often called a test set. Alternatively, methods such as [*k*-fold cross-validation](./Cross-validation_(statistics)) are applied. Other strategies include using [conformal prediction](./Conformal_prediction).[[93]](./Convolutional_neural_network#cite_note-96)[[94]](./Convolutional_neural_network#cite_note-97)

 


