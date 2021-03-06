---
title: "Hidden Markove Model (HMM)"
date: 2021-03-29 08:26:28 -0400
categories: Algorithm
---

HMM is built on Markov Chain.  Markkov Chain is sequences of states that have path to each other with prbability of going to some state.  Past state is does not affecet when predicting what comes next; only current state matters.  Ex)  predict tomorrow's weather based on today, not yesterday.  
Markov chain is useful when evetns are observable.
Markov Assumption: ![image](https://user-images.githubusercontent.com/36841216/112824671-cbf94480-90c5-11eb-9143-a580e6245d18.png)

<br/>Example of Markov Chain:  ![image](https://user-images.githubusercontent.com/36841216/112824769-e501f580-90c5-11eb-9704-8ab74cea9b68.png)

Hidden Markov Chain: both observable events (words) and unobservable (POS)

<br/>First order hidden Markov model is based on assumptions:
![image](https://user-images.githubusercontent.com/36841216/112825096-4de96d80-90c6-11eb-8834-796a43ad6173.png)
Explaination: only current state affect next state.
<br/>
![image](https://user-images.githubusercontent.com/36841216/112825105-52158b00-90c6-11eb-8a78-bbf72498b9c4.png)
Explaination: probability of an output observation, o depends only on the state produced the observation q

Example:  predicting weather by consumption of ice-cream.
![image](https://user-images.githubusercontent.com/36841216/112826035-7160e800-90c7-11eb-8505-7da72661f180.png)

Markov chanin must be characterized by threee fundamental problem by Rabiner
![image](https://user-images.githubusercontent.com/36841216/112825612-f39cdc80-90c6-11eb-8626-c1e40d553d3f.png)

Part 1. Likelihood:  first problem is to compute the likelihood of a particular observation sequence. 
Given observation, the likehood of the obsevation sequence is  ![image](https://user-images.githubusercontent.com/36841216/112826908-9570f900-90c8-11eb-9fdf-02cee651d0c4.png)
Given sequence like 3 1 3 (hidden sequence), one possible hidden sequence of hot cold cold when calculating forward probability
![image](https://user-images.githubusercontent.com/36841216/112827037-c2251080-90c8-11eb-81af-ee8f8856d3a9.png)
![image](https://user-images.githubusercontent.com/36841216/112827061-ce10d280-90c8-11eb-8ad3-4115e5c39aa7.png)

we must compute the probability of ice-cream and event 3 1 3 instead by summing over all possible weather sequences, weighted by their probability.
![image](https://user-images.githubusercontent.com/36841216/112827314-221bb700-90c9-11eb-9af8-6aa68378b0ee.png)

computing joint probability of being in a particualr weather sequence and generate a particualr sequence.
![image](https://user-images.githubusercontent.com/36841216/112827340-2c3db580-90c9-11eb-8e3c-29bdc3ce4c89.png)

Computing the total probability of the observations just by summing over all possibel hidden state sequence.
![image](https://user-images.githubusercontent.com/36841216/112827684-a3734980-90c9-11eb-890a-75f638fbec29.png)

For this cass, 3(3 1 3) observables T, 2 hidden (Hot cold) states N, there are 2^3 possible hidden sequences.  By adding all of these sequences, we get the total probability of the observation.
![image](https://user-images.githubusercontent.com/36841216/112829050-863f7a80-90cb-11eb-9cb5-74330c2b4a55.png)

![image](https://user-images.githubusercontent.com/36841216/112827900-efbe8980-90c9-11eb-9a92-1593d945affc.png)

When N and T get real big, computation costs way too much, too much running time

Forward algorithm is proposed.  It is like DP programming, which computes the obseravtion probability by summing over the probablites of all possible hidden state paths that could generate the obseravtion sequence.  

Visualization of Forward Algorithm:
![image](https://user-images.githubusercontent.com/36841216/112829527-344b2480-90cc-11eb-8363-917d1c63cfe9.png)

by using this algorithm, ![image](https://user-images.githubusercontent.com/36841216/112829899-c3583c80-90cc-11eb-8496-63a08d87a63b.png)

alpha_1(1) = P(C|Start)*P(3|C) = 0.02
alpha_1(2) = P(H|Start)*P(3|H) = 0.32 
alpha_2(1) = alpha_1(1)*P(C|C)*P(1|C) + alpha_1(2)*P(C|H)*P(1|C) = 0.069  

The point is we store those alpha values somewhere, calculate alphas (no unncessary calcuation).

![image](https://user-images.githubusercontent.com/36841216/112831241-a1f85000-90ce-11eb-9d4f-89eccae1446a.png)
what this equation means is that summing over forward probability at the last sequences ends up being equilvalent to likelihood.



Part 2. Decoding:Viterbi Algorithm
Decoding task: task of determining which sequence of variables is the underlying source of some sequence of observation.
![image](https://user-images.githubusercontent.com/36841216/112831753-5db97f80-90cf-11eb-93ac-4dfe65fe80e7.png)
Ex: Given seuquence 3 1 3, find out best hidden weather state for that seuqence.
Viterbi Algorithm is like DP programming (minimum edit distance)

What is Viterbi Algorithm?
It behaves somewhat like forward algorithm but it has backtrace part
![image](https://user-images.githubusercontent.com/36841216/112835758-ac1d4d00-90d4-11eb-8739-048ac03d4f6a.png)
nlike forward algorith, it takes the max of inputs.  
Viterbi algorithm has pointer becasue it has to produce probability and most likely state sequence.  By using backsequence, most probable squences are kept.
![image](https://user-images.githubusercontent.com/36841216/112835722-9f005e00-90d4-11eb-84ec-a7d3718bed58.png)

Example of Viterbi Algorithm: 여기서는 최소하는 것을 찾아서 max 대신 min을 사용
![image](https://user-images.githubusercontent.com/36841216/112836069-12a26b00-90d5-11eb-81a6-c45ee865a2d3.png)

![image](https://user-images.githubusercontent.com/36841216/112836111-1e8e2d00-90d5-11eb-9b8d-9006aa89c7a5.png)
![image](https://user-images.githubusercontent.com/36841216/112836585-c277d880-90d5-11eb-8fe2-600b1372c55e.png)
위와 같은 식으로 각 state당 cost를 구함.  time step = 2 and S_1,1일떄, assembly line 1을 유지하는게 더 cost 가 낮음.
l_2[1] = 1

![image](https://user-images.githubusercontent.com/36841216/112836896-24384280-90d6-11eb-930b-34cd379eb1fb.png)
위와 같이 cost 낮은 assembly을 저장.

각 state에 min cost와 최적 경로를 어디간에 저장
![image](https://user-images.githubusercontent.com/36841216/112837187-87c27000-90d6-11eb-994a-cdd24cc43449.png)
![image](https://user-images.githubusercontent.com/36841216/112837201-8d1fba80-90d6-11eb-9813-aebfb4a9d120.png)
![VA-MOVIE](https://user-images.githubusercontent.com/36841216/112837582-08816c00-90d7-11eb-9363-b5d252b019c6.GIF)
at the end of stage.
![image](https://user-images.githubusercontent.com/36841216/112837712-2ea70c00-90d7-11eb-8e6b-db8daddf4017.png)

Assume most probable state is at theta_0.  
theta_0, theta_2, theta_2, theta_1, theta_0, theta_1 

Part 3: HMM training: the forward-backward algorithm (Algorithm used for training for HMM, known as Baum-Welch or specail cas for Expectation-maximization algorithm (EM))

This algorithm lets us train both trasition and emission probabilities of the HMM.
EM algorithm is an iterative algorithm that tries to compute better estimate for each iteration and improves probability as it learns.
Remember the equation for finding forward and backward probability
![image](https://user-images.githubusercontent.com/36841216/112934363-93f11080-915c-11eb-80c4-3f0a6fb2f070.png)

What forward means: 
P =  summing over (previous forward probaility * probablity of going from i to j state * probability of finding observation_t at j state).
What backward means: 
P = summing over(next backward probabiltiy * probability of going from i to j state probability of finding Obseravtion_t+1 at j state ).
Example of Forward and Backward algorithm
![image](https://user-images.githubusercontent.com/36841216/112935558-f814d400-915e-11eb-8fb3-f56a06a79bcd.png)
![image](https://user-images.githubusercontent.com/36841216/112935695-3a3e1580-915f-11eb-9dab-2c94299a0210.png)

We can see that mulitying forward and backward probability at same time step literally calcualte all of possible paths that go to that state from front and back. Here is what that means.
![image](https://user-images.githubusercontent.com/36841216/112935901-ae78b900-915f-11eb-896b-648f962aaf86.png)
<br/>summing over mulication of forwad and backward probabilty is equal to likelihood.

Definition: ![image](https://user-images.githubusercontent.com/36841216/112951967-e6d7c180-9176-11eb-9be6-f95af75e47e7.png)
<br/>![image](https://user-images.githubusercontent.com/36841216/112952133-21d9f500-9177-11eb-80e0-af7b661042e4.png)
<br/>X_t = probability of being in state i at time t and state j at time t+1, given observation and model.


<br/>Bayes's theorem:  ![image](https://user-images.githubusercontent.com/36841216/112950981-d7a44400-9175-11eb-9b03-0cf257e86d2f.png)
<br/>Probability of observation:![image](https://user-images.githubusercontent.com/36841216/112952343-58b00b00-9177-11eb-81df-2d5a61ecc9ab.png)
<br/>Using Baye's theorem and probability of observation, we can reformulze xi_t as 
<br/>![image](https://user-images.githubusercontent.com/36841216/112952479-7ed5ab00-9177-11eb-91cb-faf5b8204abc.png)
formula for computing transition probability.

<br/>predicted transition probability = (expected number of transition from state i to state j)/(expected number of transitions from state i)
![image](https://user-images.githubusercontent.com/36841216/112954802-b6dded80-9179-11eb-9399-bd1363a9e53a.png)

![image](https://user-images.githubusercontent.com/36841216/112956733-b7778380-917b-11eb-8b8d-4e09bbbdf56a.png)

<br/> what numberator means: summation over transition probability from ith state to jth state.
<br/> what denominator means: summation over all paths of transition probabilities that could possibly go from ith state.
<br/> Why sigma? regardless of time sequence, there exists ith state and transition probability. why? T-1: transition probability=100%, right before T. 
<br/>Red dotted: denominataor.
<br/>black dotted: numerator.

<br/> we also need a formual for computing observation probability.
![image](https://user-images.githubusercontent.com/36841216/112955334-45eb0580-917a-11eb-908a-75df8d5cf345.png)
We need to know the probability of being in state j at time, gamma.
![image](https://user-images.githubusercontent.com/36841216/112955942-e4776680-917a-11eb-8f13-ec632e3cd371.png)

<br/> emission probalility of seeing v_k given at j state is ![image](https://user-images.githubusercontent.com/36841216/112956191-27d1d500-917b-11eb-8663-6ab8fb221847.png)
<br/> why sigma? emission probability has nothing to do with time step.  
<br/> what numberator means: at state state, probability of v_k given o_t.
<br/> what denominator means: probability of seeing ith state.

<br/> EM-Algorithm  
<br/> E-step: fixed model paremter lambda (transition probability A and emission probability B), update forward probability and backward probability based on observation.
<br/> M-Step: update paramters A,B based xi and gamma calucatd from E step
<br/> pesudo code
![image](https://user-images.githubusercontent.com/36841216/112960364-4fc33780-917f-11eb-8b18-c60836b09344.png)


