---
title: "Transformer-XL"
date: 2021-04-25 08:26:28 -0400
categories: Paper Review
---
Abstract

Problems with vanilla transfomer: transformers are only capable of learning long-term dependency, have issues with limited-length context.  
<br/> Transfomer XL architecture is capable of learning depedency beyeond a fixed length with no distrupting tempoeral coherence. 
<br/> Transformer XL is composed of segment-level recurrence mechanism and novel positional encoding scheme.  These methods helps captuing longer-term dependency and also resolves the context fragmentation problem.
<br/> fixed length issue:  longer sequence is truncated to the fixed length.
<br/> Context-fragmentation:  Model can not capture longer dependency beyond fixed-length segments, meaning whole corpus is split into smaller segment.  context is not shared among these segments.
models does not look at previous segment.

Introduction
<br/> Transformers with self-attention have been proposed that would ease optimization and enable the learning of long-term dependency.  Auxillary losses helps train deeper neural networks (LM) but these networks segments context into a few hundreds characters without any information folowing from segments to segments, thus model does not capture any long term dependency beyond fixed contexts.  These LM faces context fragmentation; longers contexts are divided into segments.  Trasformer-XL is proposed to deal with those issues; Transformer-XL reuses hidden states obtained in previous segments.   


Related Works:
<br/> Truncated BPTT: hidden state from the previous batch are passed forward to the current batch.
<br/> Character Transformer Model: 
In vaninllla transforer, given a sequence, its job is to predcit next word.  loss is calculated at the end of the token.
![image](https://user-images.githubusercontent.com/36841216/115982709-180dab00-a5d8-11eb-852e-beb95bc4f09f.png)
for faster convergence, loss is calculated at each time step.

Models: 
two main method: 1. Vanilla Transformer Language Model 2. segment-level recurrence, 3. relative positional embedding
For training
1.  Vanilla Transformer Language Model:
  training:
    - split entire courpus into shorter segments and train the model within each segments, not taking contextual information from previous segments.  Information never flows from segments.  
    - self-attention mechanism is less affected by vanishing gradients.
  Inference:
    - it makes one prediciton at a time.  At next next, the segment is shfited to the right by only one position; new process has to start all over.   
    
2. semgent-level recurrence:
  - During training, hidden state from previous state is fixed and cahced to be reused as an extended context when model is onto new segment (exploiting information in history, ability to model longer-term dependency.  
  - previous gradient are cached and concated to the next segment.  
  - recurrent scheme is significantly faster for evaluation.
  - 
  - ![image](https://user-images.githubusercontent.com/36841216/115982804-bc8fed00-a5d8-11eb-8379-caf72ac3a9af.png)
3. positional embedding:
  - how to deal with positional embedding of old segments and new semgments's indices?  same index occurs in different sequences.
  - Instead of using absolute positional embedding, it is enough to know relative distance between key vector and query vector.
  - ![image](https://user-images.githubusercontent.com/36841216/115982923-4dff5f00-a5d9-11eb-9551-9baef9800ef1.png)


For Evaluation
   - vanilla transformer takes a segment to make only one prediction at the last position, expensive.
   - ![image](https://user-images.githubusercontent.com/36841216/115982971-93bc2780-a5d9-11eb-906e-c678474ef7d9.png)
   - For transformer XL, because we use hidden state from previous segments, we predict not one token but one segment.  less calculation
   - 
