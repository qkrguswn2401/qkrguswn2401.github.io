---
title: "COMPRESSIVE TRANSFORMERS FOR LONG-RANGE SEQUENCE MODELLING"
date: 2022-02-28 08:26:28 -0400
categories: Paper Review
---
COMPRESSIVE TRANSFORMERS FOR LONG-RANGE SEQUENCE MODELLING


Abstract:
  BLANC (BLock AttentioN for Context prediction) is based on two ideas.
    context prediction, block-attention method.
    outperformed SOTA QA models; performe better when # of answer text occurences occurs more frequently.
    trained on SQuAD and inferred on HotpotQA and show that BLANC outperformed all baseline model in zero-shot setting

Introduction:
  While QA models are designed to select answer-spans in relevant context from given passage, they sometimes result in predicting the correct answer but in contexts that are irrelvant.  
  Context prediction is an auxilary task and propsoe a block attention method, BLANC that forces the QA model to predcit the context.
  context prediction taks to predict soft labels, which are generated from given answer spans.  The block attention method effectively calculates the probability of each word in a passage.
  
 
 
  

Models:
  two novel ideas:
    soft-labeling method for context prediction
    blcok attention method that predicts the soft-labels.
  two important functons
    1.  Calculating the probability that a word in a passage belongs to the context
    2.  enabling the probability to reflect spatial locality between adjacent words.
    
  Soft-labeling for latent context
    Assumption: words near an answer-span are likely to be included in the context of a given question.  probability of words belong to the context, which is used as a soft-label for the auxiliary context prediction task.  Hypothesis: words in an answer-span are included in the context and make the probability of adjacent words decrease wit ha specific ratio as the distance between answer-span and a word increases.
    
  Block Attention
    Calculate segment embedding to predict soft-label, and localizes teh correct index of an answer-span with passage segment embedding.
    embedding spatial locality of passage segments to block attention models with following steps
      1. predicting start and end indices of context
      2. calculating passage segment with cumulaitve distribution of start and end tokens.
    
![image](https://user-images.githubusercontent.com/36841216/132169723-f0a59dd0-ebbc-4eb9-9b5f-e55fd55b50c8.png)    
![image](https://user-images.githubusercontent.com/36841216/132169669-b06fd2dc-3824-442b-bf22-eb5d0c09b42d.png)

    
