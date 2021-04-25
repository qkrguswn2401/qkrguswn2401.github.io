---
title: "Transformer-XL"
date: 2021-04-25 08:26:28 -0400
categories: Paper Review
---
Problems with vanilla transfomer: transformers are theoratically capable of learning long-term dependency, have issues with limited-length.  
<br/> Transfomer XL architecture is capable of learning depedency beyeond a fixed length with no distrupting tempoeral coherence.  
<br/> Transformer XL is composed of segment-level recurrence mechanism and novel positional encoding scheme.  These methods helps captuing longer-term dependency and also resolves the context fragmentation problem.
<br/>fixed length issue:  longer sequence is truncated to the fixed length.
<br/>Context-fragmentation:  Model can not capture longer dependency beyond fixed-length segments, meaning whole corpus is split into smaller segment.  context is not shared among these segments.
models does not look at previous segment.


Related Works:
<br/> Truncated BPTT: hidden state from the previous batch are passed forward to the current batch.
<br/> Character Transformer Model: 
In vaninllla transforer, given a sequence, its job is to predcit next word.  loss is calculated at the end of the token.
![image](https://user-images.githubusercontent.com/36841216/115982709-180dab00-a5d8-11eb-852e-beb95bc4f09f.png)
for faster convergence, loss is calculated at each time step.

two main method: 1. segment-level recurrence, 2. relative positional embedding
For training
1. semgent-level recurrence:
  - by using one segment, it predict next new segment at once.   By doing so, model looks at previous segments and predict next word by taking more context into account.
  - previous gradient are cached and concated to the next segment.  
  - ![image](https://user-images.githubusercontent.com/36841216/115982804-bc8fed00-a5d8-11eb-8379-caf72ac3a9af.png)
2. positional embedding:
  - how to deal with positional embedding of old segments and new semgments's indices?  same index occurs in different sequences.
  - Instead of using absolute positional embedding, it is enough to know relative distance between key vector and query vector.
  - ![image](https://user-images.githubusercontent.com/36841216/115982923-4dff5f00-a5d9-11eb-9551-9baef9800ef1.png)


For Evaluation
   - vanilla transformer takes a segment to make only one prediction at the last position, expensive.
   - ![image](https://user-images.githubusercontent.com/36841216/115982971-93bc2780-a5d9-11eb-906e-c678474ef7d9.png)
   - For transformer XL, because we use hidden state from previous segments, we predict not one token but one segment.  less calculation
   - 
