---
title: "What are soundex and mra"
date: 2021-02-19 08:26:28 -0400
categories: Algorithm Must-Knpw
---

Application of this algorithm is to find similarity of texts.

What is Phoneme: distinct unit of sound in specified langauge that distinguish one wrod from another ex) m and b as in mat and bat
What is homophome: each of two or more words that have the same pronunciation but different meaning.
Soundex: a phonetic algorithm, algorithm for indexing of words by theire pronounciation (useful in English).  
Purpose of this algorithm is for homophones to be encoded to the same representation even if they are spelled diffrently.

Match Rating Approach: Phonetic Algorithm for indexation and comparison of homophonous names.
Main mechanism is to find simialrity comparison by calculating the number of unmathced characters by comparing the strings from left to right and then right to left, and removing identical characters.  
It has encoding and comparison rules. 
