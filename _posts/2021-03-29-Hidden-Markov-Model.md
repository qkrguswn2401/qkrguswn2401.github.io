---
title: "Hidden Markove Model (HMM)"
date: 2021-03-29 08:26:28 -0400
categories: Algorithm
---

HMM is built on Markov Chain.  Markkov Chain is sequences of states that have path to each other with prbability of going to some state.  Past state is does not affecet when predicting what comes next; only current state matters.  Ex)  predict tomorrow's weather based on today, not yesterday.  
Markov chain is useful when evetns are observable.
Markov Assumption: ![image](https://user-images.githubusercontent.com/36841216/112824671-cbf94480-90c5-11eb-9143-a580e6245d18.png)

Example of Markov Chain:  ![image](https://user-images.githubusercontent.com/36841216/112824769-e501f580-90c5-11eb-9704-8ab74cea9b68.png)

Hidden Markov Chain: both observable events (words) and unobservable (POS)

First order hiddne Markov model is based on two simplifying assumptions:
![image](https://user-images.githubusercontent.com/36841216/112825096-4de96d80-90c6-11eb-8834-796a43ad6173.png)
Explaination: only current state affect next state.

![image](https://user-images.githubusercontent.com/36841216/112825105-52158b00-90c6-11eb-8a78-bbf72498b9c4.png)
Explaination: probability of an output observation depends only on the state produced the observation; output is produced by observation at same time step.

Example:  predicting weather by consumption of ice-cream.
![image](https://user-images.githubusercontent.com/36841216/112826035-7160e800-90c7-11eb-8505-7da72661f180.png)

Markov chanin must be characterized by threee fundamental problem by Rabiner
![image](https://user-images.githubusercontent.com/36841216/112825612-f39cdc80-90c6-11eb-8626-c1e40d553d3f.png)

1. Likelihood:  first problem is to compute the likelihood of a particular observation sequence. 
Given observation, the likehood of the obsevation sequence is  ![image](https://user-images.githubusercontent.com/36841216/112826908-9570f900-90c8-11eb-9fdf-02cee651d0c4.png)
Givne sequence like 3 1 3 when determining the probability of an ice,  ![image](https://user-images.githubusercontent.com/36841216/112827037-c2251080-90c8-11eb-81af-ee8f8856d3a9.png)
![image](https://user-images.githubusercontent.com/36841216/112827061-ce10d280-90c8-11eb-8ad3-4115e5c39aa7.png)

By doing this we do not know the actual weather sequences (hidden sequences), we need to compute probability over all possible weather sequences, 
![image](https://user-images.githubusercontent.com/36841216/112827314-221bb700-90c9-11eb-9af8-6aa68378b0ee.png)
computes joint probability of being in a particualr weather sequence and generate a particualr sequence.
![image](https://user-images.githubusercontent.com/36841216/112827340-2c3db580-90c9-11eb-8e3c-29bdc3ce4c89.png)
