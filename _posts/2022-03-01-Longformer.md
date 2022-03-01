---
title: "Longformer: The Long-Document Transformer"
date: 2022-02-28 08:26:28 -0400
categories: Paper Review
---
Longformer: The Long-Document Transformer

Abstract:
  Transformer-based models are unable to process long sequences due to self-attention operation (not scalable).  Longformer overcomes scalability issue by introducing attention mechanism which increases linearly with sequence length.  

Introduction:
  Transformer has been successful in NLP due to self-attention, which enables the network to capture global contextual information from the entire sequence.  

Model
  original transformer has self-attention componenet with O(n<sup>2</sup>) time and memory complexity where n is the input sequence length.  To address this issue, sparsifying the full self-attention matrix according to an attention pattern is proposed.  
  
  Attention pattern: 
  Employs a fixed-size window atention surrounding each token.  Given a fixed window size w, each token attends to w/2 tokens on each side.  Computation complexity of this pattern is O(n x w), which scales linearly with input sequence.  Receptive field at top layer l x w has has access to all input locations.  
  
  Dilated Sliding Window:  
  To increase the receptive field without increasing computation, sliding window can be dilated where sliding window has gaps of size dilation d.  multi-head with dilation configurations improve performance by allowing some heads without dilation to focus on local whereas with dilation focus on longer context.
  
  Globlal Attention: 
  Attention operation is symmetric.  Windowed and dilated attention are not flexible enough to learn task-specific representation.  A token with a global attention attends to all tokens across the sequence, and all tokens in the sequence attend to it.  
  Linear Projections for Global attention:
  two set of projections are used:  sliding window and global attention.  these two projection provide flexibility to model.
  
  
![image](https://user-images.githubusercontent.com/36841216/156118600-8522e35e-9531-4fc5-9eee-023a4335ba31.png)
