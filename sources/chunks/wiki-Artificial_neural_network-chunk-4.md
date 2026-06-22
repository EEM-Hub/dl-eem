---
source: sources/wiki-Artificial_neural_network.md
source_url: https://en.wikipedia.org/wiki/Artificial_neural_network
chunk: 4/7
---

## Theoretical properties

 

### Computational power

 

The [multilayer perceptron](./Multilayer_perceptron) is a [universal function](./UTM_theorem) approximator, as proven by the [universal approximation theorem](./Universal_approximation_theorem). However, the proof does not specify the number of neurons required, the network topology, the weights or the learning parameters.

 

A recurrent architecture with [rational](./Rational_number)-valued weights (as opposed to full precision real number-valued weights) has the power of a [universal Turing machine](./Universal_Turing_machine),[[177]](./Neural_network_(machine_learning)#cite_note-177) using a finite number of neurons and linear connections. Further, the use of [irrational](./Irrational_number) values for weights results in a machine with [super-Turing](./Hypercomputation) power.[[178]](./Neural_network_(machine_learning)#cite_note-178)[[179]](./Neural_network_(machine_learning)#cite_note-179)[*[failed verification](./Wikipedia:Verifiability)*]

 

### Capacity

 

A model's "capacity" property is its ability to model any given function. It is related to the amount of information that can be stored in the network and to the notion of complexity. Information capacity and the [VC dimension](./VC_dimension) are two metrics. The capacity of a network of standard neurons (not convolutional) can be derived by four rules[[180]](./Neural_network_(machine_learning)#cite_note-180) that derive from considering a neuron as an electrical element. 

 

The information capacity captures the functions that the network can model given any data as input. The VC dimension uses the principles of [measure theory](./Measure_theory) and finds the maximum capacity under optimal circumstances, given input data in a specific form. The VC Dimension for arbitrary inputs is half the information capacity of a perceptron. The VC Dimension for arbitrary points is sometimes referred to as Memory Capacity.[[181]](./Neural_network_(machine_learning)#cite_note-181)[[182]](./Neural_network_(machine_learning)#cite_note-auto2-182)

 

### Convergence

 

Models may not consistently converge on a single solution, because the system may get stuck in a local minima. Alternatively, the optimization method used might not guarantee to converge should it begin far from any local minima. Thirdly, for sufficiently large data or parameters, some methods are  impractically slow/expensive. Training may also cross some [saddle point](./Saddle_point) that may then prevent access to the solution.

 

When the width of a network approaches infinity, it is well described by its first order [Taylor expansion](./Taylor_expansion) throughout training, and so inherits the [convergence](./Convergent_series) behavior of [affine models](./Linear_model).[[183]](./Neural_network_(machine_learning)#cite_note-183)[[184]](./Neural_network_(machine_learning)#cite_note-184) When parameter numbers are small, NNs often fit target functions from low to high frequencies. This behavior is referred to as spectral bias, or the frequency principle.[[185]](./Neural_network_(machine_learning)#cite_note-185)[[186]](./Neural_network_(machine_learning)#cite_note-186)[[187]](./Neural_network_(machine_learning)#cite_note-187) This phenomenon is the opposite of the behavior of some well-studied iterative numerical schemes such as the [Jacobi method](./Jacobi_method). Deeper neural networks are more biased towards low frequency functions.[[188]](./Neural_network_(machine_learning)#cite_note-188)

 

### Generalization and statistics

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(May 2026)(Learn how and when to remove this message) |
| --- | --- |

 

Applications that must generalize well to unseen examples, must avoid [over-training](./Overfitting). This arises in convoluted or over-specified systems when the network capacity is much larger than needed.

 

Two approaches address over-training. [Cross-validation](./Cross-validation_(statistics)) and similar techniques can check for over-training and select appropriate hyperparameters to minimize generalization error. *[Regularization](./Regularization_(mathematics))* in a probabilistic (Bayesian) framework can be performed by selecting a larger prior probability over simpler models; but also in statistical learning theory, where the goal is to minimize two quantities: the 'empirical risk' and the 'structural risk', which roughly corresponds to the error over the training set and the predicted error in unseen data due to overfitting.

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/2/22/Synapse_deployment.jpg/250px-Synapse_deployment.jpg)](./File:Synapse_deployment.jpg)Confidence analysis of a neural network 

Supervised neural networks that use a [mean squared error](./Mean_squared_error) (MSE) cost function can use formal statistical methods to determine the confidence of the trained model. The MSE on a validation set can be used as an estimate for variance. This value can then be used to calculate the [confidence interval](./Confidence_interval) of network output, assuming a [normal distribution](./Normal_distribution). A confidence analysis made this way is statistically valid as long as the output [probability distribution](./Probability_distribution) stays the same and the network is not modified.

 

By adopting a [softmax activation function](./Softmax_activation_function), a generalization of the [logistic function](./Logistic_function), on the output layer of the neural network (or a softmax component in a component-based network) for categorical target variables, the outputs can be interpreted as posterior probabilities. This is useful in classification as it gives a certainty measure.

 

The softmax activation function is:

      y  i   =    e   x  i       ∑ ∑   j = 1   c    e   x  j          {\displaystyle y_{i}={\frac {e^{x_{i}}}{\sum _{j=1}^{c}e^{x_{j}}}}}  ![{\displaystyle y_{i}={\frac {e^{x_{i}}}{\sum _{j=1}^{c}e^{x_{j}}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/481884e3588b192020e8d0aafe16b41c0ed26007) 

## Applications

 

Neural networks support a broad range of applications in image processing, speech recognition, natural language processing, finance, and medicine.[*[citation needed](./Wikipedia:Citation_needed)*]
Because of their ability to model and reproduce nonlinear processes, neural networks have found applications in many disciplines. These include:

 
- [Function approximation](./Function_approximation),[[189]](./Neural_network_(machine_learning)#cite_note-189) or [regression analysis](./Regression_analysis),[[190]](./Neural_network_(machine_learning)#cite_note-190) (including [time series prediction](./Time_series#Prediction_and_forecasting), [fitness approximation](./Fitness_approximation),[[191]](./Neural_network_(machine_learning)#cite_note-191) and modeling)
- [Data processing](./Data_processing)[[192]](./Neural_network_(machine_learning)#cite_note-192) (including filtering, clustering, [blind source separation](./Blind_source_separation),[[193]](./Neural_network_(machine_learning)#cite_note-193) and compression)
- [Nonlinear system identification](./Nonlinear_system_identification)[[93]](./Neural_network_(machine_learning)#cite_note-SAB12-93) and control (including vehicle control, trajectory prediction,[[194]](./Neural_network_(machine_learning)#cite_note-194) [adaptive control](./Adaptive_control), [process control](./Process_control), and [natural resource management](./Natural_resource_management))
- [Pattern recognition](./Pattern_recognition) (including radar systems, [face identification](./Facial_recognition_system), signal classification,[[195]](./Neural_network_(machine_learning)#cite_note-195) [novelty detection](./Novelty_detection), [3D reconstruction](./3D_reconstruction),[[196]](./Neural_network_(machine_learning)#cite_note-196) object recognition, and sequential decision making[[197]](./Neural_network_(machine_learning)#cite_note-TurekNeuralNet2-197))
- Sequence recognition (including [gesture](./Gesture_recognition), [speech](./Speech_recognition), and handwritten and printed text recognition[[198]](./Neural_network_(machine_learning)#cite_note-198))
- Sensor data analysis[[199]](./Neural_network_(machine_learning)#cite_note-199) (including [image analysis](./Image_analysis))
- [Robotics](./Robotics) (including directing manipulators and [prostheses](./Prosthesis))
- [Data mining](./Data_mining) (including [knowledge discovery in databases](./Knowledge_discovery_in_databases))
- Finance[[200]](./Neural_network_(machine_learning)#cite_note-200) (such as [ex-ante](./Ex-ante) models for specific financial long-run forecasts and [artificial financial markets](./Artificial_financial_market))
- [Quantum chemistry](./Quantum_chemistry)[[201]](./Neural_network_(machine_learning)#cite_note-Balabin_20092-201)
- [General game playing](./General_game_playing)[[202]](./Neural_network_(machine_learning)#cite_note-202)
- [Generative AI](./Generative_AI)[[203]](./Neural_network_(machine_learning)#cite_note-203)
- [Data visualization](./Data_visualization)
- [Machine translation](./Machine_translation)
- Social network filtering[[204]](./Neural_network_(machine_learning)#cite_note-204)
- [E-mail spam](./E-mail_spam) filtering
- [Medical diagnosis](./Medical_diagnosis)[[205]](./Neural_network_(machine_learning)#cite_note-Ciaramella2-205)
- [Disaster response](./Disaster_response)[[206]](./Neural_network_(machine_learning)#cite_note-206)

 

NNs have been used to diagnose cancers[[207]](./Neural_network_(machine_learning)#cite_note-207)[[208]](./Neural_network_(machine_learning)#cite_note-208) and to distinguish highly invasive cancer cell lines from less invasive lines using only cell shape data.[[209]](./Neural_network_(machine_learning)#cite_note-209)[[210]](./Neural_network_(machine_learning)#cite_note-210)

 

NNs have been used to accelerate reliability analysis of infrastructures subject to natural disasters[[211]](./Neural_network_(machine_learning)#cite_note-211)[[212]](./Neural_network_(machine_learning)#cite_note-212) and to predict settling in building foundations.[[213]](./Neural_network_(machine_learning)#cite_note-213) They are used to mitigate flooding by modelling rainfall-runoff.[[214]](./Neural_network_(machine_learning)#cite_note-214) NNs have been used for building black-box models in [geoscience](./Geoscience): [hydrology](./Hydrology),[[215]](./Neural_network_(machine_learning)#cite_note-215)[[216]](./Neural_network_(machine_learning)#cite_note-216) ocean modelling and [coastal engineering](./Coastal_engineering),[[217]](./Neural_network_(machine_learning)#cite_note-217)[[218]](./Neural_network_(machine_learning)#cite_note-218) and [geomorphology](./Geomorphology).[[219]](./Neural_network_(machine_learning)#cite_note-219) NNs have been employed in [cybersecurity](./Computer_security), with the objective to discriminate between legitimate and malicious activities. For example, machine learning has been used for classifying [Android](./Android_(operating_system)) [malware](./Malware),[[220]](./Neural_network_(machine_learning)#cite_note-220) for identifying domains belonging to threat actors and for detecting URLs posing a security risk.[[221]](./Neural_network_(machine_learning)#cite_note-221) Research is underway on penetration testing, for detecting botnets,[[222]](./Neural_network_(machine_learning)#cite_note-222) credit cards frauds,[[223]](./Neural_network_(machine_learning)#cite_note-223) and network intrusions.

 

NNs have been proposed as a tool to solve [partial differential equations](./Partial_differential_equation) in physics[[224]](./Neural_network_(machine_learning)#cite_note-224)[[225]](./Neural_network_(machine_learning)#cite_note-225)[[226]](./Neural_network_(machine_learning)#cite_note-226) and simulate the properties of many-body [open quantum systems](./Open_quantum_system).[[227]](./Neural_network_(machine_learning)#cite_note-227)[[228]](./Neural_network_(machine_learning)#cite_note-228)[[229]](./Neural_network_(machine_learning)#cite_note-229) In brain research NNs have studied short-term behavior of [individual neurons](./Biological_neuron_models),[[230]](./Neural_network_(machine_learning)#cite_note-230) the dynamics of [neural circuitry](./Neural_circuit) arise from interactions between individual neurons and how behavior can arise from abstract neural modules that represent complete subsystems. Studies considered long-and short-term plasticity of neural systems and their relation to learning and memory from the individual neuron to the system level.

 

NNs show promise in profiling a user's interests from photos[[231]](./Neural_network_(machine_learning)#cite_note-231) and discovering new stable materials by efficiently predicting the total energy of crystals.[[232]](./Neural_network_(machine_learning)#cite_note-232)

 

### Image processing

 

NNs are employed in [computer vision](./Computer_vision) tasks such as image classification, object and facial recognition, and image segmentation. They have been applied to automated surveillance medical imaging for diagnosis.[[233]](./Neural_network_(machine_learning)#cite_note-:072-233)

 

### Speech recognition

 

NNs are used for speaker identification, speech-to-text, and text-to-speech conversion. NNs have conquered large vocabulary continuous [speech recognition](./Speech_recognition), outperforming traditional techniques.[[233]](./Neural_network_(machine_learning)#cite_note-:072-233)[[234]](./Neural_network_(machine_learning)#cite_note-:152-234) These advancements have enabled the development of more accurate and efficient voice-activated systems, enhancing user interfaces in technology products.[[235]](./Neural_network_(machine_learning)#cite_note-235)[[236]](./Neural_network_(machine_learning)#cite_note-236)

 

### Natural language processing

 

In [natural language processing](./Natural_language_processing), NNs are used for tasks such as [text classification](./Document_classification), [sentiment analysis](./Sentiment_analysis), [machine translation](./Machine_translation), to answer free-form questions, act as chatbots, and to summarize and analyze texts.[[233]](./Neural_network_(machine_learning)#cite_note-:072-233)[[234]](./Neural_network_(machine_learning)#cite_note-:152-234) This has implications for automated customer service, content moderation, and language understanding technologies.[[237]](./Neural_network_(machine_learning)#cite_note-237)[*[vague](./Wikipedia:Vagueness)*]

 

### Control systems

 

NNs are used to model dynamic systems for tasks such as system identification, control design, autonomous vehicles, and optimization.[[238]](./Neural_network_(machine_learning)#cite_note-238)[*[vague](./Wikipedia:Vagueness)*]

 

### Finance

 This section is an excerpt from [Applications of artificial intelligence § Trading and investment](./Applications_of_artificial_intelligence#Trading_and_investment).[[edit](https://en.wikipedia.org/w/index.php?title=Applications_of_artificial_intelligence&action=edit)] 

Large financial institutions use AI to assist with their investment practices.[[239]](./Neural_network_(machine_learning)#cite_note-239) [BlackRock](./BlackRock)'s AI engine, [Aladdin](./Aladdin_(BlackRock)), is used both within the company and by clients to help with investment decisions. Its functions include the use of [natural language processing](./Natural_language_processing) to analyze text such as news, broker reports, and social media feeds. It then gauges the sentiment on the companies mentioned and assigns a score. Banks such as [UBS](./UBS_tax_evasion_controversies) and [Deutsche Bank](./Deutsche_Bank) use SQREEM (Sequential Quantum Reduction and Extraction Model) to mine data to develop consumer profiles and match them with [wealth management](./Wealth_management) products.[[240]](./Neural_network_(machine_learning)#cite_note-240)

   

### Medicine

 

NNs analyze medical datasets. They enhance diagnostic accuracy, especially by interpreting complex [medical imaging](./Medical_imaging) for early disease detection, and by predicting patient outcomes for personalized treatment planning.[[234]](./Neural_network_(machine_learning)#cite_note-:152-234) In [drug discovery](./Drug_discovery), NNs speed up the identification of potential drug candidates and predict their efficacy and safety, significantly reducing development time and costs.[[233]](./Neural_network_(machine_learning)#cite_note-:072-233) Additionally, their application in [personalized medicine](./Personalized_medicine) and healthcare data analysis allows tailored therapies and efficient patient care management.[[234]](./Neural_network_(machine_learning)#cite_note-:152-234)

 

### Cybersecurity

 

Neural networks are widely applied in cybersecurity for anomaly detection, malware classification, and intrusion detection. By learning patterns of normal system or network behavior, NNs can identify deviations that indicate malicious activity.[[241]](./Neural_network_(machine_learning)#cite_note-241)

 

### Content creation

 

[Transformers](./Transformer_(machine_learning_model)) are used for [content creation](./Content_creation) across numerous industries.[[242]](./Neural_network_(machine_learning)#cite_note-:092-242) They can analyze samples and produce outputs that match the style of an artist or musician. For instance, [DALL-E](./DALL-E) trained on 650 million pairs of images and texts and can create artworks based on user text.[[243]](./Neural_network_(machine_learning)#cite_note-243) Companies such as [AIVA](./AIVA) and [Jukedeck](./Jukedeck) have used transformers to create original music.[[244]](./Neural_network_(machine_learning)#cite_note-244) NNs have been used to create personalized advertisements.[[242]](./Neural_network_(machine_learning)#cite_note-:092-242) Film production companies have used NNs to analyze the financial success of a film.[[245]](./Neural_network_(machine_learning)#cite_note-245) NNs have found uses in video game creation.[[246]](./Neural_network_(machine_learning)#cite_note-246)

 

## Issues

 

### Training

 

NNs require millions of training samples to become functional. As of 2026, training a commercial LLM (GPT, Grok, Gemini) typically required hundreds of thousands of computers, and cost 10s of millions of dollars.[[247]](./Neural_network_(machine_learning)#cite_note-247)[[167]](./Neural_network_(machine_learning)#cite_note-Qin12-167)

 

### Theory

 

A central claim[*[citation needed](./Wikipedia:Citation_needed)*] of NNs is that they embody new and powerful general principles for processing information. However, at root they use statistical long-developed methods. 

 

### Hardware

 

Neural networks require enormous computing resources for training.[[248]](./Neural_network_(machine_learning)#cite_note-:02-248) While the brain requires only 20 watts of power,[[249]](./Neural_network_(machine_learning)#cite_note-249) training commercial transformers requires (2026) data centers with hundreds of megawatts.[[250]](./Neural_network_(machine_learning)#cite_note-250)

 

From 1991 to 2015, computing power, especially as delivered by [GPGPUs](./General-purpose_computing_on_graphics_processing_units_(software)) (on [GPUs](./Graphics_processing_unit)), increased around a million-fold, enabling the use of the backpropagation algorithm.[[47]](./Neural_network_(machine_learning)#cite_note-SCHIDHUB42-47)

 

[Neuromorphic engineering](./Neuromorphic_engineering) or a [physical neural network](./Physical_neural_network) constructed non-von-Neumann chips to directly implement neural networks in circuitry. For example, [Alphabet](./Alphabet_Inc.) introduced custom chips ([Tensor Processing Unit](./Tensor_Processing_Unit)).[[251]](./Neural_network_(machine_learning)#cite_note-251)

 

### Concept drift

 

The statistical properties of input data may change over time, a phenomenon known as [concept drift](./Concept_drift) or [non-stationarity](./Stationary_process). Drift can reduce predictive accuracy and lead to unreliable or biased decisions if it is not detected and corrected. In practice, this means that the model's accuracy in deployment may differ substantially from levels observed during training.

 

Several strategies have been developed to monitor neural networks for drift and degradation:

 
- **Error-based monitoring**: comparing current predictions against ground-truth labels. This approach directly quantifies predictive performance but may be impractical when labels are delayed or impractical to obtain.
- **Data distribution monitoring**: detecting changes in the input data distribution using statistical tests, divergence measures, or density-ratio estimation.
- **Representation monitoring**: tracking the distribution of internal *embeddings* or hidden-layer features. Shifts in the latent representation can indicate nonstationarity even when labels are unavailable. Statistical methods such as *[statistical process control](./Statistical_process_control)* charts have been adapted for this purpose.[[252]](./Neural_network_(machine_learning)#cite_note-252)

 

### Dataset bias

 

Neural networks are dependent on the quality of their training data; low quality data can lead the model to product poor results.[[253]](./Neural_network_(machine_learning)#cite_note-:0102-253)[[254]](./Neural_network_(machine_learning)#cite_note-:172-254) Biased data produces biased results, requiring trainers to detect and correct them. For example, data that underrepresents some demographic groups may prevent cause errors, e.g., in [facial recognition](./Facial_recognition_system) and [law enforcement](./Law_enforcement).[[254]](./Neural_network_(machine_learning)#cite_note-:172-254)[[255]](./Neural_network_(machine_learning)#cite_note-:222-255) In 2018, [Amazon](./Amazon_(company)) scrapped a recruiting tool because the model favored men over women for jobs in software engineering due to the larger number of male workers in the field.[[255]](./Neural_network_(machine_learning)#cite_note-:222-255) The system penalized resumes with the word "woman" or the name of a women's college. One corrective is to add [synthetic data](./Synthetic_data) to offset the bias.[[256]](./Neural_network_(machine_learning)#cite_note-256)

 

### Lack of interpretability

 

NNs are "black box" systems that have complicated understanding of their decision-making processes. NNs are further vulnerable to adversarial examples ("poison"), that can cause incorrect predictions.

 

These concerns have led to increased research in [explainable artificial intelligence](./Explainable_artificial_intelligence) (XAI), robust machine learning, and hybrid AI approaches that combine neural learning with symbolic reasoning.[*[citation needed](./Wikipedia:Citation_needed)*]  Advocates of [hybrid](./Hybrid_neural_network) models also say that such a mixture can better capture the mechanisms of the human mind.[[257]](./Neural_network_(machine_learning)#cite_note-257)[[258]](./Neural_network_(machine_learning)#cite_note-258)

 

Progress has included local vs. non-local learning and shallow vs. deep architectures.[[259]](./Neural_network_(machine_learning)#cite_note-259)[*[clarification needed](./Wikipedia:Please_clarify)*]

 

Analyzing human thought (a biological neural network) has also proven difficult.

 

## Gallery

 
- [![A single-layer feedforward artificial neural network. Arrows originating from                                    x                        2                                     {\displaystyle x_{2}}     are omitted for clarity. There are p inputs to this network and q outputs. In this system, the value of the qth output,                                    y                        q                                     {\displaystyle y_{q}}    , is calculated as                                    y                        q                             =         K         ⋅                    (                                       ∑                                i                                         (                            x                                i                                                        w                                i                 q                                         )             −                            b                                q                                                  )                  .                 {\displaystyle y_{q}=K\cdot \left(\sum _{i}(x_{i}w_{iq})-b_{q}\right).}](//upload.wikimedia.org/wikipedia/commons/thumb/b/be/Single_layer_ann.svg/250px-Single_layer_ann.svg.png)](./File:Single_layer_ann.svg)A single-layer feedforward neural network. Arrows originating from      x  2     {\displaystyle x_{2}}  ![{\displaystyle x_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d7af1b928f06e4c7e3e8ebfd60704656719bd766) are omitted for clarity. There are *p* inputs to this network and *q* outputs. In this system, the value of the *q*th output,      y  q     {\displaystyle y_{q}}  ![{\displaystyle y_{q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/62e77051e3953cdf3818c7c8458d4f515eb5f79c), is calculated as      y  q   = K ⋅ ⋅   (   ∑ ∑   i   (  x  i    w  i q   ) − −   b  q    )  .   {\displaystyle y_{q}=K\cdot \left(\sum _{i}(x_{i}w_{iq})-b_{q}\right).}  ![{\displaystyle y_{q}=K\cdot \left(\sum _{i}(x_{i}w_{iq})-b_{q}\right).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dab100682f6d20bf79661b3423684c5e2cdd18dc)
- [![A two-layer feedforward neural network](//upload.wikimedia.org/wikipedia/commons/thumb/7/7f/Two_layer_ann.svg/120px-Two_layer_ann.svg.png)](./File:Two_layer_ann.svg)A two-layer feedforward neural network
- [![An neural network](//upload.wikimedia.org/wikipedia/commons/thumb/e/e4/Artificial_neural_network.svg/250px-Artificial_neural_network.svg.png)](./File:Artificial_neural_network.svg)An neural network
- [![An NN dependency graph](//upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Ann_dependency_%28graph%29.svg/250px-Ann_dependency_%28graph%29.svg.png)](./File:Ann_dependency_(graph).svg)An NN dependency graph
- [![A single-layer feedforward neural network with 4 inputs, 6 hidden nodes and 2 outputs. Given position state and direction, it outputs wheel based control values.](//upload.wikimedia.org/wikipedia/commons/thumb/3/32/Single-layer_feedforward_artificial_neural_network.png/250px-Single-layer_feedforward_artificial_neural_network.png)](./File:Single-layer_feedforward_artificial_neural_network.png)A single-layer feedforward neural network with 4 inputs, 6 hidden nodes and 2 outputs. Given position state and direction, it outputs wheel based control values.
- [![A two-layer feedforward neural network with 8 inputs, 2x8 hidden nodes and 2 outputs. Given position state, direction and other environment values, it outputs thruster based control values.](//upload.wikimedia.org/wikipedia/commons/thumb/5/58/Two-layer_feedforward_artificial_neural_network.png/250px-Two-layer_feedforward_artificial_neural_network.png)](./File:Two-layer_feedforward_artificial_neural_network.png)A two-layer feedforward neural network with 8 inputs, 2x8 hidden nodes and 2 outputs. Given position state, direction and other environment values, it outputs thruster based control values.
- [![Parallel pipeline structure of CMAC neural network. This learning algorithm can converge in one step.](//upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Cmac.jpg/250px-Cmac.jpg)](./File:Cmac.jpg)Parallel pipeline structure of CMAC neural network. This learning algorithm can converge in one step.

 

## See also

  
- [ADALINE](./ADALINE)
- [Autoencoder](./Autoencoder)
- [Bio-inspired computing](./Bio-inspired_computing)
- [Blue Brain Project](./Blue_Brain_Project)
- [Catastrophic interference](./Catastrophic_interference)
- [Cognitive architecture](./Cognitive_architecture)
- [Connectionist expert system](./Connectionist_expert_system)
- [Connectomics](./Connectomics)
- [Deep image prior](./Deep_image_prior)
- [Digital morphogenesis](./Digital_morphogenesis)
- [Efficiently updatable neural network](./Efficiently_updatable_neural_network)
- [Evolutionary algorithm](./Evolutionary_algorithm)
- [Family of curves](./Family_of_curves)
- [Genetic algorithm](./Genetic_algorithm)
- [Hyperdimensional computing](./Hyperdimensional_computing)
- [In situ adaptive tabulation](./In_situ_adaptive_tabulation)
- [Large width limits of neural networks](./Large_width_limits_of_neural_networks)
- [List of machine learning concepts](./List_of_machine_learning_concepts)
- [Memristor](./Memristor)
- [Mind uploading](./Mind_uploading)
- [Neural gas](./Neural_gas)
- [Neural network software](./Neural_network_software)
- [Optical neural network](./Optical_neural_network)
- [Parallel distributed processing](./Parallel_distributed_processing)
- [Philosophy of artificial intelligence](./Philosophy_of_artificial_intelligence)
- [Predictive analytics](./Predictive_analytics)
- [Quantum neural network](./Quantum_neural_network)
- [Support vector machine](./Support_vector_machine)
- [Spiking neural network](./Spiking_neural_network)
- [Stochastic parrot](./Stochastic_parrot)
- [Tensor product network](./Tensor_product_network)
- [Topological deep learning](./Topological_deep_learning)

  

## Notes

 

 


