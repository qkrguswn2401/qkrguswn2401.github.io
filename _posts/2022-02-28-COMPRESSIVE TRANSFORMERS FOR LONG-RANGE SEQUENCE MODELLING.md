---
title: "COMPRESSIVE TRANSFORMERS FOR LONG-RANGE SEQUENCE MODELLING"
date: 2022-02-28 08:26:28 -0400
categories: Paper Review
---
COMPRESSIVE TRANSFORMERS FOR LONG-RANGE SEQUENCE MODELLING


Abstract: An attentive sequence model that compresses past memories for long-rage sequence learning.  

Introduction:
  Transformer stores the hidden activiation of every time-step, and integrates this information using an attention operator.  Drawback is the computation cost of attenting every time-step in storing everything and storage cost.  Sparse attention does not solve storage problems.  This paper propooses the notion of compactly representing the past by simple dense linear-algebra components, which reduce space and computation costs.  
  Compressive Transformer maps the past hidden activations to a smaller set of compressed representations (compressive memories).  This model uses the same attention mechanism as the transformer over its set of memories and compressed memories.  
  
Related Works
  There has been attempts to replace attention operation with others.  Wu (2019) proposes an convolution-like operator that runs in linear time, which exceeds the performance of the quadratic-time self-attention.  Dai (2019) proposes the TransformerXl, which keeps past information by caching in memory;  He also proposes an novel relative positional embedding.  Child (2019) proposes Sparse Transformer, which uses fixed sparse attenntion masks to attention to roughly sqrt(n) location in memory.  This method requires keeping all memories around during training.  Sukhbaater (2019) proposes use of dynamic attention; different attention heads learn to ahve shorter or longer spans of attention.  
  
  
![image](https://user-images.githubusercontent.com/36841216/156104732-3ca62a91-ea0d-4b01-864a-733ae0dee890.png)
  Model
    Compressive Transformer, a long-range sequence model which compacts past activation into a compressed memory.  Idea of compressive transformer is built on TransformerXL, which maintains a memory of past activiations at each layer to preserve a longer history of context.  The difference between transformerXL and compressive transformer is that TransforemrXL discards the past activations when they are oldwhereas comporessive transformer compresses the old memories and stores them as compressed memory.  
    ![image](https://user-images.githubusercontent.com/36841216/156108657-a1f86e69-e94a-4a9a-bdf7-0336272e1a3c.png)
  Model.description:   n<sub>m</sub>:respective memory , n<sub>cm</sub>: compressive memory, d: hidden size, c: compression rate ( higher value indicates more coarse-grained compressed memory)
      As the model moves to the next sequence, its hidden activations are pushed into a fixed-size FIFO memory.  Old hidden activation in memory are evicted.  compression operations are applied mapping,  the old memoreis to compressed memories, which are stored in a secondary FIFO compressed memory.  
![image](https://user-images.githubusercontent.com/36841216/156108763-11c49de8-99a5-4462-88fa-289e21d6ef2e.png)

    Model.compressipon functions and losses
      (1) max/mean pooling, (2) 1D convolutions (3) dilated convolutions (4) most-used: most-used are preserved.
      Auto-encoding losses: reconstructs the original memories from compressed memories ||old_mem - new_cm||<sub>2</sub>
      attention-reconsctruction: reconsctructs the content-based attention over memory, with content-based attention over the compressed memories.
      Temporal range is increased.  
        TransforemrXL: l x n with O(n<sup>2</sup><sub>s</sub> + n<sub>s</sub>n)
        this model: l x (n<sub>m</sub> + c *n<sub>c</sub><sub>m</sub>) with O(n<sup>2</sup><sub>s</sub> + n<sub>s</sub>n( n<sub>m</sub> + n<sub>cm</sub> ))
    
    
    
    
