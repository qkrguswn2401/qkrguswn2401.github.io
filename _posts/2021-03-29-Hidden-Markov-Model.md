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