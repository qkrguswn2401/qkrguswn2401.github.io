---
title: "Bridging the Gap Between Relevance Matching and Semantic Matching"
date: 2021-06-28 08:26:28 -0400
categories: Paper Review Informatio-Retrieval
---

  IR: relevance matching
  semantic matching: to measure the semantic distance between two pieces of short texts.
  Hybrud Co-Attention Network (HCAN) is introduced to bridge the gap between IR and SM.
    Comprised of 
    Hybrid encoder module (Convnet-based and LSTM-based encoder)
    relevance matching module measures the soft term matches with importance weighting at multiple granularity.
    sematnic matching module with co-attention mechanisms that capture context-aware semantic relatednes.   
   
  Hybrid encoder module exploits three characteristics (deep, wide, contexual) to obtain sentence representation.
  relevance matching module measures the weight between pairs of texts from word-level, phrase level, sentence level.
  semantic matching module with co-attention mechanism applied at each encoder enable context-aware representation learning at multiple semantic level.  
   
![image](https://user-images.githubusercontent.com/36841216/131962147-afa11bc6-e421-4d6a-b5f2-983f3c6de2e6.png)
Figure 1: Architecture of the HCAN model


Hybrid Encoder: three encoders to extract representation
  Deep Encoder: multiple hierarchical convolution layers to obtain higher-level n-gram representation
  Wide Encoder: multiple convolutional layers in parallel with different kernel window size to obtain n-gram representation
  Contextual Encoder: unlike both wide and deep encoder, Contextual Encoder uses LSTM to extract long-range convolutional features.  obtains long-distance contextual representation for each token.  
  
Relevance Matching: captures key-word matching by calculating relevance score between query and context at each encoder layer by multiplying query and context representation.
![image](https://user-images.githubusercontent.com/36841216/132157046-86daa567-47aa-4523-883a-863d9a803784.png)
  query and context layers share same encoder layers, similar queries will be placed nearby at higher embedding space.  

Semantic Matching: captures matching via co-attention method  on intermeidate and context representations.
  Calculate bilinear attention over query and context representations obtained at intermediate encoder layers.
  Calculate attention, context-to-query and query-to-context
  
Final Classification:
  concatenate semantic matching and relevance matching for final classification.
  
