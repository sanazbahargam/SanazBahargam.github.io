---
title: 'Edge Probing'
date: 2020-11-06
permalink: /posts/2020/11/EdgeProbing/
tags:
  - NLP
  - Transformers
---

In the past couple of years, Transformers has acheived state of art results in a variety of natural language tasks. In order to better understand Transformers and what they are learning in practice, researchers have done layer-wise analysis of BERT’s hidden states to understand what BERT is learning in each layer.  They examine the hidden states between encoder layers directly and use those hidden states in a linear layer + softmax to predict what kind of information in encoded in each hidden state. 
In this post, I'm going to explain the main idea behind probing. 



References
  - [WHAT DO YOU LEARN FROM CONTEXT? PROBING FOR SENTENCE STRUCTURE IN CONTEXTUALIZED WORD REPRESENTATIONS](https://arxiv.org/pdf/1905.06316.pdf)
  - [How Does BERT Answer Questions? A Layer-Wise Analysis of Transformer Representations](https://arxiv.org/pdf/1909.04925v1.pdf)
  - [A Structural Probe for Finding Syntax in Word Representations](https://nlp.stanford.edu/pubs/hewitt2019structural.pdf)
  - [Finding Syntax with Structural Probes](https://nlp.stanford.edu//~johnhew//structural-probe.html?utm_source=quora&utm_medium=referral#the-structural-probe)

