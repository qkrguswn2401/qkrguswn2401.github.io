---
title: "Deep contexualized word representation,  ELMO"
date: 2021-02-17 08:26:28 -0400
categories: Paper Review
---
Embeddings from Language Models (ELMo)

Motivation: to deal with complex characteristics of word use (syntax and semantic), How these behaves different over linguistic context.  

How it is different:  Unlike previous word type embeddin where each token is assigned by entire input sequence, word embeddings are derived from bidrectional LSTM language model obejctive
on large text corpus.  LSTM states captures better context-depent aspects of word meaning.  
Elmo word representation are computed on top of 2 biLMs with character convolutions (CNN).  

1.  Bidirectional Langauge model:

In ELMO, there are multi hidden layers, at least 2.  because word embedding is computed on character cnn, we can find relation regardless of context, which is robust for OOV.
For example, we can find relation between dog and doggy. 
However, ELMO's biLM differs from RNN whereas forward and backward hidden layers are concatenated before sending it as input to layer in RNN for training.
In Elomo biLM, forward and backward hidden layer are sent to next layer independly as input and concatenated after training.    


To be continue,
