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

By doing this we do not know the actual weather sequences (hidden sequences), we need to compute probability over all possible weather sequences.
![image](https://user-images.githubusercontent.com/36841216/112827314-221bb700-90c9-11eb-9af8-6aa68378b0ee.png)

computes joint probability of being in a particualr weather sequence and generate a particualr sequence.
![image](https://user-images.githubusercontent.com/36841216/112827340-2c3db580-90c9-11eb-8e3c-29bdc3ce4c89.png)

Computing the total probability of the observations just by summing over all possibel hidden state sequence.
![image](https://user-images.githubusercontent.com/36841216/112827684-a3734980-90c9-11eb-890a-75f638fbec29.png)

For this cass, 3(3 1 3) observables T, 2 hidden (Hot cold) states N, there are 2^3 possible hidden sequences.  By adding all of these sequences, we get the total probability of the observation.
![image](https://user-images.githubusercontent.com/36841216/112829050-863f7a80-90cb-11eb-9cb5-74330c2b4a55.png)

![image](https://user-images.githubusercontent.com/36841216/112827900-efbe8980-90c9-11eb-9a92-1593d945affc.png)

When N and T get real big, computation costs way too much, too much running time

Forward algorithm is proposed.  It is like DP programming, which computes teh obseravtion probability by summing over the probablites of all possible hidden state paths that could generate the obseravtion sequence.  

Visualization of Forward Algorithm:
![image](https://user-images.githubusercontent.com/36841216/112829527-344b2480-90cc-11eb-8363-917d1c63cfe9.png)

by using this algorithm, ![image](https://user-images.githubusercontent.com/36841216/112829899-c3583c80-90cc-11eb-8496-63a08d87a63b.png)
where ![image](https://user-images.githubusercontent.com/36841216/112829916-cb17e100-90cc-11eb-9841-0b63319df925.png).

alpha_1(1) = P(C|Start)*P(3|C) = 0.02
alpha_1(2) = P(H|Start)*P(3|H) = 0.32 
alpha_2(1) = alpha_1(1)*P(C|C)*P(1|C) + alpha_1(2)*P(C|H)*P(1|C) = 0.069  

The point is we store those alpha values somewhere, calculate alphas (no unncessary calcuation).

![image](https://user-images.githubusercontent.com/36841216/112831241-a1f85000-90ce-11eb-9d4f-89eccae1446a.png)
what this equation means is that summing over forward probability at the last sequences ends up being equilvalent to likelihood.



2. Decoding:Viterbi Algorithm
Decoding task: taks of determining which sequence of variables is the underlying source of some sequence of observation.
![image](https://user-images.githubusercontent.com/36841216/112831753-5db97f80-90cf-11eb-93ac-4dfe65fe80e7.png)
Ex: Given seuquence 3 1 3, find out best hidden weather state for that seuqence.
Viterbi Algorithm is like DP programming (minimum edit distance)

What is Viterbi Algorithm?
It does have somewhat like forward algorithm part but it has backtrace.
![image](https://user-images.githubusercontent.com/36841216/112835758-ac1d4d00-90d4-11eb-8739-048ac03d4f6a.png)
Unlike forward algorith, it takes the one of max from inputs.  

![image](https://user-images.githubusercontent.com/36841216/112835722-9f005e00-90d4-11eb-84ec-a7d3718bed58.png)

