---
source: sources/wiki-Long_short-term_memory.md
source_url: https://en.wikipedia.org/wiki/Long_short-term_memory
chunk: 2/4
---

## Applications

 

Applications of LSTM include:

  
- [Robot control](./Robot_control)[[13]](./Long_short-term_memory#cite_note-mayer2006-13)
- [Time series prediction](./Time_series_prediction)[[7]](./Long_short-term_memory#cite_note-wierstra2005-7)
- [Speech recognition](./Speech_recognition)[[26]](./Long_short-term_memory#cite_note-graves2005-26)[[27]](./Long_short-term_memory#cite_note-fernandez2007icann-27)[[28]](./Long_short-term_memory#cite_note-graves2013-28)
- Rhythm learning[[22]](./Long_short-term_memory#cite_note-peephole2002-22)
- Hydrological rainfall–runoff modeling[[29]](./Long_short-term_memory#cite_note-29)
- Music composition[[30]](./Long_short-term_memory#cite_note-eck2002-30)
- [Energy forecasting](./Energy_forecasting)[[18]](./Long_short-term_memory#cite_note-AMVT-18)
- Grammar learning[[31]](./Long_short-term_memory#cite_note-gers2002-31)[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[32]](./Long_short-term_memory#cite_note-perez2003-32)
- [Handwriting recognition](./Handwriting_recognition)[[33]](./Long_short-term_memory#cite_note-graves2009nips-33)[[34]](./Long_short-term_memory#cite_note-34)
- Human action recognition[[35]](./Long_short-term_memory#cite_note-baccouche2011-35)
- [Sign language translation](./Sign_language)[[36]](./Long_short-term_memory#cite_note-huang2018-36)
- Protein homology detection[[37]](./Long_short-term_memory#cite_note-hochreiter2007-37)
- Predicting subcellular localization of proteins[[38]](./Long_short-term_memory#cite_note-thireou2007-38)
- Time series [anomaly detection](./Anomaly_detection)[[39]](./Long_short-term_memory#cite_note-malhotra2015-39)
- Several prediction tasks in the area of [business process management](./Business_process_management)[[40]](./Long_short-term_memory#cite_note-tax2017-40)
- Prediction in medical care pathways[[41]](./Long_short-term_memory#cite_note-choi2016-41)
- [Semantic parsing](./Semantic_parsing)[[42]](./Long_short-term_memory#cite_note-jia2016-42)
- [Object co-segmentation](./Object_co-segmentation)[[43]](./Long_short-term_memory#cite_note-Wang_Duan_Zhang_Niu_p=1657-43)[[44]](./Long_short-term_memory#cite_note-Duan_Wang_Zhai_Zheng_2018_p.-44)
- Airport passenger management[[45]](./Long_short-term_memory#cite_note-orsini2019-45)
- Short-term [traffic forecast](./Traffic_forecast)[[46]](./Long_short-term_memory#cite_note-liu2017-46)
- [Drug design](./Drug_design)[[47]](./Long_short-term_memory#cite_note-pmid29095571-47)
- [Financial forecasting](./Financial_forecasting)[[48]](./Long_short-term_memory#cite_note-saiful2020-48)
- Activity classification in video[[49]](./Long_short-term_memory#cite_note-49)

 

**2015:** Google started using an LSTM trained by CTC for speech recognition on [Google Voice](./Google_Voice).[[50]](./Long_short-term_memory#cite_note-Beau15-50)[[51]](./Long_short-term_memory#cite_note-GoogleVoiceSearch-51) According to the official blog post, the new model cut transcription errors by 49%.[[52]](./Long_short-term_memory#cite_note-googleblog2015-52)

 

**2016:** Google started using an LSTM to suggest messages in the Allo conversation app.[[53]](./Long_short-term_memory#cite_note-GoogleAllo-53) In the same year, Google released the [Google Neural Machine Translation](./Google_Neural_Machine_Translation) system for Google Translate which used LSTMs to reduce translation errors by 60%.[[10]](./Long_short-term_memory#cite_note-GoogleTranslate-10)[[54]](./Long_short-term_memory#cite_note-WiredGoogleTranslate-54)[[55]](./Long_short-term_memory#cite_note-googleblog2016-55)

 

Apple announced in its [Worldwide Developers Conference](./Worldwide_Developers_Conference) that it would start using the LSTM for quicktype[[56]](./Long_short-term_memory#cite_note-AppleQuicktype-56)[[57]](./Long_short-term_memory#cite_note-AppleQuicktype2-57)[[58]](./Long_short-term_memory#cite_note-58) in the iPhone and for Siri.[[59]](./Long_short-term_memory#cite_note-AppleSiri-59)[[60]](./Long_short-term_memory#cite_note-capes2017-60)

 

Amazon released [Polly](./Amazon_Polly), which generates the voices behind Alexa, using a bidirectional LSTM for the text-to-speech technology.[[61]](./Long_short-term_memory#cite_note-AmazonAlexa-61)

 

**2017:**  Facebook performed some 4.5 billion automatic translations every day using long short-term memory networks.[[11]](./Long_short-term_memory#cite_note-FacebookTranslate-11)

 

Microsoft reported reaching 94.9% recognition accuracy on the [Switchboard corpus](./Switchboard_corpus?action=edit&redlink=1), incorporating a vocabulary of 165,000 words. The approach used "dialog session-based long-short-term memory".[[62]](./Long_short-term_memory#cite_note-62)

 

**2018:** [OpenAI](./OpenAI) used LSTM trained by policy gradients to beat humans in the complex video game of Dota 2,[[15]](./Long_short-term_memory#cite_note-OpenAIfive-15) and to control a human-like robot hand that manipulates physical objects with unprecedented dexterity.[[14]](./Long_short-term_memory#cite_note-OpenAIhand-14)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2019:** [DeepMind](./DeepMind) used LSTM trained by policy gradients to excel at the complex video game of [Starcraft II](./Starcraft_II).[[16]](./Long_short-term_memory#cite_note-alphastar-16)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

## History

 

### Development

 

Aspects of LSTM were anticipated by "focused back-propagation",[[64]](./Long_short-term_memory#cite_note-mozer1989-64) cited by the LSTM paper.[[1]](./Long_short-term_memory#cite_note-lstm1997-1)

 

Sepp Hochreiter's 1991 German diploma thesis analyzed the [vanishing gradient problem](./Vanishing_gradient_problem) and developed principles of the method.[[2]](./Long_short-term_memory#cite_note-hochreiter1991-2) His supervisor, [Jürgen Schmidhuber](./Jürgen_Schmidhuber), considered the thesis highly significant.[[65]](./Long_short-term_memory#cite_note-DLhistory-65)

 

An early version of LSTM was published in 1995 in a technical report by [Sepp Hochreiter](./Sepp_Hochreiter) and [Jürgen Schmidhuber](./Jürgen_Schmidhuber),[[66]](./Long_short-term_memory#cite_note-66) then published in the [NIPS](./Conference_on_Neural_Information_Processing_Systems) 1996 conference.[[3]](./Long_short-term_memory#cite_note-hochreiter1996-3)

 

The most commonly used reference point for LSTM was published in 1997 in the journal [Neural Computation](./Neural_Computation_(journal)).[[1]](./Long_short-term_memory#cite_note-lstm1997-1) By introducing Constant Error Carousel (CEC) units, LSTM deals with the [vanishing gradient problem](./Vanishing_gradient_problem). The initial version of LSTM block included cells, input and output gates.[[67]](./Long_short-term_memory#cite_note-ASearchSpaceOdyssey-67)

 

[Felix Gers](./Felix_Gers), Jürgen Schmidhuber, and Fred Cummins introduced the forget gate (also called "keep gate") into the LSTM architecture in 1999,[[68]](./Long_short-term_memory#cite_note-lstm1999-68) enabling the LSTM to reset its own state.[[67]](./Long_short-term_memory#cite_note-ASearchSpaceOdyssey-67) This is the most commonly used version of LSTM nowadays. They added peephole connections in 2000.[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[22]](./Long_short-term_memory#cite_note-peephole2002-22) Additionally, the output activation function was omitted.[[67]](./Long_short-term_memory#cite_note-ASearchSpaceOdyssey-67)

 

### Development of variants

 

In 2005 Graves and Schmidhuber[[26]](./Long_short-term_memory#cite_note-graves2005-26) published LSTM with full [backpropagation through time](./Backpropagation_through_time) and bidirectional LSTM.

 

In 2006 Graves, Fernandez, Gomez, and Schmidhuber[[5]](./Long_short-term_memory#cite_note-graves2006-5) introduced a new error function for LSTM: [Connectionist Temporal Classification](./Connectionist_Temporal_Classification) (CTC) for simultaneous alignment and recognition of sequences.

 

In 2014 Kyunghyun Cho an others[[69]](./Long_short-term_memory#cite_note-cho2014-69) published a simplified variant of the forget gate LSTM[[68]](./Long_short-term_memory#cite_note-lstm1999-68) called [Gated recurrent unit](./Gated_recurrent_unit) (GRU).

 

In 2015 Srivastava, Greff, and Schmidhuber used LSTM principles[[68]](./Long_short-term_memory#cite_note-lstm1999-68) to create the [Highway network](./Highway_network), a [feedforward neural network](./Feedforward_neural_network) with hundreds of layers, much deeper than previous networks.[[70]](./Long_short-term_memory#cite_note-highway2015-70)[[71]](./Long_short-term_memory#cite_note-highway2015neurips-71)[[72]](./Long_short-term_memory#cite_note-mostcited2021-72) Concurrently, the [ResNet](./Residual_neural_network) architecture was developed. It is equivalent to an open-gated or gateless highway network.[[73]](./Long_short-term_memory#cite_note-resnet2015-73)

 

A modern upgrade of LSTM called [xLSTM](./XLSTM?action=edit&redlink=1) is published by a team led by [Sepp Hochreiter](./Sepp_Hochreiter).[[74]](./Long_short-term_memory#cite_note-74)[[75]](./Long_short-term_memory#cite_note-75) One of the 2 blocks (mLSTM) of the architecture are parallelizable like the [Transformer](./Transformer_(deep_learning_architecture)) architecture, the other ones (sLSTM) allow state tracking.

 

### Applications

 

**2001:** Gers and Schmidhuber trained LSTM to learn languages unlearnable by traditional models such as Hidden Markov Models.[[21]](./Long_short-term_memory#cite_note-peepholeLSTM-21)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

Hochreiter et al. used LSTM for [meta-learning](./Meta-learning_(computer_science)) (i.e. learning a learning algorithm).[[76]](./Long_short-term_memory#cite_note-76)

 

**2004:** First successful application of LSTM to speech [Alex Graves](./Alex_Graves_(computer_scientist)) et al.[[77]](./Long_short-term_memory#cite_note-graves2004-77)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2005:** Daan Wierstra, Faustino Gomez, and Schmidhuber trained LSTM by [neuroevolution](./Neuroevolution) without a teacher.[[7]](./Long_short-term_memory#cite_note-wierstra2005-7)

 

Mayer et al. trained LSTM to control [robots](./Robot).[[13]](./Long_short-term_memory#cite_note-mayer2006-13)

 

**2007:** Wierstra, Foerster, Peters, and Schmidhuber trained LSTM by policy gradients for [reinforcement learning](./Reinforcement_learning) without a teacher.[[78]](./Long_short-term_memory#cite_note-wierstra2007-78)

 

Hochreiter, Heuesel, and Obermayr applied LSTM to protein homology detection the field of [biology](./Biology).[[37]](./Long_short-term_memory#cite_note-hochreiter2007-37)

 

**2009:** Justin Bayer et al. introduced [neural architecture search](./Neural_architecture_search) for LSTM.[[79]](./Long_short-term_memory#cite_note-bayer2009-79)[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2009:** An LSTM trained by CTC won the [ICDAR](./ICDAR) connected handwriting recognition competition. Three such models were submitted by a team led by [Alex Graves](./Alex_Graves_(computer_scientist)).[[80]](./Long_short-term_memory#cite_note-graves2009-80) One was the most accurate model in the competition and another was the fastest.[[81]](./Long_short-term_memory#cite_note-maergner2009-81) This was the first time an RNN won international competitions.[[63]](./Long_short-term_memory#cite_note-miraculous2021-63)

 

**2013:** Alex Graves, Abdel-rahman Mohamed, and Geoffrey Hinton used LSTM networks as a major component of a network that achieved a record 17.7% [phoneme](./Phoneme) error rate on the classic [TIMIT](./TIMIT) natural speech dataset.[[28]](./Long_short-term_memory#cite_note-graves2013-28)

 

**2017:** Researchers from [Michigan State University](./Michigan_State_University), [IBM Research](./IBM_Research), and [Cornell University](./Cornell_University) published a study in the Knowledge Discovery and Data Mining (KDD) conference.[[82]](./Long_short-term_memory#cite_note-82) Their [time-aware LSTM](./Time-aware_LSTM) (T-LSTM) performs better on certain data sets than standard LSTM.

 

**2020:** Kaplan and McCandlish et al. explored the [ scaling law](./Neural_scaling_law) of LSTM architecture in language modeling and compared it with [ Transformers](./Transformer_(deep_learning)), showing that Transformers scale better than LSTM on text data. [[83]](./Long_short-term_memory#cite_note-83)

 

## See also

  Please respect alphabetical order   
- [Attention (machine learning)](./Attention_(machine_learning))
- [Deep learning](./Deep_learning)
- [Differentiable neural computer](./Differentiable_neural_computer)
- [Gated recurrent unit](./Gated_recurrent_unit)
- [Highway network](./Highway_network)
- [Long-term potentiation](./Long-term_potentiation)
- [Prefrontal cortex basal ganglia working memory](./Prefrontal_cortex_basal_ganglia_working_memory)
- [Recurrent neural network](./Recurrent_neural_network)
- [Seq2seq](./Seq2seq)
- [Transformer (machine learning model)](./Transformer_(machine_learning_model))
- [Time series](./Time_series)

  


